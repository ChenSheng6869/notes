# 剑指Offer📌

[TOC]

# 1 数组与矩阵

* 03.数组中重复的数字


* 04.二维数组中的查找


* 05.替换空格为%20✅
  * StringBuilder


* 29.顺时针打印矩阵


* 50.第一次只出现一次的数

# 2 栈队列、堆

* 09.两个栈实现队列✅
  * A,B分别作为入队,出队的栈

---

* 30.包含min函数的栈✅

---

* 31.栈的压入、弹出序列✅

---

- 40.最小的 K 个数✅**快排重点**🚨
  * **快排**+Arrays.copyOf(arr[], k);

---

- 41.1 数据流中的中位数(Hard),暂时忽略📕

  - 小顶堆+大顶堆

  - ```java
    Queue<Integer> A,B;
    A = new PriorityQueue<>();//小顶堆
    B = new PriorityQueue<>((x,y)->(y-x));//lambda表达式表示大顶堆
    ```

---

- 59.滑动窗口的最大值(Hard),暂时忽略📕

# 3 双指针

- 57.1 和为 S 的两个数字

---

- 57.2 和为 S 的连续正数序列
- 58.1 翻转单词顺序列
- 58.2 左旋转字符串

# 4 链表

- 6.从尾到头打印链表✅
  - **利用栈**:`LinkedList<Integer>() stack = new LinkedList<>();`📌
    - 1.入栈`stack.addLast(head.val)`
    - 2.出栈,放入数组`stack.removeLast()`
    - 3.返回数组

---

- 18.1 删除链表节点✅

  - 遍历链表,遍查遍删:`ListNode pre= head, cur = head.next;` 📌

    - 1.头节点就是要删除的节点;`return head.next;`

    - 2.遍历链表

      ```java
      while(cur != null && cur.val){
          pre = cur;
          cur = cur.next;
      }
      ```

    - 3.删除节点

      ```java
      //更改指针的指向,将当前节点从链表中删除
      if(cur != null) pre.next = cur.next;
      ```

---

- 18.2 删除链表中重复的结点✅

  - 重点:利用set的cotains方法,同18.1删除节点即可.**利用set集合**🚨

    - 1.初始化链表前驱,后置节点;

    - 2.**set用于保存节点的值** 🚨

      `HashSet<Integer> visited = new HashSet<>();`

    - 3.当前节点非空时,利用visited.cotains(cur.val)方法;

    - 4.若存在,删除当前节点

    - 5.不存在,继续遍历

---

- 22.链表中倒数第 K 个结点✅
  - 使用**双指针**🚨
    - 1.初始化节点,former,latter都指向头节点head
    - 2.让former与latter之间相隔k步,former往后走,直至相隔k步.
    - 3.当former为空时,former到链表尾部,与latter之间相隔k哥节点,latter节点即为所需要找的节点.

---

- 24.反转链表✅
  - **方法1:迭代,利用双指针**`cur = head, pre = null;` 🚨
    - 1.保存当前节点的下一个节点`ListNode temp = cur.next;` 
    - 2.将当前节点指向空指针(修改引用)`cur.next = pre;`
    - 3.将当前节点当作pre节点`pre = cur;`
    - 4.将保存的临时节点(next节点给cur)`cur = temp;`
  - **方法2:递归(待补充)** 🚩

---

- 25.合并两个排序的链表✅
  - **方法:初始化新节点(链表)**,`ListNode l3 = new ListNode(0), cur = l3;`
    - 0.l1,l2都不为空时(条件)
    - 1.比较l1,l2结点val的大小
    - 2.将小的节点插入
    - 3.l1,l2为null
    - 4.`cur.next = l1==null ? l2:l1`将后续链表节点插入
    - 5.`return l3.next` ,l3头节点为空,返回后续节点即可.

---

- 35.复杂链表的复制(medium)❎

---

- 52.两个链表的第一个公共结点(medium)❎

---

# 5 树

- 7.重建二叉树✅（medium）

  - 递归，回溯，根据中序遍历判断左右子树边界。
    - 要点：利用HashMap保存中序遍历，根据中序遍历区分根，左右子树🚨

  ```java
  class RebuildTheBinaryTree {
      int[] preorder;
      //用于标记中序遍历
      Map<Integer, Integer> map = new HashMap<>();
  
      public TreeNode buildTree(int[] preorder, int[] inorder) {
          this.preorder = preorder;
          //将中序遍历数组存入map,<key,value>,map.get获取的是value值
          for (int i = 0; i < inorder.length; i++) {
              map.put(inorder[i],i);
          }
          return recur(0,0,inorder.length-1);
      }
      
      TreeNode recur(int root, int left, int right){
          //相等就是自己
          if (left > right) return null;
          //1.建立根节点
          TreeNode node = new TreeNode(preorder[root]);
          //2.获取根节点在中序遍历中的索引，划分左右子树(map.get获取的是value值)
          int i = map.get(preorder[root]);
          //3.左子树根节点，左边界，右边界。
          node.left = recur(root+1, left, i-1);
          //4.右子树的根节点，左边界，右边界。(右子树根节点索引 = 根节点+左子树长度+1)
          node.right = recur(i-left+root+1, i+1, right);
          //5.回溯返回根节点
          return node;
      }
  }
  ```

