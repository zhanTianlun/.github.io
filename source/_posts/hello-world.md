---
title: 【项目总结】p2p项目个人总结
---
## 1.p2p项目分几个部分?3天实现了哪些功能?

### (后台页面的登录与退出:)

#### 	a.后台管理的登录

​		1.创建包结构,导入jar包,导入从c3p0文件,修改c3p0的配置

​		2.将html文件转换成jsp文件,修改jsp页面中的配置路径

​		3.编写创建servlet文件,service文件和dao文件

​		4.创建user类和user表相对应

​		5.在servlet中获取请求方式,创建一个login方法

​		6.在login方法中接受用户名和密码

​		7.进行非空校验,如果为空,页面重定向

​		8.调用service层,编写login方法,传入用户名和密码的参数

​		9.创建jdbcutils工具

​		10.调用dao层,连接数据库根据用户名和密码查询user,将得到user结果返回

​		11.判断user是否为空,将数据存到request,页面跳转或者重定向

​		12.在login.jsp显示存入的错误信息

#### 	b.登录的过滤

​		1.把home.jsp文件放到views路径下

​		2.创建index.jsp文件

​		3.创建一个filter过滤器

​		4.在过滤器中获取session中的user

​		5.判断user是否为空,为空表示未登录,页面重定向

​		6.不为空表示已登录,放行

​		7.在xml中配置filter

#### 	c.用户退出

​		1.在退出按钮前面添加显示user的名称

​		2.在home.jsp中给按钮标签添href属性传入参数method=logout,添加onclick事件

​		3.在userservlet中接受method参数,编写logout方法

​		4.在logout方法中销毁session,然后页面重定向



### (产品的增加与修改:)

#### 	d.产品的查询

​		1.创建product类,与表相对应

​		2.创建home.js,在home.jsp导入js

​		3.在home.js中编写查询所有产品的函数,页面加载完成后执行函数

​		4.在函数中,向服务器发送请求,传入method参数

​		5.编写productservlet页面

​		6.接受method参数,执行查询所有的方法

​		7.在方法中,调用service层,执行查询的方法,返回一个list集合

​		8.在service中调用dao层

​		9.在DAO层中,查询数据库,将结果以list集合形式返回

​		10.在js页面接受返回的list集合！

​		11.编写展示产品信息的js代码

#### 	e.产品的添加,之查询产品信息

​		1.给新增产品按钮添加click事件,绑定添加产品的函数

​		2.copy代码,在函数中弹出添加产品的层

​		3.在函数中,给弹出层的表格添加click事件

​		4.在click事件中调用serialize方法封装表格中的数据

​		5.向服务器发送请求

​		6.在servlet中接受请求方式,编写add的方法

​		7.在add方法中,创建product对象

​		8.使用beanutils封装数据到product对象

​		9.调用service层执行添加产品的方法

​		10.调用dao层,连接数据库向product表中插入数据

#### f.产品的修改,先查询产品信息,展示到弹出层

​		1.给编辑的a标签添加click事件,绑定修改产品的函数

​		2.在函数中,先修改弹出的层标题和按钮

​		3.在函数中,根据点击编辑的id,向服务器发送请求,传入id和根据id查产品采的方法参数

​		4.接受method参数,执行根据id查询的方法

​		5.调用service层,调用dao层查询产品信息,将数据返回

​		6.给弹出层的每个input添加id,将返回的数据显示在input中

​		7.在添加产品的函数中将input中的内容清空

​		8.给修改按钮绑定click事件,点击按钮,触发函数

​		9.在函数中将input中的内容封装打包,携带id的参数

​		10.向服务器发送请求,传入参数,method=editproduct

​		11.在servlet中接受参数,创建product对象,使用beautils工具封装数据到product对象中

​		12.调用service和dao层,编写editproduct方法

​		13.在修改按钮绑定的函数中,先将弹出层关闭

​		14.重新执行查询所有产品的函数,产品信息改变说明产品信息修改成功

#### g.一些BUG的修改

​			1.在新增产品的按钮绑定点击事件之间先解绑

​			2.在编辑按钮绑定点击事件之间先解绑



### (前台页面的登录:)

#### 	a.验证码的显示与点击切换

​		1.复制文件到utils里面,配置servlet

​		2.在login.html验证码的后面添加img标签和href属性,取一个id

​		3.在img标签里面添加click函数

​		4.在customer.js里面编写函数,导入js

​		5.取到id然后attr设置src属性

#### 	b.点击立即登录按钮,进行登录

​		1.在input框里添加name属性,给按钮注册onclick事件

​		2.在js页面,编写login函数

​		3.把输入框的数据封装在json里面

​		4.向服务器发送请求

#### 	c.servlet里面的登录操作

​		1.接受三个参数
​		2.判断验证码
​		2.1从session中取到checkcode
​		2.2判断两个checkcode
​		3.调用service层,执行login方法
​		4.创建customer对象
​		5.把customer对象存入到session中
​		6.判读是不是空
​		7.创建jsonResout对象 

​		8.设置type和error,并写会到浏览器



#### 	d.用户输入邮箱也可以登录

​		1.在掉serivce层之前判断录入的是不是邮箱的正则
​		2.如果是的,调用findbyemail方法,查到用户对象
​		3.把c_name设置成c.getc_name;
​		4.导入StringUtils文件
​		5.在添加表数据和登录的时候,调用stringUtils的MD5方法加密文件
​		6.在数据库中也对密码进行加密

​		7.设置password的字段为50

​		