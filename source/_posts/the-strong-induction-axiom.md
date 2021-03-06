title: The Strong Induction Axiom
url: 331.html
id: 331
categories:
  - Math
date: 2014-05-24 14:48:49
tags:
---
These are notes taken from the Lec 3 | MIT 6.042J Mathematics for Computer Science, Fall 2010 video lecture, which can be found at [https://www.youtube.com/watch?v=NuGDkmwEObM#t=4658](https://www.youtube.com/watch?v=NuGDkmwEObM#t=4658) 

What exactly does the Strong in Strong Induction mean? Let $P(n)$ be any predicate. if $P(0)$ is true then $\\forall n (P(0) \\wedge P(1) \\wedge \\ldots \\wedge P(n)) \\Rightarrow P(n+1)$ is true, then $\\forall n : P(n)$ is true. Remember the normal induction axiom? Let $P(n)$ be a predicate. If $P(0)$ is True and $\\forall n \\in \\mathbb{N} : (P(n) \\Rightarrow P(n+1))$ is True, then $\\forall n \\in \\mathbb{N}$ $P(n)$ is True. The difference is that you're assuming that all the cases starting from the base case til $n$ are true, in order to prove that $P(n+1)$ is true. The Unstacking game is demonstrated: here's a brief recap (no, actually, this is just another LaTex exercise for me) 

<script type="text/tikz">
    \begin{tikzpicture}[level distance=1.5cm, level 1/.style={sibling distance=5.5cm}, level 2/.style={sibling distance=2.5cm}, level 3/.style={sibling distance=1.2cm}, level 4/.style={sibling distance=1.5cm}]
    \tikzstyle{every node}=[minimum size=1cm,draw] [+preamble] 

    \node (Root) {8} 
	child { 
		node {4} 
		child { 
			node {2} 
			child { 
				node {1} 
			} 
			child { 
				node {1} 
			} 
		} 
		child { 
			node {2} 
			child { 
				node {1} 
			} 
			child { 
				node {1} 
			} 
		} 
	} 
	child { 
		node {4} 
		child { 
			node {3} 
			child { 
				node {2} 
				child { 
					node {1} 
				} 
				child { 
					node {1} 
				} 
			} 
			child { 
				node {1} 
			} 
		} 
		child { 
			node {1} 
		} 
	};
  
  \end{tikzpicture}
</script>

The score one would get is (4\*4)+(2\*2)+(3\*1)+(1\*1)+(1\*1)+(2\*1)+(1\*1) = 28. There must be a strategy to beat this, is there? 

<script type="text/tikz">
    \begin{tikzpicture}
  \usetikzlibrary{trees} [preamble] \tikzstyle{every node}=[minimum size=1cm,draw] \node (Root) {8} child { node {7} child { node {6} child { node {5} child {node {4} child {node {3} child {node {2} child {node {1} } child {node {1} } } child {node {1} } } child {node {1} } } child {node {1} } } child { node {1} } } child {node {1} } } child {node {1} }; 
  \end{tikzpicture}
</script>

(7\*1)+(6\*1)+(5\*1)+(4\*1)+(3\*1)+(2\*1)+(1\*1) = 28. Now one should immediately jump to the conclusion (if one is an MIT student) that all combinations lead to a score of 28. But one is not if one is reading this, so: Theorem: All strategies $S(n)$ for the Unstacking Game with $n$ starting blocks lead to the same score. Proof by strong induction: Inductive Hypothesis: $P(n)$ is the Theorem. Base Case: $S(1)$ is zero (One can't play the game with 0 blocks). Inductive step: Assume $P(1), P(2), \\ldots, P(n)$ in order to prove $P(n+1)$. With $(n+1)$ blocks, for $1 \\leq k \\leq n$: 

<script type="text/tikz">
\begin{tikzpicture} \usepackage{tikz} \usetikzlibrary{trees} \node (Root) {n+1} child {node {k}} child {node {n+1-k}}; \end{tikzpicture} 
</script>

Our score for $P(n+1)$ is $k(n+1-k)+P(k)+P(n+1-k)$ (think recursion, after each division of blocks each block is an instance of the Game). One has hit a dead end here, as one is trying to prove that $P(n+1)$ is dependent on $n$, not $k$. Honestly this example (IMHO) is rather haphazard, as the next step, which not so intuitively, is to make a good guess as to what $S(n)$ might be, and in classic MIT intuition style, our first guess yields $\\frac{n(n-1)}{2}$. Testing a few values of $n$.. $S(2) = 1$, $S(3) = 3$, $S(4) = 6$, $S(8) = 28$. Let's put $P(n)$ through its runs again.... Base case, where $P(n) = \\frac{n(n-1)}{2}$: $P(1) = 0$. Going back to the previous expression which we derived for the score, now that we have an expression for $P(n)$: $k(n+1-k) + \\frac{k(k-1)}{2} + \\frac{(n+1-k)(n-k)}{2}$ Simplifying this expression (aka plugging it into WolframAlpha...) results in $\\frac {n(n+1)}{2}$, which is $S(n+1)$. In the words of the professor, "_The_ $k$ _disappears._" We have worked backwards (to my understanding), deriving an expression for the score, reaching a dead end, where we have to stop assuming ($k$), come up with an expression for $P(n)$, and filling in the blank to prove $P$(or $S$)$(n+1)$.