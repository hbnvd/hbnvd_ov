---
tags:
  - "#DSA/DS/Sparse-table"
---
**Bảng thưa**
- Là 1 cấu trúc dữ liệu để giải quyết các truy vấn thông thường trên 1 tập dữ liệu tĩnh với $O(logn)$ và các truy vấn **lũy đẳng (Idempotence) (min, max, gcd, lcm, AND, OR) với $O(1)$**
%% Cuối chapter có so sánh với segment tree (cả 2 điều dự trên khái niệm lũy thừa của 2)%%

**Tài liệu tham khảo**
- https://viblo.asia/p/bang-thua-sparse-table-MkNLrZPlLgA
- https://wiki.vnoi.info/algo/data-structures/rmq
- https://www.geeksforgeeks.org/dsa/sparse-table/

# Khái niệm
- Tạm gọi truy vấn cần thực hiện là $f()$.
- Bảng thưa dùng mảng 2 chiều
- Ở tầng đầu tiên \[0], chính là bản copy của mảng $A$ (mảng gốc cần truy vấn). 
- Ở tầng tiếp theo \[1], ta gom 2 phần tử ở tầng trước lại rồi thực hiện truy vấn $f()$.
- Ở tầng \[2], ta gom 2 phần tử ở tầng \[1], (tương đương 4 phần tử ở tầng \[0]), rồi thực hiện $f()$
- Làm vậy liên tục cho tới tầng thứ $\lfloor \log_2(n) \rfloor$ 

- Công thức **khởi tạo** sparse table (sp), tầng là $i$, cột là $j$, truy vấn là min $$sp[i][j]=\min(sp[i-1][j],sp[i-1][j+2^{i-1}])$$
- Công thức **truy vấn $O(1)$** cho truy vấn lũy đẳng trong đoạn $[l,r]$, $k=\lfloor \log_2(r-l+1) \rfloor$

$$min(l,r)=min(sp[k][l], sp[k][r-2^k+1]$$


> [!NOTE] **LƯU Ý**
> Khi code người ta thường cho mảng tĩnh là 1 hằng số, nên tùy theo điều kiện đề bài, (cùng lắm là $n \le 10^7$) ta sẽ dùng 20 (hoặc \#define LOG 20) làm số tầng cho mảng sp

# Code
## Cpp
```cpp
// Tạo mảng
#define LOG 20
int sp[LOG][100005];

// khởi tạo
for (int i = 1; i <= n; ++i) {
	sp[0][i] = a[i];
}
for (int i = 1; i <= LOG; ++i) {
	for (int j = 1; j <= n-(1<<i)+1; ++j) {
		sp[i][j] = min(sp[i-1][j], sp[i-1][j + (1<<(i-1))]);
	}
}

// truy vấn
int l, r; cin >> l >> r;
int k = __lg(r-l+1); // (int)log2(r-l+1)
cout << min(sp[k][l], sp[k][r-(1<<k)+1]) << "\n";
```

%% Còn với truy vấn không lũy đẵng (sum, ..) thì ummm, đi học segment tree đi;) %%

# Bài tập
- https://cses.fi/problemset/task/1647/
- [[CP00012]]