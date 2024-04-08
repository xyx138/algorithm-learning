## c++优先队列

1. 引入头文件`#include<queue>`

2. 定义：`priority_queue<int, vector<int>, greater<int> > q;`

3. 参数：元素， 容器（一般是vector）， 比较函数
    > greater 为 小根堆， less为 大顶堆 *口诀*：函数名和实现的堆相反

4. 以pair为元素：则优先按first比较，再按second比较
    > 可以通过auto获取pair中的元素
    > `auto [x, y] = pair类型的数据`, **x, y不需要在之前进行声明数据类型**


### 代码

用优先队列优化最短路径算法

~~~c++
#include<iostream>
#include<vector>
#include<algorithm>
#include<cstring>
#include<queue>
using namespace std;

const int N = 510;

int g[N][N];
int dist[N];
int st[N];

int n, m;

int main(){
    cin >> n >> m;
    memset(g, 0x3f, sizeof g);
    memset(dist, 0x3f, sizeof dist);
    memset(st, 0, sizeof st);
    dist[1] = 0;
    while(m--){
        int a, b, w;
        scanf("%d%d%d", &a, &b, &w);
        g[a][b] = min(g[a][b], w);
    }

    // 优先队列声明
    priority_queue<pair<int, int>, vector<pair<int, int>> , greater<pair<int, int>>  > pri_q;
    pri_q.push(make_pair(0, 1));

    for(int i = 0; i < n; i++){
        if(pri_q.empty()) break;

        auto [d, t] = pri_q.top(); // 解绑
        pri_q.pop();


        st[t] = 1;

        for(int j = 1; j <= n; j++){
            if(!st[j] && dist[j] > dist[t] + g[t][j]){
                dist[j] = dist[t] + g[t][j];
                pri_q.push(make_pair(dist[j], j));
            }
        }
    }

    if(dist[n] == 0x3f3f3f3f) cout << -1;
    else cout << dist[n];
    
    return 0;
}


~~~