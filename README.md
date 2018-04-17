# Rewrite mysqldump files to work with PostgreSQL

Based on https://github.com/lanyrd/mysql-postgresql-converter

First of all, if possible you should use a better solution
than this script. `pgloader` is usually a safe bet. If
you for whatever reason can not do that, then by all means
do read on.

Also notice that this script is somewhat useless unless you
are using an ORM that can takes care of the db structure for
you (for example: Django's ORM, SqlAlchemy or maybe PonyORM),
as this script will only handle data.

You will need Python 3.5+ (any 3.x version could work, but
only 3.5+ has been tested).

The script expects to get a mysqldump file generated by:

    mysqldump \
        --user=root \
        --password=root \
        --add-drop-table=false \
        --add-locks=false \
        --compatible=postgresql \
        --default-character-set=utf8 \
        database_name

Example for the settings format for the `-s` flag follows:

    {
        "skip_tables": [
            "django_migrations"
        ],
        "map_tables": {
            "foo": "bar"
        }
    }
