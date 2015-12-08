# VirtualHost macros

Easy macros for making VirtualHosts in Apache configs.

* The really short macros are really only useful for basic PHP
  websites. For other purposes, you should still make <VirtualHost>
  tags (and use the individual macros).
* For SSL, certificates should be located in /etc/apache2/certs/
* SSL bundle certificate is currently always loaded from
  /etc/apache2/certs/root.crt
* Currently, admin is always admin@localhost, this should be
  changed to a variable.
* Defualt port 80 redirects to https://localtest.me/ at the moment

## Examples

    # Set up example.com as a vhost with /var/www_example.com/ as
    # document root.
    Use VHost example.com

    # Set up example.com as a vhost with an SSL certificate at
    # /etc/apache2/certs/example.com.crt and /example.com.key
    Use SecureVHost example.com example.com

    # Set up example.com to be accessible via SSL only (redirect)
    Use SecureVHost example.com example.com
    Use SecureVHostOnly example.com

## LetsEncrypt

To use LetsEncrypt with this config, first set up a config like this:

    Use VHost example.com

Restart Apache and create `/var/www_example.com`. Then, run `letsencrypt-auto` with `webroot`, like this:

    letsencrypt-auto certonly -a webroot --webroot-path /var/www_example.com/ -d example.com -d www.example.com --server https://acme-v01.api.letsencrypt.org/directory

You can now remove the first `VHost` macro use, and do something like this instead:

    Use LetsEncryptVHost example.com
    Use SecureVHostOnly example.com
