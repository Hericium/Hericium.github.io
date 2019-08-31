---
title: 系列教程javao2o商城之（三）mybatisgenerator及配置验证
date: 2019-08-27 15:05:25
tags: Java主流技术栈SSM+SpringBoot商铺系统
---
>MyBatis Generator（MBG）是MyBatis MyBatis 和iBATIS的代码生成器。它将为所有版本的MyBatis以及版本2.2.0之后的iBATIS版本生成代码。它将内省数据库表（或许多表），并将生成可用于访问表的工件。这减少了设置对象和配置文件以与数据库表交互的初始麻烦。MBG寻求对简单CRUD（创建，检索，更新，删除）的大部分数据库操作产生重大影响。您仍然需要为连接查询或存储过程手动编写SQL和对象代码。

## 1.mybatis generator安装使用

### 1.pom.xml引入
```
    <plugin>
      <groupId>org.mybatis.generator</groupId>
      <artifactId>mybatis-generator-maven-plugin</artifactId>
      <version>1.3.2</version>
      <configuration>
          <verbose>true</verbose>
          <overwrite>true</overwrite>
      </configuration>
      <executions>
          <execution>
              <id>Generate MyBatis Artifacts</id>
              <goals>
                  <goal>generate</goal>
              </goals>
          </execution>
      </executions>
  </plugin>
```

### 2. 在src/main/resources下新增 generatorConfig.xml 文件
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <properties resource="jdbc.properties"/>
    <!-- 数据库驱动 -->
    <classPathEntry location="/Users/beast/.m2/repository/mysql/mysql-connector-java/5.0.8/mysql-connector-java-5.0.8.jar" />
    <context id="DB2Tables" targetRuntime="MyBatis3">
        <commentGenerator>
            <property name="suppressDate" value="true" />
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
            <property name="suppressAllComments" value="true" />
        </commentGenerator>
        <!--数据库链接URL，用户名、密码 -->
        <jdbcConnection driverClass="${jdbc.driver}"
                        connectionURL="${jdbc.url}" userId="${jdbc.username}" password="${jdbc.password}">
        </jdbcConnection>
        <!-- 默认false，把JDBC DECIMAL 和 NUMERIC 类型解析为 Integer true，把JDBC DECIMAL 和
            NUMERIC 类型解析为java.math.BigDecimal -->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>
        <!-- 生成模型的包名和位置 -->
        <javaModelGenerator targetPackage="wang.beastxw.javao2o.entity"
                            targetProject="src/main/java">
            <!-- enableSubPackages:是否让schema作为包的后缀 -->
            <property name="enableSubPackages" value="true" />
            <!-- 从数据库返回的值被清理前后的空格 -->
            <property name="trimStrings" value="true" />
        </javaModelGenerator>
        <!-- 生成映射文件的包名和位置XML文件 -->
        <sqlMapGenerator targetPackage="resources/mapper"
                         targetProject="src/main">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>
        <!-- 生成DAO的包名和位置 -->
        <javaClientGenerator type="XMLMAPPER"
                             targetPackage="wang.beastxw.javao2o.dao" targetProject="src/main/java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>
        <!-- 要生成哪些表 -->
        <!-- tableName:用于自动生成代码的数据库表；domainObjectName:对应于数据库表的javaBean类名 -->
        <!--tb_area数据库表明-->                  <!--别名Book_Info  pojo（实体类明）-->
        <!-- 配置数据库中的表(%表示所有表)，不生成Example类 -->
        <table tableName="tb_area"
               domainObjectName="Area"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               selectByExampleQueryId="false"></table>
    </context>
</generatorConfiguration>
```
`其中classPathEntry的值是数据库驱动的地址对应maven里面的jar包，不过这里因为mysql驱动的问题(否则会一直提示找不到主键)，要降版本，上一节mysql-connector-java的版本是8.多的，降成现在这个。并且把jdbc.properties换成jdbc.driver=com.mysql.jdbc.Driver`
### 3.使用
#### 1.添加maven配置
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190827152049.png)
#### 2.输入 mybatis-generator:generate -e
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190827152111.png)

## 2.验证配置
### 1.创建地区表
```
CREATE TABLE `tb_area` (
  `area_id` int(2) NOT NULL AUTO_INCREMENT,
  `area_name` varchar(200) NOT NULL,
  `priority` int(2) NOT NULL DEFAULT '0',
  `create_time` datetime DEFAULT NULL,
  `last_edit_time` datetime DEFAULT NULL,
  PRIMARY KEY (`area_id`),
  UNIQUE KEY `UK_AREA` (`area_name`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;
```
### 2.点击之前配置的maven
### 3.你会发现mybatis generator 会自动生成 entity dao map 文件，是不是爽的飞起，不用自己写maper.xml了
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190827154529.png)
### 4.测试一个返回列表（因为mybatis generator不会自动生成查询所有数据的mybatis，所以自己写一个）
#### 1.在dao层的AreaMapper里面添加 `queryAreaList`这个方法
```
package wang.beastxw.javao2o.dao;

import wang.beastxw.javao2o.entity.Area;

import java.util.List;

public interface AreaMapper {
    List<Area> queryAreaList();

    int deleteByPrimaryKey(Integer areaId);

    int insert(Area record);

    int insertSelective(Area record);

    Area selectByPrimaryKey(Integer areaId);

    int updateByPrimaryKeySelective(Area record);

    int updateByPrimaryKey(Area record);
}
```
#### 2.在mapper的AreaMapper.xml下添加
```
<select id="queryAreaList" resultType="wang.beastxw.javao2o.entity.Area">
    SELECT
    <include refid="Base_Column_List" />
    From tb_area
    ORDER BY priority
    DESC
  </select>
```

### 5.写测试类
#### 1.新建文件如下
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190827182000.png)

#### 2.BaseTest

```
package wang.beastxw.javao2o;

import org.junit.runner.RunWith;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

/**
 * 配置spring 和 junit 整合 ， junit 启动时加载springIOC 容器
 */

@RunWith(SpringJUnit4ClassRunner.class)
// 告诉 junit spring 配置文件在哪里
@ContextConfiguration({"classpath:spring/spring-dao.xml","classpath:spring/spring-service.xml"})
public class BaseTest {

}
```
#### 3.AreaDaoTest

`先在数据库里tb_area这个表里增加一点数据`
```
package wang.beastxw.javao2o.dao;

import org.junit.Test;
import org.springframework.beans.factory.annotation.Autowired;
import wang.beastxw.javao2o.BaseTest;
import wang.beastxw.javao2o.entity.Area;

import java.util.List;

public class AreaDaoTest extends BaseTest {
    @Autowired
    AreaMapper areaMapper;

    @Test
    public void TestQueryAreaList() {
        List<Area> areaList = areaMapper.queryAreaList();
    }
}
```
#### 4.点击debug 看数据是不是和数据库里一致

![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190827182615.png)


## 3.源码
uri: https://github.com/Hericium/javao2o
分支: feature/startmvc

## 4.添加群聊一起学习(698615299)！
![](https://pxw-my.oss-cn-hangzhou.aliyuncs.com/blog/20190823103757.png)