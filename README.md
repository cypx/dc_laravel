# docker-compose config for Laravel

## requirements (on Ubuntu 16.04)

### git, docker and docker-compose

```
sudo apt update
sudo apt install apt-transport-https ca-certificates
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee -a  /etc/apt/sources.list.d/docker.list
curl -L https://github.com/docker/compose/releases/download/1.7.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

### DNS

To resolve locally all fqdn, edit your /etc/hosts and add
```
127.0.0.1 www.laravel.test
127.0.0.1 mail.laravel.test
127.0.0.1 pma.laravel.test
```

Or better, use dnsmaq to fully redirect .test domain extension
```
sudo apt install dnsmasq
echo "address=/.test/127.0.0.1" | sudo tee -a /etc/dnsmasq.conf
```

### reverse proxy

Use a docker container has reverse proxy
```
docker run --restart="always" --name="nginx-proxy" -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro jwilder/nginx-proxy
```
## usage

To init the project
```
git clone XXXXXXX/dc_laravel
cd dc_laravel
docker-compose up -d
rm -rf ./htdocs
docker-compose run composer create-project laravel/laravel ./htdocs 4.2 --prefer-dist
sudo chmod -R ugo+w htdocs/app/storage
```

To start containers
```
cd <PROJECT_PATH>
docker-compose up -d
```

To stop containers
```
cd <PROJECT_PATH>
docker-compose down
```

Infos:

* Laravel frontend: http://www.laravel.test
* phpMyAdmin: http://pma.laravel.test
* MailHog (catch all mail from project): http://mail.laravel.test
* mysql host: db
* mysql user: laravel
* mysql password: password
