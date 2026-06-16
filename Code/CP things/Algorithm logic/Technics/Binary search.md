---
tags:
  - "#DSA/Binary-search"
  - "#DSA/Devide-to-conquer"
  - "#DSA/Search"
cssclasses:
---
- Tối ưu tốc độ tìm kiếm xuống log2(n) trên phạm vi có tính đơn điệu

 **Tài liệu tham khảo**
- https://wiki.vnoi.info/algo/basic/binary-search.md
- https://usaco.guide/silver/binary-search?lang=cpp

---
# Cơ sở của tìm kiếm nhị phân
- Cho 3 biến $lo, hi, mid$, (viết tắt của low, high, middle), cách gọi này để nói rằng nó là biên giới thôi chứ để left, right, mid cũng được.
- $lo, hi$ chính là biên giới phạm vi của vùng tìm kiếm
- $mid$ luôn được duy trì để nằm ở vị trí $(lo+hi)/2$ (ở giữa $lo, hi$).
- Cho thêm 1 hàm $f(x)$, chỉ trả về true hoặc false, hàm và mảng đã cho phải đáp ứng yêu cầu là mảng có giá trị true từ lúc bắt đầu cho tới 1 điểm nào đó thì chuyển qua false tới cuối mảng (hoặc ngược lại). 

- Tìm kiếm nhị phân thường chỉ áp dụng được cho những bài có tính chất:
	- Nếu f(mid) không thỏa yêu cầu thì chắc chắc 1 nửa phải hoặc 1 nửa trái còn lại cũng không thỏa yêu cầu.
	- Ta sẽ cho $lo = mid+1$ hoặc $hi=mid-1$ để loại bỏ nữa phải hoặc nữa trái đấy

Ví dụ: tìm giá trị vị trí của $x$ trên 1 mảng $a$ độ dài $n$ đã được sắp xếp tăng dần.
```cpp
int lo = 1, hi = n, mid;
while (lo <= hi) {
	mid = lo + (hi - lo)/2; // tránh tràn số
	if (a[mid] == x) { 
		cout << mid << "\n";
		return;
	} else if (a[mid] < x) { // f(m): if (a[m] < x) true else false
		lo = mid + 1;
	} else {
		hi = mid - 1;
	}
}
cout << -1 << "\n"; // khong tim thay
return;
```
- Ví dụ trên được gọi là tìm kiếm nhị phân cơ bản.

# Tìm kiếm nhị phân: tìm biên
- Quay lại đọc khái niệm hàm $f(x)$ đi;). Tìm kiếm nhị phân tìm biên ở đây thực chất chính là tìm cái biên nơi 0000 chuyển sang 1111 hay ngược lại.

- **Tìm kiếm nhị phân trên kết quả (Tìm kiếm nhị phân tổng quát):** Áp dụng cho các bài toán tối ưu hóa mà không gian tìm kiếm là các giá trị nguyên thỏa mãn một **hàm kiểm tra đơn điệu (P)**. Có hai mục tiêu phổ biến ở dạng này:
    - Tìm giá trị $x$ **nhỏ nhất** thỏa mãn điều kiện  $P(x)=1$,.
    - Tìm giá trị $x$ **lớn nhất** thỏa mãn điều kiện $P(x)=0$,.

- Nếu muốn, dựa trên 1 mảng $a$ sắp xếp không giảm, và 1 số $t$ cố định ...:
```cpp
int idx;

// lower_bound(a.begin(), a.end(), t) - a.begin() nếu dùng mảng tĩnh
i = lower_bound(a+1, a+n+1, t) - a; // i nhỏ nhất, a[i] >= t
i = upper_bound(a+1, a+n+1, t) - a; // i nhỏ nhất, a[i] > t

// thêm vào nếu cần tìm i lớn nhất, a[i] < t hoặc a[i] <= t
if (i > 1) --i; // 1-idx
if (i > 0) --i; // 0-idx



// 2 cái hàm trên là tên hàm trong c++ á;)), nó trả về iterator nên phải      - a.begin() để lấy idx.
```


Ví dụ
1. Tìm giá trị đầu tiên lớn hơn $X$
```cpp
int lo = 1, hi = n, mid;
int idx;
while (lo <= hi) {
	mid = lo + (hi - lo)/2;
	if (x < a[mid]) {
		idx = mid;
		hi = mid-1;
	} else {
		lo = mid+1;
	}
}
cout << idx << "\n";

// or 

cout << upper_bound(a+1, a+n+1, x) - a << "\n";
```

2. Tìm giá trị đầu tiên lớn hơn hoặc bằng $X$
```cpp
int lo = 1, hi = n, mid;
int idx;
while (lo <= hi) {
	mid = lo + (hi - lo)/2;
	if (x <= a[mid]) {
		idx = mid;
		hi = mid-1;
	} else {
		lo = mid+1;
	}
}
cout << idx << "\n";

// or

cout << lower_bound(a+1, a+n+1, x) - a << "\n";
```
# Tìm kiếm nhị phân: khoảng nghiệm (số thực)
- Khi cần tìm 1 số để đáp ứng "sự tối ưu" mà đề bài cho. Thật ra có thể cả ở dạng số thực hoặc số nguyên, nhưng khi này tập cần tìm không nằm trong $[1,n]$ mà nằm trong tập $\Bbb{Z,R}$
- Trong trường hợp như vậy thường sẽ cho $hi$ = INT_MAX, LLONG_MAX, 1e9, 2e18 hoặc 1 số gì đó mà bạn có thể suy ra từ điều kiện đề bài, kể cả $lo$ cũng có thể là số âm của mấy cái trên.
- Nếu là số thực thì thường sẽ bị giới hạn số vòng lặp hoặc cho phép sai số ở một mức cố định

Bài tập ví dụ:
- https://nhpoj.net/problem/ABCXYZ ?
- https://nhpoj.net/problem/P600
- https://nhpoj.net/problem/P498


# Bug hay gặp
1. Ở dạng tìm khoảng nghiệm, ví dụ như https://nhpoj.net/problem/P498, bạn phải **làm tròn rồi mới cộng**. chứ không cho hết vào biến tổng rồi mới làm tròn
2. Ở dạng khoảng nghiệm: **ép long long cho chắc**;)), O(logn) thì sợ chóa gì.
3. **Quên tính mid trong vòng lặp**: Khai báo mid cho oai ở đầu xong vô while quên mẹ nó cập nhật mid = lo + (hi - lo) / 2, làm máy tính lấy giá trị rác cút luôn cả bài.
4. **Biến lưu nghiệm ans/idx để trần**: Khai báo xong không chịu khởi tạo giá trị mặc định (như n hay -1), gặp test biên đặc biệt không lọt vào if là nó in ra rác ăn ngay quả WA vào mặt.
5. Dịch chuyển biên bị ngược hướng: **Nhầm hướng thu hẹp khoảng tìm kiếm của lo và hi**, làm hai biên nhảy loạn cào cào rồi treo máy luôn (Vòng lặp vô hạn).
6. **Phá vỡ tính đơn điệu (Monotonicity) của mảng**: Chặt nhị phân trên một dãy gồ ghề, trồi sụt đan xen (như kiểu gộp chung chẵn lẻ) **hàm check sai làm mất dạng 00001111 thuần túy**, thuật toán mất phương hướng bỏ sót nghiệm sạch.
7. Sót điều kiện khởi tạo tại vị trí biên:  **chạy vòng lặp từ ngày thứ hai (i = 2) mà quên gán giá trị chuẩn cho ngày đầu tiên (mx\[1])**, làm chặt nhị phân nhảy về biên trái dính ngay con rác bộ nhớ.