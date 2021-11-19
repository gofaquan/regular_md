##### SQL用法举例

##### NULL

```sql	
#空值参与运算
# 空值：null
# null不等同于0，''，'null'

#理解：计算12月的基本工资和奖金
#空值参与运算：结果一定也为空。
SELECT employee_id,salary "月工资",salary * (1 + commission_pct) * 12 "年工资",commission_pct
FROM employees;
# 正确写法引入IFNULL
SELECT employee_id,last_name,salary * 12 * (1 + IFNULL(commission_pct,0)) "ANNUAL SALARY"
FROM employees;

#选择公司中有奖金的员工姓名，工资和奖金级别
#写法一
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct is NOT NULL;
#写法二
SELECT last_name,salary,commission_pct
FROM employees
WHERE NOT commission_pct <=> NULL;
```



##### 去重

```sql
#查询employees表中去除重复的job_id以后的数据 ,去重
SELECT DISTINCT job_id
FROM employees;

```

##### 查表结构

```sql
#显示表 departments 的结构，并查询其中的全部数据
DESCRIBE departments;
```

##### 模糊查询及正则

```sql	
#选择员工姓名的第三个字母是a的员工姓名
SELECT last_name
FROM employees
WHERE last_name LIKE '__a%';
#选择姓名中有字母a和k的员工姓名
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%k%' OR last_name LIKE '%k%a%';
#where last_name like '%a%' and last_name LIKE '%k%';

#显示出表 employees 表中 first_name 以 'e'结尾的员工信息
SELECT first_name,last_name
FROM employees
WHERE first_name LIKE '%e';
#寄吧正则
SELECT first_name,last_name
FROM employees
WHERE first_name REGEXP 'e$'; # 以e开头的写法：'^e'

#查询邮箱中包含 e 的员工信息
#where email like '%e%'
#WHERE email REGEXP '[e]'
```



##### IN

```sql

#显示出表 employees 的 manager_id 是 100,101,110 的员工姓名、工资、管理者id
SELECT last_name,salary,manager_id
FROM employees
WHERE manager_id IN (100,101,110);

```

##### +号的作用

```sql
# mysql的 + 号只能做运算
#数值:加法
#字符:试图转换成数值型 成功加法运算 or 失败变为0再加
select 'j'+90;              //90
```



##### 信息排序

```sql
#3. 强调格式：WHERE 需要声明在FROM后，ORDER BY之前。
SELECT employee_id,salary
FROM employees
WHERE department_id IN (50,60,70)
ORDER BY department_id DESC;

# 练习：按照salary从高到低的顺序显示员工信息
SELECT employee_id,last_name,salary
FROM employees
ORDER BY salary DESC;

# 练习：按照salary从低到高的顺序显示员工信息
SELECT employee_id,last_name,salary
FROM employees
ORDER BY salary ASC;

#默认
SELECT employee_id,last_name,salary
FROM employees
ORDER BY salary; # 如果在ORDER BY 后没有显式指名排序的方式的话，则默认按照升序排列。

#练习：显示员工信息，按照department_id的降序排列，salary的升序排列
SELECT employee_id,salary,department_id
FROM employees
ORDER BY department_id DESC,salary ASC;   #比如两个相同department_id，salary高的在上面


```

##### 别名

```sql
#2. 我们可以使用列的别名，进行排序
SELECT 你爸爸.employee_id,salary,salary * 12 as annual_sal
FROM employees as 你爸爸
ORDER BY annual_sal;

#列的别名只能在 ORDER BY 中使用，不能在WHERE中使用。
#如下操作报错！
SELECT employee_id,salary,salary * 12 annual_sal
FROM employees
WHERE annual_sal > 81600;   #annual_sal报错
```



##### 分页

```sql
#2. 分页
#2.1 mysql使用limit实现数据的分页显示
# 需求1：每页显示20条记录，此时显示第1页
SELECT employee_id,last_name
FROM employees
LIMIT 0,20; # 0+1 ~ 0+20 共20条记录
#第二页
#LIMIT 20,20; # 20+1 ~ 20+20 共20条记录

#LIMIT 20 #前20条 = LIMIT 0,20

#练习：表里有107条数据，我们只想要显示第 32、33 条数据怎么办呢？
SELECT employee_id,last_name
FROM employees
LIMIT 31,2;

#2.3 MySQL8.0新特性：LIMIT ... OFFSET ...
#练习：表里有107条数据，我们只想要显示第 32、33 条数据怎么办呢？
SELECT employee_id,last_name
FROM employees
LIMIT 2 OFFSET 31; #注意offset的不算入 => 32 ~ 33

#LIMIT 可以使用在MySQL、PGSQL、MariaDB、SQLite 等数据库中使用，表示分页。
# 不能使用在SQL Server、DB2、Oracle！无相应语法

```

##### 连接条件

