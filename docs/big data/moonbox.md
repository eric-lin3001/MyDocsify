##### Moonbox 测试环境启动

1. ###### 启动

```bash
1. 执行start-all.sh脚本：
sh /opt/moonbox/sbin/start-all.sh
2. 执行jps | grep Moonbox查看master是否存在，存在说明启动成功。
```

2. ###### 登录

```bash
1. 进入目录：
/opt/moonbox/bin
2. 执行脚本：
./moonbox-shell -h node2.develop -r local -u sally -p 123456
```

