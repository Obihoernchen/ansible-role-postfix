postfix
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-postfix.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-postfix)

Provides Postfix for your system.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/postfix.png "Dependency")

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------


- postfix_myhostname: The hostname.
- postfix_mydomain: The domain.
- postfix_myorigin: Maybe the domain.
- postfix_inet_inferfaces: A list of interfaces to listen on.
- postfix_mydestination: What domain to consider as the destination.
- postfix_mynetworks: A list of networks to relay mail for.
- postfix_relay_domains: Domains to relay.
- postfix_relayhost: Where to send mails to as a relay hop.
- postfix_smtpd_recipient_restrictions: A list of restrictions.
- postfix_spamassassin: enable spamassassin or not
- postfix_spamassassin_user: what user for spamassassin
- postfix_clamav: enable clamav or not.

Dependencies
------------

You can use this role to prepare your system.

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)

Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-latest|yes|yes|yes|
|alpine-edge|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|yes|yes|yes|
|opensuse-tumbleweed|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

Example Playbook
----------------

Basic configuration, using all defaults (See defaults/main.yml).
```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
```

To configure postfix to relay all its email to a relayhost:
```
- hosts: servers

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_relayhost: "[relay.example.com]"
```


To configure postfix to receive all mail for example.com:
```
- hosts: mailserver

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_mydestination: "example.com, $mydomain, $myhostname, localhost.$mydomain, localhost"
```

To configure postfix to use spamassassin and clamav:
```
- hosts: mailserver

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.postfix
      postfix_mydestination: "example.com, $mydomain, $myhostname, localhost.$mydomain, localhost"
      postfix_spamassassin: enabled
      postfix_clamav: enabled
```

Install this role using `galaxy install robertdebock.postfix`.

License
-------

Apache License, Version 2.0

Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
