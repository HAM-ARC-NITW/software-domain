- what is linux?
	- open-source, unix-like, and POSIX compliant operating system.
	- what is unix?
		- unix is an operating system developed at bell labs around 1970s which gave rise to a lot of the modern day operating systems.
		- bell labs used to license the source code of unix to other companies / institutes for a fee.
		- this led to a lot of different derivatives of unix which were not compatible with each other.
		- this led to the creation of POSIX (portable operating system interface) which is a family of standards which specifies how a unix-like operating system should behave. basically equivalent to "USB standard" but for operating systems.
			- this is one of the reasons why you can't run bash scripts out of the box on windows because it is not POSIX compliant. whereas, macOS is compliant.
	- why is it useful?
		- it is free and open source: anyone can view, modify and redistribute it.
			- https://upload.wikimedia.org/wikipedia/commons/1/1b/Linux_Distribution_Timeline.svg
		- scripting is treated as a first-class citizen
			- this is one of the main reasons why linux is prominent within cloud infrastructure
			- and this also makes it a great operating system for developers

- what is a shell?
	- shell is a program that gives you a way to interact with the operating system. it takes in actions which you want to do, tells the OS what needs to be done and shows the result
	- `bash` is one such command-line shell aka text-based, where you type commands and see the results.
	- other shells include `fish`, `zsh`
	
- hello world!
	- `echo "Hello, World!"`

- need some quick help? just ask `man`
	- https://xkcd.com/1692/
	- is `man` too complicated? use `tldr`: https://tldr.sh/

- file system
	- the interesting thing about linux is that everything is a file: external devices (`/dev`), processes (`/proc`) etc.
	- compared to windows, in linux, everything starts from a single root - `/`. there is no concept of separate drives like `C:\`, `D:\`
	- here are some of the important top-level directories:
		- `/home`: equivalent to "Users" directory on windows
		- `/etc`: system-wide configuration files
		- `/bin` and `/usr/bin`: executable programs
		- `/var`: mainly used to store logs 
		- `/tmp`: temporary files, which are cleared on reboot
	
- navigating the file system:
	- `pwd`: shows current working directory
	- `ls`: lists directory contents
		- hidden files: any file whose name starts with "." is hidden by default
		- use `ls -a` to also show the hidden files
	- `cd`: change working directory
	- `mkdir`: make new directory / create new folder
	- `touch`: creates new file
	- `rm`: remove file / directory
		- `-r`: recursive
		- `-f`: ignore nonexistent files
	- `cp`: copy file / directory
	- `mv`: move files
	- absolute paths: refers to the complete path of the file and it is based of the root dir (`/`). the absolute path of a file / directory remains the same irrespective of from where it is referred from in the system
	- relative paths: refers to the path from the pov of the current working dir. the relative path of a file / directory changes based on where you're currently present in the system. 
		- `./`: points to the current working directory
		- `../`: points to the immediate parent of the current working directory

- working with text files
	- `cat`: concatenate files and print their contents
	- `less`: view files in a nice pager-like interface
	- `head`: print the first N lines of a file
	- `tail`: print the last N lines of a file
	- `nano`: a simple terminal based text editor
		- use `Ctrl+O` to save the file
		- use `Ctrl+X` to exit
	- redirections
		- `|` (pipe): take the output of one command and feeds it as input to the next command
		- `>` (overwrite redirect): passes the output of a command to a file. it overwrite the content i.e. replaces the existing the content
		- `>>` (append redirect): same as above but instead of overwriting, it appends the new content at the end

- additional commands related to working with files
	- `find`: used to search for files
		- `-name`: search based on file name (or a pattern which it follows)
		- `-iname`: case-insensitive search
		- `-type`: search by type
			- `f`: only files
			- `d`: only directories
		- `-size`: search by size
		- `-delete`: delete matching files
		- `-exec`: run a command on each match
			- `{}` is used a placeholder for the matching filename
	- `wc`: used to count the number of words / characters / lines in a file
		- `-l`: count number of lines
		- `-w`: count number of words
		- `-c`: count number of characters
	- `grep`: used to search for text patterns in files
		- `-i`: case-insensitive search
		- `-r`: recursive i.e. search for this pattern in all the files present in that directory
		- `-n`: show lines numbers where this pattern was found
		- `-v`: invert search i.e. show lines which don't match
		- `-c`: count number of total matching lines

- file permissions
	- every file / directory on linux has exactly one owner and group attached to it
	- owner
		- the user who created that file / directory
		- by default, has the most control over that file / directory and can also change its permissions
	- group
		- a way to share access of the file among multiple users at once
	- `ls -l` (ex: `drwxr-xr-x`)
		- first character: file type
			- `-`: regular file
			- `d`: directory
			- `l`: symbolic link
				- basically a pointer to another file / directory
		- next 9 characters are permissions, grouped as 3 characters per permission
			- `rwx`: owner permission
			- `r-x`: group permission
			- `r-x`: others permission
	- `chmod`: used to modify permissions
		- `chmod u`: change permissions for owner
		- `chmod g`: group
		- `chmod o`: others
		- `chmod a`: all
		- `chmod g-w`: remove write permission for the group
		- `chmod 755`: 
			- `r = 4`, `w = 2`, `x = 1`
			- `7` (owner permission): 4 + 2 + 1 (`rwx`)
			- `5` (group permissions): 4 + 1 (`r-x`)
			- `5` (other permissions): 4 + 1 (`r-x`)
	- `chown`: used to change owner of a file
	- misc:
		- `useradd`: used to create a new user
			- `-m`: create home directory
			- `-s`: specific shell
			- `-G`: to which groups is this user is to be added to
		- `passwd`: used to change password of a user
		- `su`: used to change user

- bash scripting
	- shebang (`#!`)
		- tells the OS which interpreter is to be used to execute this script
		- for bash, use `#!/bin/bash`
	- variables
		- create variables using `a=` syntax
		- access them using `$a`
	- arguments
		- `$1, $2, $3`: used to access the arguments which are passed while running the bash script
		- `$@`: all the arguments as space-separated words
		- `$#`: number of arguments
	- if/else
		```bash
		if [ condition ]; then

		fi
		```
		- for strings:
			- `==`, `!=`, `-z` (used to check if string is empty or not), `-n` (opposite of `-z`)
		- for numerics:
			- `-eq`, `-ne`, `-gt`, `-lt`
		- for files / directories:
			- `-f`, `-d` (whether they exist)
	- for loops
		```bash
		for variable in ...; do
		
		done
		```
		- create ranges using `{start..end}` syntax
			- in bash, the `end` is also exclusive i.e. `[start, end]` is the range and not `[start, end)`
	- functions
		```bash
		function_name() {
			...
		}
		```
		- use `local` keyword to define a local variable so that if there is some variable in the outer scope with the similar name, then it wouldn't get updated
	- pipefail
		- https://gist.github.com/mohanpedala/1e2ff5661761d3abd0385e8223e16425
	- bash has a LOT of weird quirks which led to real outages, here are good videos covering details of some of those outages:
		- how hp accidently deleted all the research files from kyoto university's cluster which were older than 10 days due to a wrongly timed update to their log cleanup bash script: https://youtu.be/Nkm8BuMc4sQ
		- how steam's linux client ended up deleting all the files from the root folder if the steam folder has been moved/symlinked somewhere else: https://youtu.be/qzZLvw2AdvM
		- how quirky-ness of how bash pipelines exit caused outage in cloudflare: https://youtu.be/kUtarOlOT3Y 

