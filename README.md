"# Static-Library" 

Steps to create a static library Let us create and use a Static Library in UNIX or UNIX like OS.
1. Create a C file that contains functions in your library.


/* Filename: lib_mylib.c */
#include <stdio.h>
void fun(void)
{
  printf("fun() called from a static library");
}
We have created only one file for simplicity. We can also create multiple files in a library.

2. Create a header file for the library


/* Filename: lib_mylib.h */
void fun(void);
3. Compile library files.

 gcc -c lib_mylib.c -o lib_mylib.o 
4. Create static library. This step is to bundle multiple object files in one static library (see ar for details). The output of this step is static library.

 ar rcs lib_mylib.a lib_mylib.o 
5. Now our static library is ready to use. At this point we could just copy lib_mylib.a somewhere else to use it. For demo purposes, let us keep the library in the current directory.

Let us create a driver program that uses above created static library.
1. Create a C file with main function


/* filename: driver.c  */
#include "lib_mylib.h"
void main() 
{
  fun();
}

2. Compile the driver program.

gcc -c driver.c -o driver.o

3. Link the compiled driver program to the static library. Note that -L. is used to tell that the static library is in current folder (See this for details of -L and -l options).

gcc -o driver driver.o -L. -l_mylib
4. Run the driver program

./driver 
fun() called from a static library
