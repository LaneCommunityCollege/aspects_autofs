# aspects_autofs

A role to manage autofs mounts.

# Requirements

Set ```hash_behaviour=merge``` in your ansible.cfg file.

For NFS mounts, install `nfs-utils` on RedHat family systems and `nfs-common` on Debian family systems.

## Role Variables

### aspects_autofs_enabled
Default is ```False```. Set to ```True``` to actually run the role.

### aspects_autofs_mounts
A dictionary of mounts.

#### aspects_autofs_mounts.masterline
The configuration for the mount that goes in ```/etc/auto.master```.

#### aspects_autofs_mounts.miscline
The configuration for the mount that goes in ```/etc/auto.misc```.

### aspects_autofs_master_line_default_enabled
Use the ```aspects_autofs_master_line_default``` value in ```/etc/auto.master``` or not.

### aspects_autofs_master_line_default
A default line to place in the ```/etc/auto.master``` configuration file. Defaults to: ```/- /etc/auto.misc --timeout 60```

## Dependencies
### aspects_packages
[aspects_packages](https://github.com/LaneCommunityCollege/aspects_packages) is used to manage system packages.

## Example Playbook

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

## Notes

On CentOS 7, if you are using NFS home mounts, you may need to modify SELinux settings. Specificially, run:

```
setsebool -P use_nfs_home_dirs 1
```

I discovered this when ssh was returning a public key error when I tried to ssh in using ssh keys.

## License

MIT
