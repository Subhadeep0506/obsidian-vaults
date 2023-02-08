# 1. Finding Updated Records
We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.

**DataFrame: ms_employee_salary**

### ms_employee_salary
|column|type|
|---|---|
|id|int64|
|first_name|object|
|last_name|object|
|salary|int64|
|department_id|int64|

### Solution
```python
# Import your libraries
import pandas as pd

# Start writing code
extraxted = ms_employee_salary.groupby(['id', 'first_name', 'last_name', 'department_id'])['salary'].max().reset_index().sort_values('id')
```

# 2. Salaries Differences
Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries.

**DataFrames: db_employee, db_dept**

### db_employee
|column|type|
|---|---|
|id|int64|
|first_name|object|
|last_name|object|
|salary|int64|
|department_id|int64|

### db_dept
|column|type|
|---|---|
|id|int64|
|department_id|object|

### Solution:
```python
# Import your libraries
import pandas as pd

# Start writing code
joined_df = db_employee.set_index('department_id').join(db_dept.set_index('id'))

sal_diff = abs(joined_df[joined_df['department'] == "engineering"]['salary'].max() - joined_df[joined_df['department'] == "marketing"]['salary'].max())

sal_diff
```

# 3. Bikes Last Used
Find the last time each bike was in use. Output both the bike number and the date-timestamp of the bike's last use (i.e., the date-time the bike was returned). Order the results by bikes that were most recently used.

**DataFrame: dc_bikeshare_q1_2012**

### dc_bikeshare_q1_2012
```
duration:object
duration_seconds:int64
start_time:datetime64[ns]
start_station:object
start_terminal:int64
end_time:datetime64[ns]
end_station:object
end_terminal:int64
bike_number:object
rider_type:object
id:int64
```

### Solution:
```python
import pandas as pd

temp = dc_bikeshare_q1_2012.groupby('bike_number')["end_time"].max().to_frame("last_used").reset_index().sort_values(by="last_used", ascending=False)
```

# 