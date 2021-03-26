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

<div style='font-size:20px'>
  <p>思路總結：了解閉包(closure)與 lambda 的關係。</p>
  <p>關鍵字：closure、capture variable、lambda。</p>
  <p>refer: https://medium.com/citycoddee/python%E9%80%B2%E9%9A%8E%E6%8A%80%E5%B7%A7-4-lambda-function-%E8%88%87-closure-%E4%B9%8B%E8%AC%8E-7a385a35e1d8</p>
</div>



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



## Q7:

找出最大的總和分配，每行每列都只能挑選一個。

```python
a = [
    '(1,2,1)', 
    '(4,1,5)', 
    '(5,2,1)'
] #(1-1)(2-2)(3-3)

b = [
    '(13,4,7,6)',
    '(1,11,5,4)',
    '(6,7,2,8)',
    '(1,3,5,9)'
] #(1-2)(2-4)(3-3)(4-1)

c = [
    '(13,4,7,6,1)',
    '(1,11,5,4,5)',
    '(6,7,2,1,8)',
    '(2,1,1,5,9)',
    '(2,13,1,1,9)'
] #(1-5)(2-1)(3-4)(4-2)(5-3)

d = []


def OptimalAssignment(strArr):
    # 將資料轉換成想要的格式
    str_arr = []
    for row, s in enumerate(strArr, 1):
        row_arr = []
        for col, i in enumerate(s[1:-1].split(','), 1):
            row_arr += [(int(i), '('+str(row)+'-'+str(col)+')')]
        str_arr += [row_arr]
    result = do_assign(str_arr)
    
    return min(result)[1] if result else result # 避免空值，也可以寫在一開始就判斷

def do_assign(strArr):
    result = []
    if len(strArr) == 1:
        return strArr[0]
    row = 0
    for col in range(len(strArr)):
        str_re = do_assign([i[:col]+i[col+1:] for i in strArr[1:]])
        for str_s in str_re:
            result += [(strArr[row][col][0] + str_s[0], strArr[row][col][1] + str_s[1])]
    return result
```

思路總結：使用 dynamic programming 遍歷所有可能



## Q8:

座位分配問題，a = [12,2,6,7,11]，以此為例，第一個元素為座位數目，只會有偶數，排序為兩行，如：

* 1, 2
* 3, 4
* 5, 6
* 7, 8
* 9, 10
* 11, 12

後面的元素為已經被佔取的位置，找出剩餘座位，可以兩兩相連的數目。

```python
def SSS(nums):
    num = set(nums[1:])
    # initial case
    count = 1 if 1 not in num and 2 not in num else 0
    i =3
    while i <= nums[0]:
        if i not in num:
            if i+1 not in num:
                count += 1
                if i-1 not in num:
                    count += 1
            if i-2 not in num:
                count += 1
        elif i+1 not in num and i-1 not in num:
                count += 1
        i += 2
    return count
```

```python 
def SeatingStudents(arr):
    K = arr[0]
    occupied = arr[1:]
    rows = int(K / 2)
    seats = []
    x = 0
    for i in range(rows):
        seats.append([])
        for j in range(2):
            if (x + 1) in occupied:
                full_seat = "Y"
            else:
                full_seat = "N"
            seats[i].append(full_seat)
            x += 1
    print(seats)
    seating = 0
    for i in range(rows - 1):
        if (seats[i][0] == "N") and (seats[i][1] == "N"):
            seating += 1
        if (seats[i][0] == "N") and (seats[i + 1][0] == "N"):
            seating += 1
        if (seats[i][1] == "N") and (seats[i + 1][1] == "N"):
            seating += 1
    if (seats[rows - 1][0] == "N") and (seats[rows - 1][1] == "N"):
        seating += 1
    return seating
```



## Q9:

找出最大的K個總數相加，並且相加的結果必須是偶數

```python
def test2(A, K):
    if len(A) < K:
        return  -1
    elif len(A) == K:
        return -1 if sum(A)%2==1 else sum(A)
    result = []
    A.sort()
    A_even = []
    A_odd = []
    for i in A:
        if i%2 == 0:
            A_even += [i]
        else:
            A_odd += [i]
    # 將 result 指定為偶數群
    result = A_even[-K:]
    # 如果K為奇數，則偶數也必定為奇數個
    if K%2==1 and len(result)%2==0:
        result = result[1:]
    # 補齊 result 剩餘的空位，讓 len(result) == K
    if len(result) < K:
        n = K-len(result)
        result = result + A_odd[-n:]
        A_odd = A_odd[:-n]
    # 開始做置換，如果最小兩個偶數加起來小於最大兩個奇數，就做置換
    if len(result) == K and len(result)>1:
        while result[1]%2 == 0 and len(A_odd)>=2:
            if result[0] + result[1] < A_odd[-1]+A_odd[-2]:
                result = result[2:] + [A_odd.pop(), A_odd.pop()]
    # 有可能出現沒辦法滿足的結果，回傳-1 (K為奇數，而input一個偶數都沒有，可以將判斷放在程式開頭)
    return -1 if sum(result)%2==1 else sum(result)
```



## Q10

依照 input list 建立樹，'#' 代表 None，之後使用 pre-order traversal 輸出結果。

```python
strArr = ['5', '2', '6', '1', '9', '#', '8', '#', '#', '#', '#', '4', '#'] 
	# ['5', '2', '1', '9', '6', '8', '4']
strArr = ['4', '1', '5', '2', '#', '#', '#'] 
	# ['4', '1', '2', '5']
strArr = ['2', '6', '#'] 
	# ['2', '6']
strArr = ['2'] 
	# ['2']
strArr = [] 
	# []

class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
        
class traversal(object):
    def __init__(self):
        self.result = []
    
    def pre_order(self, node):
        if node.val:
            self.result += node.val
            self.pre_order(node.left)
            self.pre_order(node.right)

def ArrayChallenge(strArr):
    node_temp = []    
    # initial root
    root = TreeNode(strArr.pop(0)) if strArr else TreeNode(None)
    if root.val:
        root.left = TreeNode(None)
        root.right = TreeNode(None)
        node_temp += [root.left, root.right]
        
    #bulid the tree
    for s in strArr:
        if node_temp:
            node = node_temp.pop(0)
        node.val = None if s == '#' else s
        node.left = TreeNode(None)
        node.right = TreeNode(None)
        
        if not s == '#':
            node_temp += [node.left, node.right]
    
    # pre-order traversal
    t = traversal()
    t.pre_order(root)
    
    return t.result
```

>  思路總結：由於建樹的規則是依序 input list，所以沒辦法使用 recursion 去做（左邊 node 做完，要換右邊的 node 做，層層堆疊下必須要有上層的資訊可以），所以選擇以一個 list 紀錄依序紀錄 父node，如果node本身的 val 是 None ，則不會進入到 list 中