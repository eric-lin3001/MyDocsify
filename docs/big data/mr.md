map-reduce



1. mr example steps:

0) set classpath:

```bash
export HADOOP_CLASSPATH=$(hadoop classpath)
```

1) compile wc.java: 

```bash
javac -classpath ${HADOOP_CLASSPATH} -d 'PATH_STORE_CLASS_FILES' 'PATH_wc.java'
```

2) trans compiled files('.classes' files) to a executable jar file:

```bash
jar -cvf 'JAR_FILE_NAME' -C 'PATH_STORE_CLASS_FILES' 'PATH_STORE_JARFILE'
```

3)  execute jar file:

```bash
hadoop jar 'PATH_STORE_JARFILE' 'MAINCLASSNAME' 'PATH_HDFS_INPUT' 'PATH_HDFS_OUTPUT'
```



 



