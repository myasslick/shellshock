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
