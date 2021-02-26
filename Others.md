## Q1:

``` python
def mul():
    return [lambda x: x*i for i in range(4)]
print([m(2) for m in mul()])
# [6, 6, 6, 6]
```

### 等價於：

``` python
def mul():
    l = []
    for i in range(10)
        def lambda_test(x):
            x = x*i
            print(x)
        l.append(lambda_test)
    return l
```



## Q2:

``` python
class root(object):
    x = 10
    
class branch1(root):
    pass

class branch2(root):
    pass


print(root.x, branch1.x, branch2.x)
root.x = 30
print(root.x, branch1.x, branch2.x)
branch1.x = 20
print(root.x, branch1.x, branch2.x)

# 10 10 10
# 30 30 30 
# 30 20 30
```



## Q3:

```python
def appendList(val, l=[]):
    l.append(val)
    return l  
list1 = appendList(1)
list2 = appendList(2, l=[])
list3 = appendList('a')

print(list1) 
print(list2)
print(list3)

# [1, 'a']
# [2]
# [1, 'a']
```

<div> 
  思路總結：考 python 的 function參數被修改後，會影響到其他引用。
</div>



## Q4:

<div style='font-size:20px'>
  使用 filter 和 lambda 實現出 交集、差集、聯集。
</div>



``` python
a = [1,2,3,4,5]
b = [3,4,5,6,7]

def intersection(a, b):
    return list(filter(lambda x: x in a, b))
  
def difference(a, b):
    return list(filter(lambda x: x not in b, a))
  
def union(a, b):
    return a + list(filter(lambda x: x not in a, b))
```



## Q5:

<div style='font-size:20px'>
  使用 map 與 list comprehensive，將輸入 [1, 2, 3, 4, 5] 轉化為 [1, 4, 9, 16, 25]，並選出大於10以上的元素
</div>

``` python
[i for i in map(lambda x: x**2, [1,2,3,4,5]) if i> 10]

# [16, 25]
```



## Q6:

<div style='font-size:20px'>
  寫出一個 reverse function，反轉數字，如：1234 -> 4321、-132 -> -231，並且 input 為一個 32 bits integer
</div>

``` python
def reverse(x: int):
    if not (x >= -2**31 and x < 2**31):
    		raise 'Input exceeds limit!'
    flag = 1
    if x < 0:
        flag = -1
        x*=flag
    result = ''        
    for i in reversed(list(str(x))):
        result = result + i
    return flag*int(result)
```

