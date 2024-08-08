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


Problem 4 : Deparment Top 3 Salaries		(https://leetcode.com/problems/department-top-three-salaries/ )
