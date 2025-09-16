---
id: Purge-and-Reinstall-PostgreSQL
aliases: []
tags:
  - postgresql
---

If it's just a simple "purge" on a package with `apt-get`, there's still some traces left behind that reinstalling the PostgreSQL itself is not working.

After the basic command lines:

```bash
apt-get purge postgresql
apt-get install postgresql
```

This'll be the output from terminal:

```bash
Setting up postgresql-8.4 (8.4.3-0ubuntu9.10.1) ...
Configuring already existing cluster (configuration: /etc/postgresql/8.4/main, data: /var/lib/postgresql/8.4/main, owner: 108:112)
Error: move_conffile: required configuration file     /var/lib/postgresql/8.4/main/postgresql.conf does not exist
Error: could not create default cluster. Please create it manually with

  pg_createcluster 8.4 main --start

or a similar command (see 'man pg_createcluster').
update-alternatives: using /usr/share/postgresql/8.4/man/man1/postmaster.1.gz to provide /usr/share/man/man1/postmaster.1.gz (postmaster.1.gz) in auto mode.

Setting up postgresql (8.4.3-0ubuntu9.10.1) ...
```

`/etc/postgresql` have no files at all
`/etc/postgresql-common` has `pg_upgradecluster.d` directory with `root.crt` and `user_clusters` files.
`/etc/passwd` has a `postgres` user and the `purge` script didn't touch this file.

But if we run `pg_createcluster...` command, `psql` will complain that `/var/lib/postgresql/{version}/main/postgresql.conf does not exist`.

**Approach to the problem:**

_If the PostgreSQL installation is not damaged at all, you can drop the unwanted servers ("clusters") using `pg_dropcluster`_.

Before fully purging the PostgreSQL, make sure that the PostgreSQL isn't running at all. You can test by running `ps -C postgres`, this should show a no result output.

Then run this command line:

```bash
apt-get --purge remove postgresql\*
```

To remove everything from the system. Because only `--purge` isn't enough.

Once all PostgreSQL packages have been removed, run:

```bash
rm -r /etc/postgresql/
rm -r /etc/postgresql-common/
rm -r /var/lib/postgresql/
userdel -r postgres
groupdel postgres
```

After deleting and checking the directories and files, you should now be able to do:

```bash
apt-get install postgresql
```

For more specificity:

```bash
apt-get install postgresql-8.4 postgresql-contrib-8.4 postgresql-doc-8.4
```

_Change the version based on your preference._

**Related Notes:**

- [John Mee - Purge and Reinstall PostgreSQL in Ubuntu](https://johnmee.com/how-to-reinstall-postgresql-on-ubuntu)
- [StackOverflow - Thoroughly purge and install PostgreSQL in Ubuntu](https://stackoverflow.com/questions/2748607/how-to-thoroughly-purge-and-reinstall-postgresql-on-ubuntu)
- [[PostgreSQL Administration - Table of Contents]]
