# WTE项目开发文档

## 一.项目介绍

## 二.开发相关软件介绍

### 1.项目模块设计

​	MindMaster：一款流程图或脑图设计工具

​	ProcessOn：在线作图工具，可以用来制作思维导图和流程图，地址：https://www.processon.com

### 2.数据库相关

​	模型设计软件：PDMAN（轻量），PowerDesigner

​	数据库连接工具：Navicat

​	Redis连接工具：RedisDesktopManager

​	MongoDB连接工具：Robomongo

### 3.文档编辑

​	Typora：平时用来写文章的Markdown编辑器，编辑与预览二合一，界面简洁且功能强大！

​	Markdown Nice：支持自定义样式的在线Markdown编辑器，地址：https://mdnice.com/

​	Notepad++：文本编辑器，支持多种语言

### 4.代码开发软件

​	IDEA

​	IDEA插件：

​		Codota：官网https://www.codota.com/，Codota 是一款优秀的 AI 代码自动完成工具，可以帮助我们极大的提高开发效率。

​		Lombox：

​		Free Mybatis plugins：根据Mapper中定义的接口，自动在xml文件生成对应的xml接口配置；支持在接口和xml文件之间跳转

​		Mybatis Log plugin：这款插件可以把Mybatis输出的SQL日志还原成完整的SQL语句。

​		MybatisX：功能基本同Free Mybatis plugins，两者不能同时使用

​		Maven Helpler：解决Maven依赖冲突的好帮手，可以快速查找项目中的依赖冲突，并予以解决！

​		RestfulToolkit：一套 RESTful 服务开发辅助工具集

​		Statistic：一款代码统计工具，可以用来统计当前项目中代码的行数和大小。

### 5.接口调试工具

​	EOLINKER：接口文档设计及测试工具

​	POSTMAN：接口测试工具

### 6.其他工具软件

​	Snipaste：截屏软件

​	ScreenToGif：录屏软件

​	X-shell：一款强大的安全终端模拟软件，可以用来连接和管理远程Linux服务器。

​	Iconfont：阿里巴巴矢量图标库，可以根据关键字搜索的图标库。地址：https://www.iconfont.cn/

​	稿定设计：在线抠图、编辑图片、在线PS。地址：https://www.gaoding.com

​	Pexels：一个提供海量共享图片素材的网站。地址：https://www.pexels.com/zh-tw/

​	Tinypng：图片无损压缩网站。地址：https://tinypng.com/

​	Docsmall：不仅仅能压缩图片的压缩网站，还支持GIF、PDF的压缩。地址：https://docsmall.com/

​	Markmap-lib：Markdown笔记转思维导图工具。地址：https://markmap.js.org/

​	Shields：徽章制作工具。地址：https://shields.io/

​	小码短连接：简单易用的渠道短链接统计工具，可以有效缩短访问链接长度，看起来更美观，还可以统计链接访问次数，非常方便！地址：https://xiaomark.com/

## 二.项目环境

### 1.项目版本控制

​	采用git进行项目的版本控制

​	github地址：

​	用户名：xyh_longying

​	密码：c***l_1***9

​	token：d0bf4e6cdb91932ad675a7ddea3d841cd94f75a2

​	项目wte-base地址(master)：https://github.com/xyh-longying/wte-base.git

### 2.项目应用技术

​	JDK：1.8

​	数据库：mysql

​	框架：springboot 2.4.1、mybatis-plus 3.3.2

​	API文档生成：swagger 3.0，knife4j 2.0.4

​	工具类：hutool 4.6.3

## 三.项目结构框架搭建

### 1.wte-base项目搭建

​	提供基础数据实体类和数据库CRUD操作，项目打包成jar发布到私服，提供给其他的微服务项目使用。

​	项目基础框架：springboot、mybatis-plus

#### (1) 项目结构：

![image-20210115112340411](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210115112340411.png)

#### (2) 项目示例代码：

##### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.1</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.wt</groupId>
    <artifactId>wte-base</artifactId>
    <version>1.0.0</version>
    <name>wte-base</name>
    <description>The base data entity and base CRUD for the WTE.</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <!--SpringBoot通用依赖模块-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--Mybatis-Plus依赖-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.3.2</version>
        </dependency>
        <!--Mybatis-Plus代码生成器-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.3.2</version>
        </dependency>
        <!--Velocity模板生成引擎-->
        <dependency>
            <groupId>org.apache.velocity</groupId>
            <artifactId>velocity-engine-core</artifactId>
            <version>2.2</version>
        </dependency>
        <!--集成druid连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--Mysql数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.15</version>
        </dependency>
        <!-- hutool工具包-->
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>4.6.3</version>
        </dependency>
        <!--lombok依赖-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <!--springfox swagger官方Starter-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
    </dependencies>

    <!-- 发布jar包到私服 -->
    <distributionManagement>
        <repository>
            <id>releases</id>   <!-- 对应私服的releases仓库 -->
            <url>http://localhost:8081/repository/maven-releases/</url>
        </repository>
        <snapshotRepository>
            <id>snapshots</id>  <!-- 对应私服的snapshots仓库 -->
            <url>http://localhost:8081/repository/maven-snapshots/</url>
        </snapshotRepository>
    </distributionManagement>

    <build>
        <finalName>${project.artifactId}</finalName>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <!--防止打包生成的jar包包含BOOT-INF文件夹-->
                <configuration>
                    <skip>true</skip>
                </configuration>
            </plugin>
            <!--在这里修改版本-->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.4.3</version>
            </plugin>
        </plugins>
    </build>
</project>

```

##### generator.properties

```properties
dataSource.driverName=com.mysql.cj.jdbc.Driver
dataSource.url=jdbc:mysql://localhost:3306/wte_dev?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
dataSource.username=root
dataSource.password=root
package.base=com.wt.wte.wtebase.modules
```

##### MybatisConfig.java

```java
package com.wte.wtebase.config;

/**
 * Create by chenglong on 2021/1/11
 */
@Configuration
@MapperScan({"com.wt.wte.wtebase.modules.*.mapper"})
public class MybatisConfig {

    @Bean
    public PaginationInterceptor paginationInterceptor(){
        PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
        paginationInterceptor.setCountSqlParser(new JsqlParserCountOptimize(true));
        return paginationInterceptor;
    }
}

```

##### MybatisPlusGenerator.java

```java
package com.wte.wtebase.generator;

/**
 * MybatisPlus代码生成器
 * Create by chenglong on 2021/1/12
 */
public class MybatisPlusGenerator {
    public static void main(String[] args) {
        String projectPath = System.getProperty("user.dir");
        String moduleName = scanner("模块名");
        String[] tableNames = scanner("表名，多个英文逗号分割").split(",");
        //代码生成器
        AutoGenerator autoGenerator = new AutoGenerator();
        autoGenerator.setGlobalConfig(initGlobalConfig(projectPath));
        autoGenerator.setDataSource(initDataSourceConfig());
        autoGenerator.setPackageInfo(initPackageConfig(moduleName));
        autoGenerator.setCfg(initInjectionConfig(projectPath,moduleName));
        autoGenerator.setTemplate(initTemplateConfig());
        autoGenerator.setStrategy(initStrategyConfig(tableNames));
        autoGenerator.setTemplateEngine(new VelocityTemplateEngine());
        autoGenerator.execute();
    }

