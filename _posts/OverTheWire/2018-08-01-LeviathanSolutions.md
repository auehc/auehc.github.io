---
layout: post
title:  "Leviathan Walkthrough"
permalink: /overthewire/leviathan
---

AUTHOR: DeMarcus Campbell

This is a write-up for OverTheWire Leviathan.
I am writing this under the assumption that you have
completed the bandit series. This guide shoudl be pretty 
easy to follow along with and build upon the thought process
introduced during Bandit. 

# Level 0 
Alright for this one let's just login to the server and see what's
available to us.
`$ ssh leviathan0@leviathan.labs.overthewire.org -p 2223`
Alright, so now that we are logged in to the first level we can see that
there is a folder named `.backup`. If we hop into that directory, we can 
see that there is a pretty long file named `bookmarks.html`. We can scan
this file for important keywords to us like `password` using `grep` to find
the given regex.
`$ cat bookmarks.html | grep password`
From this we get a nice output that has the password for the next level, so 
we'll grab that and move on.  

# Level 1
After logging in we should be able to see that there is a file named `check` 
that has the permissions of leviathan2. Here we can use `ltrace` to figure out
exactly how this program works. 
`$ ltrace ./check`
We can see that the program is using a `strcmp` call, which compares two strings.
Using the string that is the program is comparing our input with we are given a 
shell. Performing `$ whoami` tells us that we are leviathan2, so we are now able to
perform actions as if we were leviathan2. Knowing this, we can just print out the 
password for leviathan2, and re-login. 
`$ cat /etc/leviathan_pass/leviathan2`  

# Level 2
On this level the first thing that we should notice is that we are given another file,
which has higher permissions than what we currently have. Create a working directory in
the `/tmp` folder using `$ mkdir`. Once you have a working directory create a small file
in this working directory so we have something to play with while learning how this executable
works. Using `ltrace` we can discover that the executable takes a file as a command line
argument, so we can use the `.bashrc` to see exactly what it does. 
`$ ltrace ./printfile ./.bashrc`
We can see that this executable prints the file that we pass as an argument. Though it likely
won't work we can try to print the password for the next level. 
`$ ./printfile /etc/leviathan_pass/leviathan3`
From the output we are told that we don't have read access to the password file for the next level.
This is of no problem to us, we can find a workaround to print the file that we want. First we shall
see how the executable handles filenames with special characters. We can use `mv` to rename the file
we created in our working directory to a name with spaces. Running the executable on this file, and
analyzing it using `ltrace` we can determine that the executable thinks that we are giving it multiple file
arguments, when we are only giving it one. This is good to know, so now we can trick this executable into 
printing the password file. We can create a blank file that is one the words in the filename with spaces using
`touch`. We can then use a *symlink* to the password file, which makes this file act as a pointer. 
`$ ln -sf /etc/leviathan_pass/leviathan3 <EMPTY FILENAME>`
From this we can use the executable to print the file with spaces in the name, and thus get our password.

# Level 3
This level is really easy and doesn't take too much work to do. As always we check our home directory, and we
find an executable. Running this executable tells us to input the password, so if we try this level's password,
we are not given anything, but that is okay. Using `ltrace` we can see if the executable is comparing our input to
anything and find the password that way. running `ltrace` on this executable shows us that it is comparing our input
to something, so if we use that string it drops us a shell. With this shell, we can just try to `cat` out the password
file, and we're done.

# Level 4
Again, another easy level. So, we are given a ditrectory named `.trash` and in that directory is an executable. When
we run this executable we are given a bunch of binary bytes. We just convert these bytes into ASCII with an online 
converter, and there's our password.

# Level 5
This level isn't too hard either. Running `ltrace` on the executable shows us that it is trying to open a file in the */tmp/*
directory. We have access to this directory, so if we create a *symlink* to the password file we can run the executable again
and get our password.

# Level 6
This level is an actual challenge in comparison to some of the previous levels. So the first thing we want to do is 
run the given executable. We then find out that the program is expecting a 4-digit code, and if you have completed *Bandit*
you should know that this means Brute Force. So, we are going to write a program that goes through all combinations of 4-digit
numbers and try to get a shell. So in the */tmp/* directory we can create a program in **BASH** to handle this for us.
```bash
#!/bin/bash

for i in {0000..9999}
do
~/leviathan6 $i
done
```
This should go through the combinations and get us what we want. After using `chmod` to make this code executable we can then
run it and get a shell. Once we have that shell print the next level's password and move on.

# Level 7
This is the final boss for this series. We look at the contents of the directory, and we see a file named *CONGRATULATIONS*.
We open this file and we get a nice message informing us that we have completed the Leviathan series. 