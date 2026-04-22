---
layout: post
title: "A Reasonably Normal First Post"
---

The Gaussian integral had stumped folks in the eighteenth century due to its resemblance, yet also its unlikeness, to an elementary antiderivative. It also stumped me not so long ago. Here it is, presented innocuously.

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

Now we divert all of our attendion to the integrand $e^{-(x^2+y^2)}$. For every point $(x,y)$ in the Cartesian plane, a simple use of Pythagoras' Theorem tells us that $x^2+y^2$ is the square of the point's distance from the origin, which we define with $r=\sqrt{x^2+y^2}$. Visually, we are now finding the volume of a (very large) bell, rotationally symmetric about the origin, in which it reaches a peak height of $e^{-(0^2+0^2)}=1$. An illustration is given below.

<figure>
  <img src="/assets/img/gaussian bell.jpg">
</figure>

We now approximate the volume of this bell using hollow cylinders that 'wrap' around each other. We start at the origin with a very thin vertical 'rod' with height $1$. We tightly wrap around this cylinder with another hollow cylinder with height $e^{-\Delta r^2}$ and 'thickness' $\Delta r$. More generally, for all $r>0$, the additional layer of volume added on per $\Delta r$ increment is just the difference in volumes of two solid cylinders - one with base radius $r$ and height $e^{-(r+\Delta r)^2}$, the other with base radius $r+\Delta r$ and height $e^{-(r+\Delta r)^2}$. The incremental volume is given below

$$
\pi \left[(r+\Delta r)^2-r^2\right]e^{-(r+\Delta r)^2}=\pi (2r\Delta r+\Delta r^2)e^{-r^2}\cdot e^{-2r\Delta r-\Delta r^2}.
$$

Now, we use the notation $o(\Delta r)$ to describe a function $f(r)$ such that $f(r)\to 0$ 'much quicker' than $\Delta r\to 0$, i.e. $\lim_{\Delta r\to0}\frac{f(r)}{\Delta r}=0$. We first observe that a factor of $\Delta r^2=o(\Delta r)$ can be distributed. Additionally, a Taylor Expansion gives $e^{-2r\Delta r-\Delta r^2}=1-2r\Delta r + o(\Delta r)$. Finally, $\Delta r$ is another factor that, when distributed, simplifies the expression above to

$$
2\pi re^{-r^2}\cdot \Delta r+o(\Delta r)
$$

Choose a partition $\Pi$ of $(0,\infty)$ small enough such that each interval is of length at most $\Delta r$. We then obtain a Lower Riemann Integral approximation of $I^2$ as

$$
\sum_\Pi \left(2\pi re^{-r^2}\cdot \Delta r+o(\Delta r)\right).
$$

Now taking the limit $\Delta r \to 0$, we get

$$
\lim_{\Delta r \to 0}\sum_\Pi \left(2\pi re^{-r^2}\cdot \Delta r+o(\Delta r)\right)=\int_0^\infty 2\pi re^{-r^2}dr.
$$

Giving us an integral that can be solved very handily by inspection! Hence (with some abuse of notation),

$$
I^2=\int_0^\infty 2\pi re^{-r^2}dr=\pi\left[-e^{-r^2}\right]^{r=\infty}_{r=0}=\pi.
$$

Hence, common sense tells us that $I>0$, and so we finally have our answer:

$$
I = \int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}.
$$

Now, of course, some normalising constants transforms the integrand above to the probability density function of a (Standard) Normal Random Variable:

$$
\frac{1}{\sqrt{2\pi}}e^\frac{-z^2}{2}.
$$

# Extra Trivia/Problems
It's well known that no elementary antiderivative exists for the definite integrals of $e^{-x^2}$ (or $e^{\alpha x^2}$ for some real $\alpha\ne0$) with respect to $x$. Consequently, this leads me to share an interesting problem I found lurking in the depths of the Simon Marais Mathematics Competition practice problems.

$$
\text{Which of the two is larger: }\int_0^{\int_0^1e^{-x^2}dx}e^{x^2}dx\text{ or }\int_0^{\int_0^1e^{x^2}dx}e^{-x^2}dx?
$$

Immediately, one gets the suspicion that the bounds from $0$ to $1$ of the nested definite integrals are arbitrary, given the lack of an elementary antiderivative. Hence we are motivated to define for $t\ge0$

$$
f(t)=\int_0^{\int_0^te^{-x^2}dx}e^{x^2}dx\quad\text{and}\quad g(t)=\int_0^{\int_0^te^{x^2}dx}e^{-x^2}dx.
$$

