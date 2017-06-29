# Case Study - American Fuzzy Lop

AFL is well known evolutionary fuzzer, capable of operating in both white-box and black-box modes.
It is designed primarily for programs written in the C family languages, and integrates well with the LLVM toolchain.

## Design Principles
AFL is designed for practicality above all else. It is extremely easy to use, often requiring no configuration at all.

## Workings
AFL tracks behavior by injecting code to detect branches.
Each transition is represented by a tuple of the form (START_BRANCH, END_BRANCH), and a series of these tuples represent an execution path.
The performance of input test cases is measured by the number of tuple transitions is causes the program to go through.
Input test cases are stored in a queue.
If a mutated test cases produces a significant difference in the number of tuples, it is added to the queue.
AFL also routinely culls the input queue, to remove test cases who's edge coverage is a strict superset of another test case.

The actual fuzzing process and test case generation/mutation can vary.
In the beginning, AFL tends to use more deterministic methods, such as:
- Sequential bit flips with varying lengths and stepovers,
- Sequential addition and subtraction of small integers,
- Sequential insertion of known interesting integers (0, 1, INT_MAX, etc)
This helps since deterministic methods tend to produce more compact test cases.
It then proceeds to more non-deterministic strategies such as stacked bit-flips, insertions, deletions, arithmetic, and so on.

AFL can also run in black-box mode, using QEMU (in user emulation mode) to track branches.
