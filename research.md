# Research

Brief overview of complete and ongoing research in the field of fuzzing and testing in general.

Vuzzers: Aplication aware Evolutionary fuzzing

http://www.cs.vu.nl/~giuffrida/papers/vuzzer-ndss-2017.pdf

In this paper, we present an application-aware evolutionary fuzzing strategy that does not require any prior knowledge of the application or input format. 
We implement our fuzzing strategy in VUzzer and evaluate it on three different datasets: DARPA Grand Challenge binaries (CGC), a set of real-world applications (binary input parsers), and the recently released LAVA dataset. On all of these datasets, VUzzer yields significantly better results than state-of-the-art fuzzers, by quickly finding several existing and new bugs. 

1) We show that modern fuzzers can be “smarter” without resorting to symbolic execution (which is hard to scale). Our application-aware mutation strategy improves the input generation process of state-of-the-art fuzzers such as AFL by orders of magnitude.
2) We present several application features to support meaningful mutation of inputs.
3) We evaluate VUzzer, a fully functional fuzzer that implements our approach, on three different datasets and show that it is highly effective.
4) To foster further research in the area and in support of open science, we are open sourcing our VUzzer prototype, available at https://www.vusec.net/projects/fuzzing.

VUzzer  is a greybox fuzzer.

ClusterFuzz:

https://nullcon.net/website/archives/ppt/goa-15/analyzing-chrome-crash-reports-at-scale-by-abhishek-arya.pdf

http://dev.chromium.org/Home/chromium-security/bugs/using-clusterfuzz

Goals:
Automated crash detection,analysis and management
Fully reproducible and minimized testcases
Real-time regression and fixed testing


IFuzzer: An Evolutionary Interpreter Fuzzer using Genetic Programming

http://www.cs.vu.nl/~herbertb/download/papers/ifuzzer-esorics16.pdf

This paper presents an automated evolutionary fuzzing technique to
find bugs in JavaScript interpreters.

It is a black box fuzzer.

 IFuzzer takes a language’s context-free grammar as input
for test generation. It uses the grammar to generate parse trees and to extract
code fragments from a given test-suite.IFuzzer leverages the fitness improvement mechanism within Genetic Programming
to improve the quality of the generated code fragments.

In summary, this paper makes the following contributions:

1. We introduce a fully automated and systematic approach for code generation
for interpreter testing by mapping the problem of interpreter fuzz testing onto
the space of evolutionary computing for code generation. By doing so, we
establish a path for applying advancements made in evolutionary approaches
to the field of interpreter fuzzing.
2. We show that Genetic Programming techniques for code generation result
in a diverse range of code fragments, making it a very suitable approach
for interpreter fuzzing. We attribute this to inherent randomness in Genetic
Programming.
3. We propose a fitness function (objective function) by analyzing and identifying
different code parameters, which guide the fuzzer to generate inputs
which can trigger uncommon behavior within interpreters.
4. We implement these techniques in a full-fledged (to be) open sourced fuzzing
tool called IFuzzer that can target any language interpreter with minimal
configuration changes.
5. We show the effectiveness of IFuzzer empirically by finding new bugs in
Mozilla’s JavaScript engine SpiderMonkey—including several exploitable security
vulnerabilities.

Demystifying Fuzzers:

http://www.blackhat.com/presentations/bh-usa-09/EDDINGTON/BHUSA09-Eddington-DemystFuzzers-PAPER.pdf

Throughout this paper criteria for fuzzer adoption will be
discussed and information about a selection of fuzzers provided, both open source and commercial. At
the end we will examine several corporate use cases and select one or more fuzzer that best meets the
perceived criteria. 

This paper also provides comparisons between various fuzzers and categorieses them into different 
types such as general,network,file,etc.


Sulley:

https://www.google.co.in/url?sa=t&rct=j&q=&esrc=s&source=web&cd=10&cad=rja&uact=8&ved=0ahUKEwiNoIj6yJ7UAhXBzFQKHdHXD1IQFghcMAk&url=https%3A%2F%2Fwww.htbridge.com%2Fpublication%2FThe-Sulley-Fuzzing-Framework.pdf&usg=AFQjCNG8_xM_PQDJGF-vXvft-WK0tbSuUg&sig2=vpwwwrwWcGK9EDWPJNlrHw

http://www.fuzzing.org/wp-content/SulleyManual.pdf

? It is a fuzzer development and fuzz testing framework consisting of multiple extensible components.  
? The real goal of this excellent framework is to simplify not only data representation but to simplify data transmission and target monitoring as well. 
? It is capable to detect, track and categorize the uncovered faults into the fuzzed application.  
? Sulley can also fuzz in parallel mode, which significantly increase the fuzzing speed.  
? It can automatically determine what unique sequence of test cases has triggered the faults

Sulley is written as a set of Python libraries, and configuration and protocol definitions happen in Python.

SPIKE: C based fuzzer creation kit

https://www.google.co.in/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwjqqLLU057UAhVEs48KHSceCpwQFggqMAE&url=https%3A%2F%2Fwww.blackhat.com%2Fpresentations%2Fbh-usa-02%2Fbh-us-02-aitel-spike.ppt&usg=AFQjCNEJLb4KGAy_0r7bxrv8Y3UXOSEdaQ&sig2=UJ_aTkuGGAnVmknDKfAzJw

SPIKE is actually a fuzzer creation kit, providing an API that allows a user to create their own fuzzers for network based 
protocols using the C programming language. SPIKE defines a number of primitives that it makes available to C coders, which
 allows it to construct fuzzed messages called “SPIKES” that can be sent to a network service to hopefully induce errors.