---
tags:
  - "#DSA/Recursion"
cssclasses:
---

> Đệ quy là 1 trong những kỹ thuật toàn năng nhất trong lập trình, đến mức người ta không coi nó như 1 kỹ thuật, mà là 1 cách tư duy khác biệt. 100% bài bạn từng giải trước đây bằng for, while đều có thể giải quyết bằng đệ quy (TLE hay không thì toi không biết nhé;)))



**Nguồn**
- https://wiki.vnoi.info/algo/basic/backtracking.md
# Khái niệm
**Bản chất**: 1 hàm tự gọi chính nó

- Đệ quy có thể áp dụng ở những bài toán có thể dựng 1 trạng thái bằng 1 hoặc nhiều trạng thái trước đó (`bài toán con`), và càng làm thì sẽ hướng tới 1 cái mốc cố định, nơi bài toán có đáp án mà không dựa vào bài toán con nào (`neo`).
Ví dụ như công thức giai thừa, ta có:
$$n! =(n-1)!$$
Với neo là :
$$0!=1$$
2 công thức trên có thể được viết lại thành công thức truy hồi sau
$$
f(n) = 
\begin{cases} 
1 & \text{if  } n = 0 \\ 
n \times f(n - 1) & \text{if  } n > 0 
\end{cases}
$$
- Code ví dụ
**Cpp**
```cpp
#define ll long long
ll factorial(ll n) {
	if (n == 0) return;
	return n*factorial(n-1);
}
```
**Python**
```python
import sys
sys.setrecursionlimit(100000)
# giới hạn đệ quy trong py thường là 10^3 nên phải tăng thêm

def factorial(n):
	if (n==0): return 1
	return n*factorial(n-1)
```

- Ngoài ra còn có tính gcd, fibonacci, ..
- Thật ra có 1 số bài toán cũng không thực sự cần đệ quy mà có thể dùng while , hoặc for để tính dần lên, vừa tránh việc tính cùng 1 giá trị 2 lần vừa giúp bỏ đi thời gian để gọi hàm, người ta gọi đây là khử đệ quy.
- Nhưng nhân loại vẫn dùng đệ quy, bởi vì có 1 số tính chất đặc thù của đệ quy mà for và while không thể thay thế (không tính việc mô phỏng hàm bằng while + stack;)) , vd như kỹ thuật backtrack hay bài toán tháp hà nội.

# 1 số kỹ thuật dựa trên đệ quy
- [[Backtrack]]
- [[Dynamic Programming]]


# Bài tập

## EZ vcl
- [[CP00017| fibonacci]]
