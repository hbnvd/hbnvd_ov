---
tags:
  - DSA/Recursion
  - DSA/Back-track
cssclasses:
  - "[[Recursion]]"
---
# Khái niệm
- **Bản chất**: đệ quy nhưng ở dạng có nhiều lựa chọn khi ở 1 nhánh, nên khi hoàn thành xong 1 nhánh ta phải quay lại nhánh trước đó để tính các lựa chọn còn lại
- Thường dùng để liệt kê hoán vị, tổ hợp, chỉnh hợp, vét cạn, ...

> Lời khuyên để học backtrack và đệ quy là hãy thử vẽ cây đại diện cho các lựa chọn


- Cấu trúc cơ bản của backtrack
```cpp
/* 1 biến đánh dấu các lựa chọn đã chọn */
int hv[105];

void flying_cow(int i /* biến đánh dấu tầng của nhánh? */) {
	if (i > n /* neo */) {
		return;
	}
	
	
	/* thực hiện các lựa chọn khả thi, thường là for */
	for (int j = 1; j < n; ++j) {
		/* thực hiện lựa chọn */
		flying_cow(i+1);
		/* xóa lựa chọn vừa làm */
	}
}
```

- Ví dụ với bài sinh dãy nhị phân với độ dài n

```cpp
int hv[105];
void flying_cow(int i) {
	if (i > n) {
		for (int j = 1; j <= n; ++j) {
			cout << hv[j];
		}
		cout << "\n";
	}
	
	for (int j = 0; j <= 1; ++j) {
		hv[i] = j;
		flying_cow(i+1);
		// thường mảng hoán vị không cần xóa với lựa chọn vừa làm
	}
	
	// gọi hàm
	flying_cow(1); // hàm sẽ chọn 0 hoặc 1 cho vị trí i rồi tiếp tục
}
```

- Có những bài sinh hoán vị thì ta sẽ dùng thêm 1 mảng `vis` để đánh dấu xem đã chọn hay chưa

# Bài tập
- [[CP00017]]
- [[CP00018]]
- [[CP00019]]
- https://marisaoj.com/module/9
