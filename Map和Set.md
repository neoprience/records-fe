# Map 类似于json对象

1.new Map(["A": 1], ["B", 2])

2.key 不仅是字符串还可以是对象

3.一个key只能对应一个value

4. set, has, delete, get, clear方法

# Set 类似于数组

1.new Set([1, 2, 3, 4])

2. 去重方法
   
3. add, delete, has

4. 不重复，自动排序

5. <strong>没有get方法，通过迭代遍历获取值</strong>

# 特点对比分析

1. Map是个二维数组，Set是一个一个为数组

2. 都不允许键重复
  
3. Map键不能修改，值可以修改；Set不能通过迭代器改变值，因为值就是键
  
4. Map键值对，Set值=键

5. <strong>for...of...迭代器可以使用</strong>

