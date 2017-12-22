
# Executable and Linkable Format（ELF）

Before introducing the _**readelf**_ and _**objdump**_, we need have an overview about Executable and Linkable Format(ELF).
>In computing, the Executable and Linkable Format (ELF, formerly named Extensible Linking Format), is a common standard file format for executable files, object code, shared libraries, and core dumps. First published in the specification for the application binary interface (ABI) of the Unix operating system version named System V Release 4 (SVR4), and later in the Tool Interface Standard, it was quickly accepted among different vendors of Unix systems. In 1999, it was chosen as the standard binary file format for Unix and Unix-like systems on x86 processors by the 86open project.

ELF files in Linux can be classified into three kinds roughly:

- Relocatable file, such as file with .o extension.
- Shared object file, such as file with .so extension.
- Executable file, such as a.out

Each ELF file is made up of one ELF header, followed by file data. The file data can include:

- Program header table, describing zero or more memory segments
- Section header table, describing zero or more sections
- Data referred to by entries in the program header table or section header table

And _**objdump**_ or _**readelf**_ can help us to read ELF header and file data in a human-friendly way.