## Vagrant Setup

How to setup Vagrant on a new machine.


- Install VirtualBox (https://www.virtualbox.org/wiki/Downloads)
- Install Vagrant (https://www.vagrantup.com/downloads.html)

- Install Vaprobash (https://fideloper.github.io/Vaprobash/)
```
curl -L http://bit.ly/vaprobash > Vagrantfile
```

- (Optional) If you tend to do this regularly, add this as an alias into your `.bash_profile`
```
alias vaprobash="curl -L http://bit.ly/vaprobash > Vagrantfile"
```

There will be a file named `Vagrantfile` in the folder now. Open this on an editor and change it as needed.
You might need to add a Github Personal Access Token to the Vagrantfile.

- Start the intallation process

Initially this will take a while, as it's installing a whole Virtual Machine.

```
vagrant up
```

After you've done the setup for the first time, you may need to setup the DocumentRoot on Apache. Login to Vagrant server and run the following commands
```
vagrant ssh
cd /etc/apache2/sites-enabled
ls # get the conf file name from here
sudo vi [file_name].conf
```
On the config file, set the `DocumentRoot` to a root directory on your disk.
```
DocumentRoot /vagrant/public_html
```

Save the file with `:w!` and `:q`

Restart Apache server.
```
sudo service apache2 reload

```
Now if you visit the IP address on the browser, Vagrant should be up and running.
```
http://192.168.22.10.xip.io/
```
