---
layout: post
title: Single Number
subtitle: leetcode算法
tags: CodeMonkey
---

## Single Number  

### 问题描述
>Given an array of integers, every element appears *twice* except for one. Find that single one.
**[single-number](https://leetcode.com/problems/single-number/)**  

### 解决方案
`思路:将所有的数进行异或，得到的结果就是所求的. 基于x^x=0. 相同为0，不同为1.`

```
int singleNumber(vector<int>& nums) 
{
     int single = 0;
     for(size_t index=0; index<nums.size(); ++index)
     {
         single ^= nums.at(index);
     }
     return single;
}     
```


## Single Number II  

### 问题描述

> Given an array of integers, every element appears *three* times except for one. Find that single one. 
**[single-number-ii](https://leetcode.com/problems/single-number-ii/)**

### 解决方案  
`思路：对数组进行排序，从左到右进行计算个数.`

```
int singleNumber(vector<int>& nums) 
{
 	//特殊情况1 
	if(nums.size() == 0)
    {
        return 0;
    }
   
    //特殊情况2
    if(nums.size() == 1)
    {
        return nums.at(nums.size()-1);
    }
    
    size_t count = 1;
    
    sort(nums.begin(), nums.end());
    
    for(size_t index=0; index<nums.size()-1; ++index)
    {
        if(nums.at(index) == nums.at(index+1))
        {
            count++;
        }
        else
        {
            if(count < 3) 
            {
                return nums.at(index);
            }
            
            count = 1;
        }
    }
    
    //特殊情况3 最后一个是single number的特殊情况
    return nums.at(nums.size()-1);
}
```  

`思路2`  

```
int singleNumber(vector<int>& nums) 
{
	int result = 0;
	vector<int> count(32, 0);
	
	for(int i=0; i<count.size(); ++i)
	{
	    for(int j=0; j<nums.size(); ++j)
	    {
	        count[i] += 1 & (nums.at(j) >> i);
	    }
	}
	
	for(int i=0; i<count.size(); ++i)
	{
	    if(count.at(i) %3 != 0)
	        result = result + (1<<i);
	}
	return result;
}
```  

`思路3`  

```
int singleNumber(vector<int>& nums) 
{
    int counterOne = 0;
    int counterTwo = 0;

    for (int i = 0; i < nums.size(); i++){
        counterOne = (~counterTwo) & (counterOne ^ nums[i]);
        counterTwo = (~counterOne) & (counterTwo ^ nums[i]);
    }
    
    return counterOne;    
}
```
