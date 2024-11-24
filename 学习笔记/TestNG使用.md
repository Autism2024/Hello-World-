# 常用注解

##  Before类别和After类别注解

- @BeforeSuite：被@BeforeSuite注解的方法，将会在testng定义的xml根元素里面的所有执行之前运行。
- @AfterSuite：被@AfterSuite注解的方法，将会在testng定义的xml根元素里面的所有执行之后运行。
- @BeforeTest：被@BeforeTest注解的方法，将会在一个元素定义的所有里面所有测试方法执行之前运行。
- @AfterTest被@AfterTest注解的方法，将会在一个元素定义的所有里面所有的测试方法执行之后运行。
- @BeforeClass：被@BeforeClass注解的方法，将会在当前测试类的第一个测试方法执行之前运行。
- @AfterClass:被@AfterClass注解的方法，将会在当前测试类的最后一个测试方法执行之后运行。
- @BeforeMethod:被@BeforeMethod注解的方法，将会在当前测试类的每一个测试方法执行之前运行。
- @AfterMethod:被@AfterMethod注解的方法，将会在当前测试类的每一个测试方法执行之后运行。

上述的注解分为Before类别和After类，我们可以在Before类别的注解方法里面做一些初始化动作，如实例化数据库连接、新建数据库连接池、创建线程池、打开文件流等等。然后，我们可以在After类别的注解方法里面做一些销毁动作，如释放数据库连接、销毁数据库连接池、销毁线程池或者关闭文件流等等。同一类别的不同注解会在不同的位置被调用，

## @Test 注解

