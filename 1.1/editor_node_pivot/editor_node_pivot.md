#Pivot Joints

The pivot joint has three properties that can be enabled: Spring, Limit and Motor.  Angles are defined in terms of body A, so be sure that if you have a static body it is connected to the joint as point A or else the rest angle and degree limits will not be defined the way they are displayed on screen.

- `Spring:` When the spring is enabled body B will be pulled towards the rest angle with force relative to the stiffness of the spring.

- `Limit:`  When limits are enabled, the range of motion of body B around body A will be limited to within those bounds.

![image](pivotIndicators.png)

> Note: When you have both Spring and Limit enabled a selection bar appears on screen to switch display of circles indicating range etc

- `Motor:`  When enabled the motor will propel body B around the joint  with a given rate.  The arrow on screen indicates the direction that the motor will propel the rotation.  A positive rate rotates the motor counter-clockwise, while a negative rate generates clockwise motion.