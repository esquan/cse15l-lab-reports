
# Lab Report 1: Remote Access and FileSystem
## __How to log into a course-specific account on ieng6__
Evelyn Quan, CSE15L Section A05

### Step 1: Download Visual Studio Code

To start off, you want to make sure you have Visual Studio Code downloaded! First, visit this [link](https://code.visualstudio.com/) and follow the instructions to download and install it on your computer.


### Step 2: Install Git

You can skip this step if you are on a Mac. If you are on a Windows, you will need to install [git](https://gitforwindows.org/), which will have tools we will utilize with Visual Studio Code.


### Step 3: Setting Up Bash

For our purposes, we want to make sure we are using the newly installed **git bash** in Visual Studio Code, and not the default **powershell**. To change this, first open a terminal in VSCode. You should see the option for this on the top menu of your screen (Click on Terminal → New Terminal). Or alternatively you can do ``Ctrl or Command + ` ``.

*insert image here later*

Next, use `Ctrl + Shift + P` to open the command palette. Type "Select Default Profile", and select **Git Bash** from the options.

You can now click on the + icon from your terminal window, and you should see a new Git Bash terminal pop up!

*insert image here later*


### Step 4: Begin Remotely Connecting

Now we can type the following command into the terminal, but replace the <mark>zz</mark> with the letters of your course-specific account (please visit [here](https://sdacs.ucsd.edu/~icc/index.php) to find your course-specific account if you have not already):

```
$ ssh cs15lsp23zz@ieng.ucsd.edu
```

(Make sure you are not typing in the $ sign, it is only supposed to illustrate we are typing a command in the terminal!)

Because this is the first time you are connecting to this server, you will see a message like this pop up:

```
Put something in this code block later.
```

To continue connecting, type ==yes== and press enter, then proceed to give your password and press enter again. *Note, when you type the password, due to security reasons, it will not appear as if you are typing anything on your computer. Rest assured that it is in fact typing something into the terminal!*

At this point, you should see something like this being outputted:

```
Put something later.
```

You have now successfully connected to a computer in the CSE basement and have remote access over it! This means that any commands that you run on your own computer will run on that computer as well.


Here's some terminology: your computer is considered the *client* while the computer in the basement is the *server*!


### Step 5: Explore

Now that you have finished ssh-ing, you can try out some commands on both your computer and the remote computer.

Here are some commands you can try out:

- cd ~
- cd
- ls -lat
- ls -a
- ls \<directory> where \<directory> is /home/linux/ieng6/cs15lsp23/cs15lsp23abc, with abc being another person's username
- cp /home/linux/ieng6/cs15lsp23/public/hello.txt ~/
- cat /home/linux/ieng6/cs15lsp23/public/hello.txt
 
Finally, if you want to log out of the remote server, you can first use `Ctrl-D` and then run the command exit.

