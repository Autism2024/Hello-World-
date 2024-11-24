## 安装Selenium-Server-Standalone

Selenium是一个优秀的自动化测试框架，可以模拟浏览器的各种操作来代替人工操作。不同的浏览器有 不同的driver来驱动。之前项目中使用的firefoxDriver,chromeDriver有一个缺点，就是浏览器必须和我的项目在同一台机器上。而项目一般是部署在linux机器上，这样一来，有如下几个缺点：
1、linux必须安装firefox,chrome浏览器，操作十分麻烦，而且受Linux版本限制。本人安装firefox还好，下载后解压就可以了，而chrome下载后还需要执行一些别的安装操作，由于linux是openSuse11的，缺各种包，从未安装成功过。
2、由于是linux系统，跑UI测试的时候，如果没有安装xmanager传输图形化界面，是看不到运行效果的。
3、在Linux上firefox浏览器运行测试总会有各种各样的问题，例如driver连接7055端口超时，在windows环境下则没有出现过。
鉴于上述问题，因此，想将测试和浏览器进行分离，通过控制远程机器的浏览器运行测试，而不仅限于在项目所在机器上。Selenium-Server-StandAlone很好的解决了这个问题。

下载地址：https://selenium-release.storage.googleapis.com/index.html

maven安装方法

安装本地jar包到本地仓库中

```java
mvn install:install-file -Dfile=C:\Users\13203\Downloads\selenium-server-standalone-3.9.0.jar -DgroupId=org.selenium -DartifactId=selenium-server-standalone -Dversion=4.0.0 -Dpackaging=jar
```

pom.xml文件中声明

1.添加 system
2.systemPath这个路径是jar包的路径。${project.basedir}只是一个系统自己的常量。

```xml
 <dependency>
            <groupId>org.selenium</groupId>
            <artifactId>selenium-server-standalone</artifactId>
            <version>3.9.0</version>
            <scope>system</scope>
            <systemPath>${project.basedir}/lib/selenium-server-standalone-3.9.0.jar</systemPath>
        </dependency>
```

## driver.get和deiver.navigate区别

我们在运行脚本时做的第一件事是打开浏览器并加载网页。我们通常使用`driver.get(“url”);`来加载网页。每次使用此命令时，页面都将被刷新。

我们也可以使用`driver.navigate().to(“url’);`加载网页。这两个命令在行为方面以相同的方式工作。但`navigate().to()`还具有其他功能，如`navigate().forward()`、`navigate().back()`和`navigate().refresh()`。

因此，区别在于`driver.get()`从不存储历史，而`driver.navigate().to()`存储浏览器历史，以便用于其他命令的转发和后退等。

在单页应用程序中，当`navigate().to()`通过更改URL (如向前/向后)导航到页面时，`get()`刷新页面。

## 常用元素定位方法

- id
- linkText
- partialLinkText
- name
- tagName
- xpath
  - 不要使用带有空格的属性
  - 不要使用动态生成的id、class等
  - 定位时候一定要找到唯一的属性
  - 查看页面是否存在frame
  - 绝对路径和相对路径
- className
- cssSelector

## webdriver常用API使用详解