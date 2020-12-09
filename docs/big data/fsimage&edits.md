1. location(dn+nn):

   /hadoop/hdfs why?

   ![Screen Shot 2020-10-20 at 09.34.14](/Users/linzeyang/Desktop/shots/Screen Shot 2020-10-20 at 09.34.14.png)

2. ll fsimage* | head -n 10(获取当前路径下，以fsimage开头的前10个文件（夹）)

   ![Screen Shot 2020-10-20 at 09.42.29](/Users/linzeyang/Desktop/shots/Screen Shot 2020-10-20 at 09.42.29.png)

3. hdfs oiv -p XML -i fsimage_0000000000012799701 -o ~/fsimage.xml

   （将fsimage_0000000000012799701镜像文件以xml格式输出在~/fsimage.xml文件里。）

4. 在local使用scp root@192.168.6.140:/root/fsimage.xml . 将fsimage.xml传回到本地查看

5. fsimage.xml snapshot:

   

   ![Screen Shot 2020-10-20 at 10.36.10](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-10-20 at 10.36.10.png)