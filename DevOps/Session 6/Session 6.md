#installing_package
## Debian Package Tool (dpkg)
- dpkg is a low-level tool for managing packages in the Debian family.
- In the terms of equivalence, dpkg in the Debian families the same as rpm in Red Hat family.
- dpkg cannot be connected to repo and is only used to install or delete through the source.
- The source file of Debian family packages is identified by the extension \*.deb.
- The dpkg data base is located in /var/lib/dpkg.

|                               |     Debian     |   Red Hat   |
| :---------------------------: | :------------: | :---------: |
| High-Level<br>Package Manager | apt_get<br>apt | yum<br>dnf  |
| Low-Level<br>Package Manager  |  dpkg<br>.deb  | rpm<br>.rpm |
>[!tip] to download a file use ```wget URL```


| Command dpkg ... | Work                                               |
| ---------------- | -------------------------------------------------- |
| -l               | For listing all files installed by the package     |
| -s               | For getting status of installed and not installed  |
| -P               | for uninstalling completely of package from system |
| -i               | For installing a package                           |

## Advanced packaging Tool (APT)
- APT tools like YUM are one of the package management tools in Debian family.
- APT manages packages through repos introduced in /etc/apt/sources.list
- The .deb files downloaded from APT will be saved in /var/cache/apt/archives/
- The meta data caches of APT update command will be saved in /car/lib/apt/lists/

| Command apt ...                 | work                           |
| ------------------------------- | ------------------------------ |
| update                          | Update the repository          |
| upgrade                         | Upgrade the installed packages |
| dist-upgrade                    | Upgrade the version of OS      |
| full-upgrade                    | Upgrade all things             |
| remove package                  | Remove the package             |
| purge                           | Remove the package compeletly  |
| list --installed                | List of the installed apps     |
| do-release-upugrade             | Upgrade the version of the ltc |
| install package --download-only | ---                            |
## Manage Groups in Linux

| # Command                                                | Work             |
| -------------------------------------------------------- | ---------------- |
| groupadd -g \[Group Id\] \[Group Name\]                  | Creating a group |
| groupdel \[Group Name\]                                  | Delete a group   |
| groupmod -g \[GID\] -n \[New Group Name\] \[Group Name\] | Modify a group   |

---

| File         | Content                     |
| ------------ | --------------------------- |
| /etc/group   | List of all groups          |
| /etc/passwd  | List of all users           |
| /etc/shadow  | List of all users password  |
| /etc/gshadow | List of all groups password |

## User Account Management in Linux

| # Command                           | work                                 |
| ----------------------------------- | ------------------------------------ |
| useradd -m                          | Give the user home                   |
| useradd -g Group                    | Primary Group                        |
| useradd -c "Artin Nemati"           | Comment                              |
| useradd -s Bash                     | Bash (/bin/bash)                     |
| useradd -u                          | UID                                  |
| useradd -p                          | Password                             |
| userdel                             | Delete the user                      |
| usermod -g 4000 -c "Mew"            | Modify the user                      |
| usermod -G DevOps,Cloud,Infra Artin | Rewrite the user to secondary groups |
| usermod -a                          | Append                               |
| usermod -aG ...                     | Append the Groups to previous groups |
| chage -l artin                      | Change age                           |
| chage -m                            | Change the Minimum Day password      |
| chage -M                            | Change the Maximum Day pasword       |
| chage -d                            | Expire time for Password             |

## Linux Permission Levels

![[Permissions.png]]


| Permission | Mnemonic |         File Permission          |        Directory Permission         |
| :--------: | :------: | :------------------------------: | :---------------------------------: |
|    Read    |    r     | Reading the contents of the file |       List directory contents       |
|   Write    |    w     |     Write or change the file     | create or remove files in directory |
|  Execute   |    x     |    Run the file as a program     |   Access (cd into) the directory    |

## Linux Permission Classes
- In Linux permission levels are classified into three permission classes:
1. User class specifies the file owner access level.
2. Group class specifies the group owner access level.
3. Others class specifies the access level of the other users.

>[!tip] Change the permission levels with chmod :
>$chmod \[ugoa] \[+ -] \[r w x] File or Directory Name

---

![[Permissions 2.png]]

---


![[Permissions Bianary.png]]

---
## Change User/Group Ownership


| Command                      | Work                              |
| ---------------------------- | --------------------------------- |
| chown artin:DevOps test file | change the owner ship of the file |
| chgrp                        | Change Group                      |
| chown -R                     | Recesive                          |
| chown -v                     | Verbose                           |

---

## Umask
- Default Permission for file : 666 - umask
- Default Permission for directory : 777 - umask

>[!warning] $umask : 0***002*** The highlighted numbers for the basic permission.

|               |   U   |   G   |   O   |        |      |
| :-----------: | :---: | :---: | :---: | :----: | :--: |
|     SUID      | rw*s* |  rwx  |  rwx  | 2 ** 2 | 4777 |
|     SGID      |  rwx  | rw*s* |  rwx  | 2 ** 1 | 2777 |
| Sticky<br>Bit |  rwx  |  rwx  | rw*t* | 2 ** 0 | 1777 |
|    Default    |   -   |   -   |   -   |   -    | 0777 |

## What is SUID?
- When the SUID bit is set on an executable file this means that the file will be executed with the same permissions as the owner of the executable file.
>[!warning] -rw*s* r-x r-x

- This mean that any user running the passwd command will be running it with the same permission as root.