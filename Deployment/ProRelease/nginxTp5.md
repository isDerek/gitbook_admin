# 8.3.1.前后端 Nginx 部署

---

### 进入到 /etc/nginx/conf.d/default.conf，编辑该文件内容如下

监听端口号为 8080，本地访问，自定义前后端根目录变量，当外部访问 IP 地址，将该访问代理到前端根目录下，若查询不到资源重新在项目根目录以及根目录文件中查询，若查询不到重写规则，将 url 定位到根目录下的 index.html 再进行访问。若项目中请求 api 路径则重写规则，若查询不到资源则重写规则定位到后台服务器的根目录。

```
server {
	listen	8080;
	server_name localhost;
	# 插座后台管控系统前端根目录
    set $plugFeRoot /fe/vue2.0/plug_back-end/dist;
     # 插座后台管控系统后端根目录
    set $plugBeRoot /be/tp5/plugServer/public;
    location / {
    	   root   $plugFeRoot;
        try_files $uri $uri/ @rewrites;
        index  index.html index.htm index.php;
    }

    location /api/ {
       if ( !-e $request_filename){
        	rewrite ^/(.*)$ /index.php/$1 last;
        	break;
        }
    }

    location @rewrites {
         rewrite ^(.+)$ /index.html last;
    }

	location /gitbook/wgm {
    	   alias  /fe/gitbook/wgm/gitbook_wgm/_book/;
        index  index.html index.htm;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
    location ~ \.php(.*)$ {
    		      root           $plugBeRoot;
                fastcgi_pass   127.0.0.1:9000;
                fastcgi_index  index.php;
                #下面两句是给fastcgi权限，可以支持 ?s=/module/controller/action的url访问模式
                fastcgi_split_path_info  ^((?U).+\.php)(/?.+)$;
                fastcgi_param  SCRIPT_FILENAME  $plugBeRoot$fastcgi_script_name;
                #下面两句才能真正支持 index.php/index/index/index的pathinfo模式
                fastcgi_param  PATH_INFO  $fastcgi_path_info;
                fastcgi_param  PATH_TRANSLATED  $plugBeRoot$fastcgi_path_info;
                include        fastcgi_params;
        }
}
```
