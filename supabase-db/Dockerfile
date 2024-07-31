# Use the official PostgreSQL base image as the parent image
FROM supabase/postgres:15.1.0.103

# Copy your custom SSL certificate and key to the appropriate location
COPY certificates/server.crt /var/lib/postgresql/server.crt
COPY certificates/server.key /var/lib/postgresql/server.key

# Copy your custom PostgreSQL config file
COPY postgresql.conf /etc/postgresql/postgresql.conf
# COPY logging.conf /etc/postgresql/logging.conf
# COPY pg_hba.conf /etc/postgresql/pg_hba.conf

# Set the correct permissions on the certificate and key files
RUN chown postgres:postgres /var/lib/postgresql/server.crt /var/lib/postgresql/server.key
RUN chmod 600 /var/lib/postgresql/server.crt /var/lib/postgresql/server.key

# Copy your SQL migration and scripts to the image
COPY supabase/realtime.sql /docker-entrypoint-initdb.d/migrations/99-realtime.sql
COPY supabase/webhooks.sql /docker-entrypoint-initdb.d/init-scripts/98-webhooks.sql
COPY supabase/roles.sql /docker-entrypoint-initdb.d/init-scripts/99-roles.sql

CMD ["postgres", "-c", "config_file=/etc/postgresql/postgresql.conf", "-c", "log_min_messages=fatal"]
