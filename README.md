ansible-role-atomic-red-team
=========

[![GitHub license](https://img.shields.io/github/license/j91321/ansible-role-atomic-red-team?style=flat-square)](https://github.com/j91321/ansible-role-atomic-red-team/blob/main/LICENSE)
[![GitHub last commit](https://img.shields.io/github/last-commit/j91321/ansible-role-atomic-red-team.svg?style=flat-square)](https://github.com/j91321/ansible-role-atomic-red-team/commit/main)
[![Build role](https://github.com/j91321/ansible-role-atomic-red-team/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/j91321/ansible-role-atomic-red-team/actions/workflows/build.yml)
[![Twitter](https://img.shields.io/twitter/follow/j91321.svg?style=social&label=Follow)](https://twitter.com/j91321)


An Ansible role that installs Atomic Red Team (both execution framework and tests).

Supported platforms:

- Windows 10
- Windows Server 2019
- Windows Server 2016

Requirements
------------

None

Role Variables
--------------

Ansible variables from defaults/main.yml
```
atomic_execution_framework_install_path: "C:\\AtomicRedTeam"
atomics_install_path: "C:\\AtomicRedTeam"
atomics_repo_owner: "redcanaryco"
atomics_repo_branch: "master"
atomics_defender_exclusion: true
powershell_profile_install: true
powershell_profile: "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\Microsoft.PowerShell_profile.ps1"
```

Setting `atomic_execution_framework_install_path` will install the execution framework in directory `invoke-atomicredteam` in the specified path. In default case the execution framework will be installed to `C:\AtomicRedTeam\invoke-atomicredteam`

Setting `atomics_install_path` will install Atomic Red Team tests (Atomics) in directory `atomics` in the specified path. In default case atomics will be installed to `C:\AtomicRedTeam\atomics`

If you contribute to Atomic Red Team or have your own fork of the project you may wish to change the `atomics_repo_owner` and `atomics_repo_branch` variables. These specify the Github user and branch from where the atomics will be downloaded.

If `atomics_defender_exclusion` is set to **true** exclusion for the atomics folder will be added to Microsoft Defender. This is necessary since some payloads from the tests will be flagged as malware. If you use different AV you must specify exclusions there before running the playbook.

If `powershell_profile_install` is set to **true** the role will add settings into `powershell_profile` that will auto import `Invoke-AtomicTest` and set the atomics folder location for execution framework.

By default the `powershell_profile` is set to `C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1` which is the Powershell profile for All Users on current host. You may wish to change it to something like `$Home\[My ]Documents\PowerShell\
Microsoft.PowerShell_profile.ps1` if you wish to auto load execution framework only for specific user.

Tags
----

You can use tag `force` to add `-Force` switch to both `Install-AtomicRedTeam` and `Install-AtomicsFolder`. This is usefull for contributors that may want to fetch the latest atomics from repository.

Dependencies
------------

None.

Example Playbook
----------------

```
- name: Install Atomic Red Team
  hosts:
    - vm_test
  vars:
    atomic_execution_framework_install_path: "C:\\tools"
    atomics_install_path: "c:\\tests"
    atomics_defender_exclusion: true
    powershell_profile_install: true
    powershell_profile: "C:\\Users\\IEUser\\Documents\\WindowsPowerShell\\Microsoft.PowerShell_profile.ps1"
  roles:
    - ansible-role-atomic-red-team
```

License
-------

MIT

Author Information
------------------

j91321
