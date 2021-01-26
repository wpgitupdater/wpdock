# wpdock
A simple WordPress development environment using Docker

## Install

Download and place the `wpdock` executable in your path, the following command places `wpdock` into the `$HOME/bin` folder:

```bash
curl https://raw.githubusercontent.com/wpgitupdater/wpdock/main/wpdock -o $HOME/bin/wpdock && chmod +x $HOME/bin/wpdock
```

## Commands

### init

Creates '.env' file in the current folder when not present.\nAdds 'db.sql' and '.wpdock' to '.gitignore', and '.htaccess' rules to prevent dot files being accessed.

```bash
wpdock init
```

### file

Displays the contents of the generated files should you prefer a manual installation.

```bash
wpdock file .env
```

### up|start

Runs `docker-compose up -d` and applies wpdock specific configurations. When `--https` is provided a caddy server is used to proxy requests from your `WORDPRESS_SITE_HOST` env to the wordpress container.

```bash
wpdock up
wpdock start --https
```

### stop

Runs `docker-compose stop`.

```bash
wpdock stop
```

### down

Runs `docker-compose down`.

```bash
wpdock down
```

### destroy

Runs `docker-compose down -v`, destroying volumes.

```bash
wpdock down
```

### exec

Proxies commands to the named container using `docker-compose exec name ...`.

For example: `wpdock exec wordpress sh` opens a session on the wordpress container.

```bash
wpdock exec [container] [command]
```

### run

Proxies commands to the named container using `docker-compose run name ...`.

For example: `wpdock run wordpress ls -al` runs `ls -al` on the wordpress container.

```bash
wpdock run [container] [command]
```

### logs

Tails container logs. When no name is provided output contains all running containers.

```bash
wpdock logs [container]
```

### compose

Proxies all commands to `docker-compose`.

```bash
wpdock compose [...args]
```

### dump

Uses the root db user to dump the database using the WordPress cli `wp db export` command. Creates a `dump.sql` file in the project root.

```bash
wpdock dump
```

### import

Imports a created `dump.sql` using the WordPress cli `wp db import` command. `dump.sql` file must be in the project root.

```bash
wpdock import
```

### [...args]

Proxies commands to the WordPress cli container `docker-compose run --rm cli wp ...`.

For example: `wpdock user list` >> `wpcli user list`

```bash
wpdock user list
wpdock search-replace 'http://' 'https://'
wpdock cli info
```
