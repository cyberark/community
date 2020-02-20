# Golang Style Guide

## Table of Contents

- [Golang Style Guide and Best Practices](#golang-style-guide-and-best-practices)
  * [Style Baseline: Effective Go](#style-baseline-effective-go)
  * [Common Go Code Review Comments (a.k.a. Common Go Coding Mistakes to
    Avoid)](#common-go-code-review-comments-aka-common-go-coding-mistakes-to-avoid)
  * [The Uber Go Style Guide](#the-uber-go-style-guide)
  * [Standard Go Project Layout](#standard-go-project-layout)
  * ["Line of Sight" Coding Best Practice](#line-of-sight-coding-best-practice)
  * [Unit Testing Best Practices](#unit-testing-best-practices)
    + [Code Coverage](#code-coverage)
    + [Mocking](#mocking)
    + [Table Drive Testing](#table-drive-testing)
  * [Package Management](#package-management)
  * [Logging](#logging)
  * [Copyright Notices](#copyright-notices)
  * [Checking Your Code with `golint` and `go vet`](#checking-your-code-with-golint-and-go-vet)
  * [Appendix](#appendix)
    + [References / Further Reading](#references--further-reading)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with
markdown-toc</a></i></small>

## Golang Style Guide and Best Practices

This document serves as a style and best practices guide for Conjur developers who are writing
Golang source code. The purpose of this guide is to provide common conventions and to describe some
common pitfalls to avoid, so that our code base is consistent, readable, and maintainable across
various projects.

Much of the content for this style guide is drawn from publicly available Golang style guides.

This guide is intended to be a "living document" in the sense that it's expected that it will evolve
as we refine and hone our Golang knowledge base.

## Style Baseline: Effective Go 

The [Effective Go](https://golang.org/doc/effective_go.html) style guide serves as a baseline for
our Golang style guidelines. Some links to the main sections of this wiki document are provided here
as a handy reference:

[Formatting](https://golang.org/doc/effective_go.html#formatting)

[Commentary](https://golang.org/doc/effective_go.html#commentary)

[Names](https://golang.org/doc/effective_go.html#names)

[Semicolons](https://golang.org/doc/effective_go.html#semicolons)

[Control structures](https://golang.org/doc/effective_go.html#control-structures)

[Functions](https://golang.org/doc/effective_go.html#functions)

[Data](https://golang.org/doc/effective_go.html#data)

[Initialization](https://golang.org/doc/effective_go.html#initialization)

[Methods](https://golang.org/doc/effective_go.html#methods)

[Interfaces and other types](https://golang.org/doc/effective_go.html#interfaces_and_types)

[The blank identifier](https://golang.org/doc/effective_go.html#blank)

[Embedding](https://golang.org/doc/effective_go.html#embedding)

[Concurrency](https://golang.org/doc/effective_go.html#concurrency)

[Errors](https://golang.org/doc/effective_go.html#errors)

## Common Go Code Review Comments (a.k.a. Common Go Coding Mistakes to Avoid)

The [Go Code Review Comments
wiki](https://github.com/golang/go/wiki/CodeReviewComments#go-code-review-comments) provides a
collection of common comments made during Golang code reviews. This can be viewed as a supplement to
the  [Effective Go](https://golang.org/doc/effective_go.html) style guide. Links to the main
sections of this document are provided as a convenient reference:

[Gofmt](https://github.com/golang/go/wiki/CodeReviewComments#gofmt)

[Comment Sentences](https://github.com/golang/go/wiki/CodeReviewComments#comment-sentences)

[Contexts](https://github.com/golang/go/wiki/CodeReviewComments#contexts)

[Copying](https://github.com/golang/go/wiki/CodeReviewComments#copying)

[Crypto Rand](https://github.com/golang/go/wiki/CodeReviewComments#crypto-rand)

[Declaring Empty
Slices](https://github.com/golang/go/wiki/CodeReviewComments#declaring-empty-slices)

[Doc Comments](https://github.com/golang/go/wiki/CodeReviewComments#doc-comments)

[Don't Panic](https://github.com/golang/go/wiki/CodeReviewComments#dont-panic)

[Error Strings](https://github.com/golang/go/wiki/CodeReviewComments#error-strings)

[Examples](https://github.com/golang/go/wiki/CodeReviewComments#examples)

[Goroutine Lifetimes](https://github.com/golang/go/wiki/CodeReviewComments#goroutine-lifetimes)

[Handle Errors](https://github.com/golang/go/wiki/CodeReviewComments#handle-errors)

[Imports](https://github.com/golang/go/wiki/CodeReviewComments#imports)

[Import Blank](https://github.com/golang/go/wiki/CodeReviewComments#import-blank)

[Import Dot](https://github.com/golang/go/wiki/CodeReviewComments#import-dot)

[In-Band Errors](https://github.com/golang/go/wiki/CodeReviewComments#in-band-errors)

[Indent Error Flow](https://github.com/golang/go/wiki/CodeReviewComments#indent-error-flow)

[Initialisms](https://github.com/golang/go/wiki/CodeReviewComments#initialisms)

[Interfaces](https://github.com/golang/go/wiki/CodeReviewComments#interfaces)

[Line Length](https://github.com/golang/go/wiki/CodeReviewComments#line-length)

[Mixed Caps](https://github.com/golang/go/wiki/CodeReviewComments#mixed-caps)

[Named Result
Parameters](https://github.com/golang/go/wiki/CodeReviewComments#named-result-parameters)

[Naked Returns](https://github.com/golang/go/wiki/CodeReviewComments#naked-returns)

[Package Comments](https://github.com/golang/go/wiki/CodeReviewComments#package-comments)

[Package Names](https://github.com/golang/go/wiki/CodeReviewComments#package-names)

[Pass Values](https://github.com/golang/go/wiki/CodeReviewComments#pass-values)

[Receiver Names](https://github.com/golang/go/wiki/CodeReviewComments#receiver-names)

[Receiver Type](https://github.com/golang/go/wiki/CodeReviewComments#receiver-type)

[Synchronous Functions](https://github.com/golang/go/wiki/CodeReviewComments#synchronous-functions)

[Useful Test Failures](https://github.com/golang/go/wiki/CodeReviewComments#useful-test-failures)

[Variable Names](https://github.com/golang/go/wiki/CodeReviewComments#variable-names)

## The Uber Go Style Guide

Uber has created a [Uber Go Style Guide](https://github.com/uber-go/guide/blob/master/style.md) for
defining their Golang conventions and best practices. This is an EXCELLENT source of best practices
and possible pitfalls to avoid.

[Guidelines](https://github.com/uber-go/guide/blob/master/style.md#guidelines)

* [Pointers to
  Interfaces](https://github.com/uber-go/guide/blob/master/style.md#pointers-to-interfaces)
* [Receivers and
  Interfaces](https://github.com/uber-go/guide/blob/master/style.md#receivers-and-interfaces)
* [Zero-value Mutexes are
  Valid](https://github.com/uber-go/guide/blob/master/style.md#zero-value-mutexes-are-valid)
* [Copy Slices and Maps at
  Boundaries](https://github.com/uber-go/guide/blob/master/style.md#copy-slices-and-maps-at-boundaries)
* [Defer to Clean Up](https://github.com/uber-go/guide/blob/master/style.md#defer-to-clean-up)
* [Channel Size is One or
  None](https://github.com/uber-go/guide/blob/master/style.md#channel-size-is-one-or-none)
* [Start Enums at One](https://github.com/uber-go/guide/blob/master/style.md#start-enums-at-one)
* [Error Types](https://github.com/uber-go/guide/blob/master/style.md#error-types)
* [Error Wrapping](https://github.com/uber-go/guide/blob/master/style.md#error-wrapping)
* [Handle Type Assertion
  Failures](https://github.com/uber-go/guide/blob/master/style.md#handle-type-assertion-failures)
* [Don't Panic](https://github.com/uber-go/guide/blob/master/style.md#dont-panic)
* [Avoid Mutable
  Globals](https://github.com/uber-go/guide/blob/master/style.md#avoid-mutable-globals)

[Performance](https://github.com/uber-go/guide/blob/master/style.md#performance)

* [Prefer strconv over
  fmt](https://github.com/uber-go/guide/blob/master/style.md#prefer-strconv-over-fmt)
* [Avoid string-to-byte
  conversion](https://github.com/uber-go/guide/blob/master/style.md#avoid-string-to-byte-conversion)
* [Prefer Specifying Map Capacity
  Hints](https://github.com/uber-go/guide/blob/master/style.md#prefer-specifying-map-capacity-hints)

[Style](https://github.com/uber-go/guide/blob/master/style.md#style)

* [Be Consistent](https://github.com/uber-go/guide/blob/master/style.md#be-consistent)
* [Group Similar
  Declarations](https://github.com/uber-go/guide/blob/master/style.md#group-similar-declarations)
* [Import Group
  Ordering](https://github.com/uber-go/guide/blob/master/style.md#import-group-ordering)
* [Package Names](https://github.com/uber-go/guide/blob/master/style.md#package-names)
* [Function Names](https://github.com/uber-go/guide/blob/master/style.md#function-names)
* [Import Aliasing](https://github.com/uber-go/guide/blob/master/style.md#import-aliasing)
* [Function Grouping and
  Ordering](https://github.com/uber-go/guide/blob/master/style.md#function-grouping-and-ordering)
* [Reduce Nesting](https://github.com/uber-go/guide/blob/master/style.md#reduce-nesting)
* [Unnecessary Else](https://github.com/uber-go/guide/blob/master/style.md#unnecessary-else)
* [Top-level Variable
  Declarations](https://github.com/uber-go/guide/blob/master/style.md#top-level-variable-declarations)
* [Prefix Unexported Globals with
  _](https://github.com/uber-go/guide/blob/master/style.md#prefix-unexported-globals-with-_)
* [Embedding in Structs](https://github.com/uber-go/guide/blob/master/style.md#embedding-in-structs)
* [Use Field Names to Initialize
  Structs](https://github.com/uber-go/guide/blob/master/style.md#use-field-names-to-initialize-structs)
* [Local Variable
  Declarations](https://github.com/uber-go/guide/blob/master/style.md#local-variable-declarations)
* [nil is a valid slice](https://github.com/uber-go/guide/blob/master/style.md#nil-is-a-valid-slice)
* [Reduce Scope of
  Variables](https://github.com/uber-go/guide/blob/master/style.md#reduce-scope-of-variables)
* [Avoid Naked
  Parameters](https://github.com/uber-go/guide/blob/master/style.md#avoid-naked-parameters)
* [Use Raw String Literals to Avoid
  Escaping](https://github.com/uber-go/guide/blob/master/style.md#use-raw-string-literals-to-avoid-escaping)
* [Initializing Struct
  References](https://github.com/uber-go/guide/blob/master/style.md#initializing-struct-references)
* [Initializing Maps](https://github.com/uber-go/guide/blob/master/style.md#initializing-maps)
* [Format Strings outside
  Printf](https://github.com/uber-go/guide/blob/master/style.md#format-strings-outside-printf)
* [Naming Printf-style
  Functions](https://github.com/uber-go/guide/blob/master/style.md#naming-printf-style-functions)

[Patterns](https://github.com/uber-go/guide/blob/master/style.md#patterns)

* [Test Tables](https://github.com/uber-go/guide/blob/master/style.md#test-tables)
* [Functional Options](https://github.com/uber-go/guide/blob/master/style.md#functional-options)

## Standard Go Project Layout

Inasmuch as possible, Go projects should follow the layout that is detailed in the [Standard Go
Project Layout](https://github.com/golang-standards/project-layout/#standard-go-project-layout).

## "Line of Sight" Coding Best Practice

Whenever possible, code should be written such that the normal (or "happy path") code flow has
minimal indentation, with the error handling being indented and dealt with first. This practice
eliminates unnecessary `else` blocks, and improves the readability of code by allowing the normal
("happy") path to be scanned quickly.

References:

* [Indent Error Flow](https://github.com/golang/go/wiki/CodeReviewComments#indent-error-flow)

* [Things in Go I Never Use](https://www.youtube.com/watch?v=5DVV36uqQ4E&feature=youtu.be&t=660)
  video by Mat Ryer

## Unit Testing Best Practices

### Table Drive Testing

In many cases, unit testing of a function or a section of code involves iterating the same test
operations with different input conditions. In these cases, it is usually possible, and preferred,
to use table-driven testing. This is described in the [Table Driven
Tests](https://github.com/golang/go/wiki/TableDrivenTests) wiki. Using this technique, the actual
test iterates through a table of input conditions and expected results. This allows the actual test
code to be reused for different test cases.

## Package Management

References:

[Using Go
Modules](https://files.slack.com/files-pri/T0A233U2Z-FR043S136/download/local-dev-go-mod.mp4) video
by Kumbirai Tanekha

[Go Modules](https://github.com/golang/go/wiki/Modules) wiki

[Using Go Modules](https://blog.golang.org/using-go-modules)

## Checking Your Code with `golint` and `go vet`

Before pushing code up to a repository, the following commands can be run to check for errors:

```
cd <top-of-source-tree>
golint ./...
go vet
```

## Appendix

### References / Further Reading

[Golang language specification](https://golang.org/ref/spec)

[Tour of Go](https://tour.golang.org/)

[How to Write Go Code](https://golang.org/doc/code.html)

[Effective Go](https://golang.org/doc/effective_go.html) Style Guide

[Go Code Review
Comments](https://github.com/golang/go/wiki/CodeReviewComments#go-code-review-comments)

[Common Go Coding Mistakes](https://github.com/golang/go/wiki/CommonMistakes)

[Awesome Go](https://awesome-go.com/): A curated list of awesome Go frameworks, libraries and
software.

Video: [Using Go
Modules](https://files.slack.com/files-pri/T0A233U2Z-FR043S136/download/local-dev-go-mod.mp4) by
Kumbirai Tanekha

[Go Modules](https://github.com/golang/go/wiki/Modules) wiki

[Using Go Modules](https://blog.golang.org/using-go-modules)

Video: [Go Best Practices](https://www.youtube.com/watch?v=MzTcsI6tn-0&feature=youtu.be&t=1457) by
Ashley McNamara & Brian Ketelsen

Video: [Things in Go I Never
Use](https://www.youtube.com/watch?v=5DVV36uqQ4E&feature=youtu.be&t=660) by Mat Ryer (Good overview
of "Line-of-Sight" coding)

[Context Use and
Misuse](https://peter.bourgon.org/go-for-industrial-programming/#context-use-and-misuse) by Peter
Bourgon

[Golang Articles](https://github.com/golang/go/wiki/Articles)

[Golang `template` Package](https://golang.org/pkg/text/template/)
