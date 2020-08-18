# Playbook for app running on port 80

```python
# This is a YAML file to install nginx onto oue web VM using YAML
---

# where do we want to install
- hosts: web

# get the facts
  gather_facts: yes

# changes access to root user
  become: true

# what do we want ansible to do for us in the playbook
# In this case our only task is to install nginx

  tasks:
  - name: Install nginx
    apt: pkg=nginx state=present

  - name: nginx reverse proxy
    shell:  |
      sudo unlink /etc/nginx/sites-enabled/default
      cd /etc/nginx/sites-available
      sudo touch reverse-proxy.conf
      sudo chmod 666 reverse-proxy.conf
      echo "server{
        listen 80;
        server_name development.local;
        location / {
            proxy_pass http://127.0.0.1:3000/;
        }
      }" >> reverse-proxy.conf
      sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
      sudo service nginx restart



# Installing nodejs
  - name: Install Nodejs
    apt: pkg=nodejs state=present

# Installing npm
  - name: Install npm
    apt: pkg=npm state=present


# Downloading pm2
  - name: Install pm2
    npm:
      name: pm2
      global: yes


  - name:
    shell: |
      cd app
      sudo npm install -g npm
      npm install
      pm2 stop all
      pm2 start app.js -f
```