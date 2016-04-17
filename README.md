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

ssh_known_hosts_path: The destination file to write to.  The default is /etc/ssh/ssh_known_hosts and ~user/.ssh/known_hosts is a good alternative.

ssh_known_hosts_state: present or absent. the default is present

ssh_known_hosts_enctype: The public key encoding type to scan for. Choices are rsa, dsa, ecdsa or ed25519. Default is rsa.

ssh_known_hosts_port: The port to connect to when scanning the remote host. Default is 22.

ssh_known_hosts_keyscan: The program to use to scan with. The default is ssh-keyscan in the current path.

ssh_known_hosts: List of dictionaries the host and its attributes to scan:

```
ssh_known_hosts:
  - name: example.com
    state: present
    dest: /etc/ssh/ssh_known_hosts
    enctype: rsa
    port: 22
    keyscan: ssh-keyscan
    aliases:
      - www.example.com
      - www2.example.com
```

Dependencies
------------

None.

Example Playbook
----------------

---
```
- hosts: all
  vars:
    ssh_known_hosts:
      - name: example.com
        state: present
        dest: /etc/ssh/ssh_known_hosts
        enctype: rsa
        port: 22
        keyscan: ssh-keyscan
        aliases:
          - www.example.com
          - www2.example.com
  roles:
    - role: sshknownhosts
```


License
-------

BSD

Author Information
------------------

Byron F. Martin
Email: http://www.bfmartin.ca/contact
Github: bfmartin
