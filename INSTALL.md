These are temporary install instructions for newnode_desktop for Linux.   Eventually some version 
of this will be in the snap store; these instructions are for use in testing newnode_desktop before
that happens.  So instead of doing `snap install newnode_desktop` or whatever, you will build the
snap from the `snapcraft.yaml` file.  

At some later date when the snap is published it will be necessary to re-install newnode_desktop 
from the published snap.   After that, further updates to the newnode_desktop app should happen automatically.

This _should_ build newnode_desktop, and run it, on any recent version of any major Linux distribution.

You do need a fair amount of disk space available because `snapcraft` is going to build the newnode_desktop
app within a VM that it creates for the purpose.


1. Install the `snap` program and other necessary tools

Instructions for how to do this on many versions of Linux are at https://snapcraft.io/docs/installing-snapd
(On some distibutions, notably Ubuntu-derived distributions, `snap` is installed by default)

At least for now, you do not need to install the `snap-store` app.

2. Install the `snapcraft` program (which is used to build a snap from a `snapcraft.yaml` file)

```bash
sudo snap install snapcraft --classic
```

Note: normally snaps run in a sandbox which protects your system from harm done by the snap.  However, the 
`snapcraft` snap actually needs to be able to run outside of the sandbox.

3. If you haven't done so already, clone the newnode_desktop repo.   (which is mostly just the `snapcraft.yaml` file)

```bash
git clone https://github.com/clostra/newnode_desktop
```

4. Build the snap.   This will create a file system, launch a VM using that file system.  
Inside that VM it will download the newnode (vpn/kit) repo and any necessary dependencies, and build the newnode `client` app.

```bash
cd newnode_desktop
snapcraft
```

If snapcraft asks you if you'd like to install `multipass`, say yes.

(the build does take several minutes)

5.  Install the snap

```bash
sudo snap install newnode-vpn-desktop*.snap --dangerous --devmode
```

(note: once the snap is installed, snapd should restart the snap automatically after reboots)

6. Test to make sure the snap has started

```bash
netstat -an | grep :8006
```

which should produce something like

```
tcp        0      0 127.0.0.1:8006          0.0.0.0:*               LISTEN     
```

7. Test newnode desktop for function

```bash
https_proxy=http://localhost:8006 wget https://cnn.com
```

8. How to look at newnode log messages

The current newnode_desktop snap runs in verbose mode and all of its output messages are copied by `snapd` to syslog.
Look wherever your Linux distribution puts log files, e.g.

```bash
ls -lrt /var/log
```

on Ubuntu.   As this snap is curently set up, newnode will spew logs of log messages.   Sorry.
