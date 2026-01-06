veic_web with symfony
===
Veic Corporation is web site

```
Copyright (c) 2022-2024 Harbin TDTC Technology Development Co., Ltd.

Apache License Version 2.0
```

- PHP8.1+
- IDE    
VS Code(Symfony Extension Pack, TWIG pack-Bajdzis)
- symfony    
[![Current Version: v6.4](https://github.com/tdtc-hrb/veic-web_sf6/blob/main/docs/sf_version.svg)](https://symfony.com/releases)

## the project structure

your-project/    
├─ assets/    
├─ bin/    
│  └─ console    
├─ config/    
├─ public/    
│  └─ index.php    
├─ src/    
│  └─ ...    
├─ templates/    
├─ migrations/    
├─ translations/    
└─ .env    
└─ composer.json    
└─ composer.lock    
└─ package.json    
└─ symfony.lock    
└─ webpack.config.js    
└─ yarn.lock



## install yarn
```bash
sudo npm install --global yarn
```
### using V2
- set proxy
```bash
sudo yarn config set proxy http://<ip:port>
sudo yarn config set https-proxy http://<ip:port>
```
- switch version
```bash
sudo yarn set version berry
```

### yarn update
V1:
```
yarn upgrade
```
V2:
```
yarn up
```

## launch
Before upgrading, set the proxy first：
```bash
cd veic-web_sf
composer update
yarn up
```

### offline
same version:    
copy ".yarn" and "vendor" to the root directory.

### ui(css+js)
```bash
yarn encore dev --watch
```

### run
[start server](https://github.com/symfony-cli/symfony-cli/releases):
```bash
symfony server:start
```
- [abuot](http://127.0.0.1:8000/en-us/about)
![hello](https://github.com/tdtc-hrb/veic-web_sf6/blob/main/public/img/hello_screenshot.png)