```sql
#云家园对线群一般都是left join，下方自连接与非自连接
#下面是where加连接条件

#出现笛卡尔积的错误
#错误的原因：缺少了多表的连接条件
#错误的实现方式：每个员工都与每个部门匹配了一遍。
SELECT employee_id,department_name #前表107条，后表27条件记录
FROM employees,departments;  #查询出2889 => 107*27 条记录

#多表查询的正确方式：需要有连接条件
SELECT employee_id,department_name
FROM employees,departments
#两个表的连接条件
WHERE employees.`department_id` = departments.department_id;

#建议：从sql优化的角度，建议多表查询时，每个字段前都指明其所在的表。

#如果查询语句中出现了多个表中都存在的字段，则必须指明此字段所在的表。
#可以给表起别名，在SELECT和WHERE中使用表的别名。#where中不能用select中列字段的别名，查看上方 别名 处笔记
#如果给表起了别名，在SELECT或WHERE中使用表名的话，必须使用表的别名，而不能再使用表的原名。
SELECT emp.employee_id,dep.department_name,emp.department_id
FROM employees emp ,deprtments dep
WHERE emp.`department_id` = dep.department_id;

#结论：如果有n个表实现多表的查询，则需要至少n-1个连接条件
#练习：查询员工的employee_id,last_name,department_name,city
SELECT e.employee_id,e.last_name,d.department_name,l.city,e.department_id,l.location_id
FROM employees e,departments d,locations l
WHERE e.`department_id` = d.`department_id` and d.`location_id` = l.`location_id`;
```

##### LEFT,RIGRHT,INNER JOIN

```sql
#自连接  vs  非自连接

#自连接的例子：
#练习：查询员工id,员工姓名及其管理者的id和姓名
SELECT emp.employee_id,emp.last_name,mgr.employee_id,mgr.last_name
FROM employees emp ,employees mgr
WHERE emp.`manager_id` = mgr.`employee_id`;


#内连接  vs  外连接
#内连接：合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行，前面的废话意思就是自己查自己
SELECT employee_id,department_name
FROM employees e,departments d
WHERE e.`department_id` = d.department_id;
#SQL99语法 INNER JOIN (可以忽略INNER，直接写 JOIN也是一样的效果) 实现上方内连接： 
SELECT last_name,department_name
FROM employees e
INNER JOIN departments d
ON e.`department_id` = d.`department_id`;

#外连接：合并具有同一列的两个以上的表的行, 结果集中除了包含一个表与另一个表匹配的行之外，
#还查询到了左表 或 右表中不匹配的行。不难，结合下方例子理解

# 外连接的分类：左外连接、右外连接、满外连接
# 左外连接：两个表在连接过程中除了返回满足连接条件的行以外还返回左表中不满足条件的行，这种连接称为左外连接。
# 右外连接：两个表在连接过程中除了返回满足连接条件的行以外还返回右表中不满足条件的行，这种连接称为右外连接。

#练习：查询所有的员工的last_name,department_name信息，

#错误写法
#既然是所有的员工，可能没有部门名字，名字左表有记录，而右表部门名无
SELECT last_name,department_name
FROM employees e,departments d
WHERE e.`department_id` = d.department_id;   # 这是有名字和部门名的 (106 results) ，需要使用左外连接配对所有
#与上方等价的JOIN / INNER JOIN 写法 (106 results)
SELECT last_name,department_name
FROM employees e
JOIN departments d  ON e.`department_id` = d.department_id;   #这是有名字和部门名的，需要使用左外连接

#正确写法
#左外连接 LEFT JOIN (是LEFT OUTER JOIN的简写)
#使用左外连接，我们多查到了一条有名字而没有部门名的可怜打工人 (107 results)
SELECT last_name,department_name
FROM employees e
LEFT JOIN departments d  ON e.`department_id` = d.department_id;  


#右外连接：RIGHT JOIN (RGIHT OUTER JOIN的简写)
#使用右外连接，我们多查到了一些空有部门名而没有分配员工的寄吧部门名 (122 results)
SELECT last_name,department_name
FROM employees e 
RIGHT OUTER JOIN departments d ON e.`department_id` = d.`department_id`;


#满外连接：mysql不支持FULL OUTER JOIN，故下方语法MySQL跑不了
#满外连接是上面左右外连接的结合，相当于把结果全部显示，没有值的字段为NULL
SELECT last_name,department_name
FROM employees e
FULL  JOIN departments d ON e.`department_id` = d.`department_id`;
```

##### UNION 

```sql
# 描述,先知道有这么个东西吧。。。。。。。。
# MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。

#UNION  和 UNION ALL的使用
# UNION：会执行去重操作
# UNION ALL:不会执行去重操作
#结论：如果明确知道合并数据后的结果数据不存在重复数据，或者不需要去除重复的数据，
#则尽量使用UNION ALL语句，以提高数据查询的效率。
```

