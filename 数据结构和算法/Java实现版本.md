## Java实现版本
（参考算法4）

---
---
### 基础算法
#### 欧几里得算法（求最大公约数）

核心思想就是辗转相除: gcd(m, n) = gcd(m, m % n)
```java

public class GcdAlgorithms {
    public static void main(String[] args) {
        int result = gcd2(100, 10);
        System.out.println(result);
    }
//    非递归实现，循环
    private static int gcd(int m, int n) {
        while (n != 0) {
            int rem = m % n;
            m = n;
            n = rem;
        }
        return m;
    }
//    递归实现
    private static int gcd2(int m, int n) {
        if(n==0){
            return m;
        }
        int p = m%n;
        return gcd2(n, p);
    }
}
```
---

#### 判断随机整数是否为素数

注意 i 取平方减少判断次数,因为一个数不可能被大于自己完全平方根的数整除

```java

import java.util.Random;

public class numsDemo {
    public static void main(String[] args) {
        System.out.println("生成的随机整数是否为素数？" + isPrime(101));
    }
    public static boolean isPrime(int bound) {
        Random random = new Random();
        int x = random.nextInt(bound);
        if (x < 2) return false;
        else {
            for (int i = 2; i*i < x; i++) {
                if (x % i == 0) return false;
            }
            return true;
        }
    }
}
```

---
#### 牛顿迭代法（求完全平方根）
Java实现开平方的牛顿迭代法. 就是求f(x)=x^2-C的根的正根。
推导过程参考：
https://baike.baidu.com/item/牛顿迭代法
和
https://blog.csdn.net/ccnt_2012/article/details/81837154
```java
import java.util.Random;

public class numsDemo {
    public static void main(String[] args) {
        System.out.println("生成的随机浮点数的完全平方根为" + sqrt(100));
    }

    public static double sqrt(int bound) {
        Random random = new Random();
        double c = random.nextInt(bound) + random.nextDouble();

        if (c < 0) {
            return Double.NaN;
        }
        double e = 1e-15;
        double x = c;
        double y = (x + c / x) / 2;
        while (Math.abs(x - y) > e) {
            x = y;
            y = (x + c / x) / 2;
        }
        return x;
    }
}
```

---
---

### 查找
#### 二分查找
```java
public class binarySearch {
    public static void main(String[] args) {
        int[] nums = new int[]{2, 3, 4, 5, 6, 7, 8, 9};
        System.out.println(search(5, nums, 0, nums.length));
        System.out.println(search2(5, nums));
    }

    //    递归版本
    public static int search(int key, int[] nums, int low, int high) {
        int mid = (low + high) / 2;
        if (nums[mid] == key) {
            return mid;
        } else if (nums[mid] < key) {
            low = mid + 1;
            return search(key, nums, low, high);
        } else if (nums[mid] > key) {
            high = mid - 1;
            return search(key, nums, low, high);
        }
        return -1;
    }

    //    非递归版本
    public static int search2(int key, int[] nums) {
        int low = 0;
        int high = nums.length;
        int mid = (low + high) / 2;
        while (low <= high) {
            mid = (low + high) / 2;
            if (nums[mid] == key) {
                System.out.println(nums[mid] == key);
                return mid;
            } else if (nums[mid] < key) {
                low = mid + 1;
            } else if (nums[mid] > key) {
                high = mid - 1;
            }
        }
        return -1;
    }
}
```

---
---

#### 排序实现

<div align="center"> <img src="./pic/sort.png"/> </div>

1. 插入排序思想

1)直接插入排序：
```java
public class insert{
    public static void insertSort(int[] a) {
        for (int i = 0; i < a.length - 1; i++) {
            for (int j = i + 1; j > 0; j--) {
                if (a[j] < a[j - 1]) {
                    int temp = a[j];
                    a[j] = a[j - 1];
                    a[j - 1] = temp;
                }
            }
        }
    }
}
```

2）折半插入排序
```java
public class insert{
    public static void insertSort(int[] a) {
        int n = a.length;
        for(int i=1;i<n;i++){
            int temp = a[i];
            int low=0;
            int high=i-1;
            while(low <= high){
                int mid = (low+high)/2;
                if(a[mid]>temp){
                    high = mid-1;
                }else{
                    low = mid+1;
                }
            }
    
            for(int j=i-1;j>=low;j--){
                a[j+1] = a[j];
            }
    
            a[low] = temp;
        }
    }
}
```

3）希尔排序

```java


```




3.选择排序思想

1)简单选择排序

```java
public class Selection{

    public static void selectSort(int[] a){
        int N = a.length;
        for(int i =0; i<N; i++){
            int minIndex = i;
            for(int j = i+1; j<N; j++){
                if(a[j]<a[minIndex]) minIndex = j
            }
        }
    }
}


```

2 希尔排序

```java

```


---
#### 树算法

BFS：

```java

public void levelOrderTraversal(TreeNode root){
      if(node==null){
            System.out.print("empty tree"); 
            return;
      }
      LinkedList<ListNode> queue = new LinkedList<>();
      queue.add(root);
      while(!queue.isEmpty()){
            ListNode node = queue.poll();
            System.out.print(node.val+"  ");
            if(node.left!=null){
                  queue.add(node.left);
            }
            if(node.right!=null){
                  deque.add(node.right);
            }
      }
}

```

---

DFS：
```java
public void depthTraversal(TreeNode root){
       if(node==null){
             System.out.print("empty tree");
             return;
       }
       LinkedList<TreeNode> stack = new LinkedList<>();
       stack.push(root);
       while(!stack.isEmpty()){
             TreeNode node = stack.pop();
             System.out.print(node.val);
             if(node.right!=null){
                   stack.push(node.right);
             }
             if(node.left!=null){
                   stack.push(node.left);
             }
       }
}
```

---

层序遍历：

---

中序遍历非递归

---
---

