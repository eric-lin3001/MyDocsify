#### DNS



- DNS（Domain Name System）

- 根域名服务器（13台）。

- 可以为一个域名配置多个服务器，即有多个ip地址，在dig查询域名信息时，就会返回多个ip地址。

- 除根服务器外，还有运营商服务器，很多域名通过运营商服务器就能解析，不需要根服务器。

- dns解析流程：

  用户请求某个域名（比如www.google.com）-> 本地服务器先查看/etc/hosts文件是否含有该域名对应的ip -> 若没有，则查看缓存是否含有该域名对应的ip -> 若还没有，则查看自己配置的dns服务器 -> 若还没有，则访问根服务器，根服务器会返回给本地服务器一个ip地址，在该ip地址可以查到所有后缀为'com'的dns（即域名-ip键值对），本地服务器再访问这个ip，该ip又会返回一个ip地址，在该ip地址可以查到所有后缀为'google.com'的dns（即域名-ip键值对）。最后，访问新返回的ip，查询到www.google.com对应的ip地址。

###### Refs:

1. 掌控【根服务器】的美国，可以关闭我们的网络吗？: https://zhuanlan.zhihu.com/p/136600842