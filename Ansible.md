**Install ansible in Control Node, As am using Amazon Linux2 OS, Amazon-linux-extras will install all required dependencies**

```bash
amazon-linux-extras install ansible2 -y
```

verify ansible version by running below command

```bash
ansible --version
```

```bash
which ansible
```

```bash
ansible-config dump
```

**Create a common user for all ansible activities**

Creating a user, Here am using "ansibleusr" user and set password.

```bash
useradd ansibleusr
```
```bash
passwd ansibleusr
```

**Provide Sudeoer permissions**
```bash
visudo
```

Add below entry to sudeor file.

```bash
ansibleusr ALL=(ALL) NOPASSWD: ALL
```

```bash
su - ansibleusr
```

**Enable SSH Connection across the instances.**

```bash
vim /etc/ssh/sshd_config
```
```bash
Set "PasswordAuthentication yes"
```

```bash
service sshd restart
```

**Connect to all the nodes and Create common user same as Above.**

```bash
useradd ansibleusr
passwd ansibleusr
visudo
ansibleusr ALL=(ALL) NOPASSWD: ALL
su - ansibleusr
vim /etc/ssh/sshd_config
Set "PasswordAuthentication yes"
service sshd restart
```

**Configure password-less authentication.**

*Perform this on Control Node*

Create an SSH Public key and Private Key in Server and Copy Public Key to across the instances. Make sure you are doing this as ansibleusr, and perform this from Control Node.

```bash
ssh-keygen -t rsa
```

```bash
ssh-copy-id ansibleuser@Managed-node-1/2/3
```

Now test the Password-less authentication. It should not prompt any password.

```bash
ssh Node-ip
```


***When we install ansible, we will get 3 IMP files under /etc/ansible***
1. ansible-config
2. hosts
3. roles

In "ansible-config" file, hosts file entry is commented default.

Create a group in hosts file (i.e; webservers / web-group / dbservers)


**Commands to verify hosts**

To list all the hosts ansible is managing run below command.

```bash
ansible all --list-hosts
```

You can also ping all/group of nodes.

```bash
ansible all -m ping -v
```

If you want to list the nodes from a specific group, use below command

```bash
ansible mygroup --list-hosts
```
