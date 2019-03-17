1. 如果报错缺少PCRE库，则安装：

    ``` sudo apt-get update ```
    ``` sudo apt-get install libpcre3 libpcre3-dev  ```
    ``` sudo apt-get install openssl libssl-dev ```


2. 安装nginx

   ``` sudo apt-get install nginx ```





**180上的配置位置：**

​    	```  sudo vim /etc/nginx/sites-available/default```

**重载配置文件（restart的话，如果配置错误则无法启动）**

​	``` sudo service nginx reload```   重载配置文件

​	``` sudo service nginx restart ``` 重启

​	``` sudo service nginx start ```      启动





**proxy_pass**(反向代理)，如果在proxy_pass后面的url加/，表示绝对根路径；如果没有/，表示相对路径，

假设下面四种情况分别用 http://192.168.1.1/proxy/test.html 进行访问。

``` 

location /proxy/ {

    proxy_pass http://127.0.0.1/;     # 代理到URL：http://127.0.0.1/test.html
    proxy_pass http://127.0.0.1;	  # 代理到URL：http://127.0.0.1/proxy/test.html
    proxy_pass http://127.0.0.1/aaa/; # 代理到URL：http://127.0.0.1/aaa/test.html
    proxy_pass http://127.0.0.1/aaa;  # 代理到URL：http://127.0.0.1/aaatest.html

}
```

HTTP静态服务器，相对路径和绝对路径：假设下面2情况分别用 /i/top.gif 进行访问。


``` 

location  /i/ {
  alias  /spool/w3/images/;    # 打开本地文件：/spool/w3/images/top.gif 
}
location  /i/ {
  root  /spool/w3/images/;		# 打开本地文件：/spool/w3/images/i/top.gif 
}
```



**location [=|~|~*|^~] /uri/ { … }**

| 前缀   | 说明                                       | 优先级  |
| ---- | ---------------------------------------- | ---- |
| =    | 精确匹配                                     | 1    |
| ^~   | uri以某个常规字符串开头，理解为匹配 url路径即可。nginx不对url做编码，因此请求为/static/20%/aa，可以被规则^~ /static/ /aa匹配到（注意是空格）。 | 2    |
| ~    | 区分大小写的正则匹配                               | 3    |
| ~*   | 不区分大小写的正则匹配                              | 3    |
| !~   | 区分大小写不匹配的正则                              | 3    |
| !~*  | 不区分大小写不匹配的正则                             | 3    |
| /    | 通用匹配，任何请求都会匹配到。                          | 4    |
|      |                                          |      |

配置缓存大小    /etc/nginx/nginx.conf    http {    }里面添加：

``` 
proxy_buffer_size 128k;
proxy_buffers   32 128k;	
proxy_busy_buffers_size 128k;
```





 