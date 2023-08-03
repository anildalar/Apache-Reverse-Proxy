# Apache-Reverse-Proxy
Apache Reverse Proxy

sudo a2enmod proxy
sudo a2enmod proxy_http
sudo systemctl reload apache2

sudo a2dissite default-ssl.conf
sudo a2dissite fcmb.dollorinfotech.com.conf
sudo a2dissite 000-default-le-ssl.conf

/etc/apache2/sites-available

vim 000-default.conf


<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.

        ProxyPreserveHost On
        Options FollowSymlinks
        ServerSignature Off
        ProxyPass / http://127.0.0.1:3000/
        ProxyPassReverse / http://127.0.0.1:3000/
</VirtualHost>
<VirtualHost *:443>
    ServerSignature Off
    Options FollowSymlinks

    # SSL Configuration
    SSLEngine on

    SSLCertificateFile /etc/letsencrypt/live/fcmb.dollorinfotech.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/fcmb.dollorinfotech.com/privkey.pem
    SSLCertificateChainFile /etc/letsencrypt/live/fcmb.dollorinfotech.com/chain.pem


    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:3000/
    ProxyPassReverse / http://127.0.0.1:3000/
</VirtualHost>

