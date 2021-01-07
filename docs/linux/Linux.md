## Linux

1. create a file and write text:

   ```shell
   cat > sample.txt
   // text to write
   // ctrl+D to save and exit.
   ```

   

2. list 5 most recently modified file in this dir:

   ```shell
   ll -t | head -5
   ```

3. list each file size in a particular dir:

   ```bash
   du -sh ./* 
   du -shc ./* #not only each file's size, but also total size
   ```

   ![image-20200929100218771](/Users/linzeyang/Library/Application Support/typora-user-images/image-20200929100218771.png)

4. count .csv file in a particular dir:

   ```bash
   find . -type f -iname '*.csv' | wc -l
   ```

   

5. (Mac) get pid from port:

   ```bash
   lsof -i tcp:8081
   ```


6. 查询所有进程号：

   ```bash
   top
   ```

   ![img](https://img-blog.csdnimg.cn/20190611100804819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM4Njk1MTgy,size_16,color_FFFFFF,t_70)

7. 查询所有服务（PID、开始时间、运行时长、启动命令等）

   ```bash
   ps auxw
   ```

8. 根据进程号查服务路径

   ```bash
   ll /proc/[进程号]/cwd
   ```

   ![Screen Shot 2021-01-07 at 09.49.56](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2021-01-07 at 09.49.56.png)

9. 查看ip

   ```bash
   ip a
   ip addr show
   ```

   ![Screen Shot 2021-01-07 at 09.56.54](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2021-01-07 at 09.56.54.png)

