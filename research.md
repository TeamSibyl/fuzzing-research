# Research

Brief overview of complete and ongoing projects and research in the field of fuzzing and testing in general.

## [Vuzzers: Aplication aware Evolutionary fuzzing](http://www.cs.vu.nl/~giuffrida/papers/vuzzer-ndss-2017.pdf)

This paper covers an application-aware evolutionary fuzzing strategy that does not require proir knowledge of the application format.
The strategy is implemented on VUzzer, and claims to outperform AFL.

> Note: VUzzer  is a greybox fuzzer.

## [ClusterFuzz](https://github.com/google/oss-fuzz/blob/master/docs/clusterfuzz.md)

ClusterFuzz is a distributed cloud fuzzing platform, and was originally designed for fuzzing Chromium at scale.

It is the backbone of OSS-fuzz, a project that seeks to fuzz-test all kinds of open-source projects.

## SPIKE: C based fuzzer creation kit

SPIKE is the grandfather of all fuzzers, and it ther first major effort to abstract fuzzers into a framework.  
It functions as a fuzzer creation kit, providing an API that allows a user to create their own fuzzers for network based protocols using the C programming language.
Unfortunately, SPIKE has terible documentation and support, and today has fallen mostly into obscurity.

## [IFuzzer: An Evolutionary Interpreter Fuzzer using Genetic Programming](http://www.cs.vu.nl/~herbertb/download/papers/ifuzzer-esorics16.pdf)

This paper presents an automated evolutionary fuzzing technique to
find bugs in JavaScript interpreters.

It is a black box fuzzer.

IFuzzer takes a language's context-free grammar as input
for test generation. It uses the grammar to generate parse trees and to extract code fragments from a given test-suite, and utilizes some evolutionary strategies to improve the quality of the generated code fragments.

In summary, this paper makes the following contributions:

1.  We introduce a fully automated and systematic approach for code generation for interpreter testing by mapping the problem of interpreter fuzz testing onto the space of evolutionary computing for code generation.
By doing so, we establish a path for applying advancements made in evolutionary approaches to the field of interpreter fuzzing.
2.  We show that Genetic Programming techniques for code generation result in a diverse range of code fragments, making it a very suitable approach for interpreter fuzzing. We attribute this to inherent randomness in Genetic Programming.
3.  We propose a fitness function (objective function) by analyzing and identifying different code parameters, which guide the fuzzer to generate inputs which can trigger uncommon behavior within interpreters.
4.  We implement these techniques in a full-fledged (to be) open sourced fuzzing tool called IFuzzer that can target any language interpreter with minimal
configuration changes.
5.  We show the effectiveness of IFuzzer empirically by finding new bugs in Mozilla's JavaScript engine SpiderMonkey including several exploitable security
vulnerabilities.

## [Demystifying Fuzzers:](http://www.blackhat.com/presentations/bh-usa-09/EDDINGTON/BHUSA09-Eddington-DemystFuzzers-PAPER.pdf)

Throughout this paper criteria for fuzzer adoption will be
discussed and information about a selection of fuzzers provided, both open source and commercial.
At the end we will examine several corporate use cases and select one or more fuzzer that best meets the
perceived criteria.

This paper also provides comparisons between various fuzzers and categorieses them into different types such as general,network,file,etc.


## [Sulley:](http://www.fuzzing.org/wp-content/SulleyManual.pdf)

Sulley is a Python framework for fuzzing.
It abstracts a fuzzer into a handful of components, and allows a developer to easily write a new one for any program/attack surface.
Sulley also has built-in parallel processing capabilities.  

SPIKE: C based fuzzer creation kit

SPIKE is actually a fuzzer creation kit, providing an API that allows a user to create their own fuzzers for network based 
protocols using the C programming language. SPIKE defines a number of primitives that it makes available to C coders, which
 allows it to construct fuzzed messages called “SPIKES” that can be sent to a network service to hopefully induce errors.

 
 Fuzzing Frameworks:
 
 http://www.blackhat.com/presentations/bh-usa-07/Amini_and_Portnoy/Whitepaper/bh-usa-07-amini_and_portnoy-WP.pdf
 
 Fuzzers List:
 
 https://www.peerlyst.com/posts/resource-open-source-fuzzers-list
 
 Evolutionary Fuzzing System:
 
 https://www.vdalabs.com/tools/EFS.pdf
 
Improving fuzzers:

http://www.cs.utah.edu/~chenyang/papers/thesis_draft.pdf
http://download.xuebalib.com/xuebalib.com.12213.pdf