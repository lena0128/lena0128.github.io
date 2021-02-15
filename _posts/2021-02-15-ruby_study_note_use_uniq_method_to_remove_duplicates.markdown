---
layout: post
title:      "Ruby Study Note: Use #uniq method to Remove Duplicates"
date:       2021-02-15 01:26:18 -0500
permalink:  ruby_study_note_use_uniq_method_to_remove_duplicates
---


***uniq() ***is an array class method which returns a new array by removing duplicate values in the array.

**What does the #uniq method do?**
* It will remove all the duplicate values in an array.
* It will return a NEW array with unique values. 
* This mothed will NOT change the original array.

The syntax is: **`uniq → new_ary`**

Here is an Example:

```
numbers = [1, 2, 3, 3, 4, 4, 5]
numbers.uniq
# => [1, 2, 3, 4, 5]

numbers
# => [1, 2, 3, 3, 4, 4, 5]
```


**How to Use #uniq Method with A Block**

If a block is given, the #uniq method will use the return value of the block for comparison. It compares values using their hash and eql? methods for efficiency. 

The syntax is: **`uniq { |item| #your code } → new_ary`**

Here is an example:

```
list = [["fruit","apple"], ["fruit","banana"], ["snack","candy"]]
list.uniq { |fruit| fruit.first } 
# => [["fruit", "apple"], ["snack", "candy"]]

list
# => [["fruit", "apple"], ["fruit", "banana"], ["snack", "candy"]]
```


When calling #uniq, it works by making a hash out of the given array elements. Every element becomes a key in the hash. Since hash keys are unique, we can get a list of all the keys in the hash; This list then becomes our new array with unique elements. When passing a block to #uniq, we can define whatever rules are considered unique.  Try out more practices:  

(1) Comparing the size of the values:
```
fruits = ["orange", "apple", "banana"]
fruits.uniq { |fruit| fruit.size }
# => ["orange", "apple"]
```



(2) Comparing the class of the values:

```
list = [1, 2, "a", "b", :c, :d]
list.uniq { |obj| obj.class }
# => [1, "a", :c]
```


(3) Comparing multiple conditions: 

```
class User
  attr_accessor :name, :age, :country  
  def initialize(name, age, country)
    @name = name 
    @age = age
    @country = country 
  end
end

user_1 = User.new("Mary", "18", "USA")
user_2 = User.new("Joe", "18", "USA")  
user_3 = User.new("Dave", "22", "UK")

[user_1, user_2, user_3].uniq { |user| [user.age, user.country] }  

# => 
[#<User:0x0000000006d56fc8 @age="18", @country="USA", @name="Mary">,
 #<User:0x00000000074d50b0 @age="22", @country="UK", @name="Dave">] 
```



**Difference between #uniq and #uniq!**

The **return value** of #uniq! is different from #uniq. 

```
uniq! → ary or nil
uniq! { |item| ... } → ary or nil
```

The #uniq! method will modify the original array and return with the altered array. For example:

```
numbers = [1, 2, 3, 3, 4, 4, 5]
numbers.uniq！
# => [1, 2, 3, 4, 5]

numbers
# => [1, 2, 3, 4, 5]
```


If no changes are made, it returns nil. For example:
```
arr = [ "a", "b", "c" ]
arr.uniq!   
# => nil
```






*References:*

https://ruby-doc.org/core-2.5.0/Array.html#method-i-uniq

https://www.rubyguides.com/2019/08/ruby-uniq-method/

