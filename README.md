<div align="center">

## Creating a comfortable ToDo list in "Visual C\+\+" using "Visual C\+\+" macros \(Not an add\-in\)\.


</div>

### Description

Using this tutorial you will be able to create a ToDo file wich writes the dates and marks the done tasks. All this using macros.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Vitaly](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/vitaly.md)
**Level**          |Beginner
**User Rating**    |4.2 (21 globes from 5 users)
**Compatibility**  |Microsoft Visual C\+\+
**Category**       |[Macros](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/macros__3-28.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/vitaly-creating-a-comfortable-todo-list-in-visual-c-using-visual-c-macros-not-an-add-in__3-1204/archive/master.zip)





### Source Code

First of all about the picture.<br>
What you have used to see as Breakpoint, means in this task list a ToDo task. The first date is the date you added the Task to ToDo, the second date is when you finished the task.<br>
<br>
Before we start you have to choose your Todo file. Just create an empty text file, in the program I will refer to it as <b>[filename]</b>, remember to replace it with your file name. The path to the file will appear as <b>[path]</b> in the tutorial and so you have to replace it as well with your path.<br>
An example to <b>[filename]</b> is: <b>Todo.txt</b><br>
An example to <b>[path]</b> is: <b>C:\Todo.txt</b><br>
<br>
Lets start with the real thing now.<br>
Go to your macro file (.dsm) and add the following sub to it:
<pre><code><font color="#000000">
Sub OpenTodoList()
<font color="#008000"><b>'DESCRIPTION: Opens the todo.</b></font>
  Documents.Open <font color="#0000a0"><b>&quot;[path]&quot;</b></font>, <font color="#0000a0"><b>&quot;Text&quot;</b></font>
End Sub
<b>Remember to replace the path with the path to your text file just like in the example</b>
</font>
</code></pre>
When you run it, the macro will open the text file which you will be using as your ToDo file.<br>
If you wish create now a button on the toolbar of "Visual C++" that will run this macro.<br>
<br>
Now lets go for the second macro, again go to the macro file and add the following Sub to it:
<pre><code><font color="#000000">
Sub WriteDate()
<font color="#008000"><b>'DESCRIPTION: Writes the date, duh.</b></font>
  ShortName=ActiveDocument.Name
  If ShortName=<font color="#0000a0"><b>&quot;[filename]&quot;</b></font> Then
   Line = ActiveDocument.Selection.CurrentLine
   Column = ActiveDocument.Selection.CurrentColumn
   <font color="#008000"><b>'Finding the bottom</b></font>
   ActiveDocument.Selection.SelectAll
   Bottom = ActiveDocument.Selection.BottomLine
   ActiveDocument.Selection.GoToLine Line
   <font color="#008000"><b>'Find the place for the date</b></font>
   Do
     ActiveDocument.Selection.LineDown
     ActiveDocument.Selection.StartOfLine
     ActiveDocument.Selection.CharRight dsExtend
   Loop Until ActiveDocument.Selection = <font color="#0000a0"><b>&quot;*&quot;</b></font>
   ActiveDocument.Selection.LineUp
   ActiveDocument.Selection.EndOfLine
   ActiveDocument.Selection = <font color="#0000a0"><b>&quot; (&quot;</b></font> &amp; CStr(Date) &amp; <font color="#0000a0"><b>&quot;)&quot;</b></font>
   <font color="#008000"><b>'Find the place to do the BreakPoint</b></font>
   ActiveDocument.Selection.LineDown
   Do
     ActiveDocument.Selection.LineUp
     ActiveDocument.Selection.StartOfLine
     ActiveDocument.Selection.CharRight dsExtend
   Loop Until ActiveDocument.Selection = <font color="#0000a0"><b>&quot;*&quot;</b></font>
   ExecuteCommand <font color="#0000a0"><b>&quot;DebugToggleBreakpoint&quot;</b></font>
   <font color="#008000"><b>'Moving back</b></font>
   ActiveDocument.Selection.GoToLine Line
   ActiveDocument.Selection.CharRight dsMove, Column
  Else
   ExecuteCommand <font color="#0000a0"><b>&quot;DebugToggleBreakpoint&quot;</b></font>
  End If
<b>Remember to replace the path with the path to your text file just like in the example</b>
</font>
</code></pre>
This is the important macro of the program, it will simulate regular Breakpoint for your programs, however, for your ToDo file it will work in a special way.<br>
To continue go to Visual C++ costumize and assign the key F9 to that macro (WriteDate in this tutorial). Now you try to use F9 in your programs and you'll see that it works as usual (just to make sure).<br>
The format of the tasks in the ToDo file has to be in a specific format if you want it to work as planned:<br>
- Every task has to start with the '*' character.<br>
- Tasks can be longer then one line, the '*' character says when a new task begins.<br>
- There should be no space lines between tasks (As on the picture).<br>
- The last line of the macro should be any line that begins with '*'. In my picture it is: "*************** END OF TASKS *************".<br><br>
After you write your task, mark it as ToDo by having the marker anywhere on the task and pressing F9. The Task will be marked with the Breakpoint mark and the starting date will appear in the end of the task. <br>
When you finish the task move the marker to there and press F9 again. The Breakpoint mark will be removed and the ending date will be added to the end of the task.<br>
<br>
<b>TIP:</b> You might want to cause the finished mark to disappear instead.
<br>
<br>
<br>
<b><font color="#a00000">I hope that you found this tutorial helping and if you did then please vote for it. Thanks.</font></b>

