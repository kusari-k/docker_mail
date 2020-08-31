# mail Container

## _setting file format_

```
###mail###
ssl_domain:example.com
hostname:example.com,example.org,example.net
user1:email1:password1
user2:email2:password2
user3:email3:password3
```

## _up container_

```
./script.sh
sudo firewall-cmd --add-forward-port=port=25:proto=tcp:toport=1025
sudo firewall-cmd --add-forward-port=port=143:proto=tcp:toport=10143
sudo firewall-cmd --add-forward-port=port=587:proto=tcp:toport=10587
sudo firewall-cmd --add-forward-port=port=993:proto=tcp:toport=10993
podman play kube podman.yml
sudo firewall-cmd --reload
#podman run -itd --pod mail_pod -v /home/podman/mail_pod/postfix:/podman/postfix -v /home/podman/mail_pod/postfix_log:/podman/postfix_log --name postfix postfix
#podman exec -it postfix bash
```

#### _SE-Linux setting_

```
sudo mkdir -p -m 777 /home/podman/mail_pod/postfix /home/podman/mail_pod/postfix_log /home/podman/mail_pod/cyrus /home/podman/mail_pod/cyrus_log /home/podman/mail_pod/cyrus_replica /home/podman/mail_pod/cyrus_replica_log
sudo semanage fcontext -a -t container_file_t "/home/podman(/.*)?"
sudo restorecon -R /home/podman
```

