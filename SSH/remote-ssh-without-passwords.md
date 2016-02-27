## SSH Setup for Remote Server Logins without a Password

### Create a new SSH key pair in a Mac

Use the following commands
```
ssh-keygen
```

### Copy your public key to a remote server

By copying your public key, you won't be prompted to enter the password every time you need to login.

Change `id_rsa_production_servers.pub` to the public key file you've created above.

```
cat -t ~/.ssh/id_rsa_production_servers.pub | ssh user@domainname.com "umask 0077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

### Handling Multiple SSH keys and aliases

To handle multiple SSH keys, create a file named `~/.ssh/config` and use a text editor to add contents below

```
# Default SSH
Host *
	IdentityFile ~/.ssh/id_rsa

# Server 1
Host awesomesite
	HostName yourdomain.com.au
	User root
	IdentityFile ~/.ssh/id_rsa_production_servers

# Server 2
Host *.github.*
  IdentityFile ~/.ssh/github_id.rsa

# Server 3
Host personalid
  HostName bitbucket.org
  IdentityFile ~/.ssh/personalid
```

After that, you can easily SSH with the following

```
ssh awesomesite
```



### For troubleshooting SSH config or connections use `-vvv` flag
```
ssh -vvv user@domainname.com
ssh -vvv domainname.com
```

### Reference

- http://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/
- http://blog.sanctum.geek.nz/uses-for-ssh-config/
