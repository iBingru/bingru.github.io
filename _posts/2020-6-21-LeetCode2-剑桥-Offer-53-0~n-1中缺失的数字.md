---
layout: post
title: LeetCode-2
---

剑桥-Offer-53 0~n-1中缺失的数字

[题目链接](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

![_config.yml]({{ site.baseurl }}/images/LeetCode/0~n-1中缺失的数字.png)

解题思路

方法一

逐个查找

1. 使用一个for循环加if语句的嵌套方法，对数组中的数字挨个进行比较。
2. 每个数字对应的数组角标正好与其相同，所以使用数组序号与i进行比较。
3. 如果if语句找到不相等的则输出对应的序号，也就是缺少的数字。

代码如下：

	```java
	class Solution {
	    public int missingNumber(int[] nums) {
	        int i;
	        for(i = 0; i < nums.length; i++){
	            if(nums[i] != i){
	                return i;
	            }
	        }
	        return nums.length;
	    }
	}
	```

方法二

二分查找

1. 定义第一个为low，最后一个为heigh，通过low和heigh求出中间数mid，并比较两个数是否相同。
2. 如果相等，则左面排列正确，对右半部分再次进行分析比较。令low = mid+1，重新计算mid值；
3. 如果不相等，则右面排列正确，对左半部分进行分析比较。
4. 令height = mid-1，重新确定mid值，在while循环中一直进行。
5. 最后返回low的值


代码如下：

	```java
	class Solution {
	    public int missingNumber(int[] nums) {
	        int low = 0, heigh = nums.length-1;
	        while(low <= heigh){
	            int mid = low + (heigh - low)/2;
	            if (nums[mid] == mid){
	                low = mid+1;
	            } else {
	                heigh = mid-1; 
	            }
	        }
	        return low;
	    }
	}
	```