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
