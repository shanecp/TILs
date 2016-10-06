# Instructions for an Initial Cloud Server Setup (Ubuntu)

Here are the instrutions for an initial setup of a cloud server with Ubuntu. Main focus in on basic security.
Login to the server via SSH as the `root` first.

### Update packages
```
sudo apt-get update
sudo apt-get upgrade
```

Install basic packages
```
sudo apt-get install -y tmux vim curl wget unzip
```

### Add a new user and remove root access

Add a new user with the name `john` and add him to the `sudo` group.
```
adduser john
<Enter a new password, and record this somewhere>
adduser john sudo
```

Then exit from the console, and see if you can login as the new user
```
exit
ssh john@<server_name_or_ip_address>
```

### Get key based SSH access to the new user
```
mkdir ~/.ssh && sudo chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
exit
scp ~/.ssh/id_rsa.pub master@<server_name_or_ip_address>:~/.ssh/authorized_keys
```

### Block root login and password authentication for security

Edit SSH Daemon options and remove root login and password authentication
```
sudo vim /etc/ssh/sshd_config
```

Then change the following options in the file
```
PermitRootLogin no		# disable root access
PasswordAuthentication no	# stops users from logging in by password (after this you can only login with SSH)
```

Save the file and exit with `:wq`

Restart SSH BUT DON'T LOGOUT!!!
```
sudo service ssh restart
```

**IMPORTANT: open a new terminal window and SSH into it, test that you can connect without a password.**
If it asks for a password, you'll lock yourself out from the account!!!. Go back and check the steps again.

```
ssh john@<server_name_or_ip_address>
```

## Install a Firewall

Use UFW (Uncomplicated Firewall) for easier administration of the firewall. This is just a front-end for `iptables`.

```
sudo apt-get install ufw
sudo ufw status 	-- check status

sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 80/tcp

-- delete a rule
sudo ufw delete allow 80/tcp

--- whitelist an IP address
sudo ufw allow from 192.168.255.255

--- enable firewall
sudo ufw enable 
sudo service ufw restart


-- disable firewall
sudo ufw disable
```

# Install Fail2Ban for failed login detection

```
sudo apt-get install fail2ban
sudo cp jail.conf jail.local
sudo vim jail.local
```

-- add your own IP to the whitelist on `jail.local` to prevent the risk of getting your static IP blacklisted
```
ignoreip = 127.0.0.1/8 110.172.125.54
```

Save the file and exit with `:wq`

Restart the service
```
sudo service fail2ban restart
```

## Locked out from the server?

Locked yourself out from the server? Too bad. Then you'll have to rebuild the image (all data will be lost). 
On DigitalOcean, this can be done by going to `Droplet > Destroy > Rebuild droplet`

## Reference
https://www.linode.com/docs/security/securing-your-server
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04
https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server
https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04
