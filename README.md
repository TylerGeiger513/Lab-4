[TITLE + EXAMPLE]: #
*I accidentally titled this lab 4... this is my lab 5 submission*

### Lab 5:   Tyler Geiger
<table>
<tr>
   <td><img width='12' height='12' src='/file.svg'/> <em>main.c</em></td>
   <td>GCC Flags</td>
   <td>GDB Commands</td>
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
   <a href="#-o-output-file-flag">-o</a><br>
   <a href="#-e-preprocessor-flag">-E</a><br>
   <a href="#-i-header-directory-flag">-I</a><br>
   <a href="#-x-language">-x</a><br>
   <a href="#-wall-warning-all-flag">-Wall</a>
</td>
<td>
   <a href="#run">run</a><br>
   <a href="#break">break</a><br>
   <a href="#step">step</a><br>
   <a href="#info">info</a><br>
   <a href="#delete">delete</a><br>
   
</td>
</tr>
</table>

--- 
## GCC FLAGS
--- 
<br><br>
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
   
<br><br>
---
<br><br>
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
<br><br>
---
<br><br>
### `-I` Header Directory Flag

   As explained above in the [-E](#-e-preprocessor-flag) when a c program is preprocessed, the included libraries *`(#include <stdio.h>)`* are concatenated to the program... Since the *stdio.h* library is a default c library, you do not need to provide the compiler with it's directory.
   
   However, if you had intended to use a third party header file, or create your own, they must be in your current directory. If the header file's are located outside of your current directory, the GCC compiler will not know where to look. This is where the `-I` flag is essential.
   
   Assume you are starting a new project, and you plan on using a large amount of custom header files, which you have placed in a directory named `headers`. Your current directory looks something like this:

<table>
   <tr>
      <td>
         ><img width='20' height='20' src='/folder.svg'/>Current-Directory<br>&emsp;&emsp;
         ><img width='20' height='20' src='/folder.svg'/> headers <br>&emsp;&emsp;&emsp;&emsp;
            ><img width='12' height='12' src='/file.svg'/> libcurl.h<br>&emsp;&emsp;&emsp;&emsp;
            ><img width='12' height='12' src='/file.svg'/> SQLite.h<br>&emsp;&emsp;&emsp;&emsp;
            ><img width='12' height='12' src='/file.svg'/> OpenSSL.h<br>&emsp;&emsp;
         ><img width='20' height='20' src='/folder.svg'/> src <br>&emsp;&emsp;&emsp;
            ><img width='12' height='12' src='/file.svg'/> main.c<br>&emsp;&emsp;&emsp;
      </td>
   </tr>
</table>

Assuming you have added the necessary `#include` lines for each header file to the beginning of main.c, simply running ```gcc main.c``` would not compile... Instead you would need to use the `-I` flag to show the compiler what directory the header files are located in. In this example, to compile main.c you would need to run `gcc -I/headers main.c` 

<br><br>
---
<br><br>

### `-x` Language
   
   By default, GCC will attempt to compile files based off of their extension, so `gcc main.c` would compile for the `c` language, while `gcc main.cpp` would compile as a `c++` program.
   
   The `-x` flag in GCC is allows the user to specify the language that gcc will compile the file under. This is useful for when the file extension doesn't match the language of the code in the file.
   
   For example: assume the provided `main.c` has been changed to `main.txt`. If you try to run `gcc main.txt` it would not compile, this is where the `-x` flag is especially useful. To tell the compiler that `main.txt`is a c program you can use the x tag as shown below:
```
$ gcc -x c main.txt -o myFile
$ ./myFile
Hello World!
```
<br><br>
---
<br><br>

### `-Wall` Warning All Flag

The `-Wall` flag is a GCC compiler which instructs the compiler to enable all warnings. This flag is useful for finding issues in your code that you may not have originally noticed. For example, warnings generated by the `-Wall` flag can include: un-used variables, invalid type conversions, uninitialized variables, syntax issues, division by zero, etc...


```c
int main() {
   int a;
   int b = 1;
   return a + b;
}
```
Using the `-Wall` flag on the above program would produce the warning:
```
warning: variable 'a' is uninitialized when used here [-Wuninitialized]
    return a + b;
           ^
```

<br><br>
---
GDB Commands
---
<br><br>
        
### `run`

In GDB the `run` command executes the program from the beginning, this is how you start the debugger. 
Once you have compiled the program using `gcc main.c -o main` and started the debugger using `gdb main` you would use the `run` command to execute the program until it you reach a breakpoint or the end of the program.

<br><br>
--- 
<br><br>

### `break`

The `break` command sets a breakpoint at the specified location... Without any arguments, the `break` command will set a breakpoint for the current line, if you would like to place a breakpoint elsewhere you will need to pass the location and/or condition like: 

`break [location] [condition]`

`[location]` can be specified multiple ways... 
   1. If you would like to set breakpoint at line *5* you would do `break 5` 
   2. If you would like to set a breakpoint when a function begins, you can pass the functions name... such as main: `break main`
   3. If you would like to set a breakpoint at a memory address you can do so like: `break 0x12345678`
  
 `[condition]` is optional, however is useful if you would only like to break if the condition is met. For example, if you would like to break on the fifth iteration of a for loop in main.c you could use: `break [line number of loop] i==5`

<br><br>
--- 
<br><br>

### `step`

The `step` command executes or *steps into* the next line of code in your program... This is useful for tracing your program line by line to identify where or why an issue is occuring. The `step` command can be used repeatedly to slowly execute your code line by line. 

Additionally, you can specify the amount of lines you would like to step forward using the syntax: `step N` with `N` being the number of lines you would like to execute.
        
<br><br>
--- 
<br><br>

### `info`

The `info` command is used to show information about the current debug process. This command has many arguments, most can be found in the docs [here](https://visualgdb.com/gdbreference/commands/#:~:text=information%20displaying%20comands)

Some useful arguments to pass the info command are 
`info breakpoints` - Information about currently set breakpoints
`info locals` - Values of the *local* variables at the current point of execution
`info variables` - Values of the variables at the current point of execution
`info functions` - Information about the programs functions
`info line` - Information about the current line

<br><br>
--- 
<br><br>

### `delete`

The delete command is used to delete breakpoints set in the debugger... 

To get a list of the breakpoints you can use the `info breakpoints` command described above, so you can then use `delete [breakpoint-num]` to delete the breakpoint of choice...


