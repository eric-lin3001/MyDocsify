1. Airflow dag packages import from:

   ```bash
   /usr/local/lib/python3.7/site-packages
   ```

2. Custom Operator Definition Packages are put here:

   ```bash
   /usr/local/lib/python3.7/site-packages/airflow/operators
   ```


3. Test single task in a dag:

   ```
   airflow test [dag_name] [task_name] 20170803
   ```

   