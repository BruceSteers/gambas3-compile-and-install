
This is a script to help ensure the fantastic Gambas3 basic latest version can be compiled
and installed on various linux disrtros it supports.

Version 2.4
Written by Bruce steers

Intention/Introduction:
Compiling and installing Gambas3 from source can be a bit tricky if you do not have all the correct software and dependencies you need installed first.
There is installation info on the Gambas wiki website giving a list of required packages for 
each distro but it is not auto-created and needs updating at times as things change.
Whilst trying to get the Gambas wiki pages for Debian and Raspbian up to date I asked on the 
developers mailing list for some "expert" advice. 
I was told by the main Gambas developer Benoît Minisini of a file that exists in the GitLab 
repository called ".gitlab-ci.yml" that is used when a "ppa" type install would happen. 
This file contains up to date lists of package requirements for various systems.

With this new knowledge I have made a shell script that does the following...

+ Offers to download/clone the latest Gambas3 or lets you select an existing folder.
+ Offers to install all dependencies/packages needed for compilation/install.
+ Offers yes or no options to run all commands needed to compile/install Gambas3
   from the './reconf-all' to the 'make install'
+ Offers to make a desktop icon and/or a menu item.

Supports..
+ Ubuntu, 
+ LinuxMint, 
+ Debian, 
+ Raspbian, 
+ Archlinux, 
+ ManjaroLinux
+ Alpine


How to use...

Simply put...
Run it from terminal, follow the instructions.
If first install say yes to everything.
Dependencies/packages will install, Gambas will compile and install, 
Desktop icon and menu are made.

IMPORTANT NOTE: any previous Gambas3 version installed from a package manager must be
removed before installing this way to avoid conflicts.
eg. type 'sudo apt-get purge gambas3*'
This is not needed to install over an existing compiled version only a repository installed one.


Full explanation / instructions.

Run this Script from terminal.
Either place the script in an already existing Gambas3 Gitlab clone folder and run 
it from there or it will ask to either download/clone to the current dir or you can
select an existing dir on your disk.

By default the script tries to detect the linux version you are running. If that's not 
working it gives a list of supported linux types to choose from or you can un-comment
(delete the '#') on the #BUILD= lines at the begining of the script to manually set the 
linux version you have.

Supported variations are...
Ubuntu/Mint (various versions), Debian (various versions), Raspbian, Archlinux, Alpine

Note. if you are using Archlinux please set manually as i do not know how to 
differntiate between archlinux and archlinux-clang

Once your linux is detected if not run from the Gambas source folder you are asked to 
download a new clone or select an existing clone dir.
If downloading a new clone you are asked for a path/name for the download folder
or it defaults to 'gambas' in the current dir.

Note. if your Gambas source folder is not a GitLab clone but an unpacked tarball it
may be missing a vital ".gitlab-ci.yml" file.
To fix this go to https://gitlab.com/gambas/gambas/-/blob/master/.gitlab-ci.yml
and download the .gitlab-ci.yml file and copy it to your Gambas source directory.

You are next asked a series of questions and must give a y/n/a answer.
y = YES, n = NO (default if no answer given) , a = Ask no more and say Yes to All
You can abort at any time pressing Ctrl-C.
The commands come in the following order...

"Run dependency install?" 
 Installs packages, needed first time or if dependencies change.

"Run './reconf-all' ?" 
 Sets up the compiling environment, needed first time, or to update environment.

"Run './configure' (y for yes, v for verbose error messages only) ?"
 Configures all the source code ready for compilation.
 (./configere produces a lot of output text making error messages hard to find,
 type 'v' to only show the error messages not the rest of the output.)
 
"Run 'make' ?"
 Compiles ALL source code ready for installation.

"Run 'make install' ?"
 Installs Gambas into the System.

 IMPORTANT: if you already have Gambas on your system either installed by using your 
  package manager to install the distro's default version or via adding the PPA then
  it MUST be completely removed first or you will get conflicts.
  on debian/ubuntu type 'sudo apt-get purge gambas3*'
  After installing from compilation Gambas3 will not show as installed in your
  package manager.

"Install Icon, desktop launcher and menu item?"
 If yes the Gambas Icon is installed then you are given 2 options...

"Install a desktop launcher?"
"Install a menu launcher?"

Icon/Launcher installation uses xdg


