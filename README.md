###Ansible Playbook Deployment Process - Ec2


#####Step 1:
#####Prep your 'group_vars/all.yml' file with the appropriate variables.
#####Prep your 'ansible.cfg' file.

######NOTE: Just about everything in 'group_vars/all.yml' is custom, and will need modified.
######        The only thing that really needs modified in 'ansible.cfg' is 'remote_user'

```bash
  vi group_vars/all.yml

  vi ansible.cfg

    - remote_user = ubuntu
```
#####Step 2:
#####Add your Ansible .pub key to your 'provision.yml' file.

```
user_data: |
            #!/bin/bash
            echo "sl35slkd67#%skd... your-key" >> "/home/ubuntu/.ssh/authorized_keys"
```
#####Step 3:
#####Provision Ec2 Instances

######NOTE: This will create an ec2 keypair if it doesnt already exist and save it in the 'keys' 
        directory. So make sure you save this. Also, it will add your 'ansible.pub' key you
        specified in 'provision.yml' to the authorized_keys section, and create an inventory
        file for you in 'inventory/{{ env }}'

```
  $ ansible-playbook provision.yml
```
#####Step 4:
#####Deploy your playbook / application
```
  $ ansible-playbook -i inventory/{{ env }} deploy.cfg
```

