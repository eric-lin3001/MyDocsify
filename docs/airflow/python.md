1. 启动虚拟环境airflow的webserver和scheduler：

   ```bash
   cd /Users/linzeyang/Desktop/cec/gitLab/AirflowPyDemo/airflow-test-env/
   source bin/activate
   export AIRFLOW_HOME=/Users/linzeyang/Desktop/cec/gitLab/AirflowPyDemo/airflow-test-env/airflow_home
   airflow webserver -D
   airflow scheduler -D
   ```


3. Test single task in a dag:

   ```
   airflow test [dag_name] [task_name] 20170803
   ```
   
6

   