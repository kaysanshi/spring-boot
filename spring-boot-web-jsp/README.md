# spring-boot
spring-boot的基本的使用方式
# springboot:
	Spring Boot是他们最新的创新，能够跟上不断变化的技术需求。 开发Spring Boot的主要动机是简化配置和部署spring应用程序的过程。
	Spring Boot为开发提供一个具有最小功能的Spring应用程序，并提供了一个新的范例。
	使用Spring Boot将能够以更灵活的方式开发Spring应用程序，并且能够通过最小(或可能没有)配置Spring来专注于解决应用程序的功能需求。它使用全新的开发模型，通过避免一些繁琐的开发步骤和样板代码和配置，使Java开发非常容易。
	Spring Boot的主要特点：
		创建独立的Spring应用程序
		直接嵌入Tomcat，Jetty或Undertow（无需部署WAR文件）
		提供“初始”的POM文件内容，以简化Maven配置
		尽可能时自动配置Spring
		提供生产就绪的功能，如指标，健康检查和外部化配置
		绝对无代码生成，也不需要XML配置
  ## 本仓库代码包括以下
       自动配置
       yml
       日志
       web开发
       缓存(cache,redis
       数据库操作(jpa,jdbc,mybatis) 
       笔记
  springboot:
			Spring Boot是他们最新的创新，能够跟上不断变化的技术需求。 开发Spring Boot的主要动机是简化配置和部署spring应用程序的过程。
			Spring Boot为开发提供一个具有最小功能的Spring应用程序，并提供了一个新的范例。
			使用Spring Boot将能够以更灵活的方式开发Spring应用程序，并且能够通过最小(或可能没有)配置Spring来专注于解决应用程序的功能需求。它使用全新的开发模型，通过避免一些繁琐的开发步骤和样板代码和配置，使Java开发非常容易。
		Spring Boot的主要特点：
				创建独立的Spring应用程序
				直接嵌入Tomcat，Jetty或Undertow（无需部署WAR文件）
				提供“初始”的POM文件内容，以简化Maven配置
				尽可能时自动配置Spring
				提供生产就绪的功能，如指标，健康检查和外部化配置
				绝对无代码生成，也不需要XML配置

		设置springBoot的banner：
		我们在 src/main/resources 目录下新建一个 banner.txt
					${AnsiColor.BRIGHT_RED}：设置控制台中输出内容的颜色
					${application.version}：用来获取 MANIFEST.MF 文件中的版本号
					${application.formatted-version}：格式化后的 ${application.version} 版本信息
					${spring-boot.version}：Spring Boot 的版本号
					${spring-boot.formatted-version}：格式化后的 ${spring-boot.version} 版本信息
		springboot的核心还是spring，他不是编写应用程序的框架，他是提供应用程序服务器功能的嵌入式servlert容器。
		
## springboot的使用：
	 在maven中引入以下的配置：
		<parent>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-parent<artifacId>
			<version>1.5.7.relesas</version>
		</parent>
		引入依赖：
			<dependency>
					<groupId>org.springframework.boot</groupId>
					<artifactId>spring-boot-starter-web</artifactId>
				</dependency>
				<dependency>
					<groupId>org.mybatis.spring.boot</groupId>
					<artifactId>mybatis-spring-boot-starter</artifactId>
					<version>1.3.2</version>
				</dependency>
### 在springboot项目中的启动类有以下配置：
		主程序类的标志：
		@SpringBootApplication= @Configuration+@EnableAutoconfiguration+@ComponentScan
  		
		@Configuration：经常与＠Bean 组合使用，使用这两个注解就可以创建一个简单的Spring 配置类， 可以用来替代相应的XML 配置文件。
   		@EnableAutoConfiguration ：能够自动配置Spring 的上下文，猜测和配置用户想要的Bean类。
   		@ComponentScan ： 会自动扫描指定包下的全部标有＠Component 的类， 并注册成Bean，包括子注解＠Service 、＠Repository 、＠Controller。这些Bean 一般是结合＠Autowired 构造函数来注入。）
		
		@AutoConfigurationPackage:自动配置包：

	控制器中的类：
		@RestController = @Controller + @ResponseBody
	
	#配置文件：

				配置yml文件：
							logging:
							level:
								cn:
									qfengx:
							portal:
								mapper: debug
							file: D:/log/portal_log.log
						server:
							port: 80
						spring:
							datasource:
								username: root
								password: 123
								url: jdbc:mysql://localhost:3306/portal?useSSL=true
								driver-class-name: com.mysql.jdbc.Driver
							servlet:
								multipart:
									max-file-size: 128MB
									max-request-size: 128MB
						mybatis:
							config-location: classpath:mybatis/mybatis-config.xml
							mapper-locations:
							- classpath:mybatis/mapper/*.xml
						upload:
							path:
								product: 
									img: D:/portal/upload/product/img/
					
### springboot的基本的概念及其术语：
		任何一个标注了@Configuration的Java类定义都是一个JavaConfig配置类。
		 <beans>
		<! -- bean定义 -->
		</beans>
		而基于JavaConfig的配置方式是这样的：
		@Configuration
		public class MockConfiguration{
		    // bean定义
		}
		任何一个标注了 @ Bean的方法，其返回值将作为一个bean定义注册到Spring的IoC容器，方法名将默认成为该bean定义的id。
			1. @Component Scan
			@Component Scan对应XML配置形式中的<context:component-scan>元素，用于配合一些元信息Java Annotation，比如@Component和@Repository等，将标注了这些元信息Annotation的bean定义类批量采集到Spring的IoC容器中。
			2. @PropertySource 与 @PropertySources
					@PropertySource用于从某些地方加载*.properties文件内容，并将其中的属性加载到IoC容器中，便于填充一些bean定义属性的占位符（placeholder），当然，这需要PropertySourcesPlaceholderConfigurer的配合。
					@Configuration
					@PropertySource("classpath:1.properties")
					@PropertySource("classpath:2.properties")
					@PropertySource("...")
					public class XConfiguration{
					    ...
					}
					@PropertySources(   
					@PropertySource("classpath:1.properties"),     @PropertySource("classpath:2.properties"),
						...
					})
					public class XConfiguration{
					    ...
					}
			@Import 只负责引入JavaConfig形式定义的IoC容器配置，如果有一些遗留的配置或者遗留系统需要以XML形式来配置（比如dubbo框架），
			通 过 @ImportResource将它们一起合并到当前JavaConfig配置的容器中：
				@Configuration
				@Import(MockConfiguration.class)
				@ImportResource("...")
				public class XConfiguration {
				    ...
				}
			@SpringBootApplication是一个“三体”结构，实际上它是一个复合Annotation：
				@Target(ElementType.TYPE)
				@Retention(RetentionPolicy.RUNTIME)
				@Documented
				@Inherited
				@Configuration
				@EnableAutoConfiguration
				@Component Scan
				public @interface SpringBootApplication{
				    ...
				}
			SpringBoot启动类拆分为两个独立的Java类，整个形势就明朗了：
				@Configuration
				@EnableAutoConfiguration
				@Component Scan
				public class DemoConfiguration {
				    @Bean
				    public Controller controller() {
					return new Controller();
				    }
				}
				public class DemoApplication {
				    public static void main(String[] args) {
					SpringApplication.run(DemoConfiguration.class, args);
				    }
				}
				所以，启动类DemoApplication其实就是一个标准的Standalone类型Java程序的main函数启动类，没有什么特殊的。

			@EnableAutoConfiguration可以帮助SpringBoot应用将所有符合条件的@Configuration配置都加载到当前SpringBoot创建并使用的IoC容器，
				@EnableAutoConfiguration作为一个复合Annotation，其自身定义关键信息如下：
				@Target(ElementType.TYPE)
				@Retention(RetentionPolicy.RUNTIME)
				@Documented
				@Inherited
				@AutoConfigurationPackage
				@Import(EnableAutoConfigurationImportSelector.class)
				public @interface EnableAutoConfiguration {
				    ...
				}
			借助于SpringFactoriesLoader的支持，@EnableAutoConfiguration可以“智能”地自动配置功效才得以大功告成！
			那么什么是springFactoriesLoader?
				其主要功能就是从指定的配置文件META-INF/spring.factories加载配置，
				spring.factories是一个典型的java properties文件，配置的格式为Key = Value形式，
				只不过Key和Value都是Java类型的完整类名（Fully qualified name）
				example.MyService=example.MyServiceImpl1, example.MyServiceImpl2
			在@EnableAutoConfiguration的场景中，它更多是提供了一种配置查找的功能支持，即根据@EnableAutoConfiguration的完整类名org.springframework.boot.autoconfigure.EnableAutoConfiguration作为查找的Key，获取对应的一组@Configuration类：
			@EnableAutoConfiguration自动配置的魔法其实就变成了：从classpath中搜寻所有META-INF/spring.factories配置文件，
			并将其中org.spring-framework.boot.autoconfigure.EnableAutoConfiguration对应的配置项通过反射（Java Reflection）实例化为对应的标注了@Configuration的JavaConfig形式的IoC容器配置类，
			然后汇总为一个并加载到IoC容器。
		@Component Scan 的功能其实就是自动扫描并加载符合条件的组件或bean定义，最终将这些bean定义加载到容器中。
		加载bean定义到Spring的IoC容器，我们可以手工单个注册，不一定非要通过批量的自动扫描完成，所以说@Component Scan是可有可无的。
				  @ConﬁgurationProperties  @Value
			功能 批量注入配置文件中的属性   一个个指定
			松散绑定（松散语法） 支持     不支持
			SpEL    不支持                支持
			JSR303数据校验 支持           不支持
			复杂类型封装 支持              不支持
			 
			1、properties配置文件在idea中默认utf-8可能会乱码 
			调整
			2、
		@PropertySource&@ImportResource&@Bean 
		@PropertySource：加载指定的配置文件；
			 @PropertySource(value="classpath:person.properties")
		@ImportResource：导入spring的配置文件，让配置文件加载到让其生效
		不推荐使用：
		@ImportResource(locations = {"classpath:beans.xml"}) 导入Spring的配置文件让其生效
			<?xml version="1.0" encoding="UTF‐8"?>
				 <beans xmlns="http://www.springframework.org/schema/beans"       
				  xmlns:xsi="http://www.w3.org/2001/XMLSchema‐instance"        
				 xsi:schemaLocation="http://www.springframework.org/schema/beans  
				 http://www.springframework.org/schema/beans/spring‐beans.xsd">         
				 <bean id="helloService" class="com.atguigu.springboot.service.HelloService">
			</bean> 
			</beans>
		推荐使用：给容器中添加组件：
		 @Configuration：指明当前类是一个配置类；就是来替代之前的Spring配置文件
 		* 在配置文件中用<bean><bean/>标签添加组件  *  */ 
			@Configuration 
			public class MyAppConfig {     
				  //将方法的返回值添加到容器中；容器中这个组件默认的id就是方法名   
				  @Bean     
				public HelloService helloService02(){       
					  System.out.println("配置类@Bean给容器中添加组件了...");        
					 return new HelloService();    
					
				 } }
		配置文件加载顺序：（互不配置）
			springboot启动会扫描以下的位置的application.properties或者application.yml文件
			-file:./config/
			-file:./
			-classpath:/config/
			-classpath:/
			以上是按照优先级从高到低顺序被加载，所有的位置的都会被加载，高优先级覆盖低优先级
			可以通过spring.config.location来改变默认的文件的配置
			项目打包后可以通过命令行参数的形式，启动项目时指定配置文件的新的位置指定的配置文件和默认的共同生效
			

		springBoot应用的启动的步骤：
		SpringApplication的run方法的实现是我们本次旅程的主要线路，该方法的主要流程大体可以归纳如下：
				1）如果我们使用的是SpringApplication的静态run方法，那么，这个方法里面首先需要创建一个SpringApplication对象实例，然后调用这个创建好的SpringApplication的实例run方法。在SpringApplication实例初始化的时候，它会提前做几件事情：
					根据classpath里面是否存在某个特征类（org.springframework.web. context.ConfigurableWebApplicationContext）来决定是否应该创建一个为Web应用使用的ApplicationContext类型，还是应该创建一个标准Standalone应用使用的ApplicationContext类型。
					使用Spring Factories Loader在应用的classpath中查找并加载所有可用的Application Context Initializer。
					使用Spring Factories Loader在应用的classpath中查找并加载所有可用的Application Listener。
					推断并设置main方法的定义类。
				2）SpringApplication实例初始化完成并且完成设置后，就开始执行run方法的逻辑了，方法执行伊始，首先遍历执行所有通过SpringFactoriesLoader可以查找到并加载的SpringApplicationRunListener，调用它们的started()方法，告诉这些SpringApplicationRunListener, “嘿，SpringBoot应用要开始执行咯！”。
				3）创建并配置当前SpringBoot应用将要使用的Environment（包括配置要使用的PropertySource以及Profile）。
				4）遍历调用所有SpringApplicationRunListener的environmentPrepared()的方法，告诉它们：“当前SpringBoot应用使用的Environment准备好咯！”。
				5）如果SpringApplication的showBanner属性被设置为true，则打印banner（SpringBoot 1.3.x版本，这里应该是基于Banner.Mode决定banner的打印行为）。
					这一步的逻辑其实可以不关心，我认为唯一的用途就是“好玩”（Just For Fun）。
				6）根据用户是否明确设置了applicationContextClass类型以及初始化阶段的推断结果，决定该为当前SpringBoot应用创建什么类型的ApplicationContext并创建完成，
					然后根据条件决定是否添加ShutdownHook，决定是否使用自定义的BeanNameGenerator，决定是否使用自定义的ResourceLoader，当然，最重要的，将之前准备好的Environment设置给创建好的ApplicationContext使用。
				7）ApplicationContext创建好之后，SpringApplication会再次借助Spring-FactoriesLoader，查找并加载classpath中所有可用的ApplicationContext-Initializer，
					然后遍历调用这些ApplicationContextInitializer的initialize (applicationContext)方法来对已经创建好的ApplicationContext进行进一步的处理。
				8）遍历调用所有SpringApplicationRunListener的contextPrepared()方法，通知它们：“SpringBoot应用使用的ApplicationContext准备好啦！”
				9 ）最核心的一步，将之前通过@EnableAutoConfiguration获取的所有配置以及其他形式的IoC容器配置加载到已经准备完毕的ApplicationContext。
				10）遍历调用所有SpringApplicationRunListener的contextLoaded()方法，告知所有SpringApplicationRunListener, ApplicationContext"装填完毕"！
				11）调用ApplicationContext的refresh()方法，完成IoC容器可用的最后一道工序。
				12）查找当前ApplicationContext中是否注入CommandlineRunner,如果有，则遍历执行他们，
				13）正常情况下遍历执行SpringApplicationRunListener的finished()方法然，只不过这种情况会将异常信息一并处理，至此一个springboot应用启动完毕。
				开始---》收集各种条件和回调接口（Application Context Initializer，ApplicatioListener）----->通知 started()；创建并准备Environment---->通告environmentPrepared()
						-----》创建并初始化ApplicationContext----->通告contextPrepared(),通告contextLoaded(),----->refresh,applicationContent完成启动程序，执行CommanadLineRunner,通告finished();
			springboot自动配置：
				 Spring Boot启动扫描所有jar包的META-INF/spring.factories中配置的 EnableAutoConfiguration组件 
				 • spring-boot-autoconfigure.jar\META-INF\spring.factories有启动时需要加载的 EnableAutoConfiguration组件配置
				 • 配置文件中使用debug=true可以观看到当前启用的自动配置的信息 
				 • 自动配置会为容器中添加大量组件 
				 • Spring Boot在做任何功能都需要从容器中获取这个功能的组件
				 • Spring Boot 总是遵循一个标准；容器中有我们自己配置的组件就用我们配置的，没有就用自动配 置默认注册进来的组件；
				
			
			springboot整合JDBC与数据源：
					1、引入starter – spring-boot-starter-jdbc
					2、配置application.yml 
					3、测试
					4、高级配置：使用druid数据源 – 引入druid – 配置属性 5、配置druid数据源监控
				springboot整合Mybatis:
					1、引入mybatis-starter – mybatis-spring-boot-starter 
					2、注解模式
					3、配置文件模式
					4、测试
			 	SpringBoot整合Durid:
					 		Durid是阿里的一个开源的项目，
							 Druid 是目前最好的数据库连接池，在功能、性能、扩展性方面，都超过其他数据库连接池，包括 DBCP、C3P0、BoneCP、Proxool、JBoss DataSource。Druid 已经在阿里巴巴部署了超过 600 个应用，经过多年生产环境大规模部署的严苛考验。Druid 是阿里巴巴开发的号称为监控而生的数据库连接池！
								# 引入依赖
								在 pom.xml 文件中引入 druid-spring-boot-starter 依赖

								<dependency>
										<groupId>com.alibaba</groupId>
										<artifactId>druid-spring-boot-starter</artifactId>
										<version>1.1.10</version>
								</dependency>
								引入数据库连接依赖

								<dependency>
										<groupId>mysql</groupId>
										<artifactId>mysql-connector-java</artifactId>
										<scope>runtime</scope>
								</dependency>提供了很多工具。让开发更加的简洁。

								tk.mybatis是在mybatis基础上
								引入mabatis的相关依赖
								<dependency>
										<groupId>tk.mybatis</groupId>
										<artifactId>mapper-spring-boot-starter</artifactId>
										<version>2.0.2</version>
								</dependency>
								引入PageHelper:这是一个Mybatis的分页的插件，支持多数据源，简化数据库的分页的查询
								<dependency>
										<groupId>com.github.pagehelper</groupId>
										<artifactId>pagehelper-spring-boot-starter</artifactId>
										<version>1.2.5</version>
								</dependency>
								# 配置 application.yml
								在 application.yml 中配置数据库连接

								spring:
									datasource:
										druid:
											url: jdbc:mysql://ip:port/dbname?useUnicode=true&characterEncoding=utf-8&useSSL=false
											username: root
											password: 123456
											initial-size: 1
											min-idle: 1
											max-active: 20
											test-on-borrow: true
											# MySQL 8.x: com.mysql.cj.jdbc.Driver
											driver-class-name: com.mysql.jdbc.Driver
								mybatis:
									type-aliases-package: 实体类的存放路径，如：com.funtl.hello.spring.boot.entity
									mapper-locations: classpath:mapper/*.xml	
							使用mybatis中的maven插件生成代码：
								在pom.xml中增加mybatis-generator-maven-plugin插件：
									<build>
										<plugins>
											<plugin>
												<groupId>org.mybatis.generator</groupId>
												<artifactId>mybatis-generator-maven-plugin</artifactId>
												<version>1.3.5</version>
												<configuration>
													<configurationFile>${basedir}/src/main/resources/generator/generatorConfig.xml</configurationFile>
													<overwrite>true</overwrite>
													<verbose>true</verbose>
												</configuration>
												<dependencies>
													<dependency>
														<groupId>mysql</groupId>
														<artifactId>mysql-connector-java</artifactId>
														<version>${mysql.version}</version>
													</dependency>
													<dependency>
														<groupId>tk.mybatis</groupId>
														<artifactId>mapper</artifactId>
														<version>3.4.4</version>
													</dependency>
												</dependencies>
											</plugin>
										</plugins>
									</build>	
									在resources目录中创建generatorConfig.xml配置问价：
									<?xml version="1.0" encoding="UTF-8"?>
										<!DOCTYPE generatorConfiguration
												PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
												"http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">

										<generatorConfiguration>
											<!-- 引入数据库连接配置 -->
											<properties resource="jdbc.properties"/>

											<context id="Mysql" targetRuntime="MyBatis3Simple" defaultModelType="flat">
												<property name="beginningDelimiter" value="`"/>
												<property name="endingDelimiter" value="`"/>
												
												<!-- 配置 tk.mybatis 插件 -->
												<plugin type="tk.mybatis.mapper.generator.MapperPlugin">
													<property name="mappers" value="com.funtl.utils.MyMapper"/>
												</plugin>

												<!-- 配置数据库连接 -->
												<jdbcConnection
														driverClass="${jdbc.driverClass}"
														connectionURL="${jdbc.connectionURL}"
														userId="${jdbc.username}"
														password="${jdbc.password}">
												</jdbcConnection>

												<!-- 配置实体类存放路径 -->
												<javaModelGenerator targetPackage="com.funtl.hello.spring.boot.entity" targetProject="src/main/java"/>

												<!-- 配置 XML 存放路径 -->
												<sqlMapGenerator targetPackage="mapper" targetProject="src/main/resources"/>

												<!-- 配置 DAO 存放路径 -->
												<javaClientGenerator
														targetPackage="com.funtl.hello.spring.boot.mapper"
														targetProject="src/main/java"
														type="XMLMAPPER"/>

												<!-- 配置需要指定生成的数据库和表，% 代表所有表 -->
												<table catalog="myshop" tableName="%">
													<!-- mysql 配置 -->
													<generatedKey column="id" sqlStatement="Mysql" identity="true"/>
												</table>
											</context>
										</generatorConfiguration>	
								配置数据源：
									在src/main/resources目录创建 jdbc.properties
									# MySQL 8.x: com.mysql.cj.jdbc.Driver
										jdbc.driverClass=com.mysql.jdbc.Driver
										jdbc.connectionURL=jdbc:mysql://ip:port/dbname?useUnicode=true&characterEncoding=utf-8&useSSL=false
										jdbc.username=root
										jdbc.password=123456	
								插件自动生成命令：mvn mybatis-generator:generate
									
						测试：
								@RunWith(SpringRunner.class)
								@SpringBootTest(classes = HelloSpringBootApplication.class)
								@Transactional
								@Rollback
								public class MyBatisTests {

										/**
										* 注入数据查询接口
										*/
										@Autowired
										private TbUserMapper tbUserMapper;

										/**
										* 测试插入数据
										*/
										@Test
										public void testInsert() {
												// 构造一条测试数据
												TbUser tbUser = new TbUser();
												tbUser.setUsername("Lusifer");
												tbUser.setPassword("123456");
												tbUser.setPhone("15888888888");
												tbUser.setEmail("topsale@vip.qq.com");
												tbUser.setCreated(new Date());
												tbUser.setUpdated(new Date());

												// 插入数据
												tbUserMapper.insert(tbUser);
										}
								}

				springboot整合jpa:
					1、引入spring-boot-starter-data-jpa 
					2、配置文件打印SQL语句 
					3、创建Entity标注JPA注解 
					4、创建Repository接口继承JpaRepository
					5、测试方法
			springboot整合redis实现缓存：
				1. 引入spring-boot-starter-data-redis 
				2. application.yml配置redis连接地址
				3. 配置缓存 – @EnableCaching、 – CachingConfigurerSupport、
				4. 测试使用缓存 
				5. 切换为其他缓存&CompositeCacheManager
			springboot整合thymeleaf:
				可以全部代替jsp的一个类似于freeMarker的模板引擎
				在无网络情况下也可运行，可以直接在服务器端查看动态页面效果，支持html圆形，在浏览器解析时会直接忽略，
				开箱即用
				提供标准，和spring标准，可以使用jstl和ognl表达式相结合，springmvc支持，直接可以绑定表单数据
				以jar运行的方式，最好不用jsp相关知识，
				Beetl和freeMarker这些都是相同的框架。
				1.引入依赖：
					<dependency>
						<groupId>org.springframework.boot</groupId>
						<artifactId>spring-boot-starter-thymeleaf</artifactId>
					</dependency>
					 <dependency>
						<groupId>net.sourceforge.nekohtml</groupId>
						<artifactId>nekohtml</artifactId>
						<version>1.9.22</version>
					</dependency>
				2.配置thymeleaf:
					在application.yml中配置：
						spring:
						 thymeleaf:
						   cache:false #开发时关闭缓存，
						   mode:LWGACHTML5
						   enc



		idea中使用springboot组件开发：
			IDEA -> New Project -> Spring Initializr	
			选择web版本开发：
				.gitignore：Git 过滤配置文件
				pom.xml：Maven 的依赖管理配置文件
				HelloSpringBootApplication.java：程序入口
				resources：资源文件目录
				static: 静态资源文件目录
				templates：模板资源文件目录
				application.properties：Spring Boot 的配置文件，实际开发中会替换成 YAML 语言配置（application.yml）
			pom.xml中：
				spring-boot-starter-web：包含了 spring-boot-starter 还自动帮我们开启了 Web 支持
			没有配置 web.xml
			没有配置 application.xml，Spring Boot 帮你配置了
			没有配置 application-mvc.xml，Spring Boot 帮你配置了
			没有配置 Tomcat，Spring Boot 内嵌了 Tomcat 容器
		自定义bannner:
			在resource中定义banner.txt在里面书写
			常用的属性设置：
				${AnsiColor.BRIGHT_RED}：设置控制台中输出内容的颜色
				${application.version}：用来获取 MANIFEST.MF 文件中的版本号
				${application.formatted-version}：格式化后的 ${application.version} 版本信息
				${spring-boot.version}：Spring Boot 的版本号
				${spring-boot.formatted-version}：格式化后的 ${spring-boot.version} 版本信息
		springboot 中的配置文件：
				修改端口号：
				在application.properties中添加：
					server.port=9090
					server.context-path=/boot
				在application.yml中配置：
					server:
					  port: 9090
					  context-path: /boot
		
