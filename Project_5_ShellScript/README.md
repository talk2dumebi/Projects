#   Shell Scripting Hands-Projects

##  Introduction to Shell Scripting and User Input

### Shell Scripting Synax Element

####    1.  Variable:- Variables let you store data. You can use variables to read, access, and manipulate data throughout your script.  Note that dollar sign `$` is required to access an existing variable's value in bash script. For example with this command `name="Patric"` and output `echo $name`

![Alt text](<images_5/Screenshot 2024-02-04 184912.png>)

####     2(a).  Control Flow:- allow you to control the flow of execution of your script based on conditions, loops, and patterns. For example using the if-else to execute script based on a condition.The following commands will be run.

1.  Make a directory `/opt/scripts`

![Alt text](<images_5/Screenshot 2024-02-04 192038.png>)

2.  cd into the folder/directory 

![Alt text](<images_5/Screenshot 2024-02-04 194137.png>)

3.  Then the script was written this file  `firstScript.sh`

![Alt text](<images_5/Screenshot 2024-02-04 194605.png>)

![Alt text](<images_5/Screenshot 2024-02-04 194847.png>)

4.  The results after inputing number were:

![Alt text](<images_5/Screenshot 2024-02-04 194802.png>)

####     2.(b) iterating through a list using a for *loop*

`This is command is run` on the file

![Alt text](<images_5/Screenshot 2024-02-04 201153.png>)

`the result`

![Alt text](<images_5/Screenshot 2024-02-04 201327.png>)


####     3. Command Substitution:- Command substitution allows the output of a command to replace the command itself. Command substitution occurs when a command is enclosed as follows: `$(command)`or back-tick ``. For example this command 

a. Using backtick for command substitution

![Alt text](<images_5/Screenshot 2024-02-04 212819.png>)

b. Using $() syntax for command substitution

![Alt text](<images_5/Screenshot 2024-02-04 213459.png>)

####     4. Input and Output:- In bash scripting, handling user input and displaying output are crucial for creating interactive and informative scripts. 

a. To read user input in a bash script, use the read command.

Accept user input

![Alt text](<images_5/Screenshot 2024-02-07 210922.png>)

And the result shows 

![Alt text](<images_5/Screenshot 2024-02-07 211840.png>)

b.  To format output in a bash script, output text in the terminal.

`echo "Hello World"`

![Alt text](<images_5/Screenshot 2024-02-07 212324.png>)

c.  Output the result of a command into file.

![Alt text](<images_5/Screenshot 2024-02-07 212712.png>)
