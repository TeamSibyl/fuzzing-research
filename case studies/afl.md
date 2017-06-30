# Case Study - American Fuzzy Lop

AFL is well known evolutionary file fuzzer, capable of operating in both white-box and black-box modes.
It is designed primarily for programs written in the C family languages, and integrates well with the LLVM toolchain.

## Design Principles
AFL is designed for practicality above all else. It is extremely easy to use, often requiring no configuration at all.

## Workings
AFL stores uses binary files as test cases, and tracks behavior by injecting code to detect branches.
Each transition between branches is represented by a tuple of the form (START_BRANCH, END_BRANCH), and a series of these tuples represent an execution path.
The performance of input test cases is measured by the number of tuple transitions is causes the program to go through.
Input test cases are stored in a queue.
AFL does not perform crossovers, relying entirely on bit manipulation and other mutations.
If a mutated test cases produces a significant difference in the number of tuples, it is added to the queue.
AFL also routinely culls the input queue, to remove test cases who's edge coverage is a strict superset of another test case.

The actual fuzzing process and test case generation/mutation can vary.
In the beginning, AFL tends to use more deterministic methods, such as:
- Sequential bit flips with varying lengths and stepovers
- Sequential addition and subtraction of small integers
- Sequential insertion of known interesting integers (0, 1, INT_MAX, etc)
This helps since deterministic methods tend to produce more compact test cases, with small differences between .
It then proceeds to more non-deterministic strategies such as stacked bit-flips, insertions, deletions, arithmetic, and so on.

AFL also periodically trims test cases to reduce their file size, to combat the gradual growth that iterative mutations produce.
This drastically improves performance, both because smaller files are easier to test, and to increase the effectiveness of further mutations(if the test cases was not trimmed, mutations may happen in irrelevant blocks, wasting time and space).
If the trimmed file produces the same execution trace as its parent, it replaces the parent file.

AFL can also run in black-box mode, using QEMU (in user emulation mode) to track branches.
