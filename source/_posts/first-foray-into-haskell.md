---
title: First foray into Haskell.
url: 429.html
id: 429
categories:
  - Math
  - Programming
date: 2014-07-30 04:11:28
tags:
---

Defining the combination formula (nCr) recursively.

Prelude> let ncr n k | k == 0 = 1 | n == k = 1 | otherwise = ncr (n-1) k + ncr (n-1) (k-1)
Prelude> ncr 3 2
3
Prelude> ncr 15 4
1365

This works because [http://www.cs.nott.ac.uk/~vxc/g51mcs/ch05_combinatorics.pdf](http://www.cs.nott.ac.uk/~vxc/g51mcs/ch05_combinatorics.pdf) , page 9.