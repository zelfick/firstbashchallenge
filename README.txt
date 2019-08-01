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

#use a run command to install the packages needed for nginx can be simpler this  is just an ilustration on how to use env variables
#but you can not use if you don't want to
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

CMD ["nginx", "-g", "daemon off;"]
# required: run this command when container is launched
# only one CMD allowed, so if there are multiple, last one wins

# remember after the build to run your container so we can see the results



#Check this sites for help and information on how to use nginx
https://hub.docker.com/_/nginx/
#Here look for the guide on how to use the command.
http://nginx.org/en/docs/beginners_guide.html#conf_structure
#Here help to install it
https://www.cyberciti.biz/faq/howto-install-setup-nginx-on-debian-linux-9/
