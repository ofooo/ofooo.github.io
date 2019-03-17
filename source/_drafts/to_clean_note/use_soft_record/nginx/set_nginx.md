---
title: 设置nginx
tags: [nginx]
---

### 185default

```json
server {
	listen 80;

	root /home/wangxiaoyu/wxydir/nginx;
	index index.html index.htm;
	
	server_name localhost;
	
	location / {
	      root  /home/wangxiaoyu/wxydir/nginx;#这里填写你的静态文件存储根目录
	      access_log   on;
	      autoindex  on;
	   }
}
```

### default

```json
# You may add here your
# server {
#	...
# }
# statements for each of your virtual hosts to this file

##
# You should look at the following URL's in order to grasp a solid understanding
# of Nginx configuration files in order to fully unleash the power of Nginx.
# http://wiki.nginx.org/Pitfalls
# http://wiki.nginx.org/QuickStart
# http://wiki.nginx.org/Configuration
#
# Generally, you will want to move this file somewhere, and start with a clean
# file but keep this around for reference. Or just disable in sites-enabled.
#
# Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
##

server {
	listen 80 default_server;
	# listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	listen 443 ssl default_server;
	ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	# allow 192.168.31.0/24;
	# deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name demo.deeplycurious.ai;

	location ^~ /cac/ {
		rewrite ^/cac/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8000;
	}
	location ^~ /wlmq/ {
		rewrite ^/wlmq/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8321;
	}
	location ^~ /conv/ {
		proxy_pass_header Server;
		proxy_set_header Host $http_host;
		proxy_redirect off;
		proxy_set_header X-Read-IP $remote_addr;
		proxy_set_header X-Scheme $scheme;
		rewrite ^/conv/(.*)$ /$1 break;
		proxy_pass http://192.168.31.52:8324/;
	}
	location ^~ /command-and-camera/ {
		rewrite ^/command-and-camera/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8000;
	}
	location ^~ /asr/ {
		rewrite ^/asr/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:5007;
	}
	location ^~ /clf/ {
		rewrite ^/clf/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:5000;
	}
	location ^~ /datainsighter/ {
		rewrite ^/datainsighter/(.*)$ /MagicData/$1 break;
		# proxy_pass https://192.168.31.80:443;
		proxy_pass https://demo.deeplycurious.ai:8327;
	}
	location ^~ /clftest/ {
		rewrite ^/clftest/(.*)$ /$1 break;
		proxy_pass http://192.168.31.188:1234;
	}
	
	
    location ~ ^/demox/(.*)$ {
	rewrite ^/demox/(.*)$ /demo/$1 break;
        proxy_pass http://192.168.31.185:50036;
    }
    location ~ ^/(.*)$ {
        # try_files $uri $uri/ =404;
        set $tmp_addr $1;
        if ($http_referer ~ ^.*/demox(.*)$ ) { 
	    #add_header X-uri "url-$1";
	    #rewrite ^/(.*)$ /$1 break;
	    #add_header X-uri1 "url-$tmp_addr";
            proxy_pass http://192.168.31.185:50036;
        }   
	if ($http_referer ~ ^.*/conv(.*)$ ) {
            proxy_pass http://192.168.31.50:8324;
        }
    }

}

server {
	listen 80;

	root /usr/share/nginx/html;
	index index.html index.htm;

	server_name lfz212.imwork.net;

	location ^~ /label/ {
		rewrite ^/label/(.*)$ /$1 break;
		proxy_pass http://192.168.31.103:80;
	}
	location / {
		proxy_pass http://lfz212.imwork.net:9080;
	}
}

server {
	listen 80;

	root /usr/share/nginx/html;
	index index.html index.htm;

	server_name in.deeplycurious.ai;

	location / {
		proxy_pass http://in.deeplycurious.ai:9080;
	}
}






server {
	listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	listen 443 ssl;
	ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	allow 192.168.31.0/24;
	deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name show.fore.run;

	#location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
	 	#try_files $uri $uri/ =404;
		# Uncomment to enable naxsi on this location
		# include /etc/nginx/naxsi.rules
	#}
        location ^~ /message/user/ {
                proxy_pass http://192.168.31.186:8010;
                proxy_http_version 1.1;
                proxy_set_header Upgrade WebSocket; #$http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_set_header Host $http_host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ^~ / {
                proxy_pass http://192.168.31.186:8010;
        }
}

server {
	listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	# listen 443 ssl;
	# ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	# ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	# allow 192.168.0.0/16;
	# deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name vcs.fore.run;

	# location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
	 	# try_files $uri $uri/ =404;
		# Uncomment to enable naxsi on this location
		# include /etc/nginx/naxsi.rules
	# }
        # location ^~ /message/user/ {
        #         proxy_pass http://192.168.31.186:8010;
        #         proxy_http_version 1.1;
        #         proxy_set_header Upgrade WebSocket; #$http_upgrade;
        #         proxy_set_header Connection "upgrade";
        #         proxy_set_header Host $http_host;
        #         proxy_set_header X-Real-IP $remote_addr;
        # }

        location ^~ / {
                proxy_pass http://192.168.31.186;
        }
}

```

