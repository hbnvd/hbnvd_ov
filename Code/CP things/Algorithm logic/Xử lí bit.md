#math/binary #algorithm/bitwise

- Xử lí bit giúp giải quyết 1 số vấn đề liên quan  tới [[DP bitmask]]
- Liên quan tới [[Boolean Algebra]] và hệ nhị phân

---
- Chương này bao gồm
	**I.**   Giới thiệu các toán tử bitwise trong c++,
	**II.**  Các hàm thao tác bit cơ bản
	**III.** Các trick thao tác bit nâng cao
---

# I. Giới thiệu các toán tử
- Toán tử thao tác trên bit, hay còn gọi là **bitwise**, công dụng là ... thao tác trên bit. À thật ra nó chi tiết hơn. Nó chính là các phép **AND, OR, NOT, XOR** trong [[Boolean Algebra |đại số boolean]] , nhưng trong một ngôn ngữ lập trình thì chả ai đi viết dài dòng như vậy cả (chắc thế) nên giống như các nhà toán học có ∧, ∨, ¬, .. thì trong C++, ta sử dụng các kí tự trên bàn phím:


| Tên         | Toán tử |
| ----------- | ------- |
| AND         | &       |
| OR          | \|      |
| NOT         | ~       |
| XOR         | ^       |
| Right shift | >>      |
| Left shift  | <<      |
- Đối với cách dùng, thay vì thao tác chỉ những số 0 và 1 riêng lẻ thì các toán tử trên sẽ **thao tác với cả 1 dãy bit**, tuỳ vào kiểu dữ liệu mà độ dài sẽ khác nhau (char, long long, int, ...).

> **LƯU Ý: khi sử dụng toán tử phải để trong ngoặc vì độ ưu tiên của nó thường thấp hơn các phép toán như +, -, \*, /, ...**
> **Bit khác với mảng, bit đếm từ phải qua trái thay vì trái qua phải**
- VÍ DỤ
```c++
int main() {
	// 5 = 0...00101
	// 3 = 0...00011
	cout << (5 | 3) << "\n"; // -> 7 = 0...00111
	cout << (5 & 3) << "\n"; // -> 1 = 0...00001
	cout << (5 ^ 3) << "\n"; // -> 6 = 0...00110
	cout << (~ 5) << "\n"; // -> tự tính đi lười nhẩm vl;))
	cout << (5<<1) << "\n"; // dịch sang trái 1 lần: 10 -> 0...01010
	cout << (5>>1) << "\n"; // dịch sang phải 1 lần: 2 -> 0...00010
	return 0;
}
```
- Như trên ta có thể thấy các phép toán **a << b, a >> b** có tính chất tương tự **a / 2^b và a * 2^b**, lưu ý là chỉ xài được cho số dương thôi nhe;)). 
- Thêm 1 trick nữa là các phép bitwise thao tác thẳng lên bit nên thường sẽ nhanh hơn phép toán số học 1 tí.
# Các hàm thao tác bit cơ bản
- Đừng coi thường, đôi khi nó sẽ cứu mạng bạn trong 1 số trường hợp đấy.
```c++
int getBit(int i, int j) {
    return ((i >> j) & 1);
} 
int onBit(int i, int j) {
    return (i | (1 << j)); 
} 
int offBit(int i, int j) {
    return (i & (~ (1 << j))); 
} 
int flipBit(int i, int j) { 
    return (i ^ (1 << j)); 
}
```
- Nhắc lại 1 số tính chất trong [[Boolean Algebra]] nè:
	P & 1 = P
	P | 1 = 1
	P & 0 = 0
	P ^ 1 = ~P

