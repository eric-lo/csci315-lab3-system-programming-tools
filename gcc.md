#gcc

`gcc` (GNU compiler Collection) is a open-source compiler system. To compile the C program to **executables**:

```sh
gcc -o hello hello.c
```

It will hide all intermediate steps (pre-process, optimize, linking and etc.) to generate *hello* directly.

To generate *object code*, 

```sh
gcc -c hello.c
```

It will generate `hello.o`.

To show all warnings during compliation, you can use `-Wall` option (`-W` stands for warning).

```sh
gcc -Wall -o hello hello.c
```