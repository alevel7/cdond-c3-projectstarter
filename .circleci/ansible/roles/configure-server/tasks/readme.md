## Back-end server configuration playbook goes here.
---
- name: "Add node.js from source"
  become: true
  shell: |
    curl -sl https://deb.nodesource.com/setup_13.x | sudo -E bash -

- name: "install dependencies."
  become: true
  apt:
    name: ["nodejs", "npm"]
    state: latest
    update_cache: yes

- name: "install pm2"
  become: true
  npm:
    name: pm2
    global: yes
    production: yes
    state: present

- name: "move env file to /etc/profile.d/"
  become: true
  copy:
    src: myenv.sh
    dest: /etc/profile.d/