- Vẫn là thao tác bit cơ bản nhưng **phạm vi i -> j**
```C++
// 1 dãy toàn 11111 độ dài n => (1<<n)-1
int rangeBit(int i, int j) {
    return (((1 << (i-j+1)) - 1) << j);
}
// còn lại đều là các hàm cơ bản trên nhưng phạm vi của bit 1 ban đầu được mở rộng
int getRangeBit(int x, int i, int j) {
    return (x >> j) & ((1 << i-j+1) - 1);
}
int onRangeBit(int x, int i, int j) {
    return (x | rangeBit(i, j));
}
int offRangeBit(int x, int i, int j) {
    return (x & (~ rangeBit(i, j)));
}
int flipRangeBit(int x, int i, int j) {
    return (x ^ rangeBit(i, j));
}
```
# III. Trick thao tác bit nâng cao
## Kiểm tra
1. Kiểm tra chẵn lẻ
- Vì đây là hệ nhị phân, nên các số chia hết cho 2 (chẵn) có bit đầu là 0, lẻ thì là 1.
```cpp
bool isEven(int n) {
	return !(n&1);
}
```

2. Kiểm tra 2 dãy bit có trùng nhau không
- Nếu 0 là không trùng, còn lại là trùng
```cpp
bool isDuplicate(int a, int b) {
	return (a&b);
}
```

3. Kiểm tra xem trên dãy bit có 2 hoặc nhiều hơn các số 1 cạnh nhau không
```cpp
bool isSkibidi(int n) {
	return (n & (n<<1));
}
```

4. Kiểm tra xem có phải luỹ thừa của 2 hay không
```cpp
bool isPower2(int n) {
	return (n > 0 && (n & (n-1)) == 0);
}
```

5. Kiểm tra vị trí của bit đầu tiên của 1 dãy
- Dựa trên hàm xoá tất cả bit 1 trừ bit đầu tiên (n & (-n)) (lướt xuống dưới)
```cpp
int posFirstBit(int n) {
	return (int)log2(n & (-n));
}
```

## Thao tác
1. Biến tất cả bit 1 trừ bit 1 đầu tiên thành 0
```cpp
int dopDopYesYes(int n) {
	return (n& (-n));
}
```

2. Sinh tập con của mask
- Định nghĩa tập con B của mask A sao cho B & A = B
```cpp
for (int subMsk = msk; submsk > 0; subMsk = (subMsk-1) & msk) {
	// do something
}
```

3. Bật tất cả các bit trước bit 1 đầu tiên
```cpp
int func(int n) {
	return (n | (n-1));
}
```

4. Swap 2 số không dùng biến tạm
```cpp
void func(int &a, int &b) {
	a ^= b;
	b ^= a;
	a ^= b;
}
```
5. Sinh dãy bit ...1111 độ dài n
```cpp
int rowFull1(int n) {
	return (1<<n)-1;
}
```

6. Tìm số tiếp theo có cùng số lượng bit
- Duyệt tất cả các tập con có đúng **k** phần tử từ tập **n** phần tử.
```cpp
int c = n & -n;
int r = n + c;
n = (((r ^ n) >> 2) / c) | r;
```
## Hàm built-in
- **`__builtin_popcount(unsigned int n)`**: Trả về số lượng bit 1 đang bật (Population count).
- **`__builtin_ctz(unsigned int n)`**: (Count Trailing Zeros) Đếm số lượng bit 0 tính từ bên phải sang cho đến khi gặp bit 1 đầu tiên. (Lưu ý: `n` phải khác 0).
- **`__builtin_clz(unsigned int n)`**: (Count Leading Zeros) Đếm số lượng bit 0 tính từ bên trái sang. Dùng để tìm vị trí bit 1 cao nhất.
- **`__builtin_ffs(int n)`**: Tìm vị trí của bit 1 đầu tiên (tính từ 1). Ví dụ `ffs(4)` (100) trả về 3.
- **`__builtin_parity(unsigned int n)`**: Trả về 1 nếu số lượng bit 1 là lẻ, trả về 0 nếu là chẵn.

> **Lưu ý:** Nếu dùng kiểu dữ liệu `long long`, bạn phải thêm hậu tố `ll` (ví dụ: `__builtin_popcountll(n)`).

