# OOP 面向对象

## 是什么 为什么 主要内容

### What is OOPs?

- Type of programming which is based on objects rather than just functions and procedures.
-  Individual objects are grouped into classes.

### Why use OOPs?

- Code can be **reused through inheritance** thereby reducing redundancy
- **Data and code are bound together by encapsulation**
- Allows **data hiding**, therefore, private data is kept confidential
- Can divide problem into sub problems
- The concept of **polymorphism gives flexibility to the program** by allowing the **entities to have multiple forms**

###  What are the main features of OOPs?

- Inheritance
- Encapsulation
- Polymorphism
- Data Abstraction

## Classes and Objects

### What is an object? object是什么

**OBJECT** is an **instance of a class**. It is a self-contained component which **consists of methods and properties** to **make** a particular type of **data useful.** 



### What is a class? class是什么

**CLASS** are a **blueprint** or a set of **instructions** to build a specific type of object.



### What is the difference between a class and an object? 区别

| Object                                                  | Class                                                        |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| A real-world entity which is an **instance of a class** | A class is basically a **template** or a **blueprint** within which objects can be created |
| An object is a **physical** entity                      | A class is a **logical** entity                              |
| Objects can be declared as and when required            | Classes are declared just once                               |



## Main Features

### Inheritance 继承

#### What is inheritance?

Inheritance is a **feature** of OOPs which **allows classes inherit** common properties from **other classes**. 



####  What are the limitations of inheritance? 局限

- **Increases the time** required to execute a program as it requires **jumping back** and forth between **different classes**
- The **parent** class and the **child** class get tightly **coupled**
- Any **modifications** to the program would **require changes both** in the **parent** as well as the **child** class



####  What is a superclass?

Parent of other class/classes



### Polymorphism 多态

#### What is polymorphism?

Polymorphism refers to the **ability to exist in multiple forms**. **Multiple definitions can be given to a single interface.**





### Protected Public Private 区别

#### Private

Like you'd think, only the **class** in which it is declared can see it. **class 里可见**

#### Package Private

It can only be seen and used by the **package** in which it was declared. This is the default in Java (which some see as a mistake). Package 里可见

#### Protected

Package Private + can be seen by subclasses or package members. 

#### Public

Everyone can see it.



# Sorting Algorithms 排序

## Quick Sort 快速排序

Idea: 

1. 随意找pivot（通常是最后一个）
2. 大于pivot放前面，小于放后面
3. 前面和后面array recursively solve

In place方法：

- func(arr,left,right)

- 把pivot swap到最后(right)
- 设置midIdx = left
- for loop 0 到 size-1
- if arr[i] >= arr[midIdx]: swap,然后midIdx++；



# Leetcode

## Permutation 排列

算法：dfs（想象成tree）然后做不同情况的剪枝

### Discrete (没有duplicate) [1,2,3]

1. Discrete (没有duplicate) [1,2,3]

Idea: bool数组确认有没有用过，for loop遍历到等于nums.size()为止

```c++
vector<vector<int>> permutation(vector<int> nums){
  vector<vector<int>> res;
  vector<bool> used 
}

void dfs(vector<vector<int>>& res, vector<int> cur, vector<bool> used){
  if(nums.size() == cur.size()){
    res.push_back(cur);
    return;
  }
  for(int i=0; i<nums.size();i++){
    if(used[i]){
      continue; //如果已经使用（已经在cur里），不需要再继续。
    }
    used[i] = true;
    cur.push_back(nums[i]);
    // recursive 的push back下一个直到cur满
    dfs(res,cur,used);
    // 记得要重设（返回tree的上一个node？）
    cur.pop_back();
    used[i] = false;
  }
}
```

### Duplicate(有重复) [1,1,2]

2. Duplicate(有重复) [1,1,2]

Idea: 基于没有重复的情况下，sort nums，然后添加condition：如果nums[i] == nums[i-1]而且前面的没有用，（不在cur里），证明这个nums[i]在之前已经有一样的情况了。

如果nums[i] == nums[i-1] 而且 used[i-1] == false(不再cur里)，那nums[i-1]必然已经跑过一次并且pop掉了。

```c++
vector<vector<int>> permutation(vector<int> nums){
  vector<vector<int>> res;
  vector<bool> used 
}

void dfs(vector<vector<int>>& res, vector<int> cur, vector<bool> used){
  if(nums.size() == cur.size()){
    res.push_back(cur);
    return;
  }
  for(int i=0; i<nums.size();i++){
    if(used[i] || (i>0 && nums[i]==nums[i-1] && used[i])){
      // i>0 保证不会out of range
      continue; //如果已经使用（已经在cur里），不需要再继续。
    }
    used[i] = true;
    cur.push_back(nums[i]);
    // recursive 的push back下一个直到cur满
    dfs(res,cur,used);
    // 记得要重设（返回tree的上一个node？）
    cur.pop_back();
    used[i] = false;
  }
}
```



## Rotate Image

### Clockwise(顺时针) 90 degree

```
1. reverse upside down
2. swap symmetrically

1,2,3    7,8,9    \      7,4,1
4,5,6 -> 4,5,6 ->  \  -> 8,5,2
7,8,9    1,2,3      \    9,6,3
```

### Anti-Clockwise(逆时针) 90 degree

```
1. reverse left right
2. swap symmetrically

1,2,3    3,2,1    \      3,6,9
4,5,6 -> 6,5,4 ->  \  -> 2,5,8
7,8,9    9,8,7      \    1,4,7
```

