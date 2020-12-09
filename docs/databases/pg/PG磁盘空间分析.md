- 可以根据命令查看磁盘空间（粒度为表）

  ```
  SELECT table_catalog AS "数据库", table_schema AS "模式", table_name, pg_size_pretty(pg_total_relation_size('"' || table_schema || '"."' || table_name || '"')) AS "大小" 
  FROM information_schema.tables
  ORDER BY  table_schema, pg_total_relation_size('"' || table_schema || '"."' || table_name || '"') DESC
  ```

- 结果共占305MB，其中star_info表最大，所占磁盘空间为<font color=red>296MB</font>

- 在验证时引申出来的问题：

  - 不同编码方式，占用的字节是不同的  ==> 即要查看pg的编码

    - 查看pg编码(该pg库所有库模式表都是统一utf8吗？)：

      ```bash
      postgres=# \encoding
      UTF8  
      ```

  - 一个utf8数字占1个字节 一个utf8英文字母占1个字节。
    - 换算：1MB（兆字节） = 1024KB（千字节）= 1024*1024B(字节) 
      - star_info: 一行共223个英文+数字，即223字节，共100W行，所以总大小：(223*1071065)/1024/1024 约为<font color=red>227MB，与命令行结果相近。验证成功。</font>

- 若要采集04-20年数据，假设每年数据量相同，那么 <font color=red>共需要</font>227*17 = 3859MB =   <font color=red>3.7G</font>的磁盘空间

- 查看磁盘总容量：

  ```bash
  [root@iZwz90d4pdwewjjjh9c5iwZ ~]# df -hl
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/vda1        40G  5.8G   32G  16% /
  tmpfs           3.9G  8.0K  3.9G   1% /dev/shm
  ```

  目前可用空间为  <font color=red>32G</font>，安全！

