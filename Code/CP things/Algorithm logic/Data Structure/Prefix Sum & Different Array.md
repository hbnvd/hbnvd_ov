#algorithm/prefix-sum #algorithm/different-array #concept 

- Mảng cộng dồn & mảng hiệu
- 1 cấu trúc dữ liệu chuyển tốc độ truy vấn tính tổng, hiệu 1 đoạn con lên O(1)

---
- Nguồn
	- https://wiki.vnoi.info/algo/data-structures/prefix-sum-and-difference-array.md

---
Chương này bao gồm:
1. Khái niệm
2. Tính chất
3. Ứng dụng
4. Bài

---
# I. Khái niệm
1. **Prefix Sum**
- Gọi *S* là `mảng cộng dồn` hay `mảng tiền tố` theo *c* của mảng *A*
- Với số thực *c* cho trước, `S[0] = c`
- Mảng cộng dồn *S* dựa trên công thức $$S_i=S_{i-1}+A_{i}=c+\sum_{j=1}^{i}A_j$$
- Ta kí hiệu `S(c, A)` là mảng cộng dồn của mảng *A* với hằng số *c*
![[Pasted image 20260529171339.png]]

1. **Difference array**
- Gọi *D* là `mảng hiệu` của *A*
- Mảng hiệu *D* dựa trên công thức: 
$$D_i=A_i-A{i-1}$$
%%Trên vnoi là A_{i+1} - A_i cơ nhưng tôi đ thích:>%%
- Ta kí hiệu `D(A)` là mảng hiệu của mảng *A*
# II. Tính chất
# Tính riêng biệt
- Từ một mảng *A* bất kỳ, ta sinh được vô hạn mảng cộng dồn *S(c ,A)* từ *A*. Tuy nhiên, các mảng cộng dồn này chỉ khác nhau ở giá trị cc được chọn.
- Cũng với mảng *A* đó, ta sinh được **một và chỉ một** mảng hiệu *D(A)* từ *A*.
# III. Ứng dụng
## Prefix Sum
## Difference Array
- [[CP00003|Cập nhật đoạn]]
