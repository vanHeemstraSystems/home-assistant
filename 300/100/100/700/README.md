# 700 - Linux

**TIP**: To uninstall a (previous) Home Assistant Supervised installation, use the uninstall script found at https://gist.github.com/stemsmit/944495cb659e3925d1ea72d457c28d8e

**TIP**: To be on the save side, (re-)install the below:

```
$ sudo apt reinstall systemd-journal-remote
$ sudo systemctl enable systemd-journal-gatewayd.socket
$ sudo systemctl start systemd-journal-gatewayd.socket
$ sudo systemctl is-enabled systemd-journal-gatewayd.socket
```

The outcome should be: ```enabled```.

We will follow this tutorial ("[Installing Home Assistant Supervised directly on Debian 11](https://www.youtube.com/watch?v=ivBPS5-zi04)") to install Home Assistent on a Debian GNU Linux 11.3 virtual machine that has been created from Parallels on a Mac Mini

*Note*: If when trying to connect to the Debian VM from outside the VM with SSH, you get a "connection refused", make sure to follow the advice at https://linuxhint.com/fix_connection_refused_ubuntu/ We fixed it by just installing and starting OpenSSL as explained in the link.

*Note*: If when trying to change to the root user with "su" and entering the password (of the first user that was created in Debian VM, when using Parallels that user is called "parallels" by default) you get a "su: Authentication failure", use "sudo su" instead with the password.

*Note*: Regarding the applications to be installed read the documentation as the video has some old/out-of-date mentionings; see https://github.com/home-assistant/supervised

**WARNING**: If during the installation of home assistant supervised you get the error ```homeassistant-supervised depends on systemd-resolved; however: Package systemd-resolved is not installed.``` follow this advise:

Debian 11 already has systemd-resolved. Install using:

```
$ sudo dpkg -i --ignore-depends=systemd-resolved ./homeassistant-supervised.deb
```

Once it installs, edit ```/var/lib/dpkg/status``` and remove ```system-resolved``` from homeassistant-supervised from ```Depends```.

## Portainer

Part of the installation includes Portainer.

Should Portainer have been installed previously, and the account ```admin``` is not accepting any passwords, you can reset the password following https://omar2cloud.github.io/rasp/psswd/ and/or https://docs.portainer.io/advanced/reset-admin

To avoid **Home Assistant** stating that you are working in an *unhealthy system* (most likely because we have Portainer running on the same Docker host) you can surpress this notion as follows:

```
$ ha jobs options --ignore-conditions healthy
```
