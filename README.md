
# The Missing Guide for ClojureScript

When I started with ClojureScript and tried to follow the official [Quick Start Guide](https://clojurescript.org/guides/quick-start) it did not seem very straightforward to me. It is a good read though after a bit of hands on experience. This guide is a compilation of things I wished to know at the beginnings.

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Quick Start](#quick-start)
	- [Create a project](#create-a-project)
- [Documentation](#documentation)
- [Resources](#resources)
	- [Tutorials](#tutorials)
	- [Books](#books)
	- [Exercises](#exercises)
- [Cookbook](#cookbook)
	- [Libraries](#libraries)
	- [JS Interop](#js-interop)
	- [IO](#io)
	- [EDN](#edn)
- [Editor setup](#editor-setup)
- [Debugging](#debugging)
- [Tools](#tools)
- [Misc](#misc)

<!-- /TOC -->

## Quick Start

Try out some code using REPL.

Under node.js install [Lumo](https://github.com/anmonteiro/lumo) with:
```
$ npm install -g lumo-cljs
$ lumo
cljs.user=> (println "hello clojure")
hello clojure
```

For Java first install [Leiningen](https://leiningen.org/) and then:
```
$ lein repl
user=> (+ 1 2)
3
```

### Create a project

#### Node.js server or CLI app

Use [cljs-node-app](https://github.com/yanatan16/cljs-node-app-template) template:
`lein new cljs-node-app <project-name>`

Compile the project: `lein cljsbuild once main`

Watch and recompile on changes: `lein cljsbuild auto main`

#### Web app

Use [re-frame](https://github.com/Day8/re-frame-template) template which uses React.js via [Reagent](https://github.com/reagent-project/reagent) under the hood:
`lein new re-frame <project-name> +test`

Start development mode with live reload: `lein figwheel dev`

Compile the project: `lein cljsbuild once main`

## Documentation

Inside REPL:

```clojure
;; Show function docs in REPL
(doc str)

;; Search in docs
(find-doc "reduce")

;; Show function source code
(source identity)
```

Browse [API documentation](https://clojuredocs.org/quickref) and refer to [Cheatsheet](http://clojure.org/cheatsheet) on the web.

## Resources

- [Official Clojure Reference](https://clojure.org/reference/reader)
- [Library Coding Standards](https://dev.clojure.org/display/community/Library+Coding+Standards)
- [Clojure Styleguide](https://github.com/bbatsov/clojure-style-guide)
- [Anki deck](https://ankiweb.net/shared/info/3248915342) for spaced-repetition learning

### Tutorials

- [Learn Clojure in Y minutes](http://learnxinyminutes.com/docs/clojure/) is a very concise indroduction to Clojure.
- [ClojureScript Unraveled](http://funcool.github.io/clojurescript-unraveled/) is an online book and guide about ClojureScript.
- [Brave Clojure – Chapter 3 Crash Course](http://www.braveclojure.com/do-things/)
  Clojure for the Brave and True is a book available online. I find chapter 3 a very good intro to Clojure. If you like more chatty style and humor in programming books then also give a read to other chapters.
- [Clojure – Functional Programming for the JVM](http://java.ociweb.com/mark/clojure/article.html) is an introductory article to functional programming and Clojure. It is aimed for Java programmers but contains interesting bits of information and goes into more low-level details.
- [Clojure from the ground up](https://aphyr.com/tags/Clojure-from-the-ground-up) is a collection of articles on various Clojure topics.

### Books

- [Programming Clojure by Stuart Halloway](https://www.amazon.com/dp/1934356867) is a best book about Clojure for programmers, I recommend anyone learning Clojure(Script) to start with this one.
- [Clojure Applied: From Practice to Practitioner](https://www.amazon.com/dp/1680500740) is a book focusing on more practical aspects of app development in Clojure. Includes chapters about domain modelling, managing state and application components.
- [Mastering Clojure](https://www.amazon.com/dp/B017XSFL4Q/) describes in detail more advanced topics like paralelism, transducers, category theory, pattern matching and logic programming.

Explore other [books](https://clojure.org/community/books) by the community.

### Exercises

- [99 Lisp Problems](http://www.ic.unicamp.br/~meidanis/courses/mc336/2006s2/funcional/L-99_Ninety-Nine_Lisp_Problems.html)
- [4Clojure](http://www.4clojure.com/problems)
- [Clojure Koans](http://clojurekoans.com/)
- [Project Euler Problems](https://projecteuler.net/archives)
- [Simple Programming Problems](https://adriann.github.io/programming_problems.html)

## Cookbook

### Libraries

Opinionated list of useful libraries. There are alternatives but if you are just starting you can't get wrong by picking these.

**Frontend**
- React wrapper framework: [re-frame](https://github.com/Day8/re-frame)
- UI Components: [re-com](https://github.com/Day8/re-com)
- Forms with validation: [Reforms](https://github.com/bilus/reforms)
- HTTP requests: [cljs-ajax](https://github.com/JulianBirch/cljs-ajax)
- Routing: [Secretary](https://github.com/gf3/secretary)
- Date, Url and other utilities: [Google Closure Library](https://google.github.io/closure-library/api/goog.html)

Check other libraries in [Awesome ClojureScript list](https://github.com/hantuzun/awesome-clojurescript).

**Backend**
- HTTP APIs: [Compojure](https://github.com/metosin/compojure-api)
- Logging: [Timbre](https://github.com/ptaoussanis/timbre)

### JS Interop

A great feature of ClojureScript is that you can work with native JS objects and use existing JS libraries.

```clojure
;; Use js/ prefix for global names, e.g. to print in browser console
(js/console.log "Hello, world!")

;; Add dot to construct new objects
(js/Date. "2017-10-16") ; new Date("2017-10-16")

;; Call methods
(.toUpperCase s) ; s.toUpperCase()

;; Use treading macro to chain calls
(-> "BOOM" (.toLowerCase) (.slice 0 -1)) ; "BOOM".toLowerCase().slice(0, -1)

;; Access attributes
(.-length s) ; s.length

;; Nested attribute access
(.-location.href js/window) ; window.location.href
(aget window "location" "href") ; window["location"]["href"]

;; Set attributes
(aset obj "attr" "val") ; obj["attr"] = "val"

;; create native js objects with #js macro
#js {:a 1 :b 2} ; {a: 1, b: 2}
#js [1 2 3] ; [1, 2, 3]

;; convert cljs data structures into js objects
(clj->js obj)

;; convert js objects to cljs data structures
(js->clj obj :keywordize-keys true))
```

See a [post with more details](http://www.spacjer.com/blog/2014/09/12/clojurescript-javascript-interop/) and [comparison of JS and Clojure](https://kanaka.github.io/clojurescript/web/synonym.html) idioms.


Use node modules by [seamlessly requiring](https://clojurescript.org/news/2017-07-12-clojurescript-is-not-an-island-integrating-node-modules) them (starting with 1.9.854):
```clojure
(ns example.core
  (:require [react :refer [createElement]]
            ["react-dom/server" :as ReactDOMServer :refer [renderToString]]))

(js/console.log (renderToString (createElement "div" nil "Hello World!")))
```

### IO

To print at ClojureScript REPL
```clojure
(println "Hello, world!")
```

Working with filesystem – require `fs` from node and call native functions.
```clojure
(def fs (js/require "fs"))
(fs.readFileSync "foo.txt" "utf8")
```

When working in repl you can use `slurp` to read a file and `spit` to write a file.
```clojure
;; Read a file into one long string
(def a-long-string (slurp "foo.txt"))

;; Write a long string out to a new file
(spit "foo.txt"
"A long
multi-line string.
Bye.")
```

Alternative approach is to use [cljs-node-io](https://github.com/pkpkpk/cljs-node-io) which is a port of [clojure.java.io](http://clojure-doc.org/articles/cookbooks/files_and_directories.html).

### EDN

EDN is to Clojure what JSON is to Javascript.

- parse: [cljs.reader/read-string](https://cljs.github.io/api/cljs.reader/read-string)
- stringify: [prn-str](http://cljs.github.io/api/cljs.core/prn-str)

## Editor setup

**[Atom](https://atom.io)**

Refer to [this guide](https://gist.github.com/jasongilman/d1f70507bed021b48625) for a good setup. Essential packages are:
- [parinfer](https://atom.io/packages/parinfer) so that you don't have to worry about parentheses
- [proto-repl](https://atom.io/packages/proto-repl) to evaluate code right within editor window

**[Spacemacs](http://spacemacs.org/)**
- Emacs distribution with Vim mode
- Looks intriguing, it's on my list of things to try

**[Cursive](https://cursive-ide.com/)**
- a great IDE based on IntelliJ


## Debugging

**Debug with Chrome DevTools**

- [Enable custom formatters](https://github.com/binaryage/cljs-devtools/blob/master/docs/installation.md#enable-custom-formatters-in-chrome)
- Data formating is done with [cljs-devtools](https://github.com/binaryage/cljs-devtools) which is already included in the [web app template](#web-app) mentioned above
- Add expressions to watches like: `cljs.core.pr_str(localvar)`

For more functionality use [Dirac](https://github.com/binaryage/dirac), a DevTools fork with additional ClojureScript related features.

**Debug node apps with Chrome DevTools**
- Run `node --inspect-brk build/main.js`
- In Chrome open `chrome://inspect` and select the session

**Call tracing inside Atom**

Use `proto-repl: save call` to record function calls and values of parameters, watch [video with instructions](https://youtu.be/buPPGxOnBnk?t=11m55s).

**General call tracing**

Trace calls with [Clairvoyant](https://github.com/spellhouse/clairvoyant) which is an alternative to  [clojure.tools.trace](https://github.com/clojure/tools.trace).

## Tools

**Code quality**
- [kibit](https://github.com/jonase/kibit) – static analysis tool that offers suggestions for code improvement
- [lein-ancient](https://github.com/xsc/lein-ancient) – check and upgrade outdated dependencies in your project
- [cljfmt](https://github.com/weavejester/cljfmt) or [lein-zprint](https://github.com/kkinnear/lein-zprint) or  [boot-fmt](https://github.com/pesterhazy/boot-fmt) for code auto-formatting

**Code exploration**
- [lein-ns-dep-graph](https://github.com/hilverd/lein-ns-dep-graph) – Explore and visualize namespace dependencies
- [lein-gossip](https://github.com/actsasgeek/lein-gossip) – Visualize call-graphs in a codebase
- [lein-instant-cheatsheet](https://github.com/cammsaul/lein-instant-cheatsheet) – Instant Cheatsheet instantly creates a cheatsheet for your project and its dependencies

## Misc

[CrossClj](https://crossclj.info/) – Explore dependencies of Clojure packages among each other, see which function are called where and with what arguments:

Bootstrapping:
- [calvin](https://github.com/eginez/calvin) – A minimalistic build tool for ClojureScript projects that does not require the JVM
- [with Lumo](https://anmonteiro.com/2017/02/compiling-clojurescript-projects-without-the-jvm/)

Articles about Lisp:
- http://www.paulgraham.com/icad.html
- https://funcall.blogspot.cz/2009/03/not-lisp-again.html
