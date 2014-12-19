---
layout: post
category: "manven"
title: "Manven构建基本步骤"
tags: ["manven"]
---
####主要步骤
1, download and install maven。  
2, mvn archetype:create -DgroupId=com.mycompany.app -DartifactId=my-app 创建新工程。  
3, mvn package 将代码打包到输出目录，一般在target下面。  
4, mvn clean 清理target目录。  
5, mvn install 将打包好的jar包安装到本地库中，一般没默认是在用户目录下的.m2\目录。  

####报错
eclipse 提示tools.jar找不到，则检查下jre环境。  

####附pom.xml主要结构：

	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	  <modelVersion>4.0.0</modelVersion>

	  <groupId>com.youth168.maventest</groupId>
	  <artifactId>my-maven-app</artifactId>
	  <version>1.0-SNAPSHOT</version>
	  <packaging>jar</packaging>

	  <name>my-maven-app</name>
	  <url>http://maven.apache.org</url>

	  <properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	  </properties>

	  <dependencies>
		<dependency>
		  <groupId>junit</groupId>
		  <artifactId>junit</artifactId>
		  <version>{latestVersion}</version>
		  <scope>test</scope>
		</dependency>
	  </dependencies>
	</project>
	

（完~）
