# Programming for Philosophers

## Introduction

It is a shame that philosophy undergraduates are, traditionally, not given any exposure to programming. Not only is programming
a ubiquitously applicable skill in the modern age, but so much of it is deeply rooted in the tradition of mathematical 
and philosophical logic. This project is the start of a textbook which teaches declarative programming and its application
to areas in philosophy.

## Structure and Content

In this book we are going to cover three programming languages: Prolog, Scheme, and Haskell. Each of these languages have
foundations woven from the intersection of philosophy, logic, mathematics, and theoretical computer science. There are formal
logico-mathematical systems on which these languages are based, and these systems are used "by hand", as it were, in their 
respective fields. Yet, Prolog, Scheme, and Haskell are programming languages, which means they are computational systems which 
allow you to run and write code on your computer. They are not just systems of deduction which need to be tediously written out 
on paper in order to be used; they are logical systems which can be automated by a computer.

The book has five main sections. The first is an obligatory preliminary section reviewing (without great depth) the necessary
prerequisite mathematical and logical facts which will be assumed as understood throughout the text. The next three are the core 
material about each respective language. The last section is a conclusion, summing up what has been discussed and pointing 
towards future avenues to be traveled by the curious. Each of the language sections is structured as follows:

1. An introduction to the formalism underlying the language.
2. An introduction to programming in the language.
3. Applications of the language to problems in philosophy.

The introduction to the formalism chapters will be the heaviest parts of the book. They exist to place the programming languages
into formal context, so that the connections between logic, programming, and philosophy can be appreciated. They also have an 
added bonus of being a perfect place to introduce historical context and pay deference to the intellectual history out of which
the languages and systems developed.

The introduction to the languages themselves will include multiple parts. First, there will be logistics, i.e., how to download
the languages, how to get the systems to run the programs you write, best practices for saving your files, and so on. Each of
the languages have free, open source implementations which we will use, and each of these implementations have a powerful
way of interacting with the code you write in a live setting so that you can get immediate feedback on the code's correctness.
Then, we will dive into the languages themselves, learning their syntax, their control structures, and how to get them to do
what we want. Important asides on best practices for each language will be included, because, as you will see, although there
are core ideas behind each programming language which are fundamentally the same, the surface of each language can seem alien
and unforgivingly dissimilar to that of the others. Testing is one of the most important aspects of programming, and so
a quick and easy way to set up tests for your programs is also covered in these sections. Finally, as a summation of the 
chapter, there is a final cheat-sheet for the language. Programmers look things up all the time, and it's more common than not
to have a document explaining what every piece of code you're using in your project open on your screen while you write your
own code. This is in stark contrast to the rarity of being allowed a formula sheet in math class. Programming is not done by
memorizing every part of the language; it's done by internalizing how to use the language, and so it is perfectly fine to have a 
cheat-sheet there to remind you of the syntax and predefined functions which make up the language. None of those are interesting
things to memorize, anyway. The fun, and challenging, part of programming is understanding how to put all of those things together
to write a program that does what you want it to do. So, the cheat-sheet is provided for each language to be used whenever 
necessary.

The applications section is where we cover what we can actually do with the language, as it relates to philosophy. Some necessary
background on the philosophical topic/problem will be introduced, and then we will work through implementing a system as a
program which allows us to solve, or otherwise create a computational model with with we can experiment with, the problem. The
full code itself will be available on Github.

Below is a brief explication of these three sections for each of our programming languages, as well as a very cursory overview
of what the languages look like and how we interact with them.

### Prolog

Prolog is a logic programming language, and indeed the name derives from the phrase "programming in logic". Prolog is a 
form of first-order logic which uses Horn-clauses to represent logical formulae, and resolution as the deductive system.
The first section in this part of the book will review basic facts about first-order logic, and then introduce the 
subset that comprises Prolog's syntax, as well as how resolution works and how it differs from a more common type of
deductive system such as natural deduction or sequent calculus.

