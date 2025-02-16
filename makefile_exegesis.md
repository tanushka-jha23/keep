# Makefile - A Build System

I love writing code in C. Sometimes, I find it a little hard to write code purely in C when it comes to a big project and when it's about compiling the files of that bigger project it is even more harder. Wait! Do you know what compilation is?
```
    #include <stdio.h>
    
    int main() {
        printf("Hello World!");
    }
```
You must have seen this code at some point of your life. To execute this code, you have to write the following command on your terminal.
`gcc main.c -o main`
This command will eventually give an executable file which you can run by writing "./main", on your terminal.
BUT, Have you ever thought about working of this command?

Let's understand the process of compilation in C step-by-step,

Here, In this example *main.c* file contains *printf* function. The execution of "printf" is written inside the standard file "stdio.c" of C. "stdio.c" is a dependency of "main.c". By including "stdio.h", you are including the dependency of "main.c".

- `gcc main.c -o main` internally attaches "stdio.c" as `gcc main.c stdio.c -o main`.
- Both the files (main.c and stdio.c) will be converted to their object files("main.o" and "stdio.o"). 
- Linker will link these object files and produce an executable file.

After getting the executable file, you can run this file using `./main` command. 
From the above example it is easyu to understand that whenever you compile a C file, it will be compiled in 3 steps.

Now, let's take another example to understand more,
`gcc main.c string_lib.c utils.c math_utils.c -o main`.

Here, "main.c" has 3 dependencies. Whenever any dependency changes the command runs and all the three dependent files will be converted to their object files. Then the linker will link them.
Everytime, this compilation will take 5 steps (4 steps to convert 4 C files to their object files and 1 step to link them).

Imagine a scenario where a file has 20 dependencies. In this case, everytime compilation occurs in 22 steps. 
Don't you think there's no need to do these 22 steps everytime?
Obviously, there is no need of converting all the files. Only those files, which got changed after the last compilation needs to be converted to their object files again.

Here, in such cases this way of compilation becomes slow and to solve this we use *BUILD SYSTEMS*.


## Build Systems and Makefile

Build systems are tools that automates the process of compilation, linking and execution.
Makefile is one of the build system in C. It automates the compilation of code written in C.

Let's discuss about the example taken in the previous topic using Makefile,
`gcc main.c string_lib.c utils.c math_utils.c -o main`.

### Makefile
```
main: main.o string_lib.o utils.o math_utils.o
    gcc main.o string_lib.o utils.o math_utils.o -o main

main.o: main.c
    gcc main.c -o main.o -c

string_lib.o: src/string_lib.c
    gcc src/string_lib.c -o string_lib.o -c

utils.o: src/utils.c
    gcc src/utils.c -o utils.o -c

math_utils.o: src/math_utils.c
    gcc src/math_utils.c -o math_utils.o -c
```

To understand the code written in this makefile, you must be aware with the syntax of Makefile.
```
target: dependencies
    code to execute
```
Makefiles have 2 most important components, *TARGETS* and *DEPENDENCIES*. Targets have various dependencies and when any of the dependencies change, the code in the target will be executed.

In the above Makefile, there are total 5 targets (main, main.o, string_lib.o, utils.o and math_utils.o).
- Target "main" has 4 dependencies and other targets have 1 dependency. To build main, first you need to build it's dependencies.
- Firstly, `main.o, string_lib.o, utils.o and math_utils.o` targets will run to make object files of their respective dependencies.
- Then, `main` target will run to link all the ".o" files together and produce an executable file.

### How to compile using Makefile?

Here, for compilation you don't need to write that big command instead you can compile by just writing `make main`in your terminal.
You'll see the order something like this.
```
    gcc main.c -o main.o -c
    gcc src/string_lib.c -o string_lib.o -c
    gcc src/utils.c -o utils.o -c
    gcc src/math_utils.c -o math_utils.o -c
    gcc main.o string_lib.o utils.o math_utils.o -o main
```
Let's say if string_lib.c (a dependency) of main.c changes after the last compilation, only the changed target will be executed again. The order of the exxecuted commands will look like this.

```
    gcc main.c -o main.o -c
    gcc src/string_lib.c -o string_lib.o -c
    gcc main.o string_lib.o utils.o math_utils.o -o main
```
You can clearly notice the difference in this way of compilation and the one that we were discussing before.
Here, when a single dependency change, only 3 commands will run to produce an executable file.
Imagine, in the case of that 20 dependencies, only 3 commands will run and not 22 to produce the executable.

You can also create a new target `run` to run the executable file.
```
    run: main
        ./main
```
Now, you can write `make run` to run the code in executable file.
Huh! We've simplified it a lot, but just look at this syntax. Don't you think it looks a little scary?
Don't worry! You don't always have to write Makefiles manually.

## Variables
Just like any language variables in Makefile are used to assign values.
```
    object = 23
```
Here, object is the variable name and 23 is the value assigned in object.
This is how you can write a variable and assign a value to it. Remember that all the variables in Makefile contains only string value. Like in the above assignment, the value of object is "23" and not 23(int).
You can make variables for the repetitive elements in your code and then access them by writing *$(object)*.

