---
layout: post
title:  "File Permissions for Beginners"
date:   2017-02-20 23:20:07 +0100
categories: jekyll update
---

This is a quite sensitive topic in every system. Everyone should deeply
understand and do not underestimate how to deal with permissions.

#### **What you can do?**
- guarantee privacy among users,
- extract data from a non working system with a live CD,
- expose sensitive data (be careful).

#### **What permissions are?**
Every file or directory has a way to specify who can or cannot read/write/execute it. In this document we will often use files as example but it works exactly in the same way for directories.

>WARNING: Permissions can protect your data from other (same level) users only when the
system is running.
Permissions cannot protect you in any case against a root user or an amministrator with higher privilegies than yours. For this purpose you should use encryption.

#### **Appearance:**

A way to indicate permissions is to use 3 letters `rwx` (**Symbolic notation**). When the letter is present it means you can:
- `r` = Read (see the file in the directory and display the content)
- `w` = Write (edit or delete the file)
- `x` = eXecute (without this you cannot execute scripts or executables)

otherwise you see a `-`. For example:
- `rw-` you can read and write, you cannot execute.
- `r--` you can only read.
- `r-x` you can read and execute, you cannot edit.

In real files you have permissions for `u` user, `g` group and `o` others (unspecified users). It works this way:
```
rwxrwxrwx
^^^        u - user (owner)
   ^^^     g - group (a group of users you can specify)
      ^^^  o - others (everyone else)
```

Use the command `ls -l` (often just `ll`) to show the exensive details about your files:

```sh
myUser@myHost:~$ ls -l
total 12
-rw-rw-r--. 1 myUser myGroup   28 Nov  9 02:14 aFile.txt
-rw-rw-r--. 1 myUser myGroup 1302 Nov  9 02:14 index.html
drwxr-xr-x. 2 myUser myGroup 4096 Nov 13 23:54 aDirectory
```
In every line we have the 1st character that indicates what kind of element is. In this case `-` for files and `d` for directories. The next 9 characters are our permission 3 for owner, 3 for group and 3 for others.

#### **How to change permissions:**
You can use the command `chmod` (change mode) to specify `=` (and override) permissions or simply add `+` and remove `-` them from `u` user, `g` group, `o` others or `a` all the previous at the same time.

This example adds _x_ permission for the user to _aFile.txt_:
```sh
myUser@myHost:~$ chmod u+x aFile.txt
myUser@myHost:~$ ls -l
total 12
-rwxrw-r--. 1 myUser myGroup   28 Nov  9 02:14 aFile.txt
-rw-rw-r--. 1 myUser myGroup 1302 Nov  9 02:14 index.html
drwxr-xr-x. 2 myUser myGroup 4096 Nov 13 23:54 aDirectory
```
Here we remove all permission for group and others to _aFile.txt_ (multiple permission separated by comma. Only the user will be able to _rwx_ the file, all members of the group and others will not even be able to see this file in the directory):
```sh
myUser@myHost:~$ chmod g-rwx,o-rwx aFile.txt
myUser@myHost:~$ ls -l
total 12
-rwx------. 1 myUser myGroup   28 Nov  9 02:14 aFile.txt
-rw-rw-r--. 1 myUser myGroup 1302 Nov  9 02:14 index.html
drwxr-xr-x. 2 myUser myGroup 4096 Nov 13 23:54 aDirectory
```
And now we give read permission to all at the same time:
```sh
myUser@myHost:~$ chmod a+r aFile.txt
myUser@myHost:~$ ls -l
total 12
-rwxr--r--. 1 myUser myGroup   28 Nov  9 02:14 aFile.txt
-rw-rw-r--. 1 myUser myGroup 1302 Nov  9 02:14 index.html
drwxr-xr-x. 2 myUser myGroup 4096 Nov 13 23:54 aDirectory
```

#### **Numeric notation:**
With the _chmod_ command could be useful to have a shorter alternative (yep, we're lazy people).
We can assign a number to every option:

```
r-- = 4
-w- = 2
--x = 1

-wx = 3    (2+1)
r-x = 5    (4+1)
rw- = 6    (4+2)
rwx = 7    (4+2+1)
```
In this way I can have only 1 character instead of 3.

```
755  rwxr-xr-x
^    u=rwx
 ^   g=rx
  ^  o=rx
```
hence we can use `chmod 755 myfile` instead of `chmod u=rwx,g=rx,o=rx myfile` or `chmod u=rwx,go=rx myfile`.

#### **Useful examples:**
_chmod_ has a lot of options, you can see them all in the man page (`$ man chmod`). Here few useful examples:

- `chmod --reference=file1 file2`   to copy permissions from a file to another
- `chmod u+x *` adds `x` to user in all files and directories that are present in your current working directory (it doesn't effect subdirectories)
- `chmod -R 755 path/to/myDirectory`   **R**ecursive option to change them all in files/directories/subdirectories

#### **You may be intrested in:**
- `chown`
- `sticky bits`

#### **References:**
- [archinux documentation](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)
- [wikipedia](https://en.wikipedia.org/wiki/File_system_permissions)
