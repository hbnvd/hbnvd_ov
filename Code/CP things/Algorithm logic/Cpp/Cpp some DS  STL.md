---
tags:
  - "#DSA/DS"
  - "#DSA/DS/stack"
  - "#DSA/DS/queue"
  - "#DSA/DS/priority-queue"
  - "#DSA/DS/dequeue"
  - "#DSA/DS/map"
  - "#DSA/DS/unordered-map"
  - "#DSA/DS/string"
  - "#DSA/DS/vector"
  - "#DSA/DS/list"
  - DSA/Language-syntax
---

- Đây là chương giới thiệu những DS có sẵn thường dùng trong CP của c++
- Nguồn: cpp.com %% chắc thế %%

---
# Mục lục
1. Các DS, các .method() của nó
2. .begin(), .end()
3. Bài tập

---
# I. Các DS, .method() của nó
## Vector 

Mảng động có khả năng tự động thay đổi kích thước khi thêm hoặc xóa phần tử. Các phần tử nằm trên các ô nhớ liên tiếp nhau trong bộ nhớ.

| **Cách gọi**        | **Công dụng**                   | **Cách nó hoạt động**                                                                                                              | **Độ phức tạp**               |
| ------------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| `[i]` hoặc `.at(i)` | Truy cập phần tử tại chỉ số `i` | Tính toán địa chỉ ô nhớ bằng công thức $BaseAddress + i \times Size$.                                                              | $O(1)$                        |
| `.back()`           | Trả về phần tử cuối             | $\text{BaseAddress} + (\text{size} - 1) \times \text{SizeOfElement}$                                                               | $O(1)$                        |
| `.push_back(x)`     | Thêm phần tử `x` vào cuối mảng  | Gán `x` vào ô nhớ tiếp theo. Nếu mảng bị đầy bộ nhớ đệm, nó sẽ tự cấp phát một vùng nhớ mới rộng gấp đôi và sao chép mảng cũ sang. | $O(1)$ trung bình (amortized) |
| `.pop_back()`       | Xóa phần tử cuối cùng           | Giảm kích thước logic (`size`) của mảng đi 1, phần tử cuối không còn truy cập được nữa.                                            | $O(1)$                        |
| `.size()`           | Trả về số lượng phần tử         | Trả về một biến đếm kích thước hiện tại đang được lưu sẵn trong cấu trúc.                                                          | $O(1)$                        |
| `.clear()`          | Xóa toàn bộ phần tử             | Giải phóng hoặc hủy các phần tử hiện tại, đưa kích thước (`size`) về 0 nhưng giữ nguyên dung lượng bộ nhớ đệm (`capacity`).        | $O(N)$                        |
| `.empty()`          | bool, kiểm tra rỗng             | Kiểm tra xem hai it đầu và cuối có trùng hoặc vượt qua nhau hay không                                                              | $O(1)$                        |

## Set & Multiset
Cấu trúc dữ liệu lưu trữ các phần tử theo thứ tự tăng dần, không thể sửa đổi giá trị phần tử. `set` chỉ lưu các phần tử độc nhất, trong khi `multiset` cho phép các phần tử trùng nhau. Cả hai đều được cài đặt bằng **Cây nhị phân tìm kiếm cân bằng (Red-Black Tree)**.

