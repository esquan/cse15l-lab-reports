
# Lab Report 1: Remote Access and FileSystem
## __How to log into a course-specific account on ieng6__
*Evelyn Quan, CSE15L Section A05*

<br/>

This tutorial will show you the basics of remotely accessing a computer in the CSE basement, and how to log into a course-specific account on ieng6 to do so!


### Step 1: Download Visual Studio Code

To start off, you want to make sure you have Visual Studio Code downloaded! First, visit this [link](https://code.visualstudio.com/) and follow the instructions to download and install it on your computer.

<br/>

![Image](https://drive.google.com/uc?id=1Aj_flHfVfU3aDp7WzqGQMShf1i9aHkir)

<br/>

### Step 2: Install Git

You can skip this step if you are on a Mac. If you are on a Windows, you will need to install [git](https://gitforwindows.org/), which will have tools we will be able to utilize with Visual Studio Code.

<br/>

![Image](https://drive.google.com/uc?id=1IXA83iBAqLhzwm1S29kxYrIzOhTs8R6S)

<br/>

### Step 3: Setting Up Bash

For our purposes, we want to make sure we are using the newly installed **git bash** in Visual Studio Code, and not the default **powershell**. To change this, first open a terminal in VSCode. You should see the option for this on the top menu of your screen (Click on Terminal → New Terminal). Or alternatively you can do ``Ctrl or Command + ` ``.

<br/>

![Image](https://drive.google.com/uc?id=1nIHqSM2I0cg7RaM7BUR05KoqO5elErSV)

<br/>

Next, use `Ctrl + Shift + P` to open the command palette. Type <mark>Select Default Profile</mark>, and select **Git Bash** from the options.

You can now click on the + icon from your terminal window, and you should see a new Git Bash terminal pop up!

<br/>

![Image](https://drive.google.com/uc?id=1rItyYEn1c42PMInBeKvTs4Y5JQPXFyqO)

<br/>

### Step 4: Begin Remotely Connecting

Now we can type the following command into the terminal, but replace the <mark>zz</mark> with the letters of your course-specific account (please visit [here](https://sdacs.ucsd.edu/~icc/index.php) to find your course-specific account if you have not already):

```
$ ssh cs15lsp23zz@ieng6.ucsd.edu
```

*Make sure you are not typing in the $ sign, it is only supposed to illustrate we are typing a command in the terminal!*

<br/>

Because this is the first time you are connecting to this server, you will see a message like this pop up:

```
$ ssh cs15lsp23zz@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```
<br/>

To continue connecting, type <mark>yes</mark> and press enter, then proceed to give your password and press enter again. *Note, when you type the password, due to security reasons, it will not appear as if you are typing anything on your computer. Rest assured that it is in fact typing something into the terminal!*

<br/>

At this point, you should see something like this being outputted:

![Image](https://drive.google.com/uc?id=1CKyvM6vA8nUiOV1xDphblbEXAX9TUTJz)

<br/>

You have now successfully connected to a computer in the CSE basement and have remote access over it! This means that any commands that you run on your own computer will run on that computer as well.


Here's some terminology: your computer is considered the *client* while the computer in the basement is the *server*!

<br/>

### Step 5: Explore

Now that you have finished ssh-ing, you can try out some commands on both your computer and the remote computer.

Here are some commands you can try out:


- **cd ~**
- **cd**
- **ls -lat**
- **ls -a**
- **ls -s**
- **ls \<directory>** where **\<directory>** is **/home/linux/ieng6/cs15lsp23/cs15lsp23abc**, with **abc** being another person's username
- **cp /home/linux/ieng6/cs15lsp23/public/hello.txt ~/**
- **cat /home/linux/ieng6/cs15lsp23/public/hello.txt**
 
<br/>
 
For instance, typing the command `cd` without any arguments will take you to your home directory. Typing `cd ~` can also take you back to your home directory. This command ultimately serves to help you to change directories in order to access certain files/folders, as adding an argument of a path to a folder after `cd` will take you into that directory!

`ls` is also a neat command that will list all the contents of a directory for you to see. There are many options to add onto `ls`, such as `ls -s` which will print the size of each of your files in the directory, in blocks. The `cat` command is short for "concatenate", and will read data from a file and print out its contents as an output. The `cp` command will take the file(s) and/or directory given as the first argument and copy it over to the destination specified in the second argument!

<br/>

![Image](https://drive.google.com/uc?id=1_rMANa4pwc1qe1boYC9lxOB3JEAekpnv)

<br/>

Finally, if you want to log out of the remote server, you can first use `Ctrl-D`, or run the command <mark>exit</mark>.

<br/>

*Now you know some of the bascis of remote access and how to log onto a course-specific account on ieng6.*

Good work!

<br/>

---
