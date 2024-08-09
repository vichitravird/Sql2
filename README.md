# Sql2

Problem 1 : Rank Scores		(https://leetcode.com/problems/rank-scores/ )
SELECT 
s.score, COUNT(DISTINCT t.score) AS 'rank' 
FROM scores s INNER JOIN scores t ON s.score <=t.score 
GROUP BY s.id, s.score 
ORDER BY s.score DESC 

Problem 2 : Exchange Seats	(https://leetcode.com/problems/exchange-seats/ )
SELECT s1.id, COALESCE(s2.student, s1.student) AS 'student' 
FROM seat s1 LEFT JOIN seat s2 ON(s1.id + 1)^1-1=s2.id 
ORDER BY id

Problem 3 : Tree Node		(https://leetcode.com/problems/tree-node/ )
# SOLUTION1
SELECT id,
(CASE WHEN p_id IS NULL THEN 'Root'
WHEN id NOT IN (SELECT DISTINCT p_id FROM Tree WHERE p_id NOT NULL) THEN 'Leaf'
ELSE 'Inner'
END) AS 'type' FROM tree;

# SOLUTION2 
WHEN id NOT IN (SELECT p_id FROM Tree Where p_id IS NOT NULL) THEN 'Leaf'
ELSE 'Inner' END AS type
from Tree
ORDER BY id

Problem 4 : Deparment Top 3 Salaries		(https://leetcode.com/problems/department-top-three-salaries/ )
# Write your MySQL query statement below

with cte as(
select emp.name as Employee, dept.name as Department,emp.salary as salary, 
dense_rank() over(partition by emp.departmentId order by emp.salary desc) as salary_rank
from Employee emp left join Department Dept
on emp.departmentId=dept.id)

select Department, Employee, Salary
from cte
where salary_rank<=3