With $f(0)=g(0)=0$, we want to compare $f(1)$ and $g(1)$. Let $f'(t)=\frac{d}{dt}f(t)$ and $g'(t)=\frac{d}{dt}g(t)$. Then, by the Chain Rule and Fundamental Theorem of Calculus,

$$
f'(t)=\exp\left[\left(\int_0^te^{-x^2}dx\right)^2\right]\cdot e^{-t^2}\quad\text{and}\quad g'(t)=\exp\left[-\left(\int_0^te^{x^2}dx\right)^2\right]\cdot e^{t^2}.
$$

Then,

$$
\frac{f'(t)}{g'(t)}=\exp\left[\left(\int_0^te^{-x^2}dx\right)^2+\left(\int_0^te^{x^2}dx\right)^2-2t^2\right]
$$

Now, for two positive real numbers $a,b$, $(a-b)^2\ge0\implies a^2+b^2\ge2ab$, so

$$
\left(\int_0^te^{-x^2}dx\right)^2+\left(\int_0^te^{x^2}dx\right)^2\ge2\int_0^te^{-x^2}dx\cdot \int_0^te^{x^2}dx.
$$

Finally, the Cauchy-Schwartz Inequality gives

$$
2\int_0^te^{-x^2}dx\cdot \int_0^te^{x^2}dx\ge\int_0^te^{-x^2}\cdot e^{x^2}dx=2t.
$$

Observe for $t\in(0,1)$, $2t>2t^2$, therefore

$$
\frac{f'(t)}{g'(t)}\ge\exp(2t-2t^2)>1\implies f'(t)>g'(t) \implies f(1)>g(1).
$$

Thus we have our answer:

$$
\int_0^{\int_0^1e^{-x^2}dx}e^{x^2}dx>\int_0^{\int_0^1e^{x^2}dx}e^{-x^2}dx.
$$

It would be dire to not include any probability problems in this debut blog post, so I now propose one of my own:

$$
\text{If }Z\sim\mathcal{N}(0,1),\text{ evaluate }\mathbb{E}\left[\int_{-\infty}^Z e^{-x^2}dx\right].
$$

A rather simple way to go about this is using the fact that $\Phi(Z)\sim U(0,1)$, where $\Phi(Z)$ denotes the Cumulative Distribution Function of $Z$, and then do some algebraic manipulations. Instead, let's take a more scenic route! Our desired integral is

$$
\mathbb{E}\left[\int_{-\infty}^Z e^{-x^2}dx\right]=\int_{-\infty}^\infty\left(\int_{-\infty}^z e^{-x^2}dx\right)\cdot \frac{1}{\sqrt{2\pi}}e^\frac{-z^2}{2}dz.
$$

We use Fubini/Tonelli's Theorem above to get a double integral, and swap the order of integration to get

$$
\int_{-\infty}^\infty\left(\int_{-\infty}^z e^{-x^2}dx\right)\cdot \frac{1}{\sqrt{2\pi}}e^\frac{-z^2}{2}dz=\int_{-\infty}^\infty e^{-x^2}\left(\int_{z=x}^\infty\frac{1}{\sqrt{2\pi}}e^\frac{-z^2}{2}dz\right)dx=\int_{-\infty}^\infty e^{-x^2}\left(1-\Phi(x)\right)dx.
$$

Now, one more trick is to realise that $\frac12-\Phi(x)$ is an odd function with respect to $x$, and the product of an odd and even function is also an odd function, which integrates to $0$ over the real line (given the necessary conditions that we shall not check here!). So, we rewrite the integral above as

$$
\int_{-\infty}^\infty e^{-x^2}\left(1-\Phi(x)\right)dx=\int_{-\infty}^\infty e^{-x^2}\cdot\frac12dx+
\int_{-\infty}^\infty e^{-x^2}\left(\frac12-\Phi(x)\right)dx=\frac12\int_{-\infty}^\infty e^{-x^2}dx=\frac{\sqrt{\pi}}{2}.
$$

Thus, we conclude our blog debut with a $\textbf{great expectation}$:

$$
\mathbb{E}\left[\int_{-\infty}^Z e^{-x^2}dx\right]=\frac{\sqrt{\pi}}{2},\quad\text{where }Z\sim\mathcal{N}(0,1).
$$

In fact, this result holds for any *nice* random variable distributed 'symmetrically' about $0$!
