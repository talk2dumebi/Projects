#   initializing a Git Repository

1.  I created a working directory/folder with this command `mkdir Project_2`

2.  Moving into the woerking directory/ folder running this command `cd Project_2`

3.  In the working directory i run `git init` 

![Alt text](<images_2/Screenshot 2024-01-01 212849.png>)

#   Making my first commit

1. In my working directory create a file `touch index.txt` and adding sentence in the file.

2. Add git to staging area using `git add .`

3. To commit i run this command `git commit -m "initial commit`

![Alt text](<images_2/Screenshot 2023-12-26 213712.png>)

#  Working with Branches

##  Making my first Git Branch

To make my first branch i ran this command `git checkout -b master` the flag -b 
allow me create the branch and switch to the new branch.

![Alt text](<images_2/Screenshot 2024-01-05 231927.png>)

##  Listing Branches

To list branches run this command `git branch`

![Alt text](<images_2/Screenshot 2024-01-05 233349.png>)

##  Merging a branch into another branch

If two branches MAIN and MASTER exist and i want merge into one branch. If we want to merge MASTER to MAIN i will run this command `git merge master`

![Alt text](<images_2/Screenshot 2024-01-06 011758.png>)

##  Delete a git branch

To delete git branch run this command `git branch -d <branch-name>`

![Alt text](<images_2/Screenshot 2024-01-06 013116.png>)


#   Collaboration and Remote Repositories

##  Creating a Github Account

1.  Visit www.github.com

2.  Next enter username, password and email.

![Alt text](<images_2/Screenshot 2024-01-08 225329.png>)

3.  Next click on `verify` bottom to verify my identity.

![Alt text](<images_2/Screenshot 2024-01-08 225404.png>)

4.  Next click on `create account` bottom to create account.

![Alt text](<images_2/Screenshot 2024-01-08 231742.png>)

5.  An activation code will be sent to the email used, enter the code and click `continue`.

![Alt text](<images_2/Screenshot 2024-01-08 225722.png>)

6.  Next select preference and click `continue`

![Alt text](<images_2/Screenshot 2024-01-08 225852.png>)

7.  A list of Github plan will be shown click on `continue for free`

![Alt text](<images_2/Screenshot 2024-01-08 230509.png>)


#   Creating First Repository

1.  Click on the top right corner of the Github account. At the drop down menu click on new repository.

![Alt text](<images_2/Screenshot 2024-01-08 234008.png>)

2.  Fill out the form to add a unique repository name, description and tick the box to add READ.me file.

![Alt text](<images_2/Screenshot 2024-01-08 234747.png>)

3.  Next click on the green bottom to create a repository

![Alt text](<images_2/Screenshot 2024-01-08 234827.png>)


#   Pushing Local git repository to Remote github repository

Add a remote repository to the local repository with this command `git remote add origin <link to github repo>`

![Alt text](<images_2/Screenshot 2024-01-09 001023.png>)

To get the remote link click on the green bottom copy the https link

![Alt text](<images_2/Screenshot 2024-01-09 001208.png>)

After committing the changes in the local repo pushing the content to remote repo using this command `git push origin <branch-name>`

![Alt text](<images_2/Screenshot 2024-01-09 013812.png>)


#   Cloning Remote Git Repository

Git clone is a git command line utility which is used to target an existing repository and create a clone, or copy of the target repository. This command is used for it `git clone <link to the repo>`

![Alt text](<images_2/Screenshot 2024-01-09 015502.png>)
