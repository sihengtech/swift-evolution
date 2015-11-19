# Swift Programming Language Evolution

This repository tracks the ongoing evolution of Swift. It contains:

* Goals for upcoming Swift releases (this document)
* The [Swift evolution review schedule](schedule.md) tracking proposals to change Swift
* The [Swift evolution process](process.md) that governs the evolution of Swift.

This document describes goals for the Swift language on a per-release
basis, usually listing minor releases adding to the currently shipping
version and one major release out.  Each release will have many
smaller features or changes independent of these larger goals, and not
all goals are reached for each release.

Goals for past versions are included at the bottom of the document for
historical purposes, but are not necessarily indicative of the
features shipped. The release notes for each shipped version are the
definitive list of notable changes in each release.

## Development major version:  Swift 3.0

Expected release date: Fall 2016

The primary goal of this release is to stabilize the binary interface
of the language and standard library. As part of this process, we will
focus and refine the language to provide better overall consistency in
feel and implementation. Swift 3.0 will contain *source-breaking*
changes from Swift 2.x where necessarily to support these goals. More
concretely, this release is focused on several key areas:

* **Stable ABI**: Stabilize the binary interface (ABI) to guarantee a level of binary compatibility moving forward. This involves finalizing runtime data structures, name mangling, calling conventions, and so on, as well as finalizing some of the details of the language itself that have an impact on its ABI. Stabilizing the ABI also extends to the Standard Library, especially it's data types are core algorithms. Successful ABI stabilization means that applications and libraries compiled with future versions of Swift can interact at a binary level with applications and libraries compiled with Swift 3.0, even if the source language changes.
* **Resilience**: Solve the general problem of [fragile binary interface](https://en.wikipedia.org/wiki/Fragile_binary_interface_problem), which currently requires that an application be recompiled if any of the libraries it depends on changes. For example, adding a new stored property or overridable method to a class should not require all subclasses of that class to be recompiled. There are several broad concerns for resilience:
  * *What changes are resilient?*: Define the kinds of changes that can be made to a library without breaking clients of that library. Source-compatible changes to libraries are good candidates for resilient changes, but such decisions also consider the effects on the implementation.
  * *How is a resilient library implemented?*: What runtime representations are necessary to allow applications to continue to work after making resilient changes to a library? This dovetails with the stabilization of the ABI, because the stable ABI should be a resilient ABI.
  * *How do we maintain high performance?*: Resilient implementations often incur more execution overhead than non-resilient (or *fragile*) implementations, because resilient implementations need to leave some details unspecified until load time, such as the specific sizes of a class or offsets of a stored property.
* **Portability**: Make Swift available on other platforms and ensure that one can write portable Swift code that works properly on all of those platforms.
* **Type system cleanup and documentation**: Revisit and document the various subtyping and conversion rules in the type system, as well as their implementation in the compiler's type checker. The intent is to converge on a smaller, simpler type system that is more rigorously defined and more faithfully represented by the type checker.
* **Complete generics**: Generics are used pervasively in a number of Swift libraries, especially the standard library. However, there are a number of generics features the standard library requires to fully realize its vision, including recursive protocol constraints, the ability to make a constrained extension conform to a new protocol (i.e., an array of `Equatable` elements is `Equatable`), and so on. Swift 3.0 should provide those generics features needed by the standard library, because they affect the standard library's ABI.
* **Focus and refine the language**: Despite being a relatively young language, Swift's rapid development has meant that it has accumulated some language features and library APIs that don't fit will with the language as a whole. Swift 3 will remove or improve those features to provide better overall consistency for Swift.

### Out of Scope

A significant part of delivering a major release is in deciding what
*not* to do, which means deferring many good ideas. The foll

* **Full source compatibility**: Swift 3.0 will not provide full
  source compatibility. Rather, it can and will introduce
  source-breaking changes needed to support the main goals of Swift
  3.0.

* **Concurrency**: Swift 3.0 relies entirely on platform concurrency
  primitives (libdispatch, Foundation, pthreads, etc.) for
  concurrency. Language support for concurrency is an often-requested
  and potentially high-value feature, but is too large to be in scope
  for Swift 3.0.

* **C++ Interoperability**: Swift's interoperability with C and
  Objective-C is one of its major strengths, allowing it to integrate
  with platform APIs. Interoperability with C++ libraries would
  enhance Swift's ability to work with existing libraries and APIs.
  However, C++ itself is a very complex language, and providing good
  interoperability with C++ is a significant undertaking that is out
  of scope for Swift 3.0.

### Accepted proposals

* [Removing currying `func` declaration syntax](proposals/0002-remove-currying.md)
* [Removing `var` from Function Parameters and Pattern Matching](proposals/0003-remove-var-parameters-patterns.md)
* [Remove the `++` and `--` operators](proposals/0004-remove-pre-post-inc-decrement.md)

## Development minor version:  Swift 2.2

Expected release date: Spring 2016

This release will focus on fixing bugs, improving
quality-of-implementation (QoI) with better warnings and diagnostics,
improving compile times, and improving performance.  It may also put
some finishing touches on features introduced in Swift 2.0, and
include some small additive features that don't break Swift code or
fundamentally change the way Swift is used. As a step toward Swift
3.0, it will introduce warnings about upcoming source-incompatible
changes in Swift 3.0 so that users can begin migrating their code
sooner.

### Accepted proposals

* [Allow (most) keywords as argument labels](proposals/0001-keywords-as-argument-labels.md)

[swift-evolution-mailing-list]: mailto:swift-evolution@swift.org  "The swift-evolution mailing list"