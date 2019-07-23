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
        char[] code = new char[]{/*** to be replaced ***/};
        boolean comma = false;
        System.out.println("public class Quine {");
        System.out.println("    public static void main(String[] args) {");
        System.out.print("        char[] code = new char[]{");
        for(char c : code){if(comma)System.out.print(','); comma = true; System.out.print("'" + (c=='\''||c=='\\' ? "\\"+c : c == '\n' ? "\\n": c) +"'");}
        for(char c : code)System.out.print(c);
}}
```
Ok, so this program:
* Declares an array, and a boolean value
* Prints some lines (from our source code)
* Then (_this is the trick_) prints array contents as comma-separated chars
* And finally (_this is the second part of the trick_) prints array contents as chars


Now, let's suppose our array contains chars from the end of the comment to the end of the program. Our program will then
* first, print the source code beginning up to the array definition
* then prints array contents from array itself
* then prints end of source code, using array as well

Okay....

_Note_: we handle special chars like quotes, backslashes or carriage returns differently in the code

So, now, let's create an array of chars from '];' on third line up to the end of the program (and escape quotes, backslashes and carriage returns...).

```java
public class Quine {
    public static void main(String[] args) {
        char[] code = new char[]{'}',';','\n',' ',' ',' ',' ',' ',' ',' ',' ','b','o','o','l','e','a','n',' ','c','o','m','m','a',' ','=',' ','f','a','l','s','e',';','\n',' ',' ',' ',' ',' ',' ',' ',' ','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','l','n','(','"','p','u','b','l','i','c',' ','c','l','a','s','s',' ','Q','u','i','n','e',' ','{','"',')',';','\n',' ',' ',' ',' ',' ',' ',' ',' ','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','l','n','(','"',' ',' ',' ',' ','p','u','b','l','i','c',' ','s','t','a','t','i','c',' ','v','o','i','d',' ','m','a','i','n','(','S','t','r','i','n','g','[',']',' ','a','r','g','s',')',' ','{','"',')',';','\n',' ',' ',' ',' ',' ',' ',' ',' ','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','(','"',' ',' ',' ',' ',' ',' ',' ',' ','c','h','a','r','[',']',' ','c','o','d','e',' ','=',' ','n','e','w',' ','c','h','a','r','[',']','{','"',')',';','\n',' ',' ',' ',' ',' ',' ',' ',' ','f','o','r','(','c','h','a','r',' ','c',' ',':',' ','c','o','d','e',')','{','i','f','(','c','o','m','m','a',')','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','(','\'',',','\'',')',';',' ','c','o','m','m','a',' ','=',' ','t','r','u','e',';',' ','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','(','"','\'','"',' ','+',' ','(','c','=','=','\'','\\','\'','\'','|','|','c','=','=','\'','\\','\\','\'',' ','?',' ','"','\\','\\','"','+','c',' ',':',' ','c',' ','=','=',' ','\'','\\','n','\'',' ','?',' ','"','\\','\\','n','"',':',' ','c',')',' ','+','"','\'','"',')',';','}','\n',' ',' ',' ',' ',' ',' ',' ',' ','f','o','r','(','c','h','a','r',' ','c',' ',':',' ','c','o','d','e',')','S','y','s','t','e','m','.','o','u','t','.','p','r','i','n','t','(','c',')',';','\n','}','}','\n'};
        boolean comma = false;
        System.out.println("public class Quine {");
        System.out.println("    public static void main(String[] args) {");
        System.out.print("        char[] code = new char[]{");
        for(char c : code){if(comma)System.out.print(','); comma = true; System.out.print("'" + (c=='\''||c=='\\' ? "\\"+c : c == '\n' ? "\\n": c) +"'");}
        for(char c : code)System.out.print(c);
}}
```
Tadaaaaa

A quine, in Java. Now, let's talk about BF :)

_Note_ : to avoid complex char escapes, we may have stored our data into integers instead of chars.


