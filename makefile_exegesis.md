# Makefile

## Introduction to Build systems
Makefile is a build system for C. What are build systems? let's discuss about them with an example.

`gcc filename.c src.c -o filename`, this is a command for compiling a file in C.
- This command will firstly convert both the C files into their object files.
- Then a linker will lVariabink those object files and make an executable out of them.

- In this case whenever any one of the C files change, both the files will get converted into their respective 
object(".o") files and then linker will link them together to produce an executable.
- In this way of compilation, everytime the files will get converted to their object files. So, if there are 20 
C-files then everytime 21 commands(20 for converting .c into .o and 1 to link all the .o files) will run to make
an executable out of them.
- You can easily predict that this way of compilation will take a longer time to execute. Time complexity increase.

To manage this, we need build systems.
*Build system* ensures that only those files which are changed after the last execution will again get converted to their object(".o") files.
Above example can be solved using build systems. Now it will run only 2 commands, one for converting the changed C file to its object file and second for linking the object files.


## Targets and Dependencies
*Targets* and *Dependencies* are most essential components to write a Makefile.
There are targets and these targets are dependent on various dependencies, whenever any of the dependencies changes, target code will get executed again.

### Representation of Targets and Dependencies
```
test_string_split: test_string_split.o stringly.o
```
Here, Target = test_string_split and Dependencies are test_string_split.o and stringly.o.
To execute this further, the rules for getting "test_string_split.o" and "stringli.o" should be written.


## Variables
### Simple Variables in Makefile
Variables are those in which a value can be assign.
`var_name := 23`, assigning the value in some variable.
This variable can be accessed anywhere in your Makefile by writing `$(variable)`.
- In Makefile, variables always contain string values, it internally converts any integer to string.


### Automatic variables
There are various automatic variables.
- `@a` - Replaced with target
- `@^` - Replaced with all the dependencies
- `@<` - Replaced with first dependency


## Pattern matching/Stemming
- "%" is used for pattern matching.
```
test_string_split: test_string_split.o stringly.o
gcc test_string_split.o stringly.o -o test_string_split

test_string_slice: test_string_slice.o stringly.o
gcc test_string_slice.o stringly.o -o test_string_slice

```

- In above example, there are 2 targets with common pattern that their name starts with "test_".
`test_%: test_% stringly.o`
This target can be used to run test_string_split as well as test_string_slice. When one writes `make test_string_split`, % will get replaced with *string_split* everywhere in the code.






