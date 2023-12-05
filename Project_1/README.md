# Linux Basic Command

## 1.   `sudo` Command:-

sudo is commonly used to run a command as root. You must be enabled to use  sudo , and once you do, you can run commands as root by entering your user's password (not the root user password).


![Alt text](<images/Screenshot 2023-11-29 180636.png>)


## 2.   `pwd` Command:-

pwd command allows you to print the current working directory on your terminal.


![Alt text](<images/Screenshot 2023-11-29 185453.png>)


## 3.   `cd` Command:-

cd means change directory. One can invoke it specifying a folder to move into. specify a folder name, or an entire path.

![Alt text](<images/Screenshot 2023-11-29 191255.png>)

cd - this move to previous directory.

![Alt text](<images/Screenshot 2023-11-29 192805.png>)

cd.. this move one directory up.

![Alt text](<images/Screenshot 2023-11-29 194319.png>)

## 4.   `ls` Command:-

ls command is used to list files and directories in the current working directory. 

![Alt text](<images/Screenshot 2023-11-29 195024.png>)

ls -R
lists all files in the subdirectories.

ls -a
shows hidden files in addition to the visible ones.

ls -lh
shows the file sizes in easily readable format.

![Alt text](<images/Screenshot 2023-11-29 195801.png>)

## 5.   `cat` Command:-

cat prints a file's content to the standard output.

![Alt text](<images/Screenshot 2023-11-29 201903.png>)

## 6.   `cp` Command:-

cp means copies source file into destination.

![Alt text](<images/Screenshot 2023-11-29 220226.png>)

## 7.   `mv` Command:-

mv moves to new directory and can also rename file name.

mv Terraform.txt /home/ubuntu/LinuxCommand...... (move file).

![Alt text](<images/Screenshot 2023-11-29 221407.png>)

mv Terraform.txt terraBlock.txt......(rename file).

![Alt text](<images/Screenshot 2023-11-29 222451.png>)

## 8.   `mkdir` Command:-

With mkdir you can create one or multiple folders with this one command.

![Alt text](<images/Screenshot 2023-11-29 223326.png>)

mkdir Music/Songs

![Alt text](<images/Screenshot 2023-11-29 223627.png>)

## 9.   `rmdir` Command:-

rmdir means deletes an existing directory provided it is empty.

![Alt text](<images/Screenshot 2023-11-29 225510.png>)

## 10.  `rm` Command:-

rm means removes (Deletes) filename.

rm File.txt.....

![Alt text](<images/Screenshot 2023-11-29 235559.png>)

## 11.  `touch` Command:-

You can create an empty file using the  touch command.

touch sqlite.sh

![Alt text](<images/Screenshot 2023-11-30 000358.png>)


## 12.  `locate` Command:-

The locate command is the quickest and simplest way to search for files and directories by their names.

![Alt text](<images/Screenshot 2023-11-30 211146.png>)

locate -i

![Alt text](<images/Screenshot 2023-11-30 211331.png>)

## 13.  `find` Command:-

The  find  command can be used to find files or folders matching a particular search pattern. It searches recursively.

![Alt text](<images/Screenshot 2023-11-30 212052.png>)

## 14.  `grep` Command:-

grep means search for a string within an output.

![Alt text](<images/Screenshot 2023-11-30 212746.png>)

## 15.  `df` Command:-

The  df  command is used to get disk usage information. Its basic form will print information about the volumes mounted.

![Alt text](<images/Screenshot 2023-11-30 213537.png>)

df -h:  this will show those values in a human-readable format.

![Alt text](<images/Screenshot 2023-11-30 215304.png>)

## 16. `du` Command:-

The  du  command will calculate the size of a directory as a whole.

![Alt text](<images/Screenshot 2023-11-30 215724.png>)

## 17.  `head` Command:-

head means return the specified number of lines from the top.

![Alt text](<images/Screenshot 2023-11-30 224732.png>)

## 18.  `tail` Command:-

tail means return the specified number of lines from the bottom.

![Alt text](<images/Screenshot 2023-11-30 225150.png>)

## 19.  `diff` Command:-

diff means find the difference between two files.

![Alt text](<images/Screenshot 2023-11-30 230107.png>)

## 20.  `tar` Command:-

The  tar  command is used to create an archive, grouping multiple files in a single file.

![Alt text](<images/Screenshot 2023-11-30 232609.png>)

![Alt text](<images/Screenshot 2023-11-30 232632.png>)


# File Permissions and Ownership

## 21.  `chmod` Command:-

chmod means command to change file permissions.

![Alt text](<images/Screenshot 2023-11-30 234227.png>)

