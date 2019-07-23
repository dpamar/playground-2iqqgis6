# Data definition

Now, let's generate the data part. As explained, it's
* the whole source code, starting just after data definition
* and it should be encoded with successive '+' followed by '>' for each char

Not very optimal, but easy to write ;)

This is the part we want to encode
```
++++++++[->++++++++<]>--....[-]<<[<]<<++++++++[->+++++>++++++++<<]>+++>-->[[-<<<+>.>>]<.[->+<]<[->+<]>>>]<<<<[<]>[.>]
```

Let's write a BF tool that generates the data from any input


# Let's start

* Memory: empty
* Cursor: first cell
* Input: some code to convert

# Process

* Let's be smart and first generate 43 (+) and 62 (>)
* For each value in input
  * Print 43 as many times as needed
  * print 62
* Loop

# Code
```
++++++++[->+++++>++++++++<<]>+++>--<<   Generate 43 and 62
,[                                      For each value in input
  [->.<]                                Print 43 as many times as needed
  >>.                                   print 62
<<,]                                    Loop
```

# Minified version
```
++++++++[->+++++>++++++++<<]>+++>--<<,[[->.<]>>.<<,]
```

# Final state

* Memory: 0, 43, 62
* Cursor: on first cell
* Input: empty (read)
* Output: our data definition bloc