---

- 8.二叉树的下一个结点

- 26.树的子结构❓
  
  ```java
  public boolean isSubStructure(TreeNode A, TreeNode B) {
          return (A != null && B != null) && (recur(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B));
      }
      boolean recur(TreeNode A, TreeNode B) {
          if(B == null) return true;
          if(A == null || A.val != B.val) return false;
          return recur(A.left, B.left) && recur(A.right, B.right);
      }
  ```
  
  ---
  
- 27.二叉树的镜像🎯

  - 递归，递归遍历（DFS）二叉树，交换每个节点的左右子节点，生成二叉树镜像。

    - 递归解析🧵

      终止条件：节点为空，遍历至叶子节点，返回null

      递归过程：1.初始化临时节点，用于左右节点互换

      ​				   2.递归右子节点，作为根的左子节点

      ​				   3.递归左子节点，作为跟的右子节点

      返回：返回root


  ```java
  public class MirrorTree {
      public TreeNode mirrorTree(TreeNode root){
          if (root == null) return null;
          TreeNode tmp = root.left;
          root.left = mirrorTree(root.right);
          root.right = mirrorTree(tmp);
          return root;
      }
  }
  ```

---

- 28.对称的二叉树✅

  - 解析：对称，左节点==右节点，左子树的左子节点==右子树的右子节点，左子树的右子节点==右子树的左子节点

  ```java
  public class SymmetricTree {
      public boolean isSymmetic(TreeNode root){
          return root == null ? true : recur(root.left, root.right);
      }
      boolean recur(TreeNode L, TreeNode R){
          if (L == null && R == null) return true;
          if (L == null || R == null || L.val != R.val) return false;
          return recur(L.left,R.right) && recur(L.right,R.left);
      }
  }
  ```

  ---

- 32.1 从上往下打印二叉树✅

  - 解析：广度优先搜索（BFS），BFS常借助队列实现
  - 实现：当前节点入队，左右子节点入队，依次出队放入res数组

  ```java
  public class PrintTree {
      public int[] levelOrder(TreeNode root){
          if (root == null) return new int[0];
          Queue<TreeNode> queue = new LinkedList<>();
          ArrayList<Integer> ans = new ArrayList<>();
          queue.offer(root);
          while (!queue.isEmpty()){
              //返回第一个元素并从队列中删除
              TreeNode node = queue.poll();
              ans.add(node.val);
              //将左右子节点放入队列中
              if (node.left != null) queue.add(node.left);
              if (node.right != null) queue.add(node.right);
          }
          int[] res = new int[ans.size()];
          for (int i = 0; i < res.length; i++) {
              res[i] = ans.get(i);
          }
          return res;
      }
  }
  ```

  ---

  > 🛸
  >
  > **add 增加一个元素 如果队列已满，则抛出一个IIIegaISlabEepeplian异常**
  >
  > **remove 移除并返回队列头部的元素 如果队列为空，则抛出一个NoSuchElementException异常**
  >
  > **element 返回队列头部的元素 如果队列为空，则抛出一个NoSuchElementException异常**
  >
  > **offer 添加一个元素并返回true 如果队列已满，则返回false**
  >
  > **poll 移除并返问队列头部的元素 如果队列为空，则返回null**
  >
  > **peek 返回队列头部的元素 如果队列为空，则返回null**
  >
  > **put 添加一个元素 如果队列满，则阻塞**
  >
  > **take 移除并返回队列头部的元素 如果队列为空，则阻塞**

  ---

- 32.2 把二叉树打印成多行✅

  - 解析：在32.1基础上，将每一层节点放入tmp列表，将tmp放入res列表，返回res🎯

  ```java
  public List<List<Integer>> levelOrder(TreeNode root){
          Queue<TreeNode> queue = new LinkedList<>();
          List<List<Integer>> res = new ArrayList<>();
          if (root != null) queue.add(root);
          while (!queue.isEmpty()){
              List<Integer> tmp = new ArrayList<>();
              for (int i = queue.size(); i > 0; i--) {
                  //返回第一个元素并从队列中删除
                  TreeNode node = queue.poll();
                  tmp.add(node.val);
                  //将左右子节点放入队列中
                  if (node.left != null) queue.add(node.left);
                  if (node.right != null) queue.add(node.right);
              }
              //将tmp列表放入res列表中
              res.add(tmp);
          }
          return res;
      }
  ```

  ---

