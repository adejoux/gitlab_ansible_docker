# Gitlab installation with Ansible and Docker

This Ansible playbook install Gitlab with Docker.

# Parameters

Parameters are defined in **group_vars/all**:

```
gitlab_config_dir: "/srv/gitlab/config"
gitlab_logs_dir: "/srv/gitlab/logs"
gitlab_data_dir: "/srv/gitlab/data"
gitlab_image: "gitlab/gitlab-ce:latest"
gitlab_ssh_port: "2222"
gitlab_https_port: "127.0.0.1:10443"
gitlab_http_port: "127.0.0.1:10080"
gitlab_site: "git.example.com"
gitlab_smtp_server: "mail.example.com"
gitlab_smtp_user: "gitlab@example.com"
gitlab_smtp_password: "mypassword"
gitlab_smtp_domain: "example.com"
gitlab_fullchain: "/etc/letsencrypt/live/git.example.com/fullchain.pem"
gitlab_cert_key: "/etc/letsencrypt/live/git.example.com/privkey.pem"
```

#run

Run it with:
```
ansible-playbook -i hosts gitlab.yml
```

The output should be:

```
PLAY [all] *********************************************************************

TASK [setup] *******************************************************************
ok: [192.168.56.101]

TASK [docker : Install Docker] *************************************************
ok: [192.168.56.101]

TASK [docker : Install Docker python library] **********************************
ok: [192.168.56.101]

TASK [gitlab : Create gitlab directories] **************************************
ok: [192.168.56.101] => (item=/srv/gitlab/config)
ok: [192.168.56.101] => (item=/srv/gitlab/logs)
ok: [192.168.56.101] => (item=/srv/gitlab/data)

TASK [gitlab : Install Gitlab container] ***************************************
ok: [192.168.56.101]

TASK [gitlab : deploy gitlab configuration] ************************************
ok: [192.168.56.101]

TASK [gitlab : deploy gitlab NGINX configuration] ******************************
changed: [192.168.56.101]

TASK [gitlab : Enable gitlab NGINX configuration] ******************************
ok: [192.168.56.101]

TASK [gitlab : Restart NGINX] **************************************************
ok: [192.168.56.101]

PLAY RECAP *********************************************************************
192.168.56.101             : ok=9    changed=1    unreachable=0    failed=0   
```


Copyright
==========

The code is licensed as GNU AGPLv3. See the LICENSE file for the full license.

Copyright (c) 2016 Alain Dejoux <adejoux@djouxtech.net>
