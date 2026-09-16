## 时间复杂度化简规则


### 核心规则

$$O(\max\{m, n\}) = O(m + n)$$

### 证明

假设 $n \leq m$，则：

$$m \leq m + n \leq 2m$$

所以：

$$O(m) = O(m + n) = O(\max\{m, n\})$$

### 真题（2013）

**题目**：两个长度分别为 $m$ 和 $n$ 的升序链表，合并为一个长度为 $m+n$ 的降序链表，最坏情况下的时间复杂度是？

**分析**：
- 合并两个升序链表：每个节点最多访问一次 → $O(m+n)$
- 根据规则：$O(m+n) = O(\max\{m, n\})$

**答案**：D. $O(\max(m,n))$

### 记忆点

- **看到 $O(m+n)$ 或 $O(\max\{m,n\})$，它们是等价的**
- 适用场景：遍历两个独立序列的算法（如归并、合并链表等）

---

## 线性表

**重点**：学思路，链表题一定要画图！

### 不同实现方式的时间复杂度

| 实现方式 | 查找 | 插入 | 删除 |
|---------|------|------|------|
| **数组** | O(1) 随机索引 | O(n) | O(n) |
| **单链表** | O(n) | O(1) 已知位置 | O(n) |
| **双链表** | O(n) | O(1) 已知位置 | O(1) |

### 双链表要点

**重点**：双链表一般都要有哨兵（左右两大护法），用于防止越界！

```cpp
// 双链表初始化 - 左右护法
Node *head = new Node(), *tail = new Node();
head->next = tail, tail->prev = head;

// 双链表插a（在head后插入）
auto a = new Node(1);
a->next = head->next, a->prev = head;
head->next->prev = a, head->next = a;

// 双链表尾插b（在a后插入）
auto b = new Node(2);
b->next = a->next, b->prev = a;
a->next->prev = b, a->next = b;

// 删除双链表b
b->prev->next = b->next;
b->next->prev = b->prev;
```

**顺序问题**：双链表操作时，前驱后继的顺序非常重要！

### 真题

#### 筛选链表

(AcWing 3759)

**思路**：用数组记录已出现的绝对值，遇到重复就删除

```cpp
class Solution {
public:
    ListNode* filterList(ListNode* head) {
        bool st[10001] = {};
        st[head->val] = 1;
        
        for (auto p = head; p->next; )
        {
            int x = abs(p->next->val);
            if (st[x])
            {
                auto temp = p->next;
                p->next = p->next->next;
                delete temp;
            }
            else {
                st[x] = 1;
                p = p->next;
            }
        }
        return head;
    }
};
```

#### 两个链表的第一个公共结点

(AcWing 62)

**思路**：两个指针分别从两个链表头出发，走到末尾后跳到另一个链表头，最终会在公共结点相遇

```cpp
class Solution {
public:
    ListNode *findFirstCommonNode(ListNode *headA, ListNode *headB) {
        auto p = headA, q = headB;
        
        while (p != q)
        {
            p = p ? p->next : headB;
            q = q ? q->next : headA;
        }        
        return p;
    }
};
```


---

## 栈与队列

**核心思想**：理解万岁，不要死记硬背指针条件。每种写法只要搞清楚「指针指向谁」，所有操作都能现推。

### 基本概念

| 结构     | 操作限制       | 特性         |
| ------ | ---------- | ---------- |
| **栈**  | 只能在栈顶插入/删除 | 后进先出（LIFO） |
| **队列** | 队尾插入，队头删除  | 先进先出（FIFO） |

---

#### 顺序栈（数组实现）

两种写法本质相同，区别只在 `top` 的语义：

| | top 指向栈顶元素 | top 指向下一个空位 |
|--|--|--|
| 初始 | `top = -1` | `top = 0` |
| 入栈 | `stack[++top] = x` | `stack[top++] = x` |
| 出栈 | `top--` | `--top` |
| 取栈顶 | `stack[top]` | `stack[top-1]` |
| 判空 | `top == -1` | `top == 0` |

```cpp
// 写法一：top 指向栈顶元素
int stack[N], top = -1;

// 入栈
stack[++top] = x;
// 出栈
top--;
// 判空
top == -1;
```

```cpp
// 写法二：top 指向下一个空位（更常用）
int stack[N], top = 0;

// 入栈
stack[top++] = x;
// 出栈
--top;
// 判空
top == 0;
```

---

#### 循环队列（顺序存储）

**<font color="#ffa657">笔试高频考点：判空判满条件</font>**

**常用写法**：`front` 指向队头元素，`rear` 指向队尾的下一个位置

```cpp
int q[N], front = 0, rear = 0;

// 入队
q[rear] = x;
rear = (rear + 1) % N;

// 出队
front = (front + 1) % N;

// 取队头
q[front];

// 判空
front == rear;

// 判满（牺牲一个单元区分空和满）
(rear + 1) % N == front;
```