- 32.3 按之字形顺序打印二叉树

- 33.二叉搜索树的后序遍历序列✅

  - 解析

    - 方法一，递归，利用二叉搜索树，左子节点都小于根，右子节点都大于根，左右子树同理。

      根据二叉搜索树的特性，判断所有子树的正确性，如果所有子树都正确，就是此二叉树的后序遍历。

    ```java
    public class PostOrder {
        public boolean verifyPostorder(int[] postorder){
            return recur(postorder, 0, postorder.length-1);
        }
        boolean recur(int[] postorder , int i, int j){
            if (i >= j) return true;
            //遍历左子树，验证左子树序列
            int p = i;
            while (postorder[p] < postorder[j]) p++;
            //遍历右子树，验证右子树序列
            int m = p;
            while (postorder[p] > postorder[j]) p++;
            //左子树在后序遍历序列中的索引：(i, m-1)   j：root
            //右子树在后序遍历序列中的索引：(m, j-1)
            return p==j && recur(postorder, i, m-1) &&recur(postorder, m, j-1);
        }
    }
    
    ```

- 34.二叉树中和为某一值的路径

  - 🎯解析：先序遍历+路径记录

  - 递推流程：1.当前节点加入path

    ​				   2.target-=root.val，直至target为0

    ​				   3.记录路径

    ​				   4.先序：递归左右子节点

    ​				   5.递归回溯时，将当前节点从path中删除，path.pop()

    ```java
    public class PathSum {
        //返回的所有最终路径
        LinkedList<List<Integer>> res = new LinkedList<>();
        //列表path用于保存路径
        LinkedList<Integer> path = new LinkedList<>();
        public List<List<Integer>> pathSum(TreeNode root, int sum){
            recur(root, sum);
            return res;
        }
    
        public void recur(TreeNode root, int tar){
            //空节点，返回
            if (root == null) return;
            //将节点值添加进路径
            path.add(root.val);
            tar-=root.val;
            //tar值为0时,且遍历至叶子节点,将列表path添加进最终列表res
            if (tar == 0 && root.right == null && root.left == null)
                res.add(new LinkedList<>(path));
            recur(root.left, tar);
            recur(root.right, tar);
            //回溯将上一个不符合路径的值移除至列表
            path.removeLast();
        }
    }   
    ```

- 36.二叉搜索树与双向链表

  - 🎯解析：中序遍历+构造双向链表

  - 代码：

    ```java
    class Node {
        public int val;
        public Node left;
        public Node right;
    
        public Node() {
        }
    
        public Node(int val) {
            this.val = val;
        }
    
        public Node(int val, Node left, Node right) {
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }
    
    public class TreeToDoublyList {
        //相邻节点的引用关系
        //pre：前驱节点  cur：当前节点
        //pre.right = cur;  cur.left = pre;
        //循环链表
        //头节点：head  尾节点：tail
        //head.left = tail; tail.right = head;
        Node pre, head;
        //二叉搜索树构建链表
        public Node treeToDoublyList(Node root){
            if (root == null) return null;
            dfs(root);
            head.left = pre;
            pre.right = head;
            return head;
        }
    
        //打印中序遍历
        public void dfs(Node cur){
            if (cur == null) return;
            dfs(cur.left);
            if (pre != null) pre.right = cur;
            else head = cur;
            cur.left = pre;
            pre = cur;
            dfs(cur.right);
        }
    }
    ```

- 37.序列化二叉树

- 54.二叉查找树的第 K 个结点

- 55.1 二叉树的深度

- 55.2 平衡二叉树

- 68.树中两个节点的最低公共祖先

---

**每日一题**

### 2022.5

2022.5.11,序列化搜索二叉树，反序列化搜索二叉树

```java
public class SerializeBinaryTrees {
    //1.序列化二叉搜索树，返回值类型为字符串
    public String serialize(TreeNode root){
        List<Integer> list = new ArrayList<>();
        postOrder(root, list);
        String str = list.toString();
        return str.substring(1,str.length()-1);
    }

    //2.反序列化字符串，返回值为二叉搜索树
    public TreeNode deserialize(String data){
        if (data.isEmpty()) return null;
        String[] arr = data.split(",");
        Deque<Integer> stack = new ArrayDeque<>();
        int len = arr.length;
        for (int i = 0; i < len; i++) {
            stack.push(Integer.parseInt(arr[i]));
        }
        return construct(Integer.MIN_VALUE, Integer.MAX_VALUE, stack);
    }

    //3.后续遍历，添加进list
    private void postOrder(TreeNode root, List<Integer> list){
        if (root == null) return;
        postOrder(root.left, list);
        postOrder(root.right, list);
        list.add(root.val);
    }

    //4.构建搜索二叉树
    private TreeNode construct(int lower, int upper, Deque<Integer> stack){
        if (stack.isEmpty() || stack.peek() < lower || stack.peek() > upper){
            return null;
        }
        int val = stack.pop();
        TreeNode root = new TreeNode(val);
        root.right = construct(val, upper, stack);
        root.left = construct(lower, val, stack);
        return root;
    }
}
```

