# Assembler and Linker

The assembler turns the assembly code (human readable machine code) to generate object code (machine code).

For example, `hello.s` is assembled and `hello.o` is generated. 

```sh
as hello.s -o hello.o

```


However, at the stage, `hello.o` may not be *directly* executable.
Usually most programs have to rely on other library codes.


## Linker

The linker puts together all object files as well as the libraries as an executable. Libraries are only a bunch of function implementation (e.g. Math `pow()`).

![](/assets/libraries.png)

There are two kinds of libraries:

- Static library (static linked during compilation, included as part of your executable)

![](/assets/static.png)

- Shared library (dynamically linked, call at run-time)
![](/assets/dynamic.png)

For the dynamic linking, the linker only verifies if the symbols (functions and variables) that are needed by the program are completely satisfied. When the program runs, the OS will dynamically link the ".so" files.

e.g. 

```c
// math.c

int main(int argc,char *argv[])
{
    float v = 3.14;
    printf("sin(3.14) is %f\n",v);
    return 0;
}
```
When you try to compile in a normal way:

```sh
gcc math.c
```

It will show your the error:

![](/assets/math_error.png)

As the linker cannot find the math libaray: `libm.so.6`

To link it, you have to provide `-lm` option to `gcc`.
```sh
gcc math.c -lm
```

Then it can be run.

To show which libraries are dynamically linked, you can use `ldd`.

```sh
ldd a.out
```
![](/assets/math_ldd.png)


