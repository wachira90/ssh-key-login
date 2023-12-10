# SSH FINAL SUMMARY

**login root user first

## adduser

```sh
adduser wachira
```

## adduser to groups

```sh
root@fda-openshift:~# usermod -aG adm wachira
root@fda-openshift:~# usermod -aG sudo wachira
root@fda-openshift:~# usermod -aG microk8s wachira
```

## switch to user 

```sh
su - wachira
```

## generate key and copy private key

```sh
ssh-keygen -t rsa -b 4096 -N "" -f "$HOME"/.ssh/id_rsa

cp -rp .ssh/id_rsa wachira.pem
```

## permission 

```sh
chmod 0640 .ssh/authorized_keys
chmod 0600 .ssh/id_rsa
chmod 0644 .ssh/id_rsa.pub
```

## verify permission

```sh
wachira@fda-openshift:~$ ls -la .ssh/
total 24
drwx------ 2 wachira wachira 4096 Dec 10 04:10 .
drwxr-x--- 4 wachira wachira 4096 Dec 10 03:50 ..
-rw-r----- 1 wachira wachira  747 Dec 10 04:10 authorized_keys
-rw------- 1 wachira wachira 3389 Dec 10 03:27 id_rsa
-rw-r--r-- 1 wachira wachira  747 Dec 10 03:27 id_rsa.pub
-rw------- 1 wachira wachira 3389 Dec 10 03:27 wachira.pem
wachira@fda-openshift:~$
```

## copy public_key to authorized_keys

```sh
wachira@fda-openshift:~$ cat .ssh/id_rsa.pub >> .ssh/authorized_keys
```

## ssh config key login only

nano /etc/ssh/sshd_config

```sh
Include /etc/ssh/sshd_config.d/*.conf
Port 22
ListenAddress 0.0.0.0
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
UsePAM no
X11Forwarding no
PrintMotd no
AcceptEnv no
Subsystem       sftp    /usr/lib/openssh/sftp-server
AllowUsers ubuntu tewin wachira
ChallengeResponseAuthentication no
```

** use `wachira.pem` for login
