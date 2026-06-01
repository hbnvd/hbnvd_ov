#DSA/Sub-array #DSA/Kadane

- Tính tổng của 1 mảng con lớn nhất có/không chọn mảng rỗng. Nếu không chọn mảng rỗng thì nó là [[CP00005]] á;)).

---
Nguồn:
- Khái niệm:
	- https://www.geeksforgeeks.org/dsa/largest-sum-contiguous-subarray/ 
- Bài tập:
	- https://www.geeksforgeeks.org/dsa/largest-sum-contiguous-subarray/
	- https://nhpoj.net/problem/MAXSUM1D

---
Chương này bao gồm:
1. Khái niệm

---

# I. Khái niệm
- Basic vl, chả bt ghi cái gì;))
- Code này là 1-idx
```cpp
cin >> n;

for (int i = 1; i <= n; ++i) {
	cin >> a[i];
}
int ans = a[1], sum = a[1];

// dc chọn mảng rỗng
for (int i = 2; i <= n; ++i) { 
	sum = max(sum + a[i], 0);
	ans = max(ans, sum)
}
// ko cho chọn mảng rỗng
for (int i = 2; i <= n; ++i) { 
	sum = max(a[i], sum + a[i]);
	ans = max(ans, sum);
}

cout << ans << "\n";

```