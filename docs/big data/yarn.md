1. yarn是做资源管理的。
2. 以mapreduce任务为例，MRAppMaster会向ResourceManager申请
3. 空闲的NodeManager领取到ResourceManager分配的任务，任务需要相应的资源（cpu，ram，net，io等）才能运行，资源由Container创建，Container分配完相应的资源后，启动相应的MRAppmaster。MRAppmaster会读取Job.split等，确定共需要多少切片，而后向RM申请MapTask，RM又会去找空闲的NM，Container创建MapTask需要的相关资源。
4. ![Screen Shot 2020-10-20 at 13.57.23](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-10-20 at 13.57.23.png)