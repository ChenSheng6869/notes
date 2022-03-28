# 剑指Offer

# 1 数组与矩阵

* 剑指offer 03.数组中重复的数字

  ```java
  public class DuplicateNums {
      private void swap(int[] nums, int i, int j){
          int t = nums[i];
          nums[i] = nums[j];
          nums[j] = t;
      }
      //int[] nums = {2,3,1,0,2,5};
      public int duplicate(int nums[]){
          for (int i = 0; i < nums.length; i++) {
              while (nums[i] != i){
                  //2 == 1
                  if (nums[i] == nums[nums[i]]){
                      return nums[i];
                  }
                  //1,3,2,0,2,5
                  swap(nums, nums[i], i);
              }
              swap(nums, nums[i], i);
          }
          return -1;
      }
  }
  ```

* 剑指offer 04.二维数组中的查找

  ```java
  public class Search {
      //矩阵从左至右，从上至下，有规律可循
      //在二位数组中查找一个数，如果target>[i][j]往下，否则往左
      public boolean findNumberIn2DArray(int[][] matrix, int target) {
          if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
              return false;
          //确定二维数组的大小
          int rows = matrix.length, cols = matrix[0].length;
          //从二维数组的右上角开始寻找
          int r = 0, c = cols-1;
          while (r <= rows-1 && c >= 0){
              if (target == matrix[r][c])
                  return true;
              else if (target>matrix[r][c])
                  r++;
              else
                  c--;
          }
          //跳出While循环为止没有与目标值相同的点
          return false;
      }
  }
  ```

* 剑指offer 05.替换空格为%20

  ```java
  class Solution {
      public String replaceSpace(String s) {
         StringBuilder sb = new StringBuilder();
         for(int i = 0; i < s.length(); i++){
             char c = s.charAt(i);
             if(c == ' ') sb.append("%20");
             else sb.append(c);
         }
         return sb.toString();
      }
  }
  ```

  ​