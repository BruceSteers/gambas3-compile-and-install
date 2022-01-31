### Download / configure / compile and install Gambas


This is a script (2 scripts) to help ensure the fantastic Gambas3 basic latest version can be  
downloaded, compiled and and installed on various linux disrtros it supports.

### Requirements..
git or curl are required for downloading.\
The script will ask to install either dependending on choice if not installed already.\
This script is designed primarily to use git. It makes sense to install git as then updates will only
download the updated files and not the whole archive each time.

### Notes:
* Using curl works but is mostly untested as I use the git method myself.
* The first script **gambas3-download-and-install-dependencies** is also fairly untested as i never use it. I downloaded my gambas git clone a long time ago and I now just use the update/compile script.

Version 3.4\
Written by Bruce steers g3compiler@bws.org.uk\
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
repository called ".gitlab-ci.yml" that is used by GitLab itself to test compiling of Gambas.
This file contains an up to date lists of package requirements for various systems.

With this new knowledge I have made 2 shell scripts that do the following...
</pre>

* One offers to download/clone the latest Gambas3 or lets you select an existing folder.
* Download can use git to clone, or curl to download archive and unzip.
* Both offer to install ALL dependencies/packages needed for compilation/install of Gambas.
* Checks if any new dependencies/packages have been added.
* The install script offers yes or no options to run all commands needed to compile/install Gambas3
   from the './reconf-all' to the 'make install' or "yes to all" can be selected anytime to
   fully automate the process.
* Sudo password timeout can be temporarily raised while running so you don't have to stay
  and watch in order to catch the password request at 'make install'.
* Offers to make a desktop icon and/or a menu item.

Supports..
* Ubuntu,
* LinuxMint,
* Debian,
* Raspbian,
* Archlinux,
* ManjaroLinux
* Fedora (latest)\
(Fedora is a new addition, i have yet to work out how to list non-installed packages so it runs **dnf install** on all dependencies each time.
(already installed packages are skipped))

- Alpine (untested and unsupported, I do not reccomend using it on an Alpine system)

If your system or a close derivitive is not on that list this script may or may not work.\
You can try it, at worst

How to use...

Simply put...\
Run it from terminal, follow the instructions.

Firstly run 'gambas3-download-and-install-dependencies'\
This to download (if you have not already) the latest beta or stable versions using
'git clone' or 'curl' to download an archive and unpack it to a folder or selecting an existing folder.
Also this is for installing ALL dependency packages required to compile gambas.

You should only need to run the above script once. (the next script also checks for updates/dependency changes)

Then run 'gambas3-update-compile-and-install'\
This gives you options to select what part of the compiling proccesses you want to do
and has an update mode that will check for updates using git and only re-compile if updates were found.

----------------------------

Full explanation / instructions.


Run this Script from terminal.\
Either place the script in an already existing Gambas3 Gitlab clone folder and run
it from there or it will ask to either use git to clone the gambas dir to the current
dir or download the zip archive using curl and unpack or you can select an existing
downloaded dir on your disk.\
If downloading a new clone you are asked for a path/name for the download folder
or it defaults to 'gambas' in the current dir.

By default the script tries to detect the linux version you are running. If that's not
working it gives a list of supported linux types to choose from.

Supported variations are...
Ubuntu/Mint (various versions), Debian (various versions), Fedora (latest), Raspbian, Archlinux, Manjaro

Note. if you are using Archlinux-clang you may need to set manually as i do not know how to
differntiate between archlinux and archlinux-clang (it may well just work)

Once your linux is detected if not run from the Gambas source folder you are asked to
select an existing dir on first run then this directory path is saved.

Note. if your Gambas source folder is not a GitLab clone it may be missing the vital
".gitlab-ci.yml" file.\
To fix this go to https://gitlab.com/gambas/gambas/-/blob/master/.gitlab-ci.yml
and download the .gitlab-ci.yml file and copy it to your Gambas source directory.

You are then presented with an options page where you can set how you want to compile.

Main compilation/install consists of 4 parts...\
    $ ./reconf-all\
    $ ./configure -C &lt;options&gt;\
    $ make\
    # sudo make install

ALL procedures can be run or you can select what ones you want.\
Beside each command there is a number/letter that if entered will toggle or run the chosen
option/command.\
You can select **A** for ALL 4 commands or *0* for none.

There are also the following options...