default备份

```json
# You may add here your
# server {
#	...
# }
# statements for each of your virtual hosts to this file

##
# You should look at the following URL's in order to grasp a solid understanding
# of Nginx configuration files in order to fully unleash the power of Nginx.
# http://wiki.nginx.org/Pitfalls
# http://wiki.nginx.org/QuickStart
# http://wiki.nginx.org/Configuration
#
# Generally, you will want to move this file somewhere, and start with a clean
# file but keep this around for reference. Or just disable in sites-enabled.
#
# Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
##

server {
	listen 80 default_server;
	# listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	listen 443 ssl default_server;
	ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	# allow 192.168.31.0/24;
	# deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name demo.deeplycurious.ai;

	#location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
	 	#try_files $uri $uri/ =404;
		# Uncomment to enable naxsi on this location
		# include /etc/nginx/naxsi.rules
	#}
	location ^~ /cac/ {
		rewrite ^/cac/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8000;
	}
	location ^~ /wlmq/ {
		rewrite ^/wlmq/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8321;
	}
	location ^~ /conv/ {
		proxy_pass_header Server;
		proxy_set_header Host $http_host;
		proxy_redirect off;
		proxy_set_header X-Read-IP $remote_addr;
		proxy_set_header X-Scheme $scheme;
		rewrite ^/conv/(.*)$ /$1 break;
		proxy_pass http://192.168.31.52:8324/;
	}
	location ^~ /command-and-camera/ {
		rewrite ^/command-and-camera/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:8000;
	}
	location ^~ /asr/ {
		rewrite ^/asr/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:5007;
	}
	location ^~ /clf/ {
		rewrite ^/clf/(.*)$ /$1 break;
		proxy_pass http://192.168.31.185:5000;
	}
	location ^~ /datainsighter/ {
		rewrite ^/datainsighter/(.*)$ /MagicData/$1 break;
		# proxy_pass https://192.168.31.80:443;
		proxy_pass https://demo.deeplycurious.ai:8327;
	}
	location ^~ /clftest/ {
		rewrite ^/clftest/(.*)$ /$1 break;
		proxy_pass http://192.168.31.188:1234;
	}
    location ~ ^/demox/(.*)$ {
	rewrite ^/demox/(.*)$ /demo/$1 break;
        proxy_pass http://192.168.31.185:50036;
    }
    location ~ ^/(.*)$ {
        # try_files $uri $uri/ =404;
        set $tmp_addr $1;
        if ($http_referer ~ ^.*/demox(.*)$ ) { 
	    #add_header X-uri "url-$1";
	    #rewrite ^/(.*)$ /$1 break;
	    #add_header X-uri1 "url-$tmp_addr";
            proxy_pass http://192.168.31.185:50036;
        }   
	if ($http_referer ~ ^.*/conv(.*)$ ) {
            proxy_pass http://192.168.31.50:8324;
        }
    }

	# Only for nginx-naxsi used with nginx-naxsi-ui : process denied requests
	#location /RequestDenied {
	#	proxy_pass http://127.0.0.1:8080;    
	#}

	#error_page 404 /404.html;

	# redirect server error pages to the static page /50x.html
	#
	#error_page 500 502 503 504 /50x.html;
	#location = /50x.html {
	#	root /usr/share/nginx/html;
	#}

	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	#location ~ \.php$ {
	#	fastcgi_split_path_info ^(.+\.php)(/.+)$;
	#	# NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
	#
	#	# With php5-cgi alone:
	#	fastcgi_pass 127.0.0.1:9000;
	#	# With php5-fpm:
	#	fastcgi_pass unix:/var/run/php5-fpm.sock;
	#	fastcgi_index index.php;
	#	include fastcgi_params;
	#}

	# deny access to .htaccess files, if Apache's document root
	# concurs with nginx's one
	#
	#location ~ /\.ht {
	#	deny all;
	#}
}

server {
	listen 80;

	root /usr/share/nginx/html;
	index index.html index.htm;

	server_name lfz212.imwork.net;

	location ^~ /label/ {
		rewrite ^/label/(.*)$ /$1 break;
		proxy_pass http://192.168.31.103:80;
	}
	location / {
		proxy_pass http://lfz212.imwork.net:9080;
	}
}

server {
	listen 80;

	root /usr/share/nginx/html;
	index index.html index.htm;

	server_name in.deeplycurious.ai;

	location / {
		proxy_pass http://in.deeplycurious.ai:9080;
	}
}


# another virtual host using mix of IP-, name-, and port-based configuration
#
#server {
#	listen 8000;
#	listen somename:8080;
#	server_name somename alias another.alias;
#	root html;
#	index index.html index.htm;
#
#	location / {
#		try_files $uri $uri/ =404;
#	}
#}


# HTTPS server
#
#server {
#	listen 443;
#	server_name localhost;
#
#	root html;
#	index index.html index.htm;
#
#	ssl on;
#	ssl_certificate cert.pem;
#	ssl_certificate_key cert.key;
#
#	ssl_session_timeout 5m;
#
#	ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
#	ssl_ciphers "HIGH:!aNULL:!MD5 or HIGH:!aNULL:!MD5:!3DES";
#	ssl_prefer_server_ciphers on;
#
#	location / {
#		try_files $uri $uri/ =404;
#	}
#}

server {
	listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	listen 443 ssl;
	ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	allow 192.168.31.0/24;
	deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name show.fore.run;

	#location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
	 	#try_files $uri $uri/ =404;
		# Uncomment to enable naxsi on this location
		# include /etc/nginx/naxsi.rules
	#}
        location ^~ /message/user/ {
                proxy_pass http://192.168.31.186:8010;
                proxy_http_version 1.1;
                proxy_set_header Upgrade WebSocket; #$http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_set_header Host $http_host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ^~ / {
                proxy_pass http://192.168.31.186:8010;
        }
}

server {
	listen 80;
	# listen [::]:80 ipv6only=on;

	# SSL
	# listen 443 ssl;
	# ssl_certificate     /etc/nginx/ssl/demo.deeplycurious.ai.crt;
	# ssl_certificate_key /etc/nginx/ssl/demo.deeplycurious.ai.key;

	# allow 192.168.0.0/16;
	# deny all;
	root /usr/share/nginx/html;
	index index.html index.htm;

	# Make site accessible from http://localhost/
	server_name vcs.fore.run;

	# location / {
		# First attempt to serve request as file, then
		# as directory, then fall back to displaying a 404.
	 	# try_files $uri $uri/ =404;
		# Uncomment to enable naxsi on this location
		# include /etc/nginx/naxsi.rules
	# }
        # location ^~ /message/user/ {
        #         proxy_pass http://192.168.31.186:8010;
        #         proxy_http_version 1.1;
        #         proxy_set_header Upgrade WebSocket; #$http_upgrade;
        #         proxy_set_header Connection "upgrade";
        #         proxy_set_header Host $http_host;
        #         proxy_set_header X-Real-IP $remote_addr;
        # }

        location ^~ / {
                proxy_pass http://192.168.31.186;
        }
}

```




