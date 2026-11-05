# Postgres con el esquema del libro de visitas ya incluido.
# Los scripts SQL se ejecutan al inicializar un volumen vacio.
FROM postgres:16-alpine

COPY init/ /docker-entrypoint-initdb.d/

USER 0

RUN rm -f /usr/local/bin/su-exec \
    && apk add --no-cache su-exec=0.3-r0 \
    && sed -i 's/exec gosu postgres/exec su-exec postgres/' /usr/local/bin/docker-entrypoint.sh \
    && rm -f /usr/local/bin/gosu

# Mantener la inicializacion de PostgreSQL sin privilegios.
USER 70