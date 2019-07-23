# Quine theory

As stated before, any Turing-complete language admits (at least) one quine.

The complete proof is quite long, but if we rely on some theorems, we can introduce a kind of short proof that would help us to understand how to code a quine, including a BF quine.

# Definitions and theorems

_Note: these definitions and theorems might not be the exact ones but a reduced version, enough to understand the proof_

* A computable function _N_ is a function that can be computed using a Turing-complete language. We will use functions with integer parameters (0 or more)
* Any computable function _N_ can be related to an integer _n_ in an _injective_ way (one function : one integer; and one integer : at most one function)
  * E.g. our source code can be considered as a set of chars, themselves a huge amount of bits, aka a number in its binary form
* The _Universality theorem_ states that a computable function exists, named _U_, such that _U(n)_ does the same job than _N()_
  * This is what we called an _interpreter_.
  * In other words, from a number, we can execute the corresponding program, if it exists (remember: _injective_ way, so some integers may be invalid)
* The _parameterization theorem_, also called _smn theorem_ states that a computable function _S_ such that, for any integers _n_ and _m_, _s(n,m)_ does the same job than _N(m)_
  * In this application, _m_ is a fixed parameter of _N_
* Let's call _H_ a computable function over (valid) integers, called transformation
  * In other words, we transform a program identification number into another program's one

# Let's start

Let's first prove there H admits a fixed point

* Consider a computable function _N_ and its identification number _n_
* Consider _S(n,n)_, the computable function obtained when executing _N(n)_, _N_ with a fixed parameter value which is its one identification number _n_
* Consider _H(S(n,n))_, the computable function obtained when transforming by _H_ the computable function _N(n)_
* Let's have an integer _m = H(S(n,n))_. Such _H(S(n,n))_ is a computable function, with a single parameter _n_, and this function will be called _M_, identified by its number _m_
* Thanks to the universality theorem, if we know _m_, we can execute _M_
* Now, consider _M(m)_
  * By definition, _M(m) = S(m,m)_
  * By construction, _M(m) = H(S(m,m))_
* Conclusion : _S(m,m)_ is a fixed point of computable function _H_

# Apply to quine

Let's now say _H_ is the function with a parameter _n_, that prints source code of program _N_.

We proved that there is at least one computable function, named _quine_ that is a fixed point of _H_, so _quine_ and _H(quine)_ do the same job.

What does _H(quine)_ does ? It displays _quine_ source code. So _quine_ does the same, and prints its own source code.

# Quine construction

In order to get a quine, we saw that we need a function _M_, given by its value _m_. This means we needs in theory an interpreter to do that.

Actually, we can restrict this to an interpreter able to interpret _m_ which is _H(...)_. So our source code needs to be able to interpret _H_ at least - other functions are not really mandatory.

And as our _H_ is "Print source code of given program", then it's quite easy to implement.

* First, we need to declare a _data_ part in our code
* Then a function H to print the _data_ as _data declaration_
* Finally, print the _data_ as _contents_

