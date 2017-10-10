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
