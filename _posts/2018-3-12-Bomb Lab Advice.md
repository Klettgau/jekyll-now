---
layout: post
title: Advice for the Bomb Lab!
---
 I had the recent pleasure of tackling The Famous CMU Bomb lab. Throughout the course of frantically googling calling conventions for ATT Assembly,translating assebmly line by line into C and checking registers frequently, I stumbled upon some resources that would have proven useful prior to diving in.

# 1. The Lectures and Recitation from CMU
 All [CMU Lectures] for Introduction to Computer Systems  are online as well as TA Recitations for the eight labs.
 
 [CMU Lectures]:https://scs.hosted.panopto.com/Panopto/Pages/Sessions/List.aspx#folderID=%22b96d90ae-9871-4fae-91e2-b1627b43e25e%22&page=1 
 
 Additionally the course's website contains useful [Student Resources] on the IA32 and x86-64, gdb references and linux.
 
 [Student Resources]:http://csapp.cs.cmu.edu/3e/students.html
 
 The handouts accompanied with the [Bomb Lab] are essential and typically any questions about the lab can be found in the documentation.

[Bomb Lab]:http://csapp.cs.cmu.edu/3e/labs.html

# 2. Setting Up the Lab
If you are performing this lab for school, the lab writeup will vary according to the instructor and instution. You will most likely have to work directly on a school machine or remotely connect to a school account. As for the individuals doing it for the riches and glory, you will require a 64 bit OS. Once the tar is downloaded, extract it and in the folder create two new empty files. One will store  breakpoints that will be useful throughout the entire lab such as the example below.

![alt text][break]

The other file will store the answers you discovered to each phase to avoid always entering the answer.

![alt text][answer]

To use the breakpoint file we just created, enter `source fileName`. This technqiue works for all valid commands and not only setting breakpoints  in gdb. To avoid losing points, it is highly recommended that you set a breakpoint for the function explode_ bomb. 

![alt text][source]

# 3. Disassembling Options and Useful Commands

### 1. Useful Commands
Prior to this lab, I had no experience using gdb as a result the follow tips are based off the pitfalls I encountered and apologize if the following tips are elementary.  The first three shortcuts  I discovered were `i r`  `i b` and `delete breakpoint`(where breakpoint is an integer 1 to n)  for info register ,info breakpoints, and removing breakpoints.
![alt text][ib]

Info register displays all the values held in the registers  in decimal and hexademical.
![alt text][ir]

The [x Command] displays the content of a specified memory address
```
x [Address expression]
x /[Format] [Address expression]
x /[Length][Format] [Address expression]
```
The command is useful to explore regions of mememory or to confirm the data type especially if it's an array or a jump table.
### 2. Disassembling
The two common ways to disassemble the bomb blob is either in gdb or objdump. I preferred objdump to gdb since you can pipe the output to a file and use your preferred text editor. `objdump -d bomb > nameOfOutPut`. Objdump also can print out the symbol table of the binary blob  `objdump -t bomb`. Strings will display all the strings in the blob  `strings bomb`


# 4. CheatSheets
The following sites were a boon when encountering different `jmp` or checking which register is the 2 argument.

[Brown] provides a great writeup and clearly defines the different `jmp`s available or and which value is the Source and Destination.

[Wisc] while slightly dated still provides relevant information about basic operations in assembly and usage of different registers.

[Vgdb] contains many valuable tutorials on gdb and is where I got the [x Command] diagram from.

# Good Luck Hunting

[Vgdb]: http://visualgdb.com/gdbreference/commands/
[Wisc]:https://www.cs.uaf.edu/2005/fall/cs301/support/x86/index.html
[Brown]:https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf
[x Command]:http://visualgdb.com/gdbreference/commands/x "the source of the x command format"
[ir]:https://raw.githubusercontent.com/Klettgau/klettgau.github.io/master/images/ir.png "an example of info register"
[ib]:https://raw.githubusercontent.com/Klettgau/klettgau.github.io/master/images/ib.png "an example of info break and deleting a breakpoint"
[break]:https://github.com/Klettgau/klettgau.github.io/blob/master/images/breakpoints?raw=true "example of breakpoint "
[source]: https://github.com/Klettgau/klettgau.github.io/blob/master/images/source_breakpoints?raw=true "source command in gdb"
[answer]:https://github.com/Klettgau/klettgau.github.io/blob/master/images/answer%20file?raw=true "example of answer file for bomb lab"
