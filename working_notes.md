# Working Notes

## Contents

- [Ideas](#ideas)
- [Pain Points](#pain-points)
- [Tex Specimens](#tex-specimens)


## Ideas

- Racket: syntax ideas, DSL's

- Pinky issue 

- Bijective parsing — **Yes!**

- Prior work

- Drop down to LaTeX

- Scripting
    - Variables
    - Loops
    - Functions?
    - Conditionals?

- Language server, plugin

- IDE


- Maybe use `[foo bar bax]` as syntax for 
inline elements.  I like this: clean.  **Problem:** how do we deal
with brackets as part of ordinary text?
*One way would be to recognize only constructs
of the form [KEYWORDfollowed by whitespace
 as beginnning an inline 
element. This would complicate parsing somewhat.* 

- **What else?**

## Pain Points

___

[Main](#id/40b1cb50-4f1d-4807-93b4-5440b005fc43)

___

## List of pain points

- **Matrices** Definitely a pain point.
 —
don't have ideas atm for a
 good syntax (Jim).

- **Math mode generally** ??? What to
do ???  There are environments, which
I think we can handle better, but I don't
have good ideas atm about improvements
over the usual.  Maybe we should have
a collection of specimens.

- **Tables** I suggest that we should
be able to deal
with tables in several
of the common formats, e.g., csv.  In
addition to having tables in source, it
might be nice to be able to access them
as a file or by URL.

- **Images.** Make these work with both files
and URLS. Simple syntax that takes care
of placement and size options. Have defauts,
so that the user has to put in parameter
only as needed.

- **Others?** 

## Ideas

### Sample matrix format

```elm
???
```

### Sample table format

```elm
// csv-table
header: Element, Symbol, Z, A
Hydrogen, H, 1, 1.0080
Helium, He, 2, 4.00260 
Lithium, Li, 3, 7.0
source: https://pubchem.ncbi.nlm.nih.gov/periodic-table/
//
```

Here is an example of a table referenced
by URL:


```elm
// csv-table
url: https://foo.org/co2-emissions.csv
comment: For presentation to POTUS
//
```

Note that the
use of `//` to begin and end blocks
avoids the pinky problem.  The first identifier
after the leading `//` is the block name.
If we require the block begin and block
end tokens to begin at the first column,
we avoid the problem of a clash with ordinary
text.

Things like `header:` and `source:` should
be optional.  One can imagine other elements:

- `format:` e.g, *l, l, l, d* in the above
where *l* means left-align and *d* means
right-align on decimal point.

- `footer:`

- `notes:`


Parameters that are not handled by the
language should be ignored. Thus one might
put 

```elm
todo: Check those references!

```

### Sample image syntax (block)

No parameters except url:

```elm
// image
url: https://birds.org/hummingbird.png
//

```


```elm
// image
url: https://birds.org/hummingbird.png
width: 200
float: left
caption: Calypte anna
number: auto
//

```

What it should look like:

![HumCalypte anna](https://www.hummingbirdcentral.com/images/visitors/marilyn-meadows/annas-hummingbird-male-07.jpg)
Calypte anna


GetSelectionForSync

should   


## Tex Specimens



___

[Main](#id/40b1cb50-4f1d-4807-93b4-5440b005fc43)

TeX specimens with possbile alternate syntax.

- The syntax `[[ ... ]]` is clean and has both
begin and end delimiters. Moreover, the double
begin and end brackets are uncommon in normal
text. This syntax could be used for both blocks
and inline elements, perhaps with the convention
that blocks begin at the left margin. Note also
that brackets, while typed with the pinky, are
in a comfortable position and don't require the
shift key.

- Maybe we should retain underscore and caret
for sub- and super-scripts.  These characters
are not obtrusive and their visual character mirrors
their function.

- What I'm most unsure about is how to distinguish
macro (function) names and how to deal with their
 arguments. We'll need a way to group chunks of
text to signal that the chunk is one argument,
not several.



### Some examples

Here is a TeX fraction: 

```elm
f = \frac{1}{2} = \frac 1 2
```


 So we could say this (for example):


```elm
[[f = .frac 1 2]]

```

The leading period seldom occurs in natural language
or Tex and I like its visual appearance better
than backslash. But it is a pinky character and
 is also somewaht awkaward to type.

### The Specimens

#### Easy

___

```elm
\int_0^1 x^n dx = \frac{1}{n+1}
```

```elm
[[ int_0^1 x^n = /frac 1/n+1/ ]]
```

$$
\int_0^1 x^n dx = \frac{1}{n+1}
$$
___

```elm
\frac{d{\bf p}}{dt} = {\bf F}
```

$$
\frac{d{\bf p}}{dt} = {\bf F}
$$

___

```elm
  \Delta x \, \Delta p \ge \frac{\hbar}{2}
```

$$
  \Delta x \, \Delta p \ge \frac{\hbar}{2}
$$

___

```elm
h = 6.6\times 10^{-34}\;\text{Joule-sec}
```

$$
h = 6.6\times 10^{-34}\;\text{Joule-sec}
$$

___

```elm
\frac{\sin \theta_1}{\sin \theta_2} = \frac{c_1}{c_2}
```

$$
\frac{\sin \theta_1}{\sin \theta_2} = \frac{c_1}{c_2}
$$

___


```elm
\nabla t = h\left(\frac{\sin \theta_1}{c_1 \cos^2 \theta_1},
\frac{\sin \theta_2}{c_2 \cos^2 \theta_2}\right)
```

$$
\nabla t = h\left(\frac{\sin \theta_1}{c_1 \cos^2 \theta_1},
\frac{\sin \theta_2}{c_2 \cos^2 \theta_2}\right)
$$

___

```elm
\frac{h\nu}{c_1}\;\sin \theta_1
=
\frac{h \nu}{c_2}\;\sin \theta_2
```

$$
\frac{h\nu}{c_1}\;\sin \theta_1
=
\frac{h \nu}{c_2}\;\sin \theta_2
$$

___

#### Somewhat harder

___

```elm
({\mathcal F} g)(k) = 
\frac{1}{\sqrt{2\pi}} 
\int_{-\infty}^\infty g(x) e^{-ikx} dx,
```

$$
({\mathcal F} g)(k) = 
\frac{1}{\sqrt{2\pi}} 
\int_{-\infty}^\infty g(x) e^{-ikx} dx,
$$

___


```elm
g(x)  = \frac{1}{2\pi} 
\int_{-\infty}^\infty  \ket
k \braket{k|g} \,dk
```

$$
g(x)  = \frac{1}{2\pi} 
\int_{-\infty}^\infty  \ket
k \braket{k|g} \,dk
$$

___

```elm
\begin{align}
\hat f(k) &= \frac{1}{\sqrt{2\pi}}
\int_0^\infty e^{-\lambda x} e^{ikx} dx \\
   &= \frac{1}{\sqrt{2\pi}} \,
\frac{-1}{ik + \lambda}\,\Big\vert_0^\infty \\
 &= \frac{1}{\sqrt{2\pi}(ik + \lambda)}
\end{align}

```

$$
\begin{align}
\hat f(k) &= \frac{1}{\sqrt{2\pi}}
\int_0^\infty e^{-\lambda x} e^{ikx} dx \\
   &= \frac{1}{\sqrt{2\pi}} \,
\frac{-1}{ik + \lambda}\,\Big\vert_0^\infty \\
 &= \frac{1}{\sqrt{2\pi}(ik + \lambda)}
\end{align}
$$

___


```elm
\lim_{a \to 0}\int_{-\infty}^\infty 
r_a(x-\xi) f(x) dx = 
\lim_{a\to 0} av_{a,\xi} f = f(\xi)
```

$$
\lim_{a \to 0}\int_{-\infty}^\infty 
r_a(x-\xi) f(x) dx = 
\lim_{a\to 0} av_{a,\xi} f = f(\xi)
$$

___


## Letter from Nick 23 January 2020


Hi Jim,

Sorry I didn't get back to you sooner,
I was a little busy in my last few
days in Paris. There's always so much
to do in Paris and so little time.

I'm definitely interested in working
on this project. To start, I suppose we
should outline the project structure.
My initial plan is that we're going
to write a standalone compiler, which
can then be integrated into a service
such as math-markdown. But I'm also
fine with started with a narrower,
more integrated usecase then building
the compiler out as we go along.

We might want to analyze our target
audience and our target problems.
LaTeX has more than a few problems and
tackling all of them at once probably
isn't advisable. Likewise, our potential
audience varies from not extremely
tech savvy people who just LaTeX with
less backslashes to programmers who
want to automate and script everything.
One good piece of advice that I've
heard in the past is to focus on a
group who desperately need the features
you're providing. Early adoption is
always rough, so it helps if your
users are essentially dependent on
your project. What problem/userbase
has such an urgency?

One idea I had was to use existing
LaTeX code as a starting point. We
could take LaTeX code, either some of
our old code or other people's code,
then see what tedious patterns occur. We
can then design the language to remove
these tedious patterns. TypeScript has
a similar philosophy in that every new
feature or design decision is with the
intention of adding types to existing
JavaScript code. If we can design the
language to fix existing LaTeX pain
points then people will definitely
start adopting our language.

As for bijective parsing, we can take
inspiration from [Roslyn's]() parser. We
don't need a fully bijective parser to
start, but perhaps storing whitespace
can come in handy for outputting nicely
formatted LaTeX.

I'll take a more thorough look at the
docs and edit them in the next few days.

Best, Nicholas

## Letter from Jim


Hi Nick,

I figured you were busy doing things
in Paris, which is of course the best
thing to do — no problem!

Thanks for your very thoughtful letter.
Totally agree on the direction of a
standalone compiler as the first step
. Also, I really like the idea of using
some exising LaTeX code as experimental
data for the project. I’ve got a bunch
of things lying around that I will
organize to this end. I thnk it would be
good to have source text from a number
of people, since all will approach
the LaTeX beast in different ways.

About potential audience and initial
target — really important, and deserves
a lot of thought … I’ll mull this over.
One group might be undergrad science
and engineering majors who need much
of what LaTeX can provide but aren’t
up to the hassle involved. I’ll post
a little example on our online notes
to show how this might be useful for
things like problem sets. There are
two advantages.

First has to do with the service aspect:
having a workflow that is as pleasant,
effiicient, and hassle-free as possible.
Here is a scenario: To write a document,
a user just types ctrl-N (or whatever)
to make a new document, then starts
typing. No setup. Then push a button
or type a command to do one of (a)
submit the work as PDF directly as
email, (b) export the document in
whatever format: source, standard LaTeX,
or PDF, (c) maybe something else. One
possibiity for (c) is that the student
simply submit a link to the html
version of the document. Like this:

[TEMPLATE](https://math-markdown.netlify.com/#doc/jxxcarlson.problem-set-template.d739)

[ANSWERS](https://math-markdown.netlify.com/#doc/jxxcarlson.answers.b897)

You would know better than I how
students are supposed to submit work.

Some of those features exist after a
fashion in the apps I’ve been working on.

Second has to do with syntax, as we’ve
already discussed: making the new
language as easy to learn and use as
possible. This is where some discussion
and testing with some willing subjects
in our eventual target audience could
be of immense help. Math-markdown is
a little step in that direction. For a
problem set you need only the tiniest
bit of markdown + knowing enough TeX
to write formulas. Big question: do
we want to address math-mode syntax?
If we had a good idea for this, we
could translate source text in our
syntax to TeX. Hmmm …. dunno about this
one. I’ve mainly thought about text-mode.


By the way, it is easy to integrate a
new language and compiler in a project
like https://math-markdown.netlify.com/
— it is set up now to handle both
MiniLaTeX and Markdown+Math. The only
requirement is that the compiler be
available as an Elm package and that
it expose a suitable API. The API is
something we should devote some thought
to. I’d be happy to change my API’s so
that we have a consistent set across
langauges. The API for compiling source
to target is of course just a single
function call. But for an interactive
editing environment, one needs more.
I’ll try to formalize this — having
worked now on two different languages,
two different API’s have evolved, and
it would be better to have a single,
well-thought-out version.

I look forward to working up a structure
for the project. This will be fun!

Best, Jim

