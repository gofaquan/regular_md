## 基础查询

##### 查询单个字段

````sql
select grade_level from job_grades; 
````

##### 查询多个字段
```` sql
select grade_level,lowest_sal from job_grades; 
````

##### 查询所有字段

````sql
select * from job_grades 
````

##### 查询字段并且去重

````sql
 select distinct grade_level,lowest_sal from job_grades; 
````

##### 显示表的结构

````sql
desc job_grades;
````



##### 别名查询

```` apl
查询结果对应字段名改变
1.便于理解
2.去重
````

````sql
select grade_level AS 最高,lowest_sal AS 最低 from job_grades; 

或者

 select grade_level  最高,lowest_sal  最低 from job_grades; 
````



##### +号的作用

````apl
mysql的+号只能做运算
数值:加法
字符:试图转换成数值型 成功加法运算 or 失败变为0再加
select 'j'+90;              //90
````

##### 多字段连接函数`concat()`

````sql
select concat(grade_level,lowest_sal )AS 最高最低 from job_grades; 
````

在`mysql`中`NULL`加任何值都是`NULL`,引入`IFNULL` 函数,后面的值不为null的默认值，一般为0

```` sql
select concat(grade_level,',',lowest_sal,',',ifnull(highest_sal,0))薪水状况 from job_grades;
````



## 条件查询

##### 关键字

`and , or , < ,>,=,!= `

`|| , &&, !`

```` sql
#直接看语义判断作用
select * from job_grades where lowest_sal>999 and  highest_sal<99999;
select * from job_grades where lowest_sal>999  && highest_sal <99999;
````



## 模糊查询

##### 一般和通配符使用

```` apl
% 任意多个字符 
_ 任意单个字符
那么对于查询值中有_ ,%这样的可以转义后在查询 \% , \_ 
或者escape '%' ，escape '_'
````

##### 关键字

`between , like , in , and ,is null ,is not null`

```` sql
#通配符
#模糊查询含0的值
select lowest_sal from job_grades where lowest_sal like '%0%';
#模糊查询第三个字符为0的值
select lowest_sal from job_grades where lowest_sal like '__0';
#模糊查询第二个字符为%的值
select lowest_sal from job_grades where grade_level like '_%' escape '%';

#between and
#查100~9999
select lowest_sal from job_grades where lowest_sal between 100 and  9999;
#查不在100~9999
select lowest_sal from job_grades where lowest_sal not between 100 and  9999;

#in
#选择出对应值为1000或者3000的
select lowest_sal from job_grades where lowest_sal in (1000,3000);
等价于
select lowest_sal from job_grades where lowest_sal=1000 or lowest_sal=3000;
#不能等于,这里不能类比上面的模糊查询，因为是`=`不是`like`
select lowest_sal from job_grades where lowest_sal='%000' or lowest_sal='%000';
select lowest_sal from job_grades where lowest_sal='_000' or lowest_sal='_000';

#is null , is not null
select lowest_sal from job_grades where lowest_sal is null;
select lowest_sal from job_grades where lowest_sal is not null;
````



###### 经典面试题

```sql
select * from 数据表 
是否与
select * from 数据表 where 值 like '%%' ; 
等价？


#如果值中含null就不等价 ， 不含就等价
#使用like '%%'无法查出NULL的记录，所以就没有查询出
```



##### 排序查询

````sql
#由高到低 desc(降序)
select * from employees order by salary desc ;
#由低到高 asc，不写默认asc排序(升序)
select * from employees order by salary  ;

#按别名排序
#算年薪,并且添加一个字段显示,commission_pct为利率
select *,salary*12*(1+ifnull(commission_pct,0)) 年薪 from employees order by 年薪 desc ;

#按函数排序
select * from employees order by length(last_name) desc;

#多要求排
#先按年薪降序排，再按名字长度升序排
select *,salary*12*(1+ifnull(commission_pct,0)) 年薪 from employees order by 年薪 desc,length(last_name) asc;
````



## 常见函数

###### 单行函数 

