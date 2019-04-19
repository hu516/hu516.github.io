1. 安装php-fpm

   `apt install php-fpm`

2. 安装nginx

   `apt Install nginx`

3. 配置nginx

   编辑`/etc/nginx/sites-available/default`配置文件，修改默认读取 `index.html index.htm`为`index.html index.htm index.php`，放开php解析的注释；

   注意确认`fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;`中`php7.2-fpm.sock`路径or文件名是否正确；

   ![1555644606605](1555644606605.png)

4. 应用nginx配置

   `nginx -s reload`

5. 测试

   在`/var/www/html/`目录下创建phpinfo.php文件，写入内容
   
   ```html
<?php
       phpinfo();
   ?>
   ```
   
   访问http://ip/phpinfo.php 如果出现php安装信息，那么就成功了。
   
   