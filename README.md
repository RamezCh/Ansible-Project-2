# Ansible-Project-2

=====================================================

cd /etc/ansible/roles

ansible-galaxy init projectAnsible

cd projectAnsible

rm -rf tests meta README.md

vim tasks/main.yml

=====================================================

'#' Tasks file for projectAnsible

- name: Display the hostname
  command: hostname -s
  notify: Print command message

- name: Install Apache on webserver
  package: 
    name: "{{ pkg_name }}"
    state: "{{ pkg_state }}"

- name: Start Apache server
  service: 
    name: "{{ pkg_name }}"
    state: started

- name: Deploy HTML page on Apache
  template: 
    src: index.html.j2
    dest: /var/www/html/index.html
  notify: Restart the Apache server


Save the file

=====================================================

vim handlers/main.yml

'#' handlers file for projectAnsible

- name: Restart the Apache server
  service: 
    name: "{{ pkg_name }}"
    state: restarted

- name: Print command message
  debug: 
    msg: "Command executed successfully"


Save the file

=====================================================

'#' vim vars/main.yml

pkg_name: apache2
pkg_state: present


save the file

=====================================================

'#' vim templates/index.html.j2

This file is for web application.

It is deployed on server {{ ansible_nodename }}.

IP address of the Host: {{ ansible_default_ipv4.address }}.

Host Node Name: {{ ansible_nodename }}.

Host OS Family: {{ ansible_os_family }}.

save the file

=====================================================

'#' cd ../..

You will be int he /etc/ansible directory now.

'#' vim playbookProject.yml

---
- name: Execute projectAnsible role
  hosts: webserver
  become: true
  roles:
    - projectAnsible



'#' ansible-playbook playbookProject.yml
