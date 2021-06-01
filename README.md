# ssh-key-login
use ssh pem file login


## 1 MACHINE

### ssh-keygen -t rsa -b 4096 -N "" -f "$HOME"/.ssh/id_rsa

## 1 MACHINE TO 2 

### ssh ubuntu@192.168.4.42 -p 22 "mkdir -p .ssh"

## 2 MACHINE

### sudo chmod -R 700 .ssh/

## 1 MACHINE

### ssh ubuntu@192.168.4.42 -p 22 "chmod 700 .ssh; chmod 640 .ssh/authorized_keys"

## IF ERROR => chmod: cannot access ‘.ssh/authorized_keys’: No such file or directory

### ssh ubuntu@192.168.4.42 -p 22 "touch .ssh/authorized_keys"

## 1 MACHINE

### cat .ssh/id_rsa.pub | ssh ubuntu@192.168.4.42 -p 22 'cat >> .ssh/authorized_keys'

## CONFIG SSH  MACHINE  2

### nano /etc/ssh/sshd_config

## CHANGE

### PasswordAuthentication yes

## TO

### PasswordAuthentication no

## TEST 1 MACHINE TO 2

### ssh ubuntu@192.168.4.42 -p 22
