---
layout: post
title: spring boot(һ) ����
category: springboot
---
## ʲô�� Spring Boot

Spring Boot ���� Pivotal �Ŷ��ṩ��ȫ�¿�ܣ������Ŀ������������ Spring Ӧ�õĳ�ʼ��Լ��������̡��ÿ��ʹ�����ض��ķ�ʽ���������ã��Ӷ�ʹ������Ա������Ҫ�������廯�����á����ҵĻ�����⣬���� Spring Boot ��ʵ����ʲô�µĿ�ܣ���Ĭ�������˺ܶ��ܵ�ʹ�÷�ʽ������ Maven ���������е� Jar ����Spring Boot ���������еĿ�ܡ�

## ʹ�� Spring Boot ��ʲô�ô�

��ʵ���Ǽ򵥡����١����㣡ƽʱ���������Ҫ�һ�� Spring Web ��Ŀ��ʱ����Ҫ��ô���أ�

- 1������ web.xml������ Spring �� Spring mvc
- 2���������ݿ����ӡ����� Spring ����
- 3�����ü��������ļ��Ķ�ȡ������ע��
- 4��������־�ļ�
- ��
- �������֮���� Tomcat ����
- ��

���ڷǳ�����΢��������������Ŀ����ֻ����Ҫ����һ���ʼ�������ҵ���Ŀ����������һ�����֣��Ҷ���Ҫ��������һ��!

�������ʹ�� Spring Boot �أ�
�ܼ򵥣��ҽ���ֻ��Ҫ�ǳ��ٵļ������þͿ���Ѹ�ٷ���Ĵ����һ�� Web ��Ŀ�����ǹ���һ��΢����

ʹ�� Spring Boot �����ж�ˬ�����������ͼ�����

![img](http://www.itmind.net/assets/images/2016/dog.jpg)

## ��������

˵����ô�࣬�������ĺܣ�������һ������!

**Maven ������Ŀ**

- 1������ http://start.spring.io/
- 2��ѡ�񹹽����� Maven Project��Java��Spring Boot �汾 2.1.3 �Լ�һЩ���̻�����Ϣ���ɲο���ͼ��ʾ��

![img](http://www.itmind.net/assets/images/2019/springboot/spring-boot-start.png)

- 3����� Generate Project ������Ŀѹ����
- 4����ѹ��ʹ�� Idea ������Ŀ��File -> New -> Model from Existing Source.. -> ѡ���ѹ����ļ��� -> OK��ѡ�� Maven һ· Next��OK done!
- 5�����ʹ�õ��� Eclipse��Import -> Existing Maven Projects -> Next -> ѡ���ѹ����ļ��� -> Finsh��OK done!

**Idea ������Ŀ**

- 1��ѡ�� File -> New ��> Project�� �����½���Ŀ�Ŀ�
- 2��ѡ�� Spring Initializr��Next Ҳ������������Ƶ����ý��棬Idea ���������˼���
- 3����д������ݺ󣬵�� Next ѡ�������İ��ٵ�� Next�����ȷ����Ϣ������ Finish��

**��Ŀ�ṹ����**

![img](http://www.itmind.net/assets/images/2016/springboot2.png)

����ͼ��ʾ��Spring Boot �Ļ����ṹ�������ļ�:

- `src/main/java` ���򿪷��Լ����������
- `src/main/resources` �����ļ�
- `src/test/java` ���Գ���

���⣬ Spring Boot �����Ŀ¼������£�
root package �ṹ��`com.example.myproject`

```
com
  +- example
    +- myproject
      +- Application.java
      |
      +- model
      |  +- Customer.java
      |  +- CustomerRepository.java
      |
      +- service
      |  +- CustomerService.java
      |
      +- controller
      |  +- CustomerController.java
      |
```

- 1��Application.java ����ŵ���Ŀ¼����,��Ҫ������һЩ�������
- 2��model Ŀ¼��Ҫ����ʵ�������ݷ��ʲ㣨Repository��
- 3��service ����Ҫ��ҵ�������
- 4��controller ����ҳ����ʿ���

����Ĭ�����ÿ���ʡȥ�ܶ����ã���ȻҲ���Ը����Լ���ϲ�������и���
������� Application main ����������һ�� Java ��Ŀ����ˣ�

**���� web ģ��**

1��pom.xml�����֧��web��ģ�飺

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

pom.xml �ļ���Ĭ��������ģ�飺

- `spring-boot-starter` ������ģ�飬�����Զ�����֧�֡���־�� YAML����������� `spring-boot-starter-web` web ģ�����ȥ�������ã���Ϊ `spring-boot-starter-web` �Զ������� `spring-boot-starter`��
- `spring-boot-starter-test` ������ģ�飬���� JUnit��Hamcrest��Mockito��

2����д Controller ���ݣ�

```
@RestController
public class HelloWorldController {
    @RequestMapping("/hello")
    public String index() {
        return "Hello World";
    }
}
```

`@RestController` ����˼���� Controller ����ķ������� json ��ʽ�����������дʲô jackjson ���õ��ˣ�

3�����������򣬴���������� `http://localhost:8080/hello`���Ϳ��Կ���Ч���ˣ���ľ�кܼ򵥣�

**�������Ԫ����**

�򿪵�`src/test/`�µĲ�����ڣ���д�򵥵� http ���������ԣ�ʹ�� mockmvc ���У�����`MockMvcResultHandlers.print()`��ӡ��ִ�н����

```
@RunWith(SpringRunner.class)
@SpringBootTest
public class HelloTests {

  
    private MockMvc mvc;

    @Before
    public void setUp() throws Exception {
        mvc = MockMvcBuilders.standaloneSetup(new HelloWorldController()).build();
    }

    @Test
    public void getHello() throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/hello").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("Hello World")));
    }

}
```

**���������ĵ���**

������������������Ŀ���Ѿ��ܳ����˰ɣ���Ȼƽʱ����web��Ŀ�����У��Ķ���Ŀ���������Ǳ�����springBoot�Ե���֧�ֺܺã��޸�֮�����ʵʱ��Ч����Ҫ������µ����ã�

```
 <dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>
            </configuration>
        </plugin>
</plugins>
</build>
```

��ģ���������Ĵ�����������е�ʱ��ᱻ���á������ʹ�� `java -jar`����Ӧ�û�����һ���ض��� classloader ������������Ϊ����һ����������������

## �ܽ�

ʹ�� Spring Boot ���Էǳ����㡢���ٴ��Ŀ��ʹ���ǲ��ù��Ŀ��֮��ļ����ԣ����ð汾�ȸ������⣬������ʹ���κζ������������һ�����þͿ��ԣ�����ʹ�� Spring Boot �ǳ��ʺϹ���΢����

> ���������Ѿ������� Spring Boot 2.x