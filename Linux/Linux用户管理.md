##### 添加用户

````apl
useradd 用户名    

#创建用户成功会默认创建用户目录
#用户默认家目录在/home/用户名

#添加用户并且指定目录
useradd  -d   目录  用户名


#设置当前密码
passwd 


#设置其他用户密码
passwd 用户名

````

##### 删除用户

```apl
#删除用户，要先切root
userdel 用户名                 #保留了目录，一般是保留的
userdel -r  用户名             #不保留
```

##### 查询用户

````apl
id 用户名

#查看当前用户信息，显示第一次登录的用户信息，后面切换了还是显示第一个的
whoami

````

##### 切换用户

````apl
su - 切换用户名

#如果要返回原来的用户
exit/logout
````





![image-20210828214145524](C:\Users\Womanjaro\AppData\Roaming\Typora\typora-user-images\image-20210828214145524.png)

