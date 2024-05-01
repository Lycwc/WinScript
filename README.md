<HTML>
<HEAD>
<TITLE> Util Usage </TITLE>
<STYLE>
</STYLE>

<LINK href=".\regex.css" type=text/css rel=StyleSheet>
<LINK href=".\mycss.css" type=text/css rel=StyleSheet>
</HEAD>

<H2>Script File</H2>

<P>Script provides many powerful functions that may be used in many applications.  The following sections describes the script file format and the command usages.</P>

<H2>Script page</H2>
<OL>
<LI><B>Dropdown list</B>: The dropdown list provides all commands as a help. It lists what commands is provided and its format. When a command is selected, the command is copied to clipboard so that it can be pasted into a text file for further editing.</LI>
<LI><B>...</B>: Selects a script file for execution.  The file name is placed in the File name box.</LI>
<LI><B>Veiw file</B>: Opens the file in File name box with Notepad for editing.</LI>
<LI><B>Bull's eye button</B>: Drag this button to a location to get a window's information.  While the button is dragging, the current cursor position is put in Box 1, the handle of a window is put in Box 2.  The difference between current cursor position and the cursor stop position from last drag, the difference between current cursor position and the window's top left corner from last drag are placed in Box 4 separated by parenthesis, the current window's position is put in Box5.  Therefore, the first set of value in Box 4 can be used to find the relative position of two points and the second set of values in Box 4 can be used to find the relative position of a point inside a window to its top-left corner.</LI>
<LI><B>File name box</B>: It is used for entering a script file name for execution.</LI>
<LI><B>Box on the left</B>: It can be used to enter a number to repeatedly execute a script file.</LI>
<LI><B>Execute line</B>: Interprets and executes a command entered in File name box.  This function can be used to debug a command.  Multiple commands can be entered in the File name box.</LI>
<LI><B>ExecClipboard</B>: Execute the command copied into the clipboard.  For example, the examples in this usage manual can be copied into the clipboard, and then click this button to be executed.</LI>
<LI><B>Execute</B>: Interprets and executes the script file in the File name box.</LI>
<LI><B>Pause</B>: Toggle the pause state.  If script is running, clicking the button will pause its execution.  Clicking it again will resume the execution.</LI>
<LI><B>Step</B>: If the execution is in pause state, clicking this button will execute one command.</LI>
<LI><B>Cancel</B>: Cancels the execution of a script file.</LI>
<LI><B>Box 1-5</B>: These boxes can be used to communicate with script file by some commands.  They also have the function stated above as bull's eye is dragged around.</LI>
<LI><B>Display</B>: It can be used by script command to display information.  When executing a line, it displays the result of the last command.</LI>
<LI><B>Status</B>:  Displays the execution status.</LI>
</OL>

