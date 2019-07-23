# 2-step-quine

_Note_: A 2-step-quine is *not*
* a standard name, I decided this name on my own
* a multiquine, which is something completely different - that I'll present in a future playground :)

So, let's call a 2-step quine a program P that, when executed, produces a _different_ program Q, and this program Q when executed produces the original program P.

`P -> Q -> P`. 2 steps.

# Proof

We can use the same fixed point theorem to prove that at least one 2-step-quine exists.

_Well, actually, at least 2 of them exists, because P produces Q that produces P and Q produces P that produces Q..._

So, let's have a computable transformation named _H_ that, for any computable function F, prints, for each line of F source code, a _print_ instruction of this same line.

By construction, executing G = H(F) produces F source code.

Let's apply the fixed point theorem now : there is a program P that does the same job than H(P). In other words
* P generates Q=H(P)
* Q generates P by construction
`P -> Q -> P`. Q.E.D.

# The other way...

The proof is smart, and gives a way to build a 2-step-quine, but this may be a bit too complex, especially in BF. Printing instructions is expensive.

Instead, let's consider this other version of a 2-step-quine, that does not leverage the proof of existence but rather the method used in the previous steps

```java
public class TwoStepQuine1 {
    public static void main(String[] args) {
        char[][] code = new char[][]{new char[]{/*** to be replaced 1***/},new char[]{/*** to be replaced 2***/}};
        boolean comma = false;
        System.out.println("public class TwoStepQuine2 {");
        System.out.println("    public static void main(String[] args) {");
        System.out.print("        char[][] code = new char[][]{new char[]{");
        for(int i : code[0]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        System.out.print("},new char[]{");
        comma = false;
        for(int i : code[1]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        for(int i : code[1]) System.out.print((char)i);
}}
```

```java
public class TwoStepQuine2 {
    public static void main(String[] args) {
        char[][] code = new char[][]{new char[]{/*** to be replaced 1***/},new char[]{/*** to be replaced 2***/}};
        boolean comma = false;
        System.out.println("public class TwoStepQuine1 {");
        System.out.println("    public static void main(String[] args) {");
        System.out.print("        char[][] code = new char[][]{new char[]{");
        for(int i : code[0]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        System.out.print("},new char[]{");
        comma = false;
        for(int i : code[1]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        for(int i : code[0]) System.out.print((char)i);
}}
```

See ? Only 3 chars change
* class name on first line
* target class name line 5
* code[] index one line before end

After the whole quine steps, we understand that this program prints data for both parts, then prints code from data, either first or second part.

Let's grab all the code from 2nd program after the last comment, convert into comma-separated integers : this will be the first array. Let's do the same with 1st program to generate the second array.

Here is the result

```java
public class TwoStepQuine1 {
    public static void main(String[] args) {
        char[][] code = new char[][]{new char[]{125,125,59,10,32,32,32,32,32,32,32,32,98,111,111,108,101,97,110,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,112,117,98,108,105,99,32,99,108,97,115,115,32,84,119,111,83,116,101,112,81,117,105,110,101,50,32,123,34,41,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,32,32,32,32,112,117,98,108,105,99,32,115,116,97,116,105,99,32,118,111,105,100,32,109,97,105,110,40,83,116,114,105,110,103,91,93,32,97,114,103,115,41,32,123,34,41,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,34,32,32,32,32,32,32,32,32,99,104,97,114,91,93,91,93,32,99,111,100,101,32,61,32,110,101,119,32,99,104,97,114,91,93,91,93,123,110,101,119,32,99,104,97,114,91,93,123,34,41,59,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,48,93,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,105,41,59,125,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,34,125,44,110,101,119,32,99,104,97,114,91,93,123,34,41,59,10,32,32,32,32,32,32,32,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,49,93,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,105,41,59,125,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,49,93,41,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,40,99,104,97,114,41,105,41,59,10,125,125},new char[]{125,125,59,10,32,32,32,32,32,32,32,32,98,111,111,108,101,97,110,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,112,117,98,108,105,99,32,99,108,97,115,115,32,84,119,111,83,116,101,112,81,117,105,110,101,49,32,123,34,41,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,108,110,40,34,32,32,32,32,112,117,98,108,105,99,32,115,116,97,116,105,99,32,118,111,105,100,32,109,97,105,110,40,83,116,114,105,110,103,91,93,32,97,114,103,115,41,32,123,34,41,59,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,34,32,32,32,32,32,32,32,32,99,104,97,114,91,93,91,93,32,99,111,100,101,32,61,32,110,101,119,32,99,104,97,114,91,93,91,93,123,110,101,119,32,99,104,97,114,91,93,123,34,41,59,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,48,93,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,105,41,59,125,10,32,32,32,32,32,32,32,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,34,125,44,110,101,119,32,99,104,97,114,91,93,123,34,41,59,10,32,32,32,32,32,32,32,32,99,111,109,109,97,32,61,32,102,97,108,115,101,59,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,49,93,41,123,105,102,40,99,111,109,109,97,41,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,39,44,39,41,59,32,99,111,109,109,97,32,61,32,116,114,117,101,59,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,105,41,59,125,10,32,32,32,32,32,32,32,32,102,111,114,40,105,110,116,32,105,32,58,32,99,111,100,101,91,48,93,41,32,83,121,115,116,101,109,46,111,117,116,46,112,114,105,110,116,40,40,99,104,97,114,41,105,41,59,10,125,125}};
        boolean comma = false;
        System.out.println("public class TwoStepQuine2 {");
        System.out.println("    public static void main(String[] args) {");
        System.out.print("        char[][] code = new char[][]{new char[]{");
        for(int i : code[0]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        System.out.print("},new char[]{");
        comma = false;
        for(int i : code[1]){if(comma)System.out.print(','); comma = true; System.out.print(i);}
        for(int i : code[1]) System.out.print((char)i);
}}
```

Testing script:
```bash
javac TwoStepQuine1.java && java TwoStepQuine1 > TwoStepQuine2.java && javac TwoStepQuine2.java && java TwoStepQuine2 | diff TwoStepQuine1.java -
```

This other way of building 2-step-quine works fine with Java, let's apply to BF :)
