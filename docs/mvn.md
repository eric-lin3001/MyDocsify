#### maven报错汇总



1. mvn command not found : 

   ref: https://blog.csdn.net/jiangyu1013/article/details/103584140

2. maven assembly打包zip报错 You must set at least one file：

   经过测试，发现报这个错，本质是因为你assembly配置的 fileSet中的文件一个都找不到，它没有东西能帮你打包成zip。

   ref: https://docker.blog.csdn.net/article/details/109643289