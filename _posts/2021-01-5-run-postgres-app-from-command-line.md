---
layout: post
title: Run postgres.app from the command line
---

I recently started using [tmux](https://formulae.brew.sh/formula/tmux) on my macbook which lets me setup workspaces for different projects. One of these projects requires postgres to be running. I use the fantastic [postgres.app](https://postgresapp.com/) for mac which takes away all the faff of installing postgres yourself. They have a set of instructions for [installing the command line tools](https://postgresapp.com/documentation/cli-tools.html) which lets you run the `postgres` command. Unfortunately simply running postgres is not enough. Here's the steps I took:

- Follow the [instructions to install the postgres CLI tools](https://postgresapp.com/documentation/cli-tools.html)
- Open postgres.app. Click `Server settings` and copy the path to the *data directory*
- Set an enviroment variable `PGDATA` pointing to that directory (e.g. `export PGDATA="/Users/YOUR_USER/Library/Application Support/Postgres/var-12/"`)
- Run the command `postgres`

You should now have a postgres server running from the command-line with output similar to:

```
2021-01-05 16:09:42.445 CET [11710] LOG:  starting PostgreSQL 12.5 on x86_64-apple-darwin16.7.0, compiled by Apple LLVM version 8.1.0 (clang-802.0.42), 64-bit
2021-01-05 16:09:42.451 CET [11710] LOG:  listening on IPv4 address "127.0.0.1", port 5432
2021-01-05 16:09:42.451 CET [11710] LOG:  listening on IPv6 address "::1", port 5432
2021-01-05 16:09:42.452 CET [11710] LOG:  listening on Unix socket "/tmp/.s.PGSQL.5432"
2021-01-05 16:09:42.545 CET [11710] LOG:  database system is ready to accept connections
```
