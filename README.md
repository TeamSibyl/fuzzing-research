# Fuzzing

A brief overview of fuzzing.

## What is fuzzing anyway?

> Fuzzing or fuzz testing is an automated software testing technique that involves providing invalid, unexpected, or random data as inputs to a computer program.
>
> -Wikipedia

Fuzzing is essentially a brute-force technique that bombards the target program/system with malformed input with the goal of detecting an exploitable vulnerability.

Fuzzing's primary advantage over other security techniques is its inherent randomness(fuzziness), which allow it to detect all sorts of complicated bugs in a fairly intelligent manner.

## Why fuzz?

In today's software, many bugs are actually pretty simple.
A significant portion of bugs relate to:
1. Memory handling
2. Buffer/Stack/List overflows
3. Improper edge-case handling

Many well-known bugs and vulnerabilities fall into this category. For example:
1. Heartbleed was a buffer over-read issue in OpenSSL.
2. The Mirai botnet's _only_ attack method was a simple dictionary attack.
3. Shellshock was a problem of incorrectly sanitizing environment variables in the BASH environment.

Attack surfaces are getting more complicated, and as new technologies arise and build upon each other, this complexity will only increase.
Fuzzing can provide a way to automatically detect these sorts of bugs, cutting down on tester man-hours.
With the latest wave of more intelligent fuzzers, this process is also computationally viable.

Fuzzing is particularily useful for covering your bases, and removing a significant number of simple (yet exploitable) vulnerabilities.

## What about unit tests?

Unit tests are a crucial technique for ensuring program quality and correctness.
The issue with unit tests is that they are meant to ensure a unit is perfoming correctly, not in an attempt to figure out what is wrong.
This means that unit tests are rarely hardened enough to ensure the unit can handle any possible input it may reasonably be expected to handle, nor is it economical to write unit tests at that level of detail and coverage.
They are also written with knowledge of the purpose of the code they are meant to test, and thus any inadverdent assumptions made in the design of that unit creep up into the test itself.
Fuzzing operates with little to no information on the actual program.
Any such info is usually in feedback to a test it performed.

Unit tests and fuzzing are almost orthogonal, and neither justifies not using the other.

## What about penetration testing?

Penetration testing and fuzzing are complementary techniques.
Penetration testing relies on actual humans playing the adversarial role, attempting to break into the system.
There are a handful of issues here:
1. Penetration testing is slow. It requires actual humans, attacking actual systems, and thus can only happen at the speed of human thought.
2. Scaling is difficult, since it requires hiring more testers, as well as building additional targets to attack.
3. All testing is black-box testing. A penetration tester usually has no knowledge of which parts of the code they reached, which makes it difficult to know how much coverage a penetration test actually achieved.
4. Penetration testing can miss various subtle or strange issues that a human may not even consider.
For example, a tester may not test if adding extra line-ending characters or a newline in arbitrary places causes an issue, and a penetration tester wouldn't fli random bits in a message to see i the system would handle it differently.  

Fuzzing, however, is entirely automated.
Once supplied details on the commnication protocols and detection paramters, it is able to operate entirely automatically.

In addition, scaling a fuzzer merely requires more computational resources.

Fuzzing can also function as a preliminary assesment tool in penetration testing, allowing a tester to quickly find an entry point or points of concern.
For this purpose, Kali Linux includes 3 dedicated fuzzing tools(powerfuzzer, sfuzz, wfuzz).

## Trophies

Fuzzing does work! Here are some examples:
1. [This page](https://bugs.chromium.org/p/oss-fuzz/issues/list?can=1&q=status%3AFixed%2CVerified+Type%3ABug%2CBug-Security+-component%3AInfra+) tracks all the recent bugs that oss-fuzz, Google's cloud-based fuzzing platform, has discovered, and this essay
2. [This essay](https://www.dwheeler.com/essays/heartbleed.html) discusses how fuzzing could have detected heartbleed long before it had already happened.

[This page](./internals.md) describes how fuzzers work.
