## 闰年计算
1.能被4整除但不能被100整除
2.能被400整除
## instre![[屏幕截图 2024-10-21 113042.png]]am读取文件时
```c++
int main()
{
	string s;
	ifstream in("a.txt");
	ofstream out("b.txt");
	while (in)
	{
	in>>s
		for (int i = s.size() - 1; i >= 0; i--)
		{
			if (s[i] == ')' || s[i] == '(' || s[i] == ',')
			{
				s[i] = ' ';
			}
		}
		ca(s);
		out << s;
		out << endl;
	}
}

```
假设文件有五行此代码会输出六行，因为只有当in>>s读取不到时in才会更新输入流为无效,因此当读到文件尾时仍要进行一次循环

# 字母大小写转化
toupper
tolower
==用cout输出的返回字母的ascii码值==
要输出字母记得 cout<<(char)tolower('A')

# 使用cout.tie(0)注意事项

如果使用cout.tie(0)后在使用printf和cout的话会出现输出顺序不对的情况；


# memset的使用
![[Pasted image 20240817194151.png]]


# 为什么hash取模时要取质数
![[Pasted image 20240818152557.png]]

# 遍历一个字符串的所有子字符串
子字符串：**子字符串** 是字符串中的一个连续、 **非空** 的字符序列。
```c++
class Solution {
public:
    int numberOfSubstrings(string s, int k) {
        int n=s.size();
        int  res=0;
        for(int i=0;i<n;i++)
        {
		    string s;
		    s+=s[i];
		    cout<<s;
            for(int j=i+1;j<n;j++)
            {
	            s+=s[j];
	            cout<<s;
            }
        }
        return res;
    }
};
```
# 求一个数除以他的最大因数后的结果，非他本身的因数
```c++
int tackle(int a)

    {

        for (int i = 2; i <= a / i; i++)

        {

            if (a % i == 0)//第一个可以整除a的数就是答案

            {

               return i;

            }

        }

        return a;//如果没找到那么a为质数，返回其本身

    }
```



#  求从一个点出发的最短环
```c++
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

ll a[N];

ll dis[N];

void solve()

{

    int n, m;

    cin >> n >> m;

    vector<vector<int>> adj(n);

    for (int i = 0; i < m; i++)

    {

        int u, v;

        cin >> u >> v;

        u--, v--;

        adj[u].emplace_back(v);//建立邻接表

    }

    memset(dis, -1, sizeof dis);

    queue<int> dq;//将第一个点加入到队列中

    dis[0] = 0;//初始化距离

    dq.push(0);

    ll ans = n + 1;

    while (dq.size())

    {

        int u = dq.front();

        dq.pop();

        for (auto it : adj[u])

        {

            if (it == 0)

            {

                ans = min(ans, dis[u] + 1);//如果发现了指向该初始点的环则更新答案

            }

            if (dis[it] == -1)//如果没有遍历过该点则更新距离

            {

                dis[it] = dis[u] + 1;

                dq.push(it);

            }

        }

    }

    if (ans > n)

    {

        ans = -1;

    }

    cout << ans << '\n';

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


## 双向并查集，单向dfs[2101. 引爆最多的炸弹 - 力扣（LeetCode）](https://leetcode.cn/problems/detonate-the-maximum-bombs/description/)