[TITLE + EXAMPLE]: #
### Lab 4:   Tyler Geiger

<table>
<tr>
   <td><img width='12' height='12' src='/file.svg'/> <em>main.c</em></td>
   <td>GCC Flags</td>
</tr>
<tr>
<td>

```c
#include <stdio.h>
int main() {
   // example program 
   printf("Hello, World!");
   return 0;
}
```

</td>
<td>
   <a href="#-o-output-file-flag">-o (output file)</a><br>
   <a href="#-e-preprocessor-flag">-E (preprocessor)</a><br>
   <a href="#-x-language">-x (language)</a><br>
   <a href="#-E-Preprocessor-Flag">-E</a><br>
   <a href="#-E-Preprocessor-Flag">-E</a>
</td>
</tr>
</table>

---
### `-o` *Output File Flag*
   
   The `-o` flag is a GCC option the specifies the output file's name with the string preceding it. This is useful if you need the output file saved under a desired name, to do so you would need to use the `-o` flag, followed by a whitespace ` `, and then the name of the desired output. 
   
   For example:
   <table>
      <tr>
         <th>Input:</th>
         <td>
            <code>$ gcc main.c -o myname</code><br>
            <code>$ ./myname</code>
         </td>
      </tr>
      <tr>
         <th>Output:</th>
         <td>
            <code>Hello World!</code>
         </td>
      </tr>
   </table>

            
</td></tr></table>
      If you do not use the -o flag when compiling a c program using GCC, the output file name will default to a.out: 
   <table>
      <tr>
         <th>Input:</th>
         <td>
            <code>$ gcc main.c</code><br>
            <code>$ ./a.out</code>
         </td>
      </tr>
      <tr>
         <th>Output:</th>
         <td>
            <code>Hello World!</code>
         </td>
      </tr>
   </table>
   
---
### `-E` *Preprocessor Flag*
  
  Before C code can be compiled to assembly code, it needs to be pre-proccessed. The preproccessor is explained [here](https://www.tutorialspoint.com/cprogramming/c_preprocessors.htm)

  The preprocessor flag tells GCC to stop the compilation after the preprocessor, this flag is useful to ensure that the program is correctly processed by the preprocessor. Using the -E flag on a C program will print the preproccessed code to the command line: 
  ```
  $ gcc -E main.c 
  ```
  ```
  [preproccessed stdio.h code]
  
  int main() {
     printf("Hello, World!");
      return 0;
  }
  ```
  As you can see, using the -E flag stopped the compilation at the preprocessor, which removed all comments from main.c. If you were to try this example in a real compiler, the `[preproccessed stdio.h code]` would be replaced with the code from the stdio.h library found [here](https://www.gnu.org/software/m68hc11/examples/stdio_8h-source.html)

  To save the preproccessed program to a file instead of printing to the command line, you can use the `>` operator followed by the desired filename for the proccessed code... you can then use the `cat` command to display the contents of the saved file... Ex:
  ```
  $ gcc -E main.c > output
  $ cat ./output
  ```
  ```
  [preproccessed stdio.h code]
  
  int main() {
    printf("Hello, World!");
    return 0;
  }
  ```
---
### `-x` Language
   
   By default, GCC will attempt to compile files based off of their extension, so `gcc main.c` would compile for the `c` language, while `gcc main.cpp` would compile as a `c++` program.
   
   The `-x` flag in GCC is allows the user to specify the language that gcc will compile the file under. This is useful for when the file extension doesn't match the language of the code in the file.
   
   For example: assume the provided `main.c` has been changed to `main.txt`. If you try to run `gcc main.txt` it would not compile, this is where the `-x` flag is especially useful. To tell the compiler that `main.txt`is a c program you can use the x tag as shown below:
```
$ gcc -x c main.txt -o myFile
$ ./myFile
Hello World!
```

   




