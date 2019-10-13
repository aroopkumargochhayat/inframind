FROM mysql as builder

RUN ["sed", "-i", "s/exec \"$@\"/echo \"not running $@\"/", "/usr/local/bin/docker-entrypoint.sh"]

ENV MYSQL_ROOT_PASSWORD=password
ENV MYSQL_DATABASE=SALESMANAGER

COPY dump.sql /docker-entrypoint-initdb.d/

RUN ["/usr/local/bin/docker-entrypoint.sh", "mysqld", "--datadir", "/initialized-db"]

FROM mysql

COPY --from=builder /initialized-db /var/lib/mysql
EXPOSE 3306
