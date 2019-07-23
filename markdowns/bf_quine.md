# BF quine

Let's start our BF quine. What to we need ?
* A data block
* A way to replicate the data block as data
* A way to print the data block, as contents

Given a data block as an array of chars, it's not really complex to do the 3rd part : for each char in memory, print it.

The second part is a bit more complex. Let's have in memory value 44 for example, how can we write code to generate 44?

There is no need to find a complex solution to this (with multiplications 4x11 or similar). Let's just have 44 times '+', then '>' to move to the next cell.

# Let's start

* Memory: empty
* Cursor: first cell
* Input: any

# Process

* Leave 4 empty cells
* Data definition - to be competed - a set of '+' and '>' that will fill memory
* Generate and print '>' 4 times (the first "Leave 4 empty cells" command)
* Then go to data array first cell
* Generate just before values 43(+) and 62(>)
* For each cell
  * Move 3 cells to the left, and on every +1/-1 step print the 43(+)
  * Print the 62(>)
  * Move the 43 and 62 one cell on the right
* Loop
* Go to array first cell
* For each cell
  * print char
* Loop

# Code
```
>>>>                               leave 4 empty cells
$$$data definition$$$              to be completed
++++++++[->++++++++<]>--....[-]    print (62) 4 times
<<[<]<                             go 2 cells before array
<++++++++[->+++++>++++++++<<]      generate 40 and 64
>+++>-->                           then 43 and 62 and got to first data cell
[                                  for each cell
  [-<<<+>.>>]                      move value 3 cells on the left and print 43 each time
  <.                               print 62
  [->+<]<[->+<]                    moves 43 and 62 on the right
>>>]                               loop
<<<<[<]>                           Go to first array cell
[.>]                               For each cell print char

```

# Minified version
```
>>>>$$$data definition$$$++++++++[->++++++++<]>--....[-]<<[<]<<++++++++[->+++++>++++++++<<]>+++>-->[[-<<<+>.>>]<.[->+<]<[->+<]>>>]<<<<[<]>[.>]
```

# Final state

* Memory: some garbage data
* Cursor: after the data array
* Input: unchanged
* Output: unchanged
