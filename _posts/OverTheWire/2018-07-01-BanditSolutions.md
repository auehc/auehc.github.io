---
title:  "Bandit Walkthrough"
permalink: /overthewire/bandit
author: demarcus
categories: write_ups
tags: overthewire
toc: true
---




This is my personal writeup for OverTheWire's Bandit game. This guide is going
to be targeted for beginners in this type of game or Capture The Flag(CTF). There
are going to be many ways you can solve these problems, but I will only be covering
the solutions that are easier to understand rather than easier to type. This guide
is for showing you a simple thought process to solving Command Line based CTF problems. I 
will NOT just give someone the password for the level, this guide is for those that are trying to 
learn and get better at what they do. Even though I will be walking through these levels
I highly encourage you to read the manual(man) pages of the commands that OverTheWire recommends
for each bandit level. Some levels also have some reading on certain topics, that you might find
very useful.


# Level 0
So this will by far the easiest thing you will do for this set. You
are asked to SSH(Secure Shell) into their server using the username and password
`bandit0`. So depending on what Operating System(OS) your computer is
running there will be different steps you have to take to do this.

- Windows
  - Download PuTTy so that you can SSH into the machine
  - Open PuTTy and input the URL `bandit.labs.overthewire.org` into the bar and change the port number to 2220.
  - Click Open and input `bandit0` for your username and password
  - Click Yes
- Linux/Mac OS
  - Open your computer's command line commonly known as Terminal/Konsole
  - Use this command `$ ssh bandit0@bandit.labs.overthewire.org -p 2220`
    -NOTE: Do not include the double quotes and dollar sign
  - Use the password `bandit0` 
  - Type `yes`
After following these steps you should see information printed out and you should be logged into
the bandit server. You have now passed bandit0. *NOTE: I would recommend that you try to do this on
Linux/Mac OS simply because SSH is built-in to their command line by default, which will make life a
bit easier on some later stages, but this is 100% do-able using Windows and PuTTy. 


# Level 0 --> 1
So now we are given that the password into the next level can be found in a file called `readme`
that is located in the level's home directory. We can check this by running the command:
- `$ ls`
This lists all visible files in the current directory, which is the home directory. You should see
that a file called `readme` is there. We need to view the content of this file to get the password to
level 1. To view the information in this file, use:
- `$ cat readme`
This command prints the contents of the file named `readme` to the screen, which in this case is the
password to the next level. Copy the password to your clipboard, and exit this ssh session by using the command:
- `$ exit`


## Level 1 --> 2 
Log in to the bandit server again using the steps from Level 0, but replace the username bandit0 with bandit1,
and use the password that we just found in the previous level. So now it tells us that the password for level 2
can be found in a file named `-`. We can check to see that the file is there by using the `ls` command once again.
If we try to use the exact same technique as we did in the previous level it will give us a blank line waiting for
input. To exit this state use Ctrl-C. What this shows is that the special character is getting in our way. So, to get
around this, we will use a BASH(the name of command line code) wildcard to replace the `-` and print the contents of 
the file. 
- `$ cat ./?`
  - *NOTE*: `./` is the shortcut for our current location in the system, and `?` is the wildcard for a single character
This should print the password to the screen, so copy it to your clipboard, and exit the session using the `exit` command.


