vmware_tools
============

Ansible role which helps to install VMware Tools on RHEL-based guest
systems.


Usage
-----

```
# Default usage of the role
- name: My play
  hosts: all
  roles:
    - vmware_tools
```


Role variables
--------------

```
# Version of the YUM repo (see http://packages.vmware.com/tools/releases/)
vmware_tools_yumrepo_release: latest

# YUM repo URL
vmware_tools_yumrepo_url: http://packages.vmware.com/tools/releases/{{ vmware_tools_yumrepo_release }}/rhel{{ ansible_distribution_major_version }}/$basearch

# Install tools with no XWindows support?
vmware_tools_nox: yes

# RPM packages to be installed (you can force a specific version here)
vmware_tools_pkgs__default:
  - vmware-tools-esx{{ "-nox" if vmware_tools_nox else '' }}
  - vmware-tools-esx-kmods

# Additional RPM packages to be install (e.g. vmware-tools-vmxnet3-common)
vmware_tools_pkgs__custom: []

# Final list of RPM packages
vmware_tools_pkgs: "{{
  vmware_tools_pkgs__default +
  vmware_tools_pkgs__custom }}"

# Runlevels on which the service should be active (for upstart)
vmware_tools_runlevels: 235

# Start and stop sequence number for upstart
vmware_tools_init_start: 03
vmware_tools_init_stop: 99
```


License
-------

MIT


Author
------

Jiri Tyr