SWI-Prolog is an industry standard implementation of Prolog and it is what we will be using. SWI-Prolog comes with an
interactive environment which allows us to run Prolog code directly. Prolog, and logic programming in general, involves
writing a series of logical facts and inference rules in a sort of database, and then querying that database for answers
to questions involving those facts and their implications. The database can be written using a text editor and then loaded
into the SWI-Prolog interactive environment, where we than can ask it questions and have it compute results for us. 

A simple example of a set of rules and facts might look like this:

    loves(romeo, juliet).
    loves(Y, X) :- loves(X, Y).

The interpretation of the first line is that the two place relation loves is true of two objects, romeo and juliet. The second
and third line are how we form inference rules. This rule says that an object Y stands in the love relation to the object X,
just in case the object X stands in the love relation to the object Y. Or, in English, if X loves Y then Y loves X. This might
not be true in the real world, but we've told Prolog it is so, and so Prolog will reason as if it is. Now, if we load this
into SWI-Prolog we can start to ask it questions about our facts. Queries are represented textually by ?- followed by the query,
with the answer Prolog gives us underneath. So, if we ask Prolog whether romeo loves juliet:

    ?- loves(romeo, juliet).
    true .

We find that indeed this is the case. Which is good, because that was the fact we started with! We can also ask if there is any
object which romeo loves:

    ?- loves(romeo, X).
    X = juliet .

and Prolog fills the variable in which the object which, according to our facts and rules, satisfies the relation. So what about
our rule, then? If our rule is correct, then juliet should love romeo:

    ?- loves(juliet, romeo).
    true .

which confirms that our rule works how we would hope it does. This is a basic overview of what interacting with Prolog code
looks like.