```
objects = string_lib.o utils.o math_utils.o
```
Now you can write $(objects) in place of these files in the main target.

### Automatic Variables

Makefile also contains some inbuilt automatic variables to make your makefile even more simpler. Makefile provides some inbuilt variables like `@a, @^ @<`. Each one of these variable will get replaced by speicific values.

- @a - replaced with target
- @^ - replaced with dependencies
- @< - replaces with very first dependency

Let's see an example to understand it more.
```
    main.o: main.c
        gcc main.c -o main.o -c

    main.o: main.c
        gcc @^ -o @< -c
```
Both targets does the same function but the second one is written using automatic variables.

```
    objects = string_lib.o utils.o math_utils.o

    main: main.o $(objects)
        gcc @^ -o @a

    main.o: main.c
        gcc @^ -o @a -c

    string_lib.o: src/string_lib.c
        gcc @^ -o @a -c

    utils.o: src/utils.c
        gcc @^ -o @a -c

    math_utils.o: src/math_utils.c
        gcc @^ -o @a -c
```
You can clearly see the difference between this makefile and the one we've discussed before. Usage of variables at the correct place makes it easy to write as well as to understand.

Now, I want you to look at the makefile written below.
```
    test_string_split: test_string_split.o stringly.o
        gcc @^ -o @a

    test_string_slice: test_string_slice.o stringly.o
        gcc @^ -o @a
```
The above example contains two targets for testing the code of "string_split" and "string_slice".
Did you observe any common thing between these two targets?
Yes! The names of both the targets begins with "test". You can make a single target in place of these two targets and use them to compile both test_string_split and test_string_slice just by replacing "string_split" with "string_slice".

## Pattern matching or Stemming

Makefile has a stemming operator *%*.
```
    test_string_split: test_string_split.o stringly.o
        gcc @^ -o @a

    test_string_slice: test_string_slice.o stringly.o
        gcc @^ -o @a
```
You have seen this example already in the previous part but this makefile can be written in more simplifies version by using matching operator.

```
    test_%: test_%.o stringly.o
        gcc @^ -o @a
```
Here, if you want to compile "test_string_split" then you have to write `make test_string_split` and when you want to compile "test_string_slice" then you have to write `make test_string_slice`.
When you write `make test_string_split`, "%" will be replaced by "string_split".
When you write `make test_string_slice`, "%" will be replaced by "string_slice".

This way, you can write a single target to compile all the files whose name begins with "test".

## Functions

You can always put more structure to your code. There are inbuilt functions in Makefile and I'll use some of them to structurise my Makefile.

```
sources := $(wildcard src/*.c)
objects := $(notdir $(basename $(sources)))
objects := $(foreach x,$(objects),obj/$(x).o)
tests := $(notdir $(basename $(wildcard tests/test_*.c)))

.PHONY: test

test_%: tests/test_%.c $(objects)
	gcc $^ -o $@

obj/%.o: src/%.c
	gcc $^ -o $@ -c

test: $(tests)
	$(foreach x,$(tests),./$(x);)

$(objects):
```
I know this is too much to understand at once, but it's not that difficult.
In the first line you can see a variable with the name "sources", while assigning the value of sources I used a function *wildcard*.
Similarly you can see more functions throughout the code of Makefile. Let's cover them step-by-step.

- *wildcard*: This function searches for a pattern and return all the files that follows the pattern.
Let's say there are 3 files in the "src" folder, "string_lib.c", "utils.c" and "math_utils.c".
When you write $(wildcard src/*.c), it will find all the files with ".c" extension in src folder and return them.

sources will contain 3 files,
`sources := src/string_lib.c src/utils.c src/math_utils.c`

- *basename*: This function removes the extension of any file and returns the basename.
eg:- `$(basename $(sources))` will return `src/string_lib src/utils src/math_utils`. You can see that ".c" extension is removed from these files.

- *notdir*: This function removes the directory of the files and return them.
eg:- `$(notdir $(sources))` will give `string_lib.c utils.c math_utils.c`. "src" is removed from all the files of src folder.

`objects := $(notdir $(basename $(sources)))`
I think now you're able to understand what this statement is doing. This will return all the files in src folder by removing their extension and directory.
`objects := string_lib utils math_utils`

- *addprefix*: This function will add a prefix to the variable.
Now, if you want to change the directory of these files then you can use the following functions.
`(objects := addprefix obj/, $(objects))` this will result in `obj/string_lib obj/utils obj/math_utils`.

- *foreach*: If you want to add something to each file in a variable then you can use foreach function.
Let's say, you want to add ".o" extension in all the files of objects.
`$(foreach x, $(objects), $(x).o`
"foreach" function will add ".o" extension in all the files in "objects" and results in,
`objects := obj/string_lib.o obj/utils.o obj/math_utils.o`


## Moving on
If you're curious about Makefiles and want to learn more about them, you can refer the following resources.
- [https://makefiletutorial.com/]
- [https://www.gnu.org/software/make/manual/make.html]



















