# @SpringBootApplication

作用：开启组件扫描，和自动配置功能，由下面三个注解构成

- @Configureation  该类使用基于Java的配置
- @ComponentScan  启用组件扫描
- @EnableAutoConfiguration  开启自动配置



要添加自己的配置怎么办？

把要增加的配置写到单独的@Configuration标注的类中，也可以直接写到xxApplication类中。