**<font color="#ff7b72">易错</font>**：循环队列最多存 $N-1$ 个元素，不是 $N$ 个。因为 `front == rear` 既表示空也表示满，必须空一个位置来区分。

**另一种写法**：`front` 指向队头，`rear` 指向队尾元素本身

| 条件 | 公式 |
|------|------|
| 判空 | `front == (rear + 1) % N` |
| 判满 | `front == (rear + 2) % N` |
| 入队 | `rear = (rear + 1) % N; q[rear] = x;` |

> [!caution] 推导技巧
> 不要背公式。画出队列当前状态，模拟「再加一个元素」的过程，逆推初始值和判空/判满条件。

---

#### 链式存储

##### 链栈

本质 = **单链表的头插 + 头删**（栈顶 = 链表头）

```cpp
struct Node {
    int val;
    Node *next;
    Node(int v) : val(v), next(nullptr) {}
};

Node *top = nullptr;

// 入栈（头插）
Node *a = new Node(x);
a->next = top;
top = a;

// 出栈（头删）
Node *tmp = top;
top = top->next;
delete tmp;

// 取栈顶
top->val;

// 判空
top == nullptr;
```

##### 链队列

带头结点的单链表，`front` 指向头结点，`rear` 指向尾结点：

```cpp
// 初始化：front = rear = 头结点（哨兵）
Node *head = new Node(0);
Node *front = head, *rear = head;

// 入队：在 rear 后插入
rear->next = new Node(x);
rear = rear->next;

// 出队：删除 front->next
Node *tmp = front->next;
front->next = tmp->next;
if (rear == tmp) rear = front;  // 队列变空时修正 rear
delete tmp;

// 判空
front == rear;
```

---

### 应用
#### 中缀转后缀

<font color="#79c0ff">本质：表达式求值过程中，把「eval 计算」替换为「输出运算符」，把「数字压栈」替换为「直接输出数字」</font>

```cpp
#include <bits/stdc++.h>
using namespace std;

stack<char> op;
unordered_map<char, int> pr = {{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}};

int main() {
    string s;
    cin >> s;
    
    for (int i = 0; i < s.size(); i++) {
        if (isalnum(s[i])) {
            cout << s[i] << ' ';  // 数字/字母直接输出
        }
        else if (s[i] == '(') {
            op.push(s[i]);
        }
        else if (s[i] == ')') {
            while (op.top() != '(') {
                cout << op.top() << ' ';
                op.pop();
            }
            op.pop();
        }
        else {
            while (op.size() && op.top() != '(' && pr[op.top()] >= pr[s[i]]) {
                cout << op.top() << ' ';
                op.pop();
            }
            op.push(s[i]);
        }
    }
    
    while (op.size()) {
        cout << op.top() << ' ';
        op.pop();
    }
    return 0;
}
```

>[!hint] 非常吊
> **后缀表达式求值**：从左到右扫描，数字压栈，遇到运算符弹出两个数计算后压回，最终栈顶即结果。无需括号。 
>
>举例： $2 \,\,2 \,\,+\, \,1\, \,1 \,\,+\,\,\times\,\, 3\,\, +\,\, =\,\, 11$
>
**<font color="#d99694"> 用不到括号，递归形式运算</font>**

---

#### 表达式求值（必背模板）

**<font color="#ff7b72">AcWing 3302 — 全文熟背，笔试选择题/大题高频考点</font>**

**算法流程**：

1. 维护两个栈：`num`（数栈）、`op`（运算符栈）

2. 优先级：`+` `-` 为 1，`*` `/` 为 2

3. 扫描字符串：

   - 数字 → 解析完整数值，压入 `num`
   - `(` → 直接压入 `op`
   - `)` → 不断 eval 直到遇到 `(`，弹出 `(`
   - 运算符 → 若 `op` 栈顶优先级 $\geq$ 当前，则 eval；最后压入当前运算符

4. 扫描结束后，把 `op` 中剩余运算符全部 eval

5. `num.top()` 即为答案

