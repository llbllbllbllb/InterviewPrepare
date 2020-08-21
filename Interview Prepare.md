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





# RESTful API

##  **what is RESTFUL**

**REST** : **RE**presentational **S**tate **T**ransfer

**focuses on system resources(data)** and **how** state of resource should be **transported over HTTP protocol** to different clients written in different language. In RESTFUL web service HTTP methods example: GET, POST, PUT and DELETE 



## **Features of Restful API?**

- HTTP for client server communication
- XML/JSON as formatting language
- Simple URI as the address for the services
- Stateless communication (independent calls)



## **How to design good RESTFul API**

- **Every input** on the server should be **validated**.
- Input should be well-formed.
- No sensitive data through URL.
- For any session, the **user** should be **authenticated**.
- Use **message format** that is **easily understood** and is required by the client.
- **(URI)**Unified Resource Identifier **should be descriptive and easily understood**.





## **Core components of the HTTP request and HTTP response?**

### HTTP request

- **Verb:** Includes methods like GET, PUT, POST, etc.
- **URI**Uniform Resource Identifier for identifying the resources available on the server.
- HTTP Version for specifying the HTTP version.
- HTTP Request **header** for containing the information about the data.
- HTTP Request **body** that contains the representation of the resources in use.



### **HTTP Response**

- **Request Code:** This contains various codes that determine the status of the server response.
- HTTP Version for specifying the HTTP version.
- HTTP Response **header** for containing the information about the data.
- HTTP Response **body** that contains the representation of the resources in use.



## HTTP methods

- **GET:** This is a read-only operation that fetches the list of users on the server.
- **PUT:** This operation is used for the creation of any new resource on the server.
- **POST:** This operation is used for updating an old resource or for creating a new resource.
- **DELETE:** As the name suggests, this operation is used for deleting any resource on the server.
- **OPTIONS:** This operation fetches the list of any supported options of resources that are available on the server.



## **Statelessness**

In REST, ST itself defines State Transfer and Statelessness means **complete isolation**. This means, **the state of the client’s application is never stored on the server** and is passed on.

How to be stateless?: Every client passes a ‘session identifier’ which also acts as an identifier for each session.



## Difference between PUT POST

PUT is idempotent meaning, invoking it any number of times will not have an impact on resources. 

However, POST is not idempotent, meaning if you invoke POST multiple times it keeps creating more resources



## **What is Caching?**

Caching is the **process in which server response is stored** so that a cached copy can be used when required and there is **no need for generating the same response again**. This process not only **reduces the server load** but in turn increase the scalability and performance of the server. Only the client is able to cache the response and that too for a limited period of time.



# Sorting Algorithms 排序

## Complexity

![Must-Know Sorting Algorithms in Python - Zax Rosenberg](https://zaxrosenberg.com/wp-content/uploads/2017/12/sort_complexity.png)





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

Idea: 基于没有重复的情况下，sort nums，然后添加condition：**如果nums[i] == nums[i-1]而且前面的没有用，**（不在cur里），证明这个nums[i]在之前已经有一样的情况了。

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



## Rotate Image / Matrix

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

