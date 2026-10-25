<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment- -->

# How to use OPSWAT ICAP NGINX Module in Docker environment?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP Server releases deployed on Windows and Linux systems.

### [Preparation](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#preparation)

A Linux machine with Docker installed. You can install Docker with this command

HtmlCopycurl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh

Create a folder on your machine and cd into it

### [Download the OPSWAT ICAP NGINX Module](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#download-the-opswat-icap-nginx-module)

Now, go to [my.opswat.com](http://my.opswat.com/) and look for the NGINX module library file in the ICAP download page. Choose the Debian version, then download the file using WGET/CURL

Info:

Remember the NGINX version of the file you downloaded. You will need this for the next step. Here, the version is **1.22.1**

### [Define NGINX version](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#define-nginx-version)

Run this in your Linux machine. Replace <YOUR_VERSION_HERE> with the NGINX version you obtained from the above step.

HtmlCopyexport NGINX_BASE_VERSION=<YOUR_VERSION_HERE>
### [Create the Dockerfile](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#create-the-dockerfile)

In the same folder, create a file name **Dockerfile**. Then edit the file using nano/vim.

HtmlCopyARG BASE_IMAGE_TAG=1.22.1
FROM nginx:${BASE_IMAGE_TAG}
ARG BASE_IMAGE_TAG
RUN service nginx stop
COPY nginx-module-ometascan_${BASE_IMAGE_TAG}+1.4.0-1~buster_amd64.deb nginx-module-ometascan_${BASE_IMAGE_TAG}+1.4.0-1~buster_amd64.deb
# COPY nginx.conf /etc/nginx/nginx.conf.template
# COPY entrypoint.sh entrypoint.sh
RUN dpkg -i nginx-module-ometascan_${BASE_IMAGE_TAG}+1.4.0-1~buster_amd64.deb
EXPOSE 80
RUN service nginx start

Save the file. Now you have the Dockerfile to build the image.

### [Build the image](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#build-the-image)

Use the below command. Remember to define the $NGINX_BASE_VERSION environment variable before you run.

HtmlCopydocker build -t nginx-icap-module:$NGINX_BASE_VERSION --build-arg="BASE_IMAGE_TAG=$NGINX_BASE_VERSION" .

Docker will begin to build the image

After the build has completed, verify that the image has been built with `docker image list`. You should see your image with the tag is your NGINX version.

### [Using the Image](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-opswat-icap-nginx-module-in-docker-environment-#using-the-image)

Stay in the current folder or create an another folder you desired. This is where we will put our config files for NGINX. You will need: `nginx.conf` file and your `SSL certificate` (optional).

Sample nginx.conf file for ICAP scanning:

**nginx.conf with ICAP:**

HtmlCopyload_module modules/ngx_http_ometascan_module.so;
events {
worker_connections 4096;
}
http {
client_max_body_size 1000M;
server {
listen 80;
server_name localhost;
location ^~ / {
ometascan_pass http://10.10.0.5:8043;
ometascan_methods GET POST HEAD OPTIONS CONNECT PUT;
proxy_pass http://10.40.162.87:8787/upload;
# ometascan_pre_cache_size 9223372036854775807;
# ometascan_pre_cache off;
# ometascan_read_timeout 60s;
# ometascan_connect_timeout 60s;
# ometascan_send_timeout 60s;
}
}
}

**nginx.conf with ICAPS:**

HtmlCopyload_module modules/ngx_http_ometascan_module.so;
events {
worker_connections 4096;
}
http {
client_max_body_size 1000M;
server {
listen 80;
server_name localhost;
location ^~ / {
ometascan_pass http://10.10.0.5:8043;
#ometascan_ssl_trusted_certificate /etc/nginx/https.crt;
ometascan_methods GET POST HEAD OPTIONS CONNECT PUT;
proxy_pass http://10.40.162.87:8787/upload;
# ometascan_ssl_server_name off;
# ometascan_ssl_name $proxy_host;
# ometascan_ssl_ciphers DEFAULT;
# ometascan_ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3;
# ometascan_ssl_verify_depth 1;
# ometascan_ssl_verify off;
# ometascan_pre_cache_size 9223372036854775807;
# ometascan_pre_cache off;
# ometascan_read_timeout 60s;
# ometascan_connect_timeout 60s;
# ometascan_send_timeout 60s;
}
}
}

Replace:

`ometascan_pass` with your MD ICAP server URL.

`ometascan_ssl_trusted_certificate` you can leave this as is or comment it out if you are not using ICAPS.

`proxy_pass` upstream server URL

You can also modify other options by removing the `#` comments and edit.

Your folder should contains this two files before running the below command

Start the container:

**With SSL Certificate (ICAPS):**

DockerCopydocker run -d -p 8080:80 -v "$PWD/nginx.conf:/etc/nginx/nginx.conf" \
-v "$PWD/<YOUR_CRT_FILE_NAME>:/etc/nginx/https.crt" \
nginx-icap-module:$NGINX_BASE_VERSIONInfo:

Replace <YOUR_CRT_FILE_NAME> with your ICAP SSL certificate file name. In this example, the name is **my_icap_crt.crt**

**Without SSL Certificate (ICAP):**

DockerCopydocker run -d -p 8080:80 -v "$PWD/nginx.conf:/etc/nginx/nginx.conf" \
nginx-icap-module:$NGINX_BASE_VERSIONSupport:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