* 字符函数 

  ````sql
  #1.length   获取参数值的字节个数，汉字是一个字符，3字节
  select length('john')
  #2.concat 拼接字符串
  select concat(last_name,'_',first_name) 姓名 from employees；
  #3.upper、lower
  select upper('john')      //JOHN
  select lower('john')      //john,不变
  select lower('joHn')      //joHn
  #姓大写，名小写，然后加上下划线拼接
  select concat(upper(last_name),'_',lower(first_name)) 姓名 from employees；
  
  #4.substr，substring
  #截取前六个字符
  select substr('我真的是服了啊啊啊啊啊'，6); //我真的是服了
  #截取前面索引与后面索引之间的字符，包括头尾，注意是索引第一个为1，数组下标第一个才是0
  select substr('我真的是服了啊啊啊啊啊'，1，6); //我真的是服了
  #首字母大写其余小写
  select concat(upper(substr(last_name,1,1)),lower(substr(last_name,2))) from employees;
  
  #5.instr ， 返回子串第一次出现的索引，找不到返回0
  select instr('woshinidie','wo');
  
  #6.trim ,去两边的空格或字符
  select length(trim('   hhhhhh    '))   //6
  select length(trim 'a' from 'aaaaaaaaahhhhhhaaaaaaa');   //6
  
  #7.lpad 左填充, rpad 右填充 到达制定长度
  select lpad('123',5,'@'); 			//@@123
  select rpad('123',5,'@') ;			//123@@
  select lpad('123',2,'@') ;  		//12  本来就大于该长度自动删减
  ````

* 数学函数

  ````sql
  #round 四舍五入
  select round(-1.55);     		//-2
  select round(1.55);     		//2
  
  #向上取整
  select ceil(-1.02);          	//-1
  
  #向下取整
  select floor(-1.02);          	 //-2
  
  #truncate
  select truncate(1.2222222,1)    //1.2，小数点后保留一位
  
  #mod 取余  mod(a,b)    => a- a/b * b
  select mod(-10,-3)  //-1
  等价
  select -10%-3;
  ````

