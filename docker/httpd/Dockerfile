FROM httpd:2.4

COPY conf/project.conf /usr/local/apache2/conf/extra/100-project-vhost.conf

RUN echo "\nLoadModule proxy_module modules/mod_proxy.so" >> /usr/local/apache2/conf/httpd.conf
RUN echo "\nLoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so" >> /usr/local/apache2/conf/httpd.conf
RUN echo "\nLoadModule rewrite_module modules/mod_rewrite.so" >> /usr/local/apache2/conf/httpd.conf
RUN echo "\nIncludeOptional conf/extra/100-project-vhost.conf" >> /usr/local/apache2/conf/httpd.conf
