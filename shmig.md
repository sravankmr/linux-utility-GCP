
## Login to postgressql
```
sudo -u postgres psql
sudo -u ubuntu psql
```

## Create empty sql file
```
./migrations/shmig -t postgresql -d ubuntu create mytable
```

## Run migrate command
```
./migrations/shmig -t postgresql -d ubuntu migrate
```

## List commands
```
\du - users
\dn - schema
\l  - list all database
\dt - list tables
```
## entrypoint.sh

```
#!/usr/bin/env bash

echo "DB_Schema =" $1
file="test.txt"
echo "$1" > $file

set -e
WORKDIR="/home/ubuntu"

echo "workdir"

cd "$WORKDIR/testdb/db/"
#sudo dos2unix *.sql > /dev/null 2>&1
echo "test sql"
sudo chmod +x migrations/entrypoint.sh
sudo chmod +x migrations/shmig
sudo chmod +x migrations/shmig.conf

export DB_SCHEMA=$1

echo "Schema env = "$DB_SCHEMA
./migrations/shmig -t postgresql -d ubuntu migrate
```

## Setting environment variable
```
\getenv test_schema DB_SCHEMA
\echo xcreating
\echo :test_schema
\echo creating

-- all Optimizer tables except shmig_version need to reside in the optimizer_schema

CREATE SCHEMA IF NOT EXISTS :test_schema;
```
