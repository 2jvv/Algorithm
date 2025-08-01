![[Pasted image 20250113102204.png]]



一般ACM或者笔试题的时间限制是1秒或2秒。  
在这种情况下，C++代码中的操作次数控制在 ![image](https://cdn.nlark.com/yuque/__latex/5c268cea173f6049c2384fbff20bfcd4.svg) 为最佳。

下面给出在不同数据范围下，代码的时间复杂度和算法该如何选择：

1. ![image](https://cdn.nlark.com/yuque/__latex/384f78e4a8a7a7112d9e0ea088a00a0e.svg), 指数级别, dfs+剪枝，状态压缩dp
2. ![image](https://cdn.nlark.com/yuque/__latex/0594c914dbe608671e0880d82bdbb298.svg) => ![image](https://cdn.nlark.com/yuque/__latex/a77815a52a2d0050828079fb142b1410.svg)，floyd，dp，高斯消元
3. ![image](https://cdn.nlark.com/yuque/__latex/d2b5466a32c7a64c35af79f241fb9730.svg) => ![image](https://cdn.nlark.com/yuque/__latex/f2d5f588234eb61a559ff90c41511b85.svg)，![image](https://cdn.nlark.com/yuque/__latex/b6e6dc74e8d61fef571a29671fc37e76.svg)，dp，二分，朴素版Dijkstra、朴素版Prim、Bellman-Ford
4. ![image](https://cdn.nlark.com/yuque/__latex/253f9aedf1add9d923e1e2a2b09b8a34.svg) => ![image](https://cdn.nlark.com/yuque/__latex/c846cfde2a59452be86dbb5d7cc2b1f3.svg)，块状链表、分块、莫队
5. ![image](https://cdn.nlark.com/yuque/__latex/9ee75a82fd9056706244486965dee1aa.svg) => ![image](https://cdn.nlark.com/yuque/__latex/9a4b19897e03daeb7e8beeecf02e82cc.svg) => 各种sort，线段树、树状数组、set/map、heap、拓扑排序、dijkstra+heap、prim+heap、Kruskal、spfa、求凸包、求半平面交、二分、CDQ分治、整体二分、后缀数组、树链剖分、动态树
6. ![image](https://cdn.nlark.com/yuque/__latex/95249eb2ab2a287daa01e87be899bd9f.svg) => ![image](https://cdn.nlark.com/yuque/__latex/e65a67ac353abeeff44c359310d05c02.svg), 以及常数较小的 ![image](https://cdn.nlark.com/yuque/__latex/9a4b19897e03daeb7e8beeecf02e82cc.svg) 算法 => 单调队列、 hash、双指针扫描、BFS、并查集，kmp、AC自动机，常数比较小的 ![image](https://cdn.nlark.com/yuque/__latex/9a4b19897e03daeb7e8beeecf02e82cc.svg) 的做法：sort、树状数组、heap、dijkstra、spfa
7. ![image](https://cdn.nlark.com/yuque/__latex/d5435cfcec57eaa9ac83b1b876dd5e2b.svg) => ![image](https://cdn.nlark.com/yuque/__latex/e65a67ac353abeeff44c359310d05c02.svg)，双指针扫描、kmp、AC自动机、线性筛素数
8. ![image](https://cdn.nlark.com/yuque/__latex/46fb5db702ec308da1a4043279a967fe.svg) => ![image](https://cdn.nlark.com/yuque/__latex/fdb3dafc4d9679ab6e4fc92347398ed1.svg)，判断质数
9. ![image](https://cdn.nlark.com/yuque/__latex/92dbfbd9820dd04c84241dbbd01a838f.svg) => ![image](https://cdn.nlark.com/yuque/__latex/1b0fce2bd1f5925667628ba7a81a4635.svg)，最大公约数，快速幂，数位DP
10. ![image](https://cdn.nlark.com/yuque/__latex/1317a9875366965f70b259c0e0b92d0c.svg) => ![image](https://cdn.nlark.com/yuque/__latex/102dc7113a44ec36f567abd4b01dc5c8.svg)，高精度加减乘除
11. ![image](https://cdn.nlark.com/yuque/__latex/4be12b235643cdf70a6026a8ebf3ad30.svg) => ![image](https://cdn.nlark.com/yuque/__latex/d7c482861ded03d97091f1a8d81907a7.svg)，高精度加减、FFT/NTT

### '快速排序'
**思路**：快速排序是在未排序数组中找一个基准（最左边的数），将所有比基准数小的数放在基准数左边，大的数放在基准数右边。最后在基准数左边用同样的方法，右边用同样的方法直到为顺序集合  
**代码**

```cpp
void quick_sort(int l, int r)//快速排序

{

    if (l >= r)

        return;

    int rnd_idx = rand() % (r - l + 1) + l;

    int i = l - 1, j = r + 1, x = nums[rnd_idx];//随机取一个中间值

    while (i < j)//注意是小于

    {

        do

            i++;

        while (x > nums[i]);

        do

        {

            j--;

        } while (x < nums[j]);

        if (i < j)

            swap(nums[i], nums[j]);

    }//将整个数组分为小于或等于x 和 大于x两部分

    quick_sort(l, j);//在递归

    quick_sort(j + 1, r);

}
```

### 快速选择算法
**定义**：  
快速选择算法（Quickselect）是一种在未排序的数组中查找第k小/大元素的算法，时间复杂度为O(n)。它的基本思想是选择一个基准值（pivot），将数组分为两部分，一部分小于等于基准值，一部分大于基准值。然后根据k与基准值的大小关系，选择其中一部分进行递归搜索，直到找到第k小/大元素为止。快速选择算法和快速排序算法的思路类似，但是快速选择算法只需要对一部分数组进行快速排序，而不需要对整个数组进行排序。因此，快速选择算法的平均时间复杂度为O(n)，最坏时间复杂度为O(n^2)，但是最坏情况出现的概率很小。快速选择算法的时间复杂度为O(n)，空间复杂度为O(1)

**基本步骤**   
选择一个基准值pivot，可以选择数组中的任意一个元素。

将数组分为两部分，一部分小于等于pivot，一部分大于pivot。

如果k小于等于左边部分的元素个数，那么继续在左边部分中查找第k小元素；否则，在右边部分中查找第k-left个小元素。

重复步骤2和3，直到找到第k小元素为止。  
**代码**

```plain
```cpp
ll quick_select(int l, int r, int q)
{
    if (l >= r)
        return a[l];//最后当l==r时数组的值一定是要找的值
    int i = l - 1, j = r + 1, x = a[rand() % (r - l + 1) + l];
    while (i < j)
    {
        while (a[++i] < x)
            ;
        while (a[--j] > x)
            ;
        if (i < j)
            swap(a[i], a[j]);
    }
    int s = j - l + 1;//此时[l,j]数组的这段范围是小于等于 x的[j+1,r]这段范围大于x
    if (q <= s)
        return quick_select(l, j, q);
    else
        return quick_select(j + 1, r, q - s);
    //最后返回的值是第q小的数最小的数是第一位
}
```

```plain

```

### 归并排序
**思路**：先分在和  
归并排序算法有两个基本的操作，一个是分，也就是把原数组划分成两个子数组的过程。另一个是治，它将两个有序数组合并成一个更大的有序数组。  
将待排序的线性表不断地切分成若干个子表，直到每个子表只包含一个元素，这时，可以认为只包含一个元素的子表是有序表。  
将子表两两合并，每合并一次，就会产生一个新的且更长的有序表，重复这一步骤，直到最后只剩下一个子表，这个子表就是排好序的线性表。

**代码**

```cpp
void merge_sort(int nums[],int l,int r)//归并排序

{

    if(l>=r)return;

    int mid=(l+r)/2;

    merge_sort(nums,l,mid);//把元素组划分为两个子数组，最后数组中只包含一个元素

    merge_sort(nums,mid+1,r);

    int k=0,i=l,j=mid+1;

    while(i<=mid && j<=r)

    {

        if(nums[i]<nums[j])tmp[k++]=nums[i++];

        else tmp[k++]=nums[j++];

    }//比较，将更小的那个赋值给tmp数组

    while(i<=mid)tmp[k++]=nums[i++];

    while(j<=r)tmp[k++]=nums[j++];
    //防止没有赋值完

    for(i=l,j=0;i<=r;j++,i++)nums[i]=tmp[j];//将排序好的数组赋值给原数组

}
```



### 利用归并排序求逆序对
**思路**  
归并排序是将一个序列分成两个有序的序列，归并两个有序序列，归并后则该序列有序，是基于分治的思想。

根据逆序对的定义，我们也可以使用分治的算法来求解逆序对的数量。如图：

我们将序列分成两部分，我们发现逆序对的数量是三种逆序对数量的和：

左边序列的逆序对  
右边序列的逆序对  
横跨中间的逆序对

利用归并排序，我们可以分别求解左边序列的逆序对的数量和右边序列的逆序对的数量。但是我们还需要求解横跨中间的逆序对的数量。  
![[Pasted image 20240724201959.png]]

意味着在归并两个序列的过程中，我们就可以计算出横跨中间的逆序对的数量。  
时间复杂度O(nlogn)，空间复杂度O(N)  
**代码**

```cpp
ll merge_sort(int l,int r)

{

    if(l>=r)

    {

        return 0;

    }

    int i = l, mid = (l + r) / 2, j = mid + 1,k=0;

    ll res = merge_sort(l, mid) + merge_sort(mid + 1, r);//将区间分为两份，分到最小的时候在开始合并
    while (i <= mid && j <= r)

    {

        if(a[i]<=a[j])

            tmp[k++] = a[i++];

        else

        {
            tmp[k++] = a[j++];//这时候数组是排好序的在a[i]后的数一定都大于a[j]；

            res += mid - i + 1;//所以逆序数就是在mid到i之间的

        }

    }

    while(i<=mid)tmp[k++]=a[i++];

    while(j<=r)tmp[k++] = a[j++];

    for (int i = l, j = 0; i <= r;i++)

    {

        a[i] = tmp[j++];

    }

    return res;
    //最后返回逆序对的值即可

}
```

### 二分查找：前提是数组已经排好序
<font style="background-color:#f3bb2f;">l,r取谁谁就要在区间内，如取r，l就要在取得最小区间减一，反之亦然</font>  
**思想**  
以在一个升序数组中查找一个数为例。它每次考察数组当前部分的<font style="color:#DF2A3F;">中间元素，如果中间元素刚好是要找的，就结束搜索过程；如果中间元素小于所查找的值，那么左侧的只会</font>更小，不会有所查找的元素，只需到右侧查找；如果中间元素大于所查找的值同理，只需到左侧查找。



**代码**  


[34. 在排序数组中查找元素的第一个和最后一个位置 - 力扣（LeetCode）](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

```cpp
class Solution {

public:

    vector<int> searchRange(vector<int>& nums, int target) {

        vector<int> ans;

        if (nums.size() == 0) {

            ans.push_back(-1);

            ans.push_back(-1);

            return ans;

        }

        int left = -1, right = nums.size(), mid;//确定left和right的范围时一定要根据最后退出条件left+1=right，如果最后结果要取right则left就要在数组最小范围减一反之亦然

        while (left + 1 != right) {

            mid = (left + right) / 2;

            if (nums[mid] < target) {

                left = mid;

            } else {

                right = mid;

            }

        }

        // 如果未找到目标值
    //最后要判断right是否在数组范围内，不然会出错
        if (right == nums.size() || nums[right] != target) {

            ans.push_back(-1);

            ans.push_back(-1);

            return ans;

        }

        // 目标值的左边界

        ans.push_back(right);

        // 重置左边界和右边界，查找目标值的右边界

        left = -1;

        right = nums.size();

        while (left + 1 != right) {

            mid = (left + right) / 2;

            if (nums[mid] > target) {

                right = mid;

            } else {

                left = mid;

            }

        }

        // 添加右边界

        ans.push_back(left);

        return ans;

    }

};
```

### stl c++二分函数
C++ 标准库中实现了查找首个不小于给定值的元素的函数 `std::lower_bound` 和查找首个大于给定值的元素的函数 `std::upper_bound`，二者均定义于头文件 `<algorithm>` 中。

二者均采用二分实现，所以调用前必须保证元素有序。

### 浮点数二分
```cpp
#include <iostream>

#include <iomanip>

#include <cmath>

using namespace std;

// #define double long double

const double eps = 1e-12;

int main()

{

    int T = 1;

    cin >> T;

    while (T--)

    {

        double n;

        cin >> n;

        double l = 0, r = 100000, res = 0;

        while (l <= r) // 二分法查找答案

        {

            double mid = (l + r) / 2;

            if (fabs(mid * mid * mid - n) <= eps) // 满足精度

            {

                res = mid;

                break;

            }

            if (mid * mid * mid > n)

                r = mid - 0.0001;

            else if (mid * mid * mid < n)

                l = mid + 0.0001, res = mid; // 当满足条件不满足精度时返回一个近似值

        }

        // cout << setprecision(3) << fixed << res << endl; //setprecision(3)函数用来保留有效数字，fixed用来防止浮点数科学计数法

        printf("%.3lf\n", res);

    }

    return 0;

}
```



```cpp
#include <iostream>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <string>

using namespace std;

const int N = 2e5 + 10;

using ll = long long;

ll a[N];

ll tmp[N];

ll cont = 0;

void solve()

{

    double n;

    cin >> n;

    double l=-10000,r=10000,mid;

    while(r-l>=1e-8)//如果题目要求保留到第n位小数，则r-l>=1e-(n+2)

    {

        mid = (l + r) / 2;

        if (mid*mid *mid>n)

            r = mid;

            else

                l = mid;

    }

    printf("%lf", l);

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



## 高精度
#### 高精度小数乘法模板
利用小数乘整数，小数位数不变的原则先记录下小数点的位置，然后将小数乘法转换为整数乘法，最后加上在指定位置输出小数点即可

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <bitset>
#include <sstream>
#include <numeric>
using namespace std;
const int N = 1e6 + 10;
using ll = long long;
using ull = unsigned long long;
string s;
int cnt = 0;
vector<int> a(11000);
void mul(int t)
{
	for (int i = 0; i < cnt;i++)
	{
		a[i] *= 2;
	}
	for (int i = 0; i < cnt;i++)
	{
		if(a[i]>=10)
		{
			a[i + 1] += a[i] / 10;
			a[i] %= 10;
		}
	}
	if(a[cnt])
		cnt++;
}
void solve()
{
	int n;
	cin >> n;
	cin >> s;
	int t = s.size();
	int loc; // 记录小数点位置
	for(int i=s.size()-1;i>=0;i--)
	{
		if(s[i]!='.')
		{
			a[cnt++] = s[i] - '0';
		}
		else
		{
			loc = s.size() - 1 - i;//小数点位置从左往右数的位置
		}
	}
	for (int i = 0; i < n;i++)
	{
		mul(2);
	}
	if(a[loc-1]>=5)//四舍五入
	{
		a[loc]++;
	}
  for (int i = 0; i < cnt;i++)
	{
		if(a[i]>=10)
		{
			a[i + 1] += a[i] / 10;
			a[i] %= 10;
		}
	}
	if(a[cnt])
		cnt++;
    /*
	for (int i = cnt - 1; i >= loc; i--) cout << a[i];*/
    for (int i = cnt - 1; i >= 0; i--) 
	{
		if(i==loc-1)
		{
			cout << '.';
		}
		cout << a[i];
	}
    
}
int main()
{
	ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
	int T;
	T = 1;
	while (T--)
		solve();
	return 0;
}
```

#### 高精度加法
[P1601 A+B Problem（高精） - 洛谷 | 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/problem/P1601)

**代码**

```cpp
vector <int> add(vector <int> &a,vector<int> &b)

{

    int t = 0, i = 0;

    vector<int> ans;

    for (int i = 0; i < a.size() || i < b.size();i++)

    {

        if(i<a.size())

            t += a[i];

        if(i<b.size())

            t += b[i];

        ans.push_back(t % 10);//两数相加后

        t = t / 10;//t进位

    }

    if(t)//最后t只有可能时是0 、1，如果为1则要在数组后面加一位

        ans.push_back(1);

    return ans;

}

void solve()

{

    string s1, s2;

    cin >> s1 >> s2;

    vector<int> a, b;

    for (int i = s1.size()-1; i >=0;i--)

    {

        a.push_back(s1[i] - '0');

    }

    for (int i = s2.size() - 1; i >= 0; i--)

    {

        b.push_back(s2[i] - '0');

    }

    vector<int> ans = add(a, b);

    for (int i = ans.size()-1;i>=0;i--)

    {

        cout << ans[i];

    }

}
```



#### 高精度减法
[P2142 高精度减法 - 洛谷 | 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/problem/P2142)  
**代码**

```cpp
bool cmp(vector<int> a,vector<int>b)//比较a和b的大小，如果a比b小则输出的时候先输出一个负号即可

{

    if(a.size()!=b.size())

        return a.size() > b.size();

    for (int i = a.size() - 1; i >= 0; i--)

    {

        if(a[i]!=b[i])

            return a[i] > b[i];

    }

    return true;

}

vector <int> sub(vector <int> &a,vector<int> &b)

{

    int t = 0, i = 0;

    vector<int> ans;

    for (int i = 0; i < a.size();i++)//从个位开始

    {

        t = a[i] - t;

        if(i<b.size())

            t -= b[i];

        ans.push_back((t + 10) % 10);
        //此处包含两种情况，如果t<0,则加入(t+10);
        //如果t>0则直接加入t

        if(t<0)//如果t<0;代表要借位

            t = 1;

        else

        {

            t = 0;

        }

    }

    while (ans.size() > 1 && ans.back() == 0)

    {

        ans.pop_back();

    }

    return ans;

}
```

#### 高精度乘法:高精度×低位数类型
[793. 高精度乘法 - AcWing题库](https://www.acwing.com/problem/content/description/795/)

```cpp
vector <int> mul(vector <int> &a,int b)
{
    vector<int> ans;
    int t = 0;
    for (int i = 0; i < a.size() || t;i++)//注意要判断最后t是否为0若不为0则要加入到数组后
    {
        if(i<a.size())
            t += a[i] * b;
        ans.push_back(t%10);
        t = t / 10;
    }
    while(ans.back()==0 && ans.size()>1)//最后去除前导0
    {
        ans.pop_back();
    }
    return ans;
}
```

#### 高精度乘法:高精度×高精度类型
[高精度练习之乘法 II - 问题 - MYOJ](http://47.110.135.197/problem.php?cid=1612&pid=3)  
**思路**  
先将每一位乘了之后再依次相加，相乘时可以找规律  
![[Pasted image 20240725202156.png]]

```cpp
vector<int> mul(vector<int> &a, vector<int> &b)

{

    vector<int> ans(a.sizle()+b.size()+10,0);//一定要多分配数组空间

    int t = 0;

    for (int i = 0;i<a.size();i++)

        for (int j = 0; j < b.size();j++)

            {

                ans[i + j] += a[i] * b[j];//可以找到数组相乘的规律下标

            }

     t = 0;

    for (int i = 0; i < ans.size();i++)

    {

        t += ans[i];

        ans[i] = t % 10;

        t /= 10;

    }

    while(ans.back()==0 && ans.size()>1)//去前导0

        ans.pop_back();

    return ans;

}
```

#### 高精度除法
```cpp
vector<int> div(vector<int> &a, int b,int &r)//用引用传入余数r
{
    vector<int> ans;
    for (int i = a.size()-1; i>=0;i--)
    {
        r = r * 10 + a[i];
        ans.push_back(r / b);
        r = r % b;
    }
    reverse(ans.begin(), ans.end());//翻转数组，记得要在翻转后去除前导0
    while(ans.back()==0 && ans.size()>1)
        ans.pop_back();
    return ans;
}
```

#### 高精度除高精度(absent)
## 前缀和与差分
#### 前缀与差分的联系
![[Pasted image 20240715101002 1.png]]

#### 一维前缀和
[795. 前缀和 - AcWing题库](https://www.acwing.com/problem/content/797/)  
**定义**  
前缀和可以简单理解为「数列的前n项的和」，是一种重要的预处理方式，能大大降低查询的时间复杂度。[1](https://oi-wiki.org/basic/prefix-sum/#fn:note1)

C++ 标准库中实现了前缀和函数 `std::partial_sum`，定义于头文件 `<numeric>` 中。  
用于求从l，r区间的和.  
**代码**

```cpp
ll a[N];
ll prefix[N];
ll cont = 0;
void solve()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)//i从1到n方便求前缀和
    {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];//求前缀和的公式
    }
    while (m--)
    {
        int l, r;
        cin >> l >> r;
        cout << prefix[r] - prefix[l - 1] << '\n';//求l，r区间的和
    }
}
```

#### 二维前缀和
[796. 子矩阵的和 - AcWing题库](https://www.acwing.com/problem/content/798/)  
![[Pasted image 20240726210537.png]]

**代码**

```cpp
    int n, m, q;
    cin >> n >> m >> q;
    for (int i = 1;i <= n;i++)
    {
        for (int j = 1; j <= m;j++)
        {
            cin >> a[i][j];
        }
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            prefix[i][j] = a[i][j] + prefix[i - 1][j] + prefix[i][j - 1] - prefix[i - 1][j - 1];//求二维前缀和公式
        }
    }
    while(q--)
    {
        int x1,x2,y1,y2;
        cin >> x1 >> y1 >>x2 >> y2;
        cout << prefix[x2][y2] - prefix[x1 - 1][y2] - prefix[x2][y1 - 1] + prefix[x1 - 1][y1 - 1]<<'\n';//求【x1，y1】 到【x2】【y2】区间的和
    }
```

#### 一维差分
[797. 差分 - AcWing题库](https://www.acwing.com/problem/content/799/)  
**思想**  
差分是一种和前缀和相对的策略，可以当做是求和的逆运算。  
diff[i]=a[i]-a[i-1];  
本质就是找到一个数组diff对其求前缀和后是a数组

**代码**

```cpp
void insert(int l, int r,int h)//精妙之处用一个函数就可以对差分数组进行修改
{
    diff[l]+=h;
    diff[r + 1] -= h;
}
void solve()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <=n;i++)
    {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++)
    {
        insert(i, i, a[i]);//【i，i】这个区间修改为a【i】
    }
    while(m--)
    {
        int l,r,c;
        cin >> l >> r >> c;
        insert(l, r, c); //将l，r这个区间加上c
    }
    for (int i = 1; i <= n;i++)
    {
        a[i] = a[i - 1] + diff[i];//对diff数组求前缀和重新计算询问后的a数组
    }
    for (int i = 1; i <= n;i++)
    {
        cout << a[i]<< " ";
    }
}
```

#### 二维差分
**思想**  
![[Pasted image 20240726212941.png]]



```cpp
ll a[N][N];
ll diff[N][N];
ll cont = 0;
void insert(int x1, int y1, int x2, int y2, int c)
{
    diff[x1][y1] += c;
    diff[x1][y2 + 1] -= c;
    diff[x2 + 1][y1] -= c;
    diff[x2 + 1][y2 + 1] += c;
}
void solve()
{
    int n, m, q;
    cin >> n >> m >> q;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cin >> a[i][j];
            insert(i , j, i, j, a[i][j]);
        }
    }
    while (q--)
    {
        int x1, y1, x2, y2, c;
        cin >> x1 >> y1 >> x2 >> y2 >> c;
        insert(x1, y1, x2, y2, c);
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            a[i][j] = a[i][j - 1] + a[i - 1][j] - a[i - 1][j - 1] + diff[i][j];
        }
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cout << a[i][j] << ' ';
        }
        cout << '\n';
    }
}
```

## 双指针
#### 数组元素的目标和
[800. 数组元素的目标和 - AcWing题库](https://www.acwing.com/problem/content/802/)

(1)二分

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <cstring>
#include <cmath>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
ll a[N], b[N];
void solve()
{
    int n, m, x;
    cin >> n >> m >> x;
    for (int i = 0; i < n;i++)
    {
        cin >> a[i];
    }
    for (int i = 0; i < m;i++)
    {
        cin >> b[i];
    }
    for (int i = 0; i < n;i++)
    {
        int l = 0, r = m, mid;
        while(l+1!=r)
        {
            mid = (l + r) / 2;
            if(b[mid]>x-a[i])
            {
                r = mid;
            }
            else
            {
                l = mid;
            }
        }
        if(b[l]+a[i]==x)
        {
            cout << i << ' ' << l;
            return;
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

（2）

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <cstring>
#include <cmath>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
ll a[N], b[N];
void solve()
{
    int n, m, x;
    cin >> n >> m >> x;
    for (int i = 0; i < n;i++)
    {
        cin >> a[i];
    }
    for (int i = 0; i < m;i++)
    {
        cin >> b[i];
    }
    for (int i = 0,j=m-1; i < n;i++)
    {
        while(j>=0 && a[i]+b[j]>x )
            j--;
    if(j>=0 && b[j]+a[i]==x)
    {
        cout << i << " " << j;
        return;
    }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```



## 位运算
### 基本运算符
![[Pasted image 20240810184633.png]]

#### 异或^相同为0不同为1（不进位加法）
1 ⊕ 1 = 0  

0 ⊕ 0 = 0  

1 ⊕ 0 = 1  

0 ⊕ 1 = 1



#### 性质
##### a+b
<font style="background-color:#f3bb2f;">a+b=2 * (a&b)+(a^b)</font>

##### 求该数是否是二的幂
<font style="background-color:#f3bb2f;">x&(x-1) = = 0 则成立</font>

##### 求一个数二进制的个数
```cpp
int x,cont=0;
    x = 8;
    while(x)

    {
        x &= x - 1;
        cont++;
    }
    cout << cont;
```



#### bitset:可以输出一个数的二进制
例如 bitset<8>(7)高位补零  
可以输出长度为7的x二进制（高位补0）

#### lowbit![[Pasted image 20240921182528.png]]
**返回该数二进制最后一位1**

```cpp
int lowbit(int x)

{
    return x & -x;
}
```

可以求一个数的二进制有几个

## 数据结构
### 树状数组
支持单点修改，区间查询，找到第k个数



### 线段树
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
const int N = 1e5 + 10;
const ll MOD = 1e9 + 7; // 根据需要修改模数

struct SegmentTree {
    ll sum[N << 2];    // 区间和
    ll mul[N << 2];    // 区间乘积
    ll add[N << 2];    // 加法懒标记
    ll set[N << 2];    // 赋值懒标记
    bool is_set[N << 2]; // 是否有赋值标记

    // 初始化建树
    void build(int l, int r, int rt) {
        add[rt] = 0;
        is_set[rt] = false;
        if (l == r) {
            sum[rt] = a[l];
            mul[rt] = a[l];
            return;
        }
        int mid = (l + r) >> 1;
        build(l, mid, rt << 1);
        build(mid + 1, r, rt << 1 | 1);
        pushup(rt);
    }

    // 上推更新
    void pushup(int rt) {
        sum[rt] = sum[rt << 1] + sum[rt << 1 | 1];
        mul[rt] = (mul[rt << 1] * mul[rt << 1 | 1]) % MOD;
    }

    // 下推懒标记
    void pushdown(int rt, int ln, int rn) {
        if (is_set[rt]) {
            // 优先处理赋值标记
            int lson = rt << 1, rson = rt << 1 | 1;
            
            sum[lson] = set[rt] * ln;
            mul[lson] = pow(set[rt], ln) % MOD;
            set[lson] = set[rt];
            is_set[lson] = true;
            add[lson] = 0; // 赋值操作会清空加法标记
            
            sum[rson] = set[rt] * rn;
            mul[rson] = pow(set[rt], rn) % MOD;
            set[rson] = set[rt];
            is_set[rson] = true;
            add[rson] = 0;
            
            is_set[rt] = false;
        }
        
        if (add[rt]) {
            int lson = rt << 1, rson = rt << 1 | 1;
            
            // 更新左子树
            mul[lson] = (mul[lson] * pow(1 + add[rt], ln)) % MOD;
            sum[lson] += add[rt] * ln;
            add[lson] += add[rt];
            
            // 更新右子树
            mul[rson] = (mul[rson] * pow(1 + add[rt], rn)) % MOD;
            sum[rson] += add[rt] * rn;
            add[rson] += add[rt];
            
            add[rt] = 0;
        }
    }

    // 区间加法
    void update_add(int L, int R, ll val, int l, int r, int rt) {
        if (L <= l && r <= R) {
            sum[rt] += val * (r - l + 1);
            mul[rt] = (mul[rt] * pow(1 + val, r - l + 1)) % MOD;
            add[rt] += val;
            return;
        }
        int mid = (l + r) >> 1;
        pushdown(rt, mid - l + 1, r - mid);
        if (L <= mid) update_add(L, R, val, l, mid, rt << 1);
        if (R > mid) update_add(L, R, val, mid + 1, r, rt << 1 | 1);
        pushup(rt);
    }

    // 区间赋值
    void update_set(int L, int R, ll val, int l, int r, int rt) {
        if (L <= l && r <= R) {
            sum[rt] = val * (r - l + 1);
            mul[rt] = pow(val, r - l + 1) % MOD;
            set[rt] = val;
            is_set[rt] = true;
            add[rt] = 0; // 赋值操作会清空加法标记
            return;
        }
        int mid = (l + r) >> 1;
        pushdown(rt, mid - l + 1, r - mid);
        if (L <= mid) update_set(L, R, val, l, mid, rt << 1);
        if (R > mid) update_set(L, R, val, mid + 1, r, rt << 1 | 1);
        pushup(rt);
    }

    // 区间查询和
    ll query_sum(int L, int R, int l, int r, int rt) {
        if (L <= l && r <= R) return sum[rt];
        int mid = (l + r) >> 1;
        pushdown(rt, mid - l + 1, r - mid);
        ll ans = 0;
        if (L <= mid) ans += query_sum(L, R, l, mid, rt << 1);
        if (R > mid) ans += query_sum(L, R, mid + 1, r, rt << 1 | 1);
        return ans;
    }

    // 区间查询乘积
    ll query_mul(int L, int R, int l, int r, int rt) {
        if (L <= l && r <= R) return mul[rt];
        int mid = (l + r) >> 1;
        pushdown(rt, mid - l + 1, r - mid);
        ll ans = 1;
        if (L <= mid) ans = (ans * query_mul(L, R, l, mid, rt << 1)) % MOD;
        if (R > mid) ans = (ans * query_mul(L, R, mid + 1, r, rt << 1 | 1)) % MOD;
        return ans;
    }
};

SegmentTree st;
ll a[N];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; ++i) cin >> a[i];
    
    st.build(1, n, 1);
    
    while (m--) {
        int op, l, r;
        ll val;
        cin >> op;
        if (op == 1) { // 区间加
            cin >> l >> r >> val;
            st.update_add(l, r, val, 1, n, 1);
        } else if (op == 2) { // 区间赋值
            cin >> l >> r >> val;
            st.update_set(l, r, val, 1, n, 1);
        } else if (op == 3) { // 查询区间和
            cin >> l >> r;
            cout << st.query_sum(l, r, 1, n, 1) << "\n";
        } else if (op == 4) { // 查询区间乘积
            cin >> l >> r;
            cout << st.query_mul(l, r, 1, n, 1) << "\n";
        }
    }
    
    return 0;
}
```

### 离散化
**定义：**  
离散化是在**不改变**数据**相对大小**的条件下，对数据进行**相应的缩小**。  
当数据只与它们之间的相对大小有关，而与具体是多少无关时，可以进行离散化。  
从上面的例子我们也可以看出，离散化就是使离散的点(差距很大的数值)转换成更加紧密的点。(也即数组下标)这样就可以极大的缩小空间复杂度和时间复杂度，且不改变原来的属性。即我原来比你大，离散化后仍然比你大，只不过差距变小了而已。  
[802. 区间和 - AcWing题库](https://www.acwing.com/problem/content/804/)  
**代码**

```cpp
const int N = 3e5 + 10;//题目最大范围是1e5如果存下标最大就是n+2m
ll a[N],prefix[N];//
vector<pair<int, int>> cg, query;//cg存改变的值，query存询问的区间
vector<int> alls;//alls存所有区间
int find(int x)//find的本质就是找该数在alls数组里面排序后是第几个数

{

    int l = 0, r = alls.size(), mid;

    while(l+1!=r)

    {

        mid = (l + r) / 2;

        if(alls[mid]>x)

        {
            r = mid;

        }

        else

        {

            l = mid;

        }

    }

    return r;

}

void solve()

{

    int n, m;

    cin >> n >> m;

    for (int i = 0; i < n;i++)

    {

        int tmp1, tmp2;

        cin >> tmp1 >> tmp2;

        cg.push_back({tmp1, tmp2});

        alls.push_back(tmp1);

    }

    for (int i = 0; i < m;i++)

    {

        int tmp1, tmp2;

        cin >> tmp1 >> tmp2;

        query.push_back({tmp1, tmp2});

        alls.push_back(tmp1);

        alls.push_back(tmp2);

    }

    sort(alls.begin(), alls.end());//先排序后去重

    alls.erase(unique(alls.begin(), alls.end()), alls.end());

    for (int i = 0; i < n;i++)

    {

        int l = find(cg[i].first);//遍历改变的数组，将要改变的下标离散化

        a[l] += cg[i].second;

    }

    for (int i = 1; i <= alls.size();i++)

    {

        prefix[i] = prefix[i - 1] + a[i];//对a[i]求前缀和

    }

    for (int i = 0; i < m; i++)

    {

        int l = find(query[i].first);

        int r = find(query[i].second);

        cout << prefix[r] - prefix[l - 1] << '\n';

    }

}
```



## 区间合并
[803. 区间合并 - AcWing题库](https://www.acwing.com/problem/content/submission/805/)

```cpp
void solve()
{
    int n;
    cin >> n;
    for (int i = 0; i < n;i++)
    {
        int l, r;
        cin >> l >> r;
        segs.push_back({l, r});
    }
    sort(segs.begin(), segs.end());
    int st = -2e9, ed = -2e9;//设为2e9确保第一个区间可以赋值上去
    vector<pair<int, int>> ans;
    for (int i = 0; i < n; i++)
    {
        if(segs[i].first>ed)
        {
            if(ed!=-2e9)ans.push_back({st, ed});
            ed = segs[i].second;
            st = segs[i].first;
        }
        else
        {
            ed = max(ed, segs[i].second);//此处注意要与ed比较大小不能直接赋值
        }
    }
    if(ed!=-2e9)
        ans.push_back({st, ed});

    cout << ans.size();
}
```



## STL
### 链表
#### 单链表
```plain
const int N = 1e5 + 10;

using ll = long long;

ll e[N], ne[N], idx=1;

void init()

{

    ne[0] = -1;

}

void insert(int k,int x)

{

    e[idx] = x;

    ne[idx] = ne[k];

    ne[k] = idx;

    idx++;

}

void del(int k)

{

    ne[k] = ne[ne[k]];

}
void solve()

{

    int n;

    cin >> n;

    init();

    for (int i = 0; i < n;i++)

    {

        string h;

        cin >> h;

        if(h == "I")

        {

            int k,x;

            cin >>k>>x;

            insert(k,x);

        }

        else if (h == "D")

        {

            int k;

            cin >> k;

            del(k);

        }

        else if(h=="H")

        {

            int x;

            cin >> x;

            insert(0, x);

        }

    }

    for (int i = ne[0]; i != -1;i=ne[i])

    {

        cout << e[i] << ' ';

    }

}
```

#### 双链表
[827. 双链表 - AcWing题库](https://www.acwing.com/problem/content/829/)

<font style="background-color:#f3bb2f;">注意</font>  
注意双链表的初始化以及最后的循环

```cpp
ll e[N], re[N], le[N], idx = 1, head = 0, tail = 1e5;

void init()

{

    re[head] = tail;//

    le[tail] = head;

}
 for (int i = re[head]; i !=tail;i=re[i])

    {

        cout << e[i] << ' ';

    }

```



```cpp
#include <iostream>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <string>

#include <bitset>

using namespace std;

const int N = 1e5 + 10;

using ll = long long;

ll e[N], re[N], le[N], idx = 1, head = 0, tail = 1e5;

void init()

{

    re[head] = tail;//

    le[tail] = head;

}

void insert(int k,int x)

{

    e[idx] = x;

    re[idx] = re[k];

    le[idx] = k;

    re[k] = idx;

    le[re[idx]] = idx;

    idx++;

}

void del(int k)

{

    re[le[k]] = re[k];

    le[re[k]] = le[k];

}

void solve()

{

    int n;

    cin >> n;

    init();

    int k, x;

    for (int i = 0; i < n;i++)

    {

        string s;

        cin >> s;

        if(s=="R")

        {

            cin >> x;

            insert(le[tail], x);

        }

        else if(s=="L")

        {

            cin >> x;

            insert(head, x);

        }

        else if(s=="D")

        {

            cin >> k;

            del(k);

        }

        else if(s=="IL")

        {

            cin >> k >> x;

            insert(le[k], x);

        }

        else if(s=="IR")

        {

            cin >> k >> x;

            insert(k, x);

        }

    }

    for (int i = re[head]; i !=tail;i=re[i])

    {

        cout << e[i] << ' ';

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



### 栈
[3302. 表达式求值 - AcWing题库](https://www.acwing.com/problem/content/3305/)

#### 表达式求值
```cpp
#include <iostream>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <string>

#include <bitset>

using namespace std;

const int N = 1e5 + 10;

using ll = long long;

char c[N];

ll num[N];

map<char, int> p;

int ct = 0, nt = 0;

void cau()

{
/*假设式子是4/3
栈顶为3然后是4
应该是后面的除前面的所以是b/a*/

    int a = num[nt--];//注意加减乘除的顺序

    int b = num[nt--];

    char h = c[ct--];

    int ans = 0;

    if(h=='*')

        ans = a * b;

    else if(h=='/')

        ans = b/a;

    else if(h=='+')

        ans = a + b;

    else if(h=='-')

        ans = b-a;

  

    num[++nt] = ans;

}

void solve()

{

    p['-'] = 1;

    p['+'] = 1;

    p['*'] = 2;

    p['/'] = 2;//用map映射算符的优先级顺序

    string s;

    cin >> s;

    string s1;

    for (int i = 0; s[i];i++)

    {

       if(isdigit(s[i]))

       {

           s1 += s[i];

       }

       else if(s[i]=='(')

       {

        if(s1.size()!=0)

        {

            int tem = atoi(s1.c_str());

            num[++nt] = tem;

            s1.clear();

        }

           c[++ct] = s[i];

       }

       else if(s[i]==')')

       {

           if (s1.size() != 0)

           {

               int tem = atoi(s1.c_str());

               num[++nt] = tem;

               s1.clear();

           }

        while(c[ct]!='(')

        {

            cau();

        }

        ct--;

       }

       else

       {

           if (s1.size() != 0)

           {

               int tem = atoi(s1.c_str());

               num[++nt] = tem;

               s1.clear();

           }

           while (p[c[ct]] >= p[s[i]] && ct!=0)

           {

               cau();

           }

           c[++ct] = s[i];

       }

    }

    if (s1.size() != 0)//最后s1.size()可能不为0

    {

        num[++nt] = atoi(s1.c_str());

        s1.clear();

    }

   while(ct!=0)//应该是清空运算符栈顶

       cau();

   cout << num[nt];

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

#### 单调栈
[830. 单调栈 - AcWing题库](https://www.acwing.com/problem/content/832/)

```cpp
#include <iostream>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <string>

#include <bitset>

using namespace std;

const int N = 1e5 + 10;

using ll = long long;

ll stk[N], tt = 0,a[N];

void solve()

{

    int n;

    cin >> n;

    for (int i = 0; i < n;i++)

    {

        cin >> a[i];

    }

    for (int i = 0; i < n;i++)

    {

        while(stk[tt]>=a[i] && tt!=0)//一定要大于等于

        {

            tt--;

        }

        if(tt==0)

        {

            cout << -1 << ' ';

        }else

        {

            cout << stk[tt] << ' ';

        }

        stk[++tt] = a[i];

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

### 队列
[154. 滑动窗口 - AcWing题库](https://www.acwing.com/problem/content/156/)

```cpp
ll dq[N], head=0,tail=-1,a[N];

void solve()

{

    int n,k;

    cin >> n>>k;

    for (int i = 0; i < n;i++)

    {

        cin >> a[i];

    }

    for (int i = 0; i < n;i++)

    {

        while(a[dq[tail]]>=a[i] && head<=tail)//先判断队尾出队

        {

            tail--;

        }

        dq[++tail] = i;//队尾进队

        if(dq[head]<i-k+1)//在判断队头进队

        {

            head++;

        }

        if(i>=k-1)

        {

            cout << a[dq[head]]<<' ';

        }

    }

    cout << '\n';

    head = 0, tail = -1;

    for (int i = 0; i < n; i++)

    {

        while (a[dq[tail]] <=a[i] && head <= tail)

        {

            tail--;

        }

        dq[++tail] = i;

        if (dq[head] < i - k + 1)

        {

            head++;

        }

        if (i >= k - 1)

        {

            cout << a[dq[head]] << ' ';

        }

    }

}
```



## 字符串
### KMP
**思想**  
就是通过next数组求要找的这个字符串的最长公共前后缀  
然后依次匹配，若匹配则j++,若不匹配则用j=ne[j]回退;若找到则输出即可

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string>
#include <bitset>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
ll ne[N];
void solve()
{
    int n, m;
    string s1, s2;
    cin >> n >> s1 >> m >> s2;
    ne[0] = -1;
    for (int i = 1, j = -1; i < n;i++)//第一次就是预处理求最大前缀和
    {
        while(s1[i]!=s1[j+1] && j!=-1)
        {
            j = ne[j];
        }
        if(s1[i]==s1[j+1])
        {
            j++;
        }
        ne[i] = j;
    }
    for (int i = 0,j=-1; i < m;i++)
    {
        while(s1[j+1]!=s2[i] && j!=-1)
        {
            j = ne[j];
        }
        if(s2[i]==s1[j+1])
        {
            j++;
        }
        if(j==n-1)
        {
            cout << i - j<<' ';
            j = ne[j];
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### Trie
![[Pasted image 20240812095005.png]]

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string>
#include <bitset>
using namespace std;
const int N = 2e5 + 10;
using ll = long long;
ll t[N][26], idx, p,cont[N];
void insert(string s)
{
    p = 0;
    for (int i = 0; s[i];i++)
    {
        int u = s[i] - 'a';
        if(!t[p][u])
        {
            t[p][u] = ++idx;
        }
        p = t[p][u];
    }
    cont[p]++;
}
void query(string s)
{
    p = 0;
    for (int i = 0; s[i];i++)
    {
        int u = s[i] - 'a';
        if(!t[p][u])
        {
            cout << 0<<'\n';
            return;
        }
        p = t[p][u];
    }
    cout << cont[p] << '\n';
}
void solve()
{
    int n;
    cin >> n;
    for (int i = 0; i < n;i++)
    {
        string s;
        cin >> s;
        if(s=="I")
        {
            string s1;
            cin >> s1;
            insert(s1);
        }
        else
        {
            string s1;
            cin >> s1;
            query(s1);
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

#### 最大异或对
[143. 最大异或对 - AcWing题库](https://www.acwing.com/problem/content/145/)  
**思路**  
异或为相同为0，不同为1，所以如果要找最大的异或对即例如一个的二进制为（11011)他的最大异或另一个一定是（00100）先用trie树存然后查找过程中如果没有我期望的数（同一位次上相反的值）就取另一个数，最后输出结果即可

<font style="background-color:#f3bb2f;">为什么son数组要开成M：M 是 Trie 树总结点数上限。一共 N 个数，每个数 31 位，从根开始往下存，要 31 个结点，M = 31 * N</font>

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string>
#include <bitset>
using namespace std;
const int N = 1e5 + 10;
const int M = 1e7;
using ll = long long;
map<ll, ll> cont;
ll son[M][2], idx, p, a[N];
void insert(int x)
{
    p = 0;
    for (int i = 30; i >= 0; i--)
    {
        int k = x >> i & 1;
        if (!son[p][k])
        {
            son[p][k] = ++idx;
        }
        p = son[p][k];
    }
    cont[p] = x;
}
int query(int x)
{
    p = 0;
    int res = 0;
    for (int i = 30; i >= 0; i--)
    {
        int k = x >> i & 1;
        if (son[p][!k])
        {
            p = son[p][!k];
        }
        else
        {
            p = son[p][k];
        }
    }
    return cont[p] ^ x;
}
void solve()
{
    int n, ans = 0;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
        insert(a[i]);
    }
    for (int i = 0; i < n; i++)
    {
        ans = max(ans, query(a[i]));
    }
    cout << ans;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```



## 并查集
### 定义：
并查集是一种树型的数据结构，用于处理一些不相交集合的合并及查询问题（即所谓的并、查）。比如说，我们可以用并查集来判断一个森林中有几棵树、某个节点是否属于某棵树等。

主要构成：  
并查集主要由一个整型数组pre[ ]和两个函数find( )、join( )构成。  
数组 pre[ ] 记录了每个点的前驱节点是谁，函数 find(x) 用于查找指定节点 x 属于哪个集合，函数 join(x,y) 用于合并两个节点 x 和 y 。

作用：  
并查集的主要作用是求连通分支数（如果一个图中所有点都存在可达关系（直接或间接相连），则此图的连通分支数为1；如果此图有两大子图各自全部可达，则此图的连通分支数为2



[836. 合并集合 - AcWing题库](https://www.acwing.com/problem/content/838/)

### 主要代码
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string>
#include <bitset>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
ll p[N];
int find(int x)//返回其父亲
// 路径压缩，递归的过程中将每个节点都连上最初的那个父亲上
{
    if (p[x] != x)//如果他的父亲不是他自己
    {
        p[x] = find(p[x]);
    }

    return p[x];
}
void solve()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <=n; i++)
    {
        p[i] = i;
    }
    string s;
    for (int i = 0; i < m; i++)
    {
        cin >> s;
        if (s == "M")
        {
            int a, b;
            cin >> a >> b;
            p[find(a)] = find(b);
        }
        else
        {
            int a, b;
            cin >> a >> b;
            if (find(a) == find(b))
            {
                cout << "Yes" << '\n';
            }
            else
            {
                cout << "No" << '\n';
            }
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 带权的并查集
[240. 食物链 - AcWing题库](https://www.acwing.com/problem/content/description/242/)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string>
#include <bitset>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
ll p[N], d[N];
int find(int x)
{
    if (p[x] != x)
    {
        int u = find(p[x]);//先一直递归，知道找到第一个点（维护整个树顶的权值）
        d[x] += d[p[x]];//归的过程求权值
        p[x] = u;
    }
    return p[x];
}
void solve()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        p[i] = i;
    }
    int a, b, s, res = 0;
    for (int i = 0; i < m; i++)
    {
        cin >> s >> a >> b;
        if (a > n || b > n)
        {
            res++;
        }
        else//如果距离根顶的权值是相同的，那就是同类，否则就是吃与被吃的关系
        {
            int pa = find(a), pb = find(b);
            if (s == 1)
            {
                if (pa == pb)
                {
                    if ((d[a] - d[b]) % 3 != 0)
                    {
                        res++;
                    }
                }
                else
                {
                    p[pa] = pb;
                    d[pa] = d[b] - d[a];
                }
            }
            else if (s == 2)
            {
                if (pa == pb)
                {
                    if (((d[a] - d[b])-2) % 3 != 0)
                    {
                        res++;
                    }
                }
                else
                {
                    p[pa] = pb;
                    d[pa] = d[b] - d[a]+2 ;
                }
            }
        }
    }
    cout << res;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 模拟堆
[839. 模拟堆 - AcWing题库](https://www.acwing.com/problem/content/841/)



**注意辨析hp，ph数组的含义**  
**以及交换时先存下标，不然交换之后下标对应的值会变**  
heap_swap(ph[k],asize)之后，h[ph[k]],ph[ph[k]],hp[ph[k]]都变化了！  
注意交换操作并不会改变数组下标，也就是size仍然指向数组尾部，ph[k]仍然指向第k个插入位置  
这时down和up都需要继续heap_swap，也就是说会继续用到h[ph[k]],ph[ph[k]],hp[ph[k]]，这都变成h[ph[size]]啦就不能这么用啦！！  
所以需要单独储存一下ph[k]，down和up的时候继续用它就好啦！

```cpp
else if(!strcmp(action,"D")){
    int k;
    cin >> k;
    k = ph[k];   //先保存一下ph[k]
    heap_swap(k,asize);
    asize --;
    down(k);
    up(k);
}
```



```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string.h>
#include <bitset>
#include <sstream>
using namespace std;
const int N = 1e5 + 10;
using ll = long long;
using ull = unsigned long long;
ll h[N], hp[N], ph[N], sz, m; // hp通过堆的下标找到插入第几个数，ph通过插入第几个数找到堆的下标
void head_swap(int a, int b)
{
    swap(h[a], h[b]);
    swap(hp[a], hp[b]);
    swap(ph[hp[a]], ph[hp[b]]);
}
void up(int k) // 传的是堆的下标
{
    int u = k;
    if (u / 2 >0 && h[u / 2] > h[k])
    {
        k = u / 2;
    }
    if (u != k)
    {
        head_swap(k, u);
        up(k);
    }
}
void down(int k)
{
    int u = k;
    if (u * 2 <= sz && h[u * 2] < h[k])
    {
        k = u * 2;
    }
    if (u * 2 + 1 <= sz && h[u * 2 + 1] < h[k])
    {
        k = u * 2 + 1;
    }
    if (u != k)
    {
        head_swap(k,u);
        down(k);
    }
}
void solve()
{
    int n;
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        string s;
        int a, b;
        cin >> s;
        if (s == "I")
        {
            cin >> a;
            m++;
            sz++;
            hp[sz] = m;
            ph[m] = sz;
            h[sz] = a;
            up(sz);
        }
        else if (s == "PM")
        {
            cout << h[1] << '\n';
        }
        else if (s == "DM")
        {
            head_swap(1, sz);
            sz--;
            down(1);
        }
        else if (s == "D")
        {
            int k;
            cin >> k;
            k = ph[k];//注意保存数组下标
            head_swap(k,sz);
            sz--;
            up(k);
            down(k);
        }
        else if(s=="C")
        {
            int k, x;
            cin >> k >> x;
            k = ph[k];
            h[k] = x;
            up(k);
            down(k);
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 哈希表
### 数字hash
#### 拉链法
```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <string.h>

#include <bitset>

#include <sstream>

using namespace std;

const int N = 1e5 + 10;

using ll = long long;

using ull = unsigned long long;

ll h[N], e[N], ne[N],idx;

int MOD = 1e5 +7;

void insert(int x)

{

    int k = (x % MOD + MOD) % MOD;

    e[++idx] = x;

    ne[idx] = h[k];

    h[k] = idx;

  

}

bool query(int x)

{

    int k = (x % MOD + MOD) % MOD;

    for (int i = h[k]; i != 0;i=ne[i])

    {

        if(e[i]==x)

        {

            return true;

        }

    }

    return false;

}

void solve()

{

    int n;

    cin >> n;

    while(n--)

    {

        string s;

        cin >> s;

        if(s=="I")

        {

            int x;

            cin >> x;

            insert(x);

        }

        else

        {

            int x;

            cin >> x;

            if(query(x))

            {

                cout << "Yes" << '\n';

            }

            else

            {

                cout << "No" << '\n';

            }

        }

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

#### 开放寻址法
```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <string.h>
#include <bitset>
#include <sstream>
using namespace std;
const int N = 2e5 + 3;
using ll = long long;
using ull = unsigned long long;
int null = 0x3f3f3f3f;
int h[N];
int MOD = 1e5 +7;
int find(int x)
{
    int t = (x % N + N) % N;
    while (h[t] != null && h[t]!=x)
    {
        t++;
        if(t==N)
        {
            t = 0;
        }
    }
    return t;
}

void solve()
{
    memset(h, 0x3f, sizeof h);
    int n;
    cin >> n;
    while(n--)
    {
        string s;
        cin >> s;
        if(s=="I")
        {
            int x;
            cin >> x;
            h[find(x)] = x;
        }
        else
        {
            int x;
            cin >> x;
            if(h[find(x)]==null)
            {
                cout<<"No"<<'\n';
            }
            else 
            {
                cout << "Yes" << '\n';
            }
        }
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 字符串hash
本质就是对字符串求前缀和，他的p进制  
1.不能映射成 0  
不然 aa 0；aaaaa 0;  
2.get函数的理解

```cpp
如果一个字符串是12345
求从第2到第3个；23
123*h[r]*-100h*[l-1]左移l到r区间的位置*
```



```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

using namespace std;

const int N = 1e6 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

ll null = 0x3f3f3f3f;

ull p[N], h[N];

string s;

ull get(int l,int r)

{

    return h[r] - h[l - 1] * p[r - l + 1];//12345 45要12345-12300

}

void solve()

{

    int n, m;

    cin >> n >> m;

    cin >> s;

    p[0] = 1;

    for (int i = 1; i <= n;i++)

    {

        h[i] = h[i - 1] * P + s[i-1];//s下标从0开始

        p[i] = p[i - 1] * P;//P数组代表p的几次方;

    }

    for (int i = 0; i < m;i++)

    {

        int l1, r1, l2, r2;

        cin >> l1 >> r1 >> l2 >> r2;

        if(get(l1,r1)==get(l2,r2))

        {

            cout << "Yes" << '\n';

        }

        else

        {

            cout << "No" << '\n';

        }

    }

}

  

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

## 图论
![[1833_db6dffa81d-37ff39642fd8f74476ddcd99944d1b4.png]]

![[Pasted image 20240903143711.png]]

### DFS
<font style="background-color:#f3bb2f;">求连通块</font>  
数据结构 ： stack  
空间o（n）  
不具最短性  
**思想**  就是一直深度遍历，知道遍历到不能遍历为止，然后再回溯

[842. 排列数字 - AcWing题库](https://www.acwing.com/problem/content/844/)

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

using namespace std;

const int N = 1e6 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

ll  path[N];

bool st[N];

int n;

void dfs(int u)

{

    if(u==n)

    {

        for (int i = 0; i < n;i++)

        {

            cout << path[i] << ' ';

        }

        cout << '\n';

        return;

    }

    for (int i = 1; i <= n;i++)//u表示排到第几个数了 然后依次遍历n

    {

        if(!st[i])//如果st[i]没被加入path中，则加入递归

        {

            path[u] = i;

            st[i] = true;//上半部分是一直递归下半部分的回溯的时候要还原现场

            dfs(u + 1);

            st[i] = false;

        }

    }

}

void solve()

{

    cin >> n;

    dfs(0);

}

  

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

[843. n-皇后问题 - AcWing题库](https://www.acwing.com/problem/content/845/)

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
using namespace std;
const int N = 1e4 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
char path[N][N];
bool c[N], r[N], dg[N], udg[N];/主要是正对角线和反对角线的表示，然后对角线的数量是N*2/；
int n;
void dfs(int u)
{
    if (u == n)//当u到n是打印所有路径，然后回溯，打印完之后一定要回溯
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                cout << path[i][j];
            }
            cout << '\n';
        }
        cout << '\n';
        return;
    }

    for (int i = 0; i < n; i++)
    {
        if (!r[i] && !dg[u + i] && !udg[u - i+n])
        {
            path[u][i] = 'Q';
        
            r[i] = true;
            dg[u + i] = true;
            udg[u - i+n] = true;
            dfs(u + 1);//上半部分是递归，下半部分是回溯，正对角线是u+i，反对角线是u-i因为有可能是负数，所以改为u-i+n；
            r[i] = false;
            dg[u + i] = false;
            udg[u - i+n] = false;
            path[u][i] = '.';
        }
    }
}
void solve()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            path[i][j] = '.';
        }
    }
    dfs(0);
}

int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### BFS
<font style="background-color:#f3bb2f;">应用：求最短环</font>  
数据结构 ：queue  
空间o（2^n）  
具有最短性  
伪代码

```plain
bfs(s)
{ q = new queue()
q.push(s),
visited[s] = true 
while (!q.empty()) 
{ u = q.pop()
for each edge(u, v)
{ if (!visited[v])
{ q.push(v) visited[v] = true }
}
} 
}
```

**思路** 就是先将第一个点入队，设定一个初始状态，然后进入循环，判断队列是否为空，然后将第一个点出队，然后遍历该对所有符合条件的点入队，然后设定状态，最后循环结束即可



[844. 走迷宫 - AcWing题库](https://www.acwing.com/problem/content/846/)

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
using namespace std;
const int N = 1e3 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
int   path[N][N];
ll   d[N][N];
int n,m;
queue<pair<int, int>> dq;
void bfs()
{
    memset(d, -1, sizeof d);
    dq.push({1, 1});
    d[1][1] = 0;
    int x[4] = {-1, 0, 1, 0};
    int y[4] = {0, -1, 0, 1};
    while(dq.size())
    {
        auto it = dq.front();
        dq.pop();
        for (int i = 0; i < 4;i++)
        {
            int k = it.first + x[i];
            int h = it.second + y[i];
            if (path[k][h] == 0 && (k>0 && k<=n) &&(h>0 && h<=m) && d[k][h]==-1)
            {
                dq.push({k, h});
                d[k][h] = d[it.first][it.second] + 1;
            }
        }
    }
    
        cout << d[n][m];
}
void solve()
{
    cin >> n >> m;
    for (int i = 1; i <=n;i++)
    {
        for (int j = 1; j <=m;j++)
        {
            cin >> path[i][j];
        }
    }
    bfs();
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```





[AcWing 845. 八数码 - AcWing](https://www.acwing.com/activity/content/problem/content/908/)

```plain
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 1e4 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;;
string s;
queue<string> dq;
unordered_map<string, int> d;
int bfs()
{
    dq.push(s);
    d[s] = 0;
    int dx[4] = {-1, 0, 1, 0};
    int dy[4] = {0, 1, 0, -1};
    string end = "12345678x";
    while(dq.size())
    {
        auto t = dq.front();
        dq.pop();
        if(t==end)//当有一种情况与最终情况一样时，则返回
            return d[t];
        int dis = d[t];
        int k = t.find('x');
        int x = k / 3, y = k % 3;
        for (int i = 0; i < 4;i++)//遍历所有可能交换的情况
        {
            int a = x + dx[i];
            int b = y + dy[i];
            if(a>=0 && a<3 && b>=0 && b<3)
            {
                swap(t[a * 3 + b], t[k]);
                if(!d.count(t))
                {
                    d[t] = dis + 1;
                    dq.push(t);
                }
                swap(t[a * 3 + b], t[k]);//最后一定要回溯
                因为是当前这个状态可达的状态符合条件就进队
            }
        }
    }
    return - 1;
}
void solve()
{
   char c;
   for (int i = 0; i < 9;i++)
   {
       cin >> c;
       s += c;
   }
   cout << bfs() << '\n';
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 图的深度优先遍历(dfs)
[AcWing 846. 树的重心 - AcWing](https://www.acwing.com/activity/content/problem/content/909/)

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>

using namespace std;

const int N=100010,M=N*2;      // 无向图,邻接表指针2*(n-1)故令M为2N
int n;                        
int h[N],e[M],ne[M],idx,ans=N; // h[]存储邻接表各个头结点,此处e[],ne[],idx同单链表
bool stl[N];    // 标记当前这个结点是否已访问,作用:使遍历不走回头路,防止子节点搜索父节点
// head, e[M],ne[M],idx; 是一条单链表
// h[N], e[M],ne[M],idx; 是N条单链表组成邻接表
void add(int a,int b)  // 头插法
{   // e记录当前点的值,ne下一点的地址,h记录指向的第一个点的地址,idx:当前用到了哪个结点(的下标)
    e[idx]=b;
    ne[idx]=h[a];            
    h[a]=idx;
    idx++;
}

int dfs(int u)      // 返回以u为根的树中所有结点个数(存在变量sum中)
{
    int res=0,sum=1;            // res存储当前连通块中结点的最大数目
    stl[u]=true;                // 走过是true没走过是false

    for(int i=h[u];i!=-1;i=ne[i]) // 从u为表头的链表开始遍历,中间递归走各个分叉,直到u的链表尾结束
    {
        int j=e[i];                 
        if(stl[j]==false)           // 只有这一点没走过才走这一点所在的分叉
        {
            int s=dfs(j);           // s为中间变量,存储u的各个子树的结点数目
            res=max(res,s);         // 通过打擂台获得删除u后u子树中最大连通块的结点个数(图中6与3-9比谁结点多)
            sum=sum+s;              // 以u为根结点的树结点数量=1+它各个子树的结点数量
        }
    }
    res=max(res,n-sum);  // 比较删除u后的u子树中最大的连通块(6,3-9中的更大者),和整个树减u子树剩下的连通块(1-2-8-5-7)
    ans=min(res,ans);           // 在所有最大的连通块结点数目找到最小值
    return sum;                 // 返回以u为根的子树结点的个数(1+u的所有子树结点个数)
}

int main()
{
    memset(h,-1,sizeof h);      // 将h[]数组初始化成-1,-1表示空结点
    scanf("%d",&n);                 
    for(int i=0;i<n-1;i++)      // n个结点插n-1次构成树
    {
        int a,b;
        scanf("%d%d",&a,&b);
        add(a,b),add(b,a);       // 无向图a→b且b→a
    }
    dfs(1);                      // 可从树中任意一个点开始遍历

    printf("%d",ans);            // 输出所有最大的连通块结点数目中的最小值

    return 0;
}
```



### 图的宽度优先遍历(bfs)
[848. 有向图的拓扑序列 - AcWing题库](https://www.acwing.com/problem/content/850/)  
**若一个由图中所有点构成的序列 AA 满足：对于图中的每条边 (x,y)(x,y)，xx 在 AA 中都出现在 yy 之前，则称 AA 是该图的一个拓扑序列。**  
没有反向边，就如果出现入度为0的点就可以加入到拓扑序列中，如果加入到拓扑序列中，则该点的所有出度的点的边都能删除，删除后更新条件继续找符合条件的点加入到拓扑序列中



```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e5 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

ll ne[N], e[N], h[N], idx;

ll d[N];

ll dq[N], tt = -1, hh = 0;

int n, m;

void add(int a, int b)

{

    idx++;

    e[idx] = b;

    ne[idx] = h[a];

    h[a] = idx;

}

bool topsort()

{

    for (int i = 1; i <= n; i++)

    {

        if (d[i] == 0)//先将所有入度为0的点加入到队列中

        {

            dq[++tt] = i;

        }

    }

    while (tt >= hh)

    {

        int u = dq[hh++];

        for (int i = h[u]; i != -1; i = ne[i])//加入到队列中的点

        {

            int j = e[i];

            d[j]--;

            if (d[j] == 0)//如果入度为0则加入到队列中

            {
                dq[++tt] = j;

            }

        }

    }

    return tt == n - 1;

}

void solve()

{

    memset(h, -1, sizeof h);

    cin >> n >> m;

    for (int i = 0; i < m; i++)

    {

        int a, b;

        cin >> a >> b;

        add(a, b);

        d[b]++;

    }

    if (topsort())

    {

        for (int i = 0; i < n; i++)//打印拓扑序列即可

        {

            cout << dq[i]<<' ';

        }

    }

    else

    {

        cout << -1;

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



### 最短路
#### Dijkstra(最短路)(缺点<font style="background-color:#f3bb2f;">存在负权边无法使用</font> ，优点最快的寻路算法)
<font style="background-color:#f3bb2f;">dijstra算法基于贪心思想，当有负权边时，局部最优不一定是全局最优</font>  
**伪代码**

```cpp
初始化距离数组, dist[1] = 0, dist[i] = inf;
for n次循环 每次循环确定一个min加入S集合中，n次之后就得出所有的最短距离
将不在S中dist_min的点->t
t->S加入最短路集合
用t更新到其他点的距离
```

##### 朴素版
[849. Dijkstra求最短路 I - AcWing题库](https://www.acwing.com/problem/content/851/)

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e3 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

int n, m;

int g[N][N];

int dist[N];

bool st[N];

int dijkstra()

{

    memset(dist, 0x3f, sizeof dist);

    dist[1] = 0;
    //千万不能先令st[1]=true；
    //其实迭代n-1次第一次是初始化所有1能到达的点dist数组的含义就是该点距离1的位置
    //然后就可以求出最短路
    //
    for (int i = 0; i < n; i++)

    {

        int t = -1;

        for (int j = 1; j <= n; j++)

        {

            if (!st[j] && (t == -1 || dist[t] > dist[j]))

            {

                t = j;

            }

        }

        for (int j = 1; j <= n; j++)

        {

            dist[j] = min(dist[j], dist[t] + g[t][j]);

        }

        st[t] = true;

    }

    if (dist[n] == 0x3f3f3f3f)

    {

        return -1;

    }

    else

    {

        return dist[n];

    }

}

void solve()

{

    memset(g, 0x3f, sizeof g);

    cin >>

        n >> m;

    for (int i = 0; i < m; i++)

    {

        int x, y, z;

        cin >> x >> y >> z;

        g[x][y] = min(g[x][y], z);

    }

    cout << dijkstra();

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

##### 堆优化版（只记堆优化版，朴素版更易理解原理）
[850. Dijkstra求最短路 II - AcWing题库](https://www.acwing.com/problem/content/852/)  
**伪代码**

```cpp
利用邻接表，优先队列
在priority_queue[HTML_REMOVED], greater[HTML_REMOVED] > heap;中将返回堆顶
利用堆顶来更新其他点，并加入堆中类似宽搜
```



```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e6 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

ll e[N], ne[N], h[N], idx,w[N];

int dist[N];//定义int类型

bool st[N];

int n, m;

void add(int x,int y,int z)

{

    idx++;

    e[idx] = y;

    ne[idx] = h[x];

    h[x] = idx;

    w[idx] = z;

}

int dijkstra()

{

    memset(dist, 0x3f, sizeof dist);

    priority_queue<pair<int, int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;

    dist[1] = 0;

    pq.push({0, 1});

   while(pq.size())

    {

        auto it = pq.top();

        pq.pop();

        int dis = it.first, u = it.second;

        if(st[u]==true)

        {

            continue;

        }

        for (int j = h[u]; j != -1; j = ne[j])

        {

            int k = e[j];

            if(dist[k]>dist[u]+w[j])

            {

                dist[k]=dist[u]+w[j];

                pq.push({dist[k], e[j]});

            }

        }

  

        st[u] = true;

    }

    if(dist[n]==0x3f3f3f3f)//dist数组是int类型的定义所以用0x3f3f3f3f比较

    {

        return -1;

    }

    else

    {

        return dist[n];

    }

}

void solve()

{

    memset(h, -1, sizeof h);

    cin>>n>>m;

    while(m--)

    {

        int x, y, z;

        cin >> x >> y >> z;

        add(x, y, z);

    }

    cout<<dijkstra();

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



#### bellman-ford(<font style="background-color:#f3bb2f;">有边数限制的最短路</font>，存在负权边)
   <font style="background-color:#f3bb2f;">最多不超过k条边只能用bellman-ford</font>

```cpp
注意连锁想象需要备份, 
struct Edge{inta,b,c} Edge[M];
初始化dist, 松弛dist[x.b] = min(dist[x.b], backup[x.a]+x.w);
松弛k次，每次访问m条边
```

[853. 有边数限制的最短路 - AcWing题库](https://www.acwing.com/problem/content/855/)

```cpp
==backup 数组确定了每次只更新一条边==
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 1e6 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
struct Edge
{
    int a, b, c;
} edge[N];
int dis[N], backup[N];
int n, m, k;
void bellman_ford()
{
    memset(dis, 0x3f, sizeof dis);
    dis[1] = 0;//初始化
    for (int i = 0; i < k; i++)
    {
        memcpy(backup, dis, sizeof dis);
        for (int j = 0; j < m; j++)
        {
            int a = edge[j].a, b = edge[j].b, c = edge[j].c;
            dis[b] = min(dis[b], backup[a] + c);
        }
    }
    if (dis[n] > 0x3f3f3f3f / 2)
    {
        cout << "impossible";
    }
    else
    {
        cout << dis[n];
    }
}
void solve()
{
    cin >> n >> m >> k;
    for (int i = 0; i < m; i++)
    {
        int a, b, c;
        cin >> a >> b >> c;
        edge[i] = {a, b, c};
    }
    bellman_ford();
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

#### SPFA
##### 最短路
[851. spfa求最短路 - AcWing题库](https://www.acwing.com/problem/content/853/)

```cpp
利用队列优化仅加入修改过的地方
for k次
for 所有边利用宽搜模型去优化bellman_ford算法
更新队列中当前点的所有出边
```

```plain
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e5 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

int n, m;

int h[N], e[N], ne[N], w[N],idx;

int dis[N], cnt[N];

bool st[N];

void add(int a,int b,int c)

{

    idx++;

    e[idx] = b;

    ne[idx] = h[a];

    w[idx] = c;

    h[a] = idx;

}

void spfa()

{

    memset(dis, 0x3f, sizeof dis);

    dis[1] = 0;

    queue<int> q;

    q.push(1);

    st[1] = true;

    while(q.size())

    {

        int u = q.front();

        q.pop();

        st[u] = false;

        for (int i = h[u]; i != -1; i = ne[i])

        {

            int o = e[i];

            if(dis[o]>dis[u]+w[i])

            {

                dis[o] = dis[u] + w[i];

                if(!st[o])//如果该点已经在队列那就不用进队

               { q.push(o);

                st[o] = true;

                }

            }

        }

    }

    if(dis[n]==0x3f3f3f3f)

    {

        cout << "impossible";

    }

    else

    {

        cout << dis[n];

    }

}

void solve()

{

    memset(h, -1, sizeof h);

    cin >> n >> m;

    for (int i = 0; i < m;i++)

    {

        int a, b, c;

        cin >> a >> b >> c;

        add(a, b, c);

    }

    spfa();

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

##### 是否存在负环
[852. spfa判断负环 - AcWing题库](https://www.acwing.com/problem/content/854/)

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 1e5 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
int n, m;
int h[N], e[N], ne[N], w[N],idx;
int dis[N], cnt[N];
bool st[N];
void add(int a,int b,int c)
{
    idx++;
    e[idx] = b;
    ne[idx] = h[a];
    w[idx] = c;
    h[a] = idx;
}
bool spfa()
{
    queue<int> q;
    for (int i = 1; i <= n; i++)//为什么要有这一步，因为不只是判断从一号点出发的负环有可能负环1号点无法到达，因此就要从所有点开始找，就把所有点加入到队列中即可
    {
        st[i] = true;
        q.push(i);
    }
    memset(dis, 0x3f, sizeof dis);
    dis[1] = 0;
    while(q.size())
    {
        int u = q.front();
        q.pop();
        st[u] = false;
        for (int i = h[u]; i != -1; i = ne[i])
        {
            int o = e[i];
            if(dis[o]>dis[u]+w[i])
            {
                dis[o] = dis[u] + w[i];
                cnt[o] = cnt[u] + 1;
                if(cnt[o]>=n)
                {
                    return true;
                }
                if(!st[o])
               { q.push(o);
                st[o] = true;
                }
            }
        }
    }
    return false;
}
void solve()
{
    memset(h, -1, sizeof h);
    cin >> n >> m;
    for (int i = 0; i < m;i++)
    {
        int a, b, c;
        cin >> a >> b >> c;
        add(a, b, c);
    }
    if(spfa())
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

#### floyd
用于处理多源最短路算法

**伪代码**

```cpp
初始化d
k, i, j 去更新d
```

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e4 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

int g[N][N];

int n, m, k;

int INF = 0x3f3f3f3f;

void floyd()

{

    for (int i = 1; i <= n; i++)// 中继节点放最外面

    {

        for (int j = 1; j <= n; j++)

        {

            for (int k = 1; k <= n; k++)

            {

                g[j][k] = min(g[j][k], g[j][i] + g[i][k]);

            }

        }

    }

}

void solve()

{

    cin >> n >> m >> k;

    for (int i = 1; i <= n; i++)

    {

        for (int j = 1; j <= n; j++)

        {

            if (i == j)

                g[i][j] = 0;

            else

                g[i][j] = INF;

        }

    }

    for (int i = 0; i < m; i++)

    {

        int a, b, c;

        cin >> a >> b >> c;

        g[a][b] = min(g[a][b], c);

    }

    floyd();

    while (k--)

    {

        int x, y;

        cin >> x >> y;

        if (g[x][y] > INF / 2)

        {

  

            cout << "impossible" << '\n';

        }

        else

        {

            cout << g[x][y] << '\n';

        }

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



### 最小生成树
#### Prim算法(稠密图)
**基本思路**  
分为两个集合，以确定生成树的集合和为确定的集合，依次选择离集合最小的一条边，依次更新dis数组的值，然后将其加入到集合中，

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 500 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

int g[N][N];

int dis[N]; // 距离已选中的集合的距离

bool st[N];

int n, m, k;

void prim()

{

    memset(dis, 0x3f, sizeof dis);

    dis[1] = 0;

    int res = 0;

    for (int i = 0; i < n; i++)

    {

        int t = -1;

        for (int j = 1; j <= n; j++)

        {

            if (!st[j] && (t == -1 || dis[t] > dis[j]))

            {

                t = j;

            }

        }

            if (dis[t] == 0x3f3f3f3f)

            {

                cout << "impossible" << '\n';

                return;

            }

            res += dis[t];

            st[t] = true;

            for (int j = 1; j <= n; j++)

            {

                dis[j] = min(dis[j], g[t][j]);

            }

    }

    cout << res;

}

void solve()

{

    memset(g, 0x3f, sizeof g);

    cin >> n >> m;

    for (int i = 0; i < m; i++)

    {

        int a, b, c;

        cin >> a >> b >> c;

        g[a][b] = g[b][a] = min(g[a][b], c);

    }

    prim();

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

#### Kruskal（稀疏图）
**思路**

```cpp
将所有边按照权值的大小进行升序排序，然后从小到大一一判断。

如果这个边与之前选择的所有边不会组成回路，就选择这条边分；反之，舍去。

直到具有 n 个顶点的连通网筛选出来 n-1 条边为止。

筛选出来的边和所有的顶点构成此连通网的最小生成树。

判断是否会产生回路的方法为：使用并查集。

在初始状态下给各个个顶点在不同的集合中。、

遍历过程的每条边，判断这两个顶点的是否在一个集合中。

如果边上的这两个顶点在一个集合中，说明两个顶点已经连通，这条边不要。如果不在一个集合中，则要这条边。
```

[858. Prim算法求最小生成树 - AcWing题库](https://www.acwing.com/problem/content/860/)

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 2e5 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

int n, m, k;

ll p[N];

struct Edge{

    int a, b, c;

  

} edge[N];

int find(int x)

{

    if(p[x]!=x)

    {

        p[x] = find(p[x]);

    }

    return p[x];

}

bool cmp(Edge x,Edge y)

{

    return x.c < y.c;

}

void solve()

{

    int cont = 0, res = 0;

    cin >> n >> m;

    for (int i = 0; i < m;i++)

    {

        int a, b, c;

        cin >> a >> b >> c;

        edge[i] = {a, b, c};

    }

    sort(edge, edge + m, cmp);

    for (int i = 1; i <=n;i++)

    {

        p[i] = i;

    }

    for (int i = 0; i < m;i++)

    {

        int a = edge[i].a, b = edge[i].b;

        int pa = find(a), pb = find(b);

        if(pa!=pb)

        {

            cont++;

            res += edge[i].c;

            p[pa] = pb;

        }

    }

      if(cont==n-1)

      {

          cout << res;

      }

      else

      {

          cout << "impossible";

      }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

### 二分图
![[Pasted image 20241003180734.png]]

![[Pasted image 20241003180258.png]]

#### 染色法判定二分图
[860. 染色法判定二分图 - AcWing题库](https://www.acwing.com/problem/content/862/)  
**思路**  
开始对任意一未染色的顶点染色。

判断其相邻的顶点中，若未染色则将其染上和相邻顶点不同的颜色。

若已经染色且颜色和相邻顶点的颜色相同则说明不是二分图，若颜色不同则继续判断。

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 2e5 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
ll idx, e[N], ne[N], h[N];
ll color[N];
void add(int a, int b)
{
    idx++;
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx;
}
bool dfs(int u, int cor)
{
    color[u] = cor;
    for (int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if (!color[j])
        {
            if (!dfs(j, 3 - cor))//将1换成2  将2换成1
            {
                return false;
            }
        }
        else if (color[j] == cor)
        {
            return false;
        }
    }
    return true;
}
void solve()
{
    memset(h, -1, sizeof h);
    int n, m;
    cin >> n >> m;
    for (int i = 0; i < m; i++)
    {
        int a, b;
        cin >> a >> b;
        add(a, b);
        add(b, a);
    }
    for (int i = 1; i <= n; i++)
    {
        if (!color[i])
        {
            if (!dfs(i, 1))
            {
                cout << "No";
                return;
            }
        }
    }
    cout << "Yes";
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```



#### 二分图的最大匹配
![[uwE7FNHfzxn5RZY.gif]]**思路**   
1.遍历左边所有点  
2dfs遍历该点所有可达的右边的点，若该点已被遍历过则跳过，否则有两种情况匹配成功，1，该右边的点没有匹配，2，该右边的点已匹配，存在一种情况右边的点可以与另一个点匹配，然后将该点换过去，然后继续递归3然后找到匹配的点即可

<font style="background-color:#f3bb2f;">st数组的作用</font>再递归的过程中 st设为true之后就不必再重复搜索  
[860. 染色法判定二分图 - AcWing题库](https://www.acwing.com/problem/content/862/)

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 2e5 + 10;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
ll idx, e[N], ne[N], h[N];
ll match[N];//通过右半部的下标访问已经匹配的左半部的下标
ll st[N];
int n1, n2, m;
void add(int a, int b)
{
    idx++;
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx;
}
bool find(int u)
{
    for (int i = h[u]; i != -1;i=ne[i])
    {
        int j = e[i];
        if(!st[j])
        {
            st[j] = true;
            if(match[j]==0 || find(match[j]))
            {
                match[j] = u;
                return true;
            }
        }
    }
    return false;
}
void solve()
{
    memset(h, -1, sizeof h);
    cin >> n1 >> n2>> m;
    for (int i = 0; i < m;i++)
    {
        int a, b;
        cin >> a >> b;
        add(a, b);
    }
    ll res = 0;
    for (int i = 1; i <= n1;i++)
    {
        memset(st, false, sizeof st);
        if(find(i))
            res++;
    }
    cout << res;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 数论初步
### 快速幂
将n转化为2进制表示，如果n的二进制中有当前的a的几次方就加入到ans里

```cpp

ll fastpow(ll a,ll n)

{

    ll ans=1;

    while(n)

    {

        if(n&1)

            ans *= a;

        a *= a;

        n >> 1;

    }

    return ans;

}
```

### gcd最大公因数
```plain
ll gcd(ll a,ll b)

{

    return b == 0 ? a : gcd(b, a % b);

}
```



## [数论基础 - OI Wiki](https://oi-wiki.org/math/number-theory/basic/)
### 同余原理
(a-b)%m=((a%m-b%m)+m)%m

换成加法同样适用



### 质数
**定义** 为在大于1的自然数中，除了1和它本身以外不再有其他因数，素数有无穷多个。

#### 试除法判定质数
```cpp


bool isprime(int a)

{

    if(a==1)

        return false;

    else

    {

        for (int i = 2; i <= a/i;i++)

        {

            if(a%i==0)

            {

                return false;

            }

        }

    }

    return true;

}

void solve()

{

    int n;

    cin>>n;

    for (int i = 0; i < n;i++)

    {

        int a;

        cin >> a;

        if(isprime(a))

        {

            cout << "Yes"<<'\n';

        }

        else

        {

            cout << "No" << '\n';

        }

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

#### 试除法分解质因数
[867. 分解质因数 - AcWing题库](https://www.acwing.com/problem/content/869/)  
1没有质因数质数，质数最大是二

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 2e5 + 10;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

void zhiyin(int a)

{

    for (int i = 2; i <= a/ i;i++)

    {

        if(a%i==0)

        {

            int s = 0;

            while(a%i ==0)

            {

                a /= i;

                s++;

            }

            cout << i << ' ' << s << '\n';

        }

    }

    if(a>1)

        cout << a << " 1"<<'\n';

}

void solve()

{

    int n;

    cin>>n;

    for (int i = 0; i < n;i++)

    {

        int a;

        cin >> a;

        zhiyin(a);

        cout << '\n';

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```



#### 质数筛--埃式筛法
[1、素数筛（这应该是最全的总结了，四种基本方法，7种优化方法）-CSDN博客](https://blog.csdn.net/Yuki_fx/article/details/115103663)

```cpp

#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e7;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

bool vit[N];

  

int prime[N];

  

int sai(int n)

  

{

  

    int cont = 0;

  

    for (int i = 2; i <= n; i++)

  

    {

  

        if (!vit[i]) // 只对质数进行倍增筛选

  

        {

  

            prime[cont++] = i;

            for (int j = i; (ll)j * i <= n; j++) // j代表倍数

  

            {

  

                vit[i * j] = true;

            }

        }

    }

  

    return cont;

}

  

void solve()

  

{

  

    int n;

  

    cin >> n;

  

    cout << sai(n);

}

  

int main()

  

{

  

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

  

    int T;

  

    T = 1;

  

    while (T--)

  

        solve();

  

    return 0;

}
```

#### 欧拉筛法
```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 1e7;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
bool vit[N];

int prime[N];

int sai(int n)
{
    int  cont = 0;
    for (int i = 2; i <= n;i++)
    {
        if(vit[i]==false)
        {
            prime[cont++] = i;
        }
    
    for (int j = 0; j <= cont;j++)
    {
        if(i*prime[j]>n)
        {
            break;
        }
        vit[i * prime[j]] = true;
        if (i % prime[j] == 0) // 这条语句的加入，保证了每个合数只会被筛除一次，不会被重复筛除。那么为什么？

            //当 i 可以整除素数表中某个素数时，那么 i 就不需要在往后乘以其他素数了，因此往后乘以得到的结果，会以另外一种方式得到。
            {
                break;
            }
    }
    }
    return cont;
}

void solve()

{

    int n;

    cin >> n;

    cout << sai(n);
}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;
}
```

### 约数
#### 试除法求约数
```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <string.h>

#include <bitset>

#include <sstream>

#include <unordered_map>

using namespace std;

const int N = 1e7;

const int P = 131;

using ll = long long;

using ull = unsigned long long;

void yue(int n)

{

    vector<int> y;

    for (int i = 1; i <= n / i;i++)

    {

        if(n%i==0)

        {

            y.emplace_back(i);

        if(i !=n/i)

        {

            y.emplace_back(n/i);

        }

        }

    }

    sort(y.begin(), y.end());

    for (int i = 0; i < y.size();i++)

    {

        cout << y[i]<<' ';

    }

}

void solve()

{

    int t;

    cin >> t;

    for (int i = 0; i < t;i++)

    {

        int a;

        cin >> a;

        yue(a);

        cout << '\n';

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

#### 求 约数的个数
把一个数N 写成：N = (p1<sup>x1</sup>)(p<sup>x2)(p3</sup>x3)…(pk^xk)，其中pi为质数。则N的约数个数为：(x1+1)(x2+1)(x3+1)…(xk+1)  
![[Pasted image 20241005190714.png]]  
<font style="background-color:#f3bb2f;">为什么不是加而是乘</font>  因为=p<sup>x1-1 也是他的约数 p</sup>x2-2 * p^x1-1 也是他的约数所以共有(a1+1)* ( a2+1)* ...个数了

#### 求约数之和
[871. 约数之和 - AcWing题库](https://www.acwing.com/problem/content/873/)  
![[Pasted image 20241006101901.png]]

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <string.h>
#include <bitset>
#include <sstream>
#include <unordered_map>
using namespace std;
const int N = 1e7;
const int P = 131;
using ll = long long;
using ull = unsigned long long;
unordered_map<int, int> mp;
void yue(int n)
{
    for (int i = 2; i <= n / i; i++)
    {
        while (n % i == 0)
        {
            mp[i]++;
            n /= i;
        }
        }
    if (n > 1)
        mp[n]++;
}
void solve()
{
    int t;
    cin >> t;
    for (int i = 0; i < t; i++)
    {
        int a;
        cin >> a;
        yue(a);
    }
    ll res = 1;
    ll MOD = 1e9 + 7;
    for (auto it : mp)
    {
        ll t = 1;
        while(it.second--)
        {
            t = (t * it.first + 1) % MOD;
        }
        res = res * t % MOD;
    }
    
    cout << res;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

![[Pasted image 20241006101926.png]]

### 求最大公约数
![[Pasted image 20241006102202.png]]

```cpp
ll gcd(int a,int b)

{

    return b == 0 ? a : gcd(b, a % b);

}
```

### 欧拉函数：1——N中与N互质的数个数
[873. 欧拉函数 - AcWing题库](https://www.acwing.com/problem/content/875/)  
![[Pasted image 20241019160648.png]]

```cpp
void solve()

{

    int n;

    cin >> n;

    for (int j = 0; j < n; j++)

    {

        int a;

        cin >> a;

        int res = a;

        for (int i = 2; i <= a / i; i++)

        {

            if (a % i == 0)

            {

                res = res / i * (i - 1);//如果为res*(i-1)/i会溢出

                while (a % i == 0)

                {

                    a /= i;

                }

            }

        }

        if (a > 1)//如果最后a不为0，代表还有一个大于n的约数，此时为a本身

            res = res / a * (a - 1);

        cout << res << '\n';

    }

}
```



### 筛法求欧拉函数
[874. 筛法求欧拉函数 - AcWing题库](https://www.acwing.com/problem/content/876/)  
**思路**  
分为三种情况  
当前这个数记为i；  
1.该数是质数，如果该数是质数则其欧拉函数为i-1；  
2.该i * p被质数p整除，那其i * P欧拉函数为p*( i的欧拉函数)  
3.该i* p不能被质数p整除那其i * p的欧拉函数(i的欧拉函数) * (p-1)

```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <cmath>

#include <string.h>

#include <bitset>

#include <sstream>

#include <numeric>

#include <queue>

using namespace std;

const int N = 1e6 + 10;

using ll = long long;

using ull = unsigned long long;

ll prime[N], phil[N];

bool vit[N];

ll euler(ll n)

{

    phil[1] = 1;

    int cnt = 0;

    for (int i = 2; i <= n; i++)

    {

        if (!vit[i])

        {

            prime[cnt++] = i;

            phil[i] = i - 1;

        }

        for (int j = 0; prime[j] <= n / i; j++)

        {

            int t = prime[j] * i;

            vit[t] = true;

            if (i % prime[j] == 0)

            {

                phil[t] = prime[j] * phil[i];

                break;

            }

            else

            {
                phil[t] = phil[i] * (prime[j] - 1);
            }

        }

    }

    ll ans = 0;

    for (int i = 1; i <= n; i++)

    {

        ans += phil[i];

    }

    return ans;

}

void solve()

{

    int n;

    cin >> n;

    cout << euler(n);

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T = 1;

    while (T--)

        solve();

    return 0;

}
```

## 逆元
**定义**  
![[Pasted image 20241020215257.png]]  
![[Pasted image 20241020215117.png]]  
当n为质数时，可以用快速幂求逆元：  
a / b ≡ a * x (mod n)  
两边同乘b可得 a ≡ a * b * x (mod n)  
即 1 ≡ b * x (mod n)  
同 b * x ≡ 1 (mod n)  
由费马小定理可知，当n为质数时  
b ^ (n - 1) ≡ 1 (mod n)  
拆一个b出来可得 b * b ^ (n - 2) ≡ 1 (mod n)  
<font style="background-color:#f3bb2f;">故当n为质数时，b的乘法逆元 x = b ^ (n - 2)</font>

当n不是质数时，可以用扩展欧几里得算法求逆元：  
a有逆元的充要条件是a与p互质，所以gcd(a, p) = 1  
假设a的逆元为x，那么有a * x ≡ 1 (mod p)  
等价：ax + py = 1  
exgcd(a, p, x, y) 

## 快速幂
其精髓在于将底数不断平方  
将n转化为2进制表示，如果n的二进制中有当前的a的几次方就加入到ans里

```cpp
include <iostream>
#include <algorithm>

using namespace std;

typedef long long LL;


LL qmi(int a, int b, int p)
{
    LL res = 1 % p;//如果p=1，b=0,此时如果res=1;则会返回1,如果为1%p则返回0正确答案
    while (b)
    {
        if (b & 1) res = res * a % p;
        a = a * (LL)a % p;
        b >>= 1;
    }
    return res;
}


int main()
{
    int n;
    scanf("%d", &n);
    while (n -- )
    {
        int a, b, p;
        scanf("%d%d%d", &a, &b, &p);
        printf("%lld\n", qmi(a, b, p));
    }

    return 0;
}
```

### 快速幂求逆元
```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <cmath>
#include <string.h>
#include <bitset>
#include <sstream>
#include <numeric>
#include <queue>
#include <unordered_map>
using namespace std;
const int N = 1e6 + 10;
using ll = long long;
using ull = unsigned long long;
ll fastpow(int a, int b, int p)
{
    ll res = 1;
    while (b)
    {
        if (b & 1)
        {
            res = res * a % p;
        }
        b = b >> 1;
        a =(ll) a * a % p;//转换成longlong类型
    }
    return res;
}
void solve()
{
    int a, p;
    cin >> a >> p;
    if(a%p!=0)
    cout << fastpow(a, p - 2, p) << "\n";
    else
    cout<<"impossible\n";
    
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    cin >> T;
    while (T--)
        solve();
    return 0;
}
```

## 扩展欧几里得算法求逆元
证明  
![[Pasted image 20241026193006.png]]



```cpp
#include <iostream>
#include <algorithm>

using namespace std;

int exgcd(int a, int b, int &x, int &y)
{
    if (!b)
    {
        x = 1, y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    return d;
}

int main()
{
    int n;
    scanf("%d", &n);

    while (n -- )
    {
        int a, b;
        scanf("%d%d", &a, &b);
        int x, y;
        exgcd(a, b, x, y);
        printf("%d %d\n", x, y);
    }

    return 0;
}
```



### 扩展欧几里得算法求线性同余方程
<font style="background-color:#f3bb2f;">证明</font>  
![[Pasted image 20241027161731.png]]



```cpp
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <cmath>

#include <string.h>

#include <bitset>

#include <sstream>

#include <numeric>

#include <queue>

#include <unordered_map>

using namespace std;

const int N = 1e6 + 10;

using ll = long long;

using ull = unsigned long long;

const int MOD = 1e9 + 7;

using ll = long long;

ll exgcd(int a,int b,int &x,int &y)

{

    if(!b)

    {

        x = 1, y = 0;

        return a;

    }

    ll d = exgcd(b, a % b, y, x);

    y -= a / b * x;

    return d;

}

void solve()

{

    int a, b, m;

    cin >> a >> b >> m;

    int x, y;

    ll d=exgcd(a, m, x, y);

    if(b%d==0)

    {

        cout << b / d * x % m<<'\n';

    }

    else

    {

        cout << "impossible" << '\n';

    }

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    cin >> T;

    while (T--)

        solve();

    return 0;

}
```

# DP(动态规划)
动态规划//定义的是状态，不是动作，根据动作转移状态

<font style="color:black;">动态规划的大致过程：</font>

<font style="color:black;">想出设计优良的递归尝试(</font><font style="color:#ee230c;">方法、经验、固定套路很多</font><font style="color:black;">)，</font><font style="color:#ee230c;">有关尝试展开顺序的说明</font>

<font style="color:black;">-> 记忆化搜索(从顶到底的动态规划) ，</font><font style="color:#ee230c;">如果每个状态的计算枚举代价很低，往往到这里就可以了</font>

<font style="color:black;">-> 严格位置依赖的动态规划(从底到顶的动态规划) ，更多是为了下面说的 </font><font style="color:#ee230c;">进一步优化枚举做的准备</font>

<font style="color:black;">-> 进一步优化空间（</font><font style="color:#ee230c;">空间压缩</font><font style="color:black;">），一维、二维、多维动态规划都存在这种优化</font>

<font style="color:black;">-> </font><font style="color:#ee230c;">进一步优化枚举也就是优化时间（本节没有涉及，但是后续巨多内容和这有关）</font>

<font style="color:black;">解决一个问题，可能有很多尝试方法</font>

<font style="color:black;">众多的尝试方法中，可能若干的尝试方法有重复调用的情况，可以转化成动态规划</font>

<font style="color:black;">若干个可以转化成动态规划的方法中，又可能有优劣之分</font>

<font style="color:black;">判定哪个是最优的动态规划方法，</font><font style="color:#ee230c;">依据来自题目具体参数的数据量</font>

<font style="color:black;">最优的动态规划方法实现后，</font><font style="color:#ee230c;">后续又有一整套的优化技巧</font>

## 01背包 每件物品最多用一次
### 为什么可以转为一维
首先观察状态转移方程 dp[i][j]是由 dp[i-1][jxxxx]推导而来，仅看第一个维度，即i - 1 与 i ，可以发现第i层是由上一层推导而来的。

故我们不必要保存i - 2 层，比如我们计算第三层是只需要第二层的。不需要第一层的数据。

当我们去掉i时，即我们不需要控制第几层，只需要长度为j的数组，保存确认过最新的一层。作为下一层的参考。例如我们计算第三层dp时，此时dp原数据保存的是第二层的结果。

### 为什么要逆序
首先，通过上一个问题，我们确认了我们目前一维的dp数组，保存的是确认过的最新一层的数据，即上一层的数据。

当我们计算当前层时，对于二维时的状态转移方程有

dp[i][j] = max(dp[i][j], dp[i - 1][j - v[i]] + w[i]);

可以看到，dp[i - 1][j - v[i]] + w[i] 使用的上一层的原始数据（dp[i - 1]），而我们使用一维的状态转移方程时有

dp[j] = max(dp[j], dp[j - v[i]] + w[i]);

当我们从小到大更新是， 因为j - v[i] 是严格小于j 的，所以我们可以举个例子 dp[3] = max(dp[3], dp[2] + 1); 因为我们是从小到大更新的，所以当更新到dp[3]的时候，dp[2]已经更新过了，已经不是上一层的dp[2]。

而当我们逆序更新时有，举例 dp[8] = max(dp[8], dp[6] + 2)当更新dp[8]时，dp[6]还没有被更新，还是上一层的数据，这样才能保证没有读入脏数据。



![[Pasted image 20241107175857.png]]  
![[Pasted image 20241114220559.png]]  
代码  
二维

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <cmath>
#include <string.h>
#include <bitset>
#include <sstream>
#include <numeric>
#include <queue>
using namespace std;
const int N = 1e3 + 10;
using ll = long long;
using ull = unsigned long long;
ll v[N], w[N];
ll dp[N][N];//dp[i][j]第一维表示选取不超过i个物品，第二维表示选取的物品数量的最大值不超过j
void solve()
{
    int n, V;
    cin >> n >> V;
    for (int i = 1; i <=n;i++)
    {
        cin >> v[i] >> w[i];
    }
    //因为dp[0][0~n]选取0个物品所以都应该为0，全局变量自动为0，所以i从1开始
    for (int i = 1; i <=n;i++)
    {
        for (int j = 0; j <= V;j++)
        {
            dp[i][j] = dp[i - 1][j]; // 因为可能选当前这个v[i]大于背包总量，所以先要继承上一个状态;
            if(j>=v[i])
            {
                dp[i][j] = max(dp[i-1][j], dp[i-1][j-v[i]] + w[i]);//第二个是选了该物品，
            }
        }
    }
    cout << dp[n][V];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}

```

一维

```cpp
#include<iostream>
#include<cstring>
using namespace std;
const int N = 1010;
int n, m;
int dp[N];
int v[N], w[N];

int main(){
    cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i];

    for (int i = 1; i <= n; i++)
        for (int j = m; j >= v[i]; j --)
            dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
    cout << dp[m];
    return 0;
}
```



## 完全背包 每件物品有无限个
完全背包  
![[Pasted image 20241114150749.png]]

```plain
#include <iostream>

#include <stdio.h>

#include <vector>

#include <algorithm>

#include <stack>

#include <set>

#include <map>

#include <queue>

#include <cmath>

#include <string.h>

#include <bitset>

#include <unordered_map>

#include <sstream>

#include <numeric>

#include <queue>

using namespace std;

const int N = 1e3 + 10;

using ll = long long;

using ull = unsigned long long;

ll w[N],v[N];

ll dp[N][N];

void solve()

{

  

    int n, m;

    cin >> n >> m;

    for (int i = 1; i <=n;i++)

    {

        cin>>v[i]>>w[i];

    }

    for (int i = 1; i <= n;i++)

    {

        for (int j = 1; j <= m;j++)

        {

            dp[i][j] = dp[i - 1][j];

            if(j>=v[i])

            {

                dp[i][j] = max(dp[i-1][j], dp[i][j - v[i]] + w[i]);

            }

        }

    }

    cout << dp[n][m];

}

int main()

{

    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);

    int T;

    T = 1;

    while (T--)

        solve();

    return 0;

}
```

## 多重背包 物品个数不一样
### 朴素版(用于理解)
**思路**转化为0，1背包问题一直到s个第k个取与不取

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <cmath>
#include <string.h>
#include <bitset>
#include <unordered_map>
#include <sstream>
#include <numeric>
#include <queue>
using namespace std;
const int N = 1e3 + 10;
using ll = long long;
using ull = unsigned long long;
ll w[N],v[N],s[N];
ll dp[N];
void solve()
{

    int n, m;
    cin >> n >> m;
    for (int i = 1; i <=n;i++)
    {
        cin>>v[i]>>w[i]>>s[i];
    }
    for (int i = 1; i <= n;i++)
    {
        for (int j = m; j >= 0;j--)
        {
            for (int k = 0; k <= s[i] && k*v[i]<=j;k++)
            {
                dp[j] = max(dp[j], dp[j - k * v[i]] + k * w[i]);
            }
        }
    }
    cout << dp[m];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 二进制优化版
**思路** 由于从0到s[i]时间复杂度过高，可以用二进制将s[i]分为几组，  
假如s[i]为70  
1 2 4 8 16 32 可以表示1-63的物品数,在用一个70-63=7就可以表示所有1-70的数了  
然后就可以转化为0，1背包问题

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <cmath>
#include <string.h>
#include <bitset>
#include <unordered_map>
#include <sstream>
#include <numeric>
#include <queue>
using namespace std;
const int N = 3e4+ 10;
using ll = long long;
using ull = unsigned long long;
ll w[N], v[N];
ll dp[N];
void solve()
{

    int n, m;
    cin >> n >> m;
    int a, b, c;
    int cnt = 0;
    for (int i = 1; i <= n; i++)
    {
        cin >> a >> b >> c;
        int k = 1;
        while (k<=c)
        {
            cnt++;
            v[cnt] = k * a;
            w[cnt] = k * b;
             c -= k;
            k = k * 2;
        }
        if (c>0)
        {
            cnt++;
            v[cnt] = c * a;
            w[cnt] = c * b;
        }
    }//分组
    n=cnt;//在所有组里进行01背包问题
    for (int i = 1; i <= n; i++)
    {
        for (int j = m; j >= v[i]; j--)
        {
            dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
        }
    }
    cout << dp[m];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 分组背包问题   有n组每一组里面选一个问题
 每组选一个从后往前dp

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <cmath>
#include <string.h>
#include <bitset>
#include <unordered_map>
#include <sstream>
#include <numeric>
#include <queue>
using namespace std;
const int N = 3e3 + 10;
using ll = long long;
using ull = unsigned long long;
ll w[N], v[N];
ll dp[N];
void solve()
{
    int n, m;
    cin >> n >> m;
    int s = 0;
    for (int i = 0; i < n;i++)
    {
        cin >> s;
        for (int i = 0; i < s;i++)
        {
            cin >> v[i] >> w[i];
        }
            for (int j = m; j >= 0;j--)
            {
                for (int i = 0; i < s; i++)
                    if (j >=v[i])
                    {
                        dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
                    }
            }
    }
    cout << dp[m];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```



## 线性dp
### 数字三角形
[898. 数字三角形 - AcWing题库](https://www.acwing.com/problem/content/description/900/)  
![[Pasted image 20250113111706.png]]  
**思路**   
题目要求从上往下最大路径的数字和，如果从上往下最大路径和就要特判，就是两边的时候  
为了简便就从下往上求，然后当前位置dp[ i ]  j  是由dp i+1 j+1 和dp i+1 j 之间的最大值加上i j的权值决定的 dp数组表示的就是从底到当前位置的最大权值之和  
_状态转移方程_  ```c++

```plain

dp[i][j] = max(dp[i + 1][j], dp[i + 1][j + 1]) + w[i][j];

```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <numeric>
using namespace std;
const int N = 510;
using ll = long long;
using ull = unsigned long long;
ll w[N][N], dp[N][N];
void solve()
{
    int n;
    cin >> n;
    for (int i = 0; i <n; i++)
    {
        for (int j = 0; j <=i; j++)
        {
            cin >> w[i][j];
        }
    }
    for (int i = n-1; i >= 0; i--)
    {
        for (int j =0; j <= i; j++)
        {
            dp[i][j] = max(dp[i + 1][j], dp[i + 1][j + 1]) + w[i][j];
        }
    }
    cout << dp[0][0];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 最长上升子序列
[895. 最长上升子序列 - AcWing题库](https://www.acwing.com/problem/content/description/897/)  
**思路**  
dp数组表示以第i个数结尾的最长单调递增子序列个数  
状态转移方程

```cpp
遍历从0到i-1的所有数
if(a[j]<a[i])如果满足就加入与起自己比较
    dp[i] = max(dp[i], dp[j] + 1);
```

简单来说当前状态是由比他数小的状态得到的  
**代码**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <numeric>
using namespace std;
const int N = 1010;
using ll = long long;
using ull = unsigned long long;
ll dp[N], a[N];
void solve()
{
    int n;
    cin >> n;
    for (int i = 1; i <=n;i++)
    {
        cin >> a[i];
    }
    for (int i=1; i <=n;i++)
    {
        dp[i] = 1;
        for (int j = 1; j < i;j++)
        {
            if(a[j]<a[i])
                dp[i] = max(dp[i], dp[j] + 1);
        }
    }
    ll ans = 0;
    for (int i = 1; i <=n;i++)
    {
        ans = max(ans, dp[i]);
    }
    cout << ans;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}

```

最长上升子序列二  
[896. 最长上升子序列 II - AcWing题库](https://www.acwing.com/problem/content/898/)  
![[Pasted image 20250113143015.png]]  
将每个个数一样的最长子序列数分为一组然后取尾数最小的最优，可以看出结尾的数是单调递增的然后由此可以想到二分

**思路** <font style="background-color:#f3bb2f;">q数组下标代表个数，其结尾的值代表每一个个数的最长子序列遍历每个子序列中的数</font>，q数组就代这个表首先二分找到比a【i】小的数，然后将该数加1替换进去，最后输出最大个数即可

```cpp

```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <numeric>
using namespace std;
const int N = 100000;
using ll = long long;
using ull = unsigned long long;
ll q[N], a[N];
void solve()
{
    int n;
    cin >> n;
    for (int i = 1; i <=n;i++)
    {
        cin >> a[i];
    }
    int len = 0;
    for (int i = 1; i <= n;i++)
    {
        int l = 0, r = len+1, mid;
        while(l+1!=r)
        {
            mid = l + r >> 1;
            if(q[mid]>=a[i])
            {
                r = mid;
            }
            else
            {
                l = mid;
            }
        }
        q[l + 1] = a[i];
        len = max(len,l + 1);
    }
    cout << len;
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 最长公共子序列
[897. 最长公共子序列 - AcWing题库](https://www.acwing.com/problem/content/899/)

<font style="background-color:#f3bb2f;">dp方程含义</font>所有a【1-i] b 【1-j]的公共子序列的集合  
![[Pasted image 20250113210159.png]]

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <numeric>
using namespace std;
const int N = 1010;
using ll = long long;
using ull = unsigned long long;
ll dp[N][N];
void solve()
{
    int n, m;
    cin >> n >> m;
    string a, b;
    cin >> a >> b;
        for (int i = 1; i <=n; i++)
        {
            for (int j = 1; j <=m; j++)
            {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
                if (a[i-1] == b[j-1])
                {
                    dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + 1);
                }
            }
        }
    cout << dp[n][m];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

### 最长公共上升子序列
要求：求两个序列的最长公共子序列

首先状态表示dp[i][j]表示所有a[1-i] b[1-j]中以b[j]结尾的公共上升子序列

状态划分，分为不包含a[i]和包含a[i]

'a' 首先不包含a[i]的子集，那就为f[i-1][j]；

前提为a[i]等于b[i]其次包含a[i]的子集,将这个子集继续划分,在b[i]中找到数可以插入到a[i]这个子序列中，

子序列只包含b[j]一个数，长度是1；

子序列的倒数第二个数是b[1]的集合，最大长度是f[i - 1][1] + 1；

…

子序列的倒数第二个数是b[j - 1]的集合，最大长度是f[i - 1][j - 1] + 1；

优化做法：可以观察到每次循环求得的maxv是满足a[i]>b[k]的f[i-1][k]+1的前缀最大值，因此看了一将maxv提到外面，当a[i]==b[j]时候更新答案

```cpp
#include <bits/stdc++.h>
//#define int long long
using namespace std;
const int N =3001;
int a[N];
int b[N];
int dp[N][N]; // 第一个序列的前i个字母，和第二个序列的前j个字母，以b[j]结尾的公共上升子序列
void solve()
{
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++)
    {
        cin >> b[i];
    }
    for (int i = 1; i <= n; i++)
    {
        int mxv =0;
        for (int j = 1; j <= n; j++)
        {
            // 如果不考虑第a[i]个数
            dp[i][j] = dp[i - 1][j];
            //if (a[i] == b[j]) dp[i][j] = max(dp[i][j], maxv);
            //if (a[i] > b[j]) maxv = max(maxv, dp[i - 1][j] + 1);
            
           if (a[i] > b[j])
            {
                mxv = max(dp[i - 1][j], mxv);
            }
            if (a[i] == b[j])
            {
                dp[i][j] = max(dp[i][j], mxv+1);
            }
        }
    }
    int res = 0;
    for (int i = 1; i <= n; i++)
        res = max(res, dp[n][i]);
    cout << res << '\n';
}
signed main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T = 1;
    // cin >> T;
    while (T--)
        solve();
    return 0;
}
```



### 最短编辑距离
[902. 最短编辑距离 - AcWing题库](https://www.acwing.com/problem/content/904/)  
![[Pasted image 20250116111311.png]]  
**思路**  
dp【i】【j】表示将a的前i个字符与b的前j个字符匹配的最小操作数，  
删除操作f【i]【j-1]+1;插入操作f【i-1]f【j]+1  
替换操作 如果不相等f【i]【j]+1如果相等f【i-1]f【j-1】

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <bitset>
#include <sstream>
#include <numeric>
using namespace std;
const int N = 1e3 + 10;
using ll = long long;
using ull = unsigned long long;
ll dp[N][N];
void solve()
{
    int n;
    cin >> n;
    string a;
    cin >> a;
    int m;
    cin >> m;
    string b;
    cin >> b;
   for (int i = 0; i <=a.size();i++)
    {
        dp[i][0] = i;
    }
    for (int i = 0; i <= b.size();i++)
    {
        dp[0][i] = i;
    }
    for (int i = 1; i <= a.size();i++)
    {
        for (int j = 1; j <= b.size();j++)
        {
            dp[i][j] = min(dp[i - 1][j]+1, dp[i][j-1]+1);
            if(a[i-1]==b[i-1])
            {
                dp[i][j] = min(dp[i][j], dp[i - 1][j - 1]);
            }
            else
            {
                dp[i][j] = min(dp[i][j], dp[i - 1][j - 1]+1);
            }
        }
    }
    cout << dp[n][m];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```

## 区间dp
### 石子合并
[282. 石子合并 - AcWing题库](https://www.acwing.com/problem/content/description/284/)、  
**思路**  
**思路** dp【i】【j】表示i。j区间内合并石子的最小值  
依次遍历区间2-n；  
设中心点k枚举从i-k k+1-j区间值为遍历到当前的区间值

```cpp
dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j] + prefix[j] - prefix[i - 1]);

```

```cpp
#include <iostream>
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <stack>
#include <set>
#include <map>
#include <queue>
#include <unordered_map>
#include <cmath>
#include <string.h>
#include <bitset>
#include <sstream>
#include <numeric>
using namespace std;
const int N =400;
using ll = long long;
using ull = unsigned long long;
ll dp[N][N];//i,j区间内合并石子的最小值
ll a[N];
ll prefix[N];
void solve()
{
    int n;
    cin >> n;
    for (int i = 1; i <=n;i++)
    {
        cin >> a[i];
    }
    for (int i = 1; i <=n;i++)
    {
        prefix[i] = a[i] + prefix[i - 1];
    }
    for (int len = 2; len <= n;len++)
    {
        for (int i = 1; i+len-1<=n;i++)
        {
            int j = i+len-1;
            dp[i][j]=1e8;
            for (int k = i; k <j;k++)
            {
                dp[i][j] = min(dp[i][j], dp[i][k] + dp[k + 1][j] + prefix[j] - prefix[i - 1]);
            }
        }
    }
    cout << dp[1][n];
}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    while (T--)
        solve();
    return 0;
}
```





## 树形dp
树形dp的父亲结点的结果完全依赖与子节点，所以要先将所有子节点求出后，在根据状态转移方程求出子节点

### 最大独立集
**<font style="color:rgb(64, 64, 64);">选择一个点集，使得任意两个被选择的点都没有边直接相连，并且使得所有被选择的点的点权之和最大。</font>**

简单来说给你一个树，选择一个节点后就不能选择它的子节点，求最大的能够选择的节点数

**思路**：先定义状态，dp[N][2]dp[i][j]表示第i个节点选或者不选，j为1选，为0不选然后遍历所有子节点，递归，然后根据状态转移方程求出当前的节点就行



```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 6000 + 10;
using ll = long long;
using ull = unsigned long long;
vector<vector<int>> adj(N);
int n;
ll dp[N][2];
void dfs(int u,int pt)
{
   dp[u][1]=1;//选择当前节点和不选择当前节点
   dp[u][0]=0;
    for(auto it:adj[u])
    {
        if(it==pt)
        {
            continue;
        }
        dfs(it,u);
        dp[u][0]+=max(dp[it][1],dp[it][0]);
        dp[u][1]+=dp[it][0];
    }
}
void solve()
{
    cin>>n;
    for(int i=0;i<n-1;i++)
    {
        int u,v;
        cin>>u>>v;
        u--;
        v--;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    dfs(0,-1);
    cout<<max(dp[0][0],dp[0][1]);

}
int main()
{
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    int T;
    T = 1;
    //cin >> T;
    while (T--)
        solve();
    return 0;
}
```





# 博弈论
SG函数

<font style="color:rgb(0, 0, 0);">f(v)=mex{f(u)|u∈child[v]}</font>

<font style="color:rgb(0, 0, 0);">child为后继所有可能出现的状态，v为当前状态</font>

<font style="color:rgb(0, 0, 0);">其中，mex(minimal excludant)是定义在整数集合上的操作。它的自变量是任意整数集合，函数值是不属于该集合的最小自然数。</font>

<font style="color:rgb(0, 0, 0);">mex(A)=min{k|k∈∁</font><font style="color:rgb(0, 0, 0);">N</font><font style="color:rgb(0, 0, 0);">A}</font>

<font style="color:rgb(0, 0, 0);">SG为0为先手手必败态，SG大于0为先手必胜态</font>

