---
layout: post
title: "A Reasonably Normal First Post"
---

The Gaussian integral had stumped folks in the eighteenth century due to its resemblance, yet also its unlikeness, to an elementary form. It also stumped me not so long ago. Here it is, presented innocuously.

$$
I = \int_{-\infty}^{\infty} e^{-x^2}\,dx.
$$

Standard ways to go about this integral involve some 'changes to polar coordinates', or Jacobians, but to set the tone for this post and many others to come in this blog, we'll go about it in a hand-wavy and fun fashion! However, something unavoidable (from standard approaches) is first squaring the the integral and to use Fubini's Theorem:

$$
I^2
= \left(\int_{-\infty}^{\infty} e^{-x^2}\,dx\right)
  \left(\int_{-\infty}^{\infty} e^{-y^2}\,dy\right)
= \int_{-\infty}^{\infty}\int_{-\infty}^{\infty} e^{-(x^2+y^2)}\,dx\,dy.
$$

Now we divert all of our attendion to the integrand $e^{-(x^2+y^2)}$. For every point $(x,y)$ in the Cartesian plane, a simple use of Pythagoras' theorem tells us that $x^2+y^2$ is the square of the point's distance from the origin, which we define with $r=\sqrt{x^2+y^2}$. Visually, we are now finding the volume of a (very large) bell, rotationally symmetric about the origin, in which it reaches a peak height of $e^{-(0^2+0^2)}=1$. An illustration is given below.

<figure>
  <img src="/assets/img/gaussian bell.jpg">
</figure>

We now approximate the volume of this bell using hollow cynlinders of height $e^{-(x^2+y^2)}=e^{-r^2}$ that 'wrap' around each other. We start at the origin with a very thin vertical 'rod' with height $1$. We tightly wrap around this cylinder with a hollow cylinder with height $e^{-\Delta r^2}$ and 'thickness' $\Delta r$. More generally, for all $r>0$, the additional layer of volume added on per $\delta r$ increment is just the difference in volumes of two solid cylinders - one with base radius $r$ and height $e^{-(r+\Delta r)^2}$, the other with base radius $r+\Delta r$ and height $e^{-(r+\Delta r)^2}$. The incremental volume is given below

$$
\pi \left[(r+\Delta r)^2-r^2\right]e^{-(r+\Delta r)^2}=\pi (2r\Delta r+\Delta r^2)e^{-r^2}\cdot e^{-2r\Delta r-\Delta r^2}.
$$

Now, we use the notation $o(\Delta r)$ to describe a function $f(r)$ such that $f(r)\to 0$ 'much quicker' than $\Delta r\to 0$. We first observe that a factor of $\Delta r^2=o(\Delta r)$ can be distributed. Additionally, a Taylor Expansion gives $e^{-2r\Delta r-\Delta r^2}=1-2r\Delta r + o(\Delta r)$. Finally, $\Delta r$ is another factor that, when distributed, leaves a simplifies the expression above to

$$
2\pi re^{-r^2}\cdot \Delta r+o(\Delta r)
$$

Choose a partition $\Pi$ of $(0,\infty)$ small enough such that each interval is of length at most $\Delta r$. We then obtain a Lower Riemann Integral approximation of $I^2$ as

$$
\sum_\Pi 2\pi re^{-r^2}\cdot \Delta r+o(\Delta r).
$$

Now taking the limit $\Delta r \to 0$, we get

$$
\lim_{\Delta r \to 0}\sum_\Pi 2\pi re^{-r^2}\cdot \Delta r+o(\Delta r)=\int_0^\infty 2\pi re^{-r^2}dr.
$$

Giving us an integral that can be solved very handily by inspection! Hence (with some abuse of notation),

$$
I^2=\int_0^\infty 2\pi re^{-r^2}dr=\pi\left[-e^{-r^2}\right]^{r=\infty}_{r=0}=\pi.
$$

Hence, common sense tells us that $I>0$, and so we finally have our answer:

$$
I = \int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}.
$$

Now, of course, some normalising constants transforms the integrand above to the probability density function (Standard) Normal Distribution:

$$
\frac{1}{\sqrt{2\pi}}e^\frac{-z^2}{2}.
$$

# Extra Trivia/Problems
It's well known that no elementary expression exists for the definite integrals of $e^{-x^2}$ (or $e^{\alpha x^2}$ for some $\alpha\in\mathbb{R}\setminus\{0\}$) with respect to $x$. However, an interesting problem I found lurking in the depths of the Simon Marais Mathematics Competition practice problems.

$$
\text{Which of the two is larger: }\int_0^{\int_0^1e^{-x^2}dx}e^{x^2}dx\quad\text{or}\quad\int_0^{\int_0^1e^{x^2}dx}e^{-x^2}dx?
$$

More on this later...
