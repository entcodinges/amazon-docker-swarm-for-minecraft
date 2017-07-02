# amazon-docker-swarm-for-minecraft
Test for Docker swarm with minecraft

# Preparation

-Created three machines on amazon with the webgui. Used Amazon Linux AMI 2017.03.1 (HVM).
add additional volume 10GB for Docker VG.

-install ansible on master
yum install ansible --enablerepo=epel

-add directory /ansible
mkdir /ansible

-edit the file /etc/ansible/ansible.cfg
edit the path to the inventory file to /ansible
edit inventory_ignore_extensions = ~, .orig, .bak, .ini, .cfg, .retry, .pyc, .pyo, .yml, .yaml

-create ssh key in the master host
ssh-keygen

-copy the content of the id_rsa.pub into the clipboard
less /home/ec2-user/.ssh/id_rsa.pub

-connect to master and the nodeservers with the amazon pem file and add the public key to the authorized key file
vim /home/ec2-user/.ssh/authorized_keys

-connect from the master to master and the nodes with the internal dns name
ssh -i /home/ec2-user/id_rsa ec2-user@"internal dns name"

-create the ansible inventory file
```
vim /ansible/amazon.inv
[master]
"master internal name"
[node]
"node internal name"
"node internal name"
```

-create ansible playbook for install git from the file installgit.yml and saved /ansible
ansible-playbook -i amazon.inv installgit.yml

-clone the git to your amazone master machine