    /**
     * 读取控制台内容信息
     * @param tip
     * @return
     */
    private static String scanner(String tip) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入"+tip+":");
        if(scanner.hasNext()){
            String next = scanner.next();
            if(StrUtil.isNotEmpty(next)){
                return next;
            }
        }
        throw new MybatisPlusException("请输入正确的"+tip+"!");
    }

    /**
     * 初始化全局配置
     * @param projectPath
     * @return
     */
    private static GlobalConfig initGlobalConfig(String projectPath){
        GlobalConfig globalConfig = new GlobalConfig();
        globalConfig.setOutputDir(projectPath+"/src/main/java");
        globalConfig.setAuthor("chenglong");
        globalConfig.setOpen(false);
        globalConfig.setSwagger2(true);
        globalConfig.setBaseResultMap(true);
        globalConfig.setFileOverride(true);
        globalConfig.setDateType(DateType.ONLY_DATE);
        globalConfig.setEntityName("%s");
        globalConfig.setMapperName("%sMapper");
        globalConfig.setXmlName("%sMapper");
        globalConfig.setServiceName("%sService");
        globalConfig.setServiceImplName("%sServiceImpl");
        globalConfig.setControllerName("%sController");
        return globalConfig;
    }

    /**
     * 初始化数据源配置
     * @return
     */
    private static DataSourceConfig initDataSourceConfig(){
        Props props = new Props("properties/generator.properties");
        DataSourceConfig dataSourceConfig = new DataSourceConfig();
        dataSourceConfig.setUrl(props.getStr("dataSource.url"));
        dataSourceConfig.setDriverName(props.getStr("dataSource.driverName"));
        dataSourceConfig.setUsername(props.getStr("dataSource.username"));
        dataSourceConfig.setPassword(props.getStr("dataSource.password"));
        return dataSourceConfig;
    }

    /**
     * 初始化包配置
     * @param moduleName
     * @return
     */
    private static PackageConfig initPackageConfig(String moduleName){
        Props props = new Props("properties/generator.properties");
        PackageConfig packageConfig = new PackageConfig();
        packageConfig.setModuleName(moduleName);
        packageConfig.setParent(props.getStr("package.base"));
        packageConfig.setEntity("model");
        return packageConfig;
    }

    /**
     * 初始化自定义配置
     * @param projectPath
     * @param moduleName
     * @return
     */
    private static InjectionConfig initInjectionConfig(String projectPath, String moduleName){
        //自定义配置
        InjectionConfig injectionConfig = new InjectionConfig() {
            @Override
            public void initMap() {
                //可自定义属性
            }
        };
        //模板引擎是Velocity
        String templatePath = "/templates/mapper.xml.vm";
        //自定义输出配置
        List<FileOutConfig> focList = new ArrayList<>();
        //自定义配置会被优先输出
        focList.add(new FileOutConfig(templatePath) {
            @Override
            public String outputFile(TableInfo tableInfo) {
                return projectPath+"/src/main/resources/mapper/"+moduleName+"/"+tableInfo.getEntityName()+ StringPool.DOT_XML;
            }
        });
        injectionConfig.setFileOutConfigList(focList);
        return injectionConfig;
    }

    /**
     * 初始化模板配置
     * @return
     */
    private static TemplateConfig initTemplateConfig(){
        TemplateConfig templateConfig = new TemplateConfig();
        //可以对controller、service、entity模板进行配置
        templateConfig.setEntity("templates/entity.java");
        templateConfig.setMapper("templates/mapper.java");
        templateConfig.setController("templates/controller.java");
        templateConfig.setService("templates/service.java");
        templateConfig.setServiceImpl("templates/serviceImpl.java");
        //mapper.xml模板需单独配置
        templateConfig.setXml(null);
        return templateConfig;
    }

    /**
     * 初始化策略配置
     * @param tableNames
     * @return
     */
    private static StrategyConfig initStrategyConfig(String[] tableNames){
        StrategyConfig strategyConfig = new StrategyConfig();
        strategyConfig.setNaming(NamingStrategy.underline_to_camel);
        strategyConfig.setColumnNaming(NamingStrategy.underline_to_camel);
        strategyConfig.setEntityLombokModel(true);
        strategyConfig.setRestControllerStyle(true);
        //当表中带*号时可以开启通配符模式
        if(tableNames.length==1 && tableNames[0].contains("*")){
            String[] likeStr = tableNames[0].split("_");
            String likePrefix = likeStr[0] + "_";
            strategyConfig.setLikeTable(new LikeTable(likePrefix));
        } else {
            strategyConfig.setInclude(tableNames);
        }
        return strategyConfig;
    }
}

```

#### (3) 项目打包发布私服：

- 下载nexus，下载地址：https://www.sonatype.com/download-oss-sonatype

- 安装nexus，nexus-3.29.2-02-win64.zip解压，配置环境变量

  ![img](https://img2018.cnblogs.com/blog/398358/201907/398358-20190716104115113-1259525638.png)

  运行![img](https://img2018.cnblogs.com/blog/398358/201907/398358-20190716104140560-1608003030.png)

- 登录nexus，访问：http://127.0.0.1:8081，用户名admin，密码admin123

  ![image-20210113115339231](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210113115339231.png)

- 修改setting.xml

  ```xml
  <servers>
  	<server>
        <id>releases</id>
        <username>admin</username>
        <password>admin123</password>
      </server>
      
      <server>
        <id>snapshots</id>
        <username>admin</username>
        <password>admin123</password>
      </server>
  </servers>
  ```

- 修改pom.xml

  ```xml
  <!-- 发布jar包到私服 -->
  <distributionManagement>
      <repository>
          <id>releases</id>   <!-- 对应私服的releases仓库 -->
          <url>http://localhost:8081/repository/maven-releases/</url>
      </repository>
      <snapshotRepository>
          <id>snapshots</id>  <!-- 对应私服的snapshots仓库 -->
          <url>http://localhost:8081/repository/maven-snapshots/</url>
      </snapshotRepository>
  </distributionManagement>
  ```

- 运行maven的deploy命令，自动将wte-base项目打包到私服上

  ![image-20210115112505247](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210115112505247.png)

- 参考文档：https://www.cnblogs.com/knowledgesea/p/11190579.html

- 参考文档：https://blog.csdn.net/q42368773/article/details/108413339

- 参考文档：https://www.cnblogs.com/he-blog/p/6640904.html

### 2.wte-front-api项目搭建

​	wte-front-api为多模块项目，其中包含用户、商品、订单等多个子项目模块，为了便于多模块的依赖统一管理，需创建一个名为front-api-parent的父模块，其余子模块集成该父模块。

#### (1)front-api-parent项目的pom.xml		

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.1</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <groupId>com.wte</groupId>
    <artifactId>front-api-parent</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>

    <modules>
        <module>front-api-user</module>
    </modules>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
        <!--从私服引入wte-base基础数据服务-->
        <dependency>
            <groupId>com.wt</groupId>
            <artifactId>wte-base</artifactId>
            <version>1.0.0</version>
        </dependency>
        <!--SpringBoot通用依赖模块-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--Mybatis-Plus依赖-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.3.2</version>
        </dependency>
        <!--集成druid连接池-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--Mysql数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.15</version>
        </dependency>
        <!-- hutool工具包-->
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>4.6.3</version>
        </dependency>
        <!--lombok依赖-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <!--springfox swagger官方Starter-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
        <!--整合Knife4j-->
        <dependency>
            <groupId>com.github.xiaoymin</groupId>
            <artifactId>knife4j-spring-boot-starter</artifactId>
            <version>3.0.2</version>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <!--从私服下载依赖jar-->
    <repositories>
        <repository>
            <id>nexus</id>
            <url>http://localhost:8081/repository/maven-releases/</url>
            <layout>default</layout>
            <releases>
                <enabled>true</enabled><!-- 允许从仓库中下载releases的jar包 -->
            </releases>
            <snapshots>
                <enabled>true</enabled><!-- 允许从仓库中下载snapshots的jar包 -->
                <!-- 每次都会到私服中对比jar包是否发生了改变，若改变则下载最新的jar包都本地仓库；每次上传snapshots的jar包时都会有一个时间戳，因为snapshots是不稳定的随时都可能修改从新发布，所以这里需要配置成always，默认是：daily，每天更新 -->
                <updatePolicy>always</updatePolicy>
            </snapshots>
        </repository>
    </repositories>
</project>
```

#### (2)front-api-user项目

##### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.wte</groupId>
        <artifactId>front-api-parent</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <groupId>com.wte</groupId>
    <artifactId>front-api-user</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>front-api-user</name>
    <description>WTE前端接口-用户模块</description>

</project>
```

##### application.yml

```yaml
spring:
  application:
    name: front-api-user
  profiles:
    active: dev
```

##### application-dev.yml

```yaml
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/wte_dev?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
    username: root
    password: root
    driver-class-name: com.mysql.cj.jdbc.Driver
springfox:
  documentation:
    enabled: true #是否启用swagger
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl #用于打印mybatis sql 日志
```

##### application-test.yml

```yaml
server:
  port: 8080
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/wte_test?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
    username: root
    password: root
    driver-class-name: com.mysql.cj.jdbc.Driver
springfox:
  documentation:
    enabled: false
```

##### swagger.properties

创建swagger.properties，提供swagger相关参数

```properties
title=WTE FRONT USER API
description=WTE前端用户模块API文档
contactName=程龙
contactUrl=http://www.baidu.com
contactEmail=xyh_longying@qq.com
version=1.0
```

##### Swagger3Config.java

创建Swagger3Config配置类

```java
package com.wte.frontapiuser.config;

/**
 * Create by chenglong on 2021/1/14
 */
@Configuration
@EnableOpenApi
@EnableKnife4j
public class Swagger3Config {

    private static Props SWAGGER = Props.getProp("properties/swagger.properties");

    @Bean
    public Docket createRestApi(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.wte.frontapiuser.controller"))
                .paths(PathSelectors.any())
                .build();
    }

    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
                .title(SWAGGER.getStr("title"))
                .description(SWAGGER.getStr("description"))
                .contact(new Contact(SWAGGER.getStr("contactName"), SWAGGER.getStr("contactUrl"), SWAGGER.getStr("contactEmail")))
                .version(SWAGGER.getStr("version"))
                .build();
    }
}
```

##### 修改启动类FrontApiUserApplication

```java
package com.wte.frontapiuser;

/**
 * scanBasePackages增加扫描路径，方便注入bean
 */
@SpringBootApplication(scanBasePackages = {"com.wte.frontapiuser","com.wt.wte.wtebase"})
public class FrontApiUserApplication {

    public static void main(String[] args) {
        SpringApplication.run(FrontApiUserApplication.class, args);
    }

}
```

##### 接口AccountController.java

```java
package com.wte.frontapiuser.controller;

import com.wt.wte.wtebase.common.api.ApiException;
import com.wt.wte.wtebase.common.api.CommonResult;
import com.wte.frontapiuser.service.AccountService;
import com.wte.frontapiuser.service.ValidService;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import io.swagger.annotations.ApiParam;
import lombok.NonNull;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

/**
 * Create by chenglong on 2021/1/14
 */
@Api(tags = "[0101]账号管理")
@Slf4j
@RestController
@RequestMapping("/frontapi/account")
public class AccountController {
    @Autowired
    private ValidService validService;
    @Autowired
    private AccountService accountService;

