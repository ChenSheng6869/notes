# SMBMS

# 项目搭建-准备工作

> 1.搭建一个maven web项目

> 2.配置tomcat

> 3.测试项目是否能够跑起来

> 4.导入项目种会遇到的jar包

> 5.创建项目包结构

![image-20220310152517995](G:\03.学习笔记\SMBMS.assets\image-20220310152517995.png)

> 6.编写实体类

​	ORM映射：表-类映射

> 7.编写基础公共类

​	1.数据库配置文件

```java
Driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306?userUnicode=true&characterEncoding=utf-8
username=root
password=123456
```

​	2.编写数据库的公共类

​	3.编写字符编码过滤器

> 8.导入静态资源

# 1登录功能实现

> ### DAO层---->Sevice层---->Servlet层

1.编写前端页面

2.设置欢迎页面(首页)

```xml
    <welcome-file-list>
        <welcome-file>login/jsp</welcome-file>
    </welcome-file-list>
```

3.编写dao层登录用户登录的接口

4.编写dao接口的实现类

5.业务层接口

6.业务层实现类（登录实现）

7.编写Servlet控制层

8.web.xml中注册Servlet

9.测试访问,确保以上功能成功.

## 1.1 登录功能优化

移除session,返回登录界面

注册xml

## 1.1.2 登录拦截器

1.通过HttpServletRequest和HttpServletResponse拿到用户Session

2.如果用户为空,转发到登陆界面,实现不会通过用户session登录系统

## 1.2 退出功能

1.移除用户session

2.通过转发返回登录界面

## 1.3 修改密码

ajax

js: 函数:闭包	Dom	Bom

### 

> ### DAO层---->Sevice层---->Servlet层

1.导入前端素材

2.UserDao接口

3UserDao接口实现类

4.UserService层

5.UserService实现类

6.注册XML

7.实现复用,需要提取出方法

8.测试:优化密码修改使用Ajax

>  1.注册session过期时间
>
> 2.添加阿里巴巴fastjson包
>
> 3.写pwdModify方法，用JSONArray.toString方法转换字符串给前端



# 2 用户管理（难点）



![image-20220312193425140](G:\03.学习笔记\SMBMS.assets\image-20220312193425140.png)

1.导入分页的工具类

2.用户列表导入user.jsp和rollpage.jsp

## 2.1 获取用户数量

1.UserDao

2.UserDaoImpl

3.UserService

4.UserServiceImpl



## 2.2 获取用户列表

1.UserDao

2.UserDaoImpl

3.UserService

4.UserServiceImpl



# 3 获取角色操作

为了职责统一,可以把角色的操作单独放在一个包中,和pojo类对应

1.RoleDao

2.RoleDaoImpl

3.RoleService

4.RoleServiceImpl



# 4 用户显示的servlet

1.获取用户前端的数据（查询）

2.判断请求是否需要执行，看参数的值判断

3.为了实现分页，需要计算出当前页面和总页面，页面大小。。。

4.用户列表展示

5.返回前端





















































































































