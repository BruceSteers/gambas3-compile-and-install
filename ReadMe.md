
This is a script to help ensure the fantastic Gambas3 basic latest version can be compiled
and installed on various linux disrtros it supports.

Version 2.5.3\
Written by Bruce steers <g3compiler@bws.org.uk>\
Note. This script is not written by any of the gambas team members just a Gambas user/supporter.\
So please do not contact them for support if you have problems with running this script. Thank you.

<pre>
Intention/Introduction:
Compiling and installing Gambas3 from source can be a bit tricky if you do not have all
the correct software and dependencies you need installed first.

There is installation info on the Gambas wiki website giving a list of required packages for 
each distro but it is not auto-created and needs updating at times as things change.
Whilst trying to get the Gambas wiki pages for Debian and Raspbian up to date I asked on the 
developers mailing list for some "expert" advice. 
I was told by the main Gambas developer Benoît Minisini of a file that exists in the GitLab 
repository called ".gitlab-ci.yml" that is used when a "ppa" type install would happen. 
This file contains up to date lists of package requirements for various systems.

With this new knowledge I have made a shell script that does the following...
</pre>

+ Offers to download/clone the latest Gambas3 or lets you select an existing folder.
+ Download can use git to clone, or curl to download archive and unzip.
+ Sudo password timeout can be temporarily raised while running so you don't have to stay 
  and watch in order to catch the password request at 'make install'.
+ Offers to install ALL dependencies/packages needed for compilation/install.
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
+ Alpine (untested and supports badly, I do not reccomend using it on an Alpine system)


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
Note. This script can now do that for you (apt or pacman).


Full explanation / instructions.

Run this Script from terminal.
Either place the script in an already existing Gambas3 Gitlab clone folder and run 
it from there or it will ask to either use git to clone  the gambas dir to the current 
dir or you can select an existing downloaded dir on your disk.

By default the script tries to detect the linux version you are running. If that's not 
working it gives a list of supported linux types to choose from or you can un-comment
(delete the '#') on the #BUILD= lines at the begining of the script to manually set the 
linux version you have.

Supported variations are...
Ubuntu/Mint (various versions), Debian (various versions), Raspbian, Archlinux, Manjaro, Alpine

Note. if you are using Archlinux-clang you may need to set manually as i do not know how to 
differntiate between archlinux and archlinux-clang

Once your linux is detected if not run from the Gambas source folder you are asked to 
download a new clone or select an existing clone dir.
If downloading a new clone you are asked for a path/name for the download folder
or it defaults to 'gambas' in the current dir.

Note. if your Gambas source folder is not a GitLab clone it may be missing the vital 
".gitlab-ci.yml" file.
To fix this go to https://gitlab.com/gambas/gambas/-/blob/master/.gitlab-ci.yml
and download the .gitlab-ci.yml file and copy it to your Gambas source directory.

You are then asked if you would like the sudo password timeout temporarily extended while it runs.
(Timeout settings are restored before exitting). This is a 'fix' that has been added because
it can take a long time to compile on slow machines (like a raspberry PI) and will fail
if it gets to 'make install' and you are not around to type the root password because
sudo will only ask for password for a short time then timeout causing the automation to fail.

You are next asked a series of questions and must give a y/n/a answer.
y = YES, n = NO (default if no answer given) , a = Ask no more and say Yes to All
You can abort at any time pressing Ctrl-C.
The commands come in the following order...

** "Run dependency install?" 
 Installs ALL packages/dependencies needed to compile Gambas3.

** "Run './reconf-all' ?" 
 Sets up the compiling environment, needed first time, or to update environment.

** "Run './configure' (y for yes, v for verbose error messages only) ?"
 Configures all the source code ready for compilation.
 (./configere produces a lot of output text making error messages hard to find,
 type 'v' to only show the error messages not the rest of the output.)
 
** "Run 'make' ?"
 Compiles ALL source code ready for installation.

** "Run 'make install' ?"
 Installs Gambas into the System.

 IMPORTANT: if you already have Gambas3 on your system either installed by using your 
  package manager to install the distro's default version or via adding the PPA then
  it MUST be completely removed **first** or you will get conflicts.
  The script detects a packager installed Gambas3 and warns you that before 'make install' 
  is run it will remove the old installation for you.
  After installing from compilation Gambas3 will not show as installed by your
  package manager.

** "Install Icon, desktop launcher and menu item?"
 If yes the Gambas Icon is installed then you are given 2 options...

** "Install a desktop launcher?"
** "Install a menu launcher?"

(Icon/Launcher installation uses xdg)

A log file /home/username/gambas-compile-install.log is saved holding all the information about
commands run in the script. This was added at the request of the gambas developers so they can ask you
for the output message record if you are getting errors.

Note...
The Gambas team are very busy and did not make this script so if you
have problems please contact me about it and not them.

Unless you have problems occuring during the running of the commands 
./reconf-all 
./configure 
'make' 
'make install'

Everything else outside of those commands is for me to resolve :)
Thank you
Bruce Steers
