Download Link: https://assignmentchef.com/product/solved-cs-367project-2-binary-bomb
<br>
<h1>Introduction</h1>

The nefarious Dr. Evil has planted a slew of “binary bombs” on our machines. A binary bomb is a program that consists of a sequence of phases. Each phase expects you to type a particular string on <strong>stdin</strong>. If you type the correct string, then the phase is defused and the bomb proceeds to the next phase. Otherwise, the bomb explodes by printing <strong>“BOOM!!!”</strong> and then terminating. The bomb is defused when every phase has been defused.

<h1>Step 1: Get Your Bomb</h1>

Each student will attempt to defuse their own personalized bomb. Each bomb is a Linux binary executable file that has been compiled from a C program. While each bomb is unique, the phases follow basic patterns. To obtain your bomb, you need to be on a machine that can connect to the machine <strong>zeus-1.vse.gmu.edu  </strong>




Note that <strong>zeus-1</strong> is a machine within the <strong>zeus </strong>server cluster. You can access <strong>zeus-1.vse.gmu.edu </strong>just like you did with<strong> zeus</strong>. Once you are able to connect to <strong>zeus-1.vse.gmu.edu</strong>, point your Web browser to the bomb request daemon at

<u>http://zeus-1.vse.gmu.edu:15225</u>







Fill out the HTML form with your name and GMU email address, and then submit the form by clicking the “Submit” button. The request daemon will build your bomb and return it immediately to your browser in a tar file called <strong>bomb<sub>k</sub>.tar</strong>, where <strong>k</strong> is the unique number of your bomb.  Save the <strong>bombk.tar</strong> file on zeus and unpack it (<strong>tar -xvf bombk.tar</strong>).




This will create a directory called <strong>./bombk</strong> with the following files:

<ul>

 <li><strong>README</strong>: Identifies the bomb and its owner.</li>

 <li><strong>bomb</strong>: The executable binary bomb. This executable will only run on zeus.vse.gmu.edu</li>

 <li><strong>c</strong>: Source file with the bomb’s main routine.</li>

</ul>







When you defuse a phase of the bomb (as described below), the program notifies the instructor. However, each time your bomb explodes on <strong>zeus</strong> it notifies the instructor, and you lose <strong>0.5</strong> points (up to a max of 10 points) in the final score for the lab. So there are consequences to exploding the bomb. You must be careful!

Also, if you make any kind of mistake requesting a bomb (such as neglecting to save it), simply request another bomb. We see who checks out every single bomb, so let us know your old bomb and new bomb.

<h1>Step 2: Defuse Your Bomb</h1>

Your job is to defuse the bomb. You can use many tools to help you with this; please look at the hints section for some tips and ideas. The best way is to use your favorite debugger (<strong>gdb</strong>) to step through the disassembled binary.

Each of the first four phases is worth 10 points, for a total of 40 points. The 5th and 6th phases are more difficult and are worth 15 points. Defusing all six phases gives you 70 points. The phases get progressively harder to defuse, but the expertise you gain as you move from phase to phase should offset this difficulty. However, the last phase will challenge even the best students, so please don’t wait until the last minute to start!




The bomb ignores blank input lines. If you run your bomb with a command line argument, for example,




<strong>                  linux&gt; ./bomb psol.txt </strong>

<strong> </strong>

then it will read the input lines from <strong>psol.txt</strong> until it reaches <strong>EOF</strong> (end of file), and then switch over to <strong>stdin</strong>. We added this feature so you don’t have to keep retyping the solutions to phases you have already defused.




To avoid accidentally detonating the bomb, you will need to learn how to use <strong>gdb</strong> to single-step through the assembly code and how to set breakpoints. You will also need to learn how to inspect both the registers and the memory states. One of the nice side-effects of doing the lab is that you will get very good at using a debugger. This is a crucial skill that will pay big dividends the rest of your career.

<strong> </strong>

<strong> </strong>

<h1>Hand-In</h1>




There is no explicit hand-in. The bomb will notify your instructor automatically after you have successfully defused it on <strong>zeus-1.vse.gmu.edu</strong>. You can keep track of how you (and other students) are doing by looking at

<u>http://zeus-1.vse.gmu.edu:15225/scoreboard</u>




This web page is updated continuously to show the progress of the class.

Note that this web page is only accessible from a machine in the VSE labs or if you have connected to the VSE labs using a VPN.

<strong> </strong>

<strong> </strong>

<h1>Hints (Please read this!)</h1>




There are many ways of defusing your bomb. You can examine it in great detail without ever running the program, and figure out exactly what it does. This is a useful technique, but it is not always easy to do. You can also run it under a debugger, watch what it does step by step, and use this information to defuse it. This is probably the fastest way of defusing it. You may not modify your bomb in any way to defuse it; your inputs are attempted on a fresh copy of your bomb for grading purposes so you can’t circumvent it this way.

