java cProject 2: Minimal Basic (or QBasic)
Please compress your source code using 7z and upload the 7z file to oc.sjtu.edu.cn before the final deadline.
 
In 1975, Bill Gates and Paul Allen started the company that would become Microsoft by writing a BASIC interpreter for the first microcomputer, the Altair 8800 developed by the MITS corporation of Albuquerque, New Mexico. By making it possible for users to write programs for a microcomputer without having to code in machine language, the Altair and its implementation of BASIC helped to start the personal computer revolution.
In this project, your mission is to build a minimal BASIC interpreter. You need to accomplish the following objectives:
➢ To increase your familiarity with expression trees and class inheritance. 
➢ To give you a better sense of how programming languages work. Learning how an interpreter operates—particularly one that you build yourself—provides useful insights into the programming process. 
➢ To offer you the chance to adapt an existing program into one that solves a different but related task. The majority of programming that people do in the industry consists of modifying existing systems rather than creating them from scratch. 
What is BASIC? 
The programming language BASIC—the name is an acronym for Beginner’s All-purpose Symbolic Instruction Code—was developed in the mid-1960s at Dartmouth College by John Kemeny and Thomas Kurtz. It was one of the first languages designed to be easy to use and learn. Although BASIC has now pretty much disappeared as a teaching language, its ideas live on in Microsoft’s Visual Basic system, which remains in widespread use. 
In BASIC, a program consists of a sequence of numbered statements, as illustrated by the simple program below: 
10 REM Program to add two numbers
20 INPUT n1
30 INPUT n2
40 LET total = n1 + n2
50 PRINT total
60 END
The line numbers at the beginning of the line establish the sequence of operations in a program. In the absence of any control statements to the contrary, the statements in a program are executed in ascending numerical order starting at the lowest number. Here, for example, program execution begins at line 10, which is simply a comment (the keyword REM is short for REMARK) indicating that the purpose of the program is to add two numbers. Lines 20 and 30 request two values from the user, which are stored in the variables n1 and n2, respectively. The LET statement in line 40 is an example of an assignment in BASIC and sets the variable total to be the sum of n1 and n2. Line 50 displays the value of total on the console, and line 60 indicates the end of execution. A sample run of the program therefore looks like this:

Figure 1
Line numbers are also used to provide a simple editing mechanism. Statements need not be entered in order, because the line numbers indicate their relative position. Moreover, as long as the user has left gaps in the number sequence, new statements can be added in between other statements. For example, to change the program that adds two numbers into one that adds three numbers, you would need to make the following changes: 
1. Add a new line to read in the third value by typing in the command
35 INPUT n3
2. This statement is inserted into the program between line 30 and line 40. Replace the old line 40 with an update version by typing
40 LET total = n1 + n2 + n3
 
In classical implementations of BASIC, the standard mechanism for deleting lines was to type in a line number with nothing after it on the line. Note that this operation actually deleted the line and did not simply replace it with a blank line that would appear in program listings. 
Expressions in BASIC 
The LET statement illustrated by line 40 of the addition program has the general form
LET variable = expression 
and has the effect of assigning the result of the expression to the variable. In Minimal BASIC, the assignment operator is no longer part of the expression structure. The simplest expressions are variables and integer constants. These may be combined into larger expressions by enclosing an expression in parentheses or by joining two expressions with the operators +, -, *, /, and MOD. You only need to support +,-, *, /, MOD, (, ) operators with signed integers (at least 32-bit) in expressions. (Be aware of negative integers.)
The MOD operator has the same precedence as * and /. In the expression LET r = a MOD b, the absolute value of rshould be less than the absolute value of b, and the sign of ris the same as that of b. For example, 5 MOD 3 is 2 and 5 MOD (-3) is -1.
Additionally, you need to support the exponentiation operator in expressions:
exp1 ** exp2
The exponentiation operator returns the result of exp1exp2, where exp1 and exp2 are expressions. The exponentiation operator is right associative, i.e., a ** b ** c is equal to a ** (b ** c). The operator has higher precedence than *, / and MOD.
 
For all expressions and statements, you need to handle extra spaces. For example, LET a   = b + 4 *   (-5 + 4 ).
 
