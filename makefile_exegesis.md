# Makefile

## Introduction to Build systems
A Makefile is a build system for C. What are build systems? Let's discuss them with an example.

`gcc filename.c src.c -o filename`, this is a command for compiling a file in C.
- This command will first convert both the C files into their respective object files.
- Then a linker will link those object files and create an executable out of them.

- In this case, whenever any one of the C files changes, both the files will be converted into their respective 
object(".o") files and then the linker will link them together to produce an executable.
- In this method of compilation, everytime the files will be converted to their object files. So, if there are 20 
C-files then everytime 21 commands(20 for converting .c into .o and 1 to link all the .o files) will run to make
an executable out of them.
- You can easily predict that this way of compilation will take a longer time to execute. The time complexity increase.

To manage this, we need build systems.
A *Build system* ensures that only those files which have changed since the last execution will be converted to their object(".o") files again.
Above example can be solved using build systems. Now it will run only 2 commands, one for converting the changed C file to its object file and second for linking the object files.


## Targets and Dependencies
*Targets* and *Dependencies* are most essential components for writing a Makefile.
There are targets and these targets depend on various dependencies. Whenever any of the dependencies change, the target code will be executed again.

### Representation of Targets and Dependencies
```
test_string_split: test_string_split.o stringly.o
```
Here, Target = test_string_split and Dependencies are test_string_split.o and stringly.o.
To execute this further, the rules for getting "test_string_split.o" and "stringli.o" should be written.


## Variables
### Simple Variables in Makefile
Variables are used to assign values.
`var_name := 23`, assigning the value in some variable.
This variable can be accessed anywhere in your Makefile by writing `$(variable)`.
- In Makefile, variables always contain string values. In the above example the value of var_name is "23".


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

- In the above example, there are 2 targets with a common pattern that their name starts with "test_".
`test_%: test_% stringly.o`
This target can be used to run both *test_string_split* and *test_string_slice*. When one writes `make test_string_split`, % will get replaced with *string_split* everywhere in the code.






