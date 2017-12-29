# MariaDB on Kontena

[MariaDB](https://mariadb.org) is a community-developed fork of the MySQL relational database management system intended to remain free under the GNU GPL.

## Install

> Prerequisites: You need to have working [Kontena](https://www.kontena.io) Platform installed. If you are new to Kontena, check [quick start guide](https://www.kontena.io/docs/quick-start).

```
$ kontena volume create --driver local --scope grid mariadb-data
$ kontena stack install kontena/mariadb
```

This will deploy MariaDB server to your grid. Other services can connect to it with `mariadb.${GRID}.kontena.local:3306` address.

**Note:** Replace `${GRID}` with your grid name.

## Administration

Access `mysql` cli via interactive exec:

```
$ kontena service exec -it --shell mariadb/server "mysql --user root --password=\$MYSQL_ROOT_PASSWORD mysql"
```