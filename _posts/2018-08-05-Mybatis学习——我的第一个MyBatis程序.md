---
layout: post
title: MyBatis学习——我的第一个MyBatis程序
cover: /img/cover/MyBatis01.jpg
tags: ['MyBatis', '开源', '框架']
---

#### **1、创建maven父集中版本定义工程**
#### 工具：myeclipse 2016 CI 7(当初装的测试版)
##### 步骤：File->New->Maven Project
如图，把红色箭头处的选项勾上：

[![newMaven](https://i.screenshot.net/4p3ddid "newMaven")](https://i.screenshot.net/4p3ddid "newMaven")

**输入，Group id 和Arfact id，
选择红色箭头指的pom，
GroupID 是项目组织唯一的标识符，实际对应JAVA的包的结构，是main目录里java的目录结构。 
ArtifactID是项目的唯一的标识符，实际对应项目的名称，就是项目根目录的名称。**

[![newMaven2](https://i.screenshot.net/p/k4ekkbk?9b7a5d286a82d5f1afaabf0c9052324c "newMaven2")](https://i.screenshot.net/p/k4ekkbk?9b7a5d286a82d5f1afaabf0c9052324c "newMaven2")

修改pom.xml文件，在这看吧：[地址]{https://github.com/famine-life}

#### 2、创建mybatis项目，（添加 `<parent><!-- 引入父工程 --></parent>`）

创建过程：略

修改pom.xml
```java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <parent>
    <!-- 引入父工程 -->
    <!-- 版本做了统一管理    出现红×更新 -->
  	<groupId>com.liantao.parent</groupId>
	<artifactId>maven-parent</artifactId>
	<version>0.0.1-SNAPSHOT</version>
  </parent>
  
  <groupId>com.liantao.mybatis01</groupId>
  	<artifactId>mybatis01</artifactId>
  <version>1.0.1-SNAPSHOT</version>
 
  <dependencies>
	<!-- MySql -->
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
	</dependency>
	<!-- Mybatis -->
	<dependency>
		<groupId>org.mybatis</groupId>
		<artifactId>mybatis</artifactId>
	</dependency>

  </dependencies>
 
  <build/>
</project>

```

添加相关包和相关目录：**myeclipse下，右键项目，maven->update Project**

#### 3、在mysql下建立数据库ssm,并创建t_user表
```sql
DROP TABLE IF EXISTS `t_user`;
CREATE TABLE `t_user` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `user_name` varchar(100) DEFAULT NULL COMMENT '用户名',
  `password` varchar(100) DEFAULT NULL COMMENT '密码',
  `name` varchar(100) DEFAULT NULL COMMENT '姓名',
  `age` int(10) DEFAULT NULL COMMENT '年龄',
  `sex` tinyint(1) DEFAULT NULL COMMENT '性别，1男性，2女性',
  `birthday` date DEFAULT NULL COMMENT '出生日期',
  `created` datetime DEFAULT NULL COMMENT '创建时间',
  `updated` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `username` (`user_name`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8;
 
-- ----------------------------
-- Records of t_user
-- ----------------------------
INSERT INTO `t_user` VALUES ('1', 'zhangsan', '123456', '落尘曦', '30', '1', '1984-08-08', '2014-09-19 16:56:04', '2014-09-21 11:24:59');

```

#### 4、在src/main/java下创建包com.liantao.pojo，在pojo下创建实体类User.java

```java
package com.liantao.pojo;
 
import java.util.Date;
 
public class User {
    //用户id
    private Long id;
    // 用户名
    private String userName;
    // 密码
    private String password;
    // 姓名
    private String name;
    // 年龄
    private Integer age;
    // 性别， 1男性， 2女性
    private Integer sex;
    // 出生日期
    private Date birthday;
    // 创建时间
    private Date created;
    // 更新时间
    private Date updated;
    
    public User(){
    	
    }
    
    public Long getId() {
        return id;
    }
 
    public void setId(Long id) {
        this.id = id;
    }
 
    public String getuserName() {
        return userName;
    }
 
    public void setuserName(String userName) {
        this.userName = userName;
    }
 
    public String getPassword() {
        return password;
    }
 
    public void setPassword(String password) {
        this.password = password;
    }
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public Integer getAge() {
        return age;
    }
 
    public void setAge(Integer age) {
        this.age = age;
    }
 
    public Integer getSex() {
        return sex;
    }
 
    public void setSex(Integer sex) {
        this.sex = sex;
    }
 
    public Date getBirthday() {
        return birthday;
    }
 
    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }
 
    public Date getCreated() {
        return created;
    }
 
    public void setCreated(Date created) {
        this.created = created;
    }
 
    public Date getUpdated() {
        return updated;
    }
 
    public void setUpdated(Date updated) {
        this.updated = updated;
    }
 
    @Override
    public String toString() {
        return "User [id=" + id + ", userName=" + userName + ", password=" + password + ", name=" + name
                + ", age=" + age + ", sex=" + sex + ", birthday=" + birthday + ", created=" + created
                + ", updated=" + updated + "]";
    }
 
}

```

------------


#### 5、在src/main/resources创建mybatis-config.xml
记得改为你自己的配置
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/ssm"/>
        <property name="username" value="root"/>
        <property name="password" value="admin"/>
      </dataSource>
    </environment>
  </environments>
  
  <mappers>
      <!-- 默认为classpath目录-->
      <mapper resource="mapper/UserMapper.xml"/>
  </mappers>
  
</configuration>
 

```

**注意mapers下的mapper的resource地址不要写错**

#### 6、创建User实体方法定义，在src/main/resources下创建文件夹mapper，然后创建UserMapper.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
	PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	
	<!-- mapper根标签 namespace命名空间   唯一 -->
	<mapper namespace="UserMapper">
	<!-- 查询id标识(唯一) resultType 返回类型 -->
		<select id="selectUser" resultType="com.liantao.pojo.User">
			select * from t_user where id = #{id}
		</select>
	</mapper>
```

#### 7、在main/java下创建com.liantao.mybatis包，再创建MyBatisDemo.java
```java
package com.liantao.mybatis;

import java.io.IOException;
import java.io.InputStream;
 
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
 
import com.liantao.pojo.User;
 
public class MybatisDemo {
	public static void main(String[] args) throws IOException {
		//mybatis配置文件    默认路径org/mybatis/example/mybatis-config.xml
		String resource = "mybatis-config.xml";
		//读取配置文件信息
		InputStream is = Resources.getResourceAsStream(resource );
		//构件SqlSessionFactory
		SqlSessionFactory sf = new SqlSessionFactoryBuilder().build(is);
		//获取sqlSession
		SqlSession session = sf.openSession();
		try {
			  //参数1  标识要寻找的statement对象  即UserMapper.xml    参数2 标识要传入的参数
			  User user = (User) session.selectOne("UserMapper.selectUser", 1);
			  System.out.println(user);
		} finally {
		   //关闭sqlSession
		   session.close();
		}
	}
}

```
### 运行测试：
[![MyBatis01](https://i.screenshot.net/4jj6vsk "MyBatis01")](https://i.screenshot.net/4jj6vsk "MyBatis01")


**每天进步一点点！**:running:



