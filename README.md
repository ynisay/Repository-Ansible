# Repository-Ansible
Playbook: A YAML file containing a series of tasks that Ansible executes on specified hosts.Task: A single action to be performed on a host, such as installing a package or restarting a service.Module: The units of work that Ansible executes, such as apt, yum, copy, and template.Inventory: A list of hosts, optionally organized into groups, that Ansible targets.Role: A way to group related tasks, handlers, files, templates, and variables.
---
- name: Install Nginx on webservers
  hosts: webservers
  become: yes

  vars:
    nginx_package: nginx

  tasks:
    - name: Ensure Nginx is installed
      apt:
        name: "{{ nginx_package }}"
        state: present
      when: ansible_os_family == "Debian"

    - name: Ensure Nginx is installed
      yum:
        name: "{{ nginx_package }}"
        state: present
      when: ansible_os_family == "RedHat"

    - name: Ensure Nginx is started
      service:
        name: nginx
        state: started
        enabled: yes
