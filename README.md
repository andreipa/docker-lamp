# Docker LAMP Development v1.0.2

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A very basic LAMP stack environment for development. It was built using Docker Compose 3.7 and consists following:

* [PHP 7.3](https://hub.docker.com/_/php)
* [Apache 2.4](https://hub.docker.com/_/httpd)
* [MySQL 8.0](https://hub.docker.com/_/mysql)

## Getting Started

Clone this repository on your local computer and run the docker compose on your terminal.
```shell
docker-compose up -d --build
```

### Prerequisites

In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)

## Usage

### Installation

Clone this repository on your local computer and run the docker compose on your terminal.
```shell
git clone https://github.com/andreipa/docker-lamp
cd docker-lamp/
git fetch --all
docker-compose up -d --build
```
You can access your LAMP stack via `http://localhost`

### Configuration

This package comes with default configuration options. You can modify them by editing the Dockerfile inside the folders `./bin/mysql` and `./bin/webserver`.

#### Environment Variables

* `DOCUMENT_ROOT` - The document root for the Apache server. The default value is `./www`. All your sites will go here and will be synced automatically.
* `VHOSTS_DIR` - The virtual hosts. The default value for this is `./config/vhosts.` You can place your virtual hosts conf files here.
* `APACHE_LOG_DIR` - This will be used to store Apache logs. The default value for this is `./logs/apache2`.
* `MYSQL_LOG_DIR` - This will be used to store Apache logs. The default value for this is `./logs/mysql`.
* `MYSQL_DATA_DIR` - This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.
* `PHP_INI` - The file php.ini with custom configuration. You can customise as you need and saving it at `./config/php/`.

#### Database Environment Variables

* `DB_ROOT_PASSWORD` - The root password of the MySQL. Default `root`.
* `DB_USER` - Optional user name with superuser permissions. Default `user`.
* `DB_PASSWORD` - Optional password for the user. Default `root`.

## Containers

### Apache

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

* rewrite
* headers

> If you want to enable more modules. Just update `./bin/webserver/Dockerfile`.

#### Connect via SSH

You can connect to web server using `docker exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker exec -it 7.3.x-webserver /bin/bash
```

### PHP

The installed version of PHP is 7.3

#### Extensions

By default following extensions are installed.

* bcmath
* calendar
* curl
* exif
* gettext
* imagick-3.4.3
* mysqli
* pdo_sqlite
* xdebug-2.7.0RC1
* zip

> If you want to install more extension, just update `./bin/webserver/Dockerfile`.

## Built With

* Debian
* Composer

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the 
[tags on this repository](https://github.com/andreipa/docker-lamp/tags). 

## Author

* **Andrei Andrade** - *Initial work* - [andreipa](https://github.com/andreipa/docker-lamp)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details.

## Acknowledgments

* Many thanks to [Docker](https://www.docker.com/)