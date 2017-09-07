Nginx
======

Install nginx from the official repository.

This role clears the default nginx configuration and looks for additional configuration files in `/etc/nginx/conf.d/*.conf`. Roles that need nginx should include their own nginx config file and place it in this directory.

Requirements
------------

Open appropriate ports in the firewall.

Role Variables
--------------

Set the FQDN of the server:

    nginx_server_name: "{{ ansible_fqdn }}"

Include config file that redirects traffic to `nginx_http_port` to https:

    nginx_redirect_http: False

Define ports:

    nginx_http_port: 80
    nginx_https_port: 443

SSL Configuration:

    nginx_ssl_enabled: False
    nginx_ssl_cert_path: /etc/pki/tls/certs
    nginx_ssl_key_path: /etc/pki/tls/private
    nginx_ssl_filename: "{{ ansible_fqdn }}"

Define log directories:

    nginx_log_dir: /var/log/nginx
    nginx_error_log: error.log
    nginx_access_log: access.log

Change SELinux settings to allow nginx to bind to other ports (CentOS >= 6.6):

    nginx_selinux_ports:
      - context_t: "http_port_t"
        protocol: tcp
        port: "9200"


License
-------

MIT
