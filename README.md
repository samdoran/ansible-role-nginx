Nginx
========

Install Nginx from the official Nginx repository.

This role clears the default nginx configuration and looks for additional configuration files in `/etc/nginx/conf.d/*.conf`. Roles that need Nginx should include their own Nginx config file and place it in this directory with a `.conf` extension.

Requirements
------------

Open appropriate ports in the firewall.

Role Variables
--------------

Include config file that redirects traffic to `nginx_http_port` to HTTPS:

    nginx_redirect_http: False

Define ports:

    nginx_http_port: 80
    nginx_https_port: 443

Default server name:
    nginx_server_name: "{{ ansible_fqdn }}"

TLS Configuration:

    nginx_tls_enabled: no
    nginx_tls_cert_path: /etc/pki/tls/certs
    nginx_tls_key_path: /etc/pki/tls/private
    nginx_tls_filename: "{{ ansible_fqdn }}"

Define log directories:

    nginx_log_dir: /var/log/nginx
    nginx_error_log: error.log
    nginx_access_log: access.log

Change SELinux settings to allow Nginx to bind to other ports (CentOS >= 6.6):

    nginx_selinux_ports:
      - context_t: "http_port_t"
        protocol: tcp
        port: "9200"


License
-------

Apache 2.0
