---
title:  "Terminal Introduction"
date:   2016-12-05 23:20:07 +0100
categories: jekyll update
---

When it's quite a lot you use the terminal on Linux you don't even realize how many things you take for granted and you often forget how much time did you need to learn it all. But when you see a beginner you all of a sudden remember how much did you fight with that thing and how happy you were when you learned that shortcut that makes you look like a ninja.
Here a very beginner guide to have an easier life with you terminal.

A very first thing is:

>The terminal is 'case-sensitive'.
>It means that 'cat' is different than 'Cat' or 'CAT'.

>The terms _"directory"_ and _"folder"_ nowadays are basically the same. However, historically, _directory_ is mostly related to command line and _folder_ to a graphical interface.

#### **Appearance:**

When you open a new terminal from the menu you are always in you home
directory (the one that contains your Desktop, Document, Music, etc folders) and
this is the only thing that appears:

```sh
myUser@myHost:~$
```

This is called *prompt* and is telling you that the system is ready to receive your command. The tilde "``~``" before the dollar is telling: *"you are in your **home** directory"*.
The structure of a prompt it's usually:

```sh
username@hostname:path/of/your/current/directory$
```

#### **First command:**
With a lot of immagination you can figure out that to run a command you have to write the command and press _Enter_.
The directory where you are with your terminal is called _working directory_ and if you just opened a terminal, you are in your *home* directory. If you wanna a prove of it you can **P**rint your **W**orking **D**irectory with the `pwd` command:
```sh
myUser@myHost:~$ pwd
/home/myUser
```

If you want to know more about the directories before your username try to read something about _Linux filesystem structure_.

#### **Navigation:**
A first useful thing could be to *list* what you have in your working directory with the `ls` command:

```sh
myUser@myHost:~$ ls
Documents     Downloads       Music      Dropbox
myscript.sh   Videos          Pictures   Public
Desktop       helloworld.py
```

as you can imagine this is the short for **L**i**S**t.


To **C**hange **D**irectory you'll use for example:
```sh
myUser@myHost:~$ cd Desktop
myUser@myHost:~/Desktop$
```

>AUTO-COMPLETE: You can just type `$ cd Des` and press 'Tab' to autocomplete the word 'Desktop'. If you type only `$ cd D` it will not autocomplete because it has multiple choices and if you press another time 'Tab' you'll see the alternatives (Desktop, Documents, Downloads) so you just continue to write till you have only an unique alternative.

If you wanna go to the parent directory you use:

```sh
myUser@myHost:~/Desktop$ cd ..
myUser@myHost:~$
```
If you find yourself in some long directory structure and you wanna go directly to the home folder you use `~` as argument of `cd` command:

```sh
myUser@myHostName:~/Desktop/dir1/dir2/some/thing/here$ cd ~
myUser@myHostName:~$
```

>HISTORY: You can navigate through the history of the command you typed with the up and down arrows of your keyboard.

>COPY and PASTE: In order to copy and paste something you can use the right click menu or 'Ctrl + Shift + c', 'Ctrl + Shift + v'.

>DRAG and DROP: Even experienced guys often don't know that you can actually drag and drop files or folders in your terminal in order to have the full path instead of typing it or using copy and paste.
i.e. You can type `cd ` then just drag and drop the directory you want.

>IMPORTANT: If in a folder or file name there is a whitespace it's better to put the path between quotation mark (single or double); otherwise you have to put a backslash ('`\`') before each space. This because in the terminal every argument of a command is separated by space. With quotation marks you are just saying `'this is/a unique string/ no_matter what/inside'`. Alternatively the backslash is called *escape character* and is saying to the terminal that the following character is not a special character (separator between two arguments in this case) but is part of one argument. `$ cd my\ folder\ in\ here` is saying to `cd` that `"my folder in here"` is only one argument (not 4). That's why coders usually use underscores or dashes instead of whitespaces.
