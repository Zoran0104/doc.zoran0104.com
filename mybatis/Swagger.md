1. 依赖

```xml
<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger2</artifactId>
   <version>2.9.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger-ui</artifactId>
   <version>2.9.2</version>
</dependency>
```

2. 配置swagger

   ```java
   @Configuration
   @EnableSwagger2
   public class SwaggerConfig {
       @Bean
       public Docket createRestApi() {
           return new Docket(DocumentationType.SWAGGER_2)
                   .apiInfo(apiInfo())
                   .select()
                   .apis(RequestHandlerSelectors.basePackage("com.yss.ms.admin"))
                   .paths(PathSelectors.any())
                   .build();
       }
   
       private ApiInfo apiInfo() {
           return new ApiInfoBuilder()
                   .title("My application document")
                   .description("My application document")
                   .termsOfServiceUrl("http://192.168.1.198:10070/platformgroup/ms-admin")
                   .contact(new Contact("Zoran","http","http://www.baidu.com"))
                   .version("1.0")
                   .build();
       }
   }
   ```

   # 