    @ApiOperation(value = "[01010101]生成图形验证码接口")
    @RequestMapping(value = "imageCode/create",method = RequestMethod.GET)
    public CommonResult createImgCode(){
        try {
            return CommonResult.success(validService.generateImageCode());
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }

    @ApiOperation(value = "[01010102]校验图形验证码接口")
    @RequestMapping(value = "imageCode/valid",method = RequestMethod.GET)
    public CommonResult validImgCode(@RequestParam(value = "code") @NonNull @ApiParam("验证码") String code,
                                     @RequestParam(value = "uuid") @NonNull @ApiParam("验证码标识") String uuid){
        try {
            return CommonResult.success(validService.validImageCode(uuid,code));
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }

    @ApiOperation(value = "[01010103]生成短信验证码接口")
    @RequestMapping(value = "msgCode/create",method = RequestMethod.GET)
    public CommonResult createMsgCode(@RequestParam(value = "phoneNum") @NonNull @ApiParam("手机号") String phoneNum,
                                      @RequestParam(value = "type") @NonNull @ApiParam("作用类型") String type){
        try {
            return CommonResult.success(validService.generateMsgCode(type,phoneNum));
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }

    @ApiOperation(value = "[01010104]校验短信验证码接口")
    @RequestMapping(value = "msgCode/valid",method = RequestMethod.GET)
    public CommonResult validMsgCode(@RequestParam(value = "phoneNum") @NonNull @ApiParam("手机号") String phoneNum,
                                      @RequestParam(value = "code") @NonNull @ApiParam("验证码") String code){
        try {
            return CommonResult.success(validService.validMsgCode(phoneNum,code));
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }

    @ApiOperation(value = "[01010201]校验用户名是否已注册接口")
    @RequestMapping(value = "username/unique/valid",method = RequestMethod.GET)
    @ResponseBody
    public CommonResult validUsernameUnique(@RequestParam(value = "username") @NonNull @ApiParam("用户名") String username){
        try {
            return CommonResult.success(accountService.validUsernameUnique(username));
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }

    @ApiOperation(value = "[01010202]注册用户接口")
    @RequestMapping(value = "user/create",method = RequestMethod.POST)
    @ResponseBody
    public CommonResult registUser(@RequestParam(value = "username") @NonNull @ApiParam("用户名") String username,
                               @RequestParam(value = "password") @NonNull @ApiParam("密码") String password){
        try {
            return CommonResult.success(accountService.createNewUser(username,password));
        } catch (ApiException e){
            return CommonResult.failed(e);
        }
    }
}

```

创建AccountService和AccountServiceImpl，实现调用数据访问接口获取数据，此处省略该代码。

##### 启动项目

启动项目成功后，访问knife4j接口文档地址http://localhost:8080/doc.html#/home，即可查看接口文档

swgger3接口访问地址：http://localhost:8080/swagger-ui/

#### (3)springboot使用AOP记录接口访问日志

新增ApiLogAspect切面应用，为所有接口Controller增加接口访问日志输出

```java
package com.wte.frontapiuser.component;


/**
 * 统一日志处理切面
 * Create by chenglong on 2021/1/15
 */
@Aspect
@Component
@Order(1)
public class ApiLogAspect {
    private static final Logger LOGGER = LoggerFactory.getLogger(ApiLogAspect.class);

    @Pointcut("execution(public * com.wte.frontapiuser.controller.*.*(..))")
    public void apiLog(){
    }

    @Before(value = "apiLog()")
    public void doBefore(JoinPoint joinPoint) throws Throwable{
    }

    @AfterReturning(value = "apiLog()", returning = "ret")
    public void doAfterReturning(Object ret) throws Throwable{
    }

    @Around(value = "apiLog()")
    public Object doAround(ProceedingJoinPoint pjp) throws Throwable{
        //获取当前请求对象
        ServletRequestAttributes requestAttributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        HttpServletRequest request = requestAttributes.getRequest();
        String urlStr = request.getRequestURL().toString();
        Date startTime = DateUtil.date();//记录开始时间
        Object result = pjp.proceed();
        Date endTime = DateUtil.date();
        ApiLog apiLog = new ApiLog();
        MethodSignature methodSignature = (MethodSignature) pjp.getSignature();
        Method method = methodSignature.getMethod();
        if(method.isAnnotationPresent(ApiOperation.class)){
            ApiOperation apiOperation = method.getAnnotation(ApiOperation.class);
            apiLog.setDescription(apiOperation.value());
        }
//        apiLog.setUsername();
        apiLog.setStartTime(DateUtil.formatDateTime(startTime));
        apiLog.setBasePath(StrUtil.removeSuffix(urlStr, URLUtil.url(urlStr).getPath()));
        apiLog.setIp(request.getRemoteUser());
        apiLog.setUri(request.getRequestURI());
        apiLog.setUrl(urlStr);
        apiLog.setSpendTime((int) (endTime.getTime()-startTime.getTime())+"ms");
        apiLog.setResult(result);
        apiLog.setMethod(request.getMethod());
        apiLog.setParameter(getParameter(method,pjp.getArgs()));
        LOGGER.info("{}", JSONUtil.toJsonPrettyStr(JSONUtil.parse(apiLog)));
        return result;
    }

    /**
     * 根据方法和传入的参数获取请求参数
     * @param method
     * @param args
     * @return
     */
    private Object getParameter(Method method, Object[] args) {
        List<Object> argList = new ArrayList<>();
        Parameter[] parameters = method.getParameters();
        for(int i=0;i<parameters.length;i++){
            RequestBody requestBody = parameters[i].getAnnotation(RequestBody.class);
            if(requestBody!=null){
                argList.add(args[i]);
            }
            RequestParam requestParam = parameters[i].getAnnotation(RequestParam.class);
            if(requestParam!=null){
                Map<String,Object> map = new HashMap<>();
                String key = parameters[i].getName();
                if(StrUtil.isNotEmpty(requestParam.value())){
                    key = requestParam.value();
                }
                map.put(key, args[i]);
                argList.add(map);
            }
        }
        if(argList.size()==0){
            return null;
        }else if(argList.size()==1){
            return argList.get(0);
        }else {
            return argList;
        }
    }

}
```

#### (4)自定义异常类

自定义异常

```java
package com.wt.wte.wtebase.common.api;

import cn.hutool.core.map.MapUtil;
import cn.hutool.setting.dialect.Props;
import lombok.Data;

import java.util.Map;

/**
 * Create by chenglong on 2021/1/19
 */
@Data
public class ApiException extends RuntimeException {

    public static Props props = Props.getProp("properties/apiException.properties");

    private String name;
    private String code;
    private String message;

    public ApiException(String name, Map<String,String> placeHolder){
        this.name = name;
        this.code = props.getStr(name).split(":")[0];
        String msg = props.getStr(name).split(":")[1];
        if(MapUtil.isNotEmpty(placeHolder)){
            placeHolder.forEach((k,v)->{
                this.message = msg.replaceAll("\\$\\{"+k+"\\}", v);
            });
        } else {
            this.message = msg;
        }
    }

    public ApiException(String name, String message, Map<String,String> placeHolder){
        this.name = name;
        this.code = props.getStr(name).split(":")[0];
        if(MapUtil.isNotEmpty(placeHolder)){
            placeHolder.forEach((k,v)->{
                this.message = message.replaceAll("\\$\\{"+k+"\\}", v);
            });
        } else {
            this.message = message;
        }
    }
}

```

自定义异常使用示例：

```java
/**
 * 校验用户名是否唯一
 * @param username
 */
private void validUniqueUsername(String username) {
    QueryWrapper<UmsUser> wrapper = new QueryWrapper<>();
    wrapper.lambda()
            .eq(UmsUser::getIsDelete, BaseConstants.DEL_NO)
            .eq(UmsUser::getUsername,username);
    Integer countNum = umsUserService.count(wrapper);
    if(countNum>0){
        throw new ApiException(ExceptionConstants.USERNAME_NOT_UNIQUE, MapUtil.of("username", username));
    }
}
```

#### (5)集成Redis存放图形验证码

pom文件增加redis依赖

```xml
<!--redis依赖配置-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

application-***.yml增加redis配置

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/wte_dev?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
    username: root
    password: root
    driver-class-name: com.mysql.cj.jdbc.Driver
  redis:
    host: 127.0.0.1 # Redis服务器地址
    database: 0 # Redis数据库索引（默认为0）
    port: 6379 # Redis服务器连接端口
    password: 123456 # Redis服务器连接密码（默认为空）
    jedis:
      pool:
        max-active: 8 # 连接池最大连接数（使用负值表示没有限制）
        max-idle: 8 # 连接池中的最大空闲连接
        min-idle: 0 # 连接池中的最小空闲连接
        max-wait: -1ms # 连接池最大阻塞等待时间（使用负值表示没有限制）
    timeout: 3000ms # 连接超时时间（毫秒）
redis:
  key:
    prefix:
      imgCode: imgCode:authCode
      msgCode: msgCode:authCode
    expire:
      imgCode: 120
      msgCode: 120
```

wte-base项目新增RedisService接口

```java
package com.wt.wte.wtebase.common.service;

/**
 * Create by chenglong on 2021/1/20
 */
public interface RedisService {

    /**
     * 存储数据
     * @param key
     * @param value
     */
    void set(String key, String value);

    /**
     * 存储数据并设置过期时间
     * @param key
     * @param value
     * @param expireTime
     */
    void set(String key, String value, long expireTime);

    /**
     * 读取数据
     * @param key
     * @return
     */
    String get(String key);

    /**
     * 设置超时期限
     * @param key
     * @param expire
     * @return
     */
    boolean expire(String key, long expire);

    /**
     * 删除操作
     * @param key
     */
    void remove(String key);

    /**
     * 自增操作
     * @param key
     * @param delta
     * @return
     */
    Long increment(String key, long delta);
}
```

```java
package com.wt.wte.wtebase.common.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.stereotype.Service;

import java.util.concurrent.TimeUnit;

/**
 * Create by chenglong on 2021/1/20
 */
@Service
public class RedisServiceImpl implements RedisService {

    @Autowired
    private StringRedisTemplate redisTemplate;

    @Override
    public void set(String key, String value) {
        redisTemplate.opsForValue().set(key, value);
    }

    @Override
    public void set(String key ,String value, long expireTime){
        redisTemplate.opsForValue().set(key, value, expireTime, TimeUnit.SECONDS);
    }

    @Override
    public String get(String key) {
        return redisTemplate.opsForValue().get(key);
    }

    @Override
    public boolean expire(String key, long expire) {
        return redisTemplate.expire(key, expire, TimeUnit.SECONDS);
    }

    @Override
    public void remove(String key) {
        redisTemplate.delete(key);
    }

    @Override
    public Long increment(String key, long delta) {
        return redisTemplate.opsForValue().increment(key, delta);
    }
}
```

增加RedisConfig配置

```java
package com.wt.wte.wtebase.config;

import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.cache.CacheManager;
import org.springframework.cache.annotation.CachingConfigurerSupport;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.cache.RedisCacheWriter;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.GenericJackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.StringRedisSerializer;

/**
 * Create by chenglong on 2021/1/20
 */
@Configuration
@EnableCaching
public class RedisConfig extends CachingConfigurerSupport {
    private static final StringRedisSerializer STRING_SERIALIZER = new StringRedisSerializer();
    private static final GenericJackson2JsonRedisSerializer JACKSON__SERIALIZER = new GenericJackson2JsonRedisSerializer();

    @Bean
    public CacheManager cacheManager(RedisConnectionFactory redisConnectionFactory) {
        RedisCacheConfiguration redisCacheCfg=RedisCacheConfiguration.defaultCacheConfig()
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(STRING_SERIALIZER))
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(JACKSON__SERIALIZER));
        return RedisCacheManager.builder(RedisCacheWriter.nonLockingRedisCacheWriter(redisConnectionFactory))
                .cacheDefaults(redisCacheCfg)
                .build();
    }

    @Bean
    @ConditionalOnMissingBean(name = "redisTemplate")
    public RedisTemplate<String,Object> redisTemplate(RedisConnectionFactory factory){
        // 配置redisTemplate
        RedisTemplate<String, Object> redisTemplate = new RedisTemplate<>();
        redisTemplate.setConnectionFactory(factory);
        // key序列化
        redisTemplate.setKeySerializer(STRING_SERIALIZER);
        // value序列化
        redisTemplate.setValueSerializer(JACKSON__SERIALIZER);
        // Hash key序列化
        redisTemplate.setHashKeySerializer(STRING_SERIALIZER);
        // Hash value序列化
        redisTemplate.setHashValueSerializer(JACKSON__SERIALIZER);
        redisTemplate.afterPropertiesSet();
        return redisTemplate;
    }
}
```

生成图形验证码和校验图形验证码接口，图形验证码用CaptchaUtil工具类生成

```java
package com.wte.frontapiuser.service.impl;

import cn.hutool.captcha.CaptchaUtil;
import cn.hutool.captcha.ShearCaptcha;
import cn.hutool.core.lang.UUID;
import cn.hutool.core.map.MapUtil;
import cn.hutool.core.util.StrUtil;
import com.wt.wte.wtebase.base.BaseService;
import com.wt.wte.wtebase.common.api.ApiException;
import com.wt.wte.wtebase.common.api.ExceptionConstants;
import com.wt.wte.wtebase.common.service.RedisService;
import com.wte.frontapiuser.service.ValidService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

import java.util.Map;

/**
 * Create by chenglong on 2021/1/19
 */
@Slf4j
@Service
public class ValidServiceImpl extends BaseService implements ValidService {

    @Autowired
    private RedisService redisService;
    @Value("${redis.key.prefix.imgCode}")
    private String REDIS_KEY_IMGCODE;
    @Value("${redis.key.expire.imgCode}")
    private Long IMGCODE_EXPIRE_TIME;


    @Override
    public Map generateImageCode() {
        try {
            ShearCaptcha captcha = CaptchaUtil.createShearCaptcha(120, 40, 4, 4);
            String uuid = UUID.randomUUID().toString();
            redisService.set(REDIS_KEY_IMGCODE+uuid, captcha.getCode(), IMGCODE_EXPIRE_TIME);
            Map map = MapUtil.of(new String[][]{
                    {"uuid",uuid},
                    {"codeBase64",captcha.getImageBase64()},
            });
            return map;
        } catch (Exception e){
            log.info(Thread.currentThread().getStackTrace()[1]+"发生异常，异常信息：{}",e.getMessage());
            throw new ApiException(ExceptionConstants.GENERATE_IMGCODE_ERROR,MapUtil.of("msg", e.getMessage()));
        }
    }

    @Override
    public String validImageCode(String uuid, String code) {
        try {
            String imgCode = redisService.get(REDIS_KEY_IMGCODE+uuid);
            if(StrUtil.equals(imgCode, code)){
                redisService.remove(REDIS_KEY_IMGCODE+uuid);
                return "图形验证码正确";
            }else{
                throw new ApiException(ExceptionConstants.IMGCODE_NOT_CORRECT,null);
            }
        } catch (ApiException apiException){
            throw apiException;
        } catch (Exception e){
            log.info(Thread.currentThread().getStackTrace()[1]+"发生异常，异常信息：{}",e.getMessage());
            throw new ApiException(ExceptionConstants.VALID_IMGCODE_ERROR,MapUtil.of("msg", e.getMessage()));
        }
    }
}
```

#### (6)集成MongoBD记录生成的短信验证码

引入依赖

```xml
<!---mongodb相关依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

创建mongodb实体document

```java
package com.wt.wte.wtebase.nosql.mongodb.document;

/**
 * Create by chenglong on 2021/1/20
 */

import lombok.Builder;
import lombok.Data;
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.index.Indexed;
import org.springframework.data.mongodb.core.mapping.Document;

import java.util.Date;

@Document
@Builder
@Data
public class MsgCodeSendRecord {
    @Id
    private String id;
    @Indexed
    private String phoneNum;
    private String type;
    private String code;
    private String msg;
    private Date sendTime;
}
```

实现mongodb数据操作服务类

```java
package com.wt.wte.wtebase.nosql.mongodb.service;

import com.wt.wte.wtebase.nosql.mongodb.document.MsgCodeSendRecord;

import java.util.Date;

/**
 * Create by chenglong on 2021/1/20
 */
public interface MsgCodeSendRecordService {

    public Long countMsgCodeSendRecordsByPhoneNumLastOneMinute(String phoneNum, String type, Date now);

    public void saveMsgCodeSendRecords(MsgCodeSendRecord record);
}
```

```java
package com.wt.wte.wtebase.nosql.mongodb.service.impl;

import cn.hutool.core.date.DateUtil;
import com.wt.wte.wtebase.nosql.mongodb.document.MsgCodeSendRecord;
import com.wt.wte.wtebase.nosql.mongodb.service.MsgCodeSendRecordService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;
import org.springframework.stereotype.Service;

import java.util.Date;

/**
 * Create by chenglong on 2021/1/20
 */
@Service
public class MsgCodeSendRecordServiceImpl implements MsgCodeSendRecordService {

    @Autowired
    private MongoTemplate mongoTemplate;

    @Override
    public Long countMsgCodeSendRecordsByPhoneNumLastOneMinute(String phoneNum, String type, Date now) {
        Date beginTime = DateUtil.offsetMinute(now, -1);
        Query query = new Query(Criteria.where("phoneNum").is(phoneNum)
                .andOperator(Criteria.where("sendTime").gte(beginTime),Criteria.where("sendTime").lte(now)));
        return mongoTemplate.count(query, MsgCodeSendRecord.class);
    }

    @Override
    public void saveMsgCodeSendRecords(MsgCodeSendRecord record) {
        mongoTemplate.save(record);
    }
}
```

前端接口应用操作，将短信发送记录存入mongodb

ValidServiceImpl

```java
@Override
public String generateMsgCode(String type, String phoneNum) {
    try {
        validMsgCodeFrequency(type,phoneNum);
        removeMsgCodeCache(phoneNum);
        createAndSendMsgCodeStr(type,phoneNum);
        return "已发送短信验证码";
    } catch (ApiException apiException){
        throw apiException;
    } catch (Exception e){
        log.info(Thread.currentThread().getStackTrace()[1]+"发生异常，异常信息：{}",e.getMessage());
        throw new ApiException(ExceptionConstants.GENERATE_MSGCODE_ERROR,MapUtil.of("msg", e.getMessage()));
    }
}
/**
     * 校验短信验证码发送频率
     * @param type
     * @param phoneNum
     */
    private void validMsgCodeFrequency(String type, String phoneNum) {
        int maxNum = NumberUtil.parseInt(SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_FREQUENCY_NUM));
        long num = msgCodeSendRecordService.countMsgCodeSendRecordsByPhoneNumLastOneMinute(phoneNum, type, DateUtil.date());
        if(num > maxNum){
            log.info("手机号{}最近1分钟已频发送短信验证码超过{}次，无法再次发送",phoneNum,maxNum);
            throw new ApiException(ExceptionConstants.MSGCODE_SEND_FREQUENCY, MapUtil.of("phoneNum", phoneNum));
        }
    }

    /**
     * 移除缓存中已存在的手机验证码
     * @param phoneNum
     */
    private void removeMsgCodeCache(String phoneNum){
        String key = REDIS_KEY_MSGCODE+"_"+phoneNum;
        if(redisService.hasKey(key)){
            redisService.del(key);
        }
    }

    /**
     * 生成并发送短信验证码
     * @param type
     * @param phoneNum
     */
    private void createAndSendMsgCodeStr(String type, String phoneNum){
        String key = REDIS_KEY_MSGCODE+"_"+phoneNum;
        String msg = "";
        switch (type){
            case "1":
                msg = SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_TYPE_REGIST);
                break;
            case "2":
                msg = SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_TYPE_LOGIN);
                break;
        }
        String code = RandomUtil.randomNumbers(6);
        msg = StrUtil.replace(msg, "#CODE#", code);
        if(StrUtil.isNotEmpty(msg)){
            log.info("生成的短信验证码信息内容：{}", msg);
        }
        String expire = SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_EXPIRE);
        MsgCodeSendRecord record = MsgCodeSendRecord.builder().id(IdUtil.simpleUUID()).phoneNum(phoneNum).type(type).code(code).msg(msg).sendTime(DateUtil.date()).build();
        msgCodeSendRecordService.saveMsgCodeSendRecords(record);
        redisService.set(key, code, NumberUtil.parseLong(expire)*60);
        //TODO 调用短信发送接口发送真实短信

    }
```

![image-20210121111345611](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210121111345611.png)

#### (7)设置项目启动自动装配系统配置类

​	系统相关配置可由后台修改相应配置达到控制某些功能的参数设置，前期暂时把系统配置放在systemSettings.properties配置文件里，后期开发后台功能时可将所有配置存入数据库，由可视化界面来配置相关系统参数。

​	systemSettings.properties

```properties
#短信验证码发送频率，1分钟最多发送3次
msgCodeSendFrequencyNum = 3
#短信验证码时效，5分钟
msgCodeExpire = 5
#注册时发送短信验证码提示语
msgCodeTypeRegist = 【WTE】验证码：#CODE#，仅用于注册操作！
#登录时发送短信验证码提示语
msgCodeTypeLogin = 【WTE】验证码：#CODE#，您正在登录WTE手机账号（若非本人操作，请删除本短信）
```

SystemUtil，借助redis缓存将所有配置放入缓存中，需要用时从缓存读取；

```java
package com.wt.wte.wtebase.common.utils;

import cn.hutool.core.map.MapUtil;
import cn.hutool.core.util.StrUtil;
import cn.hutool.json.JSONObject;
import cn.hutool.json.JSONUtil;
import cn.hutool.setting.dialect.Props;
import com.wt.wte.wtebase.common.api.ApiException;
import com.wt.wte.wtebase.common.api.ExceptionConstants;
import com.wt.wte.wtebase.common.service.RedisService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.util.List;

/**
 * 系统工具
 * Create by chenglong on 2021/1/20
 */
@Component
public class SystemUtil {

    private static final String REDIS_SYSTEM_SETTINGS_KEY = "SYSTEM_SETTINGS";

    private static RedisService redisService;

    @Autowired
    public void setRedisService(RedisService redisService){
        SystemUtil.redisService = redisService;
    }

    public static String getSettingValue(String key){
        String settings = (String) redisService.get(REDIS_SYSTEM_SETTINGS_KEY);
        if(settings==null){
            throw new ApiException(ExceptionConstants.SYSTEM_SETTINGS_NULL, null);
        }
        JSONObject properties = JSONUtil.parseObj(settings);
        String value = properties.getStr(key);
        if(StrUtil.isEmpty(value)){
            throw new ApiException(ExceptionConstants.SYSTEM_SETTING_KEY_EMPTY, MapUtil.of("keyname", key));
        }
        return value;
    }

    public static void setSystemSettings(){
        Props props = Props.getProp("properties/systemSettings.properties");
        JSONObject settings = new JSONObject();
        props.forEach((key, value)->{
            settings.put((String) key, value);
        });
        redisService.set(REDIS_SYSTEM_SETTINGS_KEY, JSONUtil.toJsonStr(settings));
    }

    public static void setSystemSettings(List list){
        JSONObject settings = new JSONObject();
        //TODO 读取数据库的系统配置存入redis
        redisService.set(REDIS_SYSTEM_SETTINGS_KEY, JSONUtil.toJsonStr(settings));
    }
}
```

SystemRunner，前端项目设置项目启动时自动将系统配置参数放入redis缓存

```java
package com.wte.frontapiuser.component;

import com.wt.wte.wtebase.common.utils.SystemUtil;
import lombok.extern.slf4j.Slf4j;
import org.springframework.boot.ApplicationArguments;
import org.springframework.boot.ApplicationRunner;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

/**
 * Create by chenglong on 2021/1/20
 */
@Component
@Order(1)
@Slf4j
public class SystemRunner implements ApplicationRunner {
    @Override
    public void run(ApplicationArguments args) throws Exception {
        try {
            SystemUtil.setSystemSettings();
        } catch (Exception e){
            log.info("启动程序自动装配系统配置异常，异常原因：{}",e.getMessage());
        }
        log.info("启动程序自动装配系统配置完成");
    }
}
```

#### (8)集成短信发送接口

注册阿里云、开通短信服务、配置签名和模板

![image-20210121164746505](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210121164746505.png)

新增阿里云依赖

```xml
<!--阿里云sdk-->
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>4.5.3</version>
</dependency>
```

增加application-***.yml配置

```yaml
msgCodeSend:
  media: simulator # simulator-模拟器 ali-阿里云短信服务平台
ali:
  api:
    isSend: true
    regionId: cn-hangzhou
    accessKeyId: LTAI4GGBnKWh**********
    accessSecret: VIkrF0UkpbU9aW**********
    sendSms:
      signName: WTE
      templateCode:
        regist: SMS_*******
```

wte-base项目新建ShortMessageUtil

```java
package com.wt.wte.wtebase.common.utils;

import cn.hutool.core.util.StrUtil;
import cn.hutool.json.JSONObject;
import com.wt.wte.wtebase.common.api.ApiException;
import com.wt.wte.wtebase.common.api.ExceptionConstants;
import com.wt.wte.wtebase.common.constants.SystemSettingKey;
import com.wt.wte.wtebase.thirdapi.AliApi;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;

/**
 * 短信工具类
 * Create by chenglong on 2021/1/21
 */
@Component
@Slf4j
public class ShortMessageUtil {

    @Value("${msgCodeSend.media}")
    private String media;

    private static String mediaName;

    @PostConstruct
    public void setMediaName(){
        ShortMessageUtil.mediaName = this.media;
    }

    /**
     * 发送短信验证码
     * @param phoneNumber
     * @param code
     * @param type
     * @return
     */
    public static String sendCodeMessage(String phoneNumber, String code, String type){
        try {
            switch (mediaName){
                case "simulator": return simulatorSendMsgCode(phoneNumber,code,type);
                case "ali": return aliSendMsgCode(phoneNumber,code,type);
                default: return simulatorSendMsgCode(phoneNumber,code,type);
            }
        } catch (Exception e){
            throw new ApiException(ExceptionConstants.MSGCODE_SEND_FAILED, null);
        }
    }

    /**
     * 调用阿里服务发送短信验证码
     * @param phoneNumber
     * @param code
     * @param type
     * @return
     */
    private static String aliSendMsgCode(String phoneNumber, String code, String type) throws Exception {
        JSONObject param = new JSONObject();
        param.put("code", code);
        String templateCode = AliApi.getTemplateCode(type);
        return AliApi.sendSms(phoneNumber, templateCode, param);
    }

    /**
     * 模拟向手机发送验证码
     * @param phoneNumber
     * @param code
     * @param type
     * @return
     */
    private static String simulatorSendMsgCode(String phoneNumber, String code, String type) {
        String msg = "";
        switch (type){
            case "1": msg = SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_TYPE_REGIST);break;
            case "2": msg = SystemUtil.getSettingValue(SystemSettingKey.MSGCODE_TYPE_LOGIN);break;
            default: msg = "";
        }
        msg = StrUtil.replace(msg, "${code}", code);
        log.info("正在模拟向手机{}发送短信验证码信息，信息内容：{}",phoneNumber,msg);
        return msg;
    }
}
```

新增AliApi，阿里API接口

```java
package com.wt.wte.wtebase.thirdapi;

import cn.hutool.core.date.DateUtil;
import cn.hutool.core.util.StrUtil;
import cn.hutool.json.JSONObject;
import cn.hutool.json.JSONUtil;
import com.aliyuncs.CommonRequest;
import com.aliyuncs.CommonResponse;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.http.MethodType;
import com.aliyuncs.profile.DefaultProfile;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;

/**
 * Create by chenglong on 2021/1/21
 */
@Component
@Slf4j
public class AliApi {

    @Value("${ali.api.isSend}")
    private String isSend;
    @Value("${ali.api.regionId}")
    private String regionId;
    @Value("${ali.api.accessKeyId}")
    private String accessKeyId;
    @Value("${ali.api.accessSecret}")
    private String accessSecret;
    @Value("${ali.api.sendSms.signName}")
    private String signName;
    @Value("${ali.api.sendSms.templateCode.regist}")
    private String registTemplateCode;

    private static AliProperties aliProperties;
    private static String registTemplateCodeValue;

    @PostConstruct
    public void setAliProperties(){
        aliProperties = new AliProperties();
        aliProperties.setIsSend(this.isSend);
        aliProperties.setRegionId(this.regionId);
        aliProperties.setAccessKeyId(this.accessKeyId);
        aliProperties.setAccessSecret(this.accessSecret);
        aliProperties.setSignName(this.signName);
        registTemplateCodeValue = this.registTemplateCode;
    }

    /**
     * 根据类型获取模板
     * @param type
     * @return
     */
    public static String getTemplateCode(String type) {
        switch (type){
            case "1": return registTemplateCodeValue;
            default: return "";
        }
    }

    /**
     * 阿里云-发送短信接口
     */
    public static String sendSms(String phoneNumbers, String templateCode, JSONObject templateParam) throws Exception {
        String result = "";
        if(StrUtil.equals(aliProperties.getIsSend(), "true")){
            DefaultProfile profile = DefaultProfile.getProfile(aliProperties.getRegionId(), aliProperties.getAccessKeyId(), aliProperties.getAccessSecret());
            IAcsClient client = new DefaultAcsClient(profile);

            CommonRequest request = new CommonRequest();
            request.setSysMethod(MethodType.POST);
            request.setSysDomain("dysmsapi.aliyuncs.com");
            request.setSysVersion(DateUtil.today());
            request.setSysAction("SendSms");
            request.putQueryParameter("RegionId", aliProperties.getRegionId());
            request.putQueryParameter("PhoneNumbers", phoneNumbers);
            request.putQueryParameter("SignName", aliProperties.getSignName());
            request.putQueryParameter("TemplateCode", templateCode);
            request.putQueryParameter("TemplateParam", JSONUtil.toJsonStr(templateParam));
            try {
                CommonResponse response = client.getCommonResponse(request);
                result = response.getData();
                log.info("阿里云发送短信验证码结果："+result);
            } catch (ServerException e) {
                log.info("阿里云发送短信验证码异常，异常原因："+e.getMessage());
                e.printStackTrace();
                throw new Exception(e.getMessage());
            } catch (ClientException e) {
                log.info("阿里云发送短信验证码异常，异常原因："+e.getMessage());
                e.printStackTrace();
                throw new Exception(e.getMessage());
            }
        } else{
            log.info("未真实发送手机短信");
            result = "模拟已成功发送短信验证码";
        }
        return result;
    }
}
```

AliProperties类

```java
package com.wt.wte.wtebase.thirdapi;

import lombok.Data;

/**
 * Create by chenglong on 2021/1/21
 */
@Data
public class AliProperties {
    public String isSend;
    public String regionId;
    public String accessKeyId;
    public String accessSecret;
    public String signName;
}
```

#### (9)使用nimbus-jose-jwt的非对称加密（RSA）操作JWT

`nimbus-jose-jwt`是最受欢迎的JWT开源库，基于Apache 2.0开源协议，支持所有标准的签名(JWS)和加密(JWE)算法。

1. 使用jdk的keytool工具生成jwt.jks

   cmd->执行命令keytool -genkey -alias jwt -keyalg RSA -keystore jwt.jks

   alias:jwt

   秘钥库口令：wte2021

   秘钥口令：wte123

   ![image-20210122145758033](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20210122145758033.png)

2. jwt.jks放入工程的resource文件夹

3. 读取RSAkey

   pom.xml新增依赖

   ```xml
   <!--JWT解析库-->
   <dependency>
       <groupId>com.nimbusds</groupId>
       <artifactId>nimbus-jose-jwt</artifactId>
       <version>8.16</version>
   </dependency>
   <!--Spring Security RSA工具类-->
   <dependency>
       <groupId>org.springframework.security</groupId>
       <artifactId>spring-security-rsa</artifactId>
       <version>1.0.7.RELEASE</version>
   </dependency>
   ```

4. 新建JwtTokenService接口和JwtTokenServiceImpl实现类

   ```java
   package com.wt.wte.wtebase.common.service;
   
   import com.nimbusds.jose.JOSEException;
   import com.nimbusds.jose.jwk.RSAKey;
   import com.wt.wte.wtebase.common.dto.PayloadDto;
   
   import java.text.ParseException;
   
   /**
    * Create by chenglong on 2021/1/22
    */
   public interface JwtTokenService {
   
       public String generateTokenByHMAC(String payloadStr, String secret) throws JOSEException;
   
       public PayloadDto verifyTokenByHMAC(String token, String secret) throws ParseException,JOSEException ;
   
       public RSAKey getDefaultRSAKey();
   
       public String generateTokenByRSA(String payloadStr, RSAKey rsaKey) throws JOSEException;
   
       public PayloadDto verifyTokenByRSA(String token, RSAKey rsaKey) throws ParseException, JOSEException;
   }
   ```

   ```java
   package com.wt.wte.wtebase.common.service;
   
   import cn.hutool.json.JSONUtil;
   import com.nimbusds.jose.*;
   import com.nimbusds.jose.crypto.MACSigner;
   import com.nimbusds.jose.crypto.MACVerifier;
   import com.nimbusds.jose.crypto.RSASSASigner;
   import com.nimbusds.jose.crypto.RSASSAVerifier;
   import com.nimbusds.jose.jwk.RSAKey;
   import com.wt.wte.wtebase.common.dto.PayloadDto;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.ClassPathResource;
   import org.springframework.security.rsa.crypto.KeyStoreKeyFactory;
   import org.springframework.stereotype.Service;
   
   import java.security.KeyPair;
   import java.security.interfaces.RSAPrivateKey;
   import java.security.interfaces.RSAPublicKey;
   import java.text.ParseException;
   import java.util.Date;
   
   /**
    * Create by chenglong on 2021/1/22
    */
   @Service
   public class JwtTokenServiceImpl implements JwtTokenService {
   
       @Value("${RSA.filename}")
       private String rsaFilename;
       @Value("${RSA.alias}")
       private String rsaAlias;
       @Value("${RSA.storePwd}")
       private String rsaStorePwd;
       @Value("${RSA.pwd}")
       private String rsaPwd;
   
       @Override
       public String generateTokenByHMAC(String payloadStr, String secret) throws JOSEException {
           //创建JWS头，设置签名算法和类型
           JWSHeader jwsHeader = new JWSHeader.Builder(JWSAlgorithm.HS256).
                   type(JOSEObjectType.JWT)
                   .build();
           //将负载信息封装到Payload中
           Payload payload = new Payload(payloadStr);
           //创建JWS对象
           JWSObject jwsObject = new JWSObject(jwsHeader, payload);
           //创建HMAC签名器
           JWSSigner jwsSigner = new MACSigner(secret);
           //签名
           jwsObject.sign(jwsSigner);
           return jwsObject.serialize();
       }
   
       @Override
       public PayloadDto verifyTokenByHMAC(String token, String secret) throws ParseException, JOSEException {
           //从token中解析JWS对象
           JWSObject jwsObject = JWSObject.parse(token);
           //创建HMAC验证器
           JWSVerifier jwsVerifier = new MACVerifier(secret);
           if (!jwsObject.verify(jwsVerifier)) {
               throw new RuntimeException("token签名不合法！");
           }
           String payload = jwsObject.getPayload().toString();
           PayloadDto payloadDto = JSONUtil.toBean(payload, PayloadDto.class);
           if (payloadDto.getExp() < new Date().getTime()) {
               throw new RuntimeException("token已过期！");
           }
           return payloadDto;
       }
   
       @Override
       public RSAKey getDefaultRSAKey() {
           //从classpath下获取RSA秘钥对
           KeyStoreKeyFactory keyStoreKeyFactory = new KeyStoreKeyFactory(new ClassPathResource(rsaFilename), rsaStorePwd.toCharArray());
           KeyPair keyPair = keyStoreKeyFactory.getKeyPair(rsaAlias, rsaPwd.toCharArray());
           //获取RSA公钥
           RSAPublicKey publicKey = (RSAPublicKey) keyPair.getPublic();
           //获取RSA私钥
           RSAPrivateKey privateKey = (RSAPrivateKey) keyPair.getPrivate();
           return new RSAKey.Builder(publicKey).privateKey(privateKey).build();
       }
   
       @Override
       public String generateTokenByRSA(String payloadStr, RSAKey rsaKey) throws JOSEException {
           //创建JWS头，设置签名算法和类型
           JWSHeader jwsHeader = new JWSHeader.Builder(JWSAlgorithm.RS256)
                   .type(JOSEObjectType.JWT)
                   .build();
           //将负载信息封装到Payload中
           Payload payload = new Payload(payloadStr);
           //创建JWS对象
           JWSObject jwsObject = new JWSObject(jwsHeader, payload);
           //创建RSA签名器
           JWSSigner jwsSigner = new RSASSASigner(rsaKey, true);
           //签名
           jwsObject.sign(jwsSigner);
           return jwsObject.serialize();
       }
   
       @Override
       public PayloadDto verifyTokenByRSA(String token, RSAKey rsaKey) throws ParseException, JOSEException {
           //从token中解析JWS对象
           JWSObject jwsObject = JWSObject.parse(token);
           RSAKey publicRsaKey = rsaKey.toPublicJWK();
           //使用RSA公钥创建RSA验证器
           JWSVerifier jwsVerifier = new RSASSAVerifier(publicRsaKey);
           if (!jwsObject.verify(jwsVerifier)) {
               throw new RuntimeException("token签名不合法！");
           }
           String payload = jwsObject.getPayload().toString();
           PayloadDto payloadDto = JSONUtil.toBean(payload, PayloadDto.class);
           if (payloadDto.getExp() < new Date().getTime()) {
               throw new RuntimeException("token已过期！");
           }
           return payloadDto;
       }
   }
   ```

   ```yaml
   RSA: # RSA 非对称加密
     filename: jwt.jks
     alias: jwt
     storePwd: wte2021
     pwd: wte123
   ```

#### (10)整合SpringSecurity和JWT实现登录和授权

增加依赖

```xml
<!--SpringSecurity依赖配置-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<!--JWT(Json Web Token)登录支持-->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.0</version>
</dependency>
```

```yaml
jwt:
  tokenHeader: token #JWT存储的请求头
  tokenHead: WTE #JWT负载中拿到开头
  secret: wteSecret #JWT加解密使用的密钥
  expiration: 604800 #JWT的超期限时间(单位：秒，60*60*24*7)
  generate: RSA #JWT加密解密方式（RSA：nimbus非对称方式加密，HMAC：nimbus对称方式加密，JJWT：jjwt方式生成token）
```

JwtTokenUtil工具类，提供了RSA，HMAC，JJWT三种加密方式，可在application.yml里的jwt.generate进行配置。提供生成和验证token的方法

```java
package com.wt.wte.wtebase.common.utils;

import cn.hutool.core.date.DateUtil;
import cn.hutool.core.util.NumberUtil;
import cn.hutool.json.JSONUtil;
import com.nimbusds.jose.JWSObject;
import com.nimbusds.jose.jwk.RSAKey;
import com.wt.wte.wtebase.common.dto.PayloadDto;
import com.wt.wte.wtebase.common.dto.UmsUserDetails;
import com.wt.wte.wtebase.common.service.JwtTokenService;
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Component;

import java.util.*;
import java.util.stream.Collectors;

/**
 * JwtToken生成的工具类
 * Create by chenglong on 2021/1/22
 */
@Component
@Slf4j
public class JwtTokenUtil {
    @Autowired
    private JwtTokenService jwtTokenService;

    @Value("${jwt.secret}")
    private String secret;
    @Value("${jwt.expiration}")
    private Long expiration;
    @Value("${jwt.generate}")
    private String generate;

    public String generateToken(UmsUserDetails details){
        String token = new String();
        try {
            switch (generate){
                case "RSA":
                    RSAKey key = jwtTokenService.getDefaultRSAKey();
                    token = jwtTokenService.generateTokenByRSA(getPayloadStr(details),key);
                    break;
                case "HMAC":
                    token = jwtTokenService.generateTokenByHMAC(getPayloadStr(details), secret);
                    break;
                case "JJWT":
                    Map claims = getClaims(details.getUsername());
                    token = generateToken(claims);
                    break;
            }
        } catch (Exception e){
            log.info("生成JWT token发生异常，异常原因：{}",e.getMessage());
        }
        return token;
    }

    public String getUsernameFromToken(String token){
        String username = new String();
        switch (generate){
            case "RSA":
                username = getUserNameFromTokenByRSA(token);
                break;
            case "HMAC":
                username = getUserNameFromTokenByHMAC(token);
                break;
            case "JJWT":
                username = getUserNameFromTokenByClaims(token);
                break;
        }
        return username;
    }

    public boolean validateToken(String token, UserDetails details) {
        try {
            switch (generate){
                case "RSA":
                    return jwtTokenService.verifyTokenByRSA(token, jwtTokenService.getDefaultRSAKey())!=null;
                case "HMAC":
                    return jwtTokenService.verifyTokenByHMAC(token, secret)!=null;
                case "JJWT":
                    String username = getUserNameFromTokenByClaims(token);
                    return username.equals(details.getUsername()) && !isTokenExpired(token);
            }
        } catch (Exception e){
            log.info("验证JWT token发生异常，异常原因：{}",e.getMessage());
        }
        return false;
    }

    /**
     * 判断token是否已经失效
     */
    private boolean isTokenExpired(String token) {
        Date expiredDate = getExpiredDateFromToken(token);
        return expiredDate.before(new Date());
    }

    /**
     * 从token中获取过期时间
     */
    private Date getExpiredDateFromToken(String token) {
        Claims claims = getClaimsFromToken(token);
        return claims.getExpiration();
    }

    private String getPayloadStr(UmsUserDetails details){
        Date now = new Date();
        Date exp = DateUtil.offsetSecond(now, NumberUtil.parseInt(String.valueOf(expiration)));
        List<String> authorities = details.getAuthorities().stream()
                .map(authority->new String(authority.getAuthority()))
                .collect(Collectors.toList());
        PayloadDto payloadDto = PayloadDto.builder()
                .sub("wte")
                .iat(now.getTime())
                .exp(exp.getTime())
                .jti(UUID.randomUUID().toString())
                .username(details.getUsername())
                .authorities(authorities)
                .build();
        return JSONUtil.toJsonStr(payloadDto);
    }

    private Map<String,Object> getClaims(String username){
        Map<String, Object> claims = new HashMap<>();
        claims.put("sub", username);
        claims.put("created", new Date());
        return claims;
    }

    /**
     * 根据负责生成JWT的token
     */
    private String generateToken(Map<String, Object> claims) {
        return Jwts.builder()
                .setClaims(claims)
                .setExpiration(generateExpirationDate())
                .signWith(SignatureAlgorithm.HS512, secret)
                .compact();
    }

    /**
     * 生成token的过期时间
     */
    private Date generateExpirationDate() {
        return new Date(System.currentTimeMillis() + expiration * 1000);
    }

    /**
     * 从token中获取JWT中的负载
     */
    private Claims getClaimsFromToken(String token) {
        Claims claims = null;
        try {
            claims = Jwts.parser()
                    .setSigningKey(secret)
                    .parseClaimsJws(token)
                    .getBody();
        } catch (Exception e) {
            log.info("JWT格式验证失败:{}",token);
        }
        return claims;
    }

    /**
     * 从token中获取登录用户名
     */
    private String getUserNameFromTokenByClaims(String token) {
        String username;
        try {
            Claims claims = getClaimsFromToken(token);
            username =  claims.getSubject();
        } catch (Exception e) {
            username = null;
        }
        return username;
    }

    private String getUserNameFromTokenByHMAC(String token){
        try {
            //从token中解析JWS对象
            JWSObject jwsObject = JWSObject.parse(token);
            String payload = jwsObject.getPayload().toString();
            PayloadDto payloadDto = JSONUtil.toBean(payload, PayloadDto.class);
            return payloadDto.getUsername();
        } catch (Exception e){
            e.printStackTrace();
            return "";
        }
    }

    private String getUserNameFromTokenByRSA(String token){
        try {
            //从token中解析JWS对象
            JWSObject jwsObject = JWSObject.parse(token);
            String payload = jwsObject.getPayload().toString();
            PayloadDto payloadDto = JSONUtil.toBean(payload, PayloadDto.class);
            return payloadDto.getUsername();
        } catch (Exception e){
            e.printStackTrace();
            return "";
        }
    }
}
```

PayloadDto，JWT的payload信息

```java
package com.wt.wte.wtebase.common.dto;

import io.swagger.annotations.ApiModelProperty;
import lombok.Builder;
import lombok.Data;
import lombok.EqualsAndHashCode;

import java.util.List;

/**
 * Create by chenglong on 2021/1/22
 */
@Data
@EqualsAndHashCode(callSuper = false)
@Builder
public class PayloadDto {
    @ApiModelProperty("主题")
    private String sub;
    @ApiModelProperty("签发时间")
    private Long iat;
    @ApiModelProperty("过期时间")
    private Long exp;
    @ApiModelProperty("JWT的ID")
    private String jti;
    @ApiModelProperty("用户名称")
    private String username;
    @ApiModelProperty("用户拥有的权限")
    private List<String> authorities;
}
```

UmsUserDetails，用于存用户信息和权限

```java
package com.wt.wte.wtebase.common.dto;

import com.wt.wte.wtebase.base.BaseConstants;
import com.wt.wte.wtebase.modules.ums.model.UmsUser;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

/**
 * Create by chenglong on 2021/1/22
 */
public class UmsUserDetails implements UserDetails {

    private UmsUser umsUser;

    public UmsUserDetails(UmsUser umsUser) {
        this.umsUser = umsUser;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        List<GrantedAuthority> authorities = new ArrayList<>();
        authorities.add(new SimpleGrantedAuthority("All"));
        return authorities;
    }

    @Override
    public String getPassword() {
        return umsUser.getPassword();
    }

    @Override
    public String getUsername() {
        return umsUser.getUsername();
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return umsUser.getStatus() == BaseConstants.USER_STATUS_NORMAL;
    }
}
```

SecurityConfig

```java
package com.wte.frontapiuser.config;

import com.baomidou.mybatisplus.core.conditions.query.QueryWrapper;
import com.wt.wte.wtebase.base.BaseConstants;
import com.wt.wte.wtebase.common.dto.UmsUserDetails;
import com.wt.wte.wtebase.modules.ums.model.UmsUser;
import com.wt.wte.wtebase.modules.ums.service.UmsUserService;
import com.wte.frontapiuser.component.JwtAuthenticationTokenFilter;
import com.wte.frontapiuser.component.RestAuthenticationEntryPoint;
import com.wte.frontapiuser.component.RestfulAccessDeniedHandler;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

/**
 * SpringSecurity的配置
 * Create by chenglong on 2021/1/22
 */
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UmsUserService umsUserService;
    @Autowired
    private RestfulAccessDeniedHandler restfulAccessDeniedHandler;
    @Autowired
    private RestAuthenticationEntryPoint restAuthenticationEntryPoint;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable() //使用JWT，不需要csrf
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS) //基于token，不适用session
            .and().authorizeRequests()
            .antMatchers(HttpMethod.GET,"/",
                    "/*.html",
                    "/favicon.ico",
                    "/**/*.html",
                    "/**/*.css",
                    "/**/*.js",
                    "/doc.html",
                    "/swagger-resources/**",
                    "/v2/api-docs/**").permitAll()
            .antMatchers("/frontapi/account/**").permitAll() // 对AccountController的api要允许匿名访问
            .antMatchers(HttpMethod.OPTIONS).permitAll() //跨域请求会先进行一次options请求
            .anyRequest().authenticated();
        //禁用缓存
        http.headers().cacheControl();
        //添加JWT filter
        http.addFilterBefore(jwtAuthenticationTokenFilter(), UsernamePasswordAuthenticationFilter.class);
        http.exceptionHandling()
                .accessDeniedHandler(restfulAccessDeniedHandler)
                .authenticationEntryPoint(restAuthenticationEntryPoint);
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService())
                .passwordEncoder(passwordEncoder());
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        //获取登录用户信息
        return username -> {
            QueryWrapper<UmsUser> wrapper = new QueryWrapper();
            wrapper.lambda()
                    .eq(UmsUser::getIsDelete, BaseConstants.DEL_NO)
                    .eq(UmsUser::getUsername,username);
            UmsUser user = umsUserService.getOne(wrapper);
            if (user != null) {
                return new UmsUserDetails(user);
            }
            throw new UsernameNotFoundException("用户名或密码错误");
        };
    }

    @Bean
    public JwtAuthenticationTokenFilter jwtAuthenticationTokenFilter(){
        return new JwtAuthenticationTokenFilter();
    }

    @Bean
    @Override
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }
}
```

JwtAuthenticationTokenFilter，每次请求访问都经过该过滤器

```java
package com.wte.frontapiuser.component;

import cn.hutool.core.util.StrUtil;
import com.wt.wte.wtebase.common.utils.JwtTokenUtil;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.web.filter.OncePerRequestFilter;

import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * Create by chenglong on 2021/1/22
 */
@Slf4j
public class JwtAuthenticationTokenFilter extends OncePerRequestFilter {

    @Autowired
    private JwtTokenUtil jwtTokenUtil;
    @Autowired
    private UserDetailsService userDetailsService;

    @Value("${jwt.tokenHeader}")
    private String tokenHeader;
    @Value("${jwt.tokenHead}")
    private String tokenHead;

    @Override
    protected void doFilterInternal(HttpServletRequest httpServletRequest,
                                    HttpServletResponse httpServletResponse,
                                    FilterChain filterChain) throws ServletException, IOException {
        String authHeader = httpServletRequest.getHeader(this.tokenHeader);
        if(StrUtil.isNotEmpty(authHeader) && StrUtil.startWith(authHeader, this.tokenHead)){
            String authToken = StrUtil.subSuf(authHeader, this.tokenHead.length());
            String username = jwtTokenUtil.getUsernameFromToken(authToken);
            log.info("checking username:{}", username);
            if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
                UserDetails userDetails = this.userDetailsService.loadUserByUsername(username);
                if(jwtTokenUtil.validateToken(authToken,userDetails)){
                    UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
                    authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(httpServletRequest));
                    log.info("authenticated user:{}", username);
                    SecurityContextHolder.getContext().setAuthentication(authentication);
                }
            }
        }
        filterChain.doFilter(httpServletRequest, httpServletResponse);
    }
}
```

RestAuthenticationEntryPoint

```java
package com.wte.frontapiuser.component;

import cn.hutool.json.JSONUtil;
import com.wt.wte.wtebase.common.api.CommonResult;
import org.springframework.security.core.AuthenticationException;
import org.springframework.security.web.AuthenticationEntryPoint;
import org.springframework.stereotype.Component;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * Create by chenglong on 2021/1/22
 */
@Component
public class RestAuthenticationEntryPoint implements AuthenticationEntryPoint{
    @Override
    public void commence(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, AuthenticationException e) throws IOException, ServletException {
        httpServletResponse.setCharacterEncoding("UTF-8");
        httpServletResponse.setContentType("application/json");
        httpServletResponse.getWriter().println(JSONUtil.parse(CommonResult.unauthorized(e.getMessage())));
        httpServletResponse.getWriter().flush();
    }
}
```

RestfulAccessDeniedHandler

```java
package com.wte.frontapiuser.component;

import cn.hutool.json.JSONUtil;
import com.wt.wte.wtebase.common.api.CommonResult;
import org.springframework.security.access.AccessDeniedException;
import org.springframework.security.web.access.AccessDeniedHandler;
import org.springframework.stereotype.Component;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 当访问接口没有权限时，自定义的返回结果
 * Create by chenglong on 2021/1/22
 */
@Component
public class RestfulAccessDeniedHandler implements AccessDeniedHandler {
    @Override
    public void handle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, AccessDeniedException e) throws IOException, ServletException {
        httpServletResponse.setCharacterEncoding("UTF-8");
        httpServletResponse.setContentType("application/json");
        httpServletResponse.getWriter().println(JSONUtil.parse(CommonResult.forbidden(e.getMessage())));
        httpServletResponse.getWriter().flush();
    }
}
```

修改Swagger3Config配置类

```java
package com.wte.frontapiuser.config;

import cn.hutool.core.util.NumberUtil;
import cn.hutool.setting.dialect.Props;
import com.github.xiaoymin.knife4j.spring.annotations.EnableKnife4j;
import com.wt.wte.wtebase.common.api.ResultCode;
import io.swagger.v3.oas.annotations.enums.SecuritySchemeIn;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.builders.ResponseMessageBuilder;
import springfox.documentation.oas.annotations.EnableOpenApi;
import springfox.documentation.schema.ModelRef;
import springfox.documentation.service.*;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spi.service.contexts.SecurityContext;
import springfox.documentation.spring.web.plugins.Docket;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Create by chenglong on 2021/1/14
 */
@Configuration
@EnableOpenApi
@EnableKnife4j
public class Swagger3Config implements WebMvcConfigurer {

    private static Props SWAGGER = Props.getProp("properties/swagger.properties");

    @Bean
    public Docket createRestApi(){
        List<ResponseMessage> responseMessageList = new ArrayList<>();
        Arrays.stream(ResultCode.values()).forEach(errorEnum -> {
            responseMessageList.add(
                    new ResponseMessageBuilder()
                            .code(NumberUtil.parseInt(errorEnum.getCode()))
                            .message(errorEnum.getMessage())
                            .responseModel(
                            new ModelRef(errorEnum.getMessage())).build()
            );
        });
        return new Docket(DocumentationType.SWAGGER_2)
                .globalResponseMessage(RequestMethod.GET, responseMessageList)
                .globalResponseMessage(RequestMethod.POST, responseMessageList)
                .globalResponseMessage(RequestMethod.PUT, responseMessageList)
                .globalResponseMessage(RequestMethod.DELETE, responseMessageList)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.wte.frontapiuser.controller"))
                .paths(PathSelectors.any())
                .build()
                .securitySchemes(securitySchemes())
                .securityContexts(securityContexts());
    }

    /**
     * API文档基本信息
     * @return
     */
    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
                .title(SWAGGER.getStr("title"))
                .description(SWAGGER.getStr("description"))
                .contact(new Contact(SWAGGER.getStr("contactName"), SWAGGER.getStr("contactUrl"), SWAGGER.getStr("contactEmail")))
                .version(SWAGGER.getStr("version"))
                .build();
    }

    /**
     * 设置需要登录认证的路径
     * @return
     */
    private List<SecurityContext> securityContexts() {
        List<SecurityContext> securityContexts = new ArrayList<>();
        SecurityContext securityContext = SecurityContext.builder()
                .securityReferences(securityReferences())
                .forPaths(PathSelectors.regex("/frontapi/((?!account).)+/.*")) //除了frontapi/account/路径下的接口不需要登录认证，其他都需要
                .build();
        securityContexts.add(securityContext);
        return securityContexts;
    }

    private List<SecurityReference> securityReferences(){
        AuthorizationScope[] authorizationScopes = new AuthorizationScope[]{new AuthorizationScope("global", "accessEverything")};
        List<SecurityReference> securityReferences = new ArrayList<>();
        securityReferences.add(new SecurityReference("Authorization",authorizationScopes));
        return securityReferences;
    }

    /**
     * 设置请求头信息
     * @return
     */
    private List<SecurityScheme> securitySchemes() {
        List<SecurityScheme> securitySchemes = new ArrayList<>();
        ApiKey apiKey = new ApiKey("Authorization", "token", SecuritySchemeIn.HEADER.toString());
        securitySchemes.add(apiKey);
        return securitySchemes;
    }

}
```

#### (11)