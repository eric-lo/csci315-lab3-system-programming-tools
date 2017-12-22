# Makefile Structure 

It is just a plain text file named "Makefile" under a folder.

Bascially the structure is as follows:

```
target: dependencies
[tab] system command
```

For example, to compile all files,

```makefile
all: 
    gcc -o main main.c add_int.c multi_int.c
```
Then you can type `make` in the terminal and `main` executable will be produced.

```shell
make
```

You can see calling `make` will invoke the target "all". `make` will run the first target as **default**.

---
 
## Dependencies

By spliting the targets, modifying a single file will not recompile everything in the project. What you need to do is to specify the dependencies:

```makefile

all: main

main: add_int.o multi_int.o main.o
    gcc add_int.o multi_int.o main.o -o main
    
add_int.o: add_int.c
    gcc -c add_int.c

multi_int.o: multi_int.c
    gcc -c multi_int.c

main.o: main.c
    gcc -c main.c
    
clean:
    rm *.o main

```

Now you can see that the target `all` contains only a dependency. In order to fulfill the target `all`, it will go through the another dependency `main` and so on and finally all dependencies are fulfilled and compilation can take place.

The last target `clean` is a target to call `rm` to delete all compiled file.

---

## PHONY Target

In the last example you can see a new target `clean`. Actually it is not a file target, instead it is a name that user wants to execute a particular command, like `rm`.

However, in rare case if the directory has a file called `clean`, `make` will be confused. As the file called `clean` exists, the target dependency is fulfilled and nothing will be run.

```
make: 'clean' is up to date.
```

In order to tell `make` clean is not a file target, you can explicitly declare the target to be "phony"

```makefile
.PHONY: clean
all: main

main: add_int.o multi_int.o main.o
    gcc add_int.o multi_int.o main.o -o main
    
add_int.o: add_int.c
    gcc -c add_int.c

multi_int.o: multi_int.c
    gcc -c multi_int.c

main.o: main.c
    gcc -c main.c
    
clean:
    rm *.o main


```

You can try, now `make clean` can be run successfully even if the file `clean` is here.

---
## Variables

You can use variables in the Makefile to save time and get rid of repeated statements.

```makefile
CC=gcc
CFLAGS=-Wall -c

all: main

main: add_int.o multi_int.o main.o
    $(CC) add_int.o multi_int.o main.o -o main
    
add_int.o: add_int.c
   $(CC) $(CFLAGS) add_int.c

multi_int.o: multi_int.c
    $(CC) $(CFLAGS) multi_int.c

main.o: main.c
    $(CC) $(CFLAGS) main.c
    
clean:
    rm *.o main

```

In this case, we can specify the options for the compiler more easily.

---

## Implicit Rule

In some cases, you can omit the command elements in the Makefile, and the `make` can automagically do the action for you.

```makefile

CC=gcc
CFLAGS=-Wall

EXE=main
OBJ=add_int.o multi_int.o main.o

all: $(EXE)

main: $(OBJ)

clean:
        rm -f $(OBJ) $(EXE)

```

In the target `main`, you can see only dependencies are declared. However, `make` can do all the compilation jobs. It is because there are **implicit rules**.

From the manual, it states:

> n.o is made automatically from n.c with a recipe of the form ‘$(CC) $(CPPFLAGS) $(CFLAGS) -c’.

Therefore, `add_int.o` is made by using the above-mentioned rule automatically.

----
The brief introduction of Makefile stops here. Of course there are even more advanced features, please always refer to the [Make documentation](https://www.gnu.org/software/make/manual/make.html) for more information.