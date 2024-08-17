# Sql2

## Problem 1 : Rank Scores(https://leetcode.com/problems/rank-scores/ )
<br>
SELECT 
s.score, COUNT(DISTINCT t.score) AS 'rank' 
FROM scores s INNER JOIN scores t ON s.score <=t.score 
GROUP BY s.id, s.score 
ORDER BY s.score DESC 

## Problem 2 : Exchange Seats	(https://leetcode.com/problems/exchange-seats/ )
<br>
SELECT s1.id, COALESCE(s2.student, s1.student) AS 'student' 
FROM seat s1 LEFT JOIN seat s2 ON(s1.id + 1)^1-1=s2.id 
ORDER BY id

## Problem 3 : Tree Node		(https://leetcode.com/problems/tree-node/ )
<br>
SELECT id,
(CASE WHEN p_id IS NULL THEN 'Root'
WHEN id NOT IN (SELECT DISTINCT p_id FROM Tree WHERE p_id NOT NULL) THEN 'Leaf'
ELSE 'Inner'
END) AS 'type' FROM tree;
WHEN id NOT IN (SELECT p_id FROM Tree Where p_id IS NOT NULL) THEN 'Leaf'
ELSE 'Inner' END AS type
FROM Tree
ORDER BY id


## Problem 4 : Deparment Top 3 Salaries		(https://leetcode.com/problems/department-top-three-salaries/ )
<br>
WITH CTE AS(
SELECT emp.name as Employee, dept.name AS Department,emp.salary AS salary, 
dense_rank() OVER(PARTITION BY emp.departmentId ORDER BY emp.salary DESC) AS salary_rank
FROM Employee emp LEFT JOIN Department Dept
ON emp.departmentId=dept.id)

SELECT Department, Employee, Salary
FROM CTE
WHERE salary_rank<=3
