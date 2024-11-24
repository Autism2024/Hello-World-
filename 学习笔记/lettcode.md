1、Java冒泡排序

```java
/**
 * 这个类用于测试冒泡排序算法。
 */
package org.example;

import java.util.Arrays;

public class ArrayTest {
    public static void main(String[] args) {
        // 初始化一个整型数组
        int[] arr = {10, -1, 8, 0, 34};
        
        // 创建MyTools类的实例
        MyTools myTools = new MyTools();
        
        // 使用MyTools类的bubule方法对数组进行排序
        myTools.bubule(arr);
        
        // 打印排序后的数组
        System.out.println(Arrays.toString(arr));
    }
}

/**
 * 这个类包含了一个用于冒泡排序的方法。
 */
class MyTools {
    /**
     * 对传入的整型数组进行冒泡排序。
     * @param arr 需要排序的数组
     */
    public void bubule(int[] arr) {
        int temp; // 用于交换元素的临时变量
        // 外层循环控制排序的轮数，每轮都将最大的元素放到最后
        for (int i = 0; i < arr.length - 1; i++) {
            // 内层循环进行相邻元素的比较和交换
            for (int j = 0; j < arr.length - i - 1; j++) {
                // 如果当前元素大于下一个元素，交换它们
                if (arr[j] > arr[j + 1]) {
                    temp = arr[j]; // 保存当前元素的值
                    arr[j] = arr[j + 1]; // 将下一个元素放到当前元素的位置
                    arr[j + 1] = temp; // 将保存的当前元素值放到下一个元素的位置
                }
            }
        }
    }
}
```

