FROM httpd:2.4-alpine

COPY ./vhosts /usr/local/apache2/conf/vhosts

RUN \
  sed -i '/LoadModule expires_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_fcgi_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule ssl_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule http2_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  { \
    echo ''; \
    echo '# customize'; \
    echo '<Directory "/var/www/html">'; \
    echo '    Options FollowSymLinks'; \
    echo '    AllowOverride All'; \
    echo '    Require all granted'; \
    echo ''; \
    echo '    DirectoryIndex disabled'; \
    echo '    DirectoryIndex index.php index.html'; \
    echo '</Directory>'; \
    echo 'Include conf/vhosts/*.conf'; \
  } >> /usr/local/apache2/conf/httpd.conf
