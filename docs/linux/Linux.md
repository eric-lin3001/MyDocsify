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

   