Control statements in BASIC 
The statements in the addition program illustrate how to use BASIC for simple, sequential programs. If you want to express loops or conditional execution in a BASIC program, you have to use the GOTO and IF statements. The statement 
GOTO n 
transfers control unconditionally to line n in the program. If line n does not exist, your BASIC interpreter should generate an error message informing the user of that fact. 
The statement 
IF condition THEN n 
performs a conditional transfer of control. On encountering such a statement, the BASIC interpreter begins by evaluating condition, which in the minimal version of BASIC consists of two arithmetic expressions joined by one of the operators , or =. If the result of the comparison is true, control passes to line n, just as in the GOTO statement; if not, the program continues with the next line in sequence. 
For example, the following BASIC program simulates a countdown from 10 to 0: 
10 REM Program to simulate a countdown
20 LET T = 10
30 IF T . If the condition holds, the program should continue from line n just as in the GOTO statement. If not, the program continues on to the next line.
Note that the conditional operators (=, ) are not parts of expressions.
 
END	Marks the end of the program. Execution halts when this line is reached. This statement is usually optional in BASIC programs because execution also stops if the program continues past the last numbered line. 
 

Table 2. Commands to control the BASIC interpreter
RUN	This command starts program execution beginning at the lowest-numbered line. Unless the flow is changed by GOTO and IF commands, statements are executed in line-number order. Execution ends when the program hits the END statement or continues past the last statement in the program. 
 
LOAD	This command loads a file containing statements and commands. Statements and commands should be stored (also displayed in GUI) and executed respectively, as if they were entered into input box in order. A prompt window should be displayed when this command is entered. The window asks users to choose the file to load.
 
LIST	This command lists the steps in the program in numerical sequence. It has been required to be implemented in the previous version of this project. In the new version, your interpreter should be able to display all the codes that have been entered in real time, so there is no need to implement this command.
 
CLEAR	This command deletes the program so the user can start entering a new one.
 
HELP	This command provides a simple help message describing your interpreter.
 
QUIT	Typing QUIT exits from the BASIC interpreter.
 
 
Example of use
Figure 2 shows a complete session with the BASIC interpreter. The program is intended to display the terms in the Fibonacci series less than or equal to 10000. The three output windows are used to the current program, the standard output (and errors) of program代 写program 、 C++
代做程序编程语言, and the syntax tree of each line of statements. User can enter statements or commands into command input box, or load a file to be executed through LOAD button. The syntax tree is displayed only when RUN is called. CLEAR will clears the content of all three windows. The RUN and CLEAR buttons are used to execute and clear statements entered respectively. The DEBUG button is used to enter debug mode, which will discussed later.
 
Figure 2
Syntax tree display
Conceptually, syntax tree is one abstract representation of program.  More specifically, every statement in the program can be represented as a tree.  The structure of the syntax tree can be seen as the steps of the computation of the expressionin the statement. 
As you have learnt from previous programming course, some statements have side effects, in our mini basic language, the side effects include assignment and branch. And these side effects should also be displayed in the syntax tree. 
The node of the tree can be identifier definition, assignment, function call (You need not to implement function call in this project), expression computation and conditional or unconditional branch.  In your interpreter implementation, you can make the computation along the syntax tree from leaf node to root. Because the connection structures of the tree are determined by the computation rules, e.g. operator priority and association.
In your implementation, you should construct the syntax tree in infix notation.  
For displaying the syntax tree structure in your GUI window easily, you don’t need to plot the real tree. Instead, you should use indentation to display the syntax tree of each statement.
 
Followings are some concrete examples. Structure in the red border is expression of that statement. 
 
1. LET m = p + q*t
The syntax tree of this statement:
 

 	LET =
   m
   +
       p
       *
           q
           t
 
Figure 3
 
2. IF m > max THEN n 
The syntax tree of this statement:
 


 	IF THEN
   m
   >
   max
   n
Figure 4
3. GOTO n
The syntax tree of this statement:
	GOTOn
Figure 5
 
4. PRINT p + q*t
The syntax tree of this statement:

 	PRINT
   +
       p
       *
           q
           t