## Level 2 --> 3
Log into the bandit server using the username bandit2 and our new password. So now we are told that our password is stored
in a file named `spaces in this filename`. It is obvious that we will have to do something special for this file because there
is nothing particularly special about it, other than the fact that it has spaces in its filename. Therefore to inlcude spaces 
in a file name we need to use the escape character `\` before the space to tell BASH that the spaces are not separating commands
and or arguments. To get the password we will just concatenate the contents of the file to the screen using `cat` and `\`.
- `$ cat spaces\ in\ this\ filename`
  - *NOTE*: There is another solution to this problem using wildcards
Copy the resulting password and exit the SSH session.


## Level 3 --> 4
Log in to bandit server with username bandit3 and the new password. Now we are told that our password is in a hidden file in the 
`inhere` directory. This is very important to note because hidden files are only hidden from certain commands, this doesn't mean 
that we can't access its contents. There are a few ways of solving this, but since this guide is targeted for those who are new to
the field I will give the solution that is easier to understand. First we need to change our directory to the `inhere` directory:
- `$ cd inhere`
Now that we are inside of the `inhere` directory let's check its contents by using `ls`. This should show that nothing is in the 
directory. We are told that the file is in this directory, but it is hidden, to fix this we will use certain arguments for the `ls`
command to show all contents in the directory.
- `$ ls -a`
- *NOTE*: The `-a` argument for the `ls` command stands for all, so it shows all contents of the directory
Now we can see that the password file is named `.hidden` so, we will `cat` this file and retrieve our password.
- `$ cat .hidden`
Copy the contents of `.hidden` and exit the ssh session.


## Level 4 --> 5
Once again log in to the bandit server using bandit4 and our newest password. Our password file is once again located in the directory
`inhere`. So, if we list all contents of the `inhere` directory:
- `$ ls -a inhere`
we see that there are about 10 different files here, and we don't know which of these files has our password. It is very inefficient to
just print out the contents of every file in the `inhere` directory and then parsing through to find a password. They did give us one clue;
our password is in the only humand readable file in the `inhere` directory. So to check the type of information that's in all of the files 
in `inhere` we are going to use the `file` command to get more information about the files.
```bash
cd inhere
file ./*
```
- *NOTE*: The `*` is a wildcard similar to `?` but can represent an unlimited amount of characters
This shows us that `-file07` is the only file which has ASCII text, so that must be our password. 
- `$ cat ./-file07`
Copy the password and exit the session.


## Level 5 --> 6 
Log in with bandit5 and the newest password. We are given that our desired password will be in the `inhere` directory, human readable, non-executable,
and be 1033 bytes in size. To approach this we need to figure out what all is inside of `inhere` so we can gauge how much we need to do. 
- `$ ls -al inhere`
  - NOTE: The `-l` argument shows all of the contents in long form, which gives us name of file, permissions, and what type of file it is.
This shows us that all of the contents of `inhere` are directories. This makes our job a bit more complicated, since we have a lot more to search through.
If we use the `file` command to list the type of contents of all files inside of the sub-directories in `inhere`:
- `$ file */*/*`
we get a lot of files, and a number of which contain ASCII text, so that was a bust. Let's try to work with the file size to see if we can narrow down our options.
- `$ find -size 1033c`
  - *NOTE*: The 1033c means 1033 bytes
This gives us one distinct file and if we `file` it we see that it is ASCII text, with very long lines. That's strange that there is only one file in this group
that is the desired file size but has very long lines. Let's `cat` the file to see what its contents are:
- `$ cat ./inhere/mayberhere07/.file2`
we see that it has our password and a bunch of blank lines. Copy the password and exit.


## Level 6 --> 7
Login to bandit6 using the new password. Now we are told that the file is somewhere on the server and is owned by user bandit7, group bandit6, and 33 bytes in size.
If we `ls` the home directory, we will see that there is nothing special about this directory and our password clearly isn't in here.*
*NOTE*: The three files that are listed SHOULD NOT be edited they are config files for the user bandit6 and are not important to the completion of this level
So let's `cd` to the root directory so our commands can navigate to all files on the server.
- `$ cd /`
Now that we are in the root directory, we can `ls` and see that there is a number of possible directories that this password file can be in. So we can start by using the 
`file` command to find all files that meet our requirements. 
- `$ find / -size 33c -user bandit7 -group bandit6 | grep bandit`
  - *NOTE*: This is the first time we are using `grep`, it serves as a searching tool for our BASH command line
  - *NOTE*: This is a pretty weird result that `find` gives us, so we `grep` the results for the word bandit and luckily it highlights only one file for us 
If we cat out the file that `grep` highlights we get our desired password.
- `$ cat /var/libs/dpkg/info/bandit7.password
Copy the results and exit.


## Level 7 --> 8 
Login to bandit7 using the new password. Now we are given a file and that our password is in the file next to the word `millionth`. Let's cat out the file to see what it looks like.
- `$ cat data.txt`
Well, that just isn't going to work we need a way to find that one line within this file, so we can still cat out the file, but this time we are going to pipe `|` the results into `grep`
so that it can do the reading work for us. 
- `$ cat data.txt | grep millionth`
This prints out the line that has the word millionth and thus our password.
Copy and exit.


## Level 8 --> 9
Login to bandit8. We are told that the next password is the only unique line in the file `data.txt`. This is pretty good to know because BASH has some commands that allows us to pull unique lines
from a file. So, first we must sort the contents of the file, then we will determine the unique lines of the file.
- `$ sort data.txt | uniq -u`
  - *NOTE*: We have to sort the file first because the `uniq` command only provides our desired results for sorted lists
Copy the password and exit.


## Level 9 --> 10
Login to bandit9. Here we are told that our password is one of the human readable lines and begins with `=`, so we now know that `cat` and `grep` aren't going to work because the file consists of more
than just ASCII text. We need to search through only the strings that contain ASCII text and have `=` signs contained at the front, so we need to use the `strings` command.
- `$ strings data.txt | grep =`
This prints out a couple of possibilities, but given the history of what previous levels' passwords have looked like, we can easily tell which is our desired password.
Copy and exit.

## Level 10 --> 11
Login to bandit10. So we are told that the contents of the password file are encoded in base64, we just need to decode this data to get our password.
- `$ base64 -d data.txt`
  - *NOTE*: `-d` is the decode argument for `base64`
Copy and exit.

## Level 11 --> 12
Log into bandit11. We are given a file that has the password and a Ceasar Cipher shift of 13 has been applied to it. We need to reverse this shift, so we will use the translate(`tr`) command.
- `$ cat data.txt | tr A-Za-z n-za-mN-ZA-M`
Copy and exit.


## Level 12 --> 13
Login to bandit12. So now we start to get into some of the more challenging portions of this CTF. They give us a file that contains a hexdump of a file that has been compressed multiple times. This
means that we will be doing a lot of work to recover the human readable password file. First we will need to make a subdirectory under the `/tmp` to work in. 
- `$ mkdir /tmp/<UNIQUE NAME>`
  - NOTE: Replace <UNIQUE NAME> with your own unique name of course
We now need to make a copy of `data.txt` into this subdirectory.
- `$ cp data.txt /tmp/<UNIQUE NAME>`
Let's now move into our new working directory
- `$ cd /tmp/<UNIQUE NAME>`
We now will reverse the hexdump
```bash
$ touch tempo
$ xxd -r data.txt tempo
```	
- *NOTE*: This is the first time we are using the `touch` command. This command creates a blank with the given filename
- *NOTE*: Thsi is also the fist time we are using `xxd`. This command deals with hexdumps
Now that we have the dump reversed into tempo, we can now see what type of file it has become
- `$ file tempo`
This should say that tempo is now a gzip compressed file, to fix this we will use a variant of the gzip command to reverse it
```bash
$ mv tempo tempo.gz
$ gunzip tempo.gz
```
We now have unzipped the `tempo.gz` file, and we can check using `ls` to check and see that `tempo.gz` to `tempo`. So if we use
the `file` command to check and see what type of file that `tempo` is we can see that it is bzip.
```bash
$ file tempo
$ mv tempo tempo.bz
$ bunzip2 tempo.bz
```
After doing this we get another gzipped file named `tempo`, so we will repeat the steps we took above
```bash
$ mv tempo tempo.gz
$ gunzip tempo.gz
```
Now after doing that we do a `file` on `tempo` and we can see that it is a POSIX tar file, which we haven't dealt with yet.
We will depackage it by using the `tar` command.
```bash 
$ mv tempo tempo.tar
$ tar -f tempo.tar -x
```
This pulls out a file named `data5.bin` from the tar file, so we will run a `file` command on it to see what type of data it holds.
- `$ file data5.bin`
We see that it as well is a tar file, so we need to change its extension to the proper extension and extract the files from it.
```bash 
$ mv data5.bin data5.tar
$ tar -f data5.tar -x
```
This pulls out a file that is named `data6.bin` and the `file` command says that it is a bzipped file, so we will repeat steps we 
took above to handle bzipped compressed data.
```bash 
$ mv data6.bin data6.bz
$ bunzip2 data6.bz
```
Now we have the file `data6` and the `file` command says that it is another POSIX tar archive, so we must extract files from it.
```bash
$ mv data6 data6.tar
$ tar -f data6.tar -x
```
We should now have a file that is called `data8.bin` and `file` should show that it is a gzipped file. We know how to handle gzipped files
using the same technique as above.
```bash
$ mv data8.bin data8.gz
$ gunzip data8.gz
```
Now we have the file `data8`. We can see that the content of data8 is ASCII text by using the `file` command. Since this is the only file
that we have come across so far that has ASCII text let's print out the contents of this file to see what information it has to give us.
- `$ cat data8`
Finally!, We have found our password for the next level. Copy and exit.


## Level 13 --> 14  
This level is a bit tricky and we have to be very careful about what we do from this point on. We are given that the password for the next level
is in the directory `/etc/bandit_pass/bandit14`. They also say that we aren't going to be getting a password for the next level, but rather a SSH
private key. So first let's find the key by checking our home directory.
- `$ ls -al`
Well that was a bit easy. If we print out the contents of the file we see that it is this really long string of characters that no sane person would 
want to type. This file will allow us to SSH into the next level without a password.
- `$ cat sshkey.private`
So from this we will SSH into the next level using this file*.  *NOTE: We are NOT logging out of bandit13, but rather having nested sessions.
- `$ ssh bandit14@localhost -i sshkey.private`
  - NOTE: Enter yes when prompted.
We will copy the password for this level from the file, exit this session and open a new session for bandit14.
- `$ cat /etc/bandit_pass/bandit14`
Copy the password, exit from bandit14 and bandit13.


## Level 14 --> 15 
Login to bandit14 from PuTTy or the command line using the password we just retrieved rather than the SSH private key. We are now told that we will get the password for the next level by
by submitting our current password to the server on port 30000. This is simple to do, we will just use the `telnet` protocol to handle the connection for us. 
- `$ telnet localhost 30000`
We should now see that the connection has been opened on port 30000 and is now waiting for a response, which in this case is the password for this level. Paste the password we got in the previous
level here and we should get a response saying `Correct` and the password for bandit15. Copy and exit.


## Level 15 --> 16
Login to bandit15 using this new password. We are now told that we need to submit our password again, but this time we must use SSL encryption. The `openssl` tool set will be what we will have to
utilize to accomplish this task. 
- `$ openssl s_client -connect localhost:30001`
We should get this print out of a bunch of gibberish and a cursor awaiting input. Paste the password we used to login to this level here, and we should now get the Heartbeating error. This is good, 
because it means we are on the right track. Now, we will exit this session by using Ctrl-D, and re-enter the command, but this time with the argument that the crew at OTW suggested.
- `$ openssl s_client -connect localhost:30001 -ign_eof`
This should bring us to the screen we were at previously, but this time when we paste the password into the prompt we should get a positive response with the password to the next level.
Copy and exit.


## Level 16 --> 17
Now we are told that we need to submit our password to a server that is somewhere on the port range 31000 to 32000. We first need to check and find which of these ports is open. 
- `$ nmap localhost -p 3100-32000`
From this Network Mapper(`nmap`) we can see that there is 5 possible ports that are open. We now need to determine which of the ports is the one we want to use. `nmap` has an argument
that could have done this for us, but that functionality is not available on the version of `nmap` on this server. So to test which of the ports we want to submit our password to, we can easily
just iterate through the ports and submit the password until we find one that gives desired results.
- `$ openssl s_client -connect localhost:<PORT NUMBER FROM NMAP>`
When you find out which port from this list of 5 is the correct port. You will get a SSH private key. Copy the entire contents of the private key that is output, and on your working machine open 
a text editor like notepad, and paste it into the blank notepad file. Save this file as `key.private`. End the SSH session if you have not already, and prepare to login to bandit17.


## Level 17 --> 18
To log in to bandit17 use the private key we just found. Once you've logged in we are told that our next password is the only line that has been changed between two files. To find the difference, we will use 
the `diff` command:
- `$ diff passwords.old passwords.new`
This command should print two lines of possible passwords, and the second one is the one we want.


## Level 18 --> 19
This is where things get a bit tricky for Windows users, but it is 100% possible. Here if we try to login using bandit18 and the password, we are immediately logged out after inputting our password. We need to print
the contents of the file `readme`, but are not allowed time to input commands. We can combat this by using a arguments for the `ssh` command.
```bash
$ ssh -p 2220 bandit18@bandit.labs.overthewire.org -f
$ cat readme
```
This should print out the contents of the file right before it logs us out of the machine, but as long as we get our password.


## Level 19 --> 20
After we login, we are told that we have a setuid binary that is in our home directory. We first need to understand what a setuid binary is. Setuid binaries give us a way to do things as if we
were another user. Similar to programming, each one is unique, but can produce similar results. The first thing we need to do is figure out how this particular setuid binary works, and we are told
that we can do that by just running the binary. 
```bash
$ ls
$ ./bandit20-do
```
This example tells us that all we must do to move on to use the binary to execute commands, and they should run as if we were bandit20. Let's use this to get the bandit20 password. 
- `$ ./bandit20-do cat /etc/bandit_pass/bandit20`
Let's exit and re login as bandit20.


## Level 20 --> 21
We now have another setuid binary, but this one does something a bit different. This one takes a port number as an argument, and waits for the password for bandit20 to be input. Once the password
is sucessfully checked to be correct, it then transmits the password to bandit21 to the same port. So, here we have to do two tasks at once. There are a few ways to do this, but i'm only going to
cover one. First we need to open two SSH sessions into level 20 in different windows. Now on one session start a NetCat(`nc`) listener on a port of our choosing. 
- `$ nc -l <PORT NUMBER>`
Now that this session is listening on that designated port, we must use the setuid command that we were given to cause some traffic on this port. We now want to go to our secondary terminal session, and 
and start the setuid binary on the port that we used above.
- `$ ./suconnect <PORT NUMBER>`
This should give us a blank line because now it is listening for input from that port. So now we need to submit the password for bandit20 to this port. We will go to the first window, where we used the 
`nc` listener and enter the password for bandit20. After we do this, we should be able to see that the next password is printed to the screen for us. 


## Level 21 --> 22
So here these last few levels can be very challenging, but what's a fight without a challenge? So we are told that we are going to be dealing with `cron`, which is the task scheduler. Let's `ls` the contents
of the cron directory to see what we're working with. 
- `$ ls /etc/cron.d`
We see that there are a few files here, but only one of them has bandit22, so let's work with that one. If we `cat` out the file, we should be able to see what job it is actually running.
- `$ cat /etc/cron.d/cronjob_bandit22`
From this we can see that there is a `.sh`  file that is being run. We can cat out that file to see what it is actually doing to try and figure out what steps it is taking, and then work from there.
- `$ cat /usr/bin/cronjob_bandit22.sh`
Now reading what this file does is that it changes permissions on a file in the `/tmp` directory to 644 which means no matter what we have read access to this file. Then it prints out the contents of the 
bandit22 password file to the `/tmp` file. So now we should just need to print out the contents of the `/tmp` file and get the password from there.
- `$ cat /tmp/t706.....` *NOTE*: This is a very long file name, just copy and paste it instead of typing it out.
This gave us our password, so we're done with this level


## Level 22 --> 23
On this level we will be dealing with cron again, so let's `ls` the directory and see what we can see.
- `$ ls /etc/cron.d`
Of course we will be working with bandit23, so let's `cat` out its contents.
- `$ cat /etc/cron.d/cronjob_bandit23`
We are given a location of a shell script, so lets `cat` out that script to see what it does.
- `$ cat /usr/bin/cronjob_bandit23.sh`
This is very interesting because the script is a bit cryptic, but there is a `echo` call that is made, so let's run
the script and see what it prints out.
- `$ /usr/bin/cronjob_bandit23.sh`
So this is printing the contents of this level's password file into a file in the `/tmp` directory. So, we need to 
change this from bandit22 to bandit23. The script sets the variable `mytarget` to an `echo` command that references $myname,
which is the result of the command `$ whoami`. Let's try that `echo` command on its own and see what it gives us.
- `$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1`
This gives us a long string, but this likely isn't our password, so let's see if there is a `/tmp` file that has this
name.
- `$ cat /tmp/8ca319......` NOTE: Another long filename
Turns out there is a file with this name, and it has our password. 


## Level 23 --> 24
We have another cron issue, but this time we are told that we need to write our own scripts for this level, so let's
create a `/tmp` sub-directory so we can have a work space.
- `$ mkdir /tmp/<UNIQUE NAME>`
Now let's see what all is in the cron directory again.
- `$ ls /etc/cron.d`
We see a bandit24 file, so let's work with that.
- `$ cat /etc/cron.d/cronjob_bandit24`
Alrighty, this gives us the path to a shell script, so let's see what this script does.
- `$ cat /usr/bin/cronjob_bandit24.sh`
So we can see that it runs and deletes all scripts in `/var/spool/$myname` so let's view what all is in this general
area.
- `$ ls /var/spool`
Now we can see that there is a few directories here and a symbolic link(`symlink`). The one we care about the most is the 
bandit24 directory. Since we know that the cronjob runs every so often, and deletes everything in this directory when it 
does so, lets just assume that this directory is empty. From here we can start writing our script because we can't get 
much more information than we have now. 
- `$ vim /tmp/<YOUR DIRECTORY NAME>/<NEW FILE NAME>.sh`
  - NOTE: This will open a blank text editor within the command line, it is highly suggested that you learn how to work in this particular text editor before trying to complete this level. 
In the text editor insert these lines.
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 >> /tmp/<YOUR DIRECTORY NAME>/<UNIQUE FILENAME>.txt
```
Save this file and exit VIM to return to the terminal. Copy this script we just wrote into the bandit24 sub-directory 
under `/var/spool/` after changing permissions so that the script is executable.
```bash
$ chmod 777 /tmp/<YOUR DIRECTORY NAME>/<OUR SHELL SCRIPT>.sh
$ cp /tmp/<YOUR DIRECTORY NAME>/<OUR SHELL SCRIPT>.sh /var/spool/bandit24
```
We now can either wait a few minutes for the cronjob to execute or force an execution,and then we should be able to view a new
file in our `/tmp` directory. If we `cat` out this file we should get the password for the next level. Too easy, am I right?


## Level 24 --> 25
Here we have to perform a brute force attack. So, now we aren't told much other than there is a deamon listening on port 30002
and will give us the password to level 25 when we give the correct combination of this level's password and 4-digit pin. So,
first we need to make a working directory and move into it.
```bash
$ mkdir /tmp/<UNIQUE NAME>
$ cd /tmp/<UNIQUE NAME>
```
We now need to figure out what protocol the daemon is using to listen on the port. So we need to do a `nmap`. 
- `$ nmap localhost -p 30002`
So we can see that the port is using TCP protocol and that's all we are given, but that's fine we'll just have to 
perform a test or two.
- `$ nc -l 30002` 
This returns an error saying that this address is already in use, so we may have found out which protocol this daemon
is using. Let's try another test.
- `$ nc localhost 30002`
  - NOTE: The difference between the two lines is that the `-l` argument is listening for traffic.
This allows us to interface with the daemon, so we will take note of this. Exit the `nc` session, and let's begin 
writing our brute forcer. 
- `$ vim brute.sh`
This is the script 
```bash 
#!/bin/bash
password='<bandit24 password>'
x=0
while [ $x -lt 10000 ]; do
	foo=$(printf "%04d" $x)
	echo $password' '$foo >> numbers.txt
	x=$((x+1))
done
```
Exit VIM and save the script. We now need to change the permissions on the script so that we can execute it.
```bash
$ chmod 777 brute.sh
$ ./brute.sh
```
We now need to use all of the possible inputs and perform the attack on the daemon. 
```bash
$ cat numbers.txt | nc localhost 30002 >> rezult
$ sort rezult | uniq -u
```
This attack works by inputing every possible value from the numbers.txt file we created, and outputs our results into
the file `rezult`. We then sort and pull out the unique lines from the rezult file to get the password.
	
## Level 25 --> 26
Here we are told that logging into the next level should be easy, and not much more other than the fact that when we log
in it we won't be in a standard shell session. So let's `ls` to see whether or not we are given a clue.
- `$ ls`
We are given a SSH key, so we can use that to login to level 26. 
- `$ ssh -i bandit26.sshkey bandit26@localhost`
As soon as we login we are kicked off, so we need a way to run commands to move us forward. Since we know that the shell
is a BASH shell we have to find a way to make it understand BASH code. What we must do is resize our window that we are
running the session to bandit25 so that it is so small you can only see one line with the cursor. We run the ssh command
again. 
- `$ ssh -i bandit26.sshkey bandit26@localhost`
This time we are logged in, but not kicked off immediately. This is good. So, now we want to open `VI`, which is the 
original `VIM` and let's try to work from there.
- `$ vi`
Now that we are in vi we can make our window its normal size again. From here you can open the password file by using
- `:e /etc/bandit_pass/bandit26`
This opens the password file and gives us our desired password.


## Level 26 --> 27
This level had not been created by the most recent update of this write-up.