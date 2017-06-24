aspects_autofs
=========

A role to manage autofs mounts. Ubuntu only.

Requirements
------------

Set ```hash_behaviour=merge``` in your ansible.cfg file.

Role Variables
--------------
### aspects_autofs_enabled
Default is ```False```. Set to ```True``` to actually run the role.

### aspects_autofs_packages
A dictionary of the packages that need to be installed for autofs to work.

### aspects_autofs_mounts
A dictionary of mounts.

Example Playbook
----------------

```yaml
    - hosts: servers
      vars:
        aspects_autofs_mounts:
            userhome:
                masterline: "/home /etc/auto.misc --timeout 60"
                miscline: "user -hard,intr,tcp,actimeo=3 nfsserver:/homedata/user"
      roles:
         - { role: aspects_autofs }
```

License
-------

MIT
