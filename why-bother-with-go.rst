Why Bother with Go?
===================

Problem Domain
--------------
* #1 Run on: Linux 3.x
* #2 Absolute performance (useful ops/cpu time used)
* #3 CPU-scalability
* #4 Networking support
* #5 Access to Linux system calls
* #6 Code that can be read, understood and edited by mere mortals

Problem Domain
--------------
* #7 No surprises (low "WAT?!" frequency)
* #8 Buildability/Packageability/Deploability
* #9 Used by a critical mass / Active community / Have a future
* #10 Protect programmer from stupid errors
* #11 Expressiveness (LOC/achieved thing)
* #12 General quality and stability
* #13 Call native extensions and don't spit on the C legacy

=> "Linux System Daemon/Tool"

Options
-------

Note: numbers mean "has issues with"...

* c/c++: #6, #7, #10, #11
* python, ruby: #2, #3, #8, (#10)
* node.js: (#3), #6, #7, #8, #10

Not applicable
--------------
* Anything Windows or OSX -specific (C#, Swift, objective-c, Swift, VB)
* Ceylon
* Dart
* Lua
* PHP
* Perl
* Typescript

Weirdos
-------
* Clojure (or any other lisp-descendant)
* Erlang
* Haskell
* Ocaml
* R

Remaining
---------
* Go: ?
* Java: (#5), (#6), (#8), #11
* Rust: (not stable yet and has a weirdo factor to it)
* Scala: ?

If you are not a "Java team", the only remaining option is Go...

Go vs. Problem Domain
---------------------
* Good match, except #11 to some extent

Go Features
-----------
* Designed by old school Unix veterans (ex Bell Labs) at Google
* Language (syntax) is kept minimal and currently there has been a syntax freeze ever since the v1.0 release (2012-03-28)
* A couple of major releases per year
* Excellent support for concurrency (via "goroutines" and "channels" for communicating between them)
* Statically typed, but you don't suffer from it too much
* (Cross-)compiles platform-specific stand-alone binaries that depend on (almost) nothing

Go Features
-----------
* Comes with a good set of tools: go build, go vet, go fmt, go get, go doc, etc.
* For testing: ``go test`` (with ``-parallel``, ``-cpuprofile``, ``-memprofile``, ``-cover``, ``-bench``) and ``go build -race``
* Comes with many good packages: networking, compression, crypto, text encoding, syscalls, unicode, testing, reflection, mime
* ...and not so good ones: logging, cmdline arg parsing, database abstraction
* Build times are fast (e.g. 2.5 seconds for 26 kLOC ``consul``)

Go Features
-----------
* You can pick up most of the syntax in a matter of few hours, and after that there are not many surprises
* You write sequential, blocking code. No async callbacks.
* Maintains readability in highly concurrent code (unlike node.js)
* No VM tricks: the binary is just executable native code that gets mmap()'ed
  to memory and process execution jumps in there.

Initial Shock
-------------
* No exceptions, you need to do a LOT of ``error := f(); if error != nil { return error }``
* Varible types defined the wrong way around: ``foo func(int, int) string`` instead of ``string (*foo)(int, int)``
* No inheritance
* Strict style enforcement (curly braces required, cannot place them on separate
  lines, semantic CamelCase naming, ...)

Post-Traumatic Stress
---------------------
* **No generics of any kind**
* No constructors or destructors
* No operator overloading
* A zillion small syntactic sugar things missing
* You don't leave unused variables or imports in code (fails to compile, there are no compilation warnings, just errors)
* Network and channel operations or sleeping do not block a thread, but file i/o, syscalls and C-calls do. (TODO: is this still true?)
* => You get to google a lot what is the idiomatic Go way to do something that you have used to doing some other way

Brilliant Go Features
---------------------
* Goroutines: light-weight pre-emptable threads that scale over a *runtime-defined number* of OS threads
* Channels
* ``select`` statement, with some reservations
* ``defer`` statement
* "C" package for calling C libraries

Unknown Territory (for me)
--------------------------
* Large scale apps
* 3rd party package dependency management

Example: Setting up ``GOPATH``
------------------------------
Example::

 export GOPATH=/tmp/gopath
 go get github.com/ohmu/tjob
 go test github.com/ohmu/tjob
 go install github.com/ohmu/tjob

Notice the dependencies are automatically downloaded under ``$GOPATH/src``.
