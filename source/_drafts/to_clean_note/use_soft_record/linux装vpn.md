1. 下载浏览器插件

   1. whttps://github.com/FelisCatus/SwitchyOmega/releases/
   2. chrome打开chrome://extensions/
   3. 并把文件拖入网页安装好插件

2. 安装shadowsocks

   1. ```bash
      # 安装界面版
      sudo apt-get install shadowsocks-qt5  
      # 安装命令行版
      sudo apt install shadowsocks
      ```

3. 启动本地客户端shadowsocks

   1. ```bash
      sslocal -c 配置文件.json
      ```

      ​

4. 配置浏览器插件

   1. 点击浏览器右上角的SwitchyOmega图标
   2. 添加本地代理的ip=127.0.0.1   端口=配置端口
   3. 自动切换auto switch 
      1. 配置
      2. https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt



可以给apt设置代理。我现在用的就是，代理已经做了绕过中国了。使用的一个叫meow的东西，可以socks5转http，同时做列表过滤

1. $ cat /etc/apt/apt.conf                                
2. Acquire::http::Proxy "http://127.0.0.1:1080";
3. Acquire::https::Proxy "http://127.0.0.1:1080";