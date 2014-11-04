# To Do List & Planning

https://www.youtube.com/watch?v=7dyj6NkM8Ew

## Welcome
- Welcome! page (excite reader, spritebuilder show-off video or gif anim, promote the book, quickly summarize core features & benefits, cc vs sk, what's new)
	- Learning Resources (cocos2d class reference, forum, book, book download, learn objc, else?)
	- Learn SpriteBuilder Errata (mention anything the book got wrong or is out of date)

## Overview Articles
- Prerequisites (xcode, objc experience, developer program)
- Getting Started with SB (rudimentary info to install, create, build and run a new project)
- Getting Started with CC (rudimentary info to install, create, build and run a new project)
- Understanding Core Concepts (high-level, explain scenes, nodes, render loop - follow SK intro & existing articles)
	- cocos2d architecture (view -> scene -> nodes)
	- clear up common misconception: nodes are not views
- Understanding the scene graph (conceptual, ie overlay menu vs new scene, scrolling game with static HUD, debug overlay, rotate node around parent/anchor, parent-child relations, properties children inherit (or not) from parent, etc)
- Understanding Nodes (how each node is used for, can be used for, shouldn't be used for)
- Update & Draw Loop (draw order, update order, vsync, 60/30/20/15 fps)
- Understanding Textures (image -> texture -> sprite, position vs anchor point, image scaling vs resolution-specific files, atlas vs single files, batching, pot vs npot, image file formats and tools, preloading)
- Understanding Animations (actions vs timeline vs sprite frame vs manual property changes)
- Understanding Physics ()
- Understanding Audio ()
- Understanding Game State (global data vs ivars, using nsuserdefaults, singletons vs multitons, passing data between scenes, user data property)
- Understanding Background Mode & Pause
- Understanding Performance (simulator vs device, file size vs texture memory, premature optimization, real-world vs synthetic tests, engine code vs whatever code you write, Instruments)

## SpriteBuilder Articles
- User Interface Overview (use same terms as in book, quick overview of each detail view with example)
- Creating new (CCB) files (discuss individual types and what they are for, when to use them)
- working with file view (folders, preview, file properties, caveats of moving files)
    - working with images (add image, image properties, sprite sheets)
    - working with audio files (add file, properties)
    - working with other files (bitmap font, raw data)
	- Working with packages
- working with tileless view (filters, drag & drop, possible duplicates)
- working with node library (list, drag & drop)
- Working with the stage (zoom, pan, color, frame, language, resolution, notes)
	- grid editing mode
	- changing resolution, color, etc.
- working with nodes
	- Selecting and editing node properties (move, nudge, align)
	- grouping and changing draw order of nodes
	- working with prefabs (sub file ccb, caveats & considerations)
	- code connections (includes custom properties)
	- localizing labels
	- Adapting to Screen Resolutions (position types, insets, switching iphone/ipad view, screen mode, orientation)
- project settings
- troubleshooting (clean cache ..)

## Cocos2D Articles
- Presenting scenes (replace, push, pop, transition)
- creating nodes programmatically
- searching for and getting nodes (recursively, running code on custom subclass nodes, accessing data in other nodes, safely storing references to other nodes ie weak vs strong ref)
- converting coordinate spaces
- working with assets
	- Working with CCB files (loading as scene/node, didLoadFromCCB, scene graph of a ccb scene/sub file, etc)
	- Resolution specific file suffixes
	- supported texture & image file formats, pros & cons
- handling user input
	- Touch Events
	- Accelerometer
	- game controller
- Working with Nodes (including those not in SpriteBuilder)
	- tilemaps
	- draw node
	- batch node (?)
	- parallax
	- clipping
	- motion steak
	- progress
	- render texture
	- light node
- Subclassing notes (which init to call, when to subclass & when not, alternatives)
- Timers & Scheduling (warn against using nstimer, gcd, performselector after delay)
- Point Extensions
- Apple Framework integration (outline anything special about integrating game center, game controller, messaging, photo library, etc)
- Expert's Corner
	- Upgrading Cocos2d manually (without SB)
	- CCAppDelegate
	- adding cocos2d to existing cocoa app, managing cocos2d lifecycle as a "client view"
	- Multithreading Notes (what you can and can not do, like creating sprites with textures on background thread)
	- Optimization Notes (reuse nodes, preload, optimize for batch drawing, enable metal)
	- Memory Management (preloading, caching, unloading, avoiding retain cycles, necessary and unnecessary cleanup)
	- Profiling & Debug Stats
	- config settings
	- logging and other preprocessor macros
- Troubleshooting (common mistakes)

## Physics Articles
- working with physics (ie physics engine != real-world physics, explain shortcuts)
- ObjC vs C interface (refer to C docs on Chipmunk page)
- setup of world and physics nodes (sb and code)
- editing physics properties of a node (sb)
- working with joints (sb and code)
- categories, masks and collision types
- physics collision handling (delegate)
- force vs impulse vs velocity vs setting position
- kinematic vs dynamic vs static bodies
- enable physics debug drawing (plus explanations)
- Physics vs Actions / Timeline
- emulating a physics field (like in SK)
- Using Box2D with cocos2d (quick instructions, pros and cons)
- troubleshooting & tips (soft-body physics in book)

## Animation Articles
- Scene Transitions (maybe: gif anim with demo of each transition)
- Working with Timeline Animations (multiple articles)
	- working with keyframes
	- working with multiple timelines
	- chaining & looping timelines
	- disable autoplay
	- programming animation playback (play, stop, delegate)
	- callbacks & audio keyframes
	- creating sprite frame keyframes
- Animating with actions (programming, multiple articles)
	- action hierarchy, list
	- running actions in parallel and in sequence
	- repeating actions
	- reusing actions
	- changing action speed
	- running blocks & selectors
	- tweening
	- bezier
	- spawning actions
	- running, finding, stopping actions (mention: pause)
- Understanding Scrolling (pan the layer in opposite direction)
	- center on and follow node example

## Graphics Articles
- working with effect nodes (sb, adding effects to sprites)
	- programming effects (create, modify)
	- effect performance
- editing particle effects (list supported external tools)
	- loading particle plists
	- modifying effects at runtime
	- effect on performance (limit particle count)
	- particle limitations (can't access individual particles, particles can't have physics)
- v3 renderer example
- shader programming intro (link to cookbook)
- customizing the cocos2d GL view (depth buffer, antialiasing, etc)
- drawing sprites in a grid without black line artifacts
- what gets drawn when and why? (explain culling, visible vs opacity vs removing)

## GUI Articles
- Editing & Programming GUI controls (one article for every GUI control)
	- button
	- slider
	- box layout
	- scroll view
- GUI Design Concepts
	- popover
	- fullscreen popover
	- static HUD in scrolling game
	- GUI with physics and animations
- Using UIKit views with cocos2d
	- in front or behind
	- nodes aren't views
	- the cocos2d view controller

## Audio Articles
- ObjectAL Introduction (AVAudio vs OpenAL)
- Supported Audio formats
- Simple Audio Reference
- Advanced Audio (at least some examples, areas where OAL doc is insufficient)
- Troubleshooting

## Android Articles
- What the Android plugin does (benefits)
- Install Plugin
- Enable Android publishing
- Setup Android device, build in xcode
- different launch process (activity class)
- troubleshooting
- Technical Notes (ie Android file formats, preprocessor macros)

## Developer Articles
- importing private headers, undocumented classes
- contributor guide (pulling from github, building from sources, etc)
- CCB file format etc (the existing articles overhauled)
- spritebuilder project & packages format
