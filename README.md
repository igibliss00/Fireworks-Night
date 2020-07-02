# Fireworks Night

An iOS game app in Swift.  The objective of the game is to select the fireworks of the same colour and shake the device to make them explode before they disappear out of the screen.  

<img src="https://github.com/igibliss00/Fireworks-Night/blob/master/README_assets/1.png" width="400">

<img src="https://github.com/igibliss00/Fireworks-Night/blob/master/README_assets/2.png" width="400">

## Features

### UIBezierPath

This is used in the project to signify the path that the SKAction should follow. UIBezierPath is a path that consists of straight and curved line segments that you can render in your custom views. You use this class initially to specify just the geometry for your path. Paths can define simple shapes such as rectangles, ovals, and arcs or they can define complex polygons that incorporate a mixture of straight and curved line segments. After defining the shape, you can use additional methods of this class to render the path in the current drawing context. 

A UIBezierPath object combines the geometry of a path with attributes that describe the path during rendering. You set the geometry and attributes separately and can change them independent of one another. After you have the object configured the way you want it, you can tell it to draw itself in the current context. Because the creation, configuration, and rendering process are all distinct steps, Bézier path objects can be reused easily in your code. You can even use the same object to render the same shape multiple times, perhaps changing the rendering options between successive drawing calls.
You set the geometry of a path by manipulating the path’s current point. When you create a new empty path object, the current point is undefined and must be set explicitly. To move the current point without drawing a segment, you use the move(to: ) method. All other methods result in the addition of either a line or curve segments to the path. The methods for adding new segments always assume you are starting at the current point and ending at some new point that you specify. After adding the segment, the end point of the new segment automatically becomes the current point. ([Source](https://developer.apple.com/documentation/uikit/uibezierpath))

```
let path = UIBezierPath()
path.move(to: .zero)
path.addLine(to: CGPoint(x: xMovement, y: 1000))
```

### follow(_:asOffset:orientToPath:speed: )

Creates an action that moves the node at a specified speed along a path.

#### Parameters

- path: A path to follow.
- offset: If true, the points in the path are relative offsets to the node’s starting position. If false, the points in the node are absolute coordinate values.
- orient: If true, the node’s zRotation property animates so that the node turns to follow the path. If false, the zRotation property of the node is unchanged.
- speed: The speed at which the node should move, in points per second.

([Source](https://developer.apple.com/documentation/spritekit/skaction/1417798-follow))

```
let move = SKAction.follow(path.cgPath, asOffset: true, orientToPath:  true, speed: 200)
node.run(move)
```

In this project, the path is determined by the UIBezierPath mentioned above.

### for case let

Instead of the regular “for node in nodesAtPoint”, this project combines “case” and “let” into the mix.

```
for case let node as SKSpriteNode in nodesAtPoint {
    guard node.name == "firework" else { continue }
    node.name = "selected"
    node.colorBlendFactor = 0
}
```

This allows iterating over the collection type conditionally.  This is equivalent to iterating only if we can typecast the item as SKSpriteNode.  This syntax is required in this case because the texture needs to be present in the node that’s being iterated over.
