# Deriving Functional Programming Laws From Categorical Definitions With Scala Examples

Subtitle: **Refactors Commute**

The objective of this project is to write a paper (in LaTeX) such that for any commonly abused Category Theoretic language found in Functional Programming (e.g. Functor, Monad, Product, Coproduct, Kleisli, etc), we first disambiguate using mathematical definitions, then using the example of the Category of Scala `C` (which treats Types as `ob(C)` and (1-param) functions as `hom(C)`)  we formally derive corresponding **laws** that could (in principle) be written as Property Based tests in Scala.

For example, we can derive Functor laws in Scala like so:

## Scala Notation

Let `T`, `U` and `V` be types, then we denote morphisms by `f: T => U` and `g: U => T`.

Identity morphism on `T`:

```
def id[T]: T => T = x => x
```

For any Functor `F`, we write `F[T]` to be the associated type to `T`, and `map_F(f)` to be the associated morphism to `f`

## Scala Laws

Let `t: T`, then

```
map_F(x => g(f(x)))(t) must_=== map_F(g)(map_F(f)(t))
map_F(id[T])(t) must_=== id[F[T]](t)
```

Where we more commonly see syntax like the following (letting `l: F[T]`)

```
l.map(x => g(f(x))) must_=== l.map(f).map(g)
```

## Practical Application

The big point of the paper will be to show that use of Category Theoretic language can have practical application when these **laws** are known, because they facilitate refactoring and optimising code.  When the **laws** are not known the language isn't all that useful.

We intend on building up the notion of a Commutative Diagram and show that many refactorings or optimisations are the result of following a Commutative Diagram.


# Links

Some existing free resources

https://www.slideshare.net/samthemonad/monad-presentation-scala-as-a-category
https://wiki.haskell.org/User:Michiexile/MATH198/Lecture_4
https://bartoszmilewski.com/2014/12/23/kleisli-categories/

# README

## Install MacTeX

`brew install mactex`

Restart terminal, then can compile LaTeX with

`xelatex file_name.tex file_name.pdf`, but this seems flakey, it also installs a program called `pdflatex`, and this actually seems to work, see "Generate and open the pdf document"

## OR Intall MiKTeX

MikTek is a latex editor which includes latex templates and that.

Install MiKTeX using brew:

```
brew install miktex-console
```

## Generate and open the pdf document

The code below initially creates the pdf version of the latex document which is then opened using the second line of code:

```
pdflatex -interaction=nonstopmode functional_programming_laws_from_category_theory.tex
open ../functional_programming_laws_from_category_theory.pdf
```

NOTE: for some weird reason sometimes you have to run the above `pdflatex` command twice, particularly if you've run `bin/clean.sh` or just checked out the repo.  If you don't run it twice the PDF generated doesn't have a table of contents.





