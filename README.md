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

Step 8 - Create a CSR (Certificate Signing Request):
openssl req -new -key server.key -out server.csr

Step 9 - Use this CSR(server.csr file) to obtain a valid certificate from a certificate authority(Example: NO-IP, Namecheap etc).
-> After you buy an SSL certificate from NO-IP, you then upload the CSR(server.csr file) to them and request a valid certificate.
-> You will then wait for them to verify your request and then they will notify you par email. (Take about 30 minutes to 24 hours depending on the certificate authority)
-> Once your Certificate is approved, you then go back their plathform and download the 'PEM Chain' file and the 'CRT Package' zip that contains individual root, intermediate, and end-entity certificate files.
-> After you are done, you will have a .pem file and a zip usually containing three .crt files.

Step 10 - Paste the content of the .pem file(PEM Chain) into a file named 'ca-certs.pem'
touch ca-certs.pem
nano ca-certs.pem
Paste text inside and then save.

Step 11 - You have to merge all the .crt files in the 'CRT Package' zip into a single .crt file named 'server.crt'

