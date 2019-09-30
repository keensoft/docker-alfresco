FROM nginx:stable-alpine

RUN rm -f /etc/nginx/conf.d/*

COPY nginx.conf /etc/nginx/conf.d/alfresco.conf
COPY nginx.htpasswd /etc/nginx/conf.d/nginx.htpasswd


