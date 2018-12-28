title: My first foray into Brainfuck
url: 222.html
id: 222
categories:
  - Programming
date: 2014-03-09 02:02:46
tags:
---
Print damned.
```py
print "damned"
```

Obfuscate it.
```py
print 'qnzarq'.decode('rot13')
```

Now print "damned" in Brainfuck, and let's play codegolf.

```brainfuck
++++++++++[>++++++++++>+++++++++++<<-]>.---.>-.+.<++++.-.
```

Challenge accepted.
```brainfuck
-[>++>++>++<<<-----]>--.---.>+++++++.+.>-.-.
```

[http://www.iamcal.com/misc/bf_debug/](http://www.iamcal.com/misc/bf_debug/) Debugger to help you visualize what's going on. The first brainfuck works by incrementing the first cell to 10, then the loop increments the second cell to 100 and the 3rd cell to 110, and the <<- decrements the loop "counter", which is held by the first cell.

At the end of the loop we should have [0][100][110]. Everything after the loop just increments or decrements to the appropriate ascii decimal value and outputs to stdout. 

[http://www.asciitable.com/](http://www.asciitable.com/) The second one works by first decrementing the value of the first cell, which is 0; hopefully the bf interpreter will wrap around to 255. Not all bf interpreters do this; [https://apps.ubuntu.com/cat/applications/saucy/bf/](https://apps.ubuntu.com/cat/applications/saucy/bf/) does but [http://swapped.cc/#!/bff](http://swapped.cc/#!/bff) doesn't. 

Since the ascii decimal codes of the letters d, m, n, e, d are all in between 100 and 110 (a is 97), the shortest way I could think of was to have a big number to use as the loop counter and decrement it in intervals. 102 is 40% of 255, or 2/5ths, so after incrementing twice for cells 1, 2, and 3 go back to cell 0 and decrement by 5. At the end of the loop we should have [0][102][102][102]. 

Some interesting bf-related links: 

[https://stackoverflow.com/questions/16836860/how-does-the-brainfuck-hello-world-actually-work](https://stackoverflow.com/questions/16836860/how-does-the-brainfuck-hello-world-actually-work)
[http://esoteric.sange.fi/brainfuck/impl/interp/i.html](http://esoteric.sange.fi/brainfuck/impl/interp/i.html) 
[http://esolangs.org/wiki/Brainfuck_algorithms](http://esolangs.org/wiki/Brainfuck_algorithms) add, dup, swap, mul, if implemented in bf. 

[http://www.reddit.com/r/tinycode/comments/1oqgwm/shortest_hello_world_brainfuck_code/](http://www.reddit.com/r/tinycode/comments/1oqgwm/shortest_hello_world_brainfuck_code/)