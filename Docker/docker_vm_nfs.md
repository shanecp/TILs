# Run Docker with NFS (or rsync) on a Mac


When you're having nightmares with files not syncing or slow syncing with docker-machine, then you need some manual process to make it work. This happens because the default `vboxsf` mounting is too slow. We have to either mount the volumes (i.e folders) with RSync, NFS or Samba.

Here's how to do it with NFS (with the least amount of plugins/hacks).


1. See https://github.com/dduportal/boot2docker-vagrant-box
2. Run `vagrant init dduportal/boot2docker`
3. Need to run docker from host OS? Keep reding. Otherwise run `vagrant up` now.
4. Add these to your `.bash_profile` or `.zshrc` config.

```
export DOCKER_CERT_PATH=./tls
export DOCKER_HOST=tcp://192.168.10.10:2376
export DOCKER_TLS_VERIFY=1
export DOCKER_MACHINE_NAME=dockerhost

# Enable NFS shares. See the documentation for rsync instructions.
export B2D_NFS_SYNC=1
```
The IP add ress in `DOCKER_HOST` will be your Docker machine's IP.

5.) Create `bootlocal.sh` on the root folder (where `Vagrantfile` is) and add the following.
You need this to mound files as NFS.

```
# Regenerate certs for the newly created private network IP
sudo /etc/init.d/docker restart
# Copy tls certs to the vagrant share to allow host to use it
sudo cp -r /var/lib/boot2docker/tls /vagrant/
```

6.) Run `vagrant up`

7.) Now you should be able to see docker status by `docker ps` or login to VM with `vagrant ssh`

--------------------- ** -------

### Configuring NGINX

8.) Create an `app.conf` file and this
```
server {
    listen 192.168.10.10:80;
    index index.html;

    # Preserve the logs	
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;

    # Make the files update in (almost) real-time
    sendfile off;
}
```

9.) Create a `public` folder and add your web stuff in there.

10.) SSH to the VM, and start a new Docker nginx container.
```
docker run -d -P -v /vagrant/app.conf:/etc/nginx/sites-enabled/app.conf -v /vagrant/public:/usr/share/nginx/html --name web nginx
```

To see the created docker container, run `docker ps`. Then get the port assigned next to 80, and load it in your browser along with the IP address.

```
http://192.168.10.10:32769/
```