- what's next?
	- linux in general is just way too huge to cover within a single session, as it involves a broad range of concepts. treat the session as a _primer_ to the world of linux and bash scripting.
	- as you tinker around more with linux and bash, you'll get more familiar with it.
	- based on what you liked from the session, here are a couple of options which you can explore next:
		- did you like the concept of linux and want to play around with it?
			- play around with linux on a virtual machine to check whether all the apps which you daily drive are compatible with linux, or if there's a suitable workaround for your use case.
			- initially, try it out on a virtual machine using [virtualbox](https://virtualbox.org), and if satisfied with the experience, go ahead with dual booting linux along with windows.
			- start with a simple ubuntu / debian based distro initially. my recommendation would be linux mint, which is based on ubuntu and is quite minimal in terms of the software that gets packed along with it, as well as its graphical interface.
			- if you're on macOS:
				- on an intel-based mac, you can dual-boot via boot camp, or just use virtual machine like virtualbox. you'll have almost similar experience to windows.
				- on an apple silicon (M1/M2/M3) mac, check out [asahi linux](https://asahilinux.org). it's still quite experimental, so i wouldn't recommend daily-driving it unless you know what you're doing.
		- do you want to explore more about command-line utilies?
			- apart from command-line tools which we've covered in the sesh, there are a lot more. some of the interesting ones which you can explore further:
				- `curl`: a tool for fetching stuff from the web. it supports a huge range of protocols apart from HTTP/HTTPS. list of all the protocols which it supports are listed over here: https://curl.se/docs/manpage.html
				- `tmux`: for terminal sessions which you keep running in background and attach back later in future aka persistent terminal sessions: https://github.com/tmux/tmux/wiki
				- `jq`: for processing json data: https://jqlang.org
				- `awk`: for processing structure text files based on columns / fields: https://www.gnu.org/software/gawk/manual/gawk.html
				- `rigrep`: a fast grep-like search tool optimized for tasks related to searching in source code files: https://github.com/BurntSushi/ripgrep
				- `zoxide`: a "smarter" version of `cd`: https://github.com/ajeetdsouza/zoxide
				- `fzf`: a file fuzzy finder: https://github.com/junegunn/fzf
			- also, try exploring your distro's package manager to get familiar with how to install software tools via them
			- the linux documentation project (tldp) also has a really nice guide for bash scripting: https://tldp.org/LDP/abs/html
			- you can also go through the following two lectures from "missing semester" course:
				- https://missing.csail.mit.edu/2026/course-shell
				- https://missing.csail.mit.edu/2026/command-line-environment
		- anything which is not covered over here? drop a message in the group and we'll try to help you out 