@Test 注解是TestNG的核心注解，被打上该注解的方法，表示为一个测试方法，类比JUnit是一个道理(JUnit也是用了这个注解

- alwaysRun : 如果=true,表示即使该测试方法所依赖的前置测试有失败的情况，也要执行
- dataProvider : 选定传入参数的构造器。(@DataProvider注解将在后面章节介绍)
- dataProviderClass : 确定参数构造器的Class类。(参数构造器首先会在当前测试类里面查找，如果参数构造器不在当前测试类定义，那么必须使用该属性来执行它所在的Class类)
- dependsOnGroups : 确定依赖的前置测试组别。
- dependsOnMethods : 确定依赖的前置测试方法。
- description ： 测试方法描述信息。(建议为每个测试方法添加有意义的描述信息，这将会在最后的报告中展示出来)
- enabled : 默认为true，如果指定为false，表示不执行该测试方法。
- expectedExceptions ： 指定期待测试方法抛出的异常，多个异常以逗号(,)隔开。
- groups : 指定该测试方法所属的组，可以指定多个组，以逗号隔开。组测试的用法将在后面文章单独介绍。
- invocationCount ： 指定测试方法需要被调用的次数。
- invocationTimeOut： 每一次调用的超时时间，如果invocationCount没有指定，该参数会被忽略。应用场景可以为测试获取数据库连接，超时就认定为失败。单位是毫秒。
- priority ： 指定测试方法的优先级，数值越低，优先级越高，将会优先与其他数值高的测试方法被调用。(注意是针对一个测试类的优先级)
- timeout : 指定整个测试方法的超时时间。单位是毫秒。

## @Parameters 注解

@Parameters 注解用于为测试方法传递参数

## @DataProvider 注解

上面的小结提到@Parameters注解可以为测试方法传递参数，但是这种方式参数值需要配置在testng.xml里面，灵活性不高。而@DataProvider注解同样可以为测试方法传递参数值，并且，它是真正意义上的参数构造器，可以传入多组测试数据对测试方法进行测试。被@DataProvider注解的方法，方法返回值必须为Object[][]或者Iterator<Object[]>。



## @Factory 注解

在一个方法上面打上`@Factory`注解，表示该方法将返回能够被TestNG测试的测试类。利用了设计模式中的工厂模式



## @Listeners 注解

一般我们写测试类不会涉及到这种类型的注解，这个注解必须定义在类、接口或者枚举类级别。实用的Listener包括ISuiteListener、ITestListener和IInvokedMethodListener，他们可以在suite级别、test级别和test method一些执行点执行一些自定义操作，如打印日志。因为很少使用

## 断言

### 硬断言

- assertTrue 判断是否为True。
- assertFalse 判断是否为false。
- assertSame 判断引用地址是否相同。
- assertNotSame 判断引用地址是否不相同
- assertNull：判断是否为null。
-  assertNotNull：判断是否不为null。
- assertEquals：判断是否相等，Object类型的对象需要实现haseCode及equals方法
- assertNotEquals：判断是否不相等
- assertEqualsNoOrder：判断忽略顺序是否相等

### 软断言

  如果一个断言失败，会继续执行这个断言下的其他语句或者断言
 2）  也就是一个用例有多个断言，失败了其中一个，不影响其他断言的运行
 3）  不要忘记调用assertAll()在该用例的最后一个断言后面
 4） 软断言的类，叫SoftAssert.java，这个类是需要创建实例对象，才能调用相关实例方法进行软断言

```java
SoftAssert assertion = new SoftAssert();
assertion.assertEquals(5,6,"我俩是不是一样大");

//再强调一次，最后一定要调用assertAll()方法
assertion.assertAll();//必须有且需要放在最后
```

## 数据驱动测试

### 1、使用@DataProvider定义对象数组，数组的名称为KeyWord,这个数组可以实现每次检索不同的数据

- 缺点测试数据写在测试用例里面，维护工作量变大

### 使用CSV文件进行数据驱动测试

- 创建CSV文件：data.csv

### 使用Excel数据源文件

- apach poi进行excel数据读取

### 利用YAML进行数据驱动测试

- 在resource目录下创建application.yaml文件存放测试数据

### 利用mysql进行数据驱动测试

- 使用jdbc连接并读取数据库

1. **添加MySQL JDBC依赖**：确保你的项目中包含了MySQL JDBC驱动的依赖。如果你使用Maven，可以在`pom.xml`文件中添加如下依赖：

   xml

   ```xml
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>8.0.23</version>
   </dependency>
   ```

2. **创建数据库连接**：在你的测试代码中，使用JDBC API创建到MySQL数据库的连接。例如：

   java

   ```java
   String url = "jdbc:mysql://localhost:3306/your_database";
   String username = "your_username";
   String password = "your_password";
   Connection conn = DriverManager.getConnection(url, username, password);
   ```

3. **编写数据提供者**：使用`@DataProvider`注解来提供测试数据。你可以从数据库查询数据并返回一个`Object[][]`或者`Iterator<Object[]>`。

   java

   ```java
   @DataProvider(name = "testData")
   public static Object[][] getTestData() throws SQLException {
       List<Object[]> data = new ArrayList<>();
       String query = "SELECT * FROM your_table";
       try (Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery(query)) {
           while (rs.next()) {
               data.add(new Object[]{rs.getString("column1"), rs.getInt("column2")});
           }
       }
       Object[][] array = new Object[data.size()][];
       return data.toArray(array);
   }
   ```

4. **编写测试方法**：使用`@Test`注解来标记测试方法，并使用`dataProvider`属性来指定使用哪个数据提供者。

   java

   ```java
   @Test(dataProvider = "testData")
   public void testDataDriven(String column1, int column2) {
       // 你的测试逻辑
   }
   ```

5. **关闭数据库连接**：在测试完成后，确保关闭数据库连接。

6. **配置TestNG**：如果你需要使用`testng.xml`文件来配置测试，可以在里面指定测试类和组。

7. **运行测试**：使用TestNG运行你的测试，它将使用提供的数据来执行测试方法。

以上步骤提供了一个基本的框架，你可以根据具体需求进行调整。例如，你可能需要处理异常、设置数据库连接池或者使用更高级的数据库操作工具如MyBatis。记得在实际测试中使用正确的数据库名称、表名称和字段名称。

## pageObject设计模式

- 将页面定位元素方法和元素操作进行分离
  - 对象层：用于存放元素定位和控件操作行为
  - 操作层：用于封装哥哥模块功能用例的操作
  - 业务层：真正执行测试用例的操作模块

## pageFactory设计模式

- 将页面定位元素方法和元素操作进行分离

  - 基础层：用来存放driver对象和初始化操作

  - 对象层：用于存放元素定位和控件操作行为
  - 操作层：用于封装哥哥模块功能用例的操作
  - 业务层：真正执行测试用例的操作模块