# Core Motion Integration (Accelerometer, Gyroscope)

Cocos2D does not have built-in support for accelerometer and gyroscope. These input events are provided by the *Core Motion* framework.

The main difference to input events supported by CCResponder is that Core Motion events will be sent to one particular node, typically the scene. 

To use Core Motion you follow these simple steps:

- Create an instance of [`CMMotionManager`]( and assign it to a class property or ivar
- Set the update interval
- start accelerometer or gyroscope updates
- in the update: method, read the motion manager's acceleration/gyroscope property for updated values

<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
On the iOS Simulator Core Motion returns zero for all motion values. You have to test Core Motion functionality on an actual device.
</td></tr></table>

## Creating an instance of CMMotionManager

You will need to assign the CMMotionManager instance to a class property because you'll need to be able to access updated values (typically in the update: method) and eventually you'll have to stop updates as well. A minimal setup requires this code:

	// Objective-C
	@implementation MainScene
	{
	    CMMotionManager* _motionManager;
	}

	-(id) init {
		self = [super init];
		if (self) {
			_motionManager = [CMMotionManager new];
		}
		return self;
	}

	// Swift
	class MainScene: CCNode {
    	let _motionManager = CMMotionManager()
	}
	
<table border="0"><tr><td width="48px" bgcolor="#ffffc0"><strong>Note</strong></td><td bgcolor="#ffffc0">
You should not register multiple nodes to receive Core Motion events at the same time. Instead, make the motion manager property public to access it from other classes.
</td></tr></table>

## Starting and Stopping Accelerometer Updates

It's best to set the accelerometer update interval to the same rate as the display refresh rate, which is stored in the CCDirector property animationInterval and defaults to `1.0 / 60.0` (60 Hz). Then start accelerometer updates. You would normally do this in one of the initialization functions, be it `init`, `didLoadFromCCB` or `onEnter`.

	// Objective-C
    _motionManager.accelerometerUpdateInterval = [CCDirector sharedDirector].animationInterval;
    [_motionManager startAccelerometerUpdates];

	// Swift
    _motionManager.accelerometerUpdateInterval = CCDirector.sharedDirector().animationInterval
    _motionManager.startAccelerometerUpdates()

To stop accelerometer updates at a later time you just need to call:

	// Objective-C
    [_motionManager stopAccelerometerUpdates];

	// Swift
    _motionManager.stopAccelerometerUpdates()


## Obtaining Accelerometer Values

To receive accelerometer updates you simply check periodically for new values. Typically you'll want to use the update: method for that.

	// Objective-C
	-(void) update:(CCTime)delta {
	    CMAcceleration acceleration = _motionManager.accelerometerData.acceleration;
    	NSLog(@"accel x: %f, y: %f, z: %f", acceleration.x, acceleration.y, acceleration.z);
	}

	// Swift
    override func update(delta: CCTime) {
        if let accelData = _motionManager.accelerometerData {
            let acceleration : CMAcceleration = accelData.acceleration
            NSLog("accel x: %f, y: %f, z: %f", acceleration.x, acceleration.y, acceleration.z)
        }
    }

Acceleration values are provided via a [CMAccelerometerData](https://developer.apple.com/library/ios/documentation/CoreMotion/Reference/CMAccelerometerData_Class/index.html) object (which may be nil) which contains a [CMAcceleration property](https://developer.apple.com/library/ios/documentation/CoreMotion/Reference/CMAccelerometerData_Class/index.html#//apple_ref/c/tdef/CMAcceleration) containing the actual raw acceleration values.

## Filtering Accelerometer Values

The raw accelerometer values are typically unsuitable for controlling a game or a game character. It reacts highly sensitive to device chances which makes the resulting motion unsteady, jumpy. The solution is a so-called *low-pass filter* which is easy to implement.

You need a property/ivar in the class for each of the x,y,z components you want to filter. They ought to be of type `double`/`Double`. In this case they are called `accelerationX`, `accelerationY` and `accelerationZ`. Of course you can omit the calculations for the axis you don't need, ie in 2D games you'll mainly just need to filter X and Y components.

	// Objective-C
    const double kFilterPercent = 0.1;
    accelerationX = (acceleration.x * kFilterPercent) + (accelerationX * (1.0 - kFilterPercent));
    accelerationY = (acceleration.y * kFilterPercent) + (accelerationY * (1.0 - kFilterPercent));
    accelerationZ = (acceleration.z * kFilterPercent) + (accelerationZ * (1.0 - kFilterPercent));
    NSLog(@"filtered accel x: %f, y: %f, z: %f", accelerationX, accelerationY, accelerationZ);

	// Swift
    let kFilterPercent = 0.1;
    accelerationX = (acceleration.x * kFilterPercent) + (accelerationX * (1.0 - kFilterPercent));
    accelerationY = (acceleration.y * kFilterPercent) + (accelerationY * (1.0 - kFilterPercent));
    accelerationZ = (acceleration.z * kFilterPercent) + (accelerationZ * (1.0 - kFilterPercent));
    NSLog("filtered accel x: %f, y: %f, z: %f", accelerationX, accelerationY, accelerationZ);

The `kFilterPercent` constant represents a percentage in the range 0.0 (0%) to 1.0 (100%). At 0.1 (10%) the filter will cause the new accelerometer value to contribute only 10% to the filtered values. So over the course of 10 frames the current acceleration value will change to the one that the device is pointing at. This delay causes motion to be much smoother.

For your game you may need to experiment to find the best value for `kFilterPercent`.


## Working with Accelerometer Coordinates

In the [Core Motion guide](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/motion_event_basics/motion_event_basics.html#//apple_ref/doc/uid/TP40009541-CH6-SW4) Apples gives you this neat graph that explains the directions of the axis:

![](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Art/acceleration_axes_2x.png)

What's crucial to understand here is that these values do not change with respect to device and interface orientation. So depending on whether the game runs in LandscapeLeft or LandscapeRight orientation, you may have to invert the X and Y axis values (ie multiply with -1.0).

Furthermore, in a landscape orientation, the Y axis is actually the horizontal axis while the X axis is the vertical axis. Hence you'll find the assignment of acclerometer x values to a node's y coordinate odd at first:

	// Objective-C
    node.position = ccpAdd(node.position, ccpMult(CGPointMake(-accelerationY, accelerationX), 0.02));

	// Swift
    node.position = ccpAdd(node.position, ccpMult(CGPoint(x: -accelerationY, y: accelerationX), 0.02))

<table border="0"><tr><td width="48px" bgcolor="#d0ffd0"><strong>Tip</strong></td><td bgcolor="#d0ffd0">
If you use the accelerometer to control your game's character you should disable autorotation. Otherwise the interface orientation may change unintentionally while controlling the game, which will confuse the player and possibly even invert the controls.
</td></tr></table>

And then there's the issue of calibration. You can not expect players to play on a flat surface at all times. Most players will want to play at an angle, or even lying down holding the device above them. This requires you to calibrate the device to a desired orientation which is then used as the reference orientation. Tilting the device should then be relative to the reference orientation.

To add to this, you will have to combine the values of two axis. For instance in a landscape app where the device is tiled by a 45° angle along the Y axis then both X and Z axis acceleration values need to contribute equally to the controlled character's Y position.