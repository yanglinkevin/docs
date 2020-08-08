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
