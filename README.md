Ansible deploy apache mysql php on ubuntu
====================================

This play book performs following on a ubuntu host:

- Deploys php with apc, gd, mbstring and pdo extensions with modifiable php.ini as template and from variables in group_vars/webserver.yml. 
- Installs apache and configures virtual host customizable via template in apache role. Enables ssl and rewrite modules for apache. Creates web root directory and sets permissions. Copies source code from given zip file to apache web root.
- Deploys mysql. Creates mysql user. Dumps sql file in created database.
- Sets up and ftp user to access apache web root.
- Copies mysql backup script to db host. Creates a full backup and schedules hourly incremental backups and daily full backups which can either be saved on host or on a remote host.

How to run:

- Install ansible on your local ubuntu (virtual)machine
- Clone this repository in a folder.
- Modify `hosts` file and put ips for webserver and dbserver (They both may be same)
- Edit group_vars/dbserver.yml and group_vars/webserver.yml and put variable values according to your needs.
- Execute `ansible-playbook -i hosts -k -u root deployment.yml`
- Ansible will ask for password, give it password for host, sit back enjoy your coffee while ansible does the magic.
- Once done, open http://{{ your_host_name }} if you see phpinfo page, everything is working.