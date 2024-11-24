1、Scanner工具类

----方便在控制台扫描用户输入的工具类

格式化输入是通过类java.util.Scanner来完成的。

**默认情况下，Scanner是使用“空白”作为分隔符将输入分解为标记，**

**然后使用它所提供的不同的next方法将得到的标记转换为不同的类型的值**

```java
/**
 * @author: hupengpeng
 * @createDate: 2024年09月02日 12:48
 */
package Scanner_Test;
//导包
import java.util.Scanner;
public class Scanner_Test {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入一个整数：");
        int i = scanner.nextInt();
        System.out.println(i);
        scanner.nextLine();
        System.out.print("请输入一个字符串：");
        String str = scanner.nextLine();
        System.out.println("您输入的字符串是：" + str);
        scanner.close();
    }
}
```

- `nextInt()` 用于从输入流中读取下一个整数并返回，如果输入流中没有整数，或者不是整数，将抛出 InputMismatchException 异常。

- `nextLine()` 方法会扫描输入流中的字符，直到遇到行末尾的换行符 `\n`，然后将该行的内容作为字符串返回，同时，`nextLine()` 会将 Scanner 对象的位置移动到下一行的开头，以便下一次读取数据时从下一行的开头开始读取。

- `boolean hasNext()`：检查输入流是否还有下一个标记。
- `boolean hasNextLine()`：检查输入流是否还有下一行。
- `String next()`：读取输入流中的下一个标记（使用默认的分隔符，通常是空格或换行符）。
- `double nextDouble()`：读取输入流中的下一个双精度浮点数。

```java
        Scanner scanner = new Scanner(System.in); // 创建 Scanner 对象，从标准输入流中读取数据
//        System.out.print("请输入一个整数：");
//        if (scanner.hasNextInt()) { // 判断输入流中是否有下一个整数
//            int num = scanner.nextInt(); // 读取输入流中的下一个整数
//            System.out.println("您输入的整数是：" + num);
//        } else {
//            System.out.println("输入的不是整数！");
//        }
//        scanner.nextLine(); // 读取输入流中的换行符

        System.out.print("请输入多个单词，以空格分隔：");
        while (!scanner.hasNext("#")) { // 判断输入流中是否还有下一个标记
            String word = scanner.next();// 读取输入流中的下一个单词
            if(!word.isEmpty()){
            System.out.println("您输入的单词是：" + word);
            }

        }
        scanner.nextLine(); // 读取输入流中的换行符
        scanner.nextLine();//消耗单独输入#时多余的换行符，使得可以正常进入下一个sout

        System.out.print("请输入一个实数：");
        if (scanner.hasNextDouble()) { // 判断输入流中是否有下一个实数
            double num = scanner.nextDouble(); // 读取输入流中的下一个实数
            System.out.println("您输入的实数是：" + num);
        } else {
            System.out.println("输入的不是实数！");
        }
        scanner.nextLine(); // 读取输入流中的换行符

        System.out.print("请输入一个字符串：");
        if (scanner.hasNextLine()) { // 判断输入流中是否有下一行
            String line = scanner.nextLine(); // 读取输入流中的下一行
            System.out.println("您输入的字符串是：" + line);
        } else {
            System.out.println("输入的不是字符串！");
        }
        scanner.close(); // 关闭 Scanner 对象

```

扫描文件

Scanner 也是可以用来扫描文件的

```java
/**
 * @author: hupengpeng
 * @createDate: 2024年09月02日 13:44
 */
package Scanner_Test;

import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class Scanner_file {
    public static void main(String[] args) {
        try {
            // 创建 File 对象，表示要扫描的文件
            File file = new File("C:\\Users\\13203\\OneDrive\\桌面\\Hello-World-\\Java常用工具类.md");
            Scanner scanner = new Scanner(file); // 创建 Scanner 对象，从文件中读取数据
            while (scanner.hasNextLine()) { // 判断文件中是否有下一行
                String line = scanner.nextLine(); // 读取文件中的下一行
                System.out.println(line); // 打印读取的行
            }
            scanner.close(); // 关闭 Scanner 对象
        } catch (FileNotFoundException e) {
            System.out.println("文件不存在！");
        }
    }
}

```

