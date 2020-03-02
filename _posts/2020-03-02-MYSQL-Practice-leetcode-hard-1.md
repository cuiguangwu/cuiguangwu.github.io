## Leetcode-1850-[Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries)  

**Runtime: 330 ms, faster than 99.95% of MySQL online submissions for Department Top Three Salaries.**

1. Initial: `SELECT @Rank := 0, @Sal := null, @Type := null`

2. Merge the table of Department  into the table of Employee and sort employee with salary and department.  `SELECT D.Name Department, E.Name Employee, E.Salary Salary FROM Employee E INNER JOIN Department D ON E.DepartmentId = D.Id ORDER BY E.DepartmentId, E.Salary DESC`

3. Number employees by salary and department. 

   ` IF(@Type = Department, 
            CASE 
            WHEN @Sal = Salary THEN @Rank
            WHEN @Sal := Salary or 1 THEN @Rank := @Rank + 1 
            END, 
            @Rank := 1)`

4.  Obtain the top three salaries of the employees in different departments.

### The details of the code of solution are as flows:

```
SELECT Department, Employee, Salary
FROM (SELECT 
        Employee, 
        IF(@Type = Department, 
         CASE 
         WHEN @Sal = Salary THEN @Rank
         WHEN @Sal := Salary or 1 THEN @Rank := @Rank + 1 
         END, 
         @Rank := 1) AS Rank, 
         @Type := Department Department, 
         @Sal := Salary Salary
         FROM (SELECT @Rank := 0, @Sal := null, @Type := null) R, (SELECT D.Name Department, E.Name Employee, E.Salary Salary FROM Employee E INNER JOIN Department D ON E.DepartmentId = D.Id ORDER BY E.DepartmentId, E.Salary DESC) ED
) EDS WHERE Rank = 1 or Rank = 2 or Rank = 3 
```

