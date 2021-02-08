tags: #leetcode #mysql #korean #easy

<hr />

[1179. Reformat Department Table](https://leetcode.com/problems/reformat-department-table/)

mysql 문제가 나와서 시도해봤는데 전혀 모르겠다... 구글링을 통해 풀기는 했는데 따로 공부하지 않으면 바로 까먹을듯.

```sql
# Runtime: 449 ms, faster than 61.35%
# Memory Usage: 0B, less than 100.00%

# Write your MySQL query statement below
SELECT id,
    SUM(CASE WHEN month = 'Jan' THEN revenue END) as Jan_Revenue,
    SUM(CASE WHEN month = 'Feb' THEN revenue END) as Feb_Revenue,
    SUM(CASE WHEN month = 'Mar' THEN revenue END) as Mar_Revenue,
    SUM(CASE WHEN month = 'Apr' THEN revenue END) as Apr_Revenue,
    SUM(CASE WHEN month = 'May' THEN revenue END) as May_Revenue,
    SUM(CASE WHEN month = 'Jun' THEN revenue END) as Jun_Revenue,
    SUM(CASE WHEN month = 'Jul' THEN revenue END) as Jul_Revenue,
    SUM(CASE WHEN month = 'Aug' THEN revenue END) as Aug_Revenue,
    SUM(CASE WHEN month = 'Sep' THEN revenue END) as Sep_Revenue,
    SUM(CASE WHEN month = 'Oct' THEN revenue END) as Oct_Revenue,
    SUM(CASE WHEN month = 'Nov' THEN revenue END) as Nov_Revenue,
    SUM(CASE WHEN month = 'Dec' THEN revenue END) as Dec_Revenue
FROM Department
GROUP BY id
```