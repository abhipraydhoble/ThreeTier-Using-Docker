FROM mariadb

LABEL database = "studentapp"

ENV MARIADB_ROOT_PASSWORD=1234

COPY student-rds.sql /docker-entrypoint-initdb.d/

EXPOSE 3306

CMD ["mariadbd"]
