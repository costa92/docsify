# [首页](/#/)
# 镜像地址
## Composer 镜像
Composer 中国全量镜像正式发布！
[https://laravel-china.org/topics/4484/composer-mirror-use-help](https://laravel-china.org/topics/4484/composer-mirror-use-help)
 
使用 Composer 镜像加速有两种选项：
    选项一：全局配置，这样所有项目都能惠及（推荐）；
    选项二：单独项目配置；
    
    选项一、全局配置（推荐）
    
```$ composer config -g repo.packagist composer https://packagist.laravel-china.org
```
    选项二、单独使用
    
    $ composer config repo.packagist composer https://packagist.laravel-china.org
    
    
安装 Composer#
    
Linux/Mac：#

    wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer
    chmod a+x /usr/local/bin/composer


###安装Laravel 版本

composer create-project laravel/laravel your-project-name --prefer-dist "5.1.*"

将5.1.*改下相应的下载版本！

