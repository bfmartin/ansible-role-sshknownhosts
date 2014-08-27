sshknownhostsrole
=================

This is an ansible role that manages the SSH known hosts file usually located at /etc/ssh/ssh_known_hosts or ~user/.ssh/known_hosts.

The main purpose of this role is to wrap the sshknownhosts module located at https://github.com/bfmartin/ansible-sshknownhosts and make it suitable for Ansible Galaxy.

Requirements
------------

Any Unix-like system with an openssh server should work.

Security
--------

If an ssh_known_hosts file is constructed using ssh-keyscan without
verifying the keys, users will be vulnerable to man in the middle
attacks.  On the other hand, if the security model allows such a risk,
ssh-keyscan can help in the detection of tampered keyfiles or man in
the middle attacks which have begun after the ssh_known_hosts file was
created.

(taken from the ssh-keyscan man page)


Role Variables
--------------

This role uses the following variables. and their default values:

host: The remote host to scan. An alias for "host" is "name". This parameter is required. If used with state=present, the host is added or updated with the current key. If used with state=absent, the line containing this hostname is removed.

dest: The destination file to write to.  The default is /etc/ssh/ssh_known_hosts and ~user/.ssh/known_hosts is a good alternative.

state: present or absent. the default is present

enctype: The public key encoding type to scan for. Choices are rsa, dsa or ecdsa. Default is rsa.
port: The port to connect to when scanning the remote host. Default is 22.

keyscan: The program to use to scan with. The default is ssh-keyscan in the current path.

aliases: Aliases for the host name to add to the known hosts file. The default is "".


Dependencies
------------

None.

Example Playbook
-------------------------

---
- hosts: all
  roles:
    - { role: ssh_known_hosts, host: server1.mydomain.net, aliases: "gitserver" }





License
-------

BSD

Author Information
------------------

Byron F. Martin
Email: http://www.bfmartin.ca/contact
Github: bfmartin
