Role Name
=========

Shellshock vulnerability checker and remediation for Ubuntu-based servers.

If the remote host is using an end-of-life Ubuntu release (e.g. 13.10)
then this playbook will edit the host's ``/etc/apt/sources.list``
to use the next nearest LTS to get the latest bash update (and revert
the file change at the end).

Role Variables
--------------

There are several role variables defined in ``vars/main.yml``, but
the main one is ``SHELL_SHOCK_PATH`` which is the full path
of the shellshock test script placement on the remote host. By
default this is set to ``/tmp/shellshock``.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - shellshock

or

    - hosts: servers
      roles:
        - { role: shellshock, SHELL_SHOCK_PATH: /custom/path/shellshock.sh }


Demo
----

```
PLAY [all] ********************************************************************

GATHERING FACTS ***************************************************************
ok: [127.0.0.1]
ok: [127.0.0.3]
ok: [127.0.0.2]

TASK: [shellshock | Upload shellshock test script] ****************************
ok: [127.0.0.3]
ok: [127.0.0.1]
changed: [127.0.0.2]

TASK: [shellshock | Test if host is vulnerable to shellshock] *****************
ok: [127.0.0.3]
ok: [127.0.0.1]
changed: [127.0.0.2]

TASK: [shellshock | Switch EOL versions to use the next LTS version in /etc/apt/sources.list] ***
skipping: [127.0.0.3]
skipping: [127.0.0.1]
changed: [127.0.0.2]

TASK: [shellshock | Update bash if we are vulnerable to shellshock] ***********
skipping: [127.0.0.3]
skipping: [127.0.0.1]
changed: [127.0.0.2]

TASK: [shellshock | Test if host is still vulnerable to shellshock after update] ***
skipping: [127.0.0.3]
skipping: [127.0.0.1]
changed: [127.0.0.2]

TASK: [shellshock | Remove shellshock script] *********************************
ok: [127.0.0.2]
ok: [127.0.0.3]
ok: [127.0.0.1]

TASK: [shellshock | Revert /etc/apt/sources.list back to use EOL version] *****
skipping: [127.0.0.1]
skipping: [127.0.0.3]
changed: [127.0.0.2]

PLAY RECAP ********************************************************************
127.0.0.2                 : ok=8    changed=6    unreachable=0    failed=0
127.0.0.3                  : ok=4    changed=0    unreachable=0    failed=0
127.0.0.1                  : ok=4    changed=0    unreachable=0    failed=0

Testing
-------

I recommend using vagrant to test this role's effectiveness. Assuming you have
a directory to host your Vagrantfile:

```
vagrant init hashicorp/precise32
vagrant up
```

Then, your entry-point might be:

```
---

- hosts: all
  gather_facts: yes
  roles:
    - shellshock
```

and your testing inventory file might be:

```
192.168.33.10 ansible_ssh_private_key_file=~/.vagrant.d/insecure_private_key ansible_ssh_user=vagrant
```

Acknowledgement
---------------

The ``shellshock.sh`` is available on
[hannob/bashcheck](https://github.com/hannob/bashcheck).

License
-------

Apache (this repository)

Universal (hannaob/bashcheck)

Author Information
------------------

Yeuk Hon Wong (yeukhon@acm.org)
