---
layout: post
title: "Building SBGauge"
date: 2013-11-05 17:59
comments: true
categories: 
---

I built `SBGauge` as part of [GrooveCoach](http://www.groovecoachapp.com) as a way to indicate which 'level' the user was on. When you tapped '+' or '-' the gauge changed accordingly. As part of developing that app I was keen to open source anything I could.


Given the flexibility of this simple library, I thought it would make an interesting code walkthrough.

<!-- more -->

## Drawing the Gauge

`SBGauge` consists of two `CAShapeLayer`s: the animating gauge itself and the 'track' underneath.  The `draw` method simply creates two circles with different colors and adds them to the view's backing layer:

```obj-c
gaugeLayer = [self drawCircleLayer:self.gaugeColor];

CAShapeLayer *trackLayer = [self drawCircleLayer:self.trackColor];

[self.layer addSublayer:trackLayer];
[self.layer addSublayer:gaugeLayer];
```

The circles are drawn by the `drawCircleLayer:(UIColor *)color` method in `SBGaugeView`:

```obj-c
  circleLayer.path = [UIBezierPath bezierPathWithRoundedRect:CGRectInset(self.bounds, inset, inset)
                                                cornerRadius:radius-inset].CGPath;
```

Using `CGRectInset` means we draw *within* the view itself, not on the outside. This is especially if you're working in interface builder - the gauge shouldn't bust out of the frame you create for the view.

## Context

`SBGaugeContext` is responsible for calculating how big the segments will be and keeping track of the current 'step'.  It is initialized with the number of segments:

```obj-c
gauge = [[SBGaugeContext alloc] initWithSegments:self.segments];
```

When you tell `SBGauge` to `stepUp`, the current `SBGaugeContext` will figure out what the current 'step' should now be. `SBGauge` will then draw based on this new context.

This decouples the logic surrounding step calculations from the drawing of the view itself.

## Animating

When the view is redrawn, a `CABasicAnimation` is created to animate from the previous gauge step to the current step. `animateProgress` uses the gauge layer's 'strokeEnd' animate the length of the gauge:

```obj-c
// setup a basic animation using strokeEnd
CABasicAnimation *drawAnimation = [CABasicAnimation animationWithKeyPath:@"strokeEnd"];
drawAnimation.duration            = 0.2;
drawAnimation.repeatCount         = 1.0;
drawAnimation.removedOnCompletion = NO;

// set the from/to values based on the user's previous 'step' & the current one
drawAnimation.fromValue = [NSNumber numberWithFloat:gauge.previous];
drawAnimation.toValue   = [NSNumber numberWithFloat:gauge.value];

// set how the animation should look
drawAnimation.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseIn];

// finally apply the animation to the gauge layer
[gaugeLayer addAnimation:drawAnimation forKey:nil];
```

You'll see that `SBGaugeContext` handles the calculation of the value itself.

## Style

`SBGauge` doesn't have any additional built in 'looks' but by simply setting the `width` property, a number of different styles can be achieved. 

The size of the gauge itself is calcuated based on the containing frame (plus some hardcoded tweaking):

```obj-c
CGFloat radius = (MIN(self.frame.size.width,self.frame.size.height)/2)+40;
CGFloat inset  = self.width/2;
```

This makes it possible to get at least an idea of the size of the view in interface builder.

<hr/>

That's really all there is to it!

I've since experimented with driving the guage using a large number of steps and an `NSTimer` which find in the project's [README](http://www.github.com/stevebartholomew/SBGauge/).

[Check it out on Github](http://www.github.com/stevebartholomew/SBGauge) - I'd love your feedback.