* 日期函数

  ````sql
  #当前日期和时间
  select now();
  
  #curdate 当前日期，无时间
  select curdate();
  
  #curtime 当前时间，无日期
  select curtime();
  
  #也可以获取年月日小时秒等
  select year(now());		//7
  select month(now());    //July
  select day(now());		//10
  select dayname(now());		//Saturday
  
  
  #str_to_date:将字符通过指定格式转换成日期 
  SELECT STR_TO_DATE('2021-7-10','%Y-%c-%d');
  
  #date_format:将日期转换成字符
  SELECT DATE_FORMAT('2021/7/10','%Y年%m月%d日');
  SELECT DATE_FORMAT(NOW(),'%Y年%m月%d日');
  
  #datediff 两个日期相距多久
  select datediff(now(),'2001-10-08');    //我活了7215天了
  -------------------------------------------------------------------
  %M 月名字(January……December) 
      %W 星期名字(Sunday……Saturday) 
      %D 有英语前缀的月份的日期(1st, 2nd, 3rd, 等等。） 
      %Y 年, 数字, 4 位 
      %y 年, 数字, 2 位 
      %a 缩写的星期名字(Sun……Sat) 
      %d 月份中的天数, 数字(00……31) 
      %e 月份中的天数, 数字(0……31) 
      %m 月, 数字(01……12) 
      %c 月, 数字(1……12) 
      %b 缩写的月份名字(Jan……Dec) 
      %j 一年中的天数(001……366) 
      %H 小时(00……23) 
      %k 小时(0……23) 
      %h 小时(01……12) 
      %I 小时(01……12) 
      %l 小时(1……12) 
      %i 分钟, 数字(00……59) 
      %r 时间,12 小时(hh:mm:ss [AP]M) 
      %T 时间,24 小时(hh:mm:ss) 
      %S 秒(00……59) 
      %s 秒(00……59) 
      %p AM或PM 
      %w 一个星期中的天数(0=Sunday ……6=Saturday ） 
      %U 星期(0……52), 这里星期天是星期的第一天 
      %u 星期(0……52), 这里星期一是星期的第一天 
  ````

* 其它函数

  ````sql
  #version 当前数据库服务器的版本
  SELECT VERSION();
  
  #database 当前打开的数据库
  SELECT DATABASE();
  
  #user当前用户
  SELECT USER();
  
  #password('字符')：返回该字符的密码形式
  SELECT PASSWORD('a');
  
  #md5('字符'):返回该字符的md5加密形式
  SELECT MD5('a');
  
  ````

  

* 流程控制函数

````sql
流程控制函数具体案例：

#1.if函数: if else效果

SELECT IF(10<5,'大','小');

SELECT last_name,commission_pct,IF(commission_pct IS NULL,'没奖金！！！','有奖金!!!') 备注 FROM employees;

#2.case函数
#使用一:switch case 的效果
/*
java中
switch(变量或表达式){
	case 常量1:语句1;break;
	...
	default:语句n;break;
}

mysql中

case 要判断的变量或表达式
when 常量1 then 要显示的值1或语句1
when 常量2 then 要显示的值2或语句2
...
else 要显示的值n或语句n
end

#案例:查询员工的工资,要求:

部门号=30,显示的工资为1.1倍
部门号=40,显示的工资为1.2倍
部门号=50,显示的工资为1.3倍
其他部门,显示的工资为原工资

*/

SELECT salary 原始工资,department_id,
CASE department_id
WHEN 30 THEN salary*1.1
WHEN 40 THEN salary*1.2
WHEN 50 THEN salary*1.3
ELSE salary
END AS 新工资
FROM employees;

#3.case函数的使用二:类似于多重if
/*
java中:
if(条件1){
	语句1;
}else if(条件2){
	语句2;
}
...
else{
	语句n;
}	

mysql中:
case 
when 条件1 then 要显示的值1或语句1
when 条件2 then 要显示的值2或语句2
...
else 要显示的值n或语句n
end

*/

#案例:查询员工的工资的情况
/*
如果工资>20000，显示A级别
如果工资>15000，显示B级别
如果工资>10000，显示c级别
否则，显示D级别
*/

SELECT salary,
CASE
WHEN salary>20000 THEN 'A'
WHEN salary>15000 THEN 'B'
WHEN salary>10000 THEN 'C'
ELSE 'D'
END AS 工资等级
FROM employees;
````



###### 分组函数

```apl
功能：用作统计使用，又称为聚合函数或统计函数或组函数
分类：sum 求和、avg 平均值、max 最大值、min最小值count 计算个数
特点:
1. sum ,avg(average)    一般用于处理数值型
max、min、count可以处理任何数据类型
2.以上分组函数都忽略null
3.都可以搭配distinct使用，实现去重的统计
select sum(distinct 字段) from 表;
4. count函数
count(字段)：统计该字段非空值的个数
count(*):统计结果集的行数
5.和分组函数一同查询的字段，要求是group by后出现的字段
```

````sql
#1.简单使用
SELECT SUM(salary) FROM employees;
SELECT AVG(salary) FROM employees;
SELECT MAX(salary) FROM employees;
SELECT MIN(salary) FROM employees;
SELECT COUNT(salary) FROM employees;

SELECT SUM(salary) 和,ROUND(AVG(salary),2) 平均,MAX(salary) 最高,MIN(salary) 最低,COUNT(salary) 个数
FROM employees;

#2.参数支持哪些数据类型

SELECT SUM(last_name),AVG(last_name) FROM employees;
SELECT SUM(hiredate),AVG(hiredate) FROM employees;

SELECT MAX(last_name),MIN(last_name) FROM employees;
SELECT MAX(hiredate),MIN(hiredate) FROM employees;

SELECT COUNT(commission_pct) FROM employees;
SELECT COUNT(last_name) FROM employees;

#3.是否忽略null

SELECT SUM(commission_pct),AVG(commission_pct) FROM employees;

SELECT commission_pct FROM employees;

SELECT SUM(commission_pct),AVG(commission_pct),SUM(commission_pct)/35,AVG(commission_pct)/107 FROM employees;

SELECT MAX(commission_pct),MIN(commission_pct) FROM employees;

SELECT COUNT(commission_pct) FROM employees;

#4.和distinct搭配

SELECT SUM(DISTINCT salary),SUM(salary) FROM employees;

SELECT COUNT(DISTINCT salary),COUNT(salary) FROM employees;

#5.count函数详解

SELECT COUNT(salary) FROM employees;
SELECT COUNT(*) FROM employees;
SELECT COUNT(1) FROM employees;
/*
效率上：
MyISAM存储引擎，count(*)最高
InnoDB存储引擎，count(*)和count(1)效率>count(字段)
*/

#6.和分组函数一同查询的字段有限制
#employee_id有多个值，avg只有一个，最后只会显示一个avg和一个employee_id，那么这个employee_id是无意义的
SELECT AVG(salary),employee_id FROM employees;
````



###### 分组查询

```apl
语法:
 select 分组函数,分组后的字段
 from 表
【where 筛选条件】
 group by 分组的字段
【having 分组后的筛选】
【order by 排序列表】
注意:查询列表必须特殊,要求是分组函数和group by后出现的字段
特点:

1.分组查询中的筛选条件分为两类

			使用关键字	筛选的表	位置
分组前筛选	where		原始表		group by的前面
分组后筛选	having		分组后的结果	group by的后面
1.分组函数做条件肯定是放在having子句中
2.能用分组前筛选的，就优先考虑使用分组前筛选
3.group by子句支持单个字段分组，多个字段分组(多个字段之间用逗号隔开没有顺序要求),表达式或函数(使用较少)
4.也可以添加排序(排序放在整个分组查询的最后)
```



````sql
#引入:查询每个部门的平均工资
SELECT AVG(salary) FROM employees;

#案例1:查询每个工种的最高工资
SELECT MAX(salary),job_id FROM employees 
GROUP BY job_id;


#案例2:查询每个位置上的部门个数
SELECT COUNT(*),location_id
FROM departments
GROUP BY location_id;

#添加筛选条件
#案例1:查询邮箱中包含a字符的，每个部门的平均工资
SELECT AVG(salary),department_id FROM employees
WHERE email LIKE '%a%' GROUP BY department_id;

#案例2:查询有奖金的每个领导手下员工的最高工资
SELECT MAX(salary),manager_id FROM employees
WHERE commission_pct IS NOT NULL
GROUP BY manager_id;

#添加复杂的筛选条件
#案例1:查询哪个部门的员工个数>2
#1.查询每个部门的员工个数
SELECT COUNT(*),department_id FROM employees
GROUP BY department_id;

#2.根据1的结果进行筛选，查询哪个部门的员工个数大于2
SELECT COUNT(*),department_id FROM employees
GROUP BY department_id HAVING COUNT(*)>2;


#案例2:查询每个工种有奖金的员工的最高工资>12000的工种编号和最高工资 
#1.查询每个工种有奖金的员工的最高工资 
SELECT MAX(salary),job_id FROM employees 
WHERE commission_pct IS NOT NULL GROUP BY job_id; 

#2.根据结果继续筛选，最高工资>12000 

SELECT MAX(salary), job_id FROM employees 
WHERE commission_pct IS NOT NULL GROUP BY job_id 
HAVING MAX(salary)>12000; 

#按表达式或函数分组

#案例:按员工姓名的长度分组,查询每一组的员工个数,筛选员工个数>5

#1.查询每个长度的员工个数 
SELECT COUNT(*),LENGTH(last_name) len_name 
FROM employees GROUP BY LENGTH(last_name); 

#2.添加筛选条件
SELECT COUNT(*) c,LENGTH(last_name) len_name 
FROM employees GROUP BY len_name HAVING c>5;

SELECT COUNT(*) c,LENGTH(last_name) len_name 
FROM employees GROUP BY len_name HAVING c>5;

#按多个字段查询
#案例:查询每个部门每个工种的员工的平均工资

SELECT AVG(salary),department_id,job_id
FROM employees GROUP BY department_id,job_id;

#添加排序
#案例:查询每个部门每个工种的员工的平均工资,按平均工资的高低查询

SELECT AVG(salary),department_id,job_id
FROM employees GROUP BY department_id,job_id
ORDER BY AVG(salary) DESC;
````

# 大坑

```sql
#可以执行
select count(*),length(last_name) as c from employees group by length(last_name) having c > 5;
#不能执行
select count(*),length(last_name) from employees group by length(last_name) having  length(last_name) > 5;
#having 不能执行 单行函数！！！！！！
```

