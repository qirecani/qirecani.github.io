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
\text{Let }\tau=\min\{n\in\mathbb{N}:\sum_{i=1}^nX_i\ge1\},\text{ where each }X_i\sim U(0,1)\text{ are i.i.d. Evaluate }\mathbb{E}[\tau].
$$

A super common misconception is to think that $\mathbb{E}[X_i]=\frac12$ (true!), so it would take on average two 'draws' to get to $1$, deducing that $\mathbb{E}[\tau]=2$ (false!). However, this is clearly an underestimation since $\tau\ge2$ almost surely, and $\mathbb{P}(\tau>2)>0$, so actually, $\mathbb{E}[\tau]>2$. The *correct* way to approach this problem is to recursively define a conditional expectation $f(x)=\mathbb{E}[\tau-t\mid\sum_{i=1}^tX_i=x]$, such that for $x\in(0,1)$,

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
\mathbb{E}[\tau]=f(0)=e\approx2.718
$$

What a $\textbf{great expectation}$! Let's consider a follow up problem, under the same setup as above:

$$
\text{What is }\mathbb{E}[X_\tau]\text{ ?}
$$

Another common misconception is to assume $\mathbb{E}[X_\tau]=\mathbb{E}[X_1]=\frac12$, however, Doob's Optional Stopping here does not apply here, because the process $\\{X_t\\}$ is not a martingale. An intuitive reason why is to see $X_t$ clearly depends on $X_1,X_2,\dots,X_{t-1}$ instead of just $X_{t-1}$. Also, $0<S=\sum_{i=1}^{\tau-1}X_i<1$ almost surely, and so $X_\tau\ge1-S$ is not uniformly distributed over $(0,1)$. In fact, we can now deduce that $\mathbb{E}[X_\tau]>\frac12$.

Our 'recursive expectation' approach from before will help us tackle this problem. Let's generalise and let $f(x)$ be the expected value of the last 'draw' to reach a total sum of greater than $x$. That is, for $x\in(0,1)$,

$$
\tau_x=\min\{n\in\mathbb{N}:\sum_{i=1}^nX_i>x\},\text{ where }X_i\sim U(0,1)
$$

and

$$
f(x)=\mathbb{E}[X_{\tau_x}].
$$

We are interested in $f(1)=\mathbb{E}[X_{\tau_1}]=\mathbb{E}[X_\tau]$, and it is clear that $f(0)=\mathbb{E}[X_1]=\frac12$. Under our original experiment, if we need to reach a sum of at least $x$ to stop 'drawing', the current sum is $1-x$. Let $T\sim U(0,1)$ be the next 'draw'. If $T\in(0,x)$, the problem reduces to $f(x-T)$, otherwise $T$ is the last draw. Using the Law of Total Expectation, for $x\in(0,1)$ we have

$$
f(x)=\int_0^1f(x-t)dt=\int_0^xf(x-t)dt+\int_x^1tdt=\int_0^xf(t)dt+\frac{1-x^2}{2}.
$$

Differentiating both sides with respect to $x$ yields a first order ODE.

$$
\frac{d}{dx}f(x)=f(x)-x\iff\frac{d}{dx}f(x)-f(x)=-x
$$

We choose an integrating factor $e^{-x}$ to obtain

$$
\frac{d}{dx}\left(f(x)e^{-x}\right)=-xe^{-x}\implies f(x)e^{-x}=(x+1)e^{-x}+C\implies f(x)=x+1+Ce^x.
$$

Using $f(0)=\frac12$,

$$
f(0)=1+C=\frac12\implies C=-\frac12\implies f(x)=x+1-\frac12 e^x,\quad\forall x\in(0,1).
$$

Finally, evaluating $f(1)$ gives us another $\textbf{great expectation}$:

$$
\mathbb{E}[X_\tau]=2-\frac{e}{2}\approx0.641
$$

Now, let's take a detour before doing some more problems. We shift our attention to Order Statistics. Let $S=\\{X_1,X_2,\dots,X_n\\}$ be a set of $n$ i.i.d. continuous random variables - not necessarily $U(0,1)$! Denote $X_{(1)},X_{(2)},\dots,X_{(n)}$ as the *ordered permutation* of $S$, in non-decreasing order. We can use some combinatorics and hand-wavey limits to obtain the cdf and pdf of $X_{(k)}$, the $k^\text{th}$ order statistic of $S$, in terms of the cdf and pdf of $X$, in which shall be denoted as $F_X(x)$ and $f_X(x)$ respectively. For the cdf, if the $k^\text{th}$ largest element of $S$ is at most $x$, then $k$ elements of $S$ must be less than or equal to $x$, and the remaining $n-k$ elements must be strictly greater than $x$. We have $\binom{n}{k}$ choices for this arrangement, thus

