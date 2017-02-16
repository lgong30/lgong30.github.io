---
layout: post
title: Play with Github
categories: [skill]
tags: [git, ssh]
---

As one of the most popular modern version control tools, `git` is getting more and more popular. As a result, [Github](https://github.com) becomes a necessary part of programmers' daily life. In this post, we will introduce some tricks to help programmers play with Github. These tricks are extremely useful, when you are dealing with multiple Github accounts (_e.g.,_ one for company codes, one for personal codes). 

Avoid Password with SSH: Single Account Case
--------------------------------------------

The first trick is to avoid entering password while pushing local repositories to remote or pulling/fetching private remote repositories.

### Generating SSH Key

```shell
$ ssh-keygen -t rsa -b 4096
```

Generally, we will see outputs as follows.

```shell
Generating public/private rsa key pair.
Enter file in which to save the key (/home/mininet/.ssh/id_rsa): git_key_example
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in git_key_example.
Your public key has been saved in git_key_example.pub.
The key fingerprint is:
38:44:30:a8:a4:6f:eb:c1:66:12:bb:28:dd:bd:7c:29 mininet@mininet-vm
The key's randomart image is:
+--[ RSA 4096]----+
|   .o..          |
| ..  o           |
|o.    .          |
|o    . .         |
|..    o S        |
| +o    .         |
|oo=o .   .       |
|o=o...E o        |
|+..   o+         |
+-----------------+
```

During the above process, you will be asked to 
+ enter the file name for your key pair (In the above example, we used `git_key_example` as the file name.). If you only enter the file name, the key pair would be stored in current directory. If you want to store your key in somewhere else, you can add the full path of your file.
+ Enter a passphrase (If you use SSH out of security, then we strongly suggest you enter one. However, if you choose SSH just because you do not want to enter the password, then you are suggested to leave it empty. Because otherwise you will be asked to enter the same passphrase whenever you `git push`.).

After the above process, you will find the key pair in the directory you enter. In the above example (assume current directory is `/home/mininet/.ssh/`), you will find the following two new files:
+ git_key_example
+ git_key_example.pub
The first one is the private key and the second is the public key. 

### Upload to Github

+ Prepare (get the content of **public key**):  

  ```shell
  $ cat git_key_example.pub
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDEKiWm5RBjQJOsNmGi6GQNAqhoovXA/qVm1i+nyZ0j18kQkCaeTSdGDUs9UiV9ts7vG4MLHucRLI4dh5hvOH3gr0W7MhB8JubOptKJWtjGaw4f1Vb3xxdKGJ7igHA/ud2N5omkJIptyKXrvybLkqnkLcGgxttvqheOGczzC2g0MIa7MxqhlALkdj0QVyjrtbqltB+k0+lAqyeLRJGrWqmRZ8FlPn1KslpWKq+LFAuKNg24YF7HxbGubdVVeGsKTOowrDBN5IGdEJvlqwZsVUvGnx1oznJzpfdw80KCcm1vFmMU6E3oo3OLfgjhRvcfl5DV+OznTPPr3KbybNSAUIr5lR00LkBhKH0nxiHcERi9/E6/95/fVovY8vV38wPLXBCq/jkmQmtUFHQ86C/1f0bgAAano56Ovd2p7ur5x2pe+sCUxwcQQ3kYOpesqQhCvpkIA6kDGznsGiY1418sCj8D7na1MoifvzsPfpAbO8zAO0YtITEfaaiBum9i4GbzMTl4AzuLIff03XhPRHlew/9McG6DlKm04A96QmRbUZQHzdUyivOSpG7HCFBrYmiEga1EPV8WRRU8SJu0hftV0Upk2T46KASygvo5A0wZ6YUWytHhY8Sdtrx56y4mOtol3RkQtR/vUGCjxIbtl3Lw1J3xoxQkxynesUM8bopBgkwxiQ== mininet@mininet-vm
  ```
+ Open the browser and go to `github.com`, then  

  > Log in
  
  > Find "SSH and GPG keys" in "Personal settings"
 
  > "New SSH key"
   
  > Paste the content of your public key.

### Add Your SSH Key to `ssh-agent`

```shell
$ eval "$(ssh-agent -s)"
$ ssh-add /path/to/your_ssh_key
```

To avoid to enter the above commands every time after you restart your computer, you can add them in your bash configuration file (_e.g.,_ `~/.bashrc` for Ubuntu, `~/.bash_profile` for OS X).

Multiple Accounts Case
----------------------

Assume you have two github account, for ease of presentation, we refer to them as A and B.

+ Configure SSH keys for A and B, respectively by the above approach
+ Edit `~/.ssh/config` and add the following sentences at the end of the file: 

  ```shell
  Host github_A
    HostName github.com
    User git
    IdentityFile path/to/ssh-private-key-for-A

  Host github_B
      HostName github.com
      User git
      IdentityFile path/to/ssh-private-key-for-B
  ```
+ Change `github.com` to the corresponding host name you configured above. Suppose the remote repository associated with account A is `git@github.com:A/example.git`:  

  ```shell
  $ git remote add remote_A git@github_A:xlong88/publications.git
  $ ... 
  $ git push remote_A master
  ```
  Similar for B.






