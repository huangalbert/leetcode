



```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.nums = nums

    def sumRange(self, left: int, right: int) -> int:
        return sum(self.nums[left: right+1])


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```



```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.sums = nums
        for i, num in enumerate(nums[1:], 1):
            self.sums[i] = num + self.sums[i-1]

    def sumRange(self, left: int, right: int) -> int:
        return self.sums[right] - (0 if left==0 else self.sums[left - 1])

# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```



```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.sums = [0 for _ in range(len(nums) + 1)]
        
        for i in range(len(nums)):
            self.sums[i + 1] = self.sums[i] + nums[i]

    def sumRange(self, left: int, right: int) -> int:
        return self.sums[right + 1] - self.sums[left]
```



> 思路總結：第一個寫法最為簡潔，但必須要考慮到 python 對 list 切片時的效能，剩下兩個寫法是在 __init__ 階段就將所有sum的結果算出暫存。