$$
F_{X_{(k)}}(x)=\mathbb{P}(X_{(k)}\le x)=\binom{n}{k}\mathbb{P}(X\le x)^k\mathbb{P}(X>x)^{n-k}=\binom{n}{k}\left(F_X(x)\right)^k\left(1-F_X(x)\right)^{n-k}.
$$

Note that $f_X(x)=\frac{d}{dx}F_X(x)=\lim_{\Delta x\to0}\frac{\mathbb P(x\le X<x+\Delta x)}{\Delta x}$. We will now construct a limit to find $f_{X_{(k)}}(x)$. Following a similar combinatorical argument from above, we can reason that

$$
\mathbb{P}(x\le X_{(k)}<x+\Delta x)=k\binom{n}{k}\mathbb{P}(X\le x)^{k-1}\mathbb{P}(x\le X<x+\Delta x)\mathbb{P}(X>x)^{n-k}
$$

$$
=k\binom{n}{k}\left(F_X(x)\right)^{k-1}\left(1-F_X(x)\right)^{n-k}\cdot\mathbb{P}(x\le X<x+\Delta x).
$$

$$
\implies\lim_{\Delta x\to0}\frac{\mathbb{P}(x\le X_{(k)}<x+\Delta x)}{\Delta x}=k\binom{n}{k}\left(F_X(x)\right)^{k-1}\left(1-F_X(x)\right)^{n-k}\cdot\lim_{\Delta x\to0}\frac{\mathbb{P}(x\le X<x+\Delta x)}{\Delta x}
$$

$$
\implies f_{X_{(k)}}(x)=k\binom{n}{k}\left(F_X(x)\right)^{k-1}f_X(x)\left(1-F_X(x)\right)^{n-k}.
$$

Now, if $X\sim U(0,1)$, using $n!=\Gamma(n+1)=\int_0^\infty t^ne^{-t}dt$, we get

$$
f_{X_{(k)}}(x)=\frac{\Gamma(n+1)}{\Gamma(k)\Gamma(n-k+1)}x^{k-1}(1-x)^{n-k},\quad x\in(0,1).
$$

Those with a handy eye may recognise this as the pdf of a $\text{Beta}(k)(n-k+1)$ random variable, and indeed, this is the distribution of the $k^\text{th}$ order statistic of $S$. In particular, $\mathbb{E}[X_{(k)}]=\frac{k}{n+1}$, which agrees with an intuitive guess based on the average 'spacing' of $S$ across the interval $(0,1)$.

We are now finally ready to tackle the next problem:

$$
\text{Let }S=\\{X_1,X_2,\dots,X_n\\}\text{ be a set of }n\text{ i.i.d. }U(0,1)\text{ random variables}.
$$

$$
\text{Find }\mathbb{P}(|X_i-X_j|>x,\forall i\ne j)\text{ and }\mathbb{E}[\min(\\{|X_i-X_j|\\}_{i\ne j})].
$$

It suffices to only focus on the order statistics of $S$, where

$$
\mathbb{P}(|X_i-X_j|>x,\forall i\ne j)=\mathbb{P}(\min(X_{(2)}-X_{(1)},X_{(3)}-X_{(2)},\dots,X_{(n)}-X_{(n-1)})>x).
$$

In particular, let's try to find the joint distribution of $X_{(1)},X_{(2)},\dots,X_{(n)}$. Intuitively, every permutation of $S$ is equally likely, and so we are led to believe that $f_{X_{(1)},X_{(2)},\dots,X_{(n)}}(x_1,x_2,\dots,x_n)=n!$ with support $0<x_1<x_2,\dots,x_n$. We can confirm this by taking a similar combinatorical limit from above, where

$$
f_{X_{(1)},X_{(2)},\dots,X_{(n)}}(x_1,x_2,\dots,x_n)=\lim_{\Delta x_1\to0,\Delta x_2\to0,\dots,\Delta x_n\to0}\frac{\mathbb{P}(\bigcap_{k=1}^n\left(x_k\le X_{(k)}<x_k+\Delta x_k\right))}{\Pi_{k=1}^n\Delta x_k}=n!\Pi_{k=1}^nf_X(x_k)=n!
$$
