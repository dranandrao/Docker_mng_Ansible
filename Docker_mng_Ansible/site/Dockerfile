FROM ubuntu:latest
#Setting proxy.
ENV http_proxy http://172.16.19.10:80/
ENV https_proxy https://172.16.19.10:80/
RUN apt-get update

RUN apt-get install -y nginx
ADD nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /var/www/site
ADD index.html /var/www/site/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]