Figure 6
As what you can observe, the nodes at the same level in the tree are at the same vertical line in the indentation notation.
Each indent contains 4 spaces to make the structure of the syntax tree clear enough. 
Debugger
A debugger is an essential tool for programmers. We need to implement a debugger in our BASIC interpreter with specific functionalities. The debugger should only run when debug mode is activated, so you need to design a DEBUG button that starts this mode.

Figure 7
Upon pressing the DEBUG button, the program layout will change as depicted in Figure 7. Users can manage breakpoints by adding or deleting line numbers. If an invalid line number is entered, the program should alert the user and ignore the input. Use new command formats for these actions, such as:
ADD 120
 
DELETE 110
Remember to keep the break point list up to date. Here is a possible format for it.
120130
The user can press the RUN button to start the program. The program should execute and pause when it reaches any of the specified breakpoints. Upon stopping, the debugger window should display the values of all available variables, allowing the user to inspect the program's state. A possible display format is as follows.
Max = 10000n1 = 0
While the program is paused, the user can add new breakpoints or delete existing ones. 
Pressing the RESUME button will continue the program execution from where it left off. Additionally, there should be an EXIT button that lets the user stop the program and exit debug mode at any time.
Note that code edits should be disabled in debug mode. You don’t have to persist the state of debug mode.
Storing the program 
The first task you need to undertake is making it so your BASIC interpreter can store programs. Whenever you type in a line that begins with a line number, such as 
100 REM Program to print the Fibonacci sequence 
your interpreter has to store that line in its internal data structure so that it becomes part of the current program. As you type the rest of the lines from the program in Figure 2, the data structure inside your implementation must add the new lines and keep track of the sequence. In particular, when you correct the program by typing 
145 PRINT n1 
your data structure must know that this line goes between lines 140 and 150 in the existing program. 
Hints on the statement class hierarchy 
The primary class for expressions should be Expression, which is the abstract superclass for a hierarchy that includes three concrete subclasses for the three different expression types, as follows: 

The structure of the statements is quite similar. The primary class should be Statement, which is the abstract superclass for a set of subclasses corresponding to each of the statement types, as illustrated in the following diagram: 
Even though there are more subclasses in the Statement hierarchy, it is still somewhat easier to implement than the Expression hierarchy. One of the things that makes the Expression hierarchy complex—but also powerful—is that it is recursive. Compound expressions contain other expressions, which makes it possible to create expression trees of arbitrary complexity. Although statements in modern languages like C++ are recursive, statements in BASIC are not. 
Exception handling 
Crashing the whole interpreter because your BASIC program has a syntax error would be incredibly frustrating, since you would lose everything you’d typed in up to that point. Thus, you need to use try/catch so that your interpreter responds to errors much more gracefully. 
Strategy and tactics 
As you work through this project, you might want to keep in mind the following bits of advice: 
• The last line of the fictional memo from Bill Gates encourages his team to “get going on this project as soon as possible.” I encourage you to adopt that same strategy.
• You need to first create a project and initialize the GUI. You can use the UI editor of Qt Creator or place the UI widgets by C++ code. To finish the Minimal BASIC project, you need to proceed strategically by making carefully staged edits. To whatever extent you can, you should make sure that the BASIC project continues to run at the completion of each stage in the implementation.
• Make sure you get the project working before you embark on extensions. It’s easy to get too ambitious at the beginning and end up with a mass of code that proves impossible to debug.
Grading
• (10’) Your interpreter should be able to present a GUI and interact with user input.
o GUI should contain the input and output interfaces shown in Figure 2. 
• (20’) Your interpreter should be able to load and edit basic programs.
o Users can add, update or delete statements through input box or LOAD button.
o The statements entered by user can be stored and displayed in the correct order.
• (50’) Your interpreter should be able to interpret basic programs correctly.
o Expression parsing (display the syntax tree, although this should be done when you store the programs);
o Expression evaluation and statement execution (display the result of print if exists);
o Runtime context maintenance (e.g., the current line to be executed, all variables and their values).
o Debug mode (break points, display program variables)
• (10’) Your interpreter should be robust and correctly handle errors in the input.
• (10’) You should finish the project with object-oriented design and implementation; your code should be clear and easy to read with appropriate comments.
 
Hints:
You could learn something from this article. But there are always other ways to achieve the same goal, and you are not restricted by the article.
 
         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
