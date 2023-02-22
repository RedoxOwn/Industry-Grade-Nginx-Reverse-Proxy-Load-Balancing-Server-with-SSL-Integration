# industry-level-nginx-reverse-proxy-load-balancing-server-ssl
This is a documentation showing how to install and deploy a industry-level nginx reverse-proxy load-balancing server with best SSL integration.

Step 1 – First, install nginx:
sudo apt-get update
sudo apt-get install nginx

Step 2 – Adjust the Network Firewall if necessary.

Step 3 – At the end of the installation process, Debian 10 starts Nginx. The web server should already be up and running.
systemctl status nginx

Output
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Tue 2022-06-28 18:42:58 UTC; 49s ago
     Docs: man:nginx(8)
 Main PID: 2729 (nginx)
    Tasks: 2 (limit: 1167)
   Memory: 7.2M
   CGroup: /system.slice/nginx.service
           ├─2729 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2730 nginx: worker process
           
This output reveals that the service has started successfully.

Step 4 – Now that you have your web server up and running, you can review some basic management commands.

To stop your web server, type:
sudo systemctl stop nginx

To start the web server when it is stopped, type:
sudo systemctl start nginx

To stop and then start the service again, type:
sudo systemctl restart nginx

If you are making configuration changes, Nginx can often reload without dropping connections. To do this, type:
sudo systemctl reload nginx

By default, Nginx is configured to start automatically when the server boots. If this is not what you want, you can disable this behavior by typing:
sudo systemctl disable nginx

To re-enable the service to start up at boot, you can type:
sudo systemctl enable nginx

Step 5 - Create the SSL certificate directory and switch to it.
mkdir -p /etc/nginx/ssl/example.com
cd /etc/nginx/ssl/example.com

Step 6 - Create a private key:
openssl genrsa -des3 -out server.key 2048

Step 7 - Then Remove its passphrase:
openssl rsa -in server.key -out server.key
