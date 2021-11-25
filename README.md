# EPAM LEARN Ansible

### Create users Alice, Bob, Carol with password 's0mEp@$$':

`ansible-playbook -i inventory --vault-password-file=.vault_passwd users.yml`
