## 题目


## 描述

   Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
   
   Note:
 The solution set must not contain duplicate triplets.
 Example:
 Given array nums = [-1, 0, 1, 2, -1, -4],
 A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]

## 思路

 关键是不能重复，比如[-1,0,1],[0,1,-1]就是两个重复的数组
所以把输入的input排序

## 实现

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    let result=[];
    let l=nums.length
    //这边有个坑就是sort排序，-2会小于-4
    //nums.sort(function(){
      //  return a-b>0
    //})
    nums.sort(function(a,b){
          return a-b
    })
    for(let i=0;i<l-2;i++){
        if(i==0||(i>0&&nums[i]!=nums[i-1])){
           let start=i+1,end=l-1,num3=0-nums[i]
            while(start<end){
                if(nums[start]+nums[end]==num3){
                    result.push([nums[start],nums[end],nums[i]])
                    //碰到相同的元素往后移，或者往前移
                    while(start<end&&nums[start]==nums[start+1])start++
                    while(start<end&&nums[end]==nums[end-1])end--
                    start++
                    end--
                }else if(nums[start]+nums[end]<num3){
                    start++
                }else{
                    end--
                }
            }
        }
    }
    return result
};
```