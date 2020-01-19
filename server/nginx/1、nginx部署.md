### 一、安装

查看进程

```
ps -ef|grep nginx
```

```
1、安装编译工具及库文件
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
2、安装pcre,让nginx支持Rewrite功能

```

##### 1、安装编译工具及库文件

```
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
```

##### 2、安装pcre,让nginx支持Rewrite功能

```
cd /usr/local/src/
wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
```

##### 3、解压 进入安装目录 编译安装 查看版本

```
tar zxvf pcre-8.35.tar.gz
cd pcre-8.35
./configure
make && make install
pcre-config --version
```

##### 4、安装nginx

```
# cd /usr/local/src/			
# wget http://nginx.org/download/nginx-1.6.2.tar.gz
# tar zxvf nginx-1.6.2.tar.gz
# cd nginx-1.6.2
# ./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
# make
# make install
# /usr/local/webserver/nginx/sbin/nginx -v	查看版本
```

##### 5、更改配置

```

user  zhang;
worker_processes  1;

error_log  /usr/local/webserver/nginx/logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        /usr/local/webserver/nginx/nginx.pid;


events {
    accept_mutex on;
    multi_accept on;
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    server {
        listen       8080;
        server_name  localhost;

        location / {
            root   /develop/moose-vue/dist;
    #	    root   /develop/demo/moose-vue/master/dist;
            index  index.html index.htm;
        }
	location /prod-api/ {
	    rewrite ^/prod-api/(.*)$1 break;
	    proxy_pass http://127.0.0.1:8089/;
	} 
    }


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

### 二、操作

##### 1、启动

```
/usr/local/webserver/nginx/sbin/nginx
```

##### 2、检查配置文件

```
cd sbin
#验证配置文件是否正确
./nginx -t
```

##### 3、重新启动

```
./nginx -s reload
```

### 三、配置文件

### 四、Vue + Springboot部署

##### 配置文件：

```
server {
        listen       8080;
        server_name  localhost;

        location / {
            root   /develop/moose-vue/dist;
    #       root   /develop/demo/moose-vue/master/dist;
            index  index.html index.htm;
        }
        location /prod-api/ {
            rewrite ^/prod-api/(.*)$1 break;
            proxy_pass http://127.0.0.1:8089/;
        }
    }

```

 