# Welcome!

Welcome to this new playground about the BF language. Make sure you already read 
* [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome)
* [BrainFuck part 2 - Working with arrays](https://tech.io/playgrounds/50443/brainfuck-part-2---working-with-arrays/welcome)
* [BrainFuck part 3 - Write a BF interpreter in BF](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 4 - Advanced maths](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 5 - Math sequences](https://www.codingame.com/playgrounds/50478/brainfuck-part-5---math-sequences/welcome)
* [BrainFuck part 6 - 16-bit integers]()

playgrounds if you didn't already !

The goal of this playground is to create our own _quine_ using BF.


# Wait... what?

* A _quine_.
* Who's this guy ?

Actually, it can be both who, and what.
  * [Willard Van Orman Quine](https://en.wikipedia.org/wiki/Willard_Van_Orman_Quine) was an american logician
  * A quine is a kind of computer program that prints its own source code, named after Willard Van Orman Quine


# Ok I'm sure I can create my own quine

* Be my guest
* Ok let me try using Java 

```java
public class Quine {

    public static void main(String[] args) {
        System.out.println("public class Quine {");
        System.out.println();
        System.out.println("public static void main(String[] args) {");
        System.out.println("System.out.println(\"public class Quine {\");");
        
    }
}
```

* DAMNED !!!

Yes, actually there is a trick

# No, this thing is just not possible !

Actually it is. It can even be proved that any Turing-complete language has quines.

There is a "yet another theorem named Fixed-Point theorem" that states that, for any computable function F applied on computable functions, there is a program P so that P (the program) and F(P) (the transformed program) are doing the same thing.

Based on this theorem, let's consider a function PrintCode(...) that prints code of any computable function. Previous theorem states for at least one computable program P, PrintCode(P) and P are doing the same job. PrintCode(P) prints P source code, so P as well prints its own source code. _Q.E.D._

# So, any Turing-complete language has a quine ?

Yes, as long as any computable function can be implemented. But obviously, there is a trick...

```java
public class Quine {
    public static void main(String[] args) {
        char[] code_1 = new char[]{/*** to be completed ***/};
        char[] code_2 = new char[]{/*** to be completed ***/};
        boolean comma = false;
        for(char c : code_1)System.out.print(c);
        for(char c : code_1){if(comma)System.out.print(','); comma = true; System.out.print((int)c);}
        System.out.println("};");
        System.out.println("        char[] code_2 =new char[]{");
        comma = false;
        for(char c : code_2){if(comma)System.out.print(','); comma = true; System.out.print((int)c);}
        for(char c : code_2)System.out.print(c);
}}
```
Ok, so this program:
* Prints some chars from an array
* Prints some integers comma separated from the same array
* Prints a couple of lines
* Prints some integers comma separated from another array
* Prints some chars from the same second array


Now, let's suppose our first array contains ASCII codes from the first char of our program up to the first comment. Then, the program will
* first, print the source code beginning up to the first array definition
* then, completes first array definition using array itself

Okay.... Then, we understand what second array should contain : all the ASCII codes from the last comment to the end of the program ! 

```java
public class Quine {
     public static void main(String[] args) {
         char[] code_1 =new char[]{112,117,98,108,105,99,32,99,108,97,115,115,32,81,117,105,110,101,32,123,10,32,32,32,32,32,112,117,98,108,105,99,32,115,116,97,116,105,99,32,118,111,105,100,32,109,97,105,110,40,83,116,114,105,110,103,91,93,32,97,114,103,115,41,32,123,10,32,32,32,32,32,32,32,32,32,99,104,97,114,91,93,32,99,111,100,101,95,49,32,61,110,101,119,32,99,104,97,114,91,93,123};
        char[] code_2 =new char[]{
125,59,10,32,32,32,32,32,32,32,32,98,111,111,108,101,97,110,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,102,111,114,40,99,104,97,114,32,99,32,58,32,99,111,100,101,95,49,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,99,41,59,10,32,32,32,32,32,32,32,32,102,111,114,40,99,104,97,114,32,99,32,58,32,99,111,100,101,95,49,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,40,105,110,116,41,99,41,59,125,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,125,59,34,41,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,32,32,32,32,32,32,32,32,99,104,97,114,91,93,32,99,111,100,101,95,50,32,61,110,101,119,32,99,104,97,114,91,93,123,34,41,59,10,32,32,32,32,32,32,32,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,102,111,114,40,99,104,97,114,32,99,32,58,32,99,111,100,101,95,50,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,40,105,110,116,41,99,41,59,125,10,32,32,32,32,32,32,32,32,102,111,114,40,99,104,97,114,32,99,32,58,32,99,111,100,101,95,50,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,99,41,59,10,125,125};
        boolean comma = false;
        for(char c : code_1)System.out.print(c);
        for(char c : code_1){if(comma)System.out.print(','); comma = true; System.out.print((int)c);}
        System.out.println("};");
        System.out.println("        char[] code_2 =new char[]{");
        comma = false;
        for(char c : code_2){if(comma)System.out.print(','); comma = true; System.out.print((int)c);}
        for(char c : code_2)System.out.print(c);
}}
```
Tadaaaaa

A quine, in Java. Now, let's talk about BF :)
