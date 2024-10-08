
# Ansible Role: Backup Repo
Create a full backup of a remote repo with all it's branches and commit history.

## Requirements
 - Ansible >= 2.15
 - Run with ```become: true``` for a role or the entire playbook

## Variables
Next vars are supported in role::
```yml
# Username or a token's name
username: "dev"

# Token with the permission to read from repo
token: "token"

# Repository name in format "hub/repo" (without https)
repo: "gitlab.org.com/project/back"

# Path to directory where role will be running
workdir: "/tmp/workdir"

# Path to directory where backup will be stored
backup: "/tmp/backup"

# Check ssl during connection (disable if you are using self-signed cert on a server)
ssl: "true"
```

## How to Use
Just include role in a playbook and provide your vars:
```yml
- hosts: localhost
  become: true
  
  vars_files:
    - /vars/vault.yml
  
  roles:
    - role: devkyt.backup-repo
```

Or run in a loop for several repos:
```yml
- hosts: localhost
  become: true
  
  vars_files:
    - /vars/vault.yml
  
  tasks:
    - name: Backup repos
      include_role: 
        name: ./ansible-role-backup-repo
      vars:
        repo: "{{ item }}"
      loop:
        - gitlab.org.com/project/back
        - gitlab.org.com/project/front
        - gitlab.org.com/project/email
```

## Author
Created by Kyrylo Tykhanskyi in the foggy October 2024. 