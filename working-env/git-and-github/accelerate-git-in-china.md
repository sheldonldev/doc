# Accelerate Git in China

* if you use sockets: [https://www.cnblogs.com/StevenWind/p/11735352.html](https://www.cnblogs.com/StevenWind/p/11735352.html)

A1:基于http的git与基于http的代理

好的，一切准备就绪，因为现在有两种git协议(A,B)，两种代理协议(1,2)，所以有四种设置方法。

git config --global http.proxy "http://127.0.0.1:1080"
git config --global https.proxy "http://127.0.0.1:1080"
A2:基于http的git与基于socks5的代理

git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"

B1:基于ssh的git与基于http的代理

   修改~/.ssh/config文件，如在ubuntu下使用: gedit ~/.ssh/config

　添加如下内容:

Host github.com
HostName github.com
User git
ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=1080

　添加完毕，记得保存

 

B2:基于ssh的git与基于socks5的代理

    修改~/.ssh/config文件，如在ubuntu下使用: gedit ~/.ssh/config

　添加如下内容:

Host github.com
HostName github.com
User git
ProxyCommand nc -v -x 127.0.0.1:1080 %h %p

添加完毕，记得保存

