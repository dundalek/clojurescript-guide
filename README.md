
# The Missing Guide for ClojureScript

The official [Quick Start Guide](https://clojurescript.org/guides/quick-start) seems not very straightforward. It is a good read though after a bit of hands on experince. I believe the following guide is more approachable at the beginnings.

## Quick Start

Try out some code using REPL.

Under node.js install [Lumo](https://github.com/anmonteiro/lumo):
```
$ npm install -g lumo-cljs
$ lumo
cljs.user=> (println "hello clojure")
hello clojure

```

For Java install [Leiningen](https://leiningen.org/):
```
$ lein repl
user=> (+ 1 2)
3
```
### Documentation

```clojure
; Show function docs in REPL
(doc str)

; Search in docs
(find-doc "reduce")

; Show function source code
(source identity)
```

Read some [tutorials](#tutorials) online.
Browse [API documentation](https://clojuredocs.org/quickref) and [Cheatsheet](http://clojure.org/cheatsheet).


### Create a project

#### Node.js server or CLI app

Use [cljs-node-app](https://github.com/yanatan16/cljs-node-app-template) template:
`lein new cljs-node-app <project-name>`

Compile the project `lein cljsbuild once main`
Watch and recompile on changes: `lein cljsbuild auto main`

#### Web app

Use [re-frame](https://github.com/Day8/re-frame-template) template which uses React.js via [Reagent](https://github.com/reagent-project/reagent) under the hood:
`lein new re-frame <project-name> +test`

Start development mode with live reload: `lein figwheel dev`
Compile the project: `lein cljsbuild once main`

## Resources

- [Official Clojure Reference](https://clojure.org/reference/reader)
- [Library Coding Standards](https://dev.clojure.org/display/community/Library+Coding+Standards)
- [Clojure Styleguide](https://github.com/bbatsov/clojure-style-guide)
- [Anki deck](https://ankiweb.net/shared/info/3248915342) for spaced-repetition learning


### Tutorials

- [Learn Clojure in Y minutes](http://learnxinyminutes.com/docs/clojure/) is a very concise indroduction to Clojure.
- [ClojureScript Unraveled](http://funcool.github.io/clojurescript-unraveled/) is an online book and guide about ClojureScript.
- [Brave Clojure - Chapter 3 Crash Course](http://www.braveclojure.com/do-things/)
  Clojure for the Brave and True is a book available online. I find chapter 3 a very good intro to Clojure. If you like more chatty style and humor in programming books give a read also to other chapters.
- [Clojure - Functional Programming for the JVM](http://java.ociweb.com/mark/clojure/article.html) is an introductory article to functional programming and Clojure. It is aimed for Java programmers but contains interesting bits of information and goes into more low-level details.
- [Clojure from the ground up](https://aphyr.com/tags/Clojure-from-the-ground-up) is a collection of articles on various Clojure topics.


### Books

- [Programming Clojure by Stuart Halloway](https://www.amazon.com/dp/1934356867) is a best book about Clojure, I recommend anyone learning Clojure(Script) to start with this one.
- [Clojure Applied: From Practice to Practitioner](https://www.amazon.com/dp/1680500740) is a book focusing on more practical aspects of app development in Clojure. Includes chapters about domain modelling, managing state and application components.
- [Mastering Clojure](https://www.amazon.com/dp/B017XSFL4Q/) describes in detail more advanced topics like paralelism, transducers, category theory, pattern matching and logic programming.

Explore other [books](https://clojure.org/community/books) by the community.

### Exercises

- [99 Lisp Problems](http://www.ic.unicamp.br/~meidanis/courses/mc336/2006s2/funcional/L-99_Ninety-Nine_Lisp_Problems.html)
- [4Clojure](http://www.4clojure.com/problems)
- [Clojure Koans](http://clojurekoans.com/)
- [Project Euler Problems](https://projecteuler.net/archives)

## Cookbook

### Libraries

Frontend
- React wrapper framework: [re-frame](https://github.com/Day8/re-frame)
- HTTP library: [cljs-ajax](https://github.com/JulianBirch/cljs-ajax)
- UI Components: [re-com](https://github.com/Day8/re-com)
- Routing: [secretary](https://github.com/gf3/secretary)

See other libraries on [Awesome ClojureScript](https://github.com/hantuzun/awesome-clojurescript) list.
