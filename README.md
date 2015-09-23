# Tinderable
A simple library for creating cards like in Tinder easily and quickly. Based on <a href="https://github.com/zhxnlai/ZLSwipeableView/">ZLSwipeableView</a>.

Swift 2 full compatibility. 

# Preview

# Custom Animation
<img src="https://github.com/zhxnlai/ZLSwipeableViewSwift/blob/master/Previews/animation.gif" />

# Custom Swipe
<img src="https://github.com/zhxnlai/ZLSwipeableViewSwift/raw/master/Previews/swipe.gif" />

# Custom Direction
<img src="https://github.com/zhxnlai/ZLSwipeableViewSwift/raw/master/Previews/direction.gif" />

# Undo
<img src="https://github.com/zhxnlai/ZLSwipeableViewSwift/raw/master/Previews/undo.gif" />


# Usage

It contains the following demos: Default, Custom Animation, Custom Swipe, Custom Direction and Undo.

Just import it to your controller:

<pre>#import Tinderable</pre>

Later just use the next functions:

<pre>
var tinderable = Tinderable(frame: CGRect(x: 0, y: 0, width: 300, height: 500)))
view.addSubview(tinderable)
</pre>

The nextView property, a closure that returns an UIView, is used to provide subviews to Tinderable. After defining it, you can call loadViews and Tinderable will invoke nextView numPrefetchedViews times and animate the prefetched views.

<pre>
tinderable.nextView = {
  return UIView()
}
tinderable.numPrefetchedViews = 3
tinderable.loadViews()
</pre>

The demo app includes examples of both creating views programmatically and loading views from Xib files that use Auto Layout.

To discard all views and reload programmatically:

<pre>
tinderable.discardViews()
tinderable.loadViews()
</pre>

You can limit the direction swiping happens using the direction property and register callbacks like this. Take a look at the Custom Direction example for details.

<pre>
tinderable.direction = .Left | .Up
tinderable.direction = .All

tinderable.didStart = {view, location in
    println("Did start swiping view at location: \(location)")
}
tinderable.swiping = {view, location, translation in
    println("Swiping at view location: \(location) translation: \(translation)")
}
tinderable.didEnd = {view, location in
    println("Did end swiping view at location: \(location)")
}
tinderable.didSwipe = {view, direction, vector in
    println("Did swipe view in direction: \(direction), vector: \(vector)")
}
tinderable.didCancel = {view in
    println("Did cancel swiping view")
}
</pre>

You can swipe the top view programmatically in one of the predefined directions or with any point and direction in the view's coordinate.

<pre>
tinderable.swipeTopView(inDirection: .Left)
tinderable.swipeTopView(inDirection: .Up)
tinderable.swipeTopView(inDirection: .Right)
tinderable.swipeTopView(inDirection: .Down)

tinderable.swipeTopView(fromPoint: CGPoint(x: 100, y: 30), inDirection: CGVector(dx: 100, dy: -800))
</pre>

You can also change how the direction gets interpreted by overriding the interpretDirection property. Take a look at the Custom Swipe example for details.

You can create custom animation by overriding the animateView property. Take a look at the Custom Animation example for details.

You can undo/rewind by storing the swiped views and insert them back to the top by calling insertTopView. Take a look at the Undo example for details.
