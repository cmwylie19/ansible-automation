# Ansible Practice

## Setup Ansible on localhost with key
```
  ansible-practice ssh-keygen -t rsa -C "cmwylie19@localhost"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/---/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/---/.ssh/id_rsa.
Your public key has been saved in /Users/---/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256: --- ---@localhost

➜  ansible-practice ssh ---@localhost
Password:
Last login: Thu Oct  7 17:20:08 2021
➜  ~ exit
Connection to localhost closed.
➜  ansible-practice ssh-copy-id ---@localhost
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
Password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh '---@localhost'"
and check to make sure that only the key(s) you wanted were added.

➜  ansible-practice ansible all -m ping            
[WARNING]: Platform darwin on host localhost is using the discovered Python interpreter at /usr/bin/python, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.11/reference_appendices/interpreter_discovery.html for more information.
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

## Using filters with facts
```
ansible localhost -m setup -a "filter=ansible_all_ipv4_addresses"
[WARNING]: Platform darwin on host localhost is using the discovered Python interpreter at /usr/bin/python, but future installation of
another Python interpreter could change the meaning of that path. See https://docs.ansible.com/ansible-
core/2.11/reference_appendices/interpreter_discovery.html for more information.
localhost | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "---"
        ],
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false
}
```

## Add Public Key to vagrant
```
ssh-copy-id -i ~/.ssh/id_rsa.pub -p 2222 vagrant@localhost
```

## Connect to vagrant
```
ssh -p '2222' 'vagrant@localhost'
```


### Resources
- https://faun.pub/automation-deploying-an-app-in-gke-using-ansible-4b6687967ac3


### Init Roles Directory
```
ansible-galaxy init roles/app-tier
```

### Encrypt with ANsible Vault
```
# Encrypt 
ansible-cault encrypt secret.yaml

ansible-vault create --vault-password-file=vault-pass secret.yml

ansible-vault view secret1.yml

ansible-vault edit secret.yml

# Change password
ansible-vault rekey secret.yml

ansible-vault decrypt secret1.yml --output=secret1-decrypted.yml

ansible-playbook --ask-vault-pass site.yml

ansible-playbook --vault-password-file=vault-pass site.yml

```