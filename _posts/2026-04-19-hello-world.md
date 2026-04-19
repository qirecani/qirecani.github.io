---
layout: post
title: "A tiny Gaussian integral warm-up"
---

One of the nicest little calculations in analysis is the Gaussian integral

$$
I = \int_{-\infty}^{\infty} e^{-x^2}\,dx.
$$

At first glance this does not look elementary, and in one variable it more or less isn’t.  
The standard trick is to square the integral and move to two dimensions:

$$
I^2
= \left(\int_{-\infty}^{\infty} e^{-x^2}\,dx\right)
  \left(\int_{-\infty}^{\infty} e^{-y^2}\,dy\right)
= \int_{\mathbb{R}^2} e^{-(x^2+y^2)}\,dx\,dy.
$$

Now switch to polar coordinates:

$$
I^2
= \int_0^{2\pi}\int_0^\infty e^{-r^2} r\,dr\,d\theta
= 2\pi \int_0^\infty e^{-r^2} r\,dr.
$$

With the substitution $u=r^2$, this becomes

$$
I^2 = 2\pi \cdot \frac12 \int_0^\infty e^{-u}\,du = \pi.
$$

So

$$
I = \sqrt{\pi}.
$$

What I like about this argument is that the one-dimensional problem becomes easy only after we stop treating it as one-dimensional.