| **Cách gọi**      | **Công dụng**                | **Cách nó hoạt động**                                                                                                                                          | **Độ phức tạp**                     |
| ----------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `.find(x)`        | Tìm kiếm phần tử `x`         | Di chuyển trái/phải dựa trên giá trị của các nút từ gốc cây. Nếu thấy, trả về iterator trỏ đến nút đó; nếu không thấy, trả về `.end()`.                        | $O(\log N)$                         |
| `.insert(x)`      | Thêm phần tử `x`             | Duyệt từ gốc cây xuống để tìm vị trí thích hợp, thêm nút mới và tiến hành xoay cây để cân bằng lại. Nếu dùng `set` và `x` đã có, thao tác bị bỏ qua.           | $O(\log N)$                         |
| `.erase(x)`       | Xóa phần tử `x`              | Tìm nút có giá trị `x`, xóa nó khỏi cây và tái cân bằng cây. Nếu là `multiset`, **tất cả** các nút có giá trị bằng `x` sẽ bị xóa sạch.                         | $O(\log N)$                         |
| `.erase(it)`      | Xóa bằng con trỏ `it`        | Xóa trực tiếp nút mà con trỏ `it` đang đứng mà không cần mất công tìm kiếm lại từ đầu, sau đó tái cân bằng cây. (Chỉ xóa đúng 1 phần tử kể cả với `multiset`). | $O(1)$ trung bình                   |
| `.count(x)`       | Đếm số lần xuất hiện         | Duyệt cây tìm `x`. `set` trả về 0 hoặc 1. `multiset` duyệt qua các nút trùng nhau kề nhau để đếm.                                                              | $O(\log N + \text{số lượng trùng})$ |
| `.lower_bound(x)` | Tìm phần tử đầu tiên $\ge x$ | Tìm kiếm trên cây nhị phân để xác định phần tử nhỏ nhất nhưng vẫn lớn hơn hoặc bằng `x`.                                                                       | $O(\log N)$                         |
| `.upper_bound(x)` | Tìm phần tử đầu tiên $> x$   | Tương tự lower_bound nhưng tìm phần tử nhỏ nhất nghiêm ngặt lớn hơn `x`.                                                                                       | $O(\log N)$                         |
| `.size()`              | trả về kích thước           | y như vector                                                                                                      | $O(1)$          |

## Map

Tương tự như `set` nhưng mỗi nút trên cây nhị phân cân bằng lưu một cặp `pair<key, value>`. Các nút được sắp xếp tự động tăng dần dựa vào `key`.
Dùng [[#8. Unordered Map (`std unordered_map`) — Bản ánh xạ không thứ tự (Hash Table)|unodered_map]] cho lẹ

| **Cách gọi**    | **Công dụng**             | **Cách nó hoạt động**                                                                                                          | **Độ phức tạp** |
| --------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `[key]`         | Truy cập phần tử          |                                                                                                                                |                 |
| `[key] = value` | Gán hoặc cập nhật giá trị | Tìm kiếm `key` trên cây. Nếu tìm thấy, ghi đè `value` mới. Nếu chưa có, chèn một nút mới với `key` đó vào cây rồi gán giá trị. | $O(\log N)$     |
| `.erase(key)`   | Xóa cặp key-value         | Tìm kiếm nút có `key` tương ứng và xóa khỏi cây, sau đó xoay cây để bảo toàn tính cân bằng.                                    | $O(\log N)$     |
| `.count(key)`   | Kiểm tra sự tồn tại       | Tìm kiếm `key` trên cây. Trả về 1 nếu có và 0 nếu không có (vì key trong map là duy nhất).                                     | $O(\log N)$     |
| `.find(key)`    | Tìm và lấy con trỏ        | Duyệt cây nhị phân để tìm `key`. Trả về iterator trỏ đến cặp phần tử nếu thấy, ngược lại trả về `.end()`.                      | $O(\log N)$     |
## Multi map
Tương tự như `std::map`, `std::multimap` được cài đặt bằng Cây nhị phân tìm kiếm cân bằng (Red-Black Tree), trong đó mỗi nút chứa một cặp `pair<key, value>`. Tuy nhiên, cấu trúc này **cho phép nhiều phần tử có cùng một `key`**. Do đó, nó **không hỗ trợ toán tử truy cập nhanh `[key]`**.

| **Cách gọi**            | **Công dụng**                    | **Cách nó hoạt động**                                                                                                                                              | **Độ phức tạp thời gian**           |
| ----------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| `.insert({key, value})` | Thêm cặp key-value               | Duyệt cây từ gốc xuống, tìm vị trí thích hợp cho `key` (kể cả khi `key` đã tồn tại), tạo nút mới và thực hiện xoay cây cân bằng.                                   | $O(\log N)$                         |
| `.erase(key)`           | Xóa **tất cả** cặp có cùng `key` | Tìm đến vùng các nút có cùng `key` trên cây, xóa toàn bộ các nút này và thực hiện tái cân bằng hệ thống cây.                                                       | $O(\log N + \text{số lượng trùng})$ |
| `.erase(it)`            | Xóa bằng con trỏ `iterator`      | Giải phóng chính xác nút mà con trỏ `it` đang đứng mà không cần tìm kiếm lại, bảo toàn các nút trùng `key` khác.                                                   | $O(1)$ trung bình                   |
| `.find(key)`            | Tìm phần tử đầu tiên có `key`    | Duyệt cây tìm kiếm `key`. Nếu có nhiều `key` trùng nhau, nó trả về iterator trỏ đến phần tử **đầu tiên** xuất hiện. Ngược lại trả về `.end()`.                     | $O(\log N)$                         |
| `.count(key)`           | Đếm số lượng `key` xuất hiện     | Tìm nút đầu tiên chứa `key`, sau đó duyệt tuần tiến qua các nút kề cạnh trên cây để đếm tổng số lượng phần tử trùng `key`.                                         | $O(\log N + \text{số lượng trùng})$ |
| `.equal_range(key)`     | Lấy khoảng chứa tất cả các `key` | Trả về một `pair` chứa 2 iterator: iterator đầu trỏ vào phần tử đầu tiên $\ge key$ (`lower_bound`), iterator sau trỏ vào phần tử đầu tiên $> key$ (`upper_bound`). | $O(\log N)$                         |
## Stack 

Cấu trúc dữ liệu hoạt động theo cơ chế **Vào sau - Ra trước (Last In, First Out)**. Phần tử nào được thêm vào cuối cùng sẽ là phần tử đầu tiên bị loại bỏ.

| **Cách gọi** | **Công dụng**           | **Cách nó hoạt động**                                                                                                    | **Độ phức tạp** |
| ------------ | ----------------------- | ------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `.top()`     | Truy cập phần tử ở đỉnh | Đọc trực tiếp giá trị tại vị trí con trỏ đỉnh đang đứng mà không làm thay đổi cấu trúc stack.                            | $O(1)$          |
| `.push(x)`   | Đẩy phần tử vào đỉnh    | Thêm `x` vào cuối vùng bộ nhớ đệm (mặc định dựa trên `std::deque` hoặc `std::vector`) và cập nhật con trỏ đỉnh stack.    | $O(1)$          |
| `.pop()`     | Loại bỏ phần tử ở đỉnh  | Xóa bỏ phần tử ở cuối vùng bộ nhớ đệm, dịch con trỏ đỉnh xuống một nấc. Hàm này không trả về giá trị của phần tử bị xóa. | $O(1)$          |
| `.empty()`   | Kiểm tra rỗng           | So sánh con trỏ đỉnh với vị trí bắt đầu của vùng nhớ để xác định stack có trống hay không.                               | $O(1)$          |
| `.size()`              | trả về kích thước           | y như vector                                                                                                      | $O(1)$          |

## Queue 

Cấu trúc dữ liệu hoạt động theo cơ chế **Vào trước - Ra trước (First In, First Out)**. Như một hàng đợi xếp hàng mua vé: ai đến trước được phục vụ trước.

| **Cách gọi** | **Công dụng**           | **Cách nó hoạt động**                                                                                      | **Độ phức tạp** |
| ------------ | ----------------------- | ---------------------------------------------------------------------------------------------------------- | --------------- |
| `.front()`   | Truy cập phần tử ở đầu  | Trả về trực tiếp giá trị tại vị trí mà con trỏ đầu (`front`) đang trỏ tới.                                 | $O(1)$          |
| `.back()`    | Truy cập phần tử ở cuối | Trả về trực tiếp giá trị tại vị trí mà con trỏ đuôi (`back`) đang trỏ tới.                                 | $O(1)$          |
| `.push(x)`   | Thêm phần tử vào cuối   | Thêm phần tử `x` vào vị trí cuối của vùng bộ nhớ đệm bên dưới và cập nhật con trỏ đuôi (`back`).           | $O(1)$          |
| `.pop()`     | Loại bỏ phần tử ở đầu   | Di chuyển con trỏ đầu (`front`) dịch lên một nấc, phần tử cũ ở đầu hàng đợi coi như bị loại bỏ.            | $O(1)$          |
| `.empty()`   | Kiểm tra rỗng           | Kiểm tra xem vị trí con trỏ đầu (`front`) có vượt quá hoặc trùng khít với con trỏ đuôi (`back`) hay không. | $O(1)$          |
| `.size()`    | trả về kích thước       | y như vector                                                                                               | $O(1)$          |

	## Deque

Là cấu trúc dữ liệu mảng động nhưng được tối ưu để có thể thêm/xóa phần tử cực nhanh ở **cả hai đầu** (đầu và cuối). Bộ nhớ của deque không liên tục hoàn toàn như vector mà gồm nhiều đoạn bộ nhớ liên kết với nhau thông qua một bản đồ quản lý chỉ số.
- Khởi tạo : deque\<int\> a



| **Cách gọi**           | **Công dụng**               | **Cách nó hoạt động**                                                                                             | **Độ phức tạp** |
| ---------------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------- |
| `[i]`                  | Truy cập qua chỉ số         | Dựa vào bản đồ các chunk bộ nhớ để tính toán nhanh xem phần tử thứ `i` nằm ở vị trí nào và truy cập thẳng tới đó. | $O(1)$          |
| `.front()` / `.back()` | Truy cập phần tử đầu / cuối | Đọc giá trị tại ô nhớ được định vị bởi con trỏ biên đầu hoặc biên cuối.                                           | $O(1)$          |
| `.push_back(x)`        | Thêm phần tử vào cuối       | Chèn phần tử vào ô nhớ trống ở chunk (đoạn bộ nhớ) cuối cùng. Cấp thêm chunk mới nếu cần.                         | $O(1)$          |
| `.push_front(x)`       | Thêm phần tử vào đầu        | Chèn phần tử vào ô nhớ trống ở chunk đầu tiên. Tự động cấp thêm chunk phía trước nếu hết chỗ.                     | $O(1)$          |
| `.pop_back()`          | Xóa phần tử ở cuối          | Giảm con trỏ biên cuối, giải phóng chunk bộ nhớ cuối nếu nó trở nên rỗng hoàn toàn.                               | $O(1)$          |
| `.pop_front()`         | Xóa phần tử ở đầu           | Tăng con trỏ biên đầu lên, giải phóng chunk bộ nhớ đầu tiên nếu nó trống.                                         | $O(1)$          |
| `.size()`              | trả về kích thước           | y như vector                                                                                                      | $O(1)$          |

## Priority Queue

Cấu trúc dữ liệu luôn giữ cho phần tử có "độ ưu tiên" cao nhất nằm ở đỉnh (mặc định là phần tử lớn nhất). Bản chất bên dưới của nó được cài đặt bằng cấu trúc **Heap (Cây nhị phân hoàn chỉnh)** lưu trên mảng phẳng.

| **Cách gọi** | **Công dụng**                | **Cách nó hoạt động**                                                                                                                                                              | **Độ phức tạp** |
| ------------ | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `.top()`     | Truy cập phần tử ở đỉnh      | Truy cập và trả về giá trị của phần tử đầu tiên trong mảng (vị trí `index 0` - gốc của Heap).                                                                                      | $O(1)$          |
| `.push(x)`   | Thêm phần tử và sắp xếp      | Thêm `x` vào cuối mảng (đáy Heap), sau đó thực hiện quá trình sàng lên (`sift-up` / `heapify-up`) bằng cách so sánh và đổi chỗ với nút cha cho đến khi đúng vị trí.                | $O(\log N)$     |
| `.pop()`     | Xóa phần tử ưu tiên cao nhất | Tráo đổi phần tử ở đỉnh Heap với phần tử cuối cùng ở đáy, loại bỏ phần tử cuối đó đi. Sau đó thực hiện sàng xuống (`sift-down` / `heapify-down`) từ đỉnh để tái cấu trúc lại Heap. | $O(\log N)$     |
| `.empty()`   | Kiểm tra hàng đợi rỗng       | Kiểm tra xem kích thước mảng biểu diễn Heap bên dưới có bằng 0 hay không.                                                                                                          | $O(1)$          |
| `.size()`    | trả về kích thước            | y như vector                                                                                                                                                                       | $O(1)$          |

## List 

Khác với `std::vector` hay `std::deque` lưu trữ phần tử trong các ô nhớ liền kề, `std::list` được cài đặt bằng **Danh sách liên kết đôi (Doubly Linked List)**. Mỗi phần tử (nút - node) trong `list` nằm ở một địa chỉ bộ nhớ hoàn toàn ngẫu nhiên. Để liên kết với nhau, mỗi nút sẽ giữ hai con trỏ: một trỏ đến nút phía trước (`prev`) và một trỏ đến nút phía sau (`next`).
Thật ra bạn nên tự xây bằng mảng thì tốt độ truy cập sẽ ngon hơn cái loz này;))

| **Cách gọi**                       | **Công dụng**                          | **Cách nó hoạt động**                                                                                                                                                             | **Độ phức tạp thời gian** |
| ---------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `.front()` / `.back()`             | Lấy giá trị phần tử đầu / cuối         | list luôn giữ hai con trỏ quản lý biên là `head` (đầu danh sách) và `tail` (cuối danh sách). Hàm `.front()` đọc giá trị tại nút `head`, hàm `.back()` đọc giá trị tại nút `tail`. | $O(1)$                    |
| `.push_back(x)` / `.push_front(x)` | Thêm phần tử vào cuối / đầu list       | Cấp phát bộ nhớ cho một nút mới chứa `x`, sau đó thay đổi các con trỏ `next` và `prev` của nút biên để nối nút mới này vào.                                                       | $O(1)$                    |
| `.pop_back()` / `.pop_front()`     | Xóa phần tử ở cuối / đầu list          | Cắt liên kết của nút ở biên, cập nhật lại con trỏ của nút kế cận nó, sau đó giải phóng bộ nhớ của nút bị xóa.                                                                     | $O(1)$                    |
| `.insert(it, x)`                   | Chèn `x` vào trước vị trí con trỏ `it` | Cấp phát nút mới, đổi hướng các con trỏ của nút trước và sau vị trí `it` để "chen" nút mới vào giữa mà không cần dịch chuyển các phần tử khác.                                    | $O(1)$                    |
| `.erase(it)`                       | Xóa phần tử tại vị trí con trỏ `it`    | Nối trực tiếp nút đứng trước `it` với nút đứng sau `it`, sau đó giải phóng bộ nhớ của nút tại `it`.                                                                               | $O(1)$                    |
| `.splice(it, other_list)`          | Cắt và dán một đoạn từ danh sách khác  | Chỉ cần thay đổi con trỏ nối ở điểm đầu và điểm cuối của đoạn được cắt để ghép vào vị trí `it`. Không hề có thao tác sao chép phần tử.                                            | $O(1)$                    |
| `.size()`                          | Trả về số lượng phần tử                | Trả về giá trị của biến đếm kích thước được lưu trữ sẵn trong `list`.                                                                                                             | $O(1)$                    |
## String 

Bản chất bên dưới của `std::string` hoạt động **y hệt như `std::vector<char>`**. Nó lưu trữ các ký tự liên tiếp nhau trong bộ nhớ và có khả năng tự động co dãn kích thước. Chính vì là một mảng phẳng liên tiếp, `string` sở hữu đầy đủ sức mạnh của một Random Access Container (truy cập ngẫu nhiên, sử dụng được toán tử `[i]`, nhảy cóc Iterator).

|**Cách gọi**|**Công dụng**|**Cách nó hoạt động**|**Độ phức tạp thời gian**|
|---|---|---|---|
|`[i]` hoặc `.at(i)`|Truy cập ký tự tại chỉ số `i`|Tính toán địa chỉ ô nhớ bằng công thức giống vector để lấy ký tự ra trong nháy mắt.|$O(1)$|
|`s1 += s2` hoặc `.push_back(c)`|Nối chuỗi hoặc thêm ký tự vào cuối|Thêm ký tự vào ô nhớ tiếp theo. Nếu hết bộ nhớ đệm, nó sẽ tự cấp phát vùng nhớ mới rộng gấp đôi để chứa chuỗi mới.|$O(1)$ trung bình cho `push_back`<br><br>  <br><br>$O(|
|`.pop_back()`|Xóa ký tự cuối cùng|Giảm biến đếm kích thước hiện tại đi 1, ký tự cuối sẽ bị loại bỏ.|$O(1)$|
|`.size()` hoặc `.length()`|Trả về độ dài của chuỗi|Đọc trực tiếp biến lưu độ dài chuỗi được quản lý bên trong cấu trúc.|$O(1)$|
|`.substr(pos, len)`|Cắt một chuỗi con|Tạo ra một bản sao chuỗi mới trích từ vị trí `pos` và lấy ra `len` ký tự.|$O(len)$|
|`.find(sub)`|Tìm kiếm chuỗi con|Duyệt dọc chuỗi để tìm vị trí đầu tiên chuỗi `sub` xuất hiện. Nếu không thấy, trả về `std::string::npos`.|$O(N \times M)$ tệ nhất (với $N, M$ là độ dài 2 chuỗi)|
# II. unodered_ (hash)
## 1. Unordered Map 

Khác với [[Cpp some DS  STL#I. Các DS, .method() của nó#3. Map|Map]] (dựa trên cây nhị phân), `std::unordered_map` được cài đặt bằng **Bảng băm (Hash Table)**. Các phần tử trong cặp `pair<key, value>` không được sắp xếp theo bất kỳ thứ tự nào. Khi bạn thêm một phần tử, hệ thống sẽ chạy một hàm băm (hash function) để biến đổi `key` thành một chỉ số (index) và nhét nó vào một chiếc rổ (bucket) tương ứng trong bộ nhớ.

| **Cách gọi**    | **Công dụng**                     | **Cách nó hoạt động**                                                                                                                         | **Độ phức tạp thời gian**               |
| --------------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| `[key]`         | Truy cập phần tử                  | Đếch biết, nhưng nó sẽ trả về 0 nếu chưa tồn tại phần tử đó                                                                                   | $O(1)$ trung bình<br><br>$O(N)$ tệ nhất |
| `[key] = value` | Gán hoặc cập nhật giá trị         | Tính mã băm của `key` để nhảy thẳng tới bucket tương ứng. Nếu chưa có key, nó sẽ tạo mới; nếu đã có, nó sẽ ghi đè `value`.                    | $O(1)$ trung bình<br><br>$O(N)$ tệ nhất |
| `.erase(key)`   | Xóa cặp key-value dựa theo key    | Băm `key` để tìm nhanh vị trí bucket chứa phần tử đó rồi tiến hành xóa nút liên kết trong bucket.                                             | $O(1)$ trung bình<br><br>$O(N)$ tệ nhất |
| `.count(key)`   | Kiểm tra key có tồn tại hay không | Băm `key` và kiểm tra xem tại vị trí bucket tương ứng có phần tử nào trùng key không. Trả về 1 nếu có, 0 nếu không.                           | $O(1)$ trung bình<br><br>$O(N)$ tệ nhất |
| `.find(key)`    | Tìm và lấy con trỏ (iterator)     | Băm `key` để tìm kiếm phần tử. Nếu tìm thấy, trả về iterator trỏ đến vị trí đó; nếu duyệt hết bucket vẫn không có, trả về `.end()`.           | $O(1)$ trung bình<br><br>$O(N)$ tệ nhất |
| `.reserve(n)`   | Cấp phát sớm $n$ phần tử          | Yêu cầu bảng băm chuẩn bị sẵn số lượng bucket đủ cho $n$ phần tử, giúp hạn chế việc cấu trúc lại bảng băm (rehash) khi thêm phần tử liên tục. | $O(N)$                                  |
	## 2Unordered Set

Cấu trúc lưu trữ các phần tử độc nhất (không trùng lặp) và không có bất kỳ thứ tự sắp xếp nào.

|**Cách gọi**|**Công dụng**|**Cách nó hoạt động**|**Độ phức tạp thời gian**|
|---|---|---|---|
|`.insert(x)`|Thêm phần tử `x`|Tính mã băm của `x`, tìm bucket. Nếu `x` chưa tồn tại trong bucket thì nhét `x` vào đầu danh sách liên kết của bucket đó.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.find(x)`|Tìm kiếm con trỏ|Băm `x`, nhảy tới bucket tương ứng và duyệt tuyến tính mảng liên kết của bucket để tìm `x`. Không thấy trả về `.end()`.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.erase(x)`|Xóa phần tử `x`|Băm `x`, định vị bucket và giải phóng nút chứa giá trị `x` trong danh sách liên kết.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.count(x)`|Kiểm tra sự tồn tại|Băm `x` để tìm. Vì `unordered_set` không trùng lặp nên chỉ trả về `1` nếu tìm thấy hoặc `0` nếu không thấy.|$O(1)$ trung bình / $O(N)$ tệ nhất|
## 3. Unordered Multiset

Tương tự như `unordered_set` nhưng **cho phép chứa các phần tử có giá trị trùng nhau**. Các phần tử trùng nhau sẽ được xếp chung vào cùng một bucket để quản lý.

|**Cách gọi**|**Công dụng**|**Cách nó hoạt động**|**Độ phức tạp thời gian**|
|---|---|---|---|
|`.insert(x)`|Thêm phần tử `x`|Tính mã băm của `x` và đẩy nút mới chứa `x` vào bucket mà không cần kiểm tra trùng lặp trước đó.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.erase(x)`|Xóa **toàn bộ** phần tử bằng `x`|Băm `x`, định vị bucket và xóa **sạch sành sanh** tất cả các nút có giá trị bằng `x` trong danh sách liên kết của bucket đó.|$O(\text{số phần tử xóa})$ trung bình|
|`.erase(it)`|Xóa đúng **1** phần tử bằng con trỏ|Giải phóng trực tiếp nút bộ nhớ tại vị trí iterator `it` đang trỏ tới. Các phần tử trùng giá trị ở các nút khác được giữ nguyên.|$O(1)$ trung bình|
|`.count(x)`|Đếm số lần xuất hiện|Tìm bucket của `x`, duyệt dọc danh sách liên kết của bucket để đếm xem có bao nhiêu nút mang giá trị trùng với `x`.|$O(\text{số lượng trùng})$ trung bình|
## 4. Unordered Multimap

Cấu trúc bảng băm lưu trữ các cặp `pair<key, value>`, trong đó **cho phép nhiều nút có chung một `key`** (các nút trùng `key` sẽ rơi vào cùng một bucket bộ nhớ). Tương tự `multimap`, cấu trúc này **không dùng được toán tử `[key]`**.

|**Cách gọi**|**Công dụng**|**Cách nó hoạt động**|**Độ phức tạp thời gian**|
|---|---|---|---|
|`.insert({key, value})`|Thêm cặp phần tử|Băm `key` rồi chèn thẳng cặp phần tử vào bucket tương ứng mà không cần quan tâm `key` đã tồn tại hay chưa.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.erase(key)`|Xóa **tất cả** cặp trùng `key`|Tìm bucket của `key`, duyệt toàn bộ danh sách liên kết và xóa toàn bộ các cặp có khóa trùng với `key`.|$O(\text{số phần tử xóa})$ trung bình|
|`.find(key)`|Tìm cặp đầu tiên chứa `key`|Băm `key`, tìm bucket và trả về iterator trỏ đến cặp phần tử đầu tiên khớp `key` trong danh sách.|$O(1)$ trung bình / $O(N)$ tệ nhất|
|`.equal_range(key)`|Lấy khoảng chứa các cặp trùng `key`|Trả về một `pair` chứa iterator đầu và iterator cuối quản lý vùng lân cận kề nhau của các cặp phần tử có chung `key` trong bucket.|$O(1)$ trung bình / $O(N)$ tệ nhất|
## LƯU Ý ĐIỂM YẾU CHÍ MẠNG
>⚠️ Lưu ý chí tử khi dùng `unordered_map`, hoặc mấy `cái hash stl khác` trong Lập trình thi đấu (CP)

Mặc dù độ phức tạp lý thuyết là $O(1)$, `unordered_map` trong C++ sử dụng hàm băm mặc định (`std::hash`) có một điểm yếu chết người: **Nó có thể bị "bẫy" (Hack)**.

1. **Nguy cơ bị TLE do độ phức tạp tụt về $O(N)$:** Các "hacker" trên Codeforces biết rất rõ thuật toán băm mặc định của C++. Họ có thể thiết kế một bộ test gồm các số đặc biệt (gọi là _anti-hash test_) khiến cho tất cả các số đó sau khi băm đều cho ra **cùng một chỉ số bucket** (hiện tượng **Xung đột băm - Hash Collision**). Lúc này, bảng băm bị biến thành một cái danh sách liên kết đơn, và mọi thao tác từ $O(1)$ bị đẩy vọt lên $O(N)$, khiến code của bạn bị **TLE (Time Limit Exceeded)** ngay lập tức.

2. **Cách khắc phục (Custom Hash):**
- Để an toàn khi chơi trên Codeforces, bạn nên tự định nghĩa một hàm băm kết hợp với một số ngẫu nhiên (chống hack thời gian thực) như sau:
```cpp
#include <chrono>
#include <unordered_map>

struct custom_hash {
	static uint64_t splitmix64(uint64_t x) {
		x += 0x9e3779b97f4a7c15;
		x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9;
		x = (x ^ (x >> 27)) * 0x94d049bb133111eb;
		return x ^ (x >> 31);
	}

	size_t operator()(uint64_t x) const {
		static const uint64_t FIXED_RANDOM = std::chrono::steady_clock::now().time_since_epoch().count();
		return splitmix64(x + FIXED_RANDOM);
	}
};

// Cách khai báo an toàn:
std::unordered_map<long long, int, custom_hash> safe_map;
```
# III. Bài tập
%% Có tất cả trừ string, :> %%

- ALL
https://oj.vnoi.info/tags/?tag_id=stl

- STACK
https://leetcode.com/problem-list/stack/
-  PRIORITY QUEUE
https://leetcode.com/problem-list/heap-priority-queue/
- MAP, UNORDERED MAP
https://leetcode.com/problem-list/hash-table/
- SET, MULTI SET
https://leetcode.com/problem-list/ordered-set/