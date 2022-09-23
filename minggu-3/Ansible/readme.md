# ANSIBLE
## 1. Install Ansible
### Install Ansible using pip 
```bash
python3 -m pip install --user ansible
```
### Create Inventory file with .ini extention and fill that file with these and save
```bash
[aplikasi]
103.191.92.240 ansible_user=bahril
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-3/Ansible/1.png?raw=true)


### Create ansible.cfg and put some code below
```bash
[defaults]
inventory = inventory.ini
private_key_file = ssh.pem
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-3/Ansible/2.png?raw=true)


* You can replace private_key_file with the directorry that your id_rsa file exist. I used ssh.pem cause i saved my id_rsa key inside that file.

* After that check your connection between your localhost and the remote server using these command

```bash
ansible all-i inventory.ini -m ping
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-3/Ansible/3.png?raw=true)


## 2. Create User
### First create a file with .yaml extention and create a user in it using these commands
```bash
- hosts : all
  gather_facts: no
  become : true
  
- name: "Create User"
  ansible.builtin.user:
      name: Bahril Ilmid Nugroho
      password: yeaboa
```
## 3. Install Nginx and Docker using Ansible

### Same as before, we should create an ansible playbook with .yaml extention for nginx and docker

* Nginx
```bash
- hosts : all
  become : true
  tasks:
          - name: "nginx installation"
            ansible.builtin.apt:
              name: nginx
              state: present
              allow_downgrade: yes
          
          - name: Creates directory
            file:
              path: /home/bahril/etc/nginx/monitoring
              owner: bahril
              state: directory    
```
* Docker
```bash
- hosts : all
  become : true
  tasks:
   
   - name: "Install required system packages"
     ansible.builtin.apt:
              pkg:
                - ca-certificates 
                - curl
                - gnupg
                - lsb-release
              state: latest
              update_cache: true
   
   -  name:  "Add Docker GPG apt key"
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present
  
   -  name: "Add Docker Repository"
      apt_repository: 
        repo: deb https://download.docker.com/linux/ubuntu focal stable
        state: present
 
   -  name:  "Install docker ce"
      ansible.builtin.apt:
        name: 
          - docker-ce
          - docker-ce-cli
          - containerd.io
          - docker-compose-plugin
  
   -  name: "user without sudo"
      shell: sudo usermod -aG docker bahril
  ```

  ## 4. Install Monitoring Using Ansible on Top Docker

  ### We need 3 kinds of application to implement monitoring that are node exporter, prometheus and grafana. All of those 3 apps should be installed in remote server and we will try to install it from Ansible. When we want to execute installation file we need each of them in .yml extention. 

  * Creating docker-compose file

  ```bash

  version: '3.8'

networks:
  monitoring:
    driver: bridge
    
volumes:
  prometheus_data: {}

services:
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    expose:
      - 9100
    networks:
      - monitoring

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
    expose:
      - 9090
    networks:
      - monitoring
```
    
* Create the Prometheus Configuration File

    create this file with prometheus.yml

```bash
global:
  scrape_interval: 1m

scrape_configs:
  - job_name: "prometheus"
    scrape_interval: 1m
    static_configs:
    - targets: ["localhost:9090"]

  - job_name: "node"
    static_configs:
    - targets: ["node-exporter:9100"]

remote_write:
  - url: "<Your Prometheus remote_write endpoint>"
    basic_auth:
      username: "<Your Grafana Username>"
      password: "<Your Grafana API key>"
```
And then you can up your docker compose

```bash
docker compose up -d
```

