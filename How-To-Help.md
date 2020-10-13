
In order to add an unsupported linux distribution type like i did with Raspbian\
I need to know a couple of things..

If your distribution is not supported then i need to know the lsb details.

The output from the command lsb_release -a\
if you open a terminal and type 'lsb_release -a' then copy and pase the resulting text.\
On my Debian it look like this..

**bonus@bonus-pc:~$ lsb_release -a\
No LSB modules are available.\
Distributor ID:	Debian\
Description:	Debian GNU/Linux 10 (buster)\
Release:	10\
Codename:	buster**

If there are components disabled running ./configure then the **error** output from ./configure I will need.\
Use the following command...

**./configure -C >/dev/null**

and send me the error output.

