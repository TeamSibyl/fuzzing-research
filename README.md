# Fuzzing

A brief overview of research and progress of the 2017 CCBD fuzzing project.

# Problem Statement
Given a binary executable, profile it, attempting to identify:
1. Overall program function
2. Function of each segment
3. Control paths that perform certain functions

## Important Questions

1. What are the broad classes of program functionality?
2. What are all the types of control paths we are interested in(file I/O, network calls, etc)?
3. How much of an ML approach do we wish to take?
4. How much static analysis should we use?
Should everything be static, or should we include some dynamic analysis as well(Driller)?  

# Contributors
1. Sumeet Padavala
