---
title: 剑指offer
date: 2019-5-7 15:02:22
categories: 剑指offer
---
### 1.二维数组中的查找
#### 题目描述
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 2.数组中的重复数字
在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

- **思路：**
    寻求空间复杂度最小的答案，就是不用辅助数组，不用HashMap集合；时间复杂度为O(n)，即遍历一次即可；

    
```markdown
    // 方法1
   public boolean duplicate(int numbers[], int length, int[] duplication) {
        boolean[] k = new boolean[length];
        for (int i = 0; i < k.length; i++) {
            if (k[numbers[i]] == true) {
                duplication[0] = numbers[i];
                return true;
            }
            k[numbers[i]] = true;
        }
        return false;
    }
    
    
    //方法2
    public boolean duplicate(int numbers[], int length, int[] duplication) {
            if ((numbers == null) || (length <= 0)) {
                return false;
            }
            for (int i = 0; i < length; i++) {
                while (i != numbers[i]) {
                    if (numbers[i] == numbers[numbers[i]]) {
                        duplication[0] = numbers[i];
                        return true;
                    }
                    int temp = numbers[i];
                    numbers[i] = numbers[numbers[i]];
                    numbers[temp] = temp;
                }
            }
            return false;
        }
```



 ### 68.两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

```markdown
    方法1
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = 1; j < nums.length; j++) {
                if ((nums[j] == (target - nums[i])) && (i != j))
                    return new int[]{nums[i], nums[j]};
            }
        }
        return new int[]{0, 0};
    }
    
     方法2
     public int[] twoSum(int[] nums, int target) {
         
                 HashMap<Integer, Integer> hashMap = new HashMap<Integer, Integer>();
         
                 for (int i = 0;i<nums.length;i++){
                     if (hashMap.containsKey(nums[i])){
                         return new int[]{hashMap.get(nums[i]),i};
                     }
                     hashMap.put(target-nums[i],i);
                 }
                 return null;
             } 
    
    
```
