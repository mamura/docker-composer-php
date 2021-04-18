FROM nginx:1.19.3-alpine

WORKDIR /var/www/html

RUN apk add nano
RUN apk add sed

ARG APP_NAME
ADD app.conf /etc/nginx/conf.d/${APP_NAME}.conf
RUN chmod +x /etc/nginx/conf.d/${APP_NAME}.conf
RUN sed -i "s|APP_NAME|${APP_NAME}|" /etc/nginx/conf.d/${APP_NAME}.conf

EXPOSE 80