```cpp
#include <bits/stdc++.h>
using namespace std;

stack<int> num;
stack<char> op;

// 优先级
unordered_map<char, int> pr = {{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}};

// 用 op 栈顶运算符操作 num 栈顶两个数
void eval() {
    int b = num.top(); num.pop();  // 注意：先弹的是右操作数
    int a = num.top(); num.pop();
    char c = op.top(); op.pop();
    
    int x;
    if (c == '+') x = a + b;
    else if (c == '-') x = a - b;
    else if (c == '*') x = a * b;
    else x = a / b;
    
    num.push(x);
}

int main() {
    string s;
    cin >> s;
    
    for (int i = 0; i < s.size(); i++) {
        if (isdigit(s[i])) {
            // 解析完整数字
            int x = 0, j = i;
            while (j < s.size() && isdigit(s[j]))
                x = x * 10 + s[j++] - '0';
            num.push(x);
            i = j - 1;  // 跳过已处理的字符
        }
        else if (s[i] == '(') {
            op.push(s[i]);
        }
        else if (s[i] == ')') {
            while (op.top() != '(') eval();
            op.pop();  // 弹出左括号
        }
        else {
            // 运算符：把优先级 >= 当前的全部算完
            while (op.size() && op.top() != '(' && pr[op.top()] >= pr[s[i]])
                eval();
            op.push(s[i]);
        }
    }
    
    // 处理剩余运算符
    while (op.size()) eval();
    
    cout << num.top() << endl;
    return 0;
}
```

**<font color="#ffa657">记忆要点</font>**：`eval()` 中先弹 b 再弹 a（后进先出），减法和除法顺序不能反。

---

#### 函数调用与 DFS

- 系统用**栈**维护函数调用路径（每进入一层 push，返回时 pop）

![[Pasted image 20260724102631.png|300]]


- 递归 $\leftrightarrow$ 深度优先搜索（DFS）

![[Pasted image 20260724102716.png|300]]

- **<font color="#ffa657">尾递归</font>**（递归调用是函数最后一句）不需要栈，等价于循环
```cpp
void f(int n)
{
	if (n <= 0) return;
	
	printf("%d/n", n);  // 执行完不会回来的函数
	f(n - 1);   // 递归是函数的最后一句话: 尾递归
}  

signed main()
{
	f(5); 
	return 0;
}
```


- 队列 $\leftrightarrow$ 广度优先搜索（BFS），逐层扩展

![[Pasted image 20260724103112.png|300]]

---




## 上机题总结

### 1. 多关键字排序

**场景**：成绩排序等需要稳定排序的场合

**核心**：使用归并排序（C++ `stable_sort`）

```cpp
#include <algorithm>
stable_sort(arr.begin(), arr.end(), cmp);
```

**注意**：`stable_sort` 保证相等元素的相对顺序不变

---

### 2. 进制转换

#### 其他进制 → 十进制

**方法**：秦九韶算法（直接套娃计算）

$$x = (a_{n-1}k + a_{n-2})k + ... + a_1)k + a_0$$

**示例**：$(123)_4 = 1 \times 4^2 + 2 \times 4^1 + 3 \times 4^0 = 27_{10}$

#### 十进制 → 其他进制

**方法**：短除法


```
4 | 27
4 | 6 ... 3
4 | 1 ... 2
  | 0 ... 1
```

结果：$\large (27)_{10} = (123)_4$


#### 大数进制转换模板（a进制 → b进制）

```cpp
// Problem: 进制转换2
// URL: https://www.acwing.com/problem/content/3377/

#include <bits/stdc++.h>
using namespace std;

int main() {
    int a, b;
    string s, res;
    vector<int> A;  // 倒序存储方便进位
    
    cin >> a >> b >> s;
    
    // 字符串转数字（倒序存储）
    for (int i = s.size() - 1; i >= 0; i--) {
        char c = s[i];
        if (c >= 'a') A.push_back(c - 'a' + 10);
        else A.push_back(c - '0');
    }
    
    if (s == "0") res = "0";
    else {
        // 短除法核心
        while (A.size()) {
            int r = 0;  // 余数
            for (int i = A.size() - 1; i >= 0; i--) {
                A[i] += r * a;  // 当前位 = 原值 + 进位×进制
                r = A[i] % b;   // 余数
                A[i] /= b;      // 商
            }
            while (A.size() && A.back() == 0) A.pop_back();  // 去除前导零
            
            if (r < 10) res += to_string(r);
            else res += r - 10 + 'a';
        }
        reverse(res.begin(), res.end());
    }
    
    cout << res << endl;
    return 0;
}
```

#### 时间复杂度分析

设 $x$ 为原数，$k = \log_m x$ 为 $m$ 进制下 $x$ 的位数

| 层级 | 复杂度 |
|------|--------|
| 最外层 while | $O(\log_n x)$ |
| 里层 divide | $O(\log_m x)$ |
| **总复杂度** | $O(k^2)$ |

---

### 3. 关键技巧速查

| 场景     | 方法                | 时间复杂度        |
| ------ | ----------------- | ------------ |
| 其他→十进制 | 秦九韶算法             | $O(n)$       |
| 十进制→其他 | 短除法               | $O(\log n)$  |
| 大数进制转换 | 短除法 + 向量存储        | $O(k^2)$     |
| 稳定排序   | `stable_sort`（归并） | $O(n\log n)$ |