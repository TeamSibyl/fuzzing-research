# (State of) The Art of War: Offensive Techniques in Binary Analysis

## Forward
This document has been written with the main problem statement in mind(analyzing binaries, searching for control paths and segments), and thus large sections of the paper may not be covered.
Implementation-level details have also been omitted wherever deemed irrelevant.
This document should contain more-or-less everything you need to work on this project.

Written by Sumeet Padavala.

## Overview

This paper discusses the benefits, downsides, difficulties, and potential of binary analysis, and then details the binary analysis framework we use, called angr.

## Preliminaries

Despite the recent rise of interpreted languages, and languages run by JIT compilers, programs written in languages that compile down to binary have not decreased in popularity or importance. This is largely because of 3 factors:
1. Even interpreted languages often produce at least some binary, for performance sake
2. Core systems(e.g kernels) cannot be written in interpreted languages
3. IoT devices do not have the clock cycles to spare to run interpreted languages.
Unfortunately, many, if not most, of these languages provide little in the way of security, leading to a plethora of memory corruption issues.
It is also important to note that compilers/interpreters are not perfect. It is entirely possible for a theoretically perfect program(according to that language) to produce strange bugs at compile time.
Binary analysis is capable of detecting and fixing many of these issues, and in today's world, with more and more value being placed online, protecting it has never been more important.

## Automated Binary analysis

Over the last few years, immense strides have been made in developing automated binary analysis tools and systems.
However, there are still quite a few challenges and trade-offs:
1. Replayability: An analyzer that runs the whole program from the beginning can reliably predict how a control path will work, however many analyzers only observe sections of code, and thus may not be able to reliable determine their behavior and purpose.
2. Semantic insight: An analyzer may notice a set of behaviors for a segment, but may not be able to reason about what that segment of code does, or why it produced that behavior.
A highly replayable analysis would require a lot of state analysis.
Achieving a high level of semantic insight may require a lot of analysis into all the possible execution streams of a segment, which can quickly become intractable.

## Static techniques

Static techniques attempt to reason about a program without executing it.
Usually, these programs are interpreted in an abstract space, with data, OS interaction, and often the code itself being abstracted.
In general, static analysis tools do not produce _replayable_ results, as the tool does not actually know how to run the segment it is analyzing.
These tools also tend to operate on simpler data domains, reducing their _semantic insight_.
Ultimately, there are limits on how much information a static analysis tool can produce, since any program written in a language more complex that a _context-free grammar_ is subject to the halting problem.
There are two main types of static analysis systems; those that model the data itself, and those that model the execution of the program as a _control flow graph_.

## Dynamic techniques

Dynamic techniques actually run the code, attempting to find vulnerabilities and identify behaviors.
There are two major techniques:
1. Fuzzing: Fuzzing is a technique primarily used to explore a program, searching for inputs that crash the program(or produce some other bug). Fuzzing systems can be useful in rapidly expanding the search scope of the program, but do not produce much semantic insight, particularly in identifying (implicit) protocols, and in identifying relationships in the data flowing in and out of the process.
They are generally of limited use for our goal of identifying binary semantics, except for augmenting other techniques.
2. Symbolic execution: This technique "runs" the program with symbols as input, rather than actual inputs.
When control flow statements are executed, the system can then determine which values of the symbols cause which paths to be taken, allowing it to understand much more of the semantics of the program than nearly any other process.
This is a quite capable tool, but suffers from the same path explosion problem that static analysis systems face, and thus is not very scalable in it's basic form.

There have been various attempts to marry these approaches together, leading to techniques such as _symbolic-assisted fuzzing_.

# The angr framework

angr is a binary analysis framework, written (mostly) in Python 2. It ties together a large number of projects and approaches into a single platform.

## Design goals
1. Cross-architecture support
2. Cross-platform support
3. Support for many usage paradigms
4. Usability

## Submodules

### Intermediate representation
In order to transparently support multiple architectures, angr converts binaries to an intermediate representation(_IR_), apon which analysis is produced. Angr utilizes the libVEX IR lifter, originally designed for Valgrind, and uses pyVEX to expose it to the analysis systems.

### Binary loading
The task of loading an application binary into the analysis
system is handled by a module called CLE.
CLE abstracts over different binary formats to handle loading a given binary
and any libraries that it depends on, resolving dynamic
symbols, performing relocations, and properly initializing the
program state.

### Program state representation
Angr represents the program state of the (loaded) program using the module SimuVEX.
The state is represented as defined by a set of state plugins.
There are currently plugins for registers, symbolic and abstract memory, full POSIX state, log, solver, and architecture, each of which expose a different section or type of state representation.
SimuVEX also supports the most basic analysis operation: run a block of code(a _SimuRun_) with an input, and get one or more possible outputs.
This _SimuRun_ can either be a block of _VEX_ code, or even a Python function(which is how system calls are modeled in angr).

### Data model
The data in the registers and memory(represented in _SimState_) are represented in terms of _claripy_ abstractions.
_Claripy_'s main function is constraint solving, primarily for symbolic analysis tasks.
Claripy stores expressions as a symbol tree, and is composed of:
1. *Backends*, providing different types of representation(_data domains_) as well as solvers for those domains
2. *Frontends*, providing an interface to the backend, and allowing the user to trigger the constraint solving process, amng other things.

### Full-program analysis
Angr's main API to the whole suite is the Project class, which represents a single binary, with all it's associated representations, states, etc.
All other submodules can be accessed from this object.
There are two other interfaces of note:
1. PathGroup: Used for symbolic execution, tracks all the paths currently being explored.
2. Analysis: Manages the complete lifecycle of any full-program analysis tasks.

## Task Implementations
TODO
