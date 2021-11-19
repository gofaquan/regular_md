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

