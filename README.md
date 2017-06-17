# Fuzzing

A brief overview of fuzzing.

## What is fuzzing anyway?

> Fuzzing or fuzz testing is an automated software testing technique that involves providing invalid, unexpected, or random data as inputs to a computer program.
> 
> -Wikipedia

Fuzzing is essentially a brute-force technique that bombards the target program/system with malformed input with the goal of detecting an edge case, memory allocation issue, or other type of bug.

Fuzzing's primary advantage over other security techniques is its inherent randomness(fuzziness), which allow it to detect all sorts of complicated bugs in a fairly intelligent manner.

## Why fuzz?

In today's software, many bugs are actually pretty simple stuff.
A significant portion of bugs relate to:
1. Memory handling
2. Buffer/Stack/List overflows
3. Improper edge-case handling

However, attack surfaces are also quite complicated, and as new technologies arise and build upon each other, this complexity will increase exponentially.
Fuzzing can provide a way to automatically detect these sorts of bugs, significantly cutting down on tester man-hours.
With the latest wave of more intelligent fuzzers being developed, the process is also fairly economical computationally.

Fuzzing is particularily useful for covering your bases, and removing a significant number of fairly simple (yet exploitable) vulnerabilities, potentially saving you and your organization the embarassment of being callled out for forgetting to check for buffer overflows or injecttion attacks.    

## What about unit tests?

Unit tests are onther crucial technique for ensuring program quality and correctness.
The issue with unit tests is that they test to ensure a unit is _right_, not in an attempt to figure out what is wrong.
They are also written with knowledge of the purpose of the code they are supposed to test, and thus any inadverdent assumptions made in the design of that unit creep up into the test itself.
Fuzzing, on the other hand, operates with little to no information on the actual program.
Any such info is usually in feedback to a test it performed.

Unit tests and fuzzing are largely orthogonal, and neither justifies not using the other.

## Trophies

Fuzzing really does work! Here are a few examples:
1. [This page](https://bugs.chromium.org/p/oss-fuzz/issues/list?can=1&q=status%3AFixed%2CVerified+Type%3ABug%2CBug-Security+-component%3AInfra+) tracks all the recent bugs that oss-fuzz, Google's cloud-based fuzzing platform, has discovered, and this essay
2. [This essay](https://www.dwheeler.com/essays/heartbleed.html) discusses how fuzzing could have detected heartbleed long before it had already happened.

## Components

A fuzzer generally consists of three parts:

### Test case generator

The test case generator creates test cases for the engine to run. It is only concerned with the test case itself, and not in how it is executed. Often, the test case generator has little to no information on the attack surface.

There are quite a few viable techniques for generating these test cases. These techniques vary mostly in terms of intelligence; does the generator operate according to a ruleset/grammar/whatever, or does it simply generate random strings?

There are quite a few concerns to be aware of when creating test cases:

1. For many attack surfaces, the solution space is very large(practically infinite in many cases). In these cases, (dumber) brute-force approaches may not perform well.
2. Many communication protocols are quite stringent, and require exchanges in a certain format(such as key exchanges or handshakes), and they will kick (or ban) a client that refuses to comply. In these cases, the generator needs to follow some rules.
3. On the other hand, if the test cases conform _too_ stringently to the protocol, they may miss errors caused by the server being unable to correctly handle misbehaving clients.
4. Many attack targets depend on or are supported by other software. Usually, this software is either resistant to bugs, or is simply not of any interest. This can complicate the process of tailoring test cases to focus on the target software, and in the detection of bugs. For example, most websites run on top of Apache. Even if you can get the website itself to crash(which is frighteningly easy in far too many cases), Apache itself is almost impossible to crash. If your program detects errors by listening to the Apache logs, it may miss the failures entirely.

Test-case generators are usually paired with a mutation engine, which allows it to generate new test cases from previous ones.

One common use of this is in corrupting valid inputs.

### Detector (a.k.a Monitor)

The detector tries to detect if an error has occurred, after the execution of a test case. In general, detectors are split into categories based on their awareness of the source code of the fuzz target:

- Black box: These detectors have no knowledge whatsoever of the structure of the target program/system.
They can only detect bugs by either checking the program's logs and whether or not it crashed.
These detectors tend to be fast, simple, and widely applicable, however their accuracy is often insufficient
- White box: These detectors use static analysis to better understand the program.
They can detect potentially troublesome parts of the code and automatically generate test cases meant to test those bits of code.
These detectors tend to have the highest code coverage, but are (prohibitively) slow and expensive to run.
- Grey box: These detectors function similar to black-box, but they watch the running program more closely.
One common technique is to run the program in a debugger.
This gives the detector access few useful tools such as watches and breakpoints.

Detectors also vary based on whether the target is running locally or remotely, and whether or not the target system/program has multiple processes/components.

### Fuzzing engine

The fuzzing engine is the core of the entire fuzzer.
It controls the entire process, and is primarily responsible for executing testcases and recording the results.
It decides whether the testcase succeed in finding a bug, based on the feedback from the detector, and then decides what to do with that result.
Some fuzzers will try to mutate the testcase and then analyze all the testcases that produced the bug to try to discover the pattern. If the fuzzer is distributed, the engine is responsible for coordinating all of the different nodes.
