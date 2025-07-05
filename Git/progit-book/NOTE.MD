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

git diff command
    use it most often to answer these two questions: What have you
    changed but not yet staged? And what have you staged that you are about to commit? Although git
    status answers those questions very generally by listing the file names, git diff shows you the
    exact lines added and removed — the patch, as it were.

 If you want to see what you’ve staged that will go into your next commit, you can use git
    diff --staged. This command compares your staged changes to your last commit:
    and git diff --cached to see what you’ve staged so far (--staged and --cached are synonyms):

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

## commit

Adding the -a option to the git commit command makes
 Git automatically stage every file that is already tracked before doing the commit, letting you skip
 the git add part

## Removing Files

git rm PROJECTS.md\
force the removal with the -f option\
git rm -f this forces the file or folder that was already modified or in a staged area

 Another useful thing you may want to do is to keep the file in your working tree but remove it from
 your staging area. In other words, you may want to keep the file on your hard drive but not have
 Git track it anymore. This is particularly useful if you forgot to add something to your .gitignore
file and accidentally staged it, like a large log file or a bunch of .a compiled files. To do this, use the--cached option:
 $ git rm --cached README

You can pass files, directories, and file-glob patterns to the git rm command. That means you can do
 things such as:
 $ git rm log/\*.log

## Logging

By default, with no arguments, git log lists the commits made in that repository in reverse
 chronological order; that is, the most recent commits show up first.

git log\
Used to look the history of commits

One of the more helpful options is -p or --patch, which shows the difference (the patch output)
 introduced in each commit. You can also limit the number of log entries displayed, such as using -2
 to show only the last two entries

git log -p -2\

 Common options to git log\
 Option                 Description
-p                  Show the patch introduced with each commit.\
--stat              Show statistics for files modified in each commit.\
--shortstat         Display only the changed/insertions/deletions line from the --stat command.\
--name-only         Show the list of files modified after the commit information.\
--name-status       Show the list of files affected with added/modified/deleted information as well.\
--abbrev-commit     Show only the first few characters of the SHA-1 checksum instead of all 40.
--relative-date     Display the date in a relative format (for example, “2 weeks ago”) instead of
                    using the full date format.\
 --graph            Display an ASCII graph of the branch and merge history beside the log output.
 --pretty           Show commits in an alternate format. Option values include oneline, short,
                    full, fuller, and format (where you specify your own format).
 --oneline          Shorthand for --pretty=oneline --abbrev-commit used together.

if you want to see some abbreviated stats for each commit, you can use the --stat option:\

git log --stat

Another really useful option is --pretty

git log --pretty=oneline\
git log --pretty=short\
git log --pretty=full\
git log --pretty=fuller\
git log --pretty=format\
e.g for format\
git log --pretty=format:"%h - %an, %ar : %s"

 Useful specifiers for git log --pretty=format lists some of the more useful specifiers that format
 takes.\
 Table 1. Useful specifiers for git log --pretty=format\
 Specifier Description of Output\
 %H Commit hash\
 %h Abbreviated commit hash\
 %T Tree hash\
 %t Abbreviated tree hash\
 %P Parent hashes\
 %p Abbreviated parent hashes\
 %an Author name\
 %ae Author email\
 %ad Author date (format respects the --date=option)\
 %ar Author date, relative\
 %cn Committer name\
 %ce Committer email\
 %cd Committer date\
 %cr Committer date, relative\
 %s Subject\