Enter **R** to Remeber the choices for the next time you run the script. Usefull as ./reconf-all 
is not needed so often, I have mine set to do all but ./reconf-all and if i'm getting a problem 
then i re-enable it but mostly it isn't needed.

Enter **F** to forget your choices from the next \'make install sudo choice\' screen.\
The script could be completely autonomous but for one point/problem.\
The compile can take some time especially on slow machines, sudo will ask for password at 2 points in this script.\
First if any dependencies need installing (but not if not) and then for *\'make install\'* and if you are not watching
the compilation (ie. making dinner or something) it will get to *make install* and ask for the password and Timeout if not entered in time.\

Typing the password at the start of the process will only help if reconf, configure and make take less than 15 minutes as sudo has a 15 minute timeout by default.\
So if not set to stop and ask before performing each step the script offers to either pause before running *\'make install\'* and await your input before continuing or it can temporarily up the sudo timout limit to 2 hours.\
Once chosen and if \'Remember Choice\' was selected you will not be asked this question again unless you type *F* on th e main options page.

You can be asked a series of questions to give a y/n/a answer before each command is run.\
y = YES, n = NO (default if no answer given) , a = Ask no more and say Yes to All\
Note. Selecting a for yes to all after the proceses have begun will not activate the make install pause or upping sudo timeout.\
You can abort at any time pressing Ctrl-C.\
The commands come in the following order...

#### "Check git for updates?
This runs 'git pull' on the folder and downloads any new changes.


#### "Run dependency install?"
For the initial setup script\
 Installs ALL packages/dependencies needed to compile Gambas3.\
For the compiler script.\
 Checks if any new dependencies have been added and offers to install if so.

Both scripts use the official package list obtained from the .gitlab-ci.yml included with gambas.

#### "Run \'./reconf-all\' ?"
   Sets up the compiling environment, needed first time, or to update environment
   for compilation depending on your software. (use this if compilation was working without
   it but stops, sometimes a change happens at this level but for the most part updates won't need this step)

#### "Run \'./configure\' ?"
 Configures all the source code ready for compilation.
 (./configure produces a lot of output text making error messages hard to find,\
 type \'**v**\' to only show the error messages not the rest of the output.)\
 (Note, if you wish to send an output log as a report of compilation faliure
 to the gambas team be sure not to this feature so all the messages shows)

#### "Run \'make\' ?"
 Compiles ALL the C source code (mostly) ready for installation.

#### "Run \'make install\' ?"
Compiles all the gambas components and Installs Gambas into the System.

 IMPORTANT: if you already have Gambas3 on your system either installed by using your
  package manager to install the distro's default version or via adding the PPA then
  it MUST be completely removed **first** or you will get conflicts.
  The script detects a packager installed Gambas3 and warns you that before 'make install'
  is run it will remove the old installation for you.
  After installing from compilation Gambas3 will not show as installed by your
  package manager.


#### "Install a desktop launcher?"
Uses the gambas.desktop file to create a desktop launcher icon.

#### "Install a menu launcher?"
Newer verisons of gambas should install the menu launcher themselves but on some versions menu installing was broken so this will do it.

(Icon/Launcher installation uses xdg)

Press **E** toggle between showing ./configure \'checking\' messages adds the *-q* option.

Press **X** for a full cleanup.\
This will firstly run...\
*sudo make uninstall*\
To completely remove gambas from your system. then it runs...\
*make distclean*\
This cleans all the source folder files previously made on compile so they are re-made suitable for another distribution if needed.

You can also enter **C** to then type any command in the source folder.

<hr width=50%>

A log file /home/username/gambas-compile-install.log is saved holding all the information about
commands run in the script. This was added at the request of the gambas developers so they can ask you
for the output message record if you are getting errors.
*Note. Do not select the "Show Config errors only" option if you are sending this scripts output as an 
error report to gambasHQ as they need to see all the output to better detect any issues)

Additional Note...\
The Gambas team are very busy and did not make this script so if you
have problems with the script please contact me about it and not them.
If you have problems with the compilation not the script then contact them not me ;)
Any problems occuring during the running of the commands...\
./reconf-all\
./configure\
make\
make install\

Everything else outside of those commands is for me to resolve :)\
Thank you\
Bruce Steers

<hr width=50%>

Snapshot (main options page)
<img src="http://bws.org.uk/images/gci.png">
