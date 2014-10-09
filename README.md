Role Name
=========

Shellshock vulnerability checker and remediation.

Role Variables
--------------

There are three variables defined.

* ``SHELLSHOCK_PATH`` is the full path of the shellshock test script placement,
which defaults to ``/tmp/shellshock``.

* ``WHEN_CLAUSE`` is a comparison condition that determines whether
a host is vulnerable to ShellShock or not.

* ``FAILED_CLAUSE`` is a comaprison condition that determins whether a host is **still**
vulnerable to ShellShock or not.

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

Here is a demo on an **affected** host:

```

PLAY [all] ********************************************************************

TASK: [shellshock | Upload shellshock test script] ****************************
changed: [192.168.33.10]

TASK: [shellshock | Test if host is vulnerable to shellshock] *****************
changed: [192.168.33.10]

TASK: [shellshock | Update bash if we are vulnerable to shellshock] ***********
changed: [192.168.33.10]

TASK: [shellshock | Test if host is still vulnerable to shellshock after update] ***
changed: [192.168.33.10]

TASK: [shellshock | Remove shellshock script] *********************************
ok: [192.168.33.10]

PLAY RECAP ********************************************************************
192.168.33.10              : ok=5    changed=4    unreachable=0    failed=0
```

Here is a demo on an **unaffected** host:

```
PLAY [all] ********************************************************************

TASK: [shellshock | Upload shellshock test script] ****************************
ok: [192.168.33.10]

TASK: [shellshock | Test if host is vulnerable to shellshock] *****************
ok: [192.168.33.10]

TASK: [shellshock | Update bash if we are vulnerable to shellshock] ***********
skipping: [192.168.33.10]

TASK: [shellshock | Test if host is still vulnerable to shellshock after update] ***
skipping: [192.168.33.10]

TASK: [shellshock | Remove shellshock script] *********************************
ok: [192.168.33.10]

PLAY RECAP ********************************************************************
192.168.33.10              : ok=3    changed=0    unreachable=0    failed=0
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
