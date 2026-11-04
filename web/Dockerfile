
# web: nginx sirviendo la página y reenviando /api/ al backend.
# Imagen unprivileged: ejecuta Nginx como usuario sin privilegios.
FROM nginxinc/nginx-unprivileged:1.29-alpine

# Actualizar los paquetes del sistema para incorporar parches de seguridad.
USER root
RUN apk upgrade --no-cache

# Restaurar el usuario sin privilegios.
USER 101

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY public/ /usr/share/nginx/html/

EXPOSE 8080
