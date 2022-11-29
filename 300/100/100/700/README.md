# 700 - Linux

We will follow this tutorial ("[Installing Home Assistant Supervised directly on Debian 11](https://www.youtube.com/watch?v=ivBPS5-zi04)") to install Home Assistent on a Debian GNU Linux 11.3 virtual machine that has been created from Parallels on a Mac Mini

*Note*: If when trying to connect to the Debian VM from outside the VM with SSH, you get a "connection refused", make sure to follow the advice at https://linuxhint.com/fix_connection_refused_ubuntu/ We fixed it by just installing and starting OpenSSL as explained in the link.

*Note*: If when trying to change to the root user with "su" and entering the password (of the first user that was created in Debian VM) you get a "su: Authentication failure", use "sudo su" instead with the password.

*Note*: Regarding the applications to be installed read the documentation as the video has some old/out-of-date mentionings; see https://github.com/home-assistant/supervised

