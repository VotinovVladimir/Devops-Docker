FROM nginx

COPY hello.c /app/hello.c
COPY nginx.conf /etc/nginx/nginx.conf

RUN apt update && apt install -y \
    spawn-fcgi \
    libfcgi-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/* \
    && gcc -o /hello /app/hello.c -lfcgi 

CMD sh -c "/hello & exec nginx -g 'daemon off;'"