## 22.  `chown` Command:-

chown means command for granting ownership of files or folders.
(i have to create addUser called `students`).

![Alt text](<images/Screenshot 2023-12-01 033159.png>)

![Alt text](<images/Screenshot 2023-12-01 033251.png>)

## 24.  `kill` Command:-

The  kill  program can send a variety of signals to a program. It's not just used to terminate a program, like the name would suggest, but that's its main job.

![Alt text](<images/Screenshot 2023-12-04 214150.png>)

## 25.  `ping` Command:-

The  ping  command pings a specific network host, on the local network or on the Internet.

![Alt text](<images/Screenshot 2023-12-04 214547.png>)

## 26.  `wget` Command:-

wget means direct download files from the internet.

![Alt text](<images/Screenshot 2023-12-04 215353.png>)

## 27.  `uname` Command:-

uname means linux command to get basic information about the OS.

![Alt text](<images/Screenshot 2023-12-04 230639.png>)

## 28.  `top` Command:-

The top command is used to display dynamic realtime information about running processes in the system.

![Alt text](<images/Screenshot 2023-12-04 231141.png>)

## 29.  `history` Command:-

The command history helps you view commands you've previously run inside the terminal.

![Alt text](<images/Screenshot 2023-12-04 232330.png>)

## 30.  `man` Command:-

man means access manual pages for all Linux commands.

![Alt text](<images/Screenshot 2023-12-04 233601.png>)

## 31.  `echo` Command:-

echo means print any text that follows the command.

![Alt text](<images/Screenshot 2023-12-04 233957.png>)

## 32.  `zip, unzip` Commands:-

zip means zip files in Linux.

unzip means unzip files in Linux.

![Alt text](<images/Screenshot 2023-12-04 235829.png>)

unzip archive.zip

![Alt text](<images/Screenshot 2023-12-05 000218.png>)

## 33.  `hostname` Command:-

A hostname command is used to view a computer’s hostname and domain name (DNS) (Domain Name Service), and to display or set a computer’s hostname or domain name.

![Alt text](<images/Screenshot 2023-12-05 000602.png>)

## 34.  `useradd, userdel` Commands:-

useradd: command allows us to create a new user in Linux.

userdel: is a command-line-based utility in Linux-based operating systems that helps in removing or deleting users from the system.

sudo useradd johnDoe

![Alt text](<images/Screenshot 2023-12-05 010322.png>)

sudo userdel johnDoe

![Alt text](<images/Screenshot 2023-12-05 010418.png>)

## 35.  `apt-get` Command:-

apt-get is a command line tool for interacting with the Advanced Package Tool (APT) library (a package management system for Linux distributions). It allows you to search for, install, manage, update, and remove software.

![Alt text](<images/Screenshot 2023-12-05 011434.png>)

## 36.  `nano, vi and jed` Commands:-

Nano is a user-friendly, simple and WYSIWYG(What You See Is What You Get) text editor, which improves the features and user-friendliness of UW Pico text editor.

![Alt text](<images/Screenshot 2023-12-05 012453.png>)

![Alt text](<images/Screenshot 2023-12-05 012302.png>)

The default editor that comes with the UNIX operating system is called vi (visual editor). Using vi editor, we can edit an existing file or create a new file from scratch.

![Alt text](<images/Screenshot 2023-12-05 013800.png>)

![Alt text](<images/Screenshot 2023-12-05 013307.png>)

jed command in Linux is used to open up a text editor called “jed”. It is a friendly editor with a drop-down menu that can be used by programmers in Linux. 

![Alt text](<images/Screenshot 2023-12-05 014913.png>)

![Alt text](<images/Screenshot 2023-12-05 014723.png>)

## 37.  `alias, unalias` Commands:-

alias command instructs the shell to replace one string with another string while executing the commands.

![Alt text](<images/Screenshot 2023-12-05 021138.png>)

The unalias command removes the definition for each alias name specified, or removes all alias definitions if the -a flag is used.

![Alt text](<images/Screenshot 2023-12-05 021541.png>)

## 38.  `su` Command:-

su command in linux allows a user to switch to another user account and gain all of its privileges.

![Alt text](<images/Screenshot 2023-12-05 022144.png>)

## 39.  `htop` Command:-

htop command in Linux system is a command line utility that allows the user to interactively monitor the system’s vital resources or server’s processes in real time.

![Alt text](<images/Screenshot 2023-12-05 022408.png>)

## 40.  `ps` Command:-

The ps command, short for Process Status, is a command line utility that is used to display or view information related to the processes running in a Linux system. 

![Alt text](<images/Screenshot 2023-12-05 022724.png>)






