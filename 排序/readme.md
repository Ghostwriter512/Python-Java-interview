选择排序+冒泡排序+快速排序的python实现
=================================
##  选择排序
&#8195;&#8195;&#8195;把最值放在第一位，再从剩下的找最值放在第二位。

    def select_Sort(alist):  
    
    if len(alist) <= 1:  
        return alist  
    else:  
        for i in range(len(alist)):  
            for j in range(i+1,len(alist)):  
                if alist[i]<alist[j]:  
                    alist[i],alist[j] = alist[j],alist[i]  
        return alist

##  冒泡排序
&#8195;&#8195;&#8195;相邻的两两比较，把最值挤上去，以此类推。

    def bubble_Sort(alist):  
      
    for j in range(len(alist)-1):  
        for i in range(len(alist-1-j)):  
            if alist[i]>alist[i+1]:  
                alist[i],alist[i+1] = alist[i+1],alist[i]  
  
    return alist

##  快速排序
&#8195;&#8195;&#8195;对数列中的每一个数而言，如果比他小的数都在一个方向，而比它大的数都在另一个方向，则可以说，这个数列是有序的。

&#8195;&#8195;&#8195;left：左边数组   right:右边数组  base：基准数

&#8195;&#8195;&#8195;Python.list.pop() : pop()函数用于移除列表中的一个元素（默认最后一个元素），并且返回该元素的值。


    def quick_Sort(nums):  
  
    if len(nums)<= 1 :  
        return nums  
    left = []   
    right = []   
    base = nums.pop()   
  
    for x in nums:  
        if x < base:  
            left.append(x)  
        else:  
            right.append(x)  
    return quick_Sort(left) + [nums] + quick_Sort(right)
