# IPTables Commands

```

-- see the rules
sudo iptables -L 	list
			  -v 	verbose

sudo iptables -S 	list

iptables-save
iptables-restore

iptables-save > ~/rules.v4
iptables-restore > ~/rules.v4

apt-get install iptables perstistant
This will be saved in /etc/iptables

Port 22   SSH
Port 80	 (Web)
Port 443 (SSL)

sudo iptables -A INPUT		append to and of INPUT list
			  -i lo			loopback interface
			  -j ACCEPT 	jump to target

-- keep the established connections on going (so I don't block myself, because I'm currently connected)
sudo iptables -A INPUT
			  -m conntrack 		module
			  --ctstate	RELATED, ESTABLISHED
			  -j ACCEPT

-- allow SSH traffic (repeat for port 80 and 443)
sudo iptables -A INPUT
			  -p tcp
			  --dport 22
			  -j ACCEPT

-- drop all other requests
sudo iptables -A INPUT
			  -j DROP		(or use DENY - this sends a failed message back, DROP just times-out the connection with no message)	


-- drop a rule (this is a 1 based index, not 0 based)
sudo iptables -D INPUT 5
sudo iptables -D INPUT (Then use the rule you get form `iptables -S` here)

-- insert a rule at a given postion
sudo iptables -I INPUT 5	insert at postion 5
			  -p tcp
			  --dport 445
			  -j ACCEPT	

			  
```