Some of the first applications of Prolog were related to automated reasoning and artificial intelligence. Expert systems are
a combination of a "knowledge base" and an "inference engine" which can reason about and give answers to questions involving 
complicated domains of knowledge, acting as an "expert" with which we are consulting. Prolog has been one of the most commonly 
used programming languages for expert systems since its inception. In this book, we are going to use Prolog to create a sort of 
expert system dealing with epistemic and doxastic logic. Epistemic logic is a modal logic, that is, a logic
which includes operators which represent some sort of modality such as necessity, knowledge, temporality, and so on, which models 
the logic of knowledge. Doxastic logic similarly models the logic of belief. An important part of belief is that it is 
non-monotonic, meaning that we might believe something, but once we gain new beliefs, we can revise our beliefs and change them. 
This is starkly different than reasoning in a system of pure logic, which is inherently monotonic (that is, proving something new
will never "unprove" something already proven). We will use Prolog to model these cases of nonmonotonic "belief revision" to 
accurately model dynamic epistemic and doxastic agents (knowers and believers) in order to ask it for solutions to classical 
philosophical problems in epistemology such as
[the muddy children puzzle](https://plato.stanford.edu/entries/dynamic-epistemic/appendix-B-solutions.html#muddy): 

"Three children are playing in the mud. Father calls the children to the house, arranging them in a 
semicircle so that each child can clearly see every other child. “At least one of you has mud on your forehead”, says Father. The 
children look around, each examining every other child’s forehead. Of course, no child can examine his or her own. Father 
continues, “If you know whether your forehead is dirty, then step forward now”. No child steps forward. Father repeats himself a 
second time, “If you know whether your forehead is dirty, then step forward now”. Some but not all of the children step forward. 
Father repeats himself a third time, “If you know whether your forehead is dirty, then step forward now”. All of the remaining 
children step forward. How many children have muddy foreheads?"

Our Prolog program will be able to give us the answer to this problem, and myriad others, near instantaneously.

### Scheme

Scheme is a functional programming language. Functional programming languages are formally based on a system of computation called
the lambda calculus. The lambda calculus is a formal system that consists solely of functions, variables, and function
application. This foundations section will review the lambda calculus, how it forms a mathematical model of computation, and some
of the more interesting philosophical issues surrounding names, reference, and when we can actually say that two functions
are equivalent.

Scheme is a member of the Lisp family of programming languages. The original Lisp language was designed to be an elegant
implementation of the lambda calculus, however certain aspects of the language were not handled correctly (namely, the 
issues surrounding names, reference, and functional equivalence alluded to earlier). Scheme was introduced as a new dialect
of Lisp which corrected these issues and brought the language closer to being a more user-friendly variant of the lambda
calculus. The implementation of Scheme we will be using is called Racket, and like Prolog, it comes with a system which
allows us to write code and immediately interact with it. This system is called a REPL, which stands for "Read, Evaluate,
Print, Loop" which is a perfect description of how the system works. In Scheme, every statement we can write has a value.
This is very similar to mathematics, "2" has a value, and so does "1 + 1" (and, of course, these two statements have the 
same value). When we write down an expression in the Scheme REPL, it evaluates the expression, prints the value, and then
loops, i.e., waits to read the next expression we give it. An example of an interaction we might have with the Scheme REPL 
is this:

    > (define a 5)
    a
    > (+ a a)
    10
    > (define (add-a x) (+ a x))
    add-a
    > (add-a 4)
    9

The lines starting with \> are the expressions we entered and the lines immediately under them are the printed value Scheme
returned to us. The first line shows how we can define variables to be the names of values, and in this case we tell Scheme
that the name "a" refers to the value 5. Scheme responds by telling us the value of the variable which we just defined.
Next, we tell Scheme we want to know the value of a + a, and, since a is a name for the value 5, Scheme gives us back 10.
You are probably wondering why the addition sign is on the left of both of its arguments. Scheme uses what's called Polish
Notation, which means that operators, like +, -, /, and * are written before their arguments. This will initially feel strange,
but you will get used to it. After all, we use Polish notation with all other mathematical functions (we write f(x, y) instead
of x f y, for instance). The second thing you are probably noticing is that there are a lot of parentheses. This is the most
distinctive feature of the Lisp family of languages, and we'll discuss it at length in the book proper. For now, the easiest
explanation is that parentheses are function application. If you want to apply a function to an argument, you surround the whole
thing with parentheses. If you have a function f that takes two arguments, x and y, you would tell Scheme to evaluate it and
give you the answer by typing (f x y). So, (+ a a) tells Scheme that we want to apply the addition function to a and a. The third
input is how we can define functions. We are telling Scheme that when it sees add-a being applied to an argument, it should
evaluate (+ a x), that is, evaluate the result of applying the addition function to a and whatever argument is passed in. Since
we just defined something, Scheme responds by telling us the value which was defined, just like with a before. Finally, our last
line is an application of our newly defined function to the value 4, and Scheme correctly tells us that a + 4 is 9. There is much 
more to say about Scheme, the parentheses, and the lambda calculus, but this is a basic overview of what a session with the Scheme
REPL looks like.

Scheme and the lambda calculus touch on many interesting topics at the center of theoretical computer science, recursion theory,
mathematical logic, and the philosophies of language and of mathematics. Names, lexical biding, scope, referential transparency,
direct and indirect reference, and quotation are merely a few. In the book, we will be using Scheme and its powerful quotation
system to study the ways in which natural and mathematical languages handle reference. There is a famous distinction between
use and mention in the philosophy of language. A word is used in a sentence when what the word contributes to the meaning
of the sentence is the words *meaning*. A word is mentioned in a sentence when the sentence talks *about* the word. A classic
example of the use of "dog" in a sentence is "dogs are mammals," whereas "'Dog' has three letters," is an example of 
mentioning the word. Quotation marks, and in this case even nested quotation marks, are integral to understanding the distinction
between use and mention. Usually, when we mention a word or phrase, we put it in quotations. Otherwise, it's hard to tell if we
are expressing the meaning of the word or phrase, or if we're talking about it itself. Scheme has a mechanism for quotation as
well. In Scheme, a value can be quoted by appending an apostrophe to it, like '6. This is not the value 6, it is a symbolic
representation of it. The philosopher W.V.O. Quine introduced the important distinction between regular quotation and what
we call quasi-quotation. Sometimes, we want to quote some part of an expression, but we don't want to quote all of it. For
instance, if you wanted to explain how we conjugate regular past tense verbs in English, we might be tempted to say they
have the form "verbed", trying to communicate that we add "ed" to the end of the bare infinitive form of the verb. However,
this is not correct, as it is literal quotation. If this were correct, that would mean that to say we went to the store, we
would have to say "We verbed to the store". Quasi-quotation is a mechanism whereby we can mark some parts inside of a quotation
as able to be changed, or instantiated with some value, while the rest is rigidly held in place. Scheme has a mechanism for
quasi-quotation as well, which means that we can easily talk about Scheme programs inside of Scheme itself. This allows us to
define a program in Scheme which takes a Scheme program as input and simulates it. This is analogous to a universal
Turing machine, which is a Turing machine that simulates other Turing machines, and is traditionally used to prove the
result in mathematical logic that some problems able to be expressed as computations are unable to ever be solved by any
model of computation. We will build a "universal Scheme machine" and prove that the program has
inputs for which it will never produce an answer, showing that the "simulation" problem is one such unsolvable problem. The
advantage that writing this program in Scheme has over a Turing machine is that, once again, we can actually *run* the program.
Afterwards, we will use this program to prove Gödel's incompleteness theorem in a very idiosyncratic way. Gödel's theorem says
that formal logical theories which can prove a specific, minimum amount of arithmetical facts cannot prove all true arithmetical
facts, and furthermore that one of the facts that they cannot prove is the statement that they do not prove anything false. We
will use our Scheme program to prove a version of this result, by relating the problem to the problem of computing the smallest
size of a program able to compute a certain number, and showing that our program cannot ever compute what that size is despite
the size necessarily existing.



### Haskell

Haskell is also a functional programming language, however Haskell is not based on the same lambda calculus as Scheme. The lambda
calculus which Scheme is based off of is more specifically called the *untyped* lambda calculus. Haskell is based on the *typed*
lambda calculus. Types are similar to sets in that they are a collection of values. Types are used in programming as a sort of
tag that lets the computer know what values we want our functions to be able to take and what values we want our functions to
produce. Originally, the untyped lambda calculus was expanded to have a logical component, but this system was proven inconsistent.
Later it was discovered that adding types to the lambda calculus, which controlled which functions were allowed to be applied to
which others, made the system logically consistent. Even more so, it was later discovered that the type system (that is, the rules
for creating types and therefore creating functions and values) were in perfect synonymy with constructive and intuitionistic
systems of formal logic. This foundations section will focus on explaining the different kinds of typed lambda calculi, and how
they relate to constructive and intuitionistic logic. 

Haskell, then, is a typed lambda calculus. The main implementation of Haskell is GHC, the Glorious Glasgow Haskell Compiler. It
also has a very powerful REPL system, which we will be using to work with our code. Haskell is not a Lisp, and therefore does not
use parentheses to represent function application. Instead, and much like in mathematics, it uses juxtaposition. f x means apply
the function f to the value x. In fact, much of Haskell's syntax is heavily inspired by mathematics, and that is one of the parts
of the language that people like best. It is very easy to translate mathematical ideas directly into Haskell, and vice versa. For
instance, Haskell has a kind of expression called a list comprehension that looks and behaves similarly to set comprehensions.

    > [x | x <- [1..10], even x]
    [2,4,6,8,10]

In this example REPL session, we told Haskell that we want the list of numbers x such that x comes from the list
[1,2,3,4,5,6,7,8,9,10], and such that x is even. And sure enough, Haskell gives us the list of even numbers from 1 to 10.
The syntax for list comprehensions looks almost identical to the mathematical syntax for set comprehensions, where we would say
that the set of even numbers from 1 to 10 is { x | x 𝜖 {1, 2, .., 10} & x is even}. Another example of how mathematical Haskell's
syntax is comes when we define our own functions. Take the factorial function, which has a clear recursive definition that can be
expressed piecewise as a base case and a recursive case. In Haskell, we could define it as

    > factorial :: Int -> Int
    > factorial 1 = 1
    > factorial n = n * factorial (n - 1)

which mirrors the piecewise definition in mathematics (modulo the large curly brace we would use to connect the name with the
definition). The first line of this is a type signature. In Haskell, we can write out the type of our function by telling the
computer what types it takes as input and what type it should produce as output. In our case, we are saying factorial has the
type (::) of a function from an integer to an integer (Int -> Int). This makes sense, since the factorial function takes an
integer as input and returns an integer as output. We define the function recursive, by supplying a base case, and then a
recursive case. If the function is given the input 1, then it returns 1. If it is given a different input n, then it returns
n times the result of applying the function to n - 1, which is the mathematical definition of the factorial function as well.
Factorial of 10 is 10\*9\*8\*7\*6\*5\*4\*3\*2\*1 = 3,628,800, and if we ask Haskell using our function we get

    > factorial 10
    3628800

as expected. This is a very short example of what a REPL session in Haskell could look like.

Our applications of Haskell to problems in philosophy will focus on questions in formal semantics and the philosophy of language.
Typed lambda calculi have been used since the 1970s as the formal mathematical model for semantics of natural language. This is
because it was noticed early on that linguistic parts of speech, such as verb phrases, noun phrases, preposition phrases, and
so on, act precisely as do typed functions. Imagine that sentences have a type called Sentence. Then a verb phrase is a function
which takes a noun phrase in and returns a sentence with type Sentence. This seems very plausible, because if we squint as a
verb phrase like "is tall" we can almost imagine it like a function f(x) = "x is tall" which waits for a noun and then plugs
it into the function. In essence, this is what formal semantics is about. But, the interesting part is that it is not only
verb phrases which are treated as functions. A noun phrase can be viewed as a function waiting for a verb phrase, and once it
receives one, outputs a sentence. This is the key insight. If you remove *any* coherent piece of a sentence, whether it is a
noun phrase, or verb phrase, or adjective, or preposition, or anything else, you end up with a sentence missing a specific
type of linguistic construction, or with a specific kind of "hole", and we can abstract over that missing piece to create a
function which takes an object of that shape and returns a complete sentence. This generalizes to parts of speech other than
full sentences as well. A definite article is a function which takes a noun and returns a noun phrase. An adjective is a
function which takes a noun phrase and returns a noun phrase. This is the beauty of the typed lambda calculus, it is as flexible
as we want it to be, while still adhering to a coherent set of rules. The founder of analytic philosophy G. Frege called this idea
saturation. Functions are things unsaturated, that is, missing a piece, and once they are given that piece they become saturated,
or whole. The essence of the typed lambda calculus is the ability to use the type system to create the exact shape of the
unsaturated part of our functions that we want. We will be using Haskell as a typed lambda calculus to implement a fragment of
the English language as a series of typed functions which compute the meaning of sentences and phrases. The benefit of embedding
this fragment of English, as the process is called, into Haskell instead of using pen and paper to compute the lambda functions is,
similarly to the benefit of using Prolog and Scheme in their own projects, that we will end up with a runnable computer system that
handles all of the steps for us and allows us to use examples that would otherwise be too complex and laborious to do by hand. Not
only that, though, because we'll also have the benefit of having trust in our answer. Computers don't make mistakes, unless what
they were told to do was a mistake. So, when we get an answer from our program, we can trust that it's correct. The same cannot
be said for humans.

Implementing a fragment of English is not our end goal, however, and we will be taking the program one step further. Haskell is famous
in the computing world for its use of monads. Monads are a mathematical structure from an abstract field of mathematics called
category theory. It was discovered that monads are a great way of formally representing the idea of a computation "in a context",
and from Haskell's inception in the late 1980s, monads were used as an integral part of its type system to represent computations
that interface with the real world. This idea of monads as representing a context turns out to be widely applicable. Monads can also
be used to model challenging problems in formal semantics and the philosophy of language, such as presupposition failure. A 
presupposition is a proposition which is implicitly taken to be true. If Alice asks Bob how his sister is doing, there is a
presupposition that Bob has a sister. Presupposition failure is the linguistic situation where some sentence has a presupposition,
but that presupposition turns out to be false. If Bob has no sister, then not only would it have been inappropriate of Alice to ask
him that question, it would also be challenging for us to determine the truth of Bob's response of "She's doing well." It doesn't
strictly seem true to say that the sentence is false, since that might imply that his sister is doing poorly. But he has no sister,
and so that sentence too would have a presupposition failure. Monads can help this. One "computational context" is the context of
possible failure. Consider division: we know that if you divide any real number by any other non zero real number, you get a real
number as a result. However, if you divide any real number by zero, you get nothing. Or, the answer is not well defined. Division
of real numbers is a computational context where failure might happen. If the divisor is nonzero, then the computation succeeds. If
the divisor is zero, then the computation fails. We can use this idea of possible failure to account for presuppositional failure.
Reference is a context in which there is a chance of failure, because you might try to reference some object that doesn't exist. In
the case that the object does exist, the sentence refers to it and the truth of the sentence can be determined by its meaning. However,
if reference fails, then we have to use the computational context of the monad to represent that failure, and we cannot attempt
to calculate the meaning of the sentence, and thus its truth value, normally. Monads are a powerful abstraction, and Haskell allows
us direct access to them through its type system, and so it becomes the perfect language to formalize a monadic theory of semantics for
a fragment of the English language. Our program will explore how many of the different monads regularly used in Haskell programming
represent plausible solutions to myriad problems in the philosophy of language and formal semantics.


## Audience and Prerequisites

This book is mainly addressed to philosophy students who have taken an introduction to formal logic course (that is, more than
a "Critical Thinking and Rhetoric"-type course). While going all the way to the completeness of first-order logic is not
necessary, the student should at least be at a point where a proof of such would be accessible to them. In particular, they should
have a working knowledge of propositional and first-order logic, understand what a model is, and be comfortable with some
kind of proof system. Outside of these students, it seems plausible that there are two other types of students who would be 
prepared for this book.

A student of computer science who has made it through their discrete mathematics course has enough experience with formal logic, 
and set theory, to be prepared for the formal content in this book. If they have made it through their theory of computation 
course, then they will be extra prepared for the discussion of incompleteness and undecidability. The major obstacle facing
such students is the fact that the languages used in this book are without a doubt different from the majority, if not the 
entirety, of the languages they have used before. Declarative programming is a different mode of thinking than imperative 
programming, and much ink has been spilt about how and why. Those learners coming from a computer science background who have only
ever used languages like Java and Python need to be prepared to reorient their mind in how they think about their code. It should 
also be noted that many universities offer a course usually under some title related to "Programming Languages," and that the 
content of these courses overlap a nontrivial amount with this book. Those classes are usually focused, however, on the 
implementation and language design aspects of declarative programming and how those contrast with imperative programming, which is
not a topic this book touches in the slightest. 

Lastly, a mathematics student who has made it through their first round of higher mathematics classes (introduction to 
analysis, abstract algebra) will have what is usually described as the "mathematical maturity" required for this book. What 
that means, basically, is that they will have familiarity with logical notions such as quantifiers, bound and unbound 
variables, the logical connectives, truth conditions, and models (under the name "abstract structures satisfying some 
axioms"). But most important, of course, is familiarity with proofs. Because these students usually have not had a formal 
introduction to logic, it may be a rougher starting experience than others, and they may need to apply more effort at the
beginning. But the import of "mathematical maturity" is that these issues can be overcome with commitment to learning.