We make one request; please do not use brute force! You could write a program that will try every possible key to find the right one. But this is no good because we haven’t told you how long the strings are, nor have we told you what characters are in them. Even if you made the (wrong) assumptions that they all are less than 80 characters long and only contain letters, then you will have 2680 guesses for each phase. This will take a long time to run, and you will not get the answer before the assignment is due.

There are many tools which are designed to help you figure out both how programs work, and what is wrong when they don’t work. Here is a list of some of the tools you may find useful in analyzing your bomb, and hints on how to use them.




<strong>       </strong>

<ul>

 <li><strong>gdb</strong> The GNU debugger is a command line debugger tool available on virtually every platform. You can trace through a program line by line, examine memory and registers, look at both the source code and assembly code (we are not giving you the source code for most of your bomb), set breakpoints, set memory watch points, and write scripts. Here are some tips for using gdb. To keep the bomb from blowing up every time you type in a wrong input, you’ll want to learn how to set breakpoints.

  <ul>

   <li>The CS:APP Student Site at <u>http://csapp.cs.cmu.edu/public/students.html</u> has a very handy singlepage gdb summary.</li>

   <li>For other documentation, type <strong>help</strong> at the gdb command prompt, or type <strong>man gdb</strong>, or <strong>info gdb</strong> at a Unix prompt. Some people also like to run gdb under <strong>gdb-mode</strong> in emacs.</li>

  </ul></li>

</ul>




<ul>

 <li><strong>objdump -t</strong> This will print out the bomb’s symbol table. The symbol table includes the names of all functions and global variables in the bomb, the names of all the functions the bomb calls, and their addresses. You may learn something by looking at the function names!</li>

</ul>




<ul>

 <li><strong>objdump –d </strong>Use this to disassemble all of the code in the bomb. You can also just look at individual functions. Reading the assembler code can tell you how the bomb works. Although <strong>objdump</strong> <strong>-d</strong> gives you a lot of information, it doesn’t tell you the whole story. Calls to system-level functions are displayed in a cryptic form. For example, a call to <strong>sscanf</strong> might appear as: <strong>8048c36: e8 99 fc ff ff call 80488d4 &lt;_init+0x1a0&gt;</strong> To determine that the call was to <strong>sscanf</strong>, you would need to disassemble within <strong>gdb</strong>.</li>

 <li><strong>strings</strong> This utility will display the printable strings in your bomb.</li>

</ul>




Looking for a particular tool? How about documentation? Don’t forget, the command <strong>man</strong> is your friend. You can use this to look up information on system functions that the binary executable might use.  In particular, <strong>man ascii</strong> might come in useful.

<strong> </strong>

<h1>Advice</h1>

Based on my experience defusing bombs, I have the following advice:

<ul>

 <li>I print out all of the code associated with a particular phase when I start to diffuse it. As I work, I annotate this code with information as I figure out what is going on.</li>

 <li>As you will notice from examining <strong>c</strong>, the user input is sent into the phase as a single string. One of the first things the phase will do is try to ‘parse’ it into the form it is expecting.</li>

 <li>When you are trying to figure out what values are needed for a phase (particularly if the values are integers), try ‘interesting’ numbers like <strong>42</strong>, <strong>-17</strong>, … first. The reason for this is that if you see one of these numbers appear in a register or in a memory location, chances are pretty good that was your input.</li>

 <li>Don’t bother trying to step through system functions. This is generally a waste of time. If you don’t know what the function does, use <strong>man</strong> to investigate the parameters and return information. Then examine the parameters that are sent and the return value.</li>

 <li>If you end up inside a function that you don’t want to step through, the <strong>gdb</strong> command <strong>finish</strong> will take you to the end.</li>

 <li>The bomb functions typically have a generic name like <strong>fn7</strong> or <strong>phase2</strong>. It has been my experience that if a function has a descriptive name, you can assume that the function behaves as expected and that they are NOT trying to trick you.</li>

 <li>Understanding parameter passing is critical to this assignment. Whenever you see a reference to <strong>%esp</strong> in the lines before a call, this involves placing a parameter on the stack. It is never a bad idea to figure out what the value of the parameter is. In the called procedure, references to <strong>%ebp</strong> involve use of the parameters in the code.</li>

 <li>It may not be important to understand exactly what every statement is doing – the goal is to avoid the <strong>explode_bomb</strong> I tend to step through the code until just before one of these calls and then focus on what conditions are not being met. You can also set a breakpoint at <strong>explode_bomb</strong> to ensure you don’t accidently execute it.</li>

</ul>


