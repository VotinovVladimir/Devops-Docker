FROM alpine:3.22

COPY hello.c /app/hello.c
COPY nginx.conf /etc/nginx/nginx.conf

RUN apk add --no-cache \
    spawn-fcgi \
    fcgi-dev \
    gcc \
    libc-dev \
    && addgroup -S appuser && adduser -S appuser -G appuser \
    && gcc -o /hello /app/hello.c -lfcgi \
    && chown -R appuser:appuser /app /hello \
    && apk del gcc libc-dev

USER appuser

HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -qO- http://localhost:80/ || exit 1

CMD sh -c "/hello & exec nginx -g 'daemon off;'"
