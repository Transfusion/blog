---
title: Proof by contradiction (aka a LaTeX test)
url: 319.html
id: 319
categories:
  - Musings
  - Programming
date: 2014-05-21 22:46:23
tags:
---

\[latexpage\] What is a proof by contradiction? A proof by contradiction is if $\\neg P \\Rightarrow F$ is true. One assumes that a proposition P is False, and uses that to derive until a contradiction is reached, which can't be True. A popular example: Let's prove that $\\sqrt2$ is irrational. An irrational number is something that cannot be expanded into a fraction. (A common misconception is that Pi is $\\frac{22}{7}$ and therefore rational; no it is not exactly $\\frac{22}{7}$. See [http://mathworld.wolfram.com/PiFormulas.html](http://mathworld.wolfram.com/PiFormulas.html) Assume that $\\sqrt2$ is rational; such that we can represent it as $\\frac{a}{b}$, where $\\frac{a}{b}$ is a fraction in lowest terms. $\\Rightarrow \\sqrt2 = \\frac{a}{b}$ $\\Rightarrow 2 = \\frac{a^2}{b^2}$ $\\Rightarrow 2b^2 = a^2$ $\\Rightarrow 2 \\mid a$ $\\Rightarrow 4 \\mid a^2$ $\\Rightarrow 4 \\mid 2b^2$ $\\Rightarrow 2 \\mid b^2$ $\\Rightarrow 2 \\mid b$ If both $a$ and $b$ are even, they are not in lowest terms, as both can be divided by 2 for further simplification. Hence we have a contradiction. $\\square$