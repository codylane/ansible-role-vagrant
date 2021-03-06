Role Name
=========

This role will handle setting up vagrant base boxes, configuring users,
setting security contexts depending on how you choose to use this role.

Features
--------
* This role can handle installing vagrant on your workstation if it is
  Debian, RedHat, OSX.

* This role can configure selinux on RedHat based machines.

* This role will setup the vagrant user, ssh password, and ssh keys

* This role will configure the vagrant user's sudoer's perms.

* This role will configure the root password, root ssh key for vagrant.

* This role will download and install guest additions for virtualbox
  guests


Supported Distributions
-----------------------

Currenlty this role supports the following guest disributions:

RedHat -> Installing vagrant, setting up RedHat base boxes

Debian -> Installing vagrant, setting up Debian base boxes

This role can install vagrant on a RedHat, Debian or OSX workstation

Requirements
------------

The examples directory contains information on how to use the `vagrant`
role.

Also, it is assumed that the `root` user is configured and that you can
login as root to the machine you want to turn into a vagrant base box.

After the vagrant base box has been configured, the root user and the
vagrant user will have a default password of `vagrant`.  You can
override this if you'd like as well either using group_vars, encrypted
vault password etc.  You'll need to set this up on your own if you'd
like added security.

## First time run on a base box

You need to specify the location to you public key that you want to give
to your vagrant box.  This example below will copy the contents of
id_da.pub into the environment and be used during the ansible-playbook
run.
```
export VAGRANT_USER_PUB_KEY=$(cat ~/.ssh/id_dsa.pub)
```

This also assumes that you have a base OS installed and it is in the
running state and that you also know the ip address of the that OS.
You'll need the ip address so that you can update your inventory file.

If the base box that you are configuring doesn't have ssh keys
configured, you'll need to use the `-k` switch for ansible-playbook. You
should only have to to this once.  (See examples directory).  

Here is an example of how to configure a new ubuntu1404 base box, which
will prompt you for the root user's password and only run on the hosts
in your inventory that match ubuntu1404
```
cd examples
./setup_base_box -k -e 'hosts=ubuntu1404'
```

Role Variables
--------------

This role makes use of multiple tasks that are included conditionaly
when certian varaibles are set.  You can also specify which tasks you
want to run on the command line by specifying `-t tag1,tag2`.

(See the examples directory) for quick examples on how to pass
variables to the role to change the playbook run.


Dependencies
------------

sshpass needs to be installed

Example Playbook
----------------
## How to install vagrant on your workstation if no sudo password
```
cd exapmles
./setup_workstation
```
## How to install vagrant on your workstation if sudo password
```
cd exapmles
./setup_workstation -K
```

## How to create a base box
```
cd examples
./setup_base_box
```

(See examples directory for playbook execution)

License
-------

BSD

Author Information
------------------
Cody Lane

NOTE: I want to make this better for everyone and I hope that folks find
this role useful.  If you find a bug, please submit a pull request and
I'll take a look and merge it as ASAP.  If you'd like additional
features, please also feel free to comment and I'll priortize these
features.
