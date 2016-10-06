# How to create a new SSH key-pair on a Linux / Mac

```
ssh-keygen --help

ssh-keygen -t rsa <the type>
		   -b 4096 (bytes)
		   -C <comment>
		   -f (file = id_<filename>
```

Enter a passphrase (Add when a manual login is required. Don't use a passphrase if you're using this for automation)

```
id_<filename> <- this is the private key, don't give this to anyone
id_<filename>.pub <- this is the public key, give this to anyone
```

Get the public key with,
```
cat id_<filename>.pub
```
