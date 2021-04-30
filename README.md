# Docker LAMP Development

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/andreipa/docker-lamp?label=Version)

![banner-lamp-logo](https://user-images.githubusercontent.com/7590574/112154551-4ca6d500-8bdc-11eb-842a-8943b43807b1.png)

A very basic LAMP stack environment for development. It was built using Docker Compose 3.9 and consists following:

- [PHP 8](https://hub.docker.com/_/php)
- [Apache 2.4](https://hub.docker.com/_/httpd)
- [MySQL 8](https://hub.docker.com/_/mysql)
- [MailHog 1.0.1](https://github.com/mailhog/MailHog)
- [phpMyAdmin 5](https://hub.docker.com/_/phpmyadmin)

## Getting Started

Clone this repository on your local computer and run the docker compose on your terminal.

```shell
docker-compose up -d --build
```

### Prerequisites

In order to run this container you'll need docker installed.

- [Windows](https://docs.docker.com/windows/started)
- [OS X](https://docs.docker.com/mac/started/)
- [Linux](https://docs.docker.com/linux/started/)

## Usage

### Installation

Clone this repository on your local computer and run the docker compose on your terminal.

```shell
git clone https://github.com/andreipa/docker-lamp
cd docker-lamp/
git fetch --all
docker-compose up -d --build
```

You can access your LAMP stack via `http://localhost` or `http://app.local`

> You need to modify your hosts file. [How to Edit the Hosts File?](https://gist.github.com/andreipa/47ce0679d1905883c18b9ac3a1a9a8f6)

### Configuration

This package comes with default configuration options. You can modify them by editing the Dockerfile inside the folders `./bin/mysql` and `./bin/webserver`. The variables are contained in the default **Environment file** `./.env` - you _must_ run `doocker-compose` command from the project root, otherwise the file is ignored.

#### Environment Variables

- `DOCUMENT_ROOT` - The document root for the Apache server. The default value is `./www`. All your sites will go here and will be synced automatically. You can create subfolders for each project.
- `VHOSTS_DIR` - The virtual hosts. The default value for this is `./config/vhosts.` You can place your virtual hosts conf files here.
- `APACHE_LOG_DIR` - This will be used to store Apache logs. The default value for this is `./logs/apache2`.
- `MYSQL_LOG_DIR` - This will be used to store Apache logs. The default value for this is `./logs/mysql`.
- `MYSQL_DATA_DIR` - This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.
- `PHP_INI` - The file php.ini with custom configuration. You can customise as you need and saving it at `./config/php/`.

#### Database Environment Variables

- `DB_ROOT_PASSWORD` - The root password of the MySQL. Default `root`.
- `DB_USER` - Optional user name with superuser permissions. Default `user`.
- `DB_PASSWORD` - Optional password for the user. Default `root`.

## Containers

### Apache

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

- rewrite
- headers

> If you want to enable more modules. Just update `./bin/webserver/Dockerfile`.

#### Connect via bash

You can connect to web server using `docker exec` command to perform various operation on it. Use below command to login to container via bash.

```shell
docker exec -it php8-apache bash
```

### PHP

The installed version of PHP is 8.

#### Extensions

By default following extensions are installed.

- bcmath
- calendar
- curl
- exif
- gd
- gettext
- intl
- json
- imagick-3.4.4
- mysqli
- pdo_mysql
- pdo_sqlite
- xdebug-3.0.4
- xml
- zip

> If you want to install more extension, just update `./bin/webserver/Dockerfile`.

### MySQL

The installed version of MySQL is 8.

### phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

```
http://localhost:8080
username: root
password: root
```

### Mail

MailHog is an email-testing tool with a fake SMTP server underneath. It encapsulates the SMTP protocol with extensions and does not require specific backend implementations. MailHog runs a super simple SMTP server that hogs outgoing emails sent to it. You can see the hogged emails in a web interface. MailHog is a portable tool built with Golang. You can run it on any supported platform, and Golang binary files allow you to set it up very simple – just copy and launch.

```shell
http://localhost:8025
```

## Built With

- [Debian](https://www.debian.org/)
- [Composer](https://getcomposer.org/)
- [Browscap](https://browscap.org/)
- [MailHog](https://github.com/mailhog/MailHog)
- [phpMyAdmin](https://www.phpmyadmin.net/)

## Using this LAMP stack to host a website

The LAMP stack comes with a simple `index.php` file in the default `DOCUMENT_ROOT`. You can checkout another project containing your website into `./www` to replace the default, or you can checkout to a different directory or subdirectory - just update `DOCUMENT_ROOT` in `.env` file appropriately and rebuild with `docker-compose`.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the
[tags on this repository](https://github.com/andreipa/docker-lamp/tags).

## Author

- **Andrei Andrade** - _Initial work_ - [andreipa](https://github.com/andreipa/docker-lamp)
- **Trung Nguyen** - [t12ung](https://github.com/t12ung)
- **Andre Pretto** - [prettoandre](https://github.com/prettoandre)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details.

## Acknowledgments

- Many thanks to [Docker](https://www.docker.com/)
