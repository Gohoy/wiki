## Maven 构建bug记录

## 1. 

#### [Failure to transfer org.springframework.boot:spring-boot-starter-parent:pom:2.0.1.RELEASE from https://repo.maven.apache.org/maven2 was cached in the local repository, resolution will not be reattempt](https://www.cnblogs.com/newcaoguo/p/8825142.html)

**即打开终端，进入出错项目的根目录，然后使用 maven bin 目录下的 mvn 编译一下，完成之后右键项目 Maven——Update Project 即可。**