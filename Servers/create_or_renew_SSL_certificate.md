# Create or Renew SSL Certificate

To renew SSL you need to generate a CSR. You may use the existing key or create a new key.

```
// Create a CSR with the existing key
openssl req -new -key private.key -out csr.pem
```

Then go to your Certificate Issuer and insert the CSR. You'll get get the certificate files emailed to you as a bundle. You have to merge all files in the bundle in correct order to a single file. Usually  to order is,

1. Your SSL
2. Other Certificates
3. More Certificates
4. Root Certificate

Merge all certificates to a single file, for example 'certificates.bundle'.

Then add both key and certifiate to your server's config.

The following example is from an nginx config.

```
ssl_certificate     /etc/ssl/certificate.ca-bundle;
ssl_certificate_key /etc/ssl/private.key;
```

Then test your config and restart the server.

```
sudo nginx -t
sudo service nginx reload
```

Finally test if your certificate is properly installed.

1. Does the website load properly, and does the SSL padlock show the updated SSL expiry date?
2. Validate certtificate with https://certlogik.com/ssl-checker/
