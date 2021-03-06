# vue 项目部署方式和解决跨域问题反向代理配置

## 1. Nginx 方式托管和反向代理配置

### 	1.1	下载 对应的Nginx 版本 

> https://nginx.org/en/download.html

### 	1.2 	解压Nginx压缩包

<img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/nginxpath.png"/>

### 	1.3 	托管项目文件配置

> nginx 目录下的conf文件夹——>nginx.cof 文件
>
> 配置Vue 项目打包后的dist文件夹路径

​	<img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/configdistpath.png"/>

### 1.4	 反向代理配置

> 新增 location /api 节点，配置 api 访问路径

​		<img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/configapipath.png"/>

### 1.5	格式参考

```bash
    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   D:\xxx\xxx\xxx\dist;
            index  index.html index.htm;
        }

        location /api {
            proxy_pass  http://192.168.0.1:8000/api;
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
```



### 1.6	nginx 相关命令

```
在nginx.exe目录，打开命令行工具，用命令 启动/关闭/重启nginx  

start nginx ：启动nginx

nginx -s reload ：修改配置后重新加载生效

nginx -s reopen ：重新打开日志文件

nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

nginx -s stop :快速停止nginx

nginx -s quit ：完整有序的停止nginx
```



## 2.	IIS 方式托管和反向代理配置

### 	2.1	安装ARR(Application Request Route) 为 IIS 开启代理

> 安装后重启 IIS 会显示 Application Request Route Cache，打开该功能开启代理功能

### <img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/arr.png"/>

<img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/configproxy.png"/>

<img src="https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/setproxyenable.png"/>

### 	2.2	安装urlrewrite 配置url重写

> 选中一个项目，配置 RUL 重写 

![](https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/configurl.png)

> 添加规则

![](https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/addrule.png)

> 配置规则

![](https://raw.githubusercontent.com/Edward1220/Vue-project-publish-and-proxy-config/master/image/editrule.png)

