---
categories: Linux
tags:php nginx
---

1. 安装php-fpm，php-mysql

   `apt install php-fpm php-mysql`

2. 安装nginx

   `apt Install nginx`

3. 配置nginx

   编辑`/etc/nginx/sites-available/default`配置文件，修改默认读取 `index.html index.htm`为`index.html index.htm index.php`，添加静态文件配置，放开php解析的注释；

   ```xml
   server {
   	listen 3780 default_server;
   	listen [::]:3780 default_server;
   
   	root /var/www/html;
   
   	# Add index.php to the list if you are using PHP
   	index index.html index.htm index.nginx-debian.html index.php;
   
   	server_name _;
   
   	location / {
   		# First attempt to serve request as file, then
   		# as directory, then fall back to displaying a 404.
   		try_files $uri $uri/ =404;
                      root   /var/www/html;
                      index  index.html index.htm index.php;
   	}
   
       #静态文件，nginx自己处理
   	location ~ .*\.(html|htm|gif|jpg|jpeg|bmp|png|ico|txt|js|css|swf|ttf|woff2|eot|woff|json|exe|mp3)$ {   
   	        #路径  
   	        root /var/www/html;  
   	        #过期1天，静态文件不怎么更新，过期可以设大一点，如果频繁更新，则可以设置得小一点。  
   	        expires      1d;   
   	}  
   
   	# pass PHP scripts to FastCGI server
   	
   	location ~ \.php$ {
   		include snippets/fastcgi-php.conf;
   	
   		# With php-fpm (or other unix sockets):
   		fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
   		# With php-cgi (or other tcp sockets):
   		# fastcgi_pass 127.0.0.1:9000;
   	}
   }
   ```

   

   注意确认`fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;`中`php7.2-fpm.sock`路径or文件名是否正确； 

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

   