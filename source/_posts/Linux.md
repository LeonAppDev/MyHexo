---
title: Linux
date: 2019-04-16 16:55:56
tags:
---

## Setup user and sudo group

Sudo is not directly a group. The groups/users having sudoer rights are defined in a configuration file that you can access using sudo visudo. Check out this file to find out how it is configured on your system. Here is a good introduction https://www.garron.me/en/linux/visudo-command-sudoers-file-sudo-default-editor.html.

In your case, you have different ways to give sudo rights to chauncey.

find the group(s) having sudo rights in the sudoers file and add chauncey to one of these groups. For example, say you have this line in sudoers:

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL 
then, add chauncey to admin with sudo usermod -a -G admin chauncey.

create a new sudo group (sudo groupadd sudo) and add this lines (sudo visudo). Then once again add chauncey to the group

# the 'sudo' group has all the sudo privileges
%sudo    ALL=(ALL:ALL) ALL 
set a special rule for this user in the sudoers file using the following (note that there is no %, which is used to denote a group):

chauncey    ALL=(ALL:ALL) ALL 
Note that for all the rules I mentioned, I used the default ALL everywhere. The first one is the user(s) allowed, the second one is the host, the third one is the user as you are running the command and the last one is the commands allowed. You can tune your rules if ALL is too broad for your usecase.

To list all local users you can use:

cut -d: -f1 /etc/passwd
To list all users capable of authenticating (in some way), including non-local, see this reply: https://askubuntu.com/a/414561/571941

Some more useful user-management commands (also limited to local users):

To add a new user you can use:

sudo adduser new_username
or:

sudo useradd new_username
See also: What is the difference between adduser and useradd?

To remove/delete a user, first you can use:

sudo userdel username
Then you may want to delete the home directory for the deleted user account :

sudo rm -r /home/username
(Please use with caution the above command!)

To modify the username of a user:

usermod -l new_username old_username
To change the password for a user:

sudo passwd username
To change the shell for a user:

sudo chsh username
To change the details for a user (for example real name):

sudo chfn username
And, of course, see also: man adduser, man useradd, man userdel... and so on.

To add a user to the sudo group:

usermod -aG sudo username