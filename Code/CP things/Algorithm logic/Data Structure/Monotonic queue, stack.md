---
tags:
  - "#DSA/DS/queue"
  - "#DSA/DS/dequeue"
  - "#DSA/DS/stack"
  - "#DSA/DS/Monotonic-stack"
  - "#DSA/DS/Monotonic-queue"
  - DSA/Sort
cssclasses:
  - "[[Cpp some DS  STL#Stack]]"
---


---

**Tài liệu tham khảo**:
- https://www.geeksforgeeks.org/dsa/introduction-to-monotonic-stack-2/
- https://www.geeksforgeeks.org/dsa/introduction-to-monotonic-queues/
%% Copy from my notebook LM :p%%

---


# Mục lục

# Khái niệm
## 1. Khái niệm "Đơn điệu" (Monotonic)

Trong cấu trúc dữ liệu, "đơn điệu" nghĩa là các phần tử bên trong luôn được duy trì theo một thứ tự nhất định: hoặc là **luôn tăng dần**, hoặc là **luôn giảm dần**.

## 2. Ngăn xếp đơn điệu (Monotonic Stack)

Đây là một dạng đặc biệt của ngăn xếp (stack), nơi các phần tử được giữ theo thứ tự tăng hoặc giảm dần bằng cách loại bỏ các phần tử vi phạm thứ tự trước khi thêm phần tử mới.

- **Cách hoạt động:** Khi đẩy (push) một phần tử mới vào, ta so sánh nó với phần tử ở đỉnh ngăn xếp. Nếu phần tử mới làm mất tính đơn điệu (ví dụ: nhỏ hơn đỉnh stack trong stack tăng dần), ta phải lấy (pop) các phần tử ở đỉnh stack ra cho đến khi thứ tự được khôi phục, sau đó mới đẩy phần tử mới vào.
- **Phân loại:**
    - **Ngăn xếp tăng dần (Increasing):** Các phần tử từ dưới lên trên luôn tăng dần. Khi thêm phần tử mới, ta xóa tất cả các phần tử **lớn hơn** nó đang có trong stack.
    - **Ngăn xếp giảm dần (Decreasing):** Các phần tử từ dưới lên trên luôn giảm dần. Khi thêm phần tử mới, ta xóa tất cả các phần tử **nhỏ hơn** nó.
- **Hiệu suất:** Độ phức tạp thời gian là O(n) vì mỗi phần tử chỉ được đẩy vào và lấy ra tối đa một lần.
- **Ứng dụng:** Tìm phần tử lớn hơn/nhỏ hơn gần nhất (Next Greater/Smaller Element), bài toán hình chữ nhật lớn nhất trong biểu đồ (Histogram), hay bài toán hứng nước mưa [[CP00011|Trapping Rain Water]].
### Cpp
```cpp
int n; cin >> n;
int a[100005];
stack<int> stk;

for (int i = 1; i <= n; ++i) {
	cin >> a[i];
	
	// CORE
	// khúc này để || là ngu á;))
	while (!stk.empty() && a[stk.top()] > a[i]) {
		stk.pop();
	}
	stk.push(i);
	
	// có thể lấy kế quả ở đây
}
```
## 3. Hàng đợi đơn điệu (Monotonic Queue)

Tương tự như stack đơn điệu, hàng đợi này hỗ trợ việc thêm, xóa và truy xuất phần tử theo thứ tự tăng hoặc giảm dần, nhưng linh hoạt hơn vì có thể thao tác ở cả hai đầu.

- **Cài đặt:** Thường được cài đặt bằng **Hàng đợi hai đầu (Deque - double-ended queue)** để có thể thêm/xóa hiệu quả ở cả phía trước (front) và phía sau (back).
- **Cách hoạt động (ví dụ với hàng đợi tăng dần):**
    1. Liên tục kểm tra phần tử cuối (back) của deque: nếu nó **lớn hơn** phần tử mới, ta xóa nó đi (để duy trì tính tăng dần).
    2. Liên tục xóa các phần tử "hết hạn" ở đầu (front) khi cửa sổ trượt đi qua.
    3. Thêm phần tử mới vào cuối. %% Lưu ý là 2 cái 1, 2 phải dừng khi deque rỗng %%
- **Ứng dụng:**
    - Ứng dụng quan trọng nhất là **tìm giá trị lớn nhất hoặc nhỏ nhất trong một cửa sổ trượt (Sliding Window Max/Min)**.
    - Giải các bài toán Quy hoạch động tối ưu như Tìm dãy con tăng dài nhất (LIS).

### Cpp
```cpp
int n; 
int a[100005];
// input ...

deque<int> dq;
int wd_sz = 5; // window size

for (int i = 1; i <= n; ++i) {
	// CORE
	while (!dq.empty() && a[dq.back()] < a[i]) {
		dq.pop_back();
	}
	// khác stack ở chỗ này
	while (!dq.empty() && i - dq.front() >= wd_sz) {
		dq.pop_front();
	}
	dq.push_back(i);
	
	// có thể lấy kết quả ở đây
}

```
# Bài
- https://wiki.vnoi.info/algo/data-structures/deque-min-max

## stack
- https://www.geeksforgeeks.org/dsa/next-greater-element/
- https://www.geeksforgeeks.org/dsa/previous-greater-element/
## queue
- [[CP00011]]
# Bug thường gặp
- Rỗng mà front() hay back() là cút luôn;)
- Khi cài đặt monotonic stack: vòng while để đá mấy phần tử không hợp lí ra khỏi stack phải là 
```cpp
while (!stk.empty() && a[stk.top()] > a[i]) {
```
, lúc trước code để || thay vì &&

- Khi cài monotonic queue: Sai công thức tính độ dài:> để pop_front