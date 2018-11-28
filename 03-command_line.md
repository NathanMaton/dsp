# Learn command line

TEST

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

Top 8 from list of items above:
ls
mkdir
rm -r mydir
touch file1
rm file1
mv file1 file1a
defaults write com.apple.finder AppleShowAllFiles YES.
cp source destination

2 new ones:
cd = change directory
Ctr + A = go to beginning of line you're typing on 
Ctr + E = end of line
Ctr + L = clears screen 
Ctr + C = kills program
---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls` - shows all non-hidden files in directory  
`ls -a` - shows hidden and non hidden files in a directory
`ls -l`  - shows files with their read/write permissions and more metadata
`ls -lh`  - To display file size in human readable form
`ls -lah - shows hidden files with size in a human readable form`  
`ls -t`  -sorts files by modification time
`ls -Glp` -G removes groups, p appends directories

> > see above for list of what commands do.
---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > My response:
ls -c displays by timestamp
ls -r displays in reverse order
ls -u displays files by access time
ls -q displays all nonprinting characters as ?
ls -i Displays inode for each file
---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> >xargs is like a function from my quick reading of it. You can give it input variables and a command or function to call. Example:

''' echo '1 2 3' | xargs touch
'''

That command will create 3 files called 1 2 3 in the current directory.

 

