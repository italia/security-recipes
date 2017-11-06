FROM nginx:1.13.5

RUN \
  echo '#!/bin/sh' > /usr/local/bin/entrypoint.sh \
  && echo 'sleep 30;' >> /usr/local/bin/entrypoint.sh \
  && echo 'exec "$@"' >> /usr/local/bin/entrypoint.sh \
  && chmod +x /usr/local/bin/entrypoint.sh

RUN \
  echo '' > /etc/nginx/conf.d/default.conf \

  && echo 'upstream django {' >> /etc/nginx/conf.d/default.conf \
  && echo 'server stn_django-1:8000;' >> /etc/nginx/conf.d/default.conf \
  && echo '}' >> /etc/nginx/conf.d/default.conf \

  && echo 'server {' >> /etc/nginx/conf.d/default.conf \

  && echo 'listen 80;' >> /etc/nginx/conf.d/default.conf \
  && echo 'server_name _;' >> /etc/nginx/conf.d/default.conf \

  && echo 'keepalive_timeout 5;' >> /etc/nginx/conf.d/default.conf \

  && echo 'root /usr/share/nginx/html/securethenews;' >> /etc/nginx/conf.d/default.conf \

  && echo 'location /static/main.css {' >> /etc/nginx/conf.d/default.conf \
  && echo '  alias /usr/share/nginx/html/client/build/main.css;' >> /etc/nginx/conf.d/default.conf \
  && echo '}' >> /etc/nginx/conf.d/default.conf \

  && echo 'location /static/build.js {' >> /etc/nginx/conf.d/default.conf \
  && echo '  alias /usr/share/nginx/html/client/build/build.js;' >> /etc/nginx/conf.d/default.conf \
  && echo '}' >> /etc/nginx/conf.d/default.conf \

  && echo 'location / {' >> /etc/nginx/conf.d/default.conf \
  && echo '  try_files $uri @proxy_to_app;' >> /etc/nginx/conf.d/default.conf \
  && echo '}' >> /etc/nginx/conf.d/default.conf \

  && echo 'location @proxy_to_app {' >> /etc/nginx/conf.d/default.conf \
  && echo '  proxy_set_header Host $http_host;' >> /etc/nginx/conf.d/default.conf \
  && echo '  proxy_redirect off;' >> /etc/nginx/conf.d/default.conf \
  && echo '  proxy_pass http://django;' >> /etc/nginx/conf.d/default.conf \
  && echo '}' >> /etc/nginx/conf.d/default.conf \

  && echo '}' >> /etc/nginx/conf.d/default.conf

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
