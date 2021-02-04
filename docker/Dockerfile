FROM ubuntu:18.04

RUN set -x \
    && apt-get -qq update \
    && apt-get install -yq --no-install-recommends pgbouncer=1.8.1-1build1 \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/log/postgresql
RUN chmod -R 755 /var/log/postgresql
RUN chown -R postgres:postgres /var/log/postgresql

# Set Azure cert for TLS
RUN wget https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt
RUN openssl x509 -inform DER -in BaltimoreCyberTrustRoot.crt -text -out /etc/azure/root.crt

ENV PG_CONFIG /etc/pgbouncer/pgbouncer.ini
ENV PG_USER postgres

USER postgres
ENTRYPOINT pgbouncer -u $PG_USER $PG_CONFIG
