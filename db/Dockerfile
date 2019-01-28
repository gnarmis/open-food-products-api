FROM library/postgres:10

RUN apt-get update && apt-get install -y \
  unzip \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY create_readonly_role.sql .

COPY food_products.sql.zip .

RUN unzip food_products.sql.zip

RUN cat create_readonly_role.sql food_products.sql > init.sql

# a file named "init.sql" placed in /docker-entrypoint-initdb.d/ will
# be automatically run after basic boostrapping of the database, so
# we use this to our advantage to prepare and seed the database
# automatically on first launch
RUN cp init.sql /docker-entrypoint-initdb.d/
