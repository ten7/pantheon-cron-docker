# Pantheon cron for Docker

A docker container to run the Ansible ten7.pantheon_cron role.

## Configuration

Create a configuration file as described in the [ten7.pantheon_cron](https://github.com/ten7/pantheon-cron) Ansible role.

Once created, you have three ways to provide it to the container:
* As a base64-encoded value of the `PANTHEON_CRON_CONFIG` environment variable
* As a mounted file at the location specified by the `PANTHEON_CRON_CONFIG_FILE` environment variable
* As a mounted file at `/config/pantheon-cron/pantheon-cron.yml` inside the container.

## Use with base Docker

To run the Docker image as part of a script or in cron, use the following command:

```shell
docker run --rm -v /path/to/pantheon-cron.yml:/config/pantheon-cron/pantheon-cron.yml ten7/pantheon-cron
```

Note, that if your `pantheon-cron.yml` file depends on other files (such as SSH keys) you will need to add multiple `-v` switches to mount each one.

## Docker compose

Create the following Docker Compose file.

```yaml
version: '3'
services:
  cron:
    image: ten7/pantheon-cron
    volumes:
      - /path/to/pantheon-cron.yml:/config/pantheon-cron/pantheon-cron.yml
```

Again, if your `pantheon-cron.yml` depends on other files (such as SSH keys) you will need to add additional items under `volumes` to mount them.

Once the `docker-compose.yml` file is created, you can run backups using:

```shell
docker-compose run cron
```

## License

GPL v3

## Author Information

This Docker image was created by [TEN7](https://ten7.com/).

