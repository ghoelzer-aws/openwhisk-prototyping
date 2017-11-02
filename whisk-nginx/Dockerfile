# Update image to allow to run as Non-Root User on OpenShift
FROM projectodd/whisk_nginx:openshift-latest

#RUN chgrp -R 0 /etc/nginx && \
#    chmod -R g=u /etc/nginx

RUN chgrp -R 0 /etc/nginx
RUN chmod -R g+rw /etc/nginx
RUN find /etc/nginx -type d -exec chmod g+x {} +

ADD nginx.conf /etc/nginx/nginx.conf
