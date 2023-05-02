[TITLE + EXAMPLE]: #

# LAB 4

![File](./file.svg)
*main.c*

```c 
#include <stdio.h>
int main() {
   // example program 
   printf("Hello, World!");
   return 0;
}
```

CMD Line Labels:
:----:
| User Input: `$`| 
Compiler Output: `>`
--- 

Task 1: *Describe at least 5 gcc flags*

---
### `-o` *Output File Flag*

   When the `-o` flag is used, the output file’s name is assigned to the specified name preceding it, for example:
   ```
   $ gcc main.c -o myname
   $ ./myname
   > Hello World!
   ```
   If you do not use the -o flag when compiling a c program using GCC, the output file name will default to a.out: 
   ```
   $ gcc main.c
   $ ./a.out
   > Hello World!
   ```
---
### `-E` *Preprocessor Flag*
  
  Before C code can be compiled to assembly code, it needs to be pre-proccessed. The preproccessor is explained [here](https://www.tutorialspoint.com/cprogramming/c_preprocessors.htm)

  The preprocessor flag tells GCC to stop the compilation after the preprocessor, this flag is useful to ensure that the program is correctly processed by the preprocessor. Using the -E flag on a C program will print the preproccessed code to the command line: 
  <pre><code>
  $ gcc -E main.c 
  > <i>{preproccessed stdio.h code}</i>
  > int main() {
  >   printf("Hello, World!");
  >   return 0;
  > }
  </code></pre>
  To save the preproccessed program to a file instead of printing to the command line, you can use the `>` operator followed by the desired filename for the proccessed code... you can then use the `cat` command to display the contents of the saved file... Ex:
  <pre><code>
  $ gcc -E main.c > output
  $ cat ./output
  > <i>{preproccessed stdio.h code}</i>
  > int main() {
  >   printf("Hello, World!");
  >   return 0;
  > }
  </code></pre>
---
### `-Wall` Warning Flag



