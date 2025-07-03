# Important Git notes

$\color{red}{git \ config}$ that lets you get and set configuration variables that control
all aspects of how Git looks and operates. These variables can be stored in three different places:

 $\color{red}{[path](//)etc(//)gitconfig}$ file: Contains values applied to every user on the system and all their
 repositories. If you pass the option --system to git config, it reads and writes from this file
 specifically. Because this is a system configuration file, you would need administrative or
 superuser privilege to make changes to it.
