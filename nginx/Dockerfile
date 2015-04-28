
FROM ubuntu:14.10

MAINTAINER Mirco Zeiss <mirco.zeiss@gmail.com>

# update repository
RUN \
  apt-get update && \
  apt-get install -y \
  nginx

# create directory for page
RUN mkdir -p /var/www

# copy index.html to new /var/www/ directory
ADD index.html /var/www/index.html

# copy nginx file to nginx available sites
ADD index /etc/nginx/sites-available/index

# remove default symlink and create symlink in sites enabled
WORKDIR /etc/nginx/sites-enabled
RUN rm default
RUN ln -s /etc/nginx/sites-available/index index

# restart nginx
RUN service nginx reload

# expose port
EXPOSE 80 443

# set default command to execute when creating new container
# tell nginx to run in the foreground as it is the only process running
# in this container
# usually it runs in the background
CMD ["nginx", "-g", "daemon off;"]
