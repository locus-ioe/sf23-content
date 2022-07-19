---
title: "Miscellaneous: Command line cheatsheet"
date: 2022-07-08
tags: []
draft: false
weight: 10
---

# Command line cheatsheet for Day 9

## Connect to remote host

`ssh -i <path-to-key> username@IP`

Explanation:
`-i` stands for identity, we have to show our identity before entering into our remote host

`username`: our remote host will have user created when creating the vm,so wh have as which user we want to enter our remote host.

## Copy file from local lost to remote host

`scp -i <path-to-key> <file-path-to-copy> <username>@IP:<remote-path>`

## Printing currenting working directiory

`pwd`

Explanation:
When we are in the command line we are always inside some folder/directory, this command prints where in the file system we currently are

## List files and folders in current directory

`ls` : this list the files and folders in current directory

`ls -a`: to show all files and folders including hidden one

`ls -l` to show detailed view

`ls -al`: we can combine flags this will show all files and folder in detailed view

## Changing the directory

`cd <directory-path>`

Examples:
`cd /etc/nginx` : Absolute path
`cd conf.d`: Relative path

Absolute path : Path start from the root
Relative path : Path start from current working directory

## Create directory

`mkdir <directory_name>`

To make nested directory:

`mkdir -p first/second`: create directory named "first" inside "first" will be "directory named "second"

## create files

`touch <filename>`

## delete/remove files

`rm <file-path>` file path may include regular expression

Examples:

`rm test.py` (deletes test.py file in current folder)

`rm *.py` (deletes all python files in current folder)

## Remove Directory:

`rm -rf <directory-path>` also supports regular exrpressions

## Git commands

`git clone <remote-url>` : clone remote repository

## Basic vim command

open file for edit: `vim <filepath>`

Vim has two modes, insert mode and command mode, insert mode is used to insert text in the file, command mode is used to navigate the file

enter insert mode : Press `i`

enter command mode : Press `ESC`

Command mode bindings/shortcuts

write and exit : `:wq` (In command mode press `:` and then press w, then q then hit `ENTER`)

exit without writing :`q!`

---

move cursor down : `j`

move cursor up : `k`

move cursor left : `h`

move cursor right : `l`

find text: :`/<text>`

Paste the content from clip board :`Ctrl + Shift + v` (in insert mode)

## Nginx commands

Edit nginx.conf : `sudoedit /etc/nginx/nginx.conf`

start service : `sudo systemctl start nginx`

service status : `sudo systemctl status nginx`

stop service : `sudo systemctl stop nginx`

test nginx configuration : `sudo nginx -t`

reload configuration : `sudo nginx -s reload`
