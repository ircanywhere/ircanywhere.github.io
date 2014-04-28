Reverse Proxies
===============

Apache
~~~~~~

You can run IRCAnywhere behind Apache quite easily, you can also choose to run it behind a subdirectory if you please, this example runs it behind `http://domain.com/ircanywhere`. You can do this by adding the following to your configuration file. ::

    ProxyPreserveHost On
    RewriteEngine On

    RewriteRule ^/?ircanywhere/(.*) https://%{SERVER_NAME}:3000/$1 [P]

    RewriteRule ^/?api/(.*) https://%{SERVER_NAME}:3000/api/$1 [P]
    RewriteRule ^/?build/(.*) https://%{SERVER_NAME}:3000/build/$1 [P]
    RewriteRule ^/?websocket/(.*) https://%{SERVER_NAME}:3000/websocket/$1 [P]
    RewriteRule ^/?sounds/(.*) https://%{SERVER_NAME}:3000/sounds/$1 [P]

    ProxyPassReverse /ircanywhere/ https://%{SERVER_NAME}:3000/

    ProxyPassReverse /websocket https://%{SERVER_NAME}:3000/websocket/
    ProxyPassReverse /build https://%{SERVER_NAME}:3000/build/
    ProxyPassReverse /api https://%{SERVER_NAME}:3000/api/
    ProxyPassReverse /sounds https://%{SERVER_NAME}:3000/sounds/

Nginx
~~~~~

The following will run ircanywhere under a subdomain in nginx, like apache this can be configured to be a top level domain or a sub directory easily. ::

    server {
        listen 80;
        server_name ircanywhere.domain.com;

        location /websocket/ {
            proxy_pass http://localhost:3000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }

        location / {
            proxy_http_version 1.1;
            proxy_set_header   X-Real-IP        $remote_addr;
            proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
            proxy_set_header   X-NginX-Proxy    true;
            proxy_set_header   Host             $http_host;
            proxy_set_header   Upgrade          $http_upgrade;
            proxy_redirect     off;
            proxy_pass         http://localhost:3000;
        }
    }