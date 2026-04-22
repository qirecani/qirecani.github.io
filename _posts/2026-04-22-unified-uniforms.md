---
layout: post
title: "Unified Uniforms"
---

Let's kick off this second post with some more probability.

I first encountered the uniform distribution in high school, and I remember thinking to myself - "this can't be that hard". Oh boy, how wrong that would turn out to be...

In this post, we'll explore some interesting problems involving standard uniform distributions, that is, random variables with the following Probability Density Function (pdf)

$$
f(x)=\mathbb{1}_{\{x\in(0,1)\}}.
$$

and Cumulative Distribution Function (cdf)

$$
F(x)=x\mathbb{1}_{\{x\in(0,1)\}}.
$$

Now, I expect this post to be much lengthier than the first one, so feel free to kick back and enjoy a barrage questions that you never thought could be asked about $X\sim U(0,1)$.

$$
\text{Let }X,Y,Z\text{ each be independent }U(0,1)\text{ random variables. Prove that }(XY)^Z\sim U(0,1).
$$

Honestly, this more of an algebra exercise than a thinking exercise. Let's first find the cdf of $XY$. Using the Law of Total Probability, we have

$$
\mathbb{P}(XY\le m)=\int_0^1\mathbb{P}(XY\le m\mid Y=y)dy=\int_0^1\mathbb{P}(X\le \frac{m}{y})dy.
$$

Now, when $y\le m$, $\mathbb{P}(X\le \frac{m}{y})=1$, so the integral is

$$
\int_0^1\mathbb{P}(X\le \frac{m}{y})dy=\int_0^mdy+\int_m^1\frac{m}{y}dy=m-m\log m,\quad m\in(0,1).
$$

We now use this cdf and Law of Total Probability again, where

$$
\mathbb{P}((XY)^Z\le t)=\int_0^1\mathbb{P}((XY)^Z\le t\mid Z=z)dz=\int_0^1\mathbb{P}(XY\le t^{\frac1z}\mid Z=z)dz=\int_0^1t^{\frac1z}-t^{\frac1z}\log t^{\frac1z}dz.
$$

We now make the substitution $s=\frac1z\implies dz=\frac{-1}{s^2}ds$ and obtain

$$
\int_0^1t^{\frac1z}-t^{\frac1z}\log t^{\frac1z}dz=\int_1^\infty\frac{t^s}{s^2}\left(1-s\log t\right)dz=-\int_1^\infty d\left(\frac{t^s}{s}\right)=t,\quad t\in(0,1).
$$

$$
\implies\mathbb{P}((XY)^Z\le t)=t\implies(XY)^Z\sim U(0,1).
$$

That may as well have been a nice calculus warmup, bringing us to our next problem:

$$
\text{Let }\tau=\min(n\in\mathbb{N}:\sum_{i=1}^nX_i\ge1),\text{ where each }X_i\sim U(0,1)\text{ are i.i.d. Evaluate }\mathbb{E}[\tau].
$$

A super common misconception is to think that $\mathbb{E}[X_i]=\frac12$ (true!), so it would take on average two 'draws' to get to $1$, deducing that $\mathbb{E}[\tau]=2$ (false!). However, this is clearly an underestimation since $\tau\ge2$ almost surely, and $\mathbb{P}(\tau>2)>0$, so actually, $\mathbb{E}[\tau]>2$. The *correct* way to approach this problem is to recursively define a conditional expectation $f(x)=\mathbb{E}[\text{additional no. draws to reach a sum }\ge1\mid\text{current sum }=x]$, such that for $x\in(0,1)$,

$$
f(x)=1+\int_0^{1-x}f(x+t)dt=1+\int_x^1f(t)dt.
$$

We now differentiate both sides with respect to $x$ and get

$$
\frac{d}{dx}f(x)=-f(x).
$$

Which has a simple solution $f(x)=Ce^{-x}$. Substitute this into the integral definition of $f(0)$ to get

$$
C=f(0)=1+\int_0^1f(t)dt=1+\int_0^1Ce^{-t}dt=1+C(1-e^{-1})\implies C=e.
$$

Therefore, $f(x)=e^{1-x}$ and

$$
\mathbb{E}[\tau]=f(0)=e
$$

What a $\textbf{great expectation}$!
