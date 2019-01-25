#Dynamic Programming

###State 状态定义
储存小规模问题的结果
###Function 初始化,终点先有值
状态只加的联系,怎么通过小的状态来算大的状态
###Initialize 循环递推求解
最极限的小状态是什么
###Answer 求结果:起点
最大的那个状态是什么

###一般什么情况下可能是动态规划
- 求Maximum/Minimum
- Yes/No
- Count

###一般什么情况下不是动态规划
- 求所有具体的方案而不是方案数
- 输入数据是一个集合而不是序列

###常见DP
####Matrix DP
- state: f[x][y] 表示我从起点走到坐标x,y......
- function: 研究走到x,y这个点之前的一步
- intialize: 起点
- answer: 终点

####Sequence Dp
- state: f[i]表示“前i”个位置/数字/字母,(以第i个为)...
- function: f[i] = f[j] ... j 是i之前的一个位置
- intialize: f[0]..
- answer: f[n-1]..

####Two Sequences Dp
- state: f[i][j]代表了第一个sequence的前i个数字 /字符 配上第二个sequence的前j个...
- function: f[i][j] = 研究第i个和第j个的匹配关系
- intialize: f[i][0] 和 f[0][i]
- answer: f[s1.length()][s2.length()]
