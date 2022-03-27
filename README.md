# ansible-nginx-vhosts

```
---
- hosts: 'localhost'
  remote_user: user
  become: yes
  become_user: root
  become_method: sudo
  roles: 
    - pastir.nginx_vhost

  vars:
     - nginx_config_upstream_upload_enable: true
     - upstream_conf_file_location: /etc/nginx/conf.d
     - upstream_conf_file_name: upstreams.conf
     - upstream_template_file: templates/upstream/upstream.conf.j2
     - upstreams:
          - 
               name: backend_php7
               servers:
                  -  
                      unix_socket: unix:/var/run/php/php7.0-fpm.sock
          - 
               name: backend_php8
               zone: 
                  name: upstream_dynamic 
                  size: 64k
               servers:
                  -
                      address: backend1.example.com
                      weight: 5
                      fail_timeout: 5s
                  -
                      address: backend2.example.com
                      backup: true 
```