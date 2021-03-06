# Docker Compose for TICK stack 
# With Nginx proxy and authentication for Chronograf

Docker containers: `Nginx, Telegraf, InfluxDB, Chronograf, Kapacitor`

# Dependencies
Requires `htpasswd` to add authentication to chronograf and `make`

Arch:
```bash
yay -S apache-tools 
sudo pacman -S make
```

Debian:
```bash
sudo apt-get install apache2-utils make
```

# Configuration

#### Generate an up-to-date sample telegraf config
```bash
bash scripts/ssh-or-conf_gen.sh telegraf "telegraf config" > /tmp/telegraf.conf
```

#### Generate an up-to-date sample telegraf config
```bash
bash scripts/ssh-or-conf_gen.sh influxdb "influxd config" > /tmp/influxd.conf
```

#### Generate an up-to-date sample kapacitor config
```bash
bash scripts/ssh-or-conf_gen.sh kapacitor "kapacitord config" > /tmp/kapacitord.conf
```

# Quickstart

```bash
git clone https://gitlab.com/qrsna/tick-stack-docker.git && cd tick-stack-docker
cp .env.default .env && vim .env # edit your variables
make
docker-compose up 
```

## Start telegraf
```bash
docker-compose up -f telegraf.yml
```

### Add an additional htpasswd user
```bash
sudo htpasswd volumes/config/htpasswd/chronograf.krsna.co.za another_user
```

### Create temporary container and SSH into container
```bash
bash scripts/ssh-or-conf_gen.sh kapacitor 
bash scripts/ssh-or-conf_gen.sh influxdb
bash scripts/ssh-or-conf_gen.sh chronograf
bash scripts/ssh-or-conf_gen.sh telegraf
```

### Destroy environment
Delete configs and docker volumes
```bash
make destroy
```

## TODO
- Add SSL

  `https://tevinjeffrey.me/how-to-setup-nginx-proxy-and-lets-encrypt-with-docker/`

  `https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion`

----
Most High Bless ॐ 
हरे कृष्ण हरे कृष्ण कृष्ण कृष्ण हरे हरे हरे राम हरे राम राम राम हरे हरे
