Begin build on Symfony
====
[Installing & Setting up the Symfony Framework](https://symfony.com/doc/7.4/setup.html)

# Prepare
- Composer
- Symfony cli

## Composer
- ubuntu

add repository:
```
sudo add-apt-repository ppa:ondrej/php # Press enter when prompted.
sudo apt update
```

- [debian](https://linuxcapable.com/how-to-install-php-8-3-on-debian-linux)
```
sudo apt install extrepo -y
sudo extrepo enable sury
sudo apt update
```

### [Installing composer in Linux](https://www.transip.eu/knowledgebase/entry/3300-installing-composer-in-linux/)
In addition to the basics that come with installing PHP, 
Composer requires php-cli php-zip wget and unip.    
You install these as follows (often they will be installed already if you've installed PHP):
```
sudo apt -y install php-cli php-zip wget unzip
```
Download the composer installer with the command:
```
sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```
Finally, install Composer in the /usr/local/bin directory (so it is available to all users) with the command:
```
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```
After installation, you can remove the installer with the command:
```
sudo rm composer-setup.php
```

#### see version
```
composer --version
```

### specific php version
see versions:
```
sudo update-alternatives --config php
```
specifically choose the PHP version:
```
sudo update-alternatives --set php /usr/bin/php8.4
```

## Symfony cli
list:
```
php -m
```
- apt-transport-https
```
sudo apt autoremove
sudo apt install apt-transport-https
```
- [installation](https://symfony.com/download)
```
curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
sudo apt update
sudo apt install symfony-cli
```
- checker
```
symfony check:requirements
```

### php-xml
Q: Install and enable the SimpleXML extension.

A: [Install php-xml](https://www.php.net/manual/en/simplexml.installation.php)
```
sudo apt -y install php-xml
```

### [more lib](https://php.watch/articles/install-php82-ubuntu-debian)
```
sudo apt install php-{curl,mbstring,intl}
```

### pdo
- mysql
```
sudo apt install php8.4-pdo-mysql
```
- pgsql
```
sudo apt install php8.4-pdo-pgsql
```


# step by step
create:
```bash
composer create-project symfony/skeleton:"^7.4" veic-web_sf
```

## step 1: manage component
webapp:
```bash
cd veic-web_sf
composer require webapp
```

### [Front-end Tools: Handling CSS & JavaScript](https://symfony.com/doc/7.4/frontend.html)
- Encore
```
composer require symfony/webpack-encore-bundle
```
Webpack Encore is built with Node.js on top of Webpack.

- knp-paginator-bundle
> specific
```
composer require knplabs/knp-paginator-bundle:6.10.0
```

- Asset Mapper
> 推荐在v8.4版本, 使用 AssetMapper
remove:
```
composer remove symfony/ux-turbo
composer remove symfony/stimulus-bundle
composer remove symfony/asset-mapper
```

## step 2: manage project
- Homepage
- Product
- Company
- About
- Article
- Contact
- Sidebar

### Homepage
- Controller
```ps
php bin/console make:controller HomeController
```
- Model
```ps
php bin/console make:entity Navigation
```

```ps
php bin/console make:entity Glossary
```

### Product
- Controller
```ps
php bin/console make:controller ProductController
```

- Model
```ps
php bin/console make:entity Language
```

```ps
php bin/console make:entity Product
```

```ps
php bin/console make:entity Parameter
```

```ps
php bin/console make:entity Statu
```

```ps
php bin/console make:entity Image
```

### Company
- Controller
```ps
php bin/console make:controller CompanyController
```

- Model
```ps
php bin/console make:entity Article
```

```ps
php bin/console make:entity Type
```


### About
- Controller
```ps
php bin/console make:controller AboutController
```

- Model
```ps
php bin/console make:entity Qualification
```

### Article
- Controller
```ps
php bin/console make:controller ArticleController
```

add profile template.
```
profile.html.twig
```

### Contact
- Controller
```ps
php bin/console make:controller ContactController
```

- Model
```ps
php bin/console make:entity Contact
```

### Sidebar
- Controller
```ps
php bin/console make:controller PageController
```


## step 3: config project
更改下面的默认配置

### [route groups and prefixes](https://symfony.com/doc/7.4/routing.html#route-groups-and-prefixes)
```
cd config/routes
touch attributes.yaml
```
- attributes.yaml
```xml
controllers:
    resource: '../../src/Controller/'
    type: attribute
    prefix:
        ja: '/ja-jp'
        en: '/en-us'
        zh: '/zh-cn'
```

### routes
```
cd config
```
- routes.yaml
```
controllers:
    resource: routing.controllers
    type: attribute
```

### [support boolean type](https://stackoverflow.com/questions/9744629/doctrine2-workaround-for-mapping-mysql-bit-data-type)    
config/packages/doctrine.yaml:
```
doctrine:
    dbal:
        # ...
        mapping_types:
            bit: boolean
```
The type of support has been listed on the [official website](https://www.doctrine-project.org/projects/doctrine-dbal/en/4.2/reference/types.html#mapping-matrix)
