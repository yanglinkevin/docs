```python
class Solution:

    # 自定义排序
    def minNumber(self, nums: List[int]) -> str:

        from functools import cmp_to_key
        
        def compare(a,b) : 
            return 1 if a+b > b+a else -1
        
        nums = sorted( [str(i) for i in nums] , key=cmp_to_key(compare)) 
        return "".join(nums)
```

快排
前缀树
判断链表有环,求环的入口
最大公因数
两个链表找交点
topK
LRU
两个栈实现一个队列
树层次遍历第一层从左往右，第二层从右向左
随机数产生转换-根据(1,5)随机数生成器，生成(1,7)之内的随机数
最长公共子序列
最长上升子序列
最大子段和
股票买卖系列
合并k个链表
k个一组反转链表
接雨水
二维接雨水
零钱兑换