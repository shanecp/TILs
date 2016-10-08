# How to Install Tripwire on a new Ubuntu machine

Tripwire is an IDS (Intrusion Detection System) used to protect the integrity of the filesystem.

```
apt-get install -y tripwire

# You'll be asked for two keys
# Site Key - Used to secure configuration files
# Local Key - Used on each machine to run binaries

# Create Policy File
sudo twadmin --create-polfile /etc/tripwire/twpol.txt

# initialize database
sudo tripwire --init

# Find the files which are triggering the IDS
sudo sh -c 'tripwire --check | grep Filename > /etc/test_results.txt'

# Remove the false-positives from the policy
sudo vim /etc/tripwire/twpol.txt

# On 'Boot Scripts' section, comment out '/etc/rc.boot'
# Comment out other files found from the test_results above
# Make changes to the 'proc' section, remove var sections

# After the policy is created, build the encrypted policy file
sudo twadmin -m P /etc/tripwire/twpol.txt

# Initialize the database to implement policy
sudo tripwire --init

# Check the warnings, and add them to the list of exclusions on the policy file
sudo tripwire --check

# Delete test results
sudo rm /etc/tripwire/test_results

# Delete plain text file
sudo rm /etc/tripwire/twpol.txt

# If you need to generate the policy file again from the encrypted file, use the following
sudo sh -c 'twadmin --print-polfile > /etc/tripwire/twpol.txt'

# Setup email notifications
sudo apt-get install -y mailutils

# Send the status report
sudo tripwire --check | mail -s "Tripwire report for `uname -n`" your_email@domain.com

# Update the database (because we installed a new package)
sudo tripwire --check --interactive


# Add the tripwire check to the cron

# See if there's already a crontab
sudo crontab -l

# if there is, backup the file
sudo sh -c 'crontab -l > crontab.bad'

# Edit cron
sudo crontab -e

# Add the cron to run at 3.30am, daily
30 3 * * * /usr/sbin/tripwire --check | mail -s "Tripwire report for `uname -n`" your_email@domain.com
```

### If you have completely forgotten your site passphrase, generate a new site key with a new passphrase by running
```
twadmin -m G -S /etc/tripwire/site.key
# then run 
dpkg-reconfigure tripwire
```

# Reference
https://www.digitalocean.com/community/tutorials/how-to-use-tripwire-to-detect-server-intrusions-on-an-ubuntu-vps


