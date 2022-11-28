FROM nginxinc/nginx-unprivileged@sha256:a581d0821f38e5b211a5397d3f204eee2e2f9ac89335ffb5002a488603b1b69b as base
# image tag nginxinc/nginx-unprivileged:1.21.6-alpine-perl

USER root
RUN mkdir /usr/share/nginx/html/sites
RUN chown -R nginx:nginx /usr/share/nginx/html
COPY --chown=nginx:nginx src/ /usr/share/nginx/html/

FROM base as build-test
USER root
RUN apk --no-cache add npm
USER nginx
WORKDIR /usr/share/nginx/html/
EXPOSE 8080
CMD ["nginx","-g","daemon off;"]

FROM base as build-deploy
USER nginx
WORKDIR /usr/share/nginx/html/
EXPOSE 8080
CMD ["nginx","-g","daemon off;"]