2022.5.12,字符串数组列排序，删除不是升序的列。

```java
public class MinDeletionSize {
    public int minDeletionSize(String[] strs){
        int row = strs.length;
        int col = strs[0].length();
        int count = 0;
        //i：列，从开始遍历，逐行比较每列对应的的值再字典中是否为升序
        for (int i = 0; i < col; i++) {
            for (int j = 1; j < row; j++) {
                if (strs[j-1].charAt(i) > strs[j].charAt(i)){
                    count++;
                    //跳回第一层循环，比较下一列
                    break;
                }
            }
        }
        return count;
    }
}
```

2022.5.13 字符串有三种编辑操作:插入一个字符、删除一个字符或者替换一个字符。 给定两个字符串，编写一个函数判定它们是否只需要一次(或者零次)编辑。

```java
class Solution {
    public boolean oneEditAway(String first, String second){
        //只需要一次编辑就可以让两次输入的字符串相等
        int len = first.length() - second.length();
        if (len > 1 || len  < -1) return false;
        int count = 1;
        for (int i = 0, j = 0; i < first.length() && j < second.length(); i++,j++) {
            if (first.charAt(i) != second.charAt(j)){
                if (len == 1){
                    j--;
                } else if (len == -1){
                    i--;
                }
                //保证字符串只修改一次
                count --;
            }
        }
        //优化返回值
        return count < 0 ? false : true;
    }
}
```



# 6 贪心思想

- 14.剪绳子
- 63.股票的最大利润

# 7 二分查找

- 11.旋转数组的最小数字
- 53.数字在排序数组中出现的次数

# 8 分治

- 16.数值的整数次方

# 9 搜索

- 12.矩阵中的路径
- 13.机器人的运动范围
- 38.字符串的排列

# 10 排序

- 21.调整数组顺序使奇数位于偶数前面
- 45.把数组排成最小的数
- 51.数组中的逆序对

# 11 动态规划

- 10.1 斐波那契数列
- 10.2 矩形覆盖
- 10.3 跳台阶
- 10.4 变态跳台阶
- 42.连续子数组的最大和
- 47.礼物的最大价值
- 48.最长不含重复字符的子字符串
- 49.丑数
- 60.n个骰子的点数
- 66.构建乘积数组

# 12 数学

- 39.数组中出现次数超过一半的数字
- 62.圆圈中最后剩下的数
- 43.从 1 到 n 整数中 1 出现的次数

# 13 位运算

- 15.二进制中 1 的个数
- 56.数组中只出现一次的数字

# 14 其它

- 17.打印从 1 到最大的 n 位数
- 19.正则表达式匹配
- 20.表示数值的字符串
- 44.数字序列中的某一位数字
- 46.把数字翻译成字符串
- 61.扑克牌顺子
- 64.求 1+2+3+...+n
- 65.不用加减乘除做加法
- 67.把字符串转换成整数

# 15 360笔试

在某个仓库中，堆积了很多的货物，每个货物是一个正方体的，边长为1。所有货物恰好堆积成一个长方体，边长为R * C * L。
目前，在某次确认货物的时候，管理员意识到这一堆货物被小偷偷走了一些。
这个小偷将原来的R * C * L的货物组成的长方体偷成了恰好(R - 2) * (C - 1) * (L - 2)的长方体。
但是管理员记不得R、C、L的具体数值了，他只能计算现在的货物总数。他希望算出来最坏情况下被偷了多少的货物，输出这个最坏的值。输入
输入为一个数 n，表示题面中的(R - 2) * (C - 1) * (L - 2)

输出
输出为一个数，表示最坏情况下被偷了多少的货物

样例输入
4

样例输出
41

提示
对于100%的数据：1 <= n <= 109
样例解释：R = 3, C = 5, L = 3, 3 * 5 * 3 - (3 - 2) * (5 - 1) * (3 - 2) = 41

```java
//原体积R*C*L
//现体积(R - 2) * (C - 1) * (L - 2)
//被偷走的体积：（R0+2*C0+1*L0+1） - (R - 2) * (C - 1) * (L - 2)
//
public class Solution {
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        long n = in.nextLong();
        System.out.println(3*3*(n+1)-n);
    }
}
```

