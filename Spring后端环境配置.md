# web后端环境配置
## 安装intellij
## 安装mysql和mysql workbench
建议使用workbench进行连接，这种方式可视化效果更好
## maven安装
### 下载地址
http://maven.apache.org/download.cgi
### idea配置maven
file-settings（Mac-preferences 或者直接在help里搜索）
build，execution，deployment->build tools->maven
### 创建springboot项目
选择spring initializr填写项目信息

Sql里面勾选jpa和mysql

Maven进行依赖管理会自动下载链接mysql所需要的jar
### 连接数据库
在右侧的一排按钮点击database进行连接 可以使用testconnection看是否连接成功

## tomcat安装
### 下载地址
http://tomcat.apche.org/
### idea中配置tomcat
在tomcat中填写下载目录

 
