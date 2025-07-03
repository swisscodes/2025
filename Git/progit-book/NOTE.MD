# Important Git notes

$\color{red}{git \ config}$ that lets you get and set configuration variables that control
all aspects of how Git looks and operates. These variables can be stored in three different places:

1. $\color{red}{[path]/etc/gitconfig}$ file: Contains values applied to every user on the system and all their
 repositories. If you pass the option --system to git config, it reads and writes from this file
 specifically. Because this is a system configuration file, you would need administrative or
 superuser privilege to make changes to it.

2. ```~/.gitconfig \ or ~/.config/git/config``` file: Values specific personally to you, the user. You can
 make Git read and write to this file specifically by passing the --global option, and this affects
 all of the repositories you work with on your system.
3. config file in the Git directory (that is, .git/config) of whatever repository you’re currently
 using: Specific to that single repository. You can force Git to read from and write to this file with
 the --local option, but that is in fact the default. Unsurprisingly, you need to be located
 somewhere in a Git repository for this option to work properly.
 Each level overrides values in the previous level, so values in .git/config trump those in
 [path]/etc/gitconfig.
 On Windows systems, Git looks for the .gitconfig file in the $HOME directory (C:\Users\$USER for
 most people). It also still looks for [path]/etc/gitconfig, although it’s relative to the MSys root,
 which is wherever you decide to install Git on your Windows system when you run the installer. If
 you are using version 2.x or later of Git for Windows, there is also a system-level config file at
 C:\Documents and Settings\All Users\Application Data\Git\config on Windows XP, and in
 21
C:\ProgramData\Git\config on Windows Vista and newer. This config file can only be changed by git
 config -f `<file>` as an admin.
 You can view all of your settings and where they are coming from using:
 $ git config --list --show-origin

## clone

 $ git clone <https://github.com/libgit2/libgit2> mylibgit

## Checking the Status of Your Files

$ git status
Short Status
git status -s

 New files that aren’t tracked have a ?? next to them,
 new files that have been added to the staging area have an A,
 modified files have an M and so on

## .gitignore

The rules for the patterns you can put in the .gitignore file are as follows:
 • Blank lines or lines starting with # are ignored.
 • Standard glob patterns work, and will be applied recursively throughout the entire working
 tree.
 • You can start patterns with a forward slash (/) to avoid recursivity.
 • You can end patterns with a forward slash (/) to specify a directory.
 • You can negate a pattern by starting it with an exclamation point (!)

 Glob patterns are like simplified regular expressions that shells use. An asterisk (*) matches zero or
 more characters; [abc] matches any character inside the brackets (in this case a, b, or c); a question
 mark (?) matches a single character; and brackets enclosing characters separated by a hyphen ([0
9]) matches any character between them (in this case 0 through 9). You can also use two asterisks to
 match nested directories; a/**/z would match a/z, a/b/z, a/b/c/z, and so on.

\# ignore all .a files\
*.a

\# but do track lib.a, even though you're ignoring .a files above\
 !lib.a

\# only ignore the TODO file in the current directory, not subdir/TODO\
\TODO

\# ignore all files in any directory named build\
 build/

\# ignore doc/notes.txt, but not doc/server/arch.txt\
 doc/*.txt

\# ignore all .pdf files in the doc/ directory and any of its subdirectories\
 doc/**/*.pdf
