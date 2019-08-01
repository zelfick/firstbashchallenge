# firstbashchallenge


The idea of this example is to dockerize an application, write the dockerfile, from what we saw in docker basics, the idea is to have a nginx application or an httpd web server running with an associated index, or node.js server if you prefer which you can edit and copy during the building of the container.

As an example the dockerfile should have this sections (suggested is nginx which we use a lot in dockerbasic lecture):

# - you should use any official image of docker image to build nginx the idea is that you use this parts in your docker file:


FROM debian:stretch-slim
# if you want, you can use optional environment variables

ENV NGINX_VERSION 1.13.6-1~stretch
ENV NJS_VERSION   1.13.6.0.1.14-1~stretch

# - this app listens on port 3000, but the container should launch on port 7171
EXPOSE 3000
#  so it will respond to http://localhost:7171 on your computer

#use a run command to install the packages needed for nginx
RUN apt-get update \
	  && apt-get install --no-install-recommends --no-install-suggests -y \
						nginx=${NGINX_VERSION} \
						nginx-module-xslt=${NGINX_VERSION} \
						nginx-module-geoip=${NGINX_VERSION} \
						nginx-module-image-filter=${NGINX_VERSION} \
						nginx-module-njs=${NJS_VERSION} \
						gettext-base \


WORKDIR /usr/share/nginx/html
# change working directory to root of nginx webhost
# using WORKDIR is preferred to using 'RUN cd /some/path'


COPY index.html index.html
#use a copy sentence to put the code from your machine path index.html inside the container index.html

# rember after the build to run your container so we can see the results



#Check this sites for help and information on how to use nginx
https://hub.docker.com/_/nginx/
http://nginx.org/en/docs/beginners_guide.html#conf_structure
