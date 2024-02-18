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

c.  Pass the content of a file as input to a command

![Alt text](<images_5/Screenshot 2024-02-07 220543.png>)

d. Pass the result of a command as input to another command

![Alt text](<images_5/Screenshot 2024-02-07 222654.png>)

####    5. Functions are like a mini-script inside the scripts. We will create a function with a name & whenever that function is required, we will just type the name of the function rather than typing the whole section of a script again & again.

This function was ran:

![Alt text](<images_5/Screenshot 2024-02-07 223147.png>)

The output:

![Alt text](<images_5/Screenshot 2024-02-07 223549.png>)

#   Writing my First Shell Script


a.  Open a folder called `shell-scripting` this will hold the script, then

![Alt text](<images_5/Screenshot 2024-02-07 225440.png>)

b.  Create (cd into folder) a file called `user-input.sh` with this command `touch user-input`

![Alt text](<images_5/Screenshot 2024-02-07 230958.png>)

c.  The following command will be run

![Alt text](<images_5/Screenshot 2024-02-07 231212.png>)

d.  Save the file

![Alt text](<images_5/Screenshot 2024-02-07 231350.png>)

e.  Run the command `chmod +x <file-name>` to make the file executable

![Alt text](<images_5/Screenshot 2024-02-07 231457.png>)

f.  And run the script using this command `./<file-name>`

`./user-input.sh`

![Alt text](<images_5/Screenshot 2024-02-07 231715.png>)


#   Directory Manipulation and Navigation

a.  Open a file called `navigating-linux-filesystem.sh`

![Alt text](<images_5/Screenshot 2024-02-07 232854.png>)

b.  The following command will be run

![Alt text](<images_5/Screenshot 2024-02-07 233918.png>)


c.  Run the command `chmod +x <file-name>` to make the file executable

![Alt text](<images_5/Screenshot 2024-02-07 234303.png>)

d.  And run the script using this command `./<file-name>`

`./navigating-linux-filesystem.sh`

![Alt text](<images_5/Screenshot 2024-02-08 000235.png>)


#   File Operations and Sorting

a.  Open a file called `sorting.sh`

![Alt text](<images_5/Screenshot 2024-02-08 001101.png>)

b.  The following command will be run

![Alt text](<images_5/Screenshot 2024-02-08 001446.png>)

c.  Run the command `chmod +x <file-name>` to make the file executable

![Alt text](<images_5/Screenshot 2024-02-08 001635.png>)

d.  And run the script using this command `./<file-name>`

`./sorting.sh`

![Alt text](<images_5/Screenshot 2024-02-08 002624.png>)


#   Working with Numbers and Calculations

a.  Open a file called `calculations.sh`

![Alt text](<images_5/Screenshot 2024-02-08 003134.png>)

b.  The following command will be run

![Alt text](<images_5/Screenshot 2024-02-08 003335.png>)

c.  Run the command `chmod +x <file-name>` to make the file executable

![Alt text](<images_5/Screenshot 2024-02-08 003657.png>)

d.  And run the script using this command `./<file-name>`

`./calculations.sh`

![Alt text](<images_5/Screenshot 2024-02-08 003840.png>)


#   File Backup and Timestampling

a.  Open a file called `backup.sh`

![Alt text](<images_5/Screenshot 2024-02-08 004324.png>)

b.  The following command will be run

![Alt text](<images_5/Screenshot 2024-02-18 204107.png>)

c.  Run the command `chmod +x <file-name>` to make the file executable

![Alt text](<images_5/Screenshot 2024-02-18 204530.png>)

d.  And run the script using this command `./<file-name>`

`./backup.sh`

![Alt text](<images_5/Screenshot 2024-02-18 204107.png>)

`the backup directory`

![Alt text](<images_5/Screenshot 2024-02-18 204704.png>)


Thank you...