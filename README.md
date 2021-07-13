# EPAM LEARN Ansible

### Create users Alice, Bob, Carol with password 's0mEp@$$':

`ansible-playbook -i inventory --vault-password-file=.vault_passwd users.yml`

### Install Apache:

`ansible-playbook -i inventory --tags apache-install web.yml`

### Uninstall Apache:

`ansible-playbook -i inventory --tags apache-uninstall web.yml`

### Install FTP:

`ansible-playbook -i inventory ftp.yml`
