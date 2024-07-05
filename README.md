# Ansible-Project-2

=====================================================

# cd /etc/ansible/roles

# ansible-galaxy init projectAnsible

# ls

# cd projectAnsible

# rm -rf  tests meta README.md

# vim tasks/main.yml

press i

  - name: To execute a command
    command: hostname -s
    notify: Print command message
  - name: Install apache on webserver
    package: name={{pkg_name}} state={{pkg_state}}
  - name: Start apache Server
    service: name={{pkg_name}} state=started
  - name: Deploy html page on apache
    template: src=index.html.j2 dest=/var/www/html/index.html
    notify: Restart the apache2 server

Save the file

# vim handlers/main.yml

  - name: Restart the apache2 server
    service: name={{pkg_name}} state=restarted
  - name: Print command message
    debug: msg="command executed successfully"


Save the file

# vim vars/main.yml
pkg_name: apache2
pkg_state: present

save the file

# vim templates/index.html.j2

This file is for webapplication

It is deployed on server {{ansible_nodename}}

Ipaddress of the Host : {{ansible_default_ipv4["address"]}}

Host Node Name is : {{ansible_nodename}}

Host OS faily is : {{ansible_os_family}}



save the file

# cd ../..

You will be int he /etc/ansible directory now.

# vim playbookProject.yml


- name: execute roles
  hosts: webserver
  become: true
  roles:
   - projectAnsible



# ansible-playbook playbookProject.yml
