# Fuzzing
A brief overview of fuzzing.

## What is fuzzing anyway?

>Fuzzing or fuzz testing is an automated software testing technique that involves
>providing invalid, unexpected, or random data as inputs to a computer program.
>
> -Wikipedia

Fuzzing is esseantially a brute-force technique that bombards the target program/system with malformed input with the goal of detecting an edge case, memory allocation issue, or other type of bug.


## Components

A fuzzer generally consists of three parts:

 ### Test case generator

The test case generator creates test cases for the engine to run. It is only concerned with the test case itself, and not in how it is executed.
Often, the test case generator has little to no information on the attack surface.

There are quite a few viable techniques for generating these test cases.
These techniques vary mostly in terms of intelligence; does the generator operate according to a ruleset/grammar/whatever, or does it simply generate random strings?

There are quite a few concerns to be aware of when creating test cases:

1. For many attack surfaces, the solution space is very large(practically infinite in many cases). In these cases, (dumber) brute-force approaches may not perform well.
2. Many communication protocols are quite stringent, and require exchanges in a certain format(such as key exchanges or handshakes), and they will kick (or ban) a client that refuses to comply. In these cases, the generator needs to follow some rules.
3. On the other hand, if the test cases conform _too_ stringently to the protocol, they may miss errors caused by the server being unable to correctly handle misbehaving clients.
4. Many attack targets depend on or are supported by other software. Usually, this software is either resistant to bugs, or is simply not of any interest.
This can complicate the process of tailoring test cases to focus on the target software, and in the detection of bugs.
For example, most websites run on top of apache.
Even if you can get the website itself to crash(which is frighteningly easy in most cases), Apache itself will not crash. If your program detects errors by listening to the Apache logs, it may miss the failures entirely.

## Detector

The detector tries to detect when an error has occurred. 
