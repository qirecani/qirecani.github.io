---
layout: post
title: "A Not-So Normal First Post"
---

The Gaussian integral had stumped folks in the eighteenth century due to its resemblance, yet also its unlikeness, to an elementary form. It also stumped me not so long ago. Here it is, presented innocuously.

$$
\text{I} = \int_{-\infty}^{\infty} e^{-x^2}\,dx.
$$

Standard ways to go about this integral involve some 'changes to polar coordinates', or Jacobians, but to set the tone for this post and many others to come in this blog, we'll go about it in a hand-wavy and fun fashion! However, something unavoidable (from standard approaches) is first squaring the the integral and to use Fubini's Theorem:

$$
\text{I}^2
= \left(\int_{-\infty}^{\infty} e^{-x^2}\,dx\right)
  \left(\int_{-\infty}^{\infty} e^{-y^2}\,dy\right)
= \int_{-\infty}^{\infty}\int_{-\infty}^{\infty} e^{-(x^2+y^2)}\,dx\,dy.
$$

Now we divert all of our attendion to the integrand $e^{-(x^2+y^2)}$. For every point $(x,y)$ in the Cartesian plane, a simple use of Pythagoras' theorem tells us that $x^2+y^2$ is the square of the point's distance from the origin, which we define with $z=\sqrt{x^2+y^2}$. Visually, we are now finding the volume of a (very large) bell, rotationally symmetric about the origin, in which it reaches a peak height of $e^{-(0^2+0^2)}=1$. An illustration is given below.

<figure>
  <img src="/assets/img/gaussian bell.jpg">
</figure>

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
