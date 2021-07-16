[toc]

# 算法库



算法库 `<algorithm>` 提供大量用途的函数（例如查找、排序、计数、操作），它们在元素范围上操作。

注意范围定义为 `[first, last)` ，其中 `last` 指代要查询或修改的最后元素的*后一个*元素。

注意：first、last为指针或迭代器

1. swap(T a, T b)      //交换a， b值

2. reverse(first, last)    //反转 [first, last) 范围中的元素顺序

   ```c++
   vector<int> v{1,2,3};
   reverse(v.begin(),v.end());
   
   int a[]={4,5,6,7};
   reverse(a, a+4);	//可以使用reverse(begin(a),end(a)) (c++11)
   ```

3. random_shuffle(first, last)   //打乱给定范围 [first, last) 内的元素，每种排列出现的概率相等

4. sort(first, last, comp)

   - 省略comp参数，以升序排序范围 [first, last) 中的元素，不维持相等元素间的顺序（非稳定）

   - 可以通过重载运算符或给定二元函数comp改变排序顺序。

   ```c++
   #include <iostream>
   #include <algorithm>
   using namespace std;
   
   bool comp(int a, int b){
       return a>b;  //comp使用>号表示大的在前面，为降序排列
   }
   int main(){
       int a[] = {1,2,3,4,5,6,7};
       sort(a, a+7, comp);
       //sort在每次比较时使用comp进行比较。
       
       for(auto i:a) cout << i <<endl;
   
   }
   
   ```

   ```c++
   struct student{
       string name;
       int id;
       bool operator<(student b) const{   //重载<运算符
           return id<b.id;
       }
   }
   //sort使用小于运算符进行比较，判定谁在谁前面。
   //因此，对于自己定义的结构体，使用上述方法重载小于运算符，就可以使两个student间可以使用<进行比较，也就可以使用sort进行排序了。
   //这里可以看出是根据id的升序进行排序
   
   ```

5. unique(first, last)

   - 把范围 [first, last) 内连续的重复元素<u>移到末尾</u>。（注意没有删除）
   - 通常先排序，再去重；
   - 返回值为去重后没有重复元素的下一个元素的迭代器

   利用好unique的返回值, 然后用**erase()**删除对应区间(即重复部分)即可完成去重操作，如：

   ```c
   vector<int> v = {1,1,1,1,2,2,5,6,3,4,5};
   sort(v.begin(), v.end());    //先排序
   
   v.erase(unique(v.begin(), v.end()), v.end());		//删除重复元素
   
   for(int i: v){
   	printf("%d", i);
   }
   ```

   ![image-20210705223158455](https://gitee.com/ajream/images/raw/master/img/2021-07-05 22-32-00_image-20210705223158455.png)

6. lower_bound(first, last, a)     

   范围 [first, last) 中元素有序，返回指向范围中首个不小于（即大于或等于） a 的元素的迭代器，或若找不到这种元素则返回 last 。

7. upper_bound(first, last, a)

   范围 [first, last) 中元素有序，返回指向范围中首个大于 a 的元素的迭代器，或若找不到这种元素则返回 last 

8. max(T a, T b)

9. min(T a, T b)

10. max_element(first, last) 

11. min_element(first, last)

12. next_permutation(first, last)  变换范围 [first, last) 为按字典序的下一个排列

13. prev_permutation(first, last)  变换范围 [first, last) 为按字典序的上一个排列



杂项

```c
#include<utility>
pair<T1,T2>//二元组

//创建方法：
pair<int,int> point(1,2);
//赋值方法：
point=make_pair(1,2);

//访问方法：
cout<<point.first<<endl; //1
cout<<point.second<<endl; //2
```

