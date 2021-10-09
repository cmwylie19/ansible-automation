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