# ssh-key-login
use ssh pem file login


## A MACHINE

### ssh-keygen -t rsa -b 4096 -N "" -f "$HOME"/.ssh/id_rsa

## A MACHINE TO B 

### ssh ubuntu@192.168.4.42 -p 22 "mkdir -p .ssh"

## B MACHINE

### sudo chmod -R 700 .ssh/

## A MACHINE

### ssh ubuntu@192.168.4.42 -p 22 "chmod 700 .ssh; chmod 640 .ssh/authorized_keys"

## IF ERROR => chmod: cannot access ‘.ssh/authorized_keys’: No such file or directory

### ssh ubuntu@192.168.4.42 -p 22 "touch .ssh/authorized_keys"

## A MACHINE

### cat .ssh/id_rsa.pub | ssh ubuntu@192.168.4.42 -p 22 'cat >> .ssh/authorized_keys'

## CONFIG SSH  MACHINE  B

### nano /etc/ssh/sshd_config

## CHANGE

### PasswordAuthentication no

### ChallengeResponseAuthentication no

### UsePAM no

### PermitRootLogin no

## TEST A MACHINE TO B

### ssh ubuntu@192.168.4.42 -p 22

## Copy key.pem to another machine

### cp -rp .ssh/id_rsa key.pem

### ssh -i key.pem ubuntu@192.168.4.42 -p 22

