## Configuration Management Task -
Notes:

1. Prepare the environment (install python, docker, molecile, etc)  
2. Create a Python environment  ```#python3 -m venv .venv```
3. Activate Python virtual environment ```source ansible-venv/bin/activate```
4. Install molecule, dependencies from requirements.txt ```python3 -m pip install -r requirements.txt```
5. Create and cofigure `playbook.yml` file.
6. tree:
``` 
r$ tree
.
├── files
│   └── nice-script.sh
├── molecule
│   └── default
│       ├── converge.yml
│       └── molecule.yml
├── playbook.yml
├── README.md
└── requirements.txt
```
7. Runung and testing:  
   - molecule create (It will use Ansible to launch a Docker container based on the molecule.yml)  
```
$ molecule login
root@instance:/# lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04.4 LTS
Release:	22.04
Codename:	jammy
```
8.  - molecule converge (playbook file that contains the call for your role.)  
```
$ molecule converge

PLAY [Playbook] ****************************************************************

TASK [Gathering Facts] *********************************************************
ok: [instance]

TASK [Ensure /better-place directory exists] ***********************************
changed: [instance]

TASK [Create nice-script.sh locally] *******************************************
changed: [instance]

TASK [Copy nice-script.sh to remote machine] ***********************************
changed: [instance]

TASK [Create new user] *********************************************************
changed: [instance]

TASK [Allow user to run whoami with sudo without password] *********************
changed: [instance]

TASK [Update package cache] ****************************************************
changed: [instance]

TASK [Install apt-file] ********************************************************
changed: [instance]

TASK [Update apt-file cache] ***************************************************
changed: [instance]

TASK [Install required packages] ***********************************************
changed: [instance] => (item=tmux)
changed: [instance] => (item=vim)
changed: [instance] => (item=unzip)
changed: [instance] => (item=wget)

TASK [Download Terraform binary] ***********************************************
changed: [instance]

TASK [Unzip Terraform binary] **************************************************
changed: [instance]

PLAY RECAP *********************************************************************
instance                   : ok=12   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```
```
root@instance:/# terraform --version
Terraform v0.15.5
on linux_amd64
```
9.  - molecule verify  
10. - molecule destroy (destroy the environment).   

  Use molecule login to login into conteiner  env.