<H2>A quick tutorial</H2>
<OL>
<LI>Copy UtilProg.exe to directory C:\utils</LI>
<LI>Create scipt file <B>hellow_world.txt</B> in directory C:\script with the following contents:<BR>
&nbsp;&nbsp;&nbsp;&nbsp;SetStrVal("Hellow World", str);&nbsp;&nbsp;// Assign "Hellow World" to str<BR>
&nbsp;&nbsp;&nbsp;&nbsp;SetStrToBox(str, 4);&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// Display str in box 4
</LI>
<LI>Use File Explorer to directory C:\utils.<BR>
Double click UtilPorg.exe to start the program.<BR>
Click the DownArrow to select "<B>Script file</B>"</LI>
</LI>
<LI>Copy the following line into clipboard:<BR>
&nbsp;&nbsp;&nbsp;&nbsp;WriteIniStr("UtilProg", "script_path", "C:\scripts\");<BR>
Then click ExecClipboard.  This let UtilProg know where the scripts are located.</LI>
<LI>Close and restart the program.  This lets the abvoe step take effect.</LI>
<LI>Go to the UtilProg, click on the botton with <B>...</B> (three dots).  A dialog pops up showing the files in C:\scripts directory.  Select file <B>hellow_world.txt</B> just created, then click the <B>Ok</B> button.</LI>
<LI>Click the <B>Execute</B> button.  "Hellow world" will be shown in box 4.</LI>
<LI>Click View File button to open the file.  Make modification and execute.</LI>
</OL>

<H2>Script file format</H2>

<OL>
<LI>Scripts are generally stored in a file.  This file must be a text file but it can be an unicode text file.</LI>  
<LI>Each line in the text file can contain more than one script commands. </LI> 
<LI>A variable in the command can be any character.  For example, 2#st is a variable.  But it is better to use a descriptive variable name.</LI>
<LI>For variable, the case is insensitive.  For example, Var and var are the same variables.</LI>
<LI>It is not necessary to define a variable.  A variable is defined when it is used for the first time.</LI>
<LI>There are four types of variables: 
<UL>
<LI>string variable: Stores a string.</LI>
<LI>string stack variable: Stores an array of strings</LI>
<LI>integer variable: Stores integer.</LI>
<LI>integer stack varible: Stores an array of integers</LI>
</UL>
There is not floating variable.  Floating variable can be stored in string variable, and operated by special commands.
</LI>
<LI>When a string variable, string stack variable, or an integer stack varible is used, its value is automatically initialized with the name of the variable if it is not initialized by the program.  An integer variable is initialized with 0 if it is not initialized in the program.</LI>
<LI>It is suggested that same variable name not be used for different types of variables.  For example, if x is used as the name of a string variable, it should not be used as the name of an integer variable, nor a string stack variable, nor a integer stack variable.  Otherwise, it can get confused easily.</LI>
<LI>A command is also case-insensitive.  But it is suggested to use a capital letter for the first character of words in the command for reading clarity.  For example EndProgram() is better than endprogram().</LI>
<LI>Anything after double slashes is treated as a comment and ignored.</LI>
<LI>Anything between /* and */ is also comments and ignored.  The only requirement for /* and */ is that they must be on a seperate line and at the beginning of a line.</LI>
<LI>A constant string should be contained in two double quotes.  When the interpreter see a starting double quote, it looks for a combination of double quote and a comma (<B>",</B>) following the starting double quote as the end of the constant string.  Therefore, a double quote inside a double quote is valid.  For example, the command <SPAN class=cpp-keyword>SetStrVal</SPAN>("<I>This quote "is ok</I>", svar) will set <I><B>This quote "is ok</B></I> to string variable svar.  If <B>",</B> is used inside a constant string, two constant strings must be created with one string indulding <B>"</B> and the other including <B>,</B>.  Then the two string are concatinated together to form the desired string.</LI>
<LI>A constant character should be contained in two single quotes.  Constant characters can also be implemented with code proceeded by backslash \. For example, '<I>\0x43</I>', '<I>\67</I>', and '<I>C</I>' are the same capital letter C. Since variables are case-insensitive, constant characters 'c' and 'C' are the same.  If it is important to distinguish c and C, for example, in an <SPAN class=cpp-keyword>if</SPAN> command, character code should be used.</LI>
</OL>

<H2>Description of commands</H2>

In the description of the command, the following convensions are used for variables:
<UL>
<LI>ivc: Represents that a parameter can be either an integer variable or an integer constant (i: Integer, v: Variable, c: Constant).  This is normally an input parameter.</LI>
<LI>iv: Represents that a parameter must be an integer variable.  This is normally an output parameter.</LI>
<LI>svc: Represents that a parameter can be either a string variable or a string constant (s: String, v: Variable, c: Constant).  This is normally an input parameter.</LI>
<LI>sv: Represents that a parameter must be a string variable.  This is normally an output parameter.</LI>
<LI>In a command, the input parameters normally go first, then followed by output parameters.</LI>
<LI>If a command requires a parameter as output, do not use a number as variable (mose like by accident).  Since any character can be used as variable, the script will happily put the result into this variable.  For example, <SPAN class=cpp-keyword>SetIntVal</span>(5, 0); will set integer 5 to a variable "0".  Now the value of variable "0" is 5.  Later when constant 0 is used, it is 5, not 0. When doing the compare of a variable with 0, it will have wrong result.</LI>
</UL>

<H2>Program control commands</H2>
<P>For the control commands, the command may be appended with "c", "s", "si".  "c" means that a cal command is performed.  "s" means string comparison.  "si" means string comparison without case.  For example: ifc("2.5+x*3", >, "s+5*x"): First "2.5+x*3" and "s+5*x" are calculated, then results are compared, the action is based on the compare result.</P>

<P>
<B>
<SPAN class=cpp-keyword>If</SPAN>(val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>Iff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>Ifc</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Iffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Ifs</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Iffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Ifsi</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Iffsi</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Else</SPAN>();<BR>
<SPAN class=cpp-keyword>ElseIf</SPAN>(val:ivc, opcode, val:ivc);<BR>
<SPAN class=cpp-keyword>ElseIff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>ElseIfc</SPAN>(val:svc, opcode, val:svc);<BR>
<SPAN class=cpp-keyword>ElseIffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ElseIfs</SPAN>(val:svc, opcode, val:svc);<BR>
<SPAN class=cpp-keyword>ElseIffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ElseIfsi</SPAN>(val:svc, opcode, val:svc);<BR>
<SPAN class=cpp-keyword>ElseIffsi</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndIf</SPAN>();<BR>
</B>&nbsp; --&gt;
The <CODE>If</CODE> command is a conditional command.  The general format for the <CODE>If</CODE> command is <CODE>If Else EndIf</CODE>.  For multiple conditions, <CODE>If</CODE> command can be chained together with <CODE>ElseIf</CODE>.</P>

<P>It is not necessary to have <CODE>Else</CODE> or <CODE>ElseIf</CODE> in the <CODE>If</CODE> command, but <CODE>If</CODE> and <CODE>EndIf</CODE> must match for <CODE>If</CODE> command.  Interpretor will check whether they are matched. If they are not matched, an error is flagged and the script file will not be executed.</P>

<P><CODE>If</CODE> command takes three parameters: two integer values and an operation. If the operation result on the two variables is true, commands between <CODE>If</CODE> and <CODE>Else</CODE> or <CODE>ElseIf</CODE> are executed.  Otherwise, commands between <CODE>Else</CODE> and <CODE>EndIf</CODE> are executed.</P>

<P>An <CODE>If</CODE> command can be nested inside of another <CODE>If</CODE> command.  There is no limit to the number of nests.</P>

<P>The functions of <CODE>Iff</CODE> and <CODE>ElseIff</CODE> are the same as those of <CODE>If</CODE> and <CODE>ElseIf</CODE>.  However, <CODE>Iff</CODE> and <CODE>ElseIff</CODE> take 7 parameters, two conditions and a logic operator of the results of the two conditions to find out the true or false results.</P>

<P><CODE>If</CODE>, <CODE>ElseIf</CODE>, <CODE>Iff</CODE>, <CODE>ElseIff</CODE>, <CODE>Else</CODE>, and <CODE>EndIf</CODE> can be mixed. </P> 

<P><CODE>Ifc</CODE> (Calculate) command has the same meaning as <CODE>If</CODE> command with some differences.  The first difference is that the variables in <CODE>Ifc</CODE> are string variables.  The second difference is that expressions can be used in <CODE>Ifc</CODE> command.  For example:</P> 

<PRE>
<SPAN class=cpp-keyword>iffc</SPAN>(3+5, &gt;, 3+4, &&, 2, &gt;, 1)<SPAN class=cpp-comment></SPAN>
</PRE>

<P><CODE>Ifs</CODE> (String) command performs the string comparison.  The operation has only &gt;=, ==, !=, &lt;=, &gt;, and &lt.</P> 

<P><CODE>Ifsi</CODE> (String case Insensitive) command performs the case insensitive string comparison.  The operation has only &gt;=, ==, &lt;=, &gt;, and &lt.</P> 

<P>
<B>
<SPAN class=cpp-keyword>while</SPAN>(init:ivc, ivc, opcode, ivc, increment:ivc);<BR>
<SPAN class=cpp-keyword>whilec</SPAN>(init:svc, svc, opcode, svc, increment:svc);<BR>
<SPAN class=cpp-keyword>whiles</SPAN>(init:svc, svc, opcode, svc, increment:svc);<BR>
<SPAN class=cpp-keyword>whilesi</SPAN>(init:svc, svc, opcode, svc, increment:svc);<BR>
<SPAN class=cpp-keyword>Break</SPAN>();<BR>
<SPAN class=cpp-keyword>BreakIf</SPAN>(val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>BreakIff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>BreakIfc</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>BreakIffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>BreakIfs</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>BreakIffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>Continue</SPAN>();<BR>
<SPAN class=cpp-keyword>ContinueIf</SPAN>(val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>ContinueIff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>ContinueIfc</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ContinueIffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ContinueIfs</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ContinueIffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ContinueIffsi</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>wend</SPAN>();<BR></B>&nbsp; --&gt;
<CODE>While</CODE> command is a loop command.  It requires a matched <CODE>Wend</CODE> to mark the end of command blocks.</P>

<P><CODE>While</CODE> command takes five parameters.  The first parameter is the initial value of the variable.  The next three parameters are same as <CODE>If</CODE> command does.  The block of commands will be repeatedly executed until the operation result becomes false.  The parameters must be modified inside the block to avoid infinite loop.  The last parameter is the increment to counter variable (second parameter) after the commands between <CODE>While</CODE> and <CODE>Wend</CODE> have been executed.</P>

<P>Note that any character can be used as variable.  For example, 1 is a variable, but the intention is to use this as a constant.  If command While(1, 1, ==, 1, 1) is used, the value of constant 1 becomes 2 after first increment.  Then the value becomes 4 (2+2) after second increment, etc.  This is still an infinite loop as intended because the value is always the same although the value of variable 1 is not 1 anymore.  A better way is to use command While(0, 0, ==, 0, 0)</P>

<P><CODE>While</CODE> command can also be nested inside of another one.  Again there is no limit to the number of nests.</P>

<P><CODE>If</CODE> and <CODE>While</CODE> commands can be nested inside of each other.  There is no limit to the number of nests.  But each command must be matched in one block boundary.</P>

<P><CODE>Break</CODE> and <CODE>Continue</CODE> can exist inside a <CODE>While</CODE> command.  <CODE>Break</CODE> jumps out the loop to execute the commands after <CODE>Wend</CODE>. <CODE>Continue</CODE> goes to the beginning of the While command.</P>

<P><CODE>Break</CODE> and <CODE>Continue</CODE> can be used with <CODE>If</CODE> command to change execution sequence based on a certain condition. Multiple <CODE>Break</CODE> and <CODE>Continue</CODE> can be used in a <CODE>While</CODE> command.</P>

<P><CODE>whilec</CODE> command has the same format as <CODE>while</CODE>, but all parameters are treated as string variable.  All parameters can be a string expression.  For example, Whiles(0.1+a, n, <, 6+6, 1+0.25);.  In the loop, n should be treated as string variable.</P>

<P>See "Operation commands" section for all opcodes.  In the following example, "TEST 1" is displayed if the shift is 1, "TEST 0" is displayed if the shift is 2.</P>

<PRE>
<SPAN class=cpp-keyword>if</SPAN>(2, &gt;&gt;, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  SetStrToBox</SPAN>("TEST 1", 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>else</SPAN>();<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  SetStrToBox</SPAN>("TEST 0", 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>endIf</SPAN>();<SPAN class=cpp-comment></SPAN>
</PRE>

<P>
<B>
<SPAN class=cpp-keyword>Sub</SPAN>(name:svc);<BR>
<SPAN class=cpp-keyword>GoSub</SPAN>(name:svc);<BR>
<SPAN class=cpp-keyword>Return</SPAN>();<BR>
<SPAN class=cpp-keyword>ReturnIf</SPAN>(val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>ReturnIff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>ReturnIfs</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ReturnIfsi</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ReturnIffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ReturnIffsi</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ReturnIfc</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>ReturnIffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
</B>
&nbsp; --&gt;<CODE>Sub</CODE> defines the beginning of a subroutine. The only parameter is the name of the subroutine.  <CODE>Return</CODE> returns to the caller from the subroutine.</P>

<P><CODE>GoSub</CODE> calls a subroutine with the only parameter as the subroutine name.</P>

<P>Here are some general rules of using subroutine:</P>

<UL>
<LI>There is no local variables.  All variables used in a subroutine are global.  The variable defined (i.e., variable used for the first time) outside a subroutine can be used inside the subroutine.  The modification to a variable is transparent to anywhere outside the subroutine.  This rule applies to variables defined inside a subroutine.</LI>
<LI>For each <CODE>Sub</CODE> command, there should exists at least one matching <CODE>Return</CODE> command.</LI>
<LI>A conditional <CODE>Return</CODE> can be used inside a subroutine.</LI>
<LI>A subroutine can call another subroutine, or even itself recursively.  If a subroutine calls itself, there must be a condition to return from the subroutine.  Otherwise there will be an infinite loop, and the program may finally crash.</LI>
<LI>The recursive call to a subroutine or to itself is umlimited.</LI>
<LI>In general, the subroutine body should placed at the end of the file after the <CODE>EndProgram</CODE> command.</LI>
<LI>At the end of the main program, there should be a <CODE>EndProgram</CODE> command.  Otherwise, the subroutine will be executed.</LI>
<LI>Subroutine name can be used to return an integer value, a string value, an integre stack, and a string stack.</LI>
</UL>

<P>Subroutine example:  This program uses subruotine to calculate the factorial.  Of course, it may be easier to use a <CODE>While</CODE> loop for this.  This subroutine just illustrates the resursive subroutine call.</P>

<PRE>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(10, n);             <SPAN class=cpp-comment>// number</SPAN>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(1, fact);           <SPAN class=cpp-comment>// initial vaule</SPAN>
<SPAN class=cpp-keyword>GoSub</SPAN>(fact);                        <SPAN class=cpp-comment>// call the subroutine</SPAN>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(fact, 5);           <SPAN class=cpp-comment>// show the value: 3628800</SPAN>
<SPAN class=cpp-keyword>EndProgram</SPAN>();                       <SPAN class=cpp-comment>// end of the program</SPAN>

<SPAN class=cpp-keyword>Sub</SPAN>(fact)                           <SPAN class=cpp-comment>// Define the subroutine</SPAN>
  <SPAN class=cpp-keyword>if</SPAN>(n, ==, 1) return(); Endif();   <SPAN class=cpp-comment>// last one, return</SPAN>
  <SPAN class=cpp-keyword>op</SPAN>(fact, *, n, fact);             <SPAN class=cpp-comment>// multiply</SPAN>
  <SPAN class=cpp-keyword>op</SPAN>(n, -, 1, n);                   <SPAN class=cpp-comment>// reduce by one</SPAN>
  <SPAN class=cpp-keyword>GoSub</SPAN>(fact);                      <SPAN class=cpp-comment>// call itself</SPAN>
<SPAN class=cpp-keyword>Return</SPAN>();                           <SPAN class=cpp-comment>// return</SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>ExecStr</SPAN>(str:svc);</SPAN></B>  ---&gt; executes the code stored in the string variable.  The contents in string variable can be changed for different function.</P>

<P><B><SPAN class=cpp-keyword>ExecClipboard</SPAN>(name:svc);</B> ---&gt;<CODE> ExecClipboard</CODE> executes the code stored in the clipboard.  The parameter is the unique indicator for a particular clipboard contents.  For different clipboard contents, another upique id must be used.</P>

<P>A particular string content or clipboard content can be executed multiple times.  Once they are executed one time, the contents are stored in program memory for multiple execution.</P>

<P>
<B>
<SPAN class=cpp-keyword>EndProgram</SPAN>();<BR>
<SPAN class=cpp-keyword>EndProgramIf</SPAN>(val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>EndProgramIff</SPAN>(val:ivc,opcode,val:ivc,opcode,val:ivc,opcode,val:ivc);<BR>
<SPAN class=cpp-keyword>EndProgramIfc</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndProgramIffc</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndProgramIfs</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndProgramIfsi</SPAN>(val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndProgramIffs</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
<SPAN class=cpp-keyword>EndProgramIffsi</SPAN>(val:svc,opcode,val:svc,opcode,val:svc,opcode,val:svc);<BR>
</B>
&nbsp; --&gt;<CODE>EndProgram</CODE> ends the execution of the script.</P>

<P><B><SPAN class=cpp-keyword>Source</SPAN>(file:svc);</B> ---&gt;
<CODE>Source</CODE> command jumps to execute commands in a file, then returns to execute the next line after the <CODE>Source</CODE> command.  It treats the commands in the file as a subroutine.  This could be useful sometimes, but it can also results in unexpected consequences due to the fact that everything is global.  Also any subroutine name in the sourced files should not be the same as the file name.</P>

<P><CODE>Source</CODE> command example 1:  The following is the main program.  It sources three files.</P>

<PRE>
<SPAN class=cpp-keyword>TestShowProgram</SPAN>("C:\UserData\temp1\tt.txt");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("db_source_file1.txt", file);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Source</SPAN>(file);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Source</SPAN>("db_source_file2.txt");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Source</SPAN>("db_source_file3.txt");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(4567, 4);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>EndProgram</SPAN>();<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Source</SPAN>("db_source_file1.txt");<SPAN class=cpp-comment></SPAN>
</PRE>

<P>Command in db_source_file1.txt:</P>
<PRE>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(1234, 1);
</PRE>

<P>Command in db_source_file2.txt:</P>
<PRE>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(2345, 2);
</PRE>

<P>Command in db_source_file3.txt:</P>
<PRE>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(3456, 3);
</PRE>

<P>After execution of the main program, the edit boxes will show the correct values, i.e., 1234 in Box 1, 2345 in Box2, 3456 in Box 3, and 4567 in Box 4.</P>

<P>The tt.txt shows the program code:</P>
<PRE>
000	124	000	07c	TestShowProgram
001	024	001	018
002	002	002	002	SetStrVal
003	025	003	019
004	026	004	01a
005	035	005	023	GoSub
006	026	006	01a
007	035	007	023	GoSub
008	027	008	01b
009	035	009	023	GoSub
010	028	00a	01c
011	078	00b	04e	SetDecToBox
012	011	00c	00b
013	012	00d	00c
014	029	00e	01d	EndProgram
015	035	00f	023	GoSub
016	025	010	019
017	029	011	01d	EndProgram
018	078	012	04e	SetDecToBox
019	013	013	00d
020	014	014	00e
021	034	015	022	Return
022	078	016	04e	SetDecToBox
023	015	017	00f
024	016	018	010
025	034	019	022	Return
026	078	01a	04e	SetDecToBox
027	013	01b	00d
028	017	01c	011
029	034	01d	022	Return
</PRE>

<P>Notes for Source command:</P>
<OL>
<LI>If the parameter to the Source command is a constant string (with double quote at the beginning and end), the contents of the file is loaded into memory.  If the parameter is an variable (even the variable is assigned a file name), the file is not loaded.  So Source command with variable as parameter can run different files at run time, as the following program shows.</LI>
<LI>The file to be sourced is treated as a subroutine.  A return command is automatically added to the end of the contents of the sourced file.  If there is subroutine in the sourced file, the Return command must be added manually at a certain point.</LI>
</OL>

<P><CODE>Source</CODE> command example 2:</P>

<PRE>
<SPAN class=cpp-keyword>StrStackClearAll</SPAN>();
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "rmv_src_diff_dir.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "savehtml.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "htmltag.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "rmv_src_same_dir.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "replace_percent.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "remove_html_comments.txt");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(a, "remove_html_scripts.txt");

<SPAN class=cpp-keyword>while</SPAN>(1, ==, 1)
  <SPAN class=cpp-keyword>Selection</SPAN>(a, "Select script to execute", 0, aidx, str);
  <SPAN class=cpp-keyword>if</SPAN>(aidx, ==, -1) <SPAN class=cpp-keyword>break</SPAN>(); <SPAN class=cpp-keyword>EndIf</SPAN>();
  <SPAN class=cpp-keyword>Source</SPAN>(str);
<SPAN class=cpp-keyword>Wend</SPAN>();

<SPAN class=cpp-keyword>EndProgram</SPAN>();

<SPAN class=cpp-keyword>Source</SPAN>("rmv_src_diff_dir.txt");
<SPAN class=cpp-keyword>Source</SPAN>("savehtml.txt");
<SPAN class=cpp-keyword>Source</SPAN>("htmltag.txt");
<SPAN class=cpp-keyword>Source</SPAN>("rmv_src_same_dir.txt");
<SPAN class=cpp-keyword>Source</SPAN>("replace_percent.txt");
<SPAN class=cpp-keyword>Source</SPAN>("remove_html_comments.txt");
<SPAN class=cpp-keyword>Source</SPAN>("remove_html_scripts.txt");
</PRE>

<P>In this script file, the <CODE>Source</CODE> command in the <CODE>While</CODE> loop uses a string variable as its input parameter.  The variable is assigned a value by <CODE>Selection</CODE> command.  The other <CODE>Source</CODE> commands just loads the files into memory.  But these <CODE>Source</CODE> commands do not execute the script files since the program never run to this point.  Which script is executed depends on the <CODE>Source</CODE> command in the while loop.  Note that it is important to place a <CODE>EndProgram</CODE> command before all the <CODE>Source</CODE> commands</P>

<P>The parameter of the <CODE>Source</CODE> command takes two form, string variable and string constant.  If the parameter is a string constant, it is supposed to be script file.  The file will be loaded into memory at the compile time.  If there are <CODE>Source</CODE> commands in the sourced script, those scripts are also loaded to the memory at the compile time.  The loaded script can be very large.</P>

<P>The <CODE>Source</CODE> command always generates a GoSub command.  If the parameter is a constant, the file indicated by the constant is also loaded into memory at the compile time.  If the file is not found, an error is generated while compiling.  However, if a variable is assigned a wrong value and used in the <CODE>Source</CODE> command, unexpected results can be generated.</P>

<H2>Clipboard Command</H2>
<P><B>
<SPAN class=cpp-keyword>GetFromClipBoard</SPAN>(sv);<BR>
<SPAN class=cpp-keyword>GetFromClipBoardHtml</SPAN>(sv);<BR>
<SPAN class=cpp-keyword>SendToClipBoard</SPAN>(src str:svc);<BR>
<SPAN class=cpp-keyword>StrStackToClipboard</SPAN>(stk:sv);<BR>
<SPAN class=cpp-keyword>StrStackFromClipboard</SPAN>(stk:sv);<BR>
<SPAN class=cpp-keyword>StrStackToFile</SPAN>(stk:sv, file:svc, encode:ivc, append:iv);<BR>
<SPAN class=cpp-keyword>StrStackFromFile</SPAN>(file:svc, stack:sv);<BR>
<SPAN class=cpp-keyword>IntStackToClipboard</SPAN>(stk:sc, fmt:svc);<BR>
<SPAN class=cpp-keyword>IntStackFromClipboard</SPAN>(fmt:svc, stk:sc);<BR>
<SPAN class=cpp-keyword>IntStackFromFile</SPAN>(file:svc, fmt:svc, stack:sv);<BR>
<SPAN class=cpp-keyword>IntStackToFile</SPAN>(stk:sv, fmt:svc, file:svc, encode:ivc, append:iv);<BR>

m_cboCommand.AddString(_T("();"));

<SPAN class=cpp-keyword>IntStackFromFile</SPAN>(file:svc, fmt:svc, stack:sv););<BR>
</B>
&nbsp; --&gt; Clipboard commands include <CODE>GetFromClipBoard</CODE> and <CODE>SendToClipBoard</CODE>, both require a string variable. The contents in the clipboard should be text or unicode text.</P>

<P><CODE>GetFromClipBoardHtml</CODE> returns the copied contents with html tags.  After a section of html content is copied from a browser and pasted in a text editor, all the html tags are removd.  To keep the tags, run this command before pasting the text.</P>

<P><CODE>StrStackToClipboard</CODE> copies the contents of a string stack to clipboard.  Each item in the stack takes one line in the clipboard</P>

<P><CODE>StrStackToFile</CODE> writes the contents of the stack into a file. encode is the format written into a file.  If append is 1, the contents is appended to the file.</P>

<P><CODE>StrStackFromFile</CODE> read the contents of a file into a string stack. Each line in the file is put into aen item in the stack.</P>

<P><CODE>IntStackFromFile</CODE> read the contents of of a file into a string.  fmt </P>

<P>There are corresponding int stack functions.  These function require a fmt variable.  fmt can be %d, %x, %b.</P>

<H2>Commands related to files</H2>
<P>
<B><SPAN class=cpp-keyword>OpenReadFile</SPAN>(file name:svc, enc:iv, handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>OpenWriteFile</SPAN>(file name:svc, unicode:ivc, appen:ivc, handle:iv);</B></P>

<P>Script provides many commands to operate on files.</P>  
<P>The first group of commands for file operations is for reading from or writing to a file.  These commands only work on text files, including unicode text files. To read from or write to a file, the file must be opened first.  <CODE>OpenReadFile</CODE> opens an existing file for read.  It takes three parameters: a file name in a string variable as input, an output integer to indicate the file encoding, and another output integer that stores an unique integer handle associated with this file name.  When a file is opened successfully, <CODE>OpenReadFile</CODE> returns a non-zero handle. This handle is used in the <CODE>ReadLine</CODE> and <CODE>CloseReadFile</CODE> commands.  The second variable indicates if the file is ACCII (0), UNI16_BE (1, start with FE FF, MSB, LSB), UNI16_LE (2, same as unicode, start with FF FE, LSB, MSB), or UTF_8 (3, start with EF BB BF).  This value can be used in <CODE>OpenWriteFile</CODE> command.  When a file is opened for read, it is opened in unicode mode automatically if the file is an unicode file. <CODE>OpenWriteFile</CODE> takes four parameters: a file name, an integer to indicate what format the file is to be opened for writing, another integer for appending if the value is 1, and an output integer that stores the returned handle associated with the file name.  The second parameter is normally the value returned from <CODE>OpenReadFile</CODE> command.</P>

<P>A file can be opened either for read or for write, but not for both. To read a line from a file opened for reading, use <CODE>ReadLine</CODE> command.  The first parameter to the command is the file handle returned from <CODE>OpenReadFile</CODE> command.  The second parameter returns a flag to indicate if it is the end of the file after this read.  This flag should be checked before next read.  The line read from the file is stored in the third parameter.</P>  

<P><B><SPAN class=cpp-keyword>ReadLine</SPAN>(handle: iv, eof:iv, str: sv);</B> --&gt; 
<CODE>ReadLine</CODE> reads a line from the file.  It returns EOF (End Of File) and the string.</P>

<P><B><SPAN class=cpp-keyword>WriteLine</SPAN>(str: svc, handle: iv);</B> --&gt; 
Text is written to a file with <CODE>WriteLine</CODE> command.  <CODE>WriteLine</CODE> puts a carriage return automatically at the end of each line.</P>

<P><B><SPAN class=cpp-keyword>WriteEndl</SPAN>(handle: iv);</B> --&gt; 
<CODE>WriteEndl</CODE> writes a end of line (carriage return) to the file.</P>

<P><B><SPAN class=cpp-keyword>CloseReadFile</SPAN>(handle: iv);</B><BR<
<B><SPAN class=cpp-keyword>CloseWriteFile</SPAN>(handle: iv);</B><BR> --&gt; 
After operations are done with a file, the file should be closed with <CODE>CloseReadFile</CODE> or <CODE>CloseWriteFile</CODE>.</P>

<P>When a file is opened, the returned handle should be checked before further operations on the file.  If the handle value is zero, the file is not opened correctly.</P>

<P><B><SPAN class=cpp-keyword>IsEof</SPAN>(handle: iv, result:iv);</B> --&gt; 
For reading from a file, it should check if it is at the end of the file with <CODE>IsEof</CODE> before reading. If <CODE>IsEof</CODE> returns a non-zero value, there is no more contents to read in the file.</P>

<P>Multiple input files and output files can be opened at the same time.  The maximum number of files opened for either read or write at one time is 20.</P>


<P><B><SPAN class=cpp-keyword>ReadAll</SPAN>(fn:svc, enc:iv, str: sv);</B> --&gt;
ReadAll opens the file, reads all contents into the string variable, then closes the file.  It also returns the encoding of the file.</P>

<P><B><SPAN class=cpp-keyword>WriteAll</SPAN>(str:svc, fn:svc, enc:iv, append:sv);</B> --&gt;
WriteAll opens the file, writes all contents of the string variable into the file, then closes the file.</P>

<P><B><SPAN class=cpp-keyword>ReadAllStack</SPAN>(fn:svc, enc:iv, stkstr: sv);</B> --&gt; 
ReadAllStack open the file, read all contents into the stack variable (each line into a stack value), then close the file.  It also returns the encoding of the file.</P>

<P><B><SPAN class=cpp-keyword>RemoveDirectory</SPAN>(str:svc);</B> --&gt; 
<CODE>RemoveDirectory</CODE> removes a directory.  The directory name can have a backslash at the end, or without the backslash at the end.</P>

<P><B><SPAN class=cpp-keyword>CreateDirectory</SPAN>(str:svc, result:iv);</B> --&gt; 
<CODE>CreateDirectory</CODE> creates a new directory.  The directory name can have a backslash at the end, or without the backslash at the end.  If the directory is created successfully, the return value is non-zero.  Otherwise, a zero value is returned.</P>

<P>The second group of file operation commands includes miscellaneous commands to manipulate files.</P>

<P><B><SPAN class=cpp-keyword>IsFileExist</SPAN>(filename:svc, result:iv);</B> --&gt; 
<CODE>IsFileExist</CODE> returns a non-zero value if a file or a directory exists.  Otherwise, it returns 0.  To open a file for write, it may be necessary to check if the file already exists to avoid overwriting the contents of the file. </P>

<P><B><SPAN class=cpp-keyword>AppendFile</SPAN>(src_file1:svc, scr_file2:svc, des_file:svc);</B><BR>
<B><SPAN class=cpp-keyword>SeekTo</SPAN>(inf hand:ivc, pos:ivc);</B><BR></P>

<P><B><SPAN class=cpp-keyword>GetFileSize</SPAN>(fn:svc, des:iv);</B> --&gt; 
<CODE>GetFileSize</CODE> returns the file size in bytes.</P> 

<P><B><SPAN class=cpp-keyword>DeleteFile</SPAN>(str:svc);</B> --&gt; 
<CODE>DeleteFile</CODE> deletes an existing file.</P>

<P><B><SPAN class=cpp-keyword>MoveFile</SPAN>(src_fn:svc, des_fn:svc);</B> --&gt; 
<CODE>MoveFile</CODE> moves a file (or a directory) from one location to another, or rename the file (or a directory).</P>

<P><B><SPAN class=cpp-keyword>CopyFile</SPAN>(src_file:svc, des_file:svc);</B> --&gt; 
<CODE>CopyFile</CODE> copies the source to destination file.  The destination file of both MoveFile and CopyFile must contain file name.  The functions would not work if destination file is a directory name.</P>

<P><B><SPAN class=cpp-keyword>CompareFile</SPAN>(f1:svc, f2:svc, rlt:iv);</B> --&gt; 
<CODE>CompareFile</CODE> compare the contents of two files.  First the full pathes of the files are compared.  If they are the same, return 1. Then the file sizes are compared.  If they are different, return 0.  Finally, the contesnts of the files are commpared.  The result is 1 if they are the same.  Otherwise the result is 0.</P>

<P><B><SPAN class=cpp-keyword>FindFile</SPAN>(str:svc, Handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>FindNextFile</SPAN>(Handle:iv, dir flag:iv, fn str:iv);</B><BR>
<B><SPAN class=cpp-keyword>CloseFindFile</SPAN>(Handle:iv);</B><BR>
--&gt; To find what files are in a directory, use commands <CODE>FindFile</CODE> and <CODE>FindFileNext</CODE>. These two commands must work together to get the file names.</P>

<P><CODE>FindFile</CODE> must be used first.  <CODE>FindFile</CODE> takes a string as input, return an integer handle associated with this string.  If handle returned is 0, no file exists in the directory, or the directory does not exist. In this case, no <CODE>FindFileNext</CODE> should be called with this handle.  <CODE>FindNextFile</CODE> takes three parameters. The first one is used both as input and output.  It is generally the handle returned from <CODE>FindFile</CODE>.  After the command, the value could be changed to zero if all files are found.  Therefore, the value should be checked before calling <CODE>FindNextFile</CODE> again. The second parameter stores an integer value indicating if the file found is a directory name or a file name.  If the value is not zero, the string returned can be either a dot directory (bit 0 = 1) or a subdirectory (bit 1 = 1). The third parameter returns the name string found. Note that the string returned are file name with full path.</P>

<P>Depending on the format of the string to <CODE>FindFile</CODE> command, different types of files are returned. If the string ends with * (star) or *.* (star dot star), all files in the directory are returned in the subsequent <CODE>FindNextFile</CODE> commands.  If the string ends with <I>dir\*.ext</I>, only files with the same extension <I>ext</I> are returned in the subsequent <CODE>FindNextFile</CODE>.</P>

<P>Then <CODE>CloseFindFile</CODE> closes the FindFile handle.</P>

<P>The following example shows the uses of <CODE>FindFile</CODE> and <CODE>FindNextFile</CODE> command.  The script displays all files (no directories) in c:\test directory.</P>

<P>First <CODE>FindFile</CODE> is called with directory string.  The return handle from the call is checked.  If the value is zero, a prompt string is shown in text box 4, and script ends.</P>

<P>Then <CODE>FindNextFile</CODE> is then called in a while loop to display all files in the directory.</P>

<PRE>
<SPAN class=cpp-keyword>FindFile</SPAN>("C:\test\*.*", handle);  <SPAN class=cpp-comment>// Open handle</SPAN>

<SPAN class=cpp-keyword>if</SPAN>(handle, ==, 0)
  <SPAN class=cpp-keyword>SetStrToBox</SPAN>("Directory not exist", 4)
  <SPAN class=cpp-keyword>MessageBeep</SPAN>(); <SPAN class=cpp-keyword>EndProgram</SPAN>();
<SPAN class=cpp-keyword>endif</SPAN>();

<SPAN class=cpp-keyword>while</SPAN>(handle, !=, 0)

  <SPAN class=cpp-keyword>FindNextFile</SPAN>(handle, dotdir, filename);
  <SPAN class=cpp-keyword>if</SPAN>(dotdir, ==, 0)
    <SPAN class=cpp-keyword>Display</SPAN>(filename);
  <SPAN class=cpp-keyword>endif</SPAN>();

<SPAN class=cpp-keyword>wend</SPAN>();
</PRE>

<P>See FileInDir to find all file in a directory</P>


<P><B><SPAN class=cpp-keyword>CompareFileSize</SPAN>(f1:svc, f2:svc, rlt:iv);</B> --&gt; 
<CODE>CompareFileSize</CODE> compare the size of two files. The return values are:</P>
<OL>
<LI>1: If the size of fn1 is larger than fn2</LI>
<LI>0: If the size of fn1 is same as fn2</LI>
<LI>-1: If the size of fn1 is smaller than fn2</LI>
</OL>

<P><B><SPAN class=cpp-keyword>CompareFileAll</SPAN>(f1:svc, f2:svc, time:iv, size:iv, content:iv);</B> --&gt; 

<CODE>CompareFileAll</CODE> compare the size of two files. The return values are:</P>

<P>The date stores in a integer stack has the format: 0: Year, 1: Month, 2: DayOfWeek (Sunday: 0, Monday 1, ...), 3: Day, 4: Hour, 5: Minute, 6: Second, 7: Milliseconds.</P>

<P><B><SPAN class=cpp-keyword>CompareFileTime</SPAN>(f1:svc, f2:svc, rlt:iv);</B> --&gt; 
<CODE>CompareFileTime</CODE> compare the last write time of two files. The return values are:</P>
<OL>
<LI>2: If fn2 does not exist</LI>
<LI>1: If the last write time of fn1 is later than fn2</LI>
<LI>0: If the last write time of fn1 is same as fn2</LI>
<LI>-1: If the last write time of fn1 is earlier than fn2</LI>
<LI>-2: If fn1 does not exist</LI>
</OL>
<P>With the above values, if the return value of the command is greater than 0, f1 can be copied to f2 for backup.</P>

<P><B><SPAN class=cpp-keyword>GetFileDate</SPAN>(fn:svc, create_stk:svc, write_stk:svc, access_stk:svc);</B> --&gt; 

<CODE>GetFileDate</CODE> returns the three times in three integer stacks.  The contents of the stack is 0: Year, 1: Month, 2: DayOfWeek (Sunday: 0, Monday 1, ...), 3: Day, 4: Hour, 5: Minute, 6: Second, 7: Milliseconds..  The last parameter, access_stk is the time when it is last written.</P>

<P><B><SPAN class=cpp-keyword>SetFileDate</SPAN>(fn:svc, created stk:svc, modified stk:svc, accessed stk:svc, flag:iv);</B> --&gt; 

<CODE>SetFileDate</CODE> sets the created time, the modified time, and the accessed time stored in the stack. The three integer stacks have the same format as the stack in GetFileDate.</P>

<P>For image file (like .gif), the date shown in Window Explorer is the created date.</P>

<P><B><SPAN class=cpp-keyword>GetFileTime</SPAN>(fn:svc, cth:iv, ctl:iv, lwth:iv, lwtl:iv, lath:iv, latl:iv);</B> --&gt; 

<CODE>GetFileTime</CODE> gets the create time, last write time, last access time of the file and stores the result in two integer variables.  The two integer can be combined to form 64 bit time.  The time values can be converted in date format with function Time2Date.</P>

<P><B><SPAN class=cpp-keyword>SetFileTime</SPAN>(fn:svc, cth:iv, ctl:iv, lwth:iv, lwtl:iv, lath:iv, latl:iv);</B> --&gt; 

<CODE>SetFileTime</CODE> just sets the three file times.  It has exact the same parameters as GetFileTime, with different input/output directions.</P>

<P><B><SPAN class=cpp-keyword>FileSplit</SPAN>(fn str:svc, bytes:iv);</B><BR>
<B><SPAN class=cpp-keyword>FileCombine</SPAN>(fn str:iv);</B><BR> --&gt; 

<CODE>FileSplit</CODE> splits a large file into small files with the specified bytes.  <CODE>FileCombine</CODE> combines the splited small files into a large file.  For example:</P>
<PRE>FileSplit("test.exe", 12345);</PRE>
<P>This command will split file name test.exe into files test.0, test.1, ....  Each file has 12345 bytes.  The last has the remained bytes.</P>
<PRE>FileCombine("test.exe");</PRE>
<P>This command combines test.0, test.1, ... into file test.exe.</P>

<P><B><SPAN class=cpp-keyword>FileInDir</SPAN>(dir:svc, flag:ivc, str:svc, mm/dd/yyyy:svc, stk:sv);</B> --&gt; 
<CODE>FileInDir</CODE> finds all files in a directory (with or without last back slash), and stores the file in a string stack.  The flag determined the format of files in the stack and what files to find depending on the bit field.</P>
<P>Bit 5: 0: files with date before mm/dd/yyyy; 1: files with date after mm/dd/yyyy.<BR>
Bit 4: 0: All files inrespect of date.  1: Files indicated by mm/dd/yyyy, before or after depending on bit 5.<BR>
Bit 3 and 2 (combined with the third parameter) determine which files are to find: bit 3:2: 00: all files; 01: extension; 10: name; 11: name or extension.<BR>
Bit 1: 1: include sub-directory; 0: only this directory.<BR>
Bit 0: 1: File with full path; 0: only file name.<BR></P>
<P>The third variable is a string to be found in the file name or extension as indicated by the second parameter.  For example, if the string is "txt" and bit 3 and 2 in flag is 10, only file name that contains "txt" will be found and stored in output stack variable.  If bit 3 and 2 is 00, all file will be found, and the third variable is not important in this case.  If bit 3 and 2 is 11, files contains the third variable in either file name or extension will be found.
</P>
<PRE>
<SPAN class=cpp-keyword>FileInDir</SPAN>("c:\userdata\", 5, "bmp", "", stk);
</PRE>
<P>The above command will find all files in c:\userdata\ directory with extension bmp.  The result will contains the directory name.</P>

<P><B><SPAN class=cpp-keyword>DirInDir</SPAN>(dir:svc, dir stk:svc);</B> --&gt; 

<CODE>DirInDir</CODE> finds all sub-directory in a directory, and stores the results in a string stack.  Note that the stack is not cleared in the command.  It the command is run twice, all directories in the two directories will be appended together.</P>

<P><B><SPAN class=cpp-keyword>FileInsertLineAt</SPAN>(src_file:svc, line:svc, at:ivc, des_file:svc);</B> --&gt; 

<CODE>FileInsertLineAt</CODE> inserts a line of text at the line number specified.  If the line number is 0, the text is inserted at the beginning of the file.  If the line number is 1, the text is inserted after the line 1 of the file.  If the line number is -1, the line is inserted at the end of the file.  Of curse, the text can also be inserted at the end of the file by specifying a very large number.  Specifying -1 for line number executes fast because it does not need to read the file line-by-line.  But there may be a little difference.  If the last line in the file does not have a carriage return, the text will be appended to the end (not after) of the last line if line number is specified as -1.  However, text will be added as separate line after the last line if a large number is specified as the line number.</P>

<P><B><SPAN class=cpp-keyword>FindRepeatFileInDir</SPAN>(dir:svc, stk ret:sv);</B> --&gt; 
<CODE>FindRepeatFileInDir</CODE> finds all the files that have the same contents, even the file name, file date, file directory may be different.  The results are placed in a string stack.</P>

<P><B><SPAN class=cpp-keyword>FindRepeatFileDirInDir</SPAN>(dir1:svc, dir2:svc, stk ret:sv);</B> --&gt; 

<CODE>FindRepeatFileDirInDir</CODE> finds the files in dir1 that also exist in dir2.  The file may have repeat in both directory.</P>

<P><B><SPAN class=cpp-keyword>DeleteRepeatFileDirInDir</SPAN>(dir1:svc, dir2:svc, stk ret:sv);</B> --&gt; 
<CODE>DeleteRepeatFileDirInDir</CODE> deletes file in dir1 if it also exists dir2.  See script file FindRepeatFile.txt as example.</P>

<P><B><SPAN class=cpp-keyword>RemoveEmptyDir</SPAN>(dirname:svc);</B> --&gt; 
<CODE>RemoveEmptyDir</CODE> removes any empty directory under specified directory.  If the specified directory is empty, it is also removed.</P>

<P><B><SPAN class=cpp-keyword>BackupFile</SPAN>(dirToBack:svc, RefDir:svc, destDir:svc, Delete:ivc, last:ivc);</B> --&gt; 
<CODE>BackupFile</CODE> backs up file in source directory (first parameter) to be backed up to the destination directory (second parameter).  The files in source directory is compared with files in reference directory (third parameter).  If the fourth parameter is 1, any backed-up files are deleted.  If the fifth parameter is non-zero, only files modified in the last number of day of the fifth parameter are backed up.  If the fifth parameter is zero, any modification of files at any time are backed up.</P>

<P><B><SPAN class=cpp-keyword>FileCountInDir</SPAN>(dirname:svc, flag:ivc, cnt:iv);");</B> --&gt; <CODE>FileCountInDir</CODE>returns the number of files in a directory.  If <B>flag</B> is 0, only return the number of file in current directory.  If <B>flag</B> is 1, the number of file in current directory and its sub-directory are returned.</P>

<P><B><SPAN class=cpp-keyword>DirCat</SPAN>(dir1:svc, dir2:svc, des:sv);</B> --&gt; Cancatnate two strings in directory format.  For exampe: DirCat("dir1", "dir2", x), x contains"dir1\dir2".</P>



<H2>Commands related to mouse</H2>
<P>
<B>
<SPAN class=cpp-keyword>LeftMouseClick</SPAN>();<BR>
<SPAN class=cpp-keyword>LeftMouseClickAt</SPAN>(valx:ivc, valy:ivc);<BR>
<SPAN class=cpp-keyword>LeftMouseMenuAt</SPAN>(valx:ivc, valy:ivc, menu item:ivc, delay after:ivc);<BR>
<SPAN class=cpp-keyword>LeftMouseDrag</SPAN>(valx1:ivc, valy1:ivc, valx2:ivc, valy2:ivc);<BR>
<SPAN class=cpp-keyword>RightMouseClick</SPAN>();<BR>
<SPAN class=cpp-keyword>RightMouseClickAt</SPAN>(valx:ivc, valy:ivc);<BR>
<SPAN class=cpp-keyword>RightMouseMenuAt</SPAN>(valx:ivc, valy:ivc, menu iten:ivc, delay after:ivc);<BR>
<SPAN class=cpp-keyword>MoveMouseTo</SPAN>(valx:ivc, valy:ivc);<BR>
<SPAN class=cpp-keyword>GetMousePos</SPAN>(posx:iv, posy:iv);<BR>
<SPAN class=cpp-keyword>MouseEvent</SPAN>(event:svc, posx:ivc, posy:ivc, wheel:ivc);<BR>
<SPAN class=cpp-keyword>WaitForDrag</SPAN>();<BR>
</B>--&gt;
Mouse commands include moving the mouse to a location (<CODE>MoveMouseTo</CODE>) and clicking the left and right mouse buttons. Mouse buttons can be clicked at the current location (<CODE>LeftMouseClick</CODE> and <CODE>RightMouseClick</CODE>), or moved to a position first and then clicked (<CODE>LeftMouseClickAt</CODE> and <CODE>RightMouseClickAt</CODE>). Left mouse can also be dragged from one position to another (<CODE>LeftMouseDrag</CODE>).  This function can be used to select an area in a program.  For example, LeftMouseDrag(200, 200, 300, 500); selects the area, draw a line or square.</P>

<P>Very often, it is necessary to select a menu item with left or right mouse, this can be done with commands <CODE>LeftMouseMenuAt</CODE> and <CODE>RightMouseMenuAt</CODE>. Thes two commands take two integers as the position (x and y locations relative to upper-left corner of the screen), the third integer as the menu item, and the fourth parameter as a delay in millisecond after the mouse is clicked.</P>

<P><CODE>MouseEvent</CODE> implements the function of mouse_event except the last parameter.  With this function, all the mouse functions can be implemented.  For example, the following script implements the mouse wheel function to a window.</P>
<PRE>
<SPAN class=cpp-keyword>LeftMouseClickAt</SPAN>(339, 637); 
<SPAN class=cpp-keyword>Delay</SPAN>(100); 
<SPAN class=cpp-keyword>MouseEvent</SPAN>("WHEEL|ABS", 339, 637, -1000);
</PRE>

<P>The first parameter for <CODE>MouseEvent</CODE> could be any combination of LDOWN, RDOWN, MDOWN, LUP, RUP, MUP, WHEEL, and ABS.  ABS specifies whether posx and posy are absolute of relative.  The second and third parameters specify the location where these events to happen.  The last parameter specifies the amount of wheel movement if the event is related to mouse wheel.</P>

<P><CODE>WaitForDrag</CODE> wait for the dragging of bulleye until release.  Then program starts executing the line following this command.  While the bulleye is dragging, parameters are placed in different boxes, as explained in bulleye section.</P>

<H2>Commands related to window</H2>
<P>
<B><SPAN class=cpp-keyword>GetWindowHandleAt</SPAN>(posx:ivc, posy:ivc, des hwnd:iv);</B><BR>
<B><SPAN class=cpp-keyword>GetForegroundWindow</SPAN>(hwnd:iv);</B><BR>
<B><SPAN class=cpp-keyword>CloseWindow</SPAN>(handle: ivc);</B><BR>--&gt;
All commands related to window requires a window handle.  A window handle is an unique integer number associated with a window.  A window handle can be obtained by draging the bull's eye on the script interface on to a window, script command <CODE>GetWindowHandleAt</CODE>, or <CODE>GetForegroundWindow</CODE>. <CODE>GetWindowHandleAt</CODE> requires the position of the window, which is generally a point in the windows title, or the client area. <CODE>GetForegroundWindow</CODE> returns the handle of the acrive window.</P>

<P>There is a predefined window handle for current running UtilProg with the name <B>HUTILPROG</B>.  It is like a predefined integer variable with the value initialized to the window handle of the current running program.  <B>HUTILPORG</B> can be used in any command that requires a window handle.  It should not be initialized to any other value.  For example, the current running UtilProg will be closed if the following command is executed:</P>

<PRE><SPAN class=cpp-keyword>CloseWindow</SPAN>(<B>HUTILPROG</B>);</PRE>

<P>
<B><SPAN class=cpp-keyword>GetWindowRect</SPAN>(hwnd:ivc, left:iv, top:iv, right:iv, bottom:iv);</B><BR>
<B><SPAN class=cpp-keyword>ResizeWindow</SPAN>(hwnd:ivc, left:ivc, top:ivc, right:ivc, bottom:ivc);</B><BR>
<B><SPAN class=cpp-keyword>MoveWindowTo</SPAN>(whnd:ivc, valx:ivc, valy:ivc);</B><BR> --&gt; 

After the handle of a window is known, its area can be found with <CODE>GetWindowRect</CODE> and resized with <CODE>ResizeWindow</CODE>.  The window can moved to a new location with <CODE>MoveWindowTo</CODE>.</P>

<P><B><SPAN class=cpp-keyword>SetWindowToTop</SPAN>(whnd:ivc);</B> --&gt; 

To perform mouse or keyboard operations to a window, the window must be brought to the top with command <CODE>SetWindowToTop</CODE>.  <CODE>SetWindowToTop</CODE> only works on a window that is not minimized.</P>

<P><B><SPAN class=cpp-keyword>GetWindowText</SPAN>(hwnd:ivc, text:sv);</B> --&gt; 
The text in window's title bar can be obtained by <CODE>GetWindowText</CODE>;</P>

<P>
<B><SPAN class=cpp-keyword>PageDown</SPAN>(hwnd:ivc);</B><BR>
<B><SPAN class=cpp-keyword>PageUp</SPAN>(hwnd:ivc);</B><BR>
<B><SPAN class=cpp-keyword>LineDown</SPAN>(hwnd:ivc);</B><BR>
<B><SPAN class=cpp-keyword>LineUp</SPAN>(hwnd:ivc);</B><BR> --&gt; 

If a window has a scroll bar, the contents of the window can be scrolled one page down (<CODE>PageDown</CODE>) or up (<CODE>PageUp</CODE>), or one line up (<CODE>LineUp</CODE>) or down (<CODE>LineDown</CODE>). These four commands work in general on a client window.</P>

<P><B><SPAN class=cpp-keyword>SendMessage</SPAN>(hwnd:ivc, wm:ivc, wparam:ivc, lparam:ivc);</B><BR>
<B><SPAN class=cpp-keyword>PostMessage</SPAN>(hwnd:ivc, wm:ivc, wparam:ivc, lparam:ivc);</B><BR> --&gt; 
<CODE>SendMessage</CODE> sends a window's message to a window.  <CODE>PostMessage</CODE> is alsmost the same as <CODE>SendMessage</CODE>.  <CODE>SendMessage</CODE> may not work with a certain window.  But <CODE>PostMessage</CODE> may work.  For example, IE window can not be closed by <CODE>SendMessage</CODE> with message <CODE>WM_CLOSE</CODE>.  But <CODE>PostMessage</CODE> does work with the same message.</P>

<P><B><SPAN class=cpp-keyword>GetParent</SPAN>(hWnd:ivc, hWnd:iv);</B> --&gt; 
<CODE>GetParent</CODE> return the handle of the parent from the handle of the current window.

<P><B><SPAN class=cpp-keyword>GetAncestor</SPAN>(hWnd:ivc, hWnd:iv);</B> --&gt; 
<CODE>GetAncestor</CODE> return the handle of the very top level window.  In some cases the message must be sent to the top level window.  This command can be used to get the handle the top level window.  For example, the ms paint has a client window.  The handle of this window can obtained with command GetWindowHandleAt.  But the message can not be send to this window with this handle.  However, the message can be sent to the handle from GetAncestor</P>

<P><B><SPAN class=cpp-keyword>SendKeyboardString</SPAN>(str:svc);</B> --&gt; 
<CODE>SendKeyboardString</CODE> behaviors as if you type the string.  For example:
</P>
<PRE>
<SPAN class=cpp-keyword>Delay</SPAN>(1000);<SPAN class=cpp-keyword> SendKeyboardString</SPAN>("String");<SPAN class=cpp-comment></SPAN>
</PRE>
<P>Copy the code into clipboard, then ExecClipboard in the program, move to a text editor, "String" will be typed in the editor.</P>


<H2>Key board commands</H2>

<P>
<B><SPAN class=cpp-keyword>SendKeyBoardString</SPAN>(str:svc);</B><BR>
<B><SPAN class=cpp-keyword>SendKeyControl</SPAN>(char);</B><BR> --&gt; 

Script provides several commands to simulate keyboard typing.  All characters are sent to the application that has the keyboard focus.  <CODE>SendKeyBoardString</CODE> sends a string to an application.  This string can include space and tab.  But it can not send special character such as carriage return, F key and up down arrows.  Use <CODE>SendSpecialKey</CODE> to send these keys to an application.  <CODE>SendKeyControl</CODE> sends a character with Ctrl key.  It simulates pressing a character and Ctrl key at the same time.</P>

<P><B><SPAN class=cpp-keyword>SendSpecialKey</SPAN>(char, repeat:ivc, delay:ivc);</B> --&gt; 

The following special key strings are valid for <CODE>SendSpecialKey</CODE> function:</P>

<PRE>
BACK: Back Key
TAB: Tab key
ALT: Alt key
CAPITAL: Caps Lock
SCROLL: Scroll Lock
NUMLOCK: Num Lock
ESCAPE: Esc key
SPACE: Space key
PAGEUP: Page Up
PAGEDOWN: Page Down
END: End
HOME: Home
LEFT: Left Arrow
UP: Up Arrow
RIGHT: Right Arrow
DOWN: Down Arrow
PRINTSCREEN: Print Screen
INS: Insert
DEL: Delete
RETURN: Enter
F key: F1, F2, F3, F4, F5, F6, F7, F8, F9, F10, F11, F12
</PRE>

<P>Example: SendSpecialKey("DOWN", 4, 100); will send Down key four times to a window that has keyboard focus, with 100ms delay between each key.</P>

<P>
<B><SPAN class=cpp-keyword>ShiftCtrlAltDown</SPAN>(shift, ctrl, alt);</B><BR>
<B><SPAN class=cpp-keyword>ShiftCtrlAltUp</SPAN>(shift, ctrl, alt);</B><BR> --&gt; 

To simulate pressing a key with SHIFT, ALT, and/or CTRL key at same time, use <CODE>ShiftCtrlAltDown</CODE> and <CODE>ShiftCtrlAltUp</CODE> commands.  These two commands take three parameters, representing SHIFT, ALT, and CTRL.  If the parameter is not zero, the corresponding key is either up or down.  For example, the following commands send a capital $$SEND$$ to an application:</P>

<PRE>
<SPAN class=cpp-keyword>ShiftCtrlAltDown</SPAN>(1, 0, 0);      <SPAN class=cpp-comment>// push down SHIFt key</SPAN>
<SPAN class=cpp-keyword>SendKeyBoardString</SPAN>("44send44");
<SPAN class=cpp-keyword>ShiftCtrlAltUp</SPAN>(1, 0, 0);        <SPAN class=cpp-comment>// release SHIFt key</SPAN>
</PRE>

<P>However, the easier way is to use command in this case:</P>
<PRE>
<SPAN class=cpp-keyword>SendKeyBoardString</SPAN>("$$SEND$$");
</PRE>
<P>The above example just serves as an illustration.</P>

<P>When using <CODE>ShiftCtrlAltDown</CODE> and <CODE>ShiftCtrlAltUp</CODE> commands, they must be matched.  If SHIFT, ALT, or CTRL is down, it must be released with <CODE>ShiftCtrlAltUp</CODE> command.  Otherwise, the keyboard will be messed up when the script ends.</P>

<H2>Interface commands</H2>

<P>
<B><SPAN class=cpp-keyword>SetDecToBox</SPAN>(src val:ivc, box:ivc);</B><BR>
<B><SPAN class=cpp-keyword>GetDecFromBox</SPAN>(box:ivc, des:iv);</B><BR>
<B><SPAN class=cpp-keyword>SetHexToBox</SPAN>(src val:ivc, box:ivc);</B><BR>
<B><SPAN class=cpp-keyword>GetHexFromBox</SPAN>(box:ivc, des:iv);</B><BR>
<B><SPAN class=cpp-keyword>SetStrToBox</SPAN>(src str:svc, box:ivc);</B><BR>
<B><SPAN class=cpp-keyword>GetStrFromBox</SPAN>(box:ivc, des:sv);</B> <BR>
<B><SPAN class=cpp-keyword>SetCharToBox</SPAN>(src str:svc, box:ivc);</B><BR>
<B><SPAN class=cpp-keyword>GetCharFromBox</SPAN>(box:ivc, des:sv);</B><BR> --&gt; 

On the <CODE>Script</CODE> page, There are 5 text boxes.  A script can communicate with these boxes to get information or send information to these boxes. These functions are useful for script initialization and debugging. For example, a file name is used in a script file.  This file name may change between runs.  Instead of modifying the script file, the file name can be entered in a text box.  The script gets the contents of the text box with one of these function. </P>

<P>To handle an integer variable as a decimal number, use <CODE>SetDecToBox</CODE> and <CODE>GetDecFromBox</CODE>.  <CODE>SetHexToBox</CODE> displays an integer value as hex number in a text box.  <CODE>GetHexFromBox</CODE> treats the text in the text box as hex number. For string, use <CODE>SetStrToBox</CODE> and <CODE>GetStrFromBox</CODE> commands.
</P>

<P>
<B><SPAN class=cpp-keyword>Display</SPAN>(str:svc);</B>--&gt; <CODE>Display</CODE> command just displays a string in the display box. </P>

<P><B><SPAN class=cpp-keyword>MessageBox</SPAN>(text:svc, MB_OK:sc, rtl:iv);</B> --&gt; <CODE>MessageBox</CODE> command pops up a dialog box and display some message as a prompt.  It blocks the execution of the script until the dialog box is dismissed.  <CODE>MessageBox</CODE> has three inputs.  The first parameter is the text to be displayed.  The second is a string flag to control what buttons are displayed.  The third returns the result of what button is pressed.  The following is a table of flag, button displayed, and the result displayed:</P>

<TABLE border=1>
<TR><TD>Flag</TD><TD>Button</TD><TD>Result</TD></TR>
<TR><TD>MB_OKCANCEL</TD><TD>Ok, Cancel</TD><TD>Ok: 1, Cancel: End Program</TD></TR> 
<TR><TD>MB_YESNO</TD><TD>Yes, No</TD><TD>Yes:1, No: 0</TD></TR>
<TR><TD>MB_RETRYCANCEL</TD><TD>Retry, Cnacel</TD><TD>Retry: 1, Cancel: End Program</TD></TR>
<TR><TD>MB_ABORTRETRYIGNORE</TD><TD>Abort, Retry, Ignore</TD><TD>Abort: End Program, Retry: 1, Ignore: 0</TD></TR>
<TR><TD>MB_YESNOCANCEL</TD><TD>Yes, No, Cancel</TD><TD>Yes: 1, No: 0, Cancel: End Program</TD></TR>
<TR><TD>MB_OK</TD><TD>Ok</TD><TD>Ok: 1</TD></TR>
</TABLE>

<P>If the result is End Program, the program execution is aborted. If the result is not exit, the commands followed in the script is executed.  The returned results can be used for further selection.</P>

<P><B><SPAN class=cpp-keyword>MessageBeep</SPAN>();</B> --&gt; 

<CODE>MessageBeep</CODE> plays a waveform sound as an audio prompt.</P>

<P><B><SPAN class=cpp-keyword>GetInput</SPAN>(titile:svc, initial:scv, input:sv);</B> --&gt; 

<CODE>GetInput</CODE> command pops up a dialog box.  The command takes an input as the window title, an initial string to put in the input box, and then returns the string in the third parameter.  If the Cancel button is clicked, the initial string is returned.</P>

<P>The difference between input dialog and other text boxes in the Script page is that this command block the execution of the script until the dialog is dismissed.</P>

<P><B><SPAN class=cpp-keyword>GetPassword</SPAN>(titile:svc, initial:scv, input:sv);</B> --&gt; 

<CODE>GetPassword</CODE> is almost the same as GetInput.  When text is typed in the box, it is just diplayed as *.</P>

<P><B><SPAN class=cpp-keyword>Selection</SPAN>(var:ivc, title:svc, sort:ivc, index:iv, str:sv);</B> --&gt; 

<CODE>Selection</CODE> command pops up a dialog with a list.  An item can be selected from the list. The return value is a zero-based index of the list and item text.  Before using the <CODE>Selection</CODE> command, items must be added to variable lists with the command <CODE>StrStackPush</CODE>. For multiple items, <CODE>StrStackPush</CODE> can be repeatedly used.</P>

<P><CODE>Selection</CODE> takes five parameters.  The first is the string stack variable with texts to be added to the selection list.  The second variable is the title of the dialog box.  The third one is an integer value.  If it is one, the item in the list will be sorted.  If the value is zero, the items will be in the order they are added by the function StrStackPush.  The fouth parameter is used as both input and output.  As an input, it is the initial index of the list when the dialog pops up.  At the return, it gets the index selected.  The fifth parameter is the return string selected.</P>

<P><B><SPAN class=cpp-keyword>BmpSelection</SPAN>(limitx:ivc, limity:ivc, fn:svc, title:svc, ok:iv, posx:iv, posy:iv);</B> --&gt; 

<CODE>BmpSelection</CODE> opens dialog with three buttons.  The "Select" button opens a bit map window that covers the whole desktop.  When the mouse clicks on the window, the window is closed.  If the "Ok" button is clicked, the command returns new position where the mouse is clicked.  When the "Cancel" is clicked, the original position is not changed.  The newly clicked position is abandoned.</P> 

<P>The command takes 8 parameters.  The first two parameters are x and y coordinate limits.  If mouse is clicked outside the limits, the bit map window is not closed.  If any of the parameters is 0, the clicking of the mouse on any position of the bit map window will close the window.  The ok parameter returns 1 if Ok button is clicked, -1 if Cancel button is clicked.  The parameters posx and posy return the position where the mouse is clicked if Ok button is clicked.  If the "Select" button is not used, or the Cancel" button is clicked, these two parameters are not changed.  The last parameter "mouse" returns which mouse is clicked.  It returns 1 if left mouse is clicked on the bit map, 0 if right mouse is clicked.</P>

<P><B><SPAN class=cpp-keyword>BmpMouseClick</SPAN>(fn:svc, posx:iv, posy:iv, mouse:iv);</B> --&gt; 

<CODE>BmpMouseClick</CODE> open a bitmap window that cover the desktop.  When the mouse is clicked, the window is closed.  The command returns the position where the mouse is clicked and which mouse is clicked.</P>

<P><B><SPAN class=cpp-keyword>BmpMultiSelection</SPAN>(fn:svc, title:svc, n_sel:ivc, stk:sv);</B> --&gt; 

<CODE>BmpMultiSelection</CODE> open a bitmap window.  When left mouse is click on the dialog window, the point of click is stored in an integer stack.  When the number of click is equal to n_sel, or the right mouse is clicked, or the close button in system menu is clicked, the window is closed.  The command returns an integer stack containing the position where the left mouse is clicked.  If n_sel is set to <=0, the dialog is closed only if right mouse is clicked or the close button in system menu is clicked.  <B>Note</B> right mouse function is not implemented.</P>

<P>fn is the bitmap file name.  Title is dialog's title.  n_sel is the number of click.  stk contains the location of the click.  Example:</P>

<PRE>
<SPAN class=cpp-keyword>BmpMultiSelection</SPAN>("C:\UserData\000\script\s8.bmp", "TEST", 0, stk);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackCombine</SPAN>(stk, ",", "%d", rlt);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(rlt, 5);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>See also the following HtmlTag example for the use of <CODE>Selection</CODE> command.</P>

<P><B><SPAN class=cpp-keyword>SelectFile</SPAN>(prompt:svc, dir:svc, flag:iv, file:sv);</B> --&gt; 

<CODE>SelectFile</CODE> pops up a file dialog window.  This allows you to change to a directory and select a file.  The first parameter to this function is the prompt in dialog window's title.  The second parameter is an input string as the initial directory.  The string may include a file extension to select only a certain type of files.</P>

<P>If the initial directory ends with a backslash \, star *, or *.*, all files in the directory will be displayed in file open dialog.  If the string ends with \*.ext, only files with same extension are displayed in the file open dialog.</P>

<P>If the Ok button is clicked, the third parameter <I>flag</I> is set to one, and the selected file name with full path will be returned in the fourth parameter.  If the Cancel button is clicked, the <I>flag</I> parameter is set to 0, and an empty string will be returned.  The <I>flag</I> value and the length of the returned string should be checked to make sure that a correct file is selected.</P>

<P>Note that the file selected can be used as an input or an output file.  Care must be taken into consideration not to overwrite files.</P>

<H2>Operation commands</H2>

<P>
<B><SPAN class=cpp-keyword>SetIntVal</SPAN>(src val:ivc, des val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>SetStrVal</SPAN>(src str:svc, des str:svc);</B><BR> --&gt; 

<CODE>SetIntVal</CODE> assigns an integer value or integer variable to an integer variable.  <CODE>SetStrVal</CODE> assigns a constant string or a string variable to a string variable. They perform the initialization of a variable.</P>

<P><B><SPAN class=cpp-keyword>Op</SPAN>(val:ivc, opcode, val:ivc, des:iv);</B> --&gt; 

<CODE>Op</CODE> command performs operations of two integer variables.  There is no operation of string variables.  The operations include the following:</P>
<PRE>
<TABLE border=1>
  <TR><TD>X, +, Y</TD>  <TD>--></TD> <TD>X + Y</TD></TR>
  <TR><TD>X, -, Y</TD>  <TD>--></TD> <TD>X - Y</TD></TR>
  <TR><TD>X, *, Y</TD>  <TD>--></TD> <TD>X * Y</TD></TR>
  <TR><TD>X, /, Y</TD>  <TD>--></TD> <TD>X / Y</TD></TR>
  <TR><TD>X, &, Y</TD>  <TD>--></TD> <TD>X & Y</TD></TR>
  <TR><TD>X, |, Y</TD>  <TD>--></TD> <TD>X | Y</TD></TR>
  <TR><TD>X, ^, Y</TD>  <TD>--></TD> <TD>X ^ Y</TD></TR>
  <TR><TD>X, <, Y</TD>  <TD>--></TD> <TD>X < Y</TD></TR>
  <TR><TD>X, >, Y</TD>  <TD>--></TD> <TD>X > Y</TD></TR>
  <TR><TD>X, ++, Y</TD> <TD>--></TD> <TD>++ X</TD></TR>
  <TR><TD>X, --, Y</TD> <TD>--></TD> <TD>-- X</TD></TR>
  <TR><TD>X, ||, Y</TD> <TD>--></TD> <TD>X || Y</TD></TR>
  <TR><TD>X, &&, Y</TD> <TD>--></TD> <TD>X && Y</TD></TR>
  <TR><TD>X, >>, Y</TD> <TD>--></TD> <TD>X >> Y</TD></TR>
  <TR><TD>X, <<, Y</TD> <TD>--></TD> <TD>X << y</TD></TR>
  <TR><TD>X, <=, Y</TD> <TD>--></TD> <TD>X <= Y</TD></TR>
  <TR><TD>X, >=, Y</TD> <TD>--></TD> <TD>X >= Y</TD></TR>
  <TR><TD>X, ==, Y</TD> <TD>--></TD> <TD>X == Y</TD></TR>
  <TR><TD>X, !=, Y</TD> <TD>--></TD> <TD>X != Y</TD></TR>
</TABLE>
</PRE>

<P><CODE>If</CODE> and <CODE>While</CODE> use the same operations as <CODE>Op</CODE> command.</P>

<P><B><SPAN class=cpp-keyword>flOp</SPAN>(val str:svc, opcode:svc,  val str:svc, format:svc, result:sv);</B> --&gt; 

<CODE>flop</CODE> operates on two strings (the first one and the third one) that contain float point values.  The result is returned in a string variable (the fifth variable).  The format of the returned string is determined by the fourth variable.  The format can be one of %d, %i, %e, or %f.  The operation can only be + (add), - (subtract), * (multiply), / (divide), ^ (power), log. For log operaion, the second value can only be 2 (for base e) or 10 (for base 10).  For example, flop(10, log, 2, "%f", y) returns y=2.302585.</P>

<P><B><SPAN class=cpp-keyword>flFunc</SPAN>(func:svc, x:svc, y:sv);</B> --&gt; 

<CODE>FlFunc</CODE> performs float function operation. The first parameter is the name of the function, which includes sin, sinh, asin, cos, cosh, acos, exp, fabs, log, log10, sqrt, tan, atan, tanh.  The second and third parameters are the input and output variables of the function in string format.  For example:</P>

<P>The input strings can be in floating form as 3.45, or in integer from as 234, or in exponential form as 3.45e-2.  They can have comma in the string, for example 7,345.23.</P>

<P><SPAN class="code-yellow">SetStrVal(4, x); flfunc(log, x, y); ---> y=1.386294</SPAN></P>

<P>
<B><SPAN class=cpp-keyword>ParsePoint</SPAN>(str:svc, x:iv, y:iv);</B><BR>
<B><SPAN class=cpp-keyword>ParseRect</SPAN>(str:svc, left:iv, top:iv, right:iv, bottom:iv);</B><BR> --&gt; 

<CODE>ParsePoint</CODE> takes a string that contains two integer value separated by a comma, assigns those two integers to two integer variables as outputs.  <CODE>ParseRect</CODE> is the same as <CODE>ParsePoint</CODE>, but the string variable contains four integer values separated by commas, and assign those four values to four integer variables.  These two functions are mainly used with the bull's eye on the interface to get the position and the area of a window.</P>

<PRE>
<SPAN class=cpp-keyword>ParsePoint</SPAN>("11, 21", x, y);  // x=11, y=21<SPAN class=cpp-comment></SPAN>
</PRE>

<P>
<B><SPAN class=cpp-keyword>FormPoint</SPAN>(str:sv, x:ivc, y:ivc);</B><BR>
<B><SPAN class=cpp-keyword>FormRect</SPAN>(str:sv, left:ivc, top:ivc, right:ivc, bottom:ivc);</B><BR> --&gt; 
<CODE>FormPoint</CODE> and <CODE>FormRect</CODE> generate a string variable from two integer variables (point) or four integer variable (rect).</P>

<P>
<SPAN class=cpp-keyword>Rand</SPAN>(rand:iv);<BR>
<B><SPAN class=cpp-keyword>SRand</SPAN>(seed:ivc);<BR></B> --&gt; 

<CODE>SRand</CODE> sets a starting point for the subsequent <CODE>Rand</CODE> command.  If the seed to <CODE>SRand</CODE> is 0, the current time value is used as the seed.</P>

<P>
<B><SPAN class=cpp-keyword>Min</SPAN>(a:ivc, b:ivc, min:iv);</B><BR>
<B><SPAN class=cpp-keyword>Max</SPAN>(a:ivc, b:ivc, max:iv);</B><BR> --&gt; 
<CODE>Min</CODE> and <CODE>Max</CODE> return the min or max of two integer variable.</P>

<P><B><SPAN class=cpp-keyword>Mod</SPAN>(a:ivc, b:ivc, mod:iv);</B> --&gt; 
<CODE>Mod</CODE> return the remain of the division of two integer variable.</P>

<P>
<B><SPAN class=cpp-keyword>SwapInt</SPAN>(int:sv, int:sv);</B><BR>
<B><SPAN class=cpp-keyword>SwapStr</SPAN>(str:sv, str:sv);</B><BR> --&gt; 

<CODE>SwapInt</CODE> and <CODE>SwapStr</CODE> swaps the variable value.</P>
<P>
<B><SPAN class=cpp-keyword>SwapIntIf</SPAN>(expr:svc, int:sv, int:sv);</B><BR>
<B><SPAN class=cpp-keyword>SwapStrIf</SPAN>(expr:svc, str:sv, str:sv);</B><BR> --&gt; 
<CODE>SwapIntIf</CODE> and <CODE>SwapStrIf</CODE> swaps the variable value if the result of the expression is GREATER THAN 0.  In the example below, both integer and strign variables are swapped.</P>

<PRE>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(3, x);<SPAN class=cpp-keyword> SetIntVal</SPAN>(5, y);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SwapIntIf</SPAN>("lt(I(x), I(y))", x, y);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>(4, u);<SPAN class=cpp-keyword> SetStrVal</SPAN>(6, v);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SwapStrIf</SPAN>("lt(u, v)", u, v);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>
<B><SPAN class=cpp-keyword>Cal</SPAN>(expr:svc, format:svc, ret:sv);</B> --&gt; 
<CODE>Cal</CODE> performs the calculation of the expression string, puts the result in the return string with the format specified.  The expression can be any one of the operation addition (+), subtraction (-), multiplication (*), division (/), and (&), or (|).  The expression can have any number of balanced parentheses and the following functions.  The parameters of the function must be included in the balanced parentheses.</P>

<P>Note that * and / operations have higher precedence than + and -.  The operations goes from left to right.  So use parenthesis to group higher precedence operation.</P>

<P>
<B><SPAN class=cpp-keyword>CalInt</SPAN>(expr:svc, ret:sv);</B> --&gt; 
<CODE>CalInt</CODE> performs the same function as Cal command, but it stores the result in an integer variable so that the format parameter is not needed.</P>

<P>The following functions can be used in <CODE>Cal</CODE> and <CODE>CalInt</CODE> commands:</P>
<P>
<SPAN style="BACKGROUND-COLOR: #ffff00;">pow(x, y)</SPAN>: calculates the result of raising x to the power y.  For example: pow(8.0, 3) = 512.000000<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">sin(x)</SPAN>: sine of an angle of x radians. Example: sin(30*3.14159265/180)=0.5<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">asin(x)</SPAN>: principal value of the arc sine of x, expressed in radians.  Example: asin(0.5)*180.0/PI=30<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">sinh(x)</SPAN>: hyperbolic sine of x radians. d = log(5.0)=1.609438; sinh (d)= 2.4<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">cos(x)</SPAN>: cosine of an angle of x radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">acos(x)</SPAN>: principal value of the arc cosine of x, expressed in radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">cosh(x)</SPAN>: hyperbolic cosine of x radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">exp(c)</SPAN>: Returns the base-e exponential function of x, which is e raised to the power x.  exp(5)=148.413159.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">fabs(x)</SPAN>: Returns the absolute value of x<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">ln(x)</SPAN>: Returns the natural logarithm of x.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">log(x)</SPAN>: Returns the natural logarithm of x.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">sqrt(x)</SPAN>: Returns the square root of x.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">tan(x)</SPAN>: Returns the tangent of an angle of x radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">atan(x)</SPAN>: Returns the principal value of the arc tangent of x, expressed in radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">atan2(x, y)</SPAN>: Returns the principal value of the arc tangent of y/x, expressed in radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">tanh(x)</SPAN>: Returns the hyperbolic tangent of x radians.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">fmod(x, y)</SPAN>: Returns the floating-point remainder of numer/denom (rounded towards zero): fmod = numer - tquot * denom, Where tquot is the truncated (i.e., rounded towards zero) result of: numer/denom.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">remainder(x,y)</SPAN>: Returns the floating-point remainder of numer/denom (rounded to nearest)<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">ceil(x)</SPAN>: Rounds x upward, returning the smallest integral value that is not less than x.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">floor(x)</SPAN>: Rounds x downward, returning the largest integral value that is not greater than x.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">fmax(x, y)</SPAN>: Returns the larger of its arguments: either x or y.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">fmin(x, y)</SPAN>: Returns the smaller of its arguments: either x or y.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">gt(x, y)</SPAN>: Return 1 if x > y.  Otherwise, return 0.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">ge(x, y)</SPAN>: Return 1 if x >=y.  Otherwise, return 0.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">lt(x, y)</SPAN>: Return 1 if x < y.  Otherwise, return 0.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">le(x, y)</SPAN>: Return 1 if x <=y.  Otherwise, return 0.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">eq(x, y)</SPAN>: Return 1 if x = y.  Otherwise, return 0.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">round(x)</SPAN>: return the rounded integer value.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">trunc(x)</SPAN>: return the rounded integer value.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">sel(t, x, y)</SPAN>: if t is great than 0, return x, otherwise (less than or equal to 0) return y.<BR>
<SPAN style="BACKGROUND-COLOR: #ffff00;">sr(x, y)</SPAN>: right shift x by y bits.  x>>y.<BR>
</P>

<P>Note that Cal command does not do intensive error checking.  If the returned result is 0 or looks strange, the first thing to do is to check the syntax of the expression string.</P>

<P>Cal command examples:</P>

<PRE>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(6, x);<SPAN class=cpp-keyword> SetIntVal</SPAN>(12, y);<SPAN class=cpp-keyword> SetIntVal</SPAN>(-17, z);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>(33, u);<SPAN class=cpp-keyword> SetStrVal</SPAN>(43, v);<SPAN class=cpp-keyword> SetStrVal</SPAN>(11, w);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>cal</SPAN>("x+y*(z-u)*w+v+4", "%f", d);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(d, 1);         <SPAN class=cpp-comment>// -6547.000000</SPAN>
<SPAN class=cpp-keyword>cal</SPAN>("x+y*(z-u)*w+v+sin(y)+4", "%f", d);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(d, 2);  <SPAN class=cpp-comment>// -6547.536573</SPAN>
</PRE>

<P>The variables in Cal expression can be string variables, integer variable, or constant values.  When Cal performs calculation with a variable, the string variable is first searched.  If the variable name is not found in string variable, then integer variable is searched.  If the variable is not found, it is supposed to be a constant.  The constant can be in engineering format (1.2e2).  Again, the syntax is not intensively checked.  So 1.2e2.3 may result in wrong result.</P>

<P>Another thing to point out is that the expression is evaluated at the run time.  The expression is not interpreted first as other script commands.  This may poses a problem since string variable is searched first when calculation is performed. The follow example illustrates the point:</P>

<PRE>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(4, x);<SPAN class=cpp-keyword> Cal</SPAN>("x+3", "%d", x);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(x, 1);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>The result is 3.  Here is the explanation:  All three commands are interpreted first, but expression "x+3" is not.  During interpretation of the three commands, an integer variable x is created in the first command with value 3. In the second command, a <B>string variable x</B> is also created with value x (the third parameter of cal command). During execution time, the second command takes the value of the string variable x (x converted to 0), then add 3 to it.  The result is 3 and stored in string variable x.  The integer variable is never used in this case.  The conclusion is that any integer variable used in the expression should not be used as the result variable.  When a variable name is used as both string variable and integer variable, it must be careful to write the expression.  The following lines generate the correct results.</P>

<PRE>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(4, u);<SPAN class=cpp-keyword> Cal</SPAN>("u+3", "%d", y);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(y, 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>(4, x);<SPAN class=cpp-keyword> Cal</SPAN>("x+3", "%d", x);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(x, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(4, z);<SPAN class=cpp-keyword> cal</SPAN>("I(z)+3", "%d", z);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(z, 3);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>Since u is not defined in string variable, the first cal command uses the correct integer u variable.  The second command uses string variable, and the result is stored in the same string variable x.  In the third command, integer variable z is cast to float with function I(z).  Both integer variable z ans string variable z are created.</P>

<P>
<B><SPAN class=cpp-keyword>Solve</SPAN>(expr:svc, accu:svc, n:ivc, init:svc, var:svc);</B> --&gt; 

<CODE>Solve</CODE> finds the root of a non-linear equation using Newton method (x<sub>n+1</sub> = x<sub>n</sub> - f(x<sub>n</sub>) / f<sup>'</sup>(x<sub>n</sub>)).  The first parameter is the non-linear equation containing the variable to be solved.  The second variable is the accuracy of the target value.  The third parameter is the number of iterations.  The fourth variable is the initial value of the variable.  The last parameter is the variable.  For example:</P>
<PRE>
Solve("X*X-2", 1e-8, 100, -1.5, X) ---> -1.4142
Solve("X*X-2", 1e-8, 100,  1.5, X) --->  1.4142
</PRE>
<P>Note that the result may depend on the initial value.  Some result may be completely wrong.  This is due to the method.</P>

<P>Some of the internal variables can be probed to find out the status of the iteration:</P>
<OL>
<LI>TI__0_: Integer, 1 indicates the command return due to that the expression less than accuracy.</LI>
<LI>TI__1_: Integer, 1 indicates the command return due to that the difference of last two result is 0, or the derivative is 0.</LI>
<LI>TI__2_: Integer, 1 indicates the command return due to that the number of iteration is reached.</LI>
<LI>TS__0_: String, delta X to calculate the derivative.</LI>
<LI>TS__1_: String, Xn-DF(Xn)/F(Xn).</LI>
<LI>TS__3_, TS__4_: String, Two F results to calculate the derivative.</LI>
</OL>

<P>Variables may be used in the expression (string variable a):</P>
<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>(10.165, a);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Solve</SPAN>("x*x*x-a*x*x+3.993e-4", "0.000001", 1000, -10, x); (result: x=-0.00627207)<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>Iter</SPAN>(expr:svc, init:svc, var:svc, from:svc, delta:svc, to:svc);</B> --&gt; 
<CODE>Iter</CODE> iteratively calculates a equation.  The calculated result is used as the input of next iteration.  The number of iterations is determined by "<B>from</B>"-value, "<B>delta</B>" step, and the "<B>to</B>"-value. For example:</P>

<PRE>
SetStrVal("12.0", V); SetStrVal("0.2953e-3", L); SetStrVal("5.1", R);
SetStrVal("100e-9", DT); SetStrVal("50000e-9", T);
Iter("(V-I*R)/L*DT+I", 0, I, 0, DT, T); SetStrToBox(I, 4);
</PRE>

<P>In the example, I is the iterative variable.  The calculated result of "(V-I*R)/L*DT+I" is used for I value in the next iteration.  The final result of I is 1.361509e+000.</P>

<P>
<B><SPAN class=cpp-keyword>SelIntIf</SPAN>(i1:ivc, opcode, i2:ivc, sel1:ivc, Sel2:ivc, ret:iv);</B><BR>
<B><SPAN class=cpp-keyword>SelStrIf</SPAN>(i1:ivc, opcode, i2:ivc, sel1:svc, Sel2:svc, ret:sv);</B><BR> --&gt; 

Select integer or string depend on the condition.  The condition is always integer comparison.</P>

<P>
<B><SPAN class=cpp-keyword>SelIntCal</SPAN>(expr:svc, Sel2:ivc, ret:iv);</B><BR>
<B><SPAN class=cpp-keyword>SelStrCal</SPAN>(expr:svc, sel1:svc, Sel2:svc, ret:sv);</B><BR> --&gt; 
Select integer or strin depending the calculated result.  The command used for calculation is <CODE>cal</CODE>.</P>

<H2>String commands</H2>

<P>Many commands are provided to manipulate the string.  These include finding the length of a string, concatenating two strings, comparing two strings, finding if a sub-string exists in a string, and extracting part of a string.  There are also some commands that operate on a string and a character. Most of these commands are self explanatory.  Only <CODE>StrFomat</CODE> command needs some more explanation.</P>

<P><B>
<SPAN class=cpp-keyword>StrCat</SPAN>(str1:svc, str2:svc, str1+str2:sv);<BR>
<SPAN class=cpp-keyword>StrCatEl</SPAN>(str1:svc, str2:svc, str1+str2:sv);<BR>
<SPAN class=cpp-keyword>StrCatEndl</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrCatChar</SPAN>(str:svc, char:ivc, n:ivc, strchar:sv);<BR>
<SPAN class=cpp-keyword>StrCatInt</SPAN>(str1:svc, fmt:svc, val:ivc, rlt:sv);<BR>
<SPAN class=cpp-keyword>StrCatIntEl</SPAN>(str1:svc, fmt:svc, val:ivc, rlt:sv);<BR>
</B> --&gt; 
<CODE>StrCat</CODE> and <CODE>StrCatEl</CODE> concatenates string 2 to string 1, put the result in the destination string.  <CODE>StrCatEl</CODE> also puts a carriage return between string 1 and string 2. <CODE>StrCatChar</CODE> concatnates n number of character into the string.  <CODE>StrCatInt</CODE> concatnates a integer number to the string with the given format.</P>

<P>
<B><SPAN class=cpp-keyword>StrCompare</SPAN>(str1:svc, str2:svc, val:sv);<BR>
<SPAN class=cpp-keyword>StrCompareNoCase</SPAN>(str1:svc, str2:svc, val:sv);<BR></B> --&gt; 

<CODE>StrCompare</CODE> and <CODE>StrCompareNoCase</CODE> compare two string (with case sensitive or case insensitive),  returns Zero if <I>str1</I> and <I>str2</I> are identical, return < 0 if <I>str1</I> is less than <I>str2</I>, or returns > 0 if <I>str1</I> is greater than <I>str2</I>.</P>

<P>
<B><SPAN class=cpp-keyword>StrFind</SPAN>(str:svc, substr:svc, start:ivc, pos:iv);<BR>
<SPAN class=cpp-keyword>StrFindNoCase</SPAN>(str:svc, substr:svc, start:ivc, pos:iv);<BR></B> --&gt; 

<CODE>StrFind</CODE> finds the first position of the substring <I>substr</I> in the source string starting from position <I>start</I> of the source string.  <CODE>StrFindNoCase</CODE> finds a substring without case-sensitivity.  If the sub-string is not in the string, -1 is returned.</P>

<P>
<B><SPAN class=cpp-keyword>StrFindChar</SPAN>(str:svc, substr:svc, start:ivc, pos:iv)</B> --&gt; 
<CODE>StrFindChar</CODE> finds any of characters in substr that appears in str just after start.  For example:</P>
<PRE>StrFindChar("Open the html", "et", 3, rlt);  ---&GT; 5 char t</PRE>

<P><B><SPAN class=cpp-keyword>StrRevFind</SPAN>(str:svc, substr:svc, start:ivc, des:iv);</B> --&gt; 

<CODE>StrRevFind</CODE> is almost the same as <CODE>StrFind</CODE> except that it finds the first position of the substring <I>substr</I> in the source string starting from position <I>start</I> in reverse direction.  Parameter <I>start</I> can be -1.  In this case, the software automatically sets <I>start</I> to the end of the source string.</P>


<P><B><SPAN class=cpp-keyword>StrReverseFind</SPAN>(src:svc, char:ivc, pos:iv);</B> --&gt; 

<CODE>StrReverseFind</CODE> finds the first position of a <B>character</B> in the source string starting from the end of the source string.</P>

<P>
<B><SPAN class=cpp-keyword>StrMid</SPAN>(src:svc, start:ivc, nchar:ivc, des:sv);<BR>
<SPAN class=cpp-keyword>StrMidPos</SPAN>(src:svc, start:ivc, end:ivc, des:sv);<BR>
<SPAN class=cpp-keyword>StrLeft</SPAN>(src:svc, nchar:ivc, des:sv);<BR>
<SPAN class=cpp-keyword>StrRight</SPAN>(src:svc, nchar:ivc, des:sv);<BR>
<SPAN class=cpp-keyword>StrRightPos</SPAN>(src:svc, start:ivc, des:sv);<BR></B> --&gt; 

<CODE>StrLeft</CODE>, <CODE>StrMid</CODE>, and <CODE>StrRight</CODE> return a part of the source string at a certain location with a given length. <CODE>StrLeft</CODE> starts from the beginning of the source string, <CODE>StrMid</CODE> starts at the locations given, and <CODE>StrRight</CODE> starts from the end of the string.</P>

<P>The length parameter can also be a negative number.  In this case, the string returned starts at the opposite direction.  StrLeft returns the sub-string from beginning to the length from the end of the string.  StrRight returns sub-string from the right to the length from the beginning.  StrMid returns the sub-string from the location given to the length from the location at the right.</P>

<P>Here are some examples:</P>
<PRE>
StrLeft("0123456789", 4, s): 0123
StrLeft("0123456789", -2, s): 01234567, all except the last two chars
StrRight("0123456789", 2, s): 89
StrRight("0123456789", -2, s): 23456789, all except the first two chars
StrMid("0123456789", 5, 2, s): 56
StrMid("0123456789", 5, -2, s): 45, both contain the char 5
</PRE>

<P><CODE>StrMidPos</CODE> and <CODE>StrRightPos</CODE> return a part of the the source string between two positions.</P>

<P><B><SPAN class=cpp-keyword>StrFormat</SPAN>(des:sv, format:svc, val:ivc);</B> --&gt; 

<CODE>StrFormat</CODE> takes a string as its first parameter.  This is the result string and this makes <CODE>StrFormat</CODE> one of the commands that use the first parameter as the output. The second parameter is a format string that indicates if the third parameter is changed to hex or decimal string. The format string can also have some text inside.  The third parameter is an integer constant or variable. Note that this command only formats <B>one integer</B> variable.</P>

<P><B><SPAN class=cpp-keyword>StrFormatForPrint</SPAN>(str:svc, bnd:svc, len:ivc, rlt:sv);");</B> --&gt; 

<CODE>StrFormatForPrint</CODE> formats a long line into short lines.  The length of the formated line is determined by the third parameter len.  Sometimes a boundary is required, for example, it is desired not to split a word into two lines.  The second parameter bnd can be used for this purpose.  In this case, it will be a space.</P>

<P><B><SPAN class=cpp-keyword>StrFormatStr</SPAN>(des:sv, format:svc, val:svc);</B> --&gt; 
<CODE>StrFormatStr</CODE> takes a string as its third parameter.  The format should always use %s.  For example:</P>
<PRE>
<SPAN class=cpp-keyword>StrFormatStr</SPAN>(msg, "Do you want to delete all files with extension .%s?", ext);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>The format variable of both <CODE>StrFormat</CODE> and <CODE>StrFormatStr</CODE> accepts \t and \n for TAB and RETURN.</P>

<P><B><SPAN class=cpp-keyword>StrLength</SPAN>(src:svc, length:iv);</B> --&gt; 
<CODE>StrLength</CODE> returns the length of the string.</P>

<P><B><SPAN class=cpp-keyword>StrMaxLineLength</SPAN>(src:svc, max_length:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrMinLineLength</SPAN>(src:svc, max_length:iv);</B><BR> --&gt; 
A string may contains many lines. <CODE>StrMaxLineLength</CODE> (<CODE>StrMinLineLength</CODE>) returns the maximum (minimum) length of all lines in the string.</P>

<P>
<B><SPAN class=cpp-keyword>StrGetAt</SPAN>(str:svc, pos:ivc, char:iv);<BR>
<SPAN class=cpp-keyword>StrSetAt</SPAN>(str:svc, pos:ivc, result:iv);<BR></B> --&gt; 
<CODE>StrGetAt</CODE> and <CODE>StrSetAt</CODE> gets or set the character at the certain position.  The position value can be a negative number.  -1 is the last character.  -2 is the next to the last character.  If value is larger than the length of the string, the value is limited to 0 or the length of the string.</P>

<P><B><SPAN class=cpp-keyword>StrIsChar</SPAN>(str:svc, pos:ivc, char:ivc, char:ivc);</B> --&gt; 
<CODE>StrIsChar</CODE> checks if the nth character in the string is the character in the third parameter.  Return value is the character value in the string minus the value of the character.  If the two characters are the same, the return value is 0.</P>

<P><B><SPAN class=cpp-keyword>StrUpper</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrLower</SPAN>(src:svc, des:sv);<BR></B> --&gt; 
<CODE>StrUpper</CODE> and <CODE>StrLower</CODE> converts the string to upper or lower case.</P>


<P><B><SPAN class=cpp-keyword>StrTrim</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrTrimLeft</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrTrimRight</SPAN>(src:svc, des:sv);<BR></B> --&gt; 

<CODE>StrTrim</CODE> removes white spaces at both the beginning and the end of the string, while <CODE>StrTrimLeft</CODE> and <CODE>StrTrimRight</CODE> remove only white spaces at the beginning or end of the string, respectively.</P>


<P><B><SPAN class=cpp-keyword>StrTrimChar</SPAN>(src:svc, TrimStr:svc, des:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrTrimLeftChar</SPAN>(src:svc, TrimStr:svc, des:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrTrimRightChar</SPAN>(src:svc, TrimStr:svc, des:sv);</B><BR> --&gt; 

<CODE>StrTrimChar, StrTrimLeftChar, StrTrimRightChar</CODE> have the similiar functionalities except that some particular characters can be trimmed instead of only white spaces.  Note that the TrimStr can be a string.  For example "StrTrimChar("XX$TEST$XX", "XX", s);" will removed the "XX" at the beginnign and the end.</P>

<P>
<B><SPAN class=cpp-keyword>StrToDec</SPAN>(src:svc, des:iv);<BR>
<SPAN class=cpp-keyword>StrToHex</SPAN>(src:svc, des:iv);<BR></B> --&gt; 

<CODE>StrToDec</CODE> and <CODE>StrToHex</CODE> convert a string containing decimal digits and hex-decimal digits to an integer value. With <CODE>StrToDec</CODE>, the string can be floating point string, for example, 1234.567e1 is converted to decimal value 12346.  However, string 0x23a is converted to decimal value 0.  The value converted is the rounded value.  0.5 will be converted to 1.  -0.5 will converted to -1.</P>


<P><B><SPAN class=cpp-keyword>StrGetLine</SPAN>(str:svc, pos:ivc, endpos:iv, line:sv);</B> --&gt; 

<CODE>StrGetLine</CODE> returns a line from a multiline string separated by \r (0x0d) and/or \n (0x0a).  It returns the text between \r (0x0d) and/or \n (0x0a).  \r and/or \n are skipped.  The function returns an empty line if it sees \r\n\r\n. The input is normally obtained from the clipboard.  This function can be repeatedly used to get all lines in a text:</P>

<PRE>
GetFromClipBoard(text);
StrLength(text, end);
If(end, &lt;=, 1) EndProgram(); EndIf();

While(0, cnt, &lt;, end, 0)
  StrGetLine(text, cnt, cnt, lineread);
  // Do something to lineread
Wend();
</PRE>

<P><B><SPAN class=cpp-keyword>StrReplace</SPAN>(src:svc, sub:svc, rep:svc, pos:ivc, str:sv);</B> --&gt; 

<CODE>StrReplace</CODE> replaces a substring (second parameter) in the source string (first parameter) with another string (the third parameter) after a certain location (the fourth parameter) only once.  Any matched string before the location will not be replaced.</P>  


<P><B><SPAN class=cpp-keyword>StrReplaceAll</SPAN>(src:svc, sub:svc, rep:svc, str:sv);</B> --&gt; 
<CODE>StrReplaceAll</CODE> replaces all substrings in the source string with another string.</P>


<P><B><SPAN class=cpp-keyword>StrReplaceChar</SPAN>(src:svc, sub:svc, rep:svc, pos:ivc, str:sv);</B> --&gt; 

<CODE>StrReplaceChar</CODE> replaces any character in the source string (first parameter) that matches the character in the second string (second parameter) with a string in the third parameter beginning at a certain location (the fourth parameter).  It just replaces the first matched character once after the start position.  Example:</P>
<PRE>
StrReplaceChar("This $ and % or & and test", "%&d$", "*#", 0, x); // x="This *# and % or & and test"
</PRE>
<P>Only the $ is replaced with *#.  %, &, and d will not be replaced because they are after $.</P>


<P><B><SPAN class=cpp-keyword>StrReplaceCharAll</SPAN>(src:svc, sub:svc, rep:svc, str:sv);</B> --&gt; 

<CODE>StrReplaceCharAll</CODE> replaces all characters in the source string (first parameter) that match the character (second parameter) with another string (the third parameter).  For example:</P>
<PRE>
StrReplaceCharAll("This $ and % or & and test", "$%&d", "*#", str); // x="This *# an*# *# or *# an*# test"
</PRE>
<P>will convert all character $, %, &, or d in the first string to *#, then store the result into variable x.</P>

<P>To replace special characters, the following command can be used.  The two commands replace all TABs with spaces.</P>
<PRE>
  StrCatChar("", '\t', 1, strtab);
  StrReplaceCharAll(str, strtab, " ", str);
</PRE>

<P><B><SPAN class=cpp-keyword>StrInsertAt</SPAN>(src:svc, sub:svc, pos:ivc, str:sv);</B> --&gt; 

<CODE>StrInsertAt</CODE> inserts a string (the second parameter) into the source string (the first parameter) at a certain location (the third parameter).</P>

<P><B><SPAN class=cpp-keyword>StrInsertCharAt</SPAN>(src:svc, char:ivc, n:ivc, pos:ivc, str:sv);</B> --&gt; 

<CODE>StrInsertCharAt</CODE> inserts a character (the second parameter) n (third parameter) times into the source string (the first parameter) at a certain location (the fourth parameter).</P>

<P><B><SPAN class=cpp-keyword>StrRemoveRepeat</SPAN>(src str:svc, char:ivc, des str:sv);</B> --&gt; 

<CODE>StrRemoveRepeat</CODE> removes the repeated characters (not the first one) in a string.</P>

<P><B><SPAN class=cpp-keyword>StrRemoveBetween</SPAN>(src str:svc, n1:ivc, n2:ivc, des str:sv);</B> --&gt; 

<CODE>StrRemoveBetween</CODE> removes characters between <I>n1</I> and <I>n2</I>.</P>

<P><B><SPAN class=cpp-keyword>StrReplaceBetweenStr</SPAN>(str:svc, s1:svc, s2:svc, rep:svc, flag:ivc, pos:ivc, rtn:sv);</B> --&gt; 

<CODE>StrReplaceBetweenStr</CODE> replaces string between <I>s1</I> and <I>s2</I> with the string <I>rep</I>, starting from <I>pos</I> with some <I>flags</I>.  <I>s1</I> and <I>s2</I> are strings.  The new character index after <I>s2</I> is returned in <I>pos</I>, and resulting string in in <I>rtn</I>.  The <I>flag</I> has the following meanings:</P>

<P>Bit0=0: <I>s1</I> and <I>s2</I> are also replaced.  Bit0=1: <I>s1</I> and <I>s2</I> are not replaced. For example:</P>

<PRE>
StrReplaceBetweenStr("T&lt;P&gt;ES&lt;/P&gt;T", "&lt;P&gt;", "&lt;/P&gt;", "$$", 0, 0, t);-->T$$T
StrReplaceBetweenStr("T&lt;P&gt;ES&lt;/P&gt;T", "&lt;P&gt;", "&lt;/P&gt;", "$$", 1, 0, t);-->T&lt;P&gt;$$&lt;/P&gt;T
</PRE>

<P>Bit1=0: <I>s1</I> and <I>s2</I> are case insenstive.  Bit1=1: <I>s1</I> and <I>s2</I> are case sensitive. For example:</P>

<PRE>
StrReplaceBetweenStr("T&lt;b&gt;ES&lt;/B&gt;T", "&lt;B&gt;", "&lt;/B&gt;", "$$", 0, 0, t);-->T$$T
StrReplaceBetweenStr("T&lt;b&gt;ES&lt;/B&gt;T", "&lt;B&gt;", "&lt;/B&gt;", "$$", 2, 0, t);-->T&lt;b&gt;ES&lt;/B&gt;T
StrReplaceBetweenStr("T&lt;B&gt;ES&lt;/B&gt;T", "&lt;b&gt;", "&lt;/B&gt;", "$$", 2, 0, t);-->T&lt;B&gt;ES&lt;/B&gt;T
</PRE>

<P>The rest of the bits of <I>flag</I> determines how many occurances of matchs to be replaced.  If the value is 0, all occurances will be replaced.  If the value is 1, only the first occurance is replaced.  If the value is 2, the first two occurances are replaced, etc.</P>

<P><B><SPAN class=cpp-keyword>StrFillChar</SPAN>(src str:svc, char:ivc, num:ivc, des str:sv);</B> --&gt; 

<CODE>StrFillChar</CODE> fills the source string with a character to a length specified by the third parameter.  StrFillChar("XY", '$', 5, x); ----> "XY$$$"</P>

<P><B><SPAN class=cpp-keyword>StrRemoveEmptyLine</SPAN>(src str:svc, lineleft:ivc, des str:sv);</B> --&gt; 

<CODE>StrRemoveEmptyLine</CODE> removes any extra empty line more than the second parameter.  For example, if the second parameter is 0, all line separators (0xd, 0xa) are removed.  The result is that there is only one line.  If the second parameter is 1, any empty line more than 1 will be removed.  The result is that there is no empty line.  If the second parameter is 2, there is at most one empty line.</P>

<P><B><SPAN class=cpp-keyword>StrInsertEmptyLine</SPAN>(src str:svc, lineleft:ivc, des str:sv);</B> --&gt; 

<CODE>StrInsertEmptyLine</CODE> inserts any extra empty line by the pearmeter "linekept" if necessary.  For example, if the second parameter linekept is 1, there is will be one empty line between two non-empty lines.  If the parameter is 0, there is no empty line between two non-empty lines.</P>

<P><B><SPAN class=cpp-keyword>StrToEnd</SPAN>(src:svc, start:ivc, nchar_toend:ivc, ret_str:sv);</B> --&gt; 

<CODE>StrToEnd</CODE> returns the sub-string from the starting position to the end of the string minus the number of characters specified in the third parameter.  For example:</P>
<PRE>
StrToEnd("1234567890123456789", 4, 0, x);    x="567890123456789"
StrToEnd("1234567890123456789", 4, 2, x);    x="5678901234567"
StrToEnd("1234567890123456789", 4, 200, x);  x="1234"
StrToEnd("1234567890123456789", 4, 17, x);   x="34"
</PRE>
<P>In the third example, the length of the string is only 19, 200 is larger than 19, so the result string starts at 0.  It starts at 2 in the fourth example, since 19-17=2.</P>

<P><B><SPAN class=cpp-keyword>StrToken</SPAN>(str:svc, token_str:svc, start:ivc, ret_pos:iv, ret_token:iv, ret_str:sv);</B> --&gt; 

<CODE>StrToken</CODE>: From the starting position, find the first character in string that is in the token string.  Returns the position after this first character in string, the token character, and the sub-string from the start position to the token, not including the token.  For example:</P>
<PRE>
StrToken("1234567890123456789", "98765", 8, x, y, z)   --> x=9,  y=0x39, z=""
StrToken("1234567890123456789", "8765", 8, x, y, z);   --> x=15, y=0x35, z="901234"
StrToken("1234567890123x456789", "876x5", 8, x, y, z); --> x=14, y=0x78, z="90123"
</PRE>

<P>In the above examples, all searches starts from character '9' (0 based, end of "8").  In the first example, '9' in the string is first character in the token string matched.  So the return position x is 9, the character that matched is y=0x39 ('9').  The string from the start position to matched position is empty.  In the second case, the first matched character after "8" is '5', and the position of '5' after position 8 is 15 (x=15).  The string between start and match is "901234".</P>

<P><B><SPAN class=cpp-keyword>StrDoubleQuote</SPAN>(src:svc, quote:svc, des:sv");</B> --&gt; 

<CODE>StrDoubleQuote</CODE> adds double "quote" to the begin and the end of the sting.  If "quote" is empty, double quote is added, otherwise the text is added.</P> 

<P><B><SPAN class=cpp-keyword>StrEnclose</SPAN>(src:svc, before:svc, after:svc, des:sv");</B> --&gt; 
<CODE>StrEnclose</CODE> encloses the source string in other two strings ("before" and "after").</P> 

<P><B><SPAN class=cpp-keyword>StrGetBetween</SPAN>(src:svc, str1:svc, str2:svc, start:ivc, end:iv, des:sv);</B> --&gt; 

<CODE>StrGetBetween</CODE> returns the string between "str1" and "str2" of the source string "src", and stores the result in the destination string "des".  The search starts at position in variable "<I>start</I>".  The position at the end of variable "str2" is returned in variable end if both strings are found after the position in <I>start</I> variable.  If either of variables "str1" and "str2" is not found, the value in variable <I>end</I> is -1.  This can be used to determine if the search is successful.  In the following example, n is 8, des="56", and t="90".</P> 

<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("1234567890", infn);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetIntVal</SPAN>(0, m);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrGetBetween</SPAN>(infn, "34", "78", m, n, des);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrToBox</SPAN>(des, 4);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(m, 1);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(n, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrRightPos</SPAN>(infn, n, t);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(t, 5)<SPAN class=cpp-comment></SPAN>
</PRE>

<P>des="56", m=0, n=8, t="90".  This command can be repeatedly called to find all the strings between two strings.</P>

<P><B><SPAN class=cpp-keyword>SubStrCount</SPAN>(str:svc, substr:svc, count:iv);</B><BR>
<B><SPAN class=cpp-keyword>SubStrCountNoCase</SPAN>(str:svc, substr:svc, count:iv);</B><BR>
--&gt; Count the number of sub-string in the string with case sensitive or case insensitive.</P>

<P>
<B><SPAN class=cpp-keyword>OpenTag</SPAN>(str:svc, substr:svc, start:ivc, des1:iv, des2:iv);<BR>
<SPAN class=cpp-keyword>CloseTag</SPAN>(str:svc, substr:svc, start:ivc, des1:iv, des2:iv);<BR> --&gt; 
</B>

<CODE>OpenTag</CODE> finds all open tags in string (case insensitive).  It returns two integer values marking the start position and the end position of the first tag after the start position.</P>

<P><CODE>CloseTag</CODE> find the close tags (case insensitive).  It returns two integer values marking the start position and the end position of the first tag after the start position.</P>

<P><B><SPAN class=cpp-keyword>OpenCloseTag</SPAN>(str:svc, substr:svc, start:ivc, des1:iv, des2:iv);
</B> --&gt; 
<CODE>OpenCloseTag</CODE> finds beginning position of open tag and the end position of the close tags after the start position.  The tag can be nested, for example, &lt;div 1&gt;...&lt;div 2&gt...&lt;/div 2&gt;...&lt;/div 1&gt;.  In this case, the return values are beginning position of &ltdiv 1&gt; and the end position of &lt/div 1&gt;.  If the string contains no open tag and close tag, or the string contains only close tag, the return values are both -1.  </P>

<P><B><SPAN class=cpp-keyword>OpenTagInfo</SPAN>(str:svc, tag:svc, strstk:sv, startstk:sv, endstk:sv);<BR>
<SPAN class=cpp-keyword>CloseTagInfo</SPAN>(str:svc, tag:svc, strstk:sv, startstk:sv, endstk:sv);</B><BR> --&gt; 
<CODE>OpenTagInfo</CODE> finds all open tags.  It returns one string stack and two integer stacks.  The first stack is a string stack containing the open tag string.  The other two integer stacks are the start and end of the tag position.</P>

<P><CODE>CloseTagInfo</CODE> finds all close tags.  It returns one string stack two integer stacks.  The first stack is a string stack containing the close tag string.  All close tag are the same so that the string stack contains the same string.  The other two integer stacks are the start and end of the tag position.</P>

<P><B><SPAN class=cpp-keyword>OpenTagContain</SPAN>(str:svc, tag:svc, contain:svc, start:ivc, des1:iv, des2:iv);</B>--&gt; 
<CODE>OpenTagContain</CODE> finds an open tag that contains a certain string, starting from a postion.  The return values are the tags start and close positions.</P>

<P><B><SPAN class=cpp-keyword>TagInfo</SPAN>(str:svc, tag:svc, seqstk:sv, startstk:sv, endstk:sv);</B> --&gt; 

<CODE>TagInfo</CODE> finds both open and close tags.  It returns three integer stacks.  The first stack is the open and the close tag sequence.  The open tag increases the number, the close tag decreases the number.  The other two integer stacks are the start and end of the tag position.  The following example finds all DIV tags that contains the string "block-inject block-inject-1" in a file with start and end position:</P>
<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("div", tag)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("block-inject block-inject-1", class);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>//StrDoubleQuote(class, class);</SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>ReadAll</SPAN>(infn, enc, text);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>TagInfo</SPAN>(text, tag, seq, start, end)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(seq, cnt);<SPAN class=cpp-keyword> SetIntVal</SPAN>(0, flag);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>While</SPAN>(0, k, &lt;, cnt, 1)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  IntStackGetAt</SPAN>(seq, k, l);<SPAN class=cpp-keyword> IntStackGetAt</SPAN>(start, k, n);<SPAN class=cpp-keyword> IntStackGetAt</SPAN>(end, k, m);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  if</SPAN>(flag, ==, 0)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>    StrMidPos</SPAN>(text, n, m, s);<SPAN class=cpp-keyword> StrFind</SPAN>(s, class, 0, nn);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>    if</SPAN>(nn, !=, -1)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>      op</SPAN>(l, -, 1, cs);<SPAN class=cpp-keyword> SetIntVal</SPAN>(n, cstk);<SPAN class=cpp-keyword> SetIntVal</SPAN>(1, flag);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>    Endif</SPAN>();<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  Else</SPAN>();<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>    BreakIf</SPAN>(l, ==, cs);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  EndIf</SPAN>()<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Wend</SPAN>()<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrMidPos</SPAN>(text, cstk, m, t);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SendToClipboard</SPAN>(t)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>EndProgram</SPAN>()<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>TagClass</SPAN>(str:svc, tag:svc, class:svc, start stk:sv, end stk:sv);
</B> --&gt; 

<CODE>TagClass</CODE> finds the open and close tags that contains a specified sub string.  The "class" string is any string only in the open tag, not between the open and close tag.  The "start" and "end integer stacks are not cleared so that it is better to clear these two variables before call this function.  In the following example, INS tags containing "adsbygoogle " are removed.  Any other INS tags that do not contain "adsbygoogle " are not removed.  Note that pop command is used to get the position from the stack.  This insures that the tags close to the end of the file are removed first so that the positions at the beginning of the string keep unchanged.</P>

<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("ins", tag)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("adsbygoogle ", class);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>ReadAll</SPAN>(infn, enc, text);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>TagClass</SPAN>(text, tag, class, start, end);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(start, cnt);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(cnt, 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>while</SPAN>(0, k, &lt;, cnt, 1)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  IntStackPop</SPAN>(start, x);<SPAN class=cpp-keyword> IntStackPop</SPAN>(end, y);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  StrRemoveBetween</SPAN>(text, x, y, text);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Wend</SPAN>();<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>WriteAll</SPAN>(text, outfn, enc, 0);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>EndProgram</SPAN>()<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>TagClassHier</SPAN>(str:svc, tag:svc, class:svc, start stk:sv, end stk:sv);</B> --&gt; 
<CODE>TagClassHier</CODE> find the tag hierarchy.
</P>

<P><B><SPAN class=cpp-keyword>RemoveTag</SPAN>(str:svc, tag:svc, class:svc, rlt:sv);</B> &nbsp;--&gt; <CODE>RemoveTag</CODE> Removes all the spicified tags in a string.  class is a string contained in the tag.</P>

<P><B><SPAN class=cpp-keyword>ExtractTag</SPAN>(str:svc, tag:svc, class:svc, rlt:sv);</B> &nbsp;--&gt; 
<CODE>ExtractTag</CODE> extracts all the spicified tags in a string.  class is a string contained in the tag.</P>

<PRE>
<SPAN class=cpp-keyword>RemoveTag</SPAN>(all, "script", "", all);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>ExtractTag</SPAN>(all, "ul", "primary-menu", all);<SPAN class=cpp-comment></SPAN>
</PRE>
<P>The first line removes all SCRIPT tags.  The second line extracts UL tags containing "primary-menu".</P>

<P><B><SPAN class=cpp-keyword>ExtractImg</SPAN>(str:svc, class:svc, desstk:iv);</B>  &nbsp;--&gt;&nbsp; Extract all the image link in the string. </P>

<PRE>
<SPAN class=cpp-keyword>ExtractImg</SPAN>(str, "", img_stk);<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>HtmlTag</SPAN>(src:svc, tag:svc, class:svc, des:sv);</B> &nbsp;--&gt; <CODE>
HtmlTag</CODE> creates an html tag.</P>

<P><B><SPAN class=cpp-keyword>StrContainStkAnd</SPAN>(str:svc, substr stk:sv, exist:iv);</B> &nbsp;--&gt; <CODE>StrContainAnd</CODE> finds whether multiple sub-strings are in a string.  The sub-strings are specified by a string stack.  If there is more than one sub-strings in the string stack, all sub-strings must be in the string.  The return value is -1 if any of the sub-string is not in the string.  If all sub-string is in the string, the return value is the number of strings. Example:</P>

<PRE>
<SPAN class=cpp-keyword>StrStackPush</SPAN>(ss, "text");<SPAN class=cpp-keyword> StrStackPush</SPAN>(ss, "text3");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("This is text1 and text2 and text3", s);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrContainAnd</SPAN>(s, ss, x);<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>StrContainStkAndNoCase</SPAN>(str:svc, substr stk:sv, exist:iv);</B> &nbsp;--&gt; The case insenstive version of <CODE>StrContainAnd</CODE></P>


<P><B><SPAN class=cpp-keyword>StrContainStkOr</SPAN>(str:svc, substr stk:sv, exist:iv);</B> &nbsp;--&gt; <CODE>StrContainOr</CODE> is similar to <CODE>StrContainAnd</CODE>.  It returns a positive number if any of the sub-strings (all of the sub-string) is in a string.  The number is the index of the sub-string.  The return value is -1 if none of the sub-strings is in the string. For example, if the sub-string are "TEST0", "TEST1", ....  If TEST1 is in the string while TEST0 is not, the return value 1.</P>

<P><B><SPAN class=cpp-keyword>StrContainStkOrNoCase</SPAN>(str:svc, substr stk:sv, exist:iv);</B> &nbsp;--&gt; The case insenstive version of <CODE>StrContainOr</CODE></P>

<P><B><SPAN class=cpp-keyword>StrContainStrAnd(str:svc, find:svc, sep:svc, start:ivc, flag:ivc, return:iv);</B> &nbsp;--&gt; 
<CODE>StrContainStrAnd</CODE> finds whether multiple substrings (second variable) are in a string (first variable).  The multiple substrings are in a string seperated by a seperator (third variable).  The search starts at a certain character (fourth variable).  A flag indicates differnt search methods: bit0=0: case sensitive; bit0=1: case insensitive; bit1=0: no sequence of the substring; bit1=1: follow the sequence of the substrings.  The return value is -1 if any of the substrings is not in the string.  If all the substrings is in the string, the return value depends on the bit2 of the flag.  If the flag is 0, the index of the closest substring is returned.  If the bit is one, the index of the farthest is returned.</P>
<PRE>
StrContainStrAnd("Return(); SetStrToBox(str, 1);", "tur#str", "#", 0, 0, x); SetDecToBox(x, 1); // x=2
StrContainStrAnd("Return(); SetStrToBox(str, 1);", "tur#str", "#", 0, 4, x); SetDecToBox(x, 1); // x=22
StrContainStrAnd("Return(); SetStrToBox(str, 1);", "str#tur", "#", 0, 5, x); SetDecToBox(x, 1); // x=13
StrContainStrAnd("Return(); SetStrToBox(str, 1);", "str#tur", "#", 0, 3, x); SetDecToBox(x, 1); // x=-1
</PRE>

<P><B><SPAN class=cpp-keyword>StrContainStrOr(str:svc, find:svc, sep:svc, start:ivc, flag:ivc, return:iv);</B> &nbsp;--&gt; 
<CODE>StrContainStrOr</CODE> is almost the same as <CODE>StrContainStrAnd</CODE> except that the return value is -1 if non of the substrings is in the string.  If any of the sunstrings is in the string, the return value is non-zero.</P>

<P><B><SPAN class=cpp-keyword>StrMapLine</SPAN>(str:svc, pos stk:sv, line stk:iv, cnt stk:iv);</B> &nbsp;--&gt; <CODE>StrMapLine</CODE> maps the character position to the line number and the character position on the line.  str contains the text with line return character 0xd and 0xa.  pos stk is integer stack containing the position to be mapped.  The value in this stack should be arranged in ascending order.  line stk and cnt stk return the line number and the character position on this line.  Line count (line) is 1 based.  Character position (cnt) is zero based.  The following script illustrates the use of this command:</P>

<PRE>
<SPAN class=cpp-keyword>StrCatEl</SPAN>("", "01234567890123", s);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrCatEl</SPAN>(s, "another_line2", s);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrCatEl</SPAN>(s, "the_thirdline3", s);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 4);<SPAN class=cpp-keyword> IntStackPush</SPAN>(x, 14);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrMapLine</SPAN>(s, x, l, c);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(l, 0, t);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(t, 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(c, 0, t);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(t, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(l, 1, t);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(t, 3);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(c, 1, t);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(t, 4);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>There are three lines in the string.  The first line has 14 characters, plus two characters 0xd and 0xa.  The second position to map is 14.  The mapped result is line 1 and character 14.  If the value is increased to 15, the result is 1 and 16.  If the value is increased again to 16, the result is 2 and 0.  The value 31 maps to 3 and 0.</P>

<P>See also dbStrMapLine.txt</P>

<P><B><SPAN class=cpp-keyword>ForEachStrLine</SPAN>(str, line_idx0:ivc, line_idx:iv, char_idx0:ivc, char_idx:iv, rtn:sv); <SPAN class=cpp-keyword>ForEachStrLineEnd</SPAN></B> &nbsp;--&gt; These two commands forms a loop.  In each pass of the loop, the line index, character index, and the line of string are returned.  line_idx and char_idx start at line_idx0.  At the end of the loop idx value is -1.  <code>If</code>, <code>break</code>, <code>continue</code>, <code>while</code> loop, or even <code>ForEachStrLine</code> loop commands can be used in the loop.</P>

<P><B><SPAN class=cpp-keyword>ForEachStrchar</SPAN>(str, char_idx0:ivc, char_idx:iv, rtn:iv); <SPAN class=cpp-keyword>ForEachStrCharEnd</SPAN></B> &nbsp;--&gt; These two commands forms a loop.  In each pass of the loop, character index, and the character are returned.  char_idx starts at 0.  At the end of the loop idx value is -1.  <code>If</code>, <code>break</code>, <code>continue</code>, <code>while</code> loop, or even <code>ForEachStrChar</code> loop commands can be used in the loop.</P>

<P><B><SPAN class=cpp-keyword>StrFirstWord</SPAN>(str:svc, substr:svc, firstword:sv);</B> &nbsp;--&gt; <code>StrFirstWord</code> returns a sub-string of str, starting from the beginning, until any character in surstring.  For example:</P>
<PRE>
<SPAN class=cpp-keyword>StrFirstWord</SPAN>("no matching symbolic information found", "id", s)<SPAN class=cpp-comment></SPAN>
</PRE>
<P>The returned sub-string is "no match", since after this is the character 'i', which in substr.</P>

<P><B><SPAN class=cpp-keyword>StrFirstWordSkip</SPAN>(str:svc, substr:svc, firstword:sv, remstr:sv);</B> &nbsp;--&gt; <code>StrFirstWordSkip</code> returns two sub-strings of str.  The first sub-string starts from the beginning, ends until any character in surstring.  The second sub-string starts from a character that is in substr, ends at the end of str.  For example:</P>
<PRE>
<SPAN class=cpp-keyword>StrFirstWordSkip</SPAN>("no matching symbolic information found", "lc", s, t)<SPAN class=cpp-comment></SPAN>
</PRE>

<P>The first returned sub-string is "no mat", since after this is the character 'c', which in substr.  The second returned sub-string is "hing symbolic information found".</P>

<P><B><SPAN class=cpp-keyword>StrValStr</SPAN>(src:svc, sep:svc, str:sv);</B> &nbsp;--&gt; <code>StrValStr</code> converts a hex or dec string into values and stores the value in output string.  Hex string must start with 0x. Hex and dec string can be mixed. For example:</P>

<PRE>
<SPAN class=cpp-keyword>StrValStr</SPAN>("0x8f6c 36807 0x4e86 0x5934 0x53bb", " ", s);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(s, 4)<SPAN class=cpp-comment></SPAN>
</PRE>

<P>After execution of above lines, Box 4 will contain chinese characters "转过了头去".  In the above example, the seperator is a space.  The seperator can be STR_DA if the string contains one value per line.</P>

<H2>Miscllanous commands</H2>

<P><B><SPAN class=cpp-keyword>Delay</SPAN>(ms:ivc);</B> &nbsp;--&gt; <CODE>Delay</CODE> command delays ivc ms before the execution of the next command in the script file.</P>

<P><B><SPAN class=cpp-keyword>GetDate</SPAN>(year, month, weekday, day, hour, minue, second, ms);</B> &nbsp;--&gt; <CODE>GetDate</CODE> returns the current system time in integer variables year, month, weekday, day, hour, minue, second, and ms.</P>

<P><B><SPAN class=cpp-keyword>GetTime</SPAN>(th:iv, tl:iv);</B> &nbsp;--&gt; <CODE>GetTime</CODE> returns the current system time in two integer values th and tl.</P>

<P><B><SPAN class=cpp-keyword>DayOfWeek</SPAN>(str:mm/dd/yyyy, weekday:iv);</B> &nbsp;--&gt; <CODE>DayOfWeek</CODE> takes a string containing the date in format mm/dd/yyyy, returns the day of week in an integer.  Return value 0 is Sunday.</P>

<P><B><SPAN class=cpp-keyword>Time2Date</SPAN>(th:ivc, tl:ivc, stk:sv);</B> &nbsp;--&gt; <CODE>Time2Date</CODE> converts time in th and tl to date format stored in an integer stack.  The contents of the integer stack: 0: Year, 1: Month, 2: DayOfWeek (Sunday: 0, Monday 1, ...), 3: Day, 4: Hour, 5: Minute, 6: Second, 7: Milliseconds.</P>

<P><B><SPAN class=cpp-keyword>Date2Time</SPAN>(stk:sv, th:ivc, tl:ivc);</B> &nbsp;--&gt; <CODE>Date2Time</CODE> converts the date to time.</P>

<P><B><SPAN class=cpp-keyword>TimeCompare</SPAN>(th1:ivc, tl1:ivc, th2:ivc, tl2:ivc, rlt:iv);</B> &nbsp;--&gt; 
<CODE>TimeCompare</CODE> compares two time values th1:tl1 and th2:tl2.  If th1:tl1 is equal to th2:tl2, the return value rlt is 0.  If th1:tl1 is less than th2:tl2, the return value rlt is -1.  If th1:tl1 is greater than th2:tl2, the return value rlt is 1.  </P>

<P><B><SPAN class=cpp-keyword>AscTime</SPAN>(int stk:sv, str:sv);</B> &nbsp;--&gt; <CODE>AscTime</CODE> converts an integer stack to a time string of format: Fri Oct 18 22:20:48 2019. See <CODE>Time2Date</CODE> for integer stack format.  Example:</P>
<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("2021,5,2,25,5,36,23,54", s);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>IntStackSplit</SPAN>(t, s, ",");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Date2Time</SPAN>(t, th, tl);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(th, 1);<SPAN class=cpp-keyword> SetDecToBox</SPAN>(tl, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Time2Date</SPAN>(th, tl, x);<SPAN class=cpp-keyword> IntStackCombine</SPAN>(x, ",", "%d", s);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(s, 4);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>AscTime</SPAN>(t, s);<SPAN class=cpp-keyword>  SetStrToBox</SPAN>(s, 5);<SPAN class=cpp-comment></SPAN>
</PRE>

<P>Box 1 conatins integer 30888231, Box 2 contains integer -440720672, Box 4 contains string  "2021,5,2,25,5,36,23,54", Box 5 contains string "Tue May 25 05:36:23 2021".</P>

<P><B><SPAN class=cpp-keyword>URLDownload</SPAN>(url:svc, timoutsec:ivc, fn:svc, flag:ivc, return flag:iv);</B> &nbsp;--&gt; <CODE>URLDownload</CODE> downloads a http link to a file.  Parameter timeout determines the timeout in second if downloading is not sucessful.  The third parameter is a flag.  If the value is 0, the command will return even the download is not finished.  If the flag is 1, the function will not return until the download is finished or the time is out.  The fourth parameter is a return flag that shows if download is sucessful (1) or not (0).</P>

<P><B><SPAN class=cpp-keyword>URLDownloadStatus</SPAN>(progress:iv, max:iv);</B> &nbsp;--&gt; <CODE>URLDownloadStatus</CODE> return two status of the current downloading: The first parameter is the bytes currently downloaded.  The second parameter is the maximum number of bytes to be downloaded.  For example, a file to download has 10000 bytes.  This function may return 122 and 10000.  This means that currently 122 bytes have already downloaded out of total of 10000 bytes.  When using this function, the timeout value in command URLDownload is normally set to a big value.  Here is an example using URLDownload and URLDownloadStatus:</P>

<PRE>
<SPAN class=cpp-keyword>URLDownload</SPAN>(urllink, 1000, filename, 0, sucess);
<SPAN class=cpp-keyword>SetWindowToTop</SPAN>(hUtilProg);

<SPAN class=cpp-keyword>SetIntVal</SPAN>(0, cnt)
<SPAN class=cpp-keyword>while</SPAN>(cnt, <, 1000, 1)
  <SPAN class=cpp-keyword>delay</SPAN>(2000)
  <SPAN class=cpp-keyword>UrlDownloadStatus</SPAN>(p, m)
  <SPAN class=cpp-keyword>if</SPAN>(p, ==, m) <SPAN class=cpp-keyword>break</SPAN>(); <SPAN class=cpp-keyword>endif</SPAN>();
<SPAN class=cpp-keyword>Wend</SPAN>();
</PRE>

<P><B><SPAN class=cpp-keyword>URLToUTF8</SPAN>(url:svc, uft8:sv);</B> &nbsp;--&gt; <CODE>URLToUtf8</CODE> converts an URL address in unicode to UTF8 address for downloading with command <CODE>URLDownload</CODE>.  When downloading a file, the address in unicode format will not work.  It is necessary to convert the unicode address in UTF8 format first with this command.</P>

<P><B><SPAN class=cpp-keyword>ParseFile</SPAN>(fullpath:ivc, path:sv, full fn:sv, fn: sv, ext:sv);</B> &nbsp;--&gt; <CODE>ParseFile</CODE> separates a full path into path, file name with extension, file name, and file extension.  If the last character of path is the backslash \, ffn, fn, and ext are all empty.  If there is no dot . between the last backslash \ and the end of the string, ffn and fn will be the same and ext will be empty.</P>

<P>The path variable returned from this function contains the backslash in the last character.</P>

<P><CODE>ParseFile</CODE> also works for ParseFile(".\t1\fn.txt", dir, fn, ffn, ext);  The result is dir=.\t1\</P>

<P><B><SPAN class=cpp-keyword>FormFile</SPAN>(fullpath:iv, path:svc, full fn:svc, fn: svc, ext:svc);<</B> &nbsp;--&gt; <CODE>FormFile</CODE> forms the full path.  The input/output parameter directions are reversed as those in <CODE>ParseFile</CODE>.  If parameter ffn is not empty, path and ffn are combined into full path file name.  If ffn is empty, path, fn, and ext are combined into full file name.</P>

<P><B><SPAN class=cpp-keyword>ParseURL</SPAN>(url:ivc, path:sv, full fn:sv, fn: sv, ext:sv);</B> &nbsp;--&gt; <CODE>ParseURL</CODE> is the same as <CODE>ParseFile</CODE>, except that the first parameter is URL.  In URL, a forward slash is used to separate the entities.</P>

<P><B><SPAN class=cpp-keyword>SetPauseVal</SPAN>(pause:ivc);</B> &nbsp;--&gt; <CODE>SetPauseVal</CODE> may be used to pause (pause value is 1) or start (pause value is zero) the execution of a script. This command is normally used with the Pause button on the interface.  The function of the Pause button on the interface is to toggle the pause value.  Therefore, if the <CODE>SetPauseVal</CODE> sets the pause value to 1 to pause the execution of the script file, clicking on the Pause button will toggle the pause value to zero, thus starting the execution of the script file.</P>


<P><B><SPAN class=cpp-keyword>RunApplication</SPAN>(app:svc, str:svc);</B> &nbsp;--&gt; <CODE>RunApplication</CODE> takes two parameters as inputs.  The first parameter is the name of the application.  The second parameter is the command line input to the application.  This command starts the application with command line input.  For example, the following command opens a web page with internet explorer:</P>
<PRE>
<SPAN class=cpp-keyword>RunApplication</SPAN>("iexplore", "http://www.yahoo.com");
</PRE>

<P>Some of the application names: iexplore, chrome, notepad, mspaint, cmd, explorer, winword, excel, wmplayer.exe.</P>

<P>Some of the parameter may contain spaces, the application will not interpret the parameter correctly.  For example:</P>
<PRE>
<SPAN class=cpp-keyword>RunApplication</SPAN>("wmplayer.exe", "c:/music/music dir/msuic file.mp3");
</PRE>

<P>wmplayer will say the file is not correct since it interprets the parameter as three parameters.  Double quote must be added to the begin and the end of the string.  StrDoubleQuote command can be used to perform the function.</P>

<P><CODE>RunApplication</CODE> does not return the handle of the window.  The following program show how to get the handles of the window and its client area:</P>

<PRE>
<SPAN class=cpp-keyword>RunApplication</SPAN>("iexplore", "C:\UserData\000\script\chars.html");<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// Wait for sometime for window to open, then get the handle</SPAN>
<SPAN class=cpp-keyword>Delay</SPAN>(1000);<SPAN class=cpp-keyword> GetForegroundWindow</SPAN>(han);<SPAN class=cpp-keyword> setHexToBox</SPAN>(han, 1);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// Get the title and area of the window:</SPAN>
<SPAN class=cpp-keyword>GetWindowText</SPAN>(han, s);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(s, 4);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>GetWindowRect</SPAN>(han, l, t, r, b);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>FormRect</SPAN>(l, t, r, b, sv);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(sv, 5);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// This is not the client window. Change the location, get client handle</SPAN>
<SPAN class=cpp-keyword>op</SPAN>(l, +, 200, l);<SPAN class=cpp-keyword> op</SPAN>(t, +, 200, t);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>GetWindowHandleAt</SPAN>(l, t, hwnd);<SPAN class=cpp-keyword> setHexToBox</SPAN>(hwnd, 2);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// Just for test: Set other window to foreground, then bing this window to foreground</SPAN>
<SPAN class=cpp-keyword>Delay</SPAN>(10000);<SPAN class=cpp-keyword> SetWindowToTop</SPAN>(hwnd);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// Select some text, then copy to clipboard:</SPAN>
<SPAN class=cpp-keyword>Delay</SPAN>(10000);<SPAN class=cpp-keyword> SendKeyControl</SPAN>('c');<SPAN class=cpp-comment></SPAN>
</PRE>
<P>The window handle "han" is not the handle of explore.  If you move the bull's eye around the very edges of left, bottom, and right, you will see the handle is the same as "han".  So the top left corner of the 
window is added with some values to get to the client area, then the handle is obtained again with command <CODE>GetWindowHandleAt</CODE>.  The added value may vary with different application.</P>

<P>
<B><SPAN class=cpp-keyword>ChangeId3</SPAN>(fn:svc, stk:svc);</B><BR>
<B><SPAN class=cpp-keyword>ChangeTag</SPAN>(fn:svc, tag stk:svc);</B><BR>
<B><SPAN class=cpp-keyword>ChangeId3Tag</SPAN>(fn:svc, id3 stk:svc, tag stk:svc);</B><BR> &nbsp;--&gt; 

<CODE>ChangeId3</CODE> changes ID3 of an mp3 file. <CODE>ChangeTag</CODE> Change the TAG of an mp3 file.  <CODE>ChangeId3Tag</CODE> changes both ID3 and TAG. The ID3 and TAG should be stored in stack variables.</P>

<P>For ID3, each frame in the ID3 takes three entries.  The first one is the name of the frame, the second one is an encoding flag.  The string only contains one character.  Value 1 indicates that the third parameter is encoded in UNICODE LE format.  Value zero indicates that the third parameter can be either ASCII or GB2312.  The third parameter is the contents of the frame.  The order of the frame is not important.</P>
<P>For TAG, each item only takes one entry.  The entry is the contents of the item.  The items must be in the following order and length: (Note: There is one extra item after comment for track number.  If the string character for track is zero, the comment item can be maximum of 30 character.  If the string character for track is not zero, the comment field can only be 28 character.  The 29th character is normally 0, marking the end of the comment.  The 30th character is the track number if there is one.  If the string is longer than 30 characters, only the first 28 character are used.).</P>

<TABLE border="1">
<TR>
<TH width="20%"> <B><I>item</I></B></FONT></TH>
<TH width="20%"> <B><I>type</I></B></FONT></TH>
<TH width="20%"> <B><I>length (b)</I></B></FONT></TH>
</TR>
<TR>
<TD><FONT face=Verdana>header</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>3 (not required)</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>song name</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>30</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>artist</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>30</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>album name</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>30</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>year</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>4</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>comment</FONT></TD>
<TD><FONT face=Verdana>string</FONT></TD>
<TD><FONT face=Verdana>30</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana>genre</FONT></TD>
<TD><FONT face=Verdana>byte</FONT></TD>
<TD><FONT face=Verdana>1</FONT></TD>
</TR>
<TR>
<TD><FONT face=Verdana><B>total</B></FONT></TD>
<TD>&nbsp;</TD>
<TD><FONT face=Verdana><B>128</B></FONT></TD>
</TR>
</TABLE>

<P>In the above table, the header is not required.</P>

<P>
<B><SPAN class=cpp-keyword>ReadId3</SPAN>(fn:svc, stk:svc, enc:ivc);</B><BR>
<B><SPAN class=cpp-keyword>ReadTag</SPAN>(fn:svc, tag stk:svc, enc:ivc);</B><BR> &nbsp;--&gt; 

<CODE>ReadId3</CODE> and <CODE>ReadTag</CODE> just read back the information in the stack variables. <CODE>ReadTag</CODE> normally returns 8 values int the stack variable.  The first six variables has the same meaning as those in the table.  The 7th value is the track number.  The 8the value is the genre.</P>

<P>Following is an example of the use of ChangeId3Tag:</P>

<PRE>
<SPAN class=cpp-keyword>StrCatChar</SPAN>("", 0, 1, x0)            // string with character value 0
<SPAN class=cpp-keyword>StrCatChar</SPAN>("", 1, 1, x1)            // string with character value 1
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "TALB"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x1); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "Chinese Song");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "COMM"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x0); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "Nothing");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "TCON"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x0); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "Other");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "TIT2"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x0); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "01");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "TRCK"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x0); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "01");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "TPE1"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, x1); <SPAN class=cpp-keyword>StrStackPush</SPAN>(id3, "Larry");

// total of 6 items
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, "01.mp3");       // song name
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, "01.mp3");       // aritst
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, "Chinese Song"); // album name
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, "1998");         // year
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, "01.mp3");       // comments
<SPAN class=cpp-keyword>StrCatChar</SPAN>("", 2, 1, x)            // track 2 character
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, x);              // track
<SPAN class=cpp-keyword>StrCatChar</SPAN>("", 3, 1, x)            // track 3 character
<SPAN class=cpp-keyword>StrStackPush</SPAN>(tag, x);              // genre

// any one of the following commands can be used
<SPAN class=cpp-comment>//ChangeId3("c:\temp\fin.mp3", id3);</SPAN>
<SPAN class=cpp-comment>//ChangeTag("c:\temp\fin.mp3", tag);</SPAN>
<SPAN class=cpp-keyword>ChangeId3Tag</SPAN>("c:\temp\fin.mp3", id3, tag);
</PRE>

<P>The program creates two stack variables, one for ID3 and one for TAG.  The frame name and contents in ID3 are paired.  The contents of TAG must pushed in the shown sequence (may be modified later).  Characters with value less than 0x100 will be written into file in a single byte.  Unicode characters are written into file in LE format, i.e., LSB first, then MSB.  In order to store a value in the string stack, as the genre in TAG stack variable in the example above, StrCatChar can be used.</P>

<P><CODE>ReadId3</CODE> and <CODE>ReadTag</CODE> both take one encode variable.  It has three encoding: 0: ANSI, 1: LE, 2: GE</P>

<P><B><SPAN class=cpp-keyword>AppendMp3</SPAN>(stk:svc, des file:sv);</B> &nbsp;--&gt; <CODE>AppendMp3</CODE> appends all files in a string stack together, then save the result in destination file.  The ID of the result file uses the ID in the first file in the stack.</P>

<P><B><SPAN class=cpp-keyword>SwapMbLB</SPAN>(src str:svc, des str:svc);</B> &nbsp;--&gt;<CODE>SwapMbLB</CODE> swaps the upper byte with the lower byte of all characters in a string.  This function is mainly used to change big endian to little endian for unicode text.</P>

<P>
<B><SPAN class=cpp-keyword>UnicodeToGb2312</SPAN>(src str:svc, des str:svc);</B><BR>
<B><SPAN class=cpp-keyword>Gb2312ToUnicode</SPAN>(src str:svc, des str:svc);</B><BR>
<B><SPAN class=cpp-keyword>UnicodeToUTF8</SPAN>(src str:svc, des str:svc);</B><BR>
<B><SPAN class=cpp-keyword>UTF8ToUnicode</SPAN>(src str:svc, des str:svc);</B><BR>
<B><SPAN class=cpp-keyword>UTF8ToUnicodeFile</SPAN>(srcFile:svc, desFile:svc);</B><BR>
<B><SPAN class=cpp-keyword>Gb2312ToUnicodeFile</SPAN>(srcFile:svc, desFile:svc);</B><BR>
<B><SPAN class=cpp-keyword>UnicodeToGb2312File</SPAN>(srcFile:svc, desFile:svc);</B><BR>
<B><SPAN class=cpp-keyword>UnicodeToUTF8File</SPAN>(srcFile:svc, desFile:svc);</B><BR> &nbsp;--&gt; 

<CODE>UnicodeToGb2312</CODE>, <CODE>UnicodeToUTF8</CODE>, and <CODE>UTF8ToUnicode</CODE> perform format change of a string.  For commands ended with File, the contents in the source file is converted and saved in the destination file.  Source and destination files can the same file.</P>

<P>
<B><SPAN class=cpp-keyword>ReadRegInt</SPAN>(key:svc, val:iv);</B><BR>
<B><SPAN class=cpp-keyword>ReadRegStr</SPAN>(key:svc, val:sv);</B><BR>
<B><SPAN class=cpp-keyword>WriteRegInt</SPAN>(key:svc, val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>WriteRegStr</SPAN>(key:svc, val:svc);</B><BR>
<B><SPAN class=cpp-keyword>ReadIniInt</SPAN>(sect:svc, key:svc, val:iv);</B><BR>
<B><SPAN class=cpp-keyword>ReadIniStr</SPAN>(sect:svc, key:svc, val:sv);</B><BR>
<B><SPAN class=cpp-keyword>WriteIniInt</SPAN>(sect:svc, key:svc, val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>WriteIniStr</SPAN>(sect:svc, key:svc, val:svc);</B><BR> &nbsp;--&gt; 
<CODE>ReadRegInt</CODE>, <CODE>ReadRegStr</CODE>, <CODE>WriteRegInt</CODE>, and <CODE>WriteRegStr</CODE> are used to read or write integer number or string to registry.  All these functions take a key and the string or integer to read or write.  The key will be stored in HKEY_LOCAL_MACHINE\SOFTWARE\UtilProg.  One of the use for these functions is to remember a directory name in a script, as shown in the following example:


<P><CODE>ReadIniInt</CODE>, <CODE>ReadIniStr</CODE>, <CODE>WriteIniInt</CODE>, <CODE>WriteIniStr</CODE> read and write the information into INI file.</P>

<P>Two variables in INI file, called script_path and editor_name, are used in the program.  These two variables are setup by running "Execute Line" button on GUI with the following lines:</P>
<PRE>
WriteIniStr("UtilProg", "editor_name", "C:\UserData\000\util\Notepadpp1\notepadpp.exe");
WriteIniStr("UtilProg", "script_path", "C:\UserData\000\script\");
</PRE>

<P>
<B><SPAN class=CPP-KEYWORD>DecodeText</SPAN>(datfile:svc, password:svc, outtext:sv, error:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>EncodeText</SPAN>(text:svc, password:svc, format:ivc, datfile:svc);</B><BR>
<B><SPAN class=CPP-KEYWORD>DecodeFile</SPAN>(datfile:svc, password:svc, outfile:sv, error:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>EncodeFile</SPAN>(textfile:svc, password:svc, datfile:svc);</B><BR> &nbsp;--&gt; 

<CODE>EncodeText</CODE> encodes a string variable randomly and writes the result in a file.  The first variable is the text to be encoded.  The second variable is the password.  It must be at least 9 characters (max 11 chars).  The characters can be numbers or lower case or upper case character.  To make the password hard to guess, mix lower case, upper case, and numerical together for the password.  The third variable is the format of the string.  If the string is ANSI text, format should be 0.  If the string is Unicode, format should be 1.  It is possible to set format to 1 for ANSI string, but the file size may be relatively large.  The fourth variable is the file for the encoded text.</P>

<P><CODE>DecodeText</CODE> decodes the encoded text in a file to text.  The first variable is the file that contains the encoded text, the second variable is the password.  The third variable is the decoded text. the fourth variable indicates the error.  If the decoding is successful, the return value is zero.  If the return value is 1, the password is not correct.</P>
 
<PRE>
<SPAN class=cpp-keyword>GetFromClipboard</SPAN>(text);
<SPAN class=cpp-keyword>EncodeText</SPAN>(text, "pass22word",  1, "c:\datfile.dat");
<SPAN class=cpp-keyword>DecodeText</SPAN>("c:\datfile.dat", "pass22word", outtext, error);
<SPAN class=cpp-keyword>SendToClipboard</SPAN>(outtext);
</PRE>

<P>Before run the program, copy some unicode text to the clipboard.  After run the program, paste the text into the notepad.  The text should be the same as before.</P>

<P><CODE>EncodeFile</CODE> and <CODE>DecodeFile</CODE> work on files instead of text.  <CODE>EncodeFile</CODE> and <CODE>DecodeFile</CODE> can be used for both text and binary files.</P>

<P>
<B><SPAN class=CPP-KEYWORD>IsSpace</SPAN>(val:ivc, result:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>IsDigit</SPAN>(val:ivc, result:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>IsXDigit</SPAN>(val:ivc, result:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>IsCharAlpha</SPAN>(val:ivc, result:iv);</B><BR>
<B><SPAN class=CPP-KEYWORD>IsCharAlphaNumeric</SPAN>(val:ivc, result:iv);</B><BR> &nbsp;--&gt; 
<CODE>IsSpace</CODE> (space, tab), <CODE>IsDigit</CODE> (0 to 9), <CODE>IsXDigit</CODE> (0 to 9, A to F, a to f), <CODE>IsCharAlpha</CODE> (a-z, A-Z), and <CODE>IsCharAlphaNumeric</CODE> (0-9, a-z, A-Z): Each of these commands returns non-zero value if the integer value is a particular representation of a character.</P>

<P><B>
<SPAN class=CPP-KEYWORD>FltToFx</SPAN>(val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxToFlt</SPAN>(val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxToFx</SPAN>(val_str:svc, exp:ivc, fra:ivc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxAdd</SPAN>(val_str:svc, opcode:svc,  val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxSub</SPAN>(val_str:svc, opcode:svc,  val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxMpy</SPAN>(val_str:svc, opcode:svc,  val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>FxDIv</SPAN>(val_str:svc, opcode:svc,  val_str:svc, exp:ivc, fra:ivc, result:sv);<BR>
<SPAN class=CPP-KEYWORD>IntToBin</SPAN>(int:ivc, bit:ivc, str:bin);<BR></B>
 &nbsp;--&gt; 
<CODE>Flt2Fx</CODE> converts a string with a floating number to a IEEE fixed number (exponent=3, mantissa=23).  exp and fra specify the number of digits for exponent and fration parts.  For example, <CODE>flt2fx</CODE>("1234.5", 8, 23, rlt); returns 449A5000</P>

<P><CODE>Fx2Flt</CODE> converts a string with hex integer to a IEEE floating number.  For example, <CODE>fx2flt</CODE>("0x449a5000", 8, 23, rlt); or <CODE>fx2flt</CODE>("449a5000", 8, 23, rlt); returns 1.2345e+3.</P>

<P><CODE>Fx2Fx</CODE> converts a fixed IEEE point (in a string) to another fixed IEEE number of a different format.  <CODE>fx2fx</CODE>("0x449a5000", 8, 23, 8, 18, rlt); returns 224D280.</P>

<P><CODE>FxAdd</CODE>, <CODE>FxSub</CODE>, <CODE>FxMpy</CODE>, and <CODE>FxDIv</CODE> perform IEEE floating number operation.</P>

<P><B><SPAN class=CPP-KEYWORD>CharToHex</SPAN>(ascii:ivc, val:iv);</B> &nbsp;--&gt; 

<CODE>CharToHex</CODE> converts hex number '0'-'9', 'A'-'F' to integer value.  For example, CharToHex('C', v); the value of v is 12. CharToHex('c', v); has the same result.</P>


<P><B><SPAN class=CPP-KEYWORD>HexDump</SPAN>(sfn:svc, naddr:ivc, bpl:ivc, flag:ivc);</B> &nbsp;--&gt; 

<CODE>HexDump</CODE> dumps a hex file to text file with the same file name and .hex extension.  naddr specifies number bytes for  address.  It can only be 4, 6, and 8.  Any other value set it to 8.  bpl specifies the number of bytes to dump for each line.  Bit 0 of <B>"flag"</B> indicates ASCII code is also dumped.  The Bit 1 of <B>"flag"</B> indicates address is also dumped.  Therefore, if <B>"flag"</B> is 0, only hex bytes are dumped.  If <B>"flag"</B> is 1, hex bytes and its corresponding ASCII codes are dumped.  If <B>"flag"</B> is 2, the start address and hex bytes are dumped.  If <B>"flag"</B> is 3, the address, hex byte, and ASCII are dumped.  For example, the command <CODE>HexDump</CODE>("file.exe", 6, 8, 3) will dump the hex contents in file file.exe to file.hex with lines like (including address, hex bytes, and ASCII bytes):</P>

<PRE>001248 e2 34 4a 67 98 65 67 54 .4Jg.egT</PRE>

<P><B><SPAN class=CPP-KEYWORD>HexDumpToClipboard</SPAN>(fn:svc, nbyte:ivc);</B> &nbsp;--&gt; 
This command dumps nbyte of bytes to clip board.</P>

<P>Both functions work ok with unicode file name.</P>

<P><B><SPAN class=CPP-KEYWORD>Txt2Hex</SPAN>(file name:svc);</B> &nbsp;--&gt; <CODE>Txt2Hex</CODE> converts a file with hex number to a hex file.  The output file name is the same as input file name , but with .hex extension.  The format of the input text file is one two-digit number per line.  The hex number can have 0x at the front.</P>

<P><B><SPAN class=CPP-KEYWORD>GetCmdLineParam</SPAN>(n_param:ivc, str:sv);</B> &nbsp;--&gt; 
When UtiProg program is started from command line (from cmd.exe), parameters can be added.  GetCmdLineParam returns the nth parameter (indicated by n_param) in str.  For example: From the directory where the UtilPorg is located, start the command:</P>
<P>Settings.exe param1 "param 2" param3</P>
<P>In a script file, run GetCmdLineParam.  If n_param=0 returns "Settings.exe", n_param=2 returns "param 2".</P>

<H2>Stack Variables</H2>

<P>Stack variables are used to store values under one name as a pool.  They are like arrays, but are not completely the same.  It is not necessary to define the size of the variable.  The value can be added to the pool in sequence by the <CODE>Push</CODE> function.  After values are added, they can be modified (<CODE>SetAt</CODE> command) and extracted (<CODE>GetAt</CODE> command) with an index (the index is zero based).  They can also be extracted in sequence by the <CODE>Pop</CODE> function.  In this case, the value is pulled out of the pool, and it does not exist anymore.  As the name suggested, a stack variable is like a stack, the first value pushed in the variable is the last one popped out from the variable.</P>

<P>There are two types of stack vasriables, string and integer.  String stack variables are used to store strings.  For example, three string variables can be defined, first_name, middle_name, and last_name.  Then names can be added to the defined string stack variables.  Integer stack variable is used in the same way to store integers.</P>

<P>Functions related to string variables start with <CODE>StrStack</CODE>.  Function related to integer variables start with <CODE>IntStack</CODE>.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(var:svc, cnt:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackGetVarValCount</SPAN>(var:svc, cnt:iv);</B><BR> &nbsp;--&gt; 
<CODE>IntStackGetVarValCount</CODE> returns the number of integers (strings) in the stack.  If this function is applied to an undefined stack, the return value is -1.  If the stack variable is pushed and popped with the same number of time, this function returns 0.  So the decision on the number of integers (string) in the stack is either <=0 or >0.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackGetVarCount</SPAN>(cnt:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackGetVarCount</SPAN>(cnt:iv);</B><BR> &nbsp;--&gt; 
<CODE>IntStackGetVarCount</CODE> returns the number of the stack variable.  This function returns 0 if there is no stack variable defined.</P>


<P>
<B><SPAN class=cpp-keyword>IntStackPush</SPAN>(var:svc, val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackPop</SPAN>(var:svc, val:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackPush</SPAN>(var:svc, val:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackPushUnique</SPAN>(var:svc, val:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackPop</SPAN>(var:svc, val:sv);</B><BR> &nbsp;--&gt; 
<CODE>IntStackPush</CODE> and <CODE>IntStackPop</CODE> push and pop a integer at the end of the stack.</P>


<P>
<B><SPAN class=cpp-keyword>IntStackGetAt</SPAN>(var:svc, idx:ivc, val:iv);</B><BR>
<B><SPAN class=cpp-keyword>IntStackSetAt</SPAN>(var:svc, idx:ivc, val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackGetAt</SPAN>(var:svc, idx:ivc, val:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackSetAt</SPAN>(var:svc, idx:ivc, val:svc);</B><BR>&nbsp;--&gt; 
<CODE>IntStackGetAt</CODE> returns the nth (idx) value of the stack variable.  If idx is -1 or idx is greater than or equal to the total number of values, the command returns the last value.  For example, if a stack contain 5 values, indexed as 0, 1, 2, 3, 4.  <CODE>IntStackGetVarValCount</CODE> returns 5.  If 5 is used as idx in the command, the last value will be returned from this command.</P>


<P>
<B><SPAN class=cpp-keyword>IntStackGetLast</SPAN>(var:svc, val:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackGetLast</SPAN>(var:svc, val:sv);</B><BR> &nbsp;--&gt; 
<CODE>IntStackGetLast</CODE> returns the last value pushed, but the stack variable is unchanged.  This is different from <CODE>pop</CODE>, which pulls the value out of the stack.</P>

<P>If the parameter to stack commands is incorrect, no action will be taken.  For example, if the variable to the <CODE>Pop</CODE> command does not exist, the popped value will be undefined.  If the index to <CODE>GetAt</CODE> or <CODE>SetAt</CODE> is larger than number of the value pushed, the value will not be set or the returned value will be undefined.</P>

<P>
<B><SPAN class=cpp-keyword>StrStackClearVar</SPAN>(var:svc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackClearVar</SPAN>(var:svc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackClearAll</SPAN>();</B><BR>
<B><SPAN class=cpp-keyword>StrStackClearAll</SPAN>();</B><BR> &nbsp;--&gt; 
<CODE>IntStackClearVar</CODE> clears a integer stack variable.  <CODE>IntStackClearAll</CODE> clears all integer stack variables.</P>

<P><B>
<SPAN class=cpp-keyword>IntStackDeleteAt</SPAN>(var:svc, idx:ivc)<BR>
<SPAN class=cpp-keyword>IntStackInsertAt</SPAN>(var:svc, idx:ivc, val:svc)<BR>
<SPAN class=cpp-keyword>StrStackDeleteAt</SPAN>(var:svc, idx:ivc)<BR>
<SPAN class=cpp-keyword>StrStackInsertAt</SPAN>(var:svc, idx:ivc, val:svc)<BR></B> &nbsp;--&gt; 
These command insert or delete a value to stack variable.  The insertion is at the item before the index.  For example, if the index is 1, the new item is inserted before index 1, after item 0.  For an integer stack containing 1, 2, if the index is 1, the value to insert is 3, then the stack becomes 1, 3, 2 after insertion.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackCopy</SPAN>(src:svc, des:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackCopy</SPAN>(src:svc, des:svc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackAppend</SPAN>(src:svc, app:svc, rlt:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackAppend</SPAN>(src:svc, append:svc, rlt:sv);</B><BR>
<B><SPAN class=cpp-keyword>IntStackMove</SPAN>(src:svc, des:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackMove</SPAN>(stk var:svc, stklen:iv);</B><BR>
<B><SPAN class=cpp-keyword>IntStackSwap</SPAN>(src:svc, des:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackSwap</SPAN>(stk var:svc, stklen:iv);</B><BR> &nbsp;--&gt; 

<CODE>IntStackCopy</CODE> (<CODE>StrStackCopy</CODE>) command copies all values in one stack variable to another.  The contents of the destination stack variable, if any, will be deleted.  If the destination variable does not exist, it will be created.  <CODE>IntStackAppend</CODE> (<CODE>StrStackAppend</CODE>) appends contents of one stack variable to another.  For the move command, the source stack is gone.</P>

<P><B><SPAN class=cpp-keyword>IntStackFind</SPAN>(var:svc, val:ivc, start:ivc, rlt:iv);<BR>
<SPAN class=cpp-keyword>StrStackFind</SPAN>(var:svc, substr:svc, start:ivc, rlt:iv);<BR>
<SPAN class=cpp-keyword>StrStackFindNoCase</SPAN>(var:svc, substr:svc, start:ivc, rlt:iv);<BR></B>&nbsp;--&gt;

<CODE>IntStackFind</CODE> (<CODE>StrStackFind</CODE>) command finds an integer (string) in the stack, starting at the position indicated by the third parameter.  The result is the position of the integer (string) in the stack (zero based), and is returned in the fourth parameter.  If the integer (string) is not found after the position, -1 is returned.</P>

<P>Note that <CODE>StrStackFind</CODE> finds the exact string in the stack.  If the stack contains "Str", the find string is "tr", the return value will be -1.</P>

<P><B><SPAN class=cpp-keyword>StrStackStrIn</SPAN>(stk:svc, substr:svc, start:ivc, ivc:cases, rlt:iv);</B>&nbsp;--&gt; Find if a string is contained in the elements of a string stack.  Return the index if found, otherwise return -1.  If "cases" is 0, the find is case sensitive.  If it is 1, find is not case sensitive.</P>

<P><B><SPAN class=cpp-keyword>StrStackInStr</SPAN>(stk:svc, substr:svc, start:ivc, ivc:cases, rlt:iv);</B>&nbsp;--&gt; Find if any element of a string stack is contained in the sub-string.  Return the index of the string stack if found, otherwise return -1.  If "cases" is 0, the find is case sensitive.  If it is 1, find is not case sensitive.</P>

<P>Note that <CODE>StrStackStrIn</CODE> and <CODE>StrStackInStr</CODE> just find if one string is in another string, they are net necessarily the same.</P>

<P><B><SPAN class=cpp-keyword>IntStackSplit</SPAN>(var:svc, int str:svc, split str:svc);<BR>
<SPAN class=cpp-keyword>StrStackSplit</SPAN>(stk:svc, str:svc, split str:svc);<BR></B>&nbsp;--&gt;

<CODE>IntStackSplit</CODE> (<CODE>StrStackSplit</CODE>) command splits an integer (or just a) string separated by the split string.  The split integers (strings) are stored in the stack.  The initial contents (if exist) of the stack are overwritten.  The split string can be any string, for example, a space.  As an example, the following line will store each line in outtext into stack stkdata:</P>
<PRE>
  StrStackSplit(stkdata, outtext, STR_DA);
</PRE>

<P>For IntStackSplit, the conversion from string to integer is proceeded as much as possible, for example:</P>
<PRE>
SetStrVal("12 34 56 67d x", s)
IntStackSplit(istk, s, " ");
IntStackCombine(istk, " ", "%d", str);
SendToClipboard(str);  ---> 12 34 56 67 0
</PRE>
<P>67d is converted to integer 67.  x is converted to integer 0.  If 67d is proceeded with 0x, it will be treated as hex number.  This is shown in the following example:</P>

<PRE>
SetStrVal("0x12 0x34 56 78 '3' '\t'", s);
IntStackSplit(x, s, " ");
IntStackCombine(x, " ", "%02x", t); SetStrToBox(t, 5);
</PRE>
<P>The result is 12 34 38 4e 33 09.  All are in hex values.</P>

<P><B><SPAN class=cpp-keyword>IntStackCombine</SPAN>(stk var:svc, separator:svc, fmt:svc, rlt str:sv);<BR>
<SPAN class=cpp-keyword>StrStackCombine</SPAN>(stk var:svc, separator:svc, rlt str:sv);"));<BR></B>&nbsp;--&gt;

<CODE>IntStackCombine</CODE> (<CODE>StrStackCombine</CODE>) command combines the integers (or strings) in the stack variable into a string, separated by the separator.  For <CODE>IntStackCombine</CODE>, a format string is also needed.  The meaning of the format string is the same as StrFormat. The output is placed in a string variable.</P>

<P><B><SPAN class=cpp-keyword>StrStackCat</SPAN>(stk1:sv, sep:svc, stk2:sv, rtn:sv);");</B>

<CODE>StrStackCat</CODE> concatenates each element of the two string stacks with seperator in between.  For example if the two correponding elements of the stacks are "x1" and "y1", the seperator is ", ", the element of the output is "x1, y1".</P>

<P><B><SPAN class=cpp-keyword>IntStackSort</SPAN>(istk:sv, order:ivc);<BR>
<SPAN class=cpp-keyword>StrStackSort</SPAN>(itsk:svc, order:ivc, case:ivc);"));<BR></B>&nbsp;--&gt;

<CODE>IntStackSort</CODE> (<CODE>StrStackSort</CODE>) command sorts the integers (or strings) in the stack variable in a certain order.  The <B>"order"</B> parameter can be 0 (ascending order) or 1 (decending order).  For <CODE>StrStackSort</CODE>, the string in the stack can be text string of floating point value.  This is determined by the bit 1 of <B>"case"</B> parameter.  If the value of bit 1 is 1, the string in the stack should be purely floating number.  If the value is 0, the string in the stack is text.  For text sort, the case sensitive paramter can be specified with a value 0 (case insenstive) or 1 (case sensitive) at bit 0 of <B>"case"</B> parameter.  Therefore there are three cases for the value of parameter <B>"case"</B>: 0: performs a case sensitive sort (00); 1: perform a case insensitive sort (01); 2. perform a floating value sort (1x).</P>

<P><B><SPAN class=cpp-keyword>IntStackSortInt</SPAN>(itsk:sv, order:ivc, istk:sv);<BR>
<SPAN class=cpp-keyword>IntStackSortStr</SPAN>(itsk:sv, order:ivc, sstk:sv);<BR>
<SPAN class=cpp-keyword>StrStackSortInt</SPAN>(stsk:sv, order:ivc, case:sv, itsk:sv);<BR>
<SPAN class=cpp-keyword>StrStackSortStr</SPAN>(sstk:sv, order:ivc, case:svc, stsk:sv);<BR></B>&nbsp;--&gt;

<CODE>IntStackSortInt</CODE> and <CODE>IntStackSortStr</CODE> (<CODE>StrStackSortInt</CODE> and <CODE>StrStackSortStr</CODE>) sorts the first stack, <B>"istk"</B>, and at the same time changes the ordering of the second stack (<B>"istk"</B> or <B>"sstk"</B>), accordingly.  The sort is in ascending if the value of the second variable <B>"order"</B> is 1, descending order if the value is 0.  For string stack, the third variable <B>"case"</B> determines if the sort is case insensitive (0) or case sensitive (1).</P>

<P><B><SPAN class=cpp-keyword>IntStackMax</SPAN>(stk var:svc, maxval:iv);<BR>
<SPAN class=cpp-keyword>IntStackMin</SPAN>(stk var:svc, minval:iv);<BR>
<SPAN class=cpp-keyword>IntStackSum</SPAN>(stk var:svc, sumval:iv);<BR>
<SPAN class=cpp-keyword>StrStackMax</SPAN>(stk var:svc, maxval:iv);<BR>
<SPAN class=cpp-keyword>StrStackMin</SPAN>(stk var:svc, minval:iv);<BR></B>&nbsp;--&gt;

<CODE>IntStackMax</CODE>, <CODE>IntStackMin</CODE>, or <CODE>IntStackSum</CODE> find the maximum value, minimum value, or Sum of all values in the stack.  String stack must contain number for these command.</P>

<P><B><SPAN class=cpp-keyword>IntStackMaxAll</SPAN>((stk var1:ivc, stk var2:ivc, rlt stk:iv);<BR>
<SPAN class=cpp-keyword>IntStackMinAll</SPAN>((stk var1:ivc, stk var2:ivc, rlt stk:iv);<BR></B>&nbsp;--&gt;

<CODE>IntStackMaxAll</CODE> and <CODE>IntStackMinAll</CODE> find the maximum and minimum value of values at the same index and place the result in the output stack.</P>

<P>For all stack array functions, the first parameter is the number of column that the single-dimensioned array is divided into.  For example, the single-dimensioned array has 20 elements.  If the column is 6, the two-dimensioned array will have 4 rows, but the fourth row only has two elements.</P>

<P>In all functions, row index and column index are 0 based.</P>

<P><B><SPAN class=cpp-keyword>IntStackArrayGetAt</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, ColIdx:ivc, rtnint:iv);<BR>
<SPAN class=cpp-keyword>IntStackArraySetAt</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, ColIdx:ivc, intval:ivc);<BR>
<SPAN class=cpp-keyword>StrStackArrayGetAt</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, ColIdx:ivc, rtnint:sv);<BR>
<SPAN class=cpp-keyword>StrStackArraySetAt</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, ColIdx:ivc, intval:svc);<BR></B>&nbsp;--&gt;

<CODE>IntStackArrayGetAt</CODE> (<CODE>StrStackArrayGetAt</CODE>) returns the value at the <B>"rowidx"</B> and <B>"colidx"</B>.  <CODE>IntStackArraySetAt</CODE> (<CODE>StrStackArraySetAt</CODE>) sets the value at the <B>"rowidx"</B> and <B>"colidx"</B>.  In all commands, the stack is divided into an array with <B>"column"</B> of columns</P>

<P><B><SPAN class=cpp-keyword>IntStackArrayGetRow</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, rtn stk:sv);<BR>
<SPAN class=cpp-keyword>IntStackArrayGetCol</SPAN>((stk var:svc, column:ivc, ColIdx:ivc, rtn stk:sv);<BR>
<SPAN class=cpp-keyword>StrStackArrayGetRow</SPAN>((stk var:svc, column:ivc, RowIdx:ivc, rtn stk:sv);<BR>
<SPAN class=cpp-keyword>StrStackArrayGetCol</SPAN>((stk var:svc, column:ivc, ColIdx:ivc, rtn stk:sv);<BR></B> &nbsp;--&gt;

<CODE>IntStackArrayGetRow</CODE> (<CODE>StrStackArrayGetRow</CODE>) returns the <B>RowIdx</B>'th row.  <CODE>IntStackArrayGetCol</CODE> (<CODE>StrStackArrayGetCol</CODE>) returns the <B>ColIdx</B>'th column.  The stack is divided into an array with <B>"column"</B> of columns</P>

<P><B><SPAN class=cpp-keyword>IntStackSetAll</SPAN>(var:svc, nelement:ivc, val:ivc);<BR>
<SPAN class=cpp-keyword>StrStackSetAll</SPAN>((var:svc, nelement:ivc, val:svc);<BR></B> &nbsp;--&gt;

<CODE>IntStackSetAll</CODE> (<CODE>StrStackSetAll</CODE>) creates a integer stack variable with number of elements specified by the second variable, then sets all the elements to a certain integer (string).  If the stack variable exists, the stack variable is reset.  If the stack variable does not exist, it will be created.  Example:</P>
<P><SPAN class="code-yellow">StrStackSetAll(stk, 5, "1110");</SPAN></P>
<P>The command creates string stack stk of 5 elements, and sets all the elements to string "1110".</P>

<P><B><SPAN class=cpp-keyword>StrStackGetLength</SPAN>(stk var:svc, stklen:iv);</B> &nbsp;--&gt;

<CODE>StrStackGetLength</CODE> finds the length of all the elements, puts the results in an integer stack, whose elements correspond to the elements in the string <B>stack</B>.</P>

<P><B><SPAN class=cpp-keyword>StrStackMaxLength</SPAN>(stk var:svc, maxlen:iv);<BR>
<SPAN class=cpp-keyword>StrStackMinLength</SPAN>(stk var:svc, minlen:iv);<BR></B>&nbsp;--&gt;

<CODE>StrStackMaxLength</CODE> finds the maximum (minimum) length of all the elements, puts the results in an integer <B>variable</B>.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackRemoveRepeat</SPAN>(src stk var:sv, dest stck:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackRemoveRepeat</SPAN>(src stk var:sv, dest stck:sv);</B><BR> &nbsp;--&gt;

<CODE>IntStackRemoveRepeat</CODE> (<CODE>StrStackRemoveRepeat</CODE>) removes all repeat elements except the first one.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackOp</SPAN>(var:svc, op, val:svc, var:sv);"));</B><BR>
<B><SPAN class=cpp-keyword>StrStackOp</SPAN>(var:svc, op, val:svc, fmt:svc, var:sv);</B><BR> &nbsp;--&gt;
These commands perform the operation of two stacks element by element.  See sections for the types of operation used for integer stack (op command) and string stack (flop command).</P>


<P><B><SPAN class=cpp-keyword>IntStackReverse</SPAN>(var:svc, at:ivc, var:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackReverse</SPAN>(var:svc, at:ivc, var:sv);</B><BR> &nbsp;--&gt;
The elements of a stack are reversed in order.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackToClipboard</SPAN>(stk:sc, fmt:svc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackToClipboard</SPAN>(stk:sc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackFromClipboard</SPAN>(fmt:svc, stk:sc);</B><BR>
<B><SPAN class=cpp-keyword>StrStackFromClipboard</SPAN>(stk:sc);</B><BR>
<B><SPAN class=cpp-keyword>IntStackFromFile</SPAN>(file:svc, fmt:svc, stack:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackFromFile</SPAN>(file:svc, stack:sv);</B><BR>
<B><SPAN class=cpp-keyword>IntStackToFile</SPAN>(stk:sv, fmt:svc, file:svc, encode:ivc, append:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackToFile</SPAN>(stk:sv, file:svc, encode:ivc, append:iv);</B> <BR>&nbsp;--&gt;

These commands perform the conversion between stack and clipboard or file.  For integer stack, a format string is required.  The format of the contents in file or clipboard is one value or string per line.  For example, if the integer stack contains 9, 10, 11.  After IntStackToClipboard(stk, "%02x"), the clipboard result is 09, 0a, 0b, each on one line.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackDiff</SPAN>(int stk1:svc, int stk2:svc, int diff:sv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackDiff</SPAN>(str stk1:svc, str stk2:svc, int diff:sv);</B><BR>&nbsp;--&gt;
These commands compare each element of two stacks, put the result in the third stack.  For integer stack, each element of the output integer stack is the difference of the two input integer stacks.  For string stack, it is string comparison.  So if the input elements are equal, the output is 0.</P>

<P>
<B><SPAN class=cpp-keyword>IntStackFindRepeat</SPAN>(int stk1:svc, int:svc, repeat:iv);</B><BR>
<B><SPAN class=cpp-keyword>StrStackFindRepeat</SPAN>(str stk1:svc, str:svc, repeat:iv);</B><BR> &nbsp;--&gt;
The command find the number of repeat of a integer (string) in the stack.</P>

<P><B><SPAN class=cpp-keyword>StrStackAddStr</SPAN>(var:svc, str:svc, pos:ivc, rlt:sv);</B> &nbsp;--&gt;
This command adds a string to all elements of a stack variable.  The position can be any value.  If it is 0, the string is added at the beginning of each elements in the stack.  If the position value -1, the string is added to the end of each elements.  If the value is greater than the length of the element, the string is added to the end of the string.</P>

<P><B><SPAN class=cpp-keyword>StrStackInt</SPAN>(var:svc, rlt:iv);</B> &nbsp;--&gt;
<CODE>StrStackInt</CODE> converts the elements of a string stack to an integer stack.</P>

<P><B><SPAN class=cpp-keyword>IntStackStr</SPAN>(var:svc, fmt:svc, rlt:iv);</B> &nbsp;--&gt; converts each element of an integer, put the converted result into a string stack with the format given.</P>

<P><B><SPAN class=cpp-keyword>StrStackCases</SPAN>(var:svc, case:ivc, out:sv);</B> &nbsp;--&gt; changes the cases of a string stack.  case=0: change to all lower case.  case=1: change to all upper case.  case=2: change the first character to upper case.</P>

<P><B><SPAN class=cpp-keyword>ForEachStrStack</SPAN>(stk, idx0:ivc, idx:iv, rtn:sv);<BR><SPAN class=cpp-keyword>ForEachStrStackEnd</SPAN>();<BR></B> &nbsp;--&gt; These two commands form a loop.  In each loop, the index to the stack item (<B>"idx"</B>) and item (<B>"rtn"</B>) are returned.  The index starts at idx0 (usually equal to 0), goes until the end of the stack.  At command <code>ForEachStrStackEnd</code>, <B>"idx"</B> is increaed by 1.  If <B>"idx"</B> is at the end of stack, the loop ends.  Otherwise, the loop is repeated.  At the end of the loop (the command following <code>ForEachStrStackEnd</code>) idx is -1.  This value can be used to determine if loop jumps out (<code>break</code> command in the loop), or the loop goes until the end of the stack.  <code>If</code>, <code>break</code>, <code>continue</code>, <code>while</code> loop, or even <code>ForEachStrStack</code> loop commands can be used inside the loop.</P>
<P>Note that <B>"idx"</B> can be changed in the loop.  For example, if it is desired to jump over one item at a certain point, <B>"if"</B> command and <B>"op<"</B> command can be inserted in the loop.</P>

<P><B><SPAN class=cpp-keyword>ForEachIntStack</SPAN>(stk, idx0:ivc, idx:iv, rtn:iv);<BR> <SPAN class=cpp-keyword>ForEachIntStackEnd</SPAN>();<BR></B> &nbsp;--&gt; These two commands are the same as as <code>ForEachStrStack</code> loop except they apply to IntStack.</P>

<P><B><SPAN class=cpp-keyword>StrStackTrim</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrStackTrimLeft</SPAN>(src:svc, des:sv);<BR>
<SPAN class=cpp-keyword>StrStackTrimRight</SPAN>(src:svc, des:sv);<BR>
</B> &nbsp;--&gt; These three commnad trim each elements of a stack.</P>

<P>Stack example 1:</P>

<PRE>
<SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 10); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 11); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 12);
<SPAN class=cpp-keyword>IntStackPush</SPAN>(y, 13); <SPAN class=cpp-keyword>IntStackPush</SPAN>(y, 14);

<SPAN class=cpp-keyword>IntStackGetVarCount</SPAN>(cnt);        <SPAN class=cpp-comment>// return 2, x and y</SPAN>

<SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(x, cnt);  <SPAN class=cpp-comment>// return 3, three values 10, 11, and 12</SPAN>

<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 0, val); 
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 1, val); 
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 2, val); 
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 3, val);   <SPAN class=cpp-comment>// value not determined</SPAN>

<SPAN class=cpp-keyword>IntStackSetAt</SPAN>(x, 1, 1234);

<SPAN class=cpp-keyword>IntStackPop</SPAN>(x, val);   <SPAN class=cpp-comment>// 12</SPAN>
<SPAN class=cpp-keyword>IntStackPop</SPAN>(x, val);   <SPAN class=cpp-comment>// 1234</SPAN>
<SPAN class=cpp-keyword>IntStackPop</SPAN>(x, val);   <SPAN class=cpp-comment>// 10</SPAN>
<SPAN class=cpp-keyword>IntStackPop</SPAN>(x, val); 
<SPAN class=cpp-keyword>IntStackPop</SPAN>(x, val); 

<SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(x, cnt);
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(cnt,4);

<SPAN class=cpp-keyword>StrStackPush</SPAN>(z, "testty0");
<SPAN class=cpp-keyword>StrStackGetVarValCount</SPAN>(z, cnt);
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(cnt,3);
<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(z, 0, v); <SPAN class=cpp-keyword>SetStrToBox</SPAN>(v, 5); <SPAN class=cpp-keyword>Delay</SPAN>(1000);
<SPAN class=cpp-keyword>StrStackSetAt</SPAN>(z, 0, "modified");
<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(z, 0, v); <SPAN class=cpp-keyword>SetStrToBox</SPAN>(v, 5); <SPAN class=cpp-keyword>Delay</SPAN>(1000);
</PRE>

<P>Stack example 2:  Note that in the following example, the variable x is initialized with different values.  In the above example, variable is not initialized in the program.  The value of the variable is automatically initialized with the name of the variable when the program is executed.</P>
<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("a", x);
<SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 10); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 11); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 12);
<SPAN class=cpp-keyword>SetStrVal</SPAN>("b", x);
<SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 23); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 24); <SPAN class=cpp-keyword>IntStackPush</SPAN>(x, 25);

<SPAN class=cpp-keyword>IntStackGetVarCount</SPAN>(cnt);        <SPAN class=cpp-comment>// return 2, a and b</SPAN>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(cnt,1);

<SPAN class=cpp-keyword>IntStackGetVarValCount</SPAN>(a, cnt);  <SPAN class=cpp-comment>// return 3, three values 10, 11, and 12</SPAN>
<SPAN class=cpp-keyword>SetDecToBox</SPAN>(cnt,2);

<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(a, 0, val);   <SPAN class=cpp-comment>// return 10</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(a, 1, val);   <SPAN class=cpp-comment>// return 11</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(a, 2, val);   <SPAN class=cpp-comment>// return 12</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(a, 3, val);   <SPAN class=cpp-comment>// return 0</SPAN>

<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(b, 0, val);   <SPAN class=cpp-comment>// return 23</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(b, 1, val);   <SPAN class=cpp-comment>// return 24</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(b, 2, val);   <SPAN class=cpp-comment>// return 25</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(b, 3, val);   <SPAN class=cpp-comment>// return 0</SPAN>

<SPAN class=cpp-keyword>SetStrVal</SPAN>("a", x);
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 0, val);   <SPAN class=cpp-comment>// return 10</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 1, val);   <SPAN class=cpp-comment>// return 11</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 2, val);   <SPAN class=cpp-comment>// return 12</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 3, val);   <SPAN class=cpp-comment>// return 0</SPAN>

<SPAN class=cpp-keyword>SetStrVal</SPAN>("b", x);
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 0, val);   <SPAN class=cpp-comment>// return 23</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 1, val);   <SPAN class=cpp-comment>// return 24</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 2, val);   <SPAN class=cpp-comment>// return 25</SPAN>
<SPAN class=cpp-keyword>IntStackGetAt</SPAN>(x, 3, val);   <SPAN class=cpp-comment>// return 0</SPAN>
</PRE>

<P>Stack example 3:  Double array.  Each elements of stack is a variable that in turn is a stack.</P>

<PRE>

<SPAN class=cpp-keyword>StrStackPush</SPAN>(name, "name1"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(name, "name2");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(name, "name3"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(name, "name4");

<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(name, 0, x);
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name11"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name12");

<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(name, 1, x);
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name21"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name22");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name23");

<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(name, 2, x);
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name31"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name32");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name33"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name34");

<SPAN class=cpp-keyword>StrStackGetAt</SPAN>(name, 3, x);
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name41"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name42");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name43"); <SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name44");
<SPAN class=cpp-keyword>StrStackPush</SPAN>(x, "name45");

<SPAN class=cpp-keyword>SetStrVal</SPAN>("", all);

<SPAN class=cpp-keyword>while</SPAN>(0, cnt, <, 4, 1)

  <SPAN class=cpp-keyword>StrStackGetAt</SPAN>(name, cnt, x); <SPAN class=cpp-keyword>StrCatEl</SPAN>(all, "x", all);
  <SPAN class=cpp-keyword>StrStackGetVarValCount</SPAN>(x, valcnt);
  
  <SPAN class=cpp-keyword>while</SPAN>(0, k, <, valcnt, 1)
    <SPAN class=cpp-keyword>StrStackGetAt</SPAN>(x, k, y); <SPAN class=cpp-keyword>StrCatEl</SPAN>(all, y, all);
  <SPAN class=cpp-keyword>Wend</SPAN>();

  <SPAN class=cpp-keyword>StrCAtEl</SPAN>(all, STR_DA, all); 

<SPAN class=cpp-keyword>Wend</SPAN>();

<SPAN class=cpp-keyword>SendToClipBoard</SPAN>(all);

</PRE>

<P>Stack example 4:  Two dimensional array.</P>

<PRE>
<SPAN class=cpp-keyword>SetStrVal</SPAN>("0.2", a);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Whiles</SPAN>(0.1+a, n, &lt;, 6+6, 1+0.25)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>  StrStackPush</SPAN>(x, n);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>Wend</SPAN>()<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>StrStackCombine</SPAN>(x, " ", sv);<SPAN class=cpp-keyword> SendToClipboard</SPAN>(sv);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-comment>// 0.3 1.55 2.8 4.05 5.3 6.55 7.8 9.05 10.3 11.55</SPAN>
<SPAN class=cpp-keyword>StrStackArrayGetAt</SPAN>(x, 4, 1, 2, n);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(n, 1); <SPAN class=cpp-comment>// 7.8</SPAN>
<SPAN class=cpp-keyword>StrStackArrayGetCol</SPAN>(x, 4, 1, y);<SPAN class=cpp-keyword> StrStackCombine</SPAN>(y, " ", n);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(n, 2);    <SPAN class=cpp-comment>// 1.55 6.55 11.55</SPAN>
<SPAN class=cpp-keyword>StrStackArrayGetRow</SPAN>(x, 4, 1, y);<SPAN class=cpp-keyword> StrStackCombine</SPAN>(y, " ", n);<SPAN class=cpp-keyword> SetStrToBox</SPAN>(n, 3);    <SPAN class=cpp-comment>// 5.3 6.55 7.8 9.05</SPAN>
</PRE>


<H2>Command line parameters</H2>

<P>A script can have any numbers of parameters:</P>
<OL>
  <LI>The parameters follow the script file name (with extension) in the edit box. For example: <B>file_find.txt(dir_name)</B>.</LI>  
  <LI>The parameters are surrounded by parenthesis ().</LI>
  <LI>The parameters are separated by comma.</LI>
  <LI>The parameters are numbered from 1.  The number increases by 1 for each parameter.</LI>
  <LI>The parameters are used in script file by proceeding the number by $.</LI>
  <LI>All parameters are constant by default.  The string constant should not be surround by double quotes.  If the string is surrounded by double quotes, the double quotes are counted as the characters of the string.</LI>
</OL>

<P>For example, script file db_parameter.txt contains the following line:</P>

<PRE>SetStrToBox($1, 1); SetStrToBox($2, 2);</PRE>

<P>In the file name box, enter <SPAN class="textbox">db_parameter.txt(1, "test");</SPAN>.  After execution of the script file, box 1 will have 1, and box 2 will contain <B><I>"test"</I></B> since double signs are used in the second parameter.  $ sign variables are string variables.</P>

<H2>Bitmap commands</H2>

<P>All bitmap operations use a handle.  The value of this handle is obtained by bitmap functions.  It should never be changed explicitly by script.  However, the value can be checked to see if a operation is successful if the value is not -1.</P>

<P>All functions assume that the coordinates start from top-left corner until specifically specified. X-coordinate increases from left to right.  Y-coordinate increases from top to bottom. This is the same format as the MS Paint.  The coordinate of top-left corner is (0, 0), increase toward right and bottom.</P>

<P><B><SPAN class=cpp-keyword>LoadBmp</SPAN>(fn:svc, handle:iv);</B>  &nbsp;--&gt;
<CODE>LoadBmp</CODE> loads a bitmap file into memory. It returns a handle (a not-zero value) to data in the memory.  If a bitmap is not loaded correctly, the handle will be -1.  This handle is used for any command that manipulate the bitmap.  Multiple bitmap can be loaded at the same time with multiple <CODE>LoadBmp</CODE> command.</P>

<P><B><SPAN class=cpp-keyword>SaveBmp</SPAN>(handle:iv, fn:svc);</B> &nbsp;--&gt;
<CODE>SaveBmp</CODE> saves a bitmap to file.</P>

<P><B><SPAN class=cpp-keyword>GetBmpSize</SPAN>(handle:iv, width:iv, height:iv);</B> &nbsp;--&gt;
Return the size of the bitmap.</P>

<P>
<B><SPAN class=cpp-keyword>GetPixVal</SPAN>(handle:iv, x:ivc, y:ivc, val:ivc);</B><BR>
<B><SPAN class=cpp-keyword>SetPixVal</SPAN>(handle:iv, x:ivc, y:ivc, val:ivc);</B><BR> &nbsp;--&gt;
Get or set one pixel of a btimap.</P>

<P>
<B><SPAN class=cpp-keyword>GetPixValRight</SPAN>(handle:iv, x:ivc, y:ivc, val:ivc)</B>;<BR>
<B><SPAN class=cpp-keyword>SetPixValRight</SPAN>(handle:iv, x:ivc, y:ivc, val:ivc)</B>;<BR> &nbsp;--&gt;
Get or set one pixel of a btimap starting the count from right on the x axis.</P>
</P>

<P><B><SPAN class=cpp-keyword>CopyBmp</SPAN>(handlefrom:iv, handleto:iv);</B> &nbsp;--&gt;
Copy one bitmap to another bitmap.</P>

<P><B><SPAN class=cpp-keyword>Area</SPAN>(handle:iv, left:ivc, top:ivc, right:ivc, bottom:ivc);</B> &nbsp;--&gt;
Returns the rectangle area of a bitmap.  For example, Area(h, 10, 10, 50, 50); h will become a image with 40X40 in size.  The original image will be overwritten, so it may be good to run the command on the copy of a image using command <CODE>CopyBmp</CODE>.</P>

<P><B><SPAN class=cpp-keyword>CreateBmp</SPAN>(handlefrom:iv, width:ivc, height:ivc, val:ivc, handleto:iv);</B> &nbsp;--&gt;
Create an empty bitmap from the existing bitmap.  The dimension of the created bitmap will be the same as the source bitmap.</P>

<P>
<B><SPAN class=cpp-keyword>RotateBmp90</SPAN>(handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>RotateBmp180</SPAN>(handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>RotateBmp270</SPAN>(handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>FlipBmpVertical</SPAN>(handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>FlipBmpHorizontal</SPAN>(handle:iv);</B><BR> &nbsp;--&gt;
Rotate or flip a bitmap</P>

<P>
<B><SPAN class=cpp-keyword>SplitBmpX</SPAN>(handle:iv, cbleft:iv, cbright:iv, linex:ivc);</B><BR>
<B><SPAN class=cpp-keyword>SplitBmpY</SPAN>(handle:iv, cbleft:iv, cbright:iv, liney:ivc);</B><BR>
<B><SPAN class=cpp-keyword>CombineBmpX</SPAN>(cbleft:iv, cbright:iv, offset:ivc, des_handle:iv);</B><BR>
<B><SPAN class=cpp-keyword>CombineBmpY</SPAN>(cbtop:iv, cbbottom:iv, offset:ivc, des_handle:iv);</B><BR> &nbsp;--&gt;

<CODE>SplitBmpX</CODE> or <CODE>SplitBmpY</CODE> splits a bitmap into two bitmap images with handles <B>"cbleft"</B> and <B>"cbright"</B> along vertical line (X) or horizontal line (Y).  The <B>"linex"</B> or <B>"liney"</B> value should always be a positive number.  <CODE>CombineBmpX</CODE> or <CODE>ConbineBmpY</CODE> combines two bitmap images into one image.  The <B>"offset"</B> can be either positive or negative value.  If the value is positive, the first <I><B>"offset"</B></I> pixels of the second image will be ignored.  If the value is negative, the function will try to match the two images starting from <B>"offset"</B> number of pixel until a match is found.  if there is no match, the <B>"offset"</B> is set to 0, then two images are combined.</P>

<P>
<B><SPAN class=cpp-keyword>ClearBmpEdges</SPAN>(handle:iv, left:ivc, top:ivc, right:ivc, bottom:ivc, val:ivc);</B> &nbsp;--&gt;

<CODE>ClearBmpEdges</CODE> sets the pixel to val on each side determined by the four parameters.  The left parameter means the area on the left from 0 to <B>"left"</B> pixel is set to val.  The right parameter means the area on the right from <B>"right"</B> pixel to the right edge is set to val.  For example, if right is the width minus one, only 1 pixel on the right is set to val.  The bottom and top parameter have the same means.</P>

<P><B><SPAN class=cpp-keyword>ClearBmpEdgesWidth</SPAN>(handle:iv, left:ivc, top:ivc, right:ivc, bottom:ivc, val:ivc);</B>
&nbsp;--&gt;<CODE>ClearBmpEdgesWidth</CODE> sets the pixel to val on each side determined by the four parameters.  Each parameter specifies how wide on each edge is set to val.</P>

<P><B><SPAN class=cpp-keyword>ClearBmpArea</SPAN>(handle:iv, left:ivc, top:ivc, right:ivc, bottom:ivc, val:ivc);</B> &nbsp;--&gt;
<CODE>ClearBmpArea</CODE> sets the pixel to val inside the rectangle determined by the four parameters.</P>

<P>
<B><SPAN class=cpp-keyword>AreaMarginsSize</SPAN>(handle:iv, minwidth:ivc, minheight:ivc);</B><BR>
<B><SPAN class=cpp-keyword>AreaMarginsEdges</SPAN>(handle:iv, left:ivc, top:ivc, right:ivc, bottom:ivc);</B><BR> &nbsp;--&gt;

<CODE>AreaMarginsSize</CODE> and <CODE>AreaMarginsEdges</CODE> start from the most outside edges of the four edges, counts the number of pixels on each lines parallel to the edges.  Take the example of the left edge, the function starts from 0, counts the number of pixels on the first vertical line.  If the number of pixel on this vertical line is greater than margin_pix (deafult=5, meaning this vertical line may hit the text already), the a counter is increased.  If the counter value is ever increased by greater than margin_cnt, the process stops.  The white area on the left is defined by moving back (to left) by the sum of margin_cnt and margin_val (some extra).  For the right side, the process starts from the most right vertical line, move towards the left side.  It is seen that margin_val adds extra on all four edges.  After all four edges are done, the area is resized by the four edges found to eliminate the white margins of the image.  The minimum area is limited by the size parameters (width and height) with command <CODE>AreaMarginsSize</CODE> or four maximum edges with command <CODE>FindMarginsEdges</CODE>.  <CODE>SetMarginsParam</CODE> sets up the criteria for counting.  The parameters minwidth and minheight in AreaMarginsize limits the minimum area of the bitmap (no less than the width and height specified).  The parameters in AreaMarginEdges limits the maximum white area on all four sides, thus limits the minimum area of the bitmap. Example: </P>
<PRE>
<SPAN class=cpp-keyword>LoadBmp</SPAN>("C:\ssx.bmp", h);<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>SetMarginsParam</SPAN>(2, 2, 5)<SPAN class=cpp-comment></SPAN>
<SPAN class=cpp-keyword>AreaMarginsSize</SPAN>(h, 30, 30);  <SPAN class=cpp-comment>// or</SPAN>
<SPAN class=cpp-comment>//AreaMarginsEdges(h, 20, 20, 20, 20);</SPAN>
<SPAN class=cpp-keyword>SaveBmp</SPAN>(h, "C:\ssx2.bmp")<SPAN class=cpp-comment></SPAN>
</PRE>

<P><B><SPAN class=cpp-keyword>SetMarginsParam</SPAN>(margin_pix:ivc, margin_cnt:ivc, margin_val:ivc)</B> &nbsp;--&gt;

<CODE>SetMarginsParam</CODE> sets up the three parameters.  The default values are margin_pix=5; margin_cnt = 5; margin_val = 10;</P>

<P><B><SPAN class=cpp-keyword>RemoveIsolatedPix</SPAN>(handle:iv);</B><BR></P>

<P><B><SPAN class=cpp-keyword>BmpTYpe</SPAN>(handle:iv, type: iv);</B> &nbsp;--&gt; Return the type of the bitmap, or the number of bit for each pixcel.  The value can be 1, 4, 8, 16, 24, and 32.</P>

<P><B><SPAN class=cpp-keyword>ChangeBmpRange</SPAN>(handle:iv, from:iv, to:iv, changeto:iv);</B> &nbsp;--&gt; Change the bit value of a bitmap.  If the bit is in the range "from" and "to" (inclusive), change it to value "changeto".</P>

<P><B><SPAN class=cpp-keyword>ConvertBmp</SPAN>(handle:iv, bitCount:iv, val:iv, changeto:iv);</B> &nbsp;--&gt; Convert a bitmap image from one format (for example, 24 bit) to another (for example 4 bit).  Right now, it can only convert to 1 bit (black/white) image from other bitmap image formats.  "handle" is the source image handle to be converted.  "bitCount" is the destination format.  It should be always set to 1 (black/white image).  "val": value to compare with the pixel value in image.  If the value at a pixel position is greater than the "val", the value in the converted image at the same pixel position is set to 1.  Otherwise, the value is set to 0.  "ChangeTo" is the handle of the converted image.  With this handle, other operations can be performed on the converted image (for example, save the image to a file).  The "val" takes different formats: For 32 and 24 bit image, "val" is in format 0xa0a0a0 (three bytes).  For 8 bit image, "val" is in format 0xa0 (one byte, from 0 to 255).  For 4 bit image, "val" is in format 0xa (from 0 to 15).</P>

<P>
<B><SPAN class=cpp-keyword>FindBmpMargins</SPAN>(handle:iv, left:iv, top:iv, right:iv, bottom:iv);</B><BR>&nbsp;--&gt;
<CODE>FindBmpMargins</CODE> find the margins.</P>

 
<H2>Tips and tricks</H2>
<OL>

<LI>
<P><B>How to close a window:</B></P>
<P>Three commands can be used to close a window:</P>
<PRE>
SendMessage(hwnd, WM_CLOSE, 0, 0);
PostMessage(hwnd, WM_CLOSE, 0, 0);
CloseWindow(hwnd);
</PRE>
<P><CODE>CloseWindow</CODE> is the same as <CODE>PostMessage</CODE>(hwnd, WM_CLOSE, 0, 0).  For some window, <CODE>SendMessage</CODE> may not work.  <CODE>PostMessage</CODE> may be used to close the sindow.</P>
</LI>

<LI>
<P><B>Pre-defined string:</B></P>
<P><B>STR_DA</B>: Contains characters 0xd and 0xa.  This is the carriage return in Window system.</P>
<P>StrReplaceAll(text, STR_DA, "", text); replaces all Carriage Return with nothing.</P>
<P><B>STR_AD</B>: Contains characters 0xa and 0xd.</P>
<P>StrReplaceAll(text, STR_AD, "", text); removes multiple Carriage Return.</P>
<P><B>EditorName</B>: the editor name used for editing the script: SetStrToBox(EditorName, 4);</P>
<P><B>ScriptPath</B>: the path where the script is stored.<P>
<P><B>ScriptName</B>: the name of the script.<P>
<P><B>ProgPath</B>: the UtilProg path where it started.<P>
<P><B>M_PI</B>: the value of PI (3.1415926535897932384).<P>
<P><B>M_E</B>: the value of natural e (2.718281828459045).<P>
<P><B>STR_D</B>: Contains characters 0xd.</P>
<P><B>STR_A</B>: Contains characters 0xa.</P>
<P><B>STR_DQ</B>: Contains double quote characters 0x22.</P>
<P><B>STR_SQ</B>: Contains single quote characters 0x27.</P>
<P><B>STR_TAB</B>: Contains TAB characters 0x09.</P>
</LI>

<LI>
<P><B>Pre-defined integer:</B></P>
<P><B>HUTILPROG</B>: Contains the handle of UTILPROG.</P>
</LI>

<LI>
<P><B>Create an infinite loop:</B></P>
<PRE>
while(0, 0, ==, 0, 0)
  .................
wend()
</PRE>
</LI>

<LI>
<P><B>Create string variable that contains a single character (especially special character):</B></P>
<PRE>
StrCatChar("", '\t', 1, s);
</PRE>
</LI>

<LI>
<P><B>Multiply entries of subroutine:</B>Multiply subroutine names can have one RETURN as in the following example:</P>
<PRE>
Sub("INIT")
  SetIntVal(20, x);
Sub("INIT1")
  SetDecToBox(x, 1);
Return();
</PRE>
<P>If GoSub("INIT") is called, the variable is initialised with value 20.  If GoSub("INIT1") is called, the calling routine must initialise the variable x.  Otherwise, the value of variable is 0.</P>
</LI>

</OL>


<p><HR></p>

<H2>Backup files:</H2>
<P>Backs up files from one directory to another.  The following describes how the backup works:</P>

<P>To backup, three directories are required:</P>
<UL>
<LI><B>Dir to back</B>:  The directory to be backed up.</LI>
<LI><B>Old directory</B>: The old directory previously backed up.</LI>
<LI><B>New directory</B>: The directory where the new backup should be.</LI>
</UL>

<P>The program searches all files in the <B>Dir to back</B> and its sub-directories, compares each file with
file in exact location in <B>OlD directory</B>.  If the two files are different, the file in <B>Dir to back</B>
will be copied to <B>New directory</B>.  The comparison criteria is file size and modified date and time.
In this way, any file in <B>Dir to back</B> that is newer than that in Old directory, or that does not 
exist in <B>Old directory</B>, will be copied to <B>New directory</B>.  <B>Old directory</B> and 
<B>New directory</B> can be the same.  In this case, the files in <B>New directory</B> (or
<B>Old directory</B> since they are the same) will be overwritten.</P>

<P>If there are many directories to be backed up, these directories can be placed in a file, then
<B>In file</B> is checked for backup.  Each directory takes one line.  The program will read three non-empty lines 
each time, interprets as <B>Dir to back</B>, <B>Old directory</B> and <B>New directory</B>, and performs the backup 
by these three directories.  Empty line is ignored so that empty line can be inserted every three lines 
for readability.  In this case, the text boxes for <B>Dir to back</B>, <B>Old directory</B>, and 
<B>New directory</B> contain the same file.</P>

<P>If <B>Log file</B> is checked, the names of the backup files will be written in a file in the first 
Dir to back directory.</P>

<P>If <B>Delete backed</B> is checked, any file that is backed up in Dir to back will be deleted.</P>

<P><B>Exist Dir:</B> If it is checked, files in <B>Dir to back</B> are only copied to <B>New directory</B> if the directory exist in <B>New directory</B>.</P>

<P><B>Last:</B> If it is checked, only files modified in the last few days are copied to <B>New directory</B>.</P>


<p><HR></p>

<H2>Find string:</H2>

<ol>
<li><B>Mid</B>: Find all text between two strings in the edit boxes, inclusively</li>
<li><B>Left</B>: Find all text to the left of the string in the edit box, 
    i.e. from the beginning of the line to the string, inclusively</li>
<li><B>Right</B>: Find all text to the right of the string in the edit box, 
    i.e, from the string to the end of the line, inclusively</li>

<li><B>Contain</B>:  Find the whole line that contains the string</li>
<li><B>M</B>: Find the M string.</li>
<li><B>P</B>: Find the P string</li>
    <ul>
      <li>If the text box is empty, and wether M or P radio is checked, the text box
          is automatically filled.  The contents can be modified.</li>

      <li>If HTTP is checked, find all text between HTTP:// and M or P file, inclusively</li>
      <li>If HTTP is not checked: 
        <ul>
          <li>If the string is not empty (src=", for example), find all text between the 
              string and M or P file.</li>
          <li>If the string is empty, find the whole line that contain M or P string</li>
        </ul>
      </li>
    </ul>
<LI><B>Whole directory</B>: If it is checked, all files in the directory that has the same extension will be
searched for the string.</LI>
<LI><B>Line number</B>: If it is checked, the line number is inserted at the beginning of the line in the ouput file.</LI>
</li>
</ol>

<p><HR></p>

<H2>Rename:</H2>

Rename files in a directory.  To use the function, Select a file from a directory.  
The action applies to all files in the directory.
<ol>
<li><B>... button</B>: Pop up a file dialog box to allows selection of a file, and put the selected file
in the text box on the left after the dialog is dissmised.</li>
<LI><B>All files in the directory</B>:  If it is checked, all file in the directory will be changed.
Otherwise, only those file with the same extension are changed.</LI>
<li><B>Change ext</B>: Change the extension of all files in the directory to the type in the 
           text box next to the button.<br>
           <I>Example</I>: Change all files in the directory to htm</li>
<li><B>Add Pfx</B>: Add a prefix to all files in the directory with text in the text box.</li>
<li><B>Rename</B>: Rename the file names according to the contents stored in a file.  This
    file is selected by clicking the ... button.  Each lines in the file has three parts.
    The first part is the original file name, then three characters, TAB(\t)$&$&TAB(\t),
    then followed by the file name to be renamed.  These four characters and the
    TABs proceeded and followed the characters are just delimiters.
    The file name inside the file should not include the directory name.  The following
    is an example line:
    <br>
    <br>20075714362511.mp3&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp$&$&&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp望春风.mp3
    <br>
    <br>The original file name can be obtained by 3.</li>
<li><B>Seq dirs</B>: Rename the directory in sequence.  The vlaue in text box is the start number 
           for the directory name.  The directory name is always 4 digits.  For example, 
           if the value is 3, the directory will be renamed as 0003, 0004, ...</li>
<li><B>Seq files</B>: Change the file name of all files in the directory to the digit sequence with
           the number of digits in the text box.  For example, if the text box is 5, the files
           in the directory are sequenced as 00000, 00001, ...  The extension of the file
           will not be changed.  The number in the next edit box is the start number.</li>
<LI>The next four radio button and the in down order checkbox allpied to all actions above. They determines
if the original file name or directory name are searched by <B>Name</B>, <B>Size</B>, <B>Type</B>, 
or <B>Time</B>, and if they are <B>in down order.</B></LI>

</ol>

<p><HR></p>

<H2>File name changes:</H2>
<ol>
<LI><B>...</B>: to select a file in a directory and put the file selected in the text box.</LI>
<li><B>Repace %20 with spze</B>: Replace text %20 in a file name with a space.</li>
<li><B>Remove last chars</B>:  Remove last chars of the file name. The text box next specifies how many character are removed</li>
<li><B>Remove chars contained</B>: Remove characters in a files name. These characters are entered in text box next to it</li>
<li><B>Remove dir chars at end</B>: Remove chars at the end of a directory.  If the directory
        does not contain the chars, keep it unchanged.</li>
</ol>

<p><HR></p>

<H2>File Format</H2>

<P>This page mainly works on text file. Sometime when a file is copied from a HTML, each line is a paragraph.  The real 
    paragraph has lots of lines (paragraph).  If the captured file (.txt) is resized,
    each line will run across two or more lines, with the last line being incomplete.
    It is desirable to remove the carriage return at the end of the line so that the 
    paragraph ends at the real paragraph.  This page performs the reformating function.</P>
 
<P>The separatation of the true paragraph can be a empty line, a line with space at
    the begin.</P>

<ol>
<li><B>...</B>:Select the file to be converted.</li>
<LI><B>All files</B>:  Apply the action to all files in a directory if it is checked.</LI>
<li>Click the correct checkbox:
    <ul>
       <li><B>Keep empty lines</B>: Sometimes, there are lots of continuous empty lines in a file.
          This option allows these lines to be removed with some line left.
          To remove the uncessary lines, check the Keep empty lines, enter the minimum
          lines lines to be left in the edit box. </li>

       <li><B>Add empty lines</B>: To add empty lines between paragraph, use the Add Lines option.  
          The number of empty lines added is in the edit box.
		  <br>Note that <B>Keep empty lines</B> and <B>Add empty lines</B> share the same edit box.
		  </li>

       <li><B>Remove lines</B>: This option removes lines less than, equal to, or greater than certain
          characters.  The comparison text box can be <=, >=, ==, <, or >.  The next text box is
          the number of characters.</li>

       <li><B>Empty line</B>:  If the true paragraph is seperated by empty lines, check this one.
           number of the empty lines that seperates the prargraph can be entered in the box.</li>
       <li><B>Initial space</B>: If there are some space at the beginning of the true paragraph,
           This option may be used.  The number of space can specified in the text box.</li>
       <li><B>At least chars</B>: If the number of characters are less than that in the text box
           This also marks a true paragraph.</li>
       <li><B>All files</B>: If this option is checked, do the changes for all the files in the
          directory if the file selected has not an extension.  If the file has an extension,
          all the files with the same extension will be changed.  If this option is not
          checked, only the file in the text box is changed.</li>
    </ul>
<li>Click the Start button to do the changes.</li>
</ol>

<H3>Notes: option priority</H3>

<ol>
<li><B>Keep empty lines</B>: if this option is checked, other options do not have any effect.</li>
<li><B>Add empty lines</B>: Uncheck Keep empty lines, and check this option.</li>
<li><B>Remove lines</B>: Uncheck both Keep empty lines and Add empty lines, and check this option.</li>
<li><B>Last three options</B>: Uncheck Keep empty lines, Add empty lines, Remove lines. The last three
    options work as a group.</li>
</ol>

<H3>Functions on the right hand side are for formatting unicode:</H3>


<P>When the selection is None, it works the way as above.  Otherwise, it works in one of
    the folowing cases.</P>
<ol>
<li><B>Remove unicode</B>:  Remove unicode test, just leave english.</li>
<li><B>Keep unicode</B>: remove english, just leave unicode.</li>
<li><B>Remove unicode line</B>: remove any paragraph that contains unicode.</li>
<li><B>Keep unicode line</B>: keep any paragraph that contains unicode.</li>
<li><B>Swap bytes</B>: swap between big endian and small endian.</li>
</ol>

<p><HR></p>

<H2>Delete repeat file</H2>

<P>Upper part is used to find repeat file in different directory and subdirectory.
    The repeat files are put in a file called FileName.TXT in the last directory.
    This text file can be viewed and modified, then files in the FileName.TXT can 
    be deleted with the Delete button in the lower part.</P>
<ol>
<li><B><..></B>: open a dialog box to select a directory and put in the text box below.
    <br>Multiple directory can be added to text box by repeatedly using of this button.</li>
<li><B>Del</B>: Delete an item selected in text box.</li>
<li><B>Clear</B>: Remove all items in the text box.</li>
<li><B>Find</B>: Start finding all the repeated files in the directory in the text box.
    There are two ways to find the repeat files: A. Just compare the file size by
    check the size check box.  B: Compare the file size and contents by unchecking
    the check box.  The results are placed in file FILENAME.TXT in the last 
    directory in the text box.</li>
<li><B>Exist</B>: Compare the files in the last direstory with other directories in
    the list box.  Put the result in file FILENAME.TXT in the last directory.
    All the files in the last directory are listed in the file.  If there are
    same files (contents) in other directories, these files will be listed
    together.
    <br>At least two items must be entered in the edit box  to enable the Exist button.
<li><B>Merge</B>: Merge the files in directories to the first dierectory.  The directories
    can be entered in the edit box or in a file.  Files in the subdirectories will
    not be merged.</li>
<li><B>Size</B> check box: When this box is checked, only file sizes are compared.</li>
<li><B>Sub dir</B> check box: When this box is checked, only files in sub directories 
    are also compared.</li>
</ol>

<P>The functions at the bottom part of the dialog only work on the contents in a file:</P>
<ol>
<li><B>...</B>: Open a dialog box to select a file.  Then put the file name select in the
    text box below.</li>
<li><B>Remove</B>: Remove repeat files in directory entered in the edit box.  Only directory
    and file extension are important (for example, c:\test\ or c:\test\*.txt).  If the file in the edit 
    box has an extension, only the repeat files with the same extension are removed.
    If only directory is entered in the text box, the last character must be a back slash.<br>
	In this case, all files in directory are compared and the repeat files are removed.
	Note that the file removed will be random.  For example, if file.txt and file1.txt
    are the same, which file is removed is completely random.</li>
<li><B>Delete</B>: Delete all files who names are listed in a file in the text box. 
    This file can be generated from Find or Exist button, or any other method.
    Two options are added for this button:  This and Not.  Also a text box is added
    so that a directory name can be placed here.  The following options determine 
    which files are to be deleted:
	<UL><LI>If none of the options are checked, all files listed in the file in the text 
	box will be deleted.  </LI>
	<LI>If both options are checked, only the first file in the group is kept, the rest of the files in
    the group will be deleted. </LI> 
	<LI>If This option is checked, only files with the same path name as in the directory text box are deleted.</LI>
	<LI>If Not option is checked, all files with path name differnt from the directory text box will be deleted.</LI></UL>
    Example:  a.txt, b.txt, and c.txt are the same, and reside in directories
    x, y, and z, respectively.  These files are listed in file FileName.txt
    as a group seperated by an empty line.  The directory text box is x.
    If none of the options are checked, all three file will be deleted.  
    If This option is checked, only a.txt is deleted.  If Not is checked, 
    both b.txt and c.txt will be deleted. If both options are checked, only
    a.txt is kept since it is the first file in the group.  b.txt and c.txt
    are deleted.  If b.txt is the first file in the group, a.txt and b.txt
    will be deleted.
    <br>
    <br>Note the three files are listed in the file in one group.  If they are not in the
    same group, the options will not work.  But delete all option still works.
    If any of the options or both of the options are checked, the contents of
    file that contains files to be deleted are grouped with the blank line as
    seperator.  This file is normally generated with Find or Exist button.
    <br>
    <br>The directory name in the directory edit box must end with a back slash, and
    the directory name must be exactly the same as one of the directory in the
    file (case sensitive).</li>

<li><B>Merge directory</B>:
    <br>There are two Merge buttons:
    <ul>
    <li>The top one merges directory entered in the list box.  At least two directories
        must be selected.</li>
    <li>The bottom Merge button merges directories in a file.  The directory can be many
        groups separated by an empty line.  Each group must have at least two directories.</li>
    </ul>

    Note:
    <ol>
    <li>Merge only work at the current directory.  It does do anything to the 
        subdirectories.</li>
    <li>Merge will merge all the directories to the first directory.  Then delete
        any other directories except the first directory.</li>
    </ol>
</li>
</ol>

<p><HR></p>

<H2>Delete file</H2>

<OL>
<LI><B>...</B>: Select a file and put the file in the text box</LI>
<LI><B>Subdirectories</B>: If it is checked, the procedure interates through the subdirectories.</LI>
<LI><B>Ext</B>: Specify the file extension that will be deleted. The file extension should be separted by comma, for example txt,html,exe.  note that there is no space between extensions.</LI>
<LI><B>Except</B>: If it is checked, those files with extension different from the specified extension will be deleted.</LI>
<LI><B>Size</B>: If it is checked, file size is compared with specified size in bytes.  If the result is true,
the file is deleted.  The file comparison can be >=, <=, ==, <, and >.</LI>
</OL>

<p><HR></p>

<H2>Delete directory:</H2>
<P>Delete directory works on two directories, a <B>Directory to be deleted</B> and a <B>Reference directory</B>. The program searches every file in <B>Directory to be deleted</B>, then compares with <B>Reference directory</B>.  If the the file exists in <B>Reference directory</B> in exactly the same directory hierarchy, the file in <B>Directory to be deleted</B> will be deleted.</P>

<P>If <B>Delete empty directory</B> is checked, any empty directory in <B>Directory to be deleted</B> will be deleted.  In this case, Only <B>Directory to be deleted</B> needs to be filled.</P>

<P><B>Exact path hierarchy:</B> If it is checked, files in <B>Directory to be deleted</B> is checked against the files in <B>Preference directory</B> in the exact path.  If it is not checked, a file in <B>Directory to be deleted</B> will be deleted as long as a same file (contents) exists in <B>Preference directory</B>.</P>
<p><HR></p>


<p><HR></p>

<H2>Get file name:</H2>

Get the file name in a single directory.  Put the result in file FileName.txt.
<br>The name sequence in file FileName.txt can be ordered in name, size, type, 
    or time modified.  If size, type, and time modified are the same, the name 
    will be ordered from a to z.
<br>If the type of the files are entered in Type text box, only one type can be used and
    it must in the following format: *, *.txt, or *.htm, or *.doc.
<br>
Check box options:
<br><B>Full path</B>: If the full path is necessary, check this option.  
The file name obtained looks like c:/test/file.txt...
<br><B>Dir</B>:  The file obtained indcludes subdirectory name under.
<br><B>Dir</B>:  The file obtained indcludes file name under.
<br><B>Sub</B>:  File name and subdirectory name in subdirectory are all obtained.
<br><B>Space</B>: Only applicable if <B>Sub</B> is checked.  Separate each subdirectory with an emply line.

<p><HR></p>

<H2>Change Paint format:</H2>

<H3>Procedure to change the formats of a picture</H3>
<OL>
<LI>Generate picure files in a certain directory.</LI>
<LI>Run Paint.  Open one of the files in the above directory.  This will set up the correct
     directory for Paint to work.  This is very important.</LI>
<LI>Move Paint to upleft corner.  This is also important.</LI>
<LI>Select output format to be converted.</LI>
<LI>Click the Browse button to select a file in the directory.</LI>
<LI>Click Start button to start the convert procedure.</LI>
</OL>
Notes:
<OL>
<LI>All file in the directory with the same extention will be converted.</LI>
<LI>Any file name that is the same as the output file name in the directory will be deleted.</LI>
<LI>When converting file to a diferent format, some corlor may be lost.  For example, when
       converting a 24-bit BMP file to Monochrome BMP, all the colors will be lost.  In this
       case, Paint will ask if you want to do so.  Check the Add Yes for this purpose.</LI>
<LI>For item 3, it is suggested to open a file and save is to the taarget format manually.
      If Paint asks to confirm the color loss, Add Yes button should be checked.</LI>
</OL>
<p><HR></p>

<H2>HTML directory:</H2>
<P>When an html file is saved, the html text is saved in a file.  A directory associated with
this html text file is also created.  The directory name is uaually the html test file name plus
_files. All image files and maybe other files are saved in this directory.
In html text file, these images and other files are linked to the directory.
It may be desirable sometimes to put all files in the same directory.  This page performs
such a function.  It moves the html text file to the associated directory.  Then searches the file for 
anything related to the directory created and change the directory to the current directory.</P>
<OL>
<LI><B>...</B>: Select html files and put them in Directory box.</LI>
<LI><B>Files in file</B>: only those html files in a file will be changed.</LI>
<LI><B>Whole directory</B>: All html files in the directory will be changed if this is checked.</LI>
<LI><B>Sub dir</B>: The change will iterate through subdirectories.</LI>
<LI><B>Change button</B>: Perform the change.</LI>
<LI><B>Delete button</B>: Delete the html text file and the directory associated with this file and its 
sub-directories.</LI>
</OL>
If a html text file does not have any directory associated with it, the file will not be changed
or deleted.

<p><HR></p>
<H2>Remove html tag:</H2>
<P>When a web page is saved, it may contain many unnecessary contents.  This page is designed
to remove these contents or to extract useful contents.</P>
<OL>
<LI><B>...</B>: Select a file and put it in the In directory box.</LI>
<LI><B>In directory</B>: contain the file selected.</LI>
<LI><B>Whole directory</B>: perform the function on all files in the directory if this is checked.</LI>
<LI><B>Overwrite orignal</B>: The output will be written back to orignal file if this is checked.
Otherwise, the output is written to FindText.html.</LI>
<LI><B>Extract</B>: The tag is extracted into a file if this is checked.</LI>
<LI><B>Tag</B>: html tag to be extracted or removed.</LI>
<LI><B>Level</B>: Because a html tag may contain the same tag inside, this box contains the number of levels.
If the number is positive, the level is counted from the first tag from the top.  If the level
is negative, the level counted from the inside tag that is closest to the text.</LI>
<LI><B>Text box</B>: An unique text string the tag contains for searching.</LI>
</OL>

<p><HR></p>
<H2>Generate Html from images:</H2>
Searches for all image file with the same extension, generates an html file.
<p><HR></p>
<H2>Concatinate files:</H2>

<P>Concatinate many files into the output file TMP$$$$.txt.  Files must be <B>text</B> files.</P>

<OL>
<LI><B>...</B>: Selects the files to be concatinated.  Multiple files may be selected.</LI>
<LI><B>In directory</B>: Contains the files selected.</LI>
<LI><B>Delete</B>: Deletes a file from the selected list.</LI>
<LI><B>Files in file</B>: Indicates the files to be concatinated are in a file.</LI>
<LI><B>U button</B>: Moves the file up in the sequence.</LI>
<LI><B>D button</B>: Moves the file down in the sequence.</LI>
</OL>

<p><HR></p>
<H2>Replace Tab:</H2>
<P>Replaces the TAB with spaces.</P>
<OL>
<LI><B>Tab size to be replaced</B>: Enter the numner of characters to replace the tab.</LI>
<LI><B>In directory</B>: The file name selected to be replaced.</LI>
<LI><B>Replace all tab</B>: If it is checked, all tabs in a line will be replaced.  If it is not checked, only the initial tabs in a line will be replaced.</LI>
<LI><B>All files</B>: The above options apply to the files in the directory with the same extension.</LI>
</OL>

<p><HR></p>
<H2>Replace Text:</H2>
This page replaces text in a text file or an unicode text file.

<OL>
<LI><B>...</B>: Pops up a file open dialog for selecting files.  Multiple files can be selectd by holding down SHIFT key or CTRL key.</LI>
<LI><B>Directory box</B> will be filled when a file is selected.</LI>
<LI><B>Whole directory</B>: If this is checked, the whole directory will be searched for files to change. If the file selected in step 1 has an extension, only those files with the same extension will be changed. If the file selected does not have an extension, any file found will be changed. In this case, only the first file in <B>Directory box</B> is used for the extenstion check if multiple files are selected.  The rest of the files will be ignored. If <B>Whole directory</B> is not checked, only those files listed in the Directory box are changed</LI>
<LI><B>Special code</B>: Special code can be buried in the replace text.  These codes can be \r, \n, and \t. Hex number can also used as the special code.  The number must start with 0x followed by fourhex digits.  So 7 characters are need for speical code.  For example, the replace text can be "<I>test\r\ntext</I>".  If Special code is not checked, the replace text will be exactly "<I>test\r\ntext</I>". If Special code is checked, the replace text is <I>test</I> plus carriage return plus <I>text</I>.  As another example, the above replace string can be "<I>test\0x000d\0x000atext</I>" if Special code is checked.  Hex number with less than four digits will be ignored.  For example, <I>\0x00dz</I> will bot be treated as special code, but as text. Note that it requires two special code \r\n\ or \0x000d\0x000a to insert a new line.</LI>
<LI><B>Find</B>: the original string to be replaced.</LI>
<LI><B>Rep</B>: the replace string.</LI>
</OL>

<p><HR></p>
<H2>Convert Notepad format:</H2>
This page converts a Unix text file into a text file readable by Notepad.

<p></p><HR align="left">
<H2>IEEE convert:</H2>
This page converts between a floating number and IEEE integer number.

<p><HR></p>
<H2>Hex dump:</H2>
This dumps a hex file to to a text file.

<p><HR></p>

<H2>Download the whole page links:</H2>
<OL>
<LI>Save the page.</LI>
<LI>Search the link with http:// and .html.  (or type in the search string html
      and check the HTTP.) Sometime the name may be just .htm</LI>
<LI>Download the the html (htm) files.</LI>
<LI>Search http:// and picture files. Sometimes the picture file use a relative path.
      For example, the picture file in the html may look like
      src="images/pictureFileName.gif".  So search for src=" and .gif. 
      In this case, open the the web page (not the one downloaded), select the picture, then
      right click and select property, the address shown may be:
      http://www.contextures.com/images/pictureFileName.gif
      So change src=" to http://www.contextures.com to form the link to the pictures.</LI>
<LI>Download the image file</LI>
<LI>Make necessary change in .html to the image directory.  In this case replace
      all images/ with nothing since images and the html are in the same directory.
      Images are not in the sub-directory</LI>
</OL>


</HTML>
