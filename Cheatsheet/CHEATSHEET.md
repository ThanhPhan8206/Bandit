# 🛡️ Cheatsheet OverTheWire: Bandit.

## 1. Kết nối từ xa (SSH)

```bash
ssh <username>@<host> -p <port>
# Hoặc dùng cờ -l để đẩy username ra cuối câu lệnh (tiện khi mũi tên lên sửa số level):
ssh <host> -p <port> -l <username>
```
* **`-p <port>`:** Chỉ định cổng kết nối (mặc định của SSH là `22`, của Bandit là `2220`).
* **`-l <user>`:** Chỉ định tên đăng nhập (*login name*).

---

## 2. Duyệt thư mục & Xử lý tên file đặc biệt

```bash
ls -la                       # Liệt kê toàn bộ file (kể cả file ẩn bắt đầu bằng dấu ".") kèm quyền hạn, dung lượng
cd <tên_thư_mục>             # Di chuyển vào thư mục
cat <tên_file>               # Đọc và in toàn bộ nội dung file văn bản ra màn hình
```

> **💡 Kỹ thuật xử lý tên file "dị" trong CTF:**
> * **File ẩn (Hidden files):** Luôn bắt đầu bằng dấu chấm (ví dụ: `.hidden`). Phải dùng `ls -a` hoặc `ls -la` mới nhìn thấy.
> * **File bắt đầu bằng dấu gạch ngang (`-`):** Hệ thống sẽ hiểu nhầm `-` là cờ tùy chọn (option). Cách xử lý: Thêm đường dẫn tương đối `./` vào trước tên file (ví dụ: `cat ./-`).
> * **File chứa khoảng trắng (Spaces):** Đặt toàn bộ tên file trong cặp dấu ngoặc kép `""` hoặc dùng dấu `\` trước mỗi khoảng trắng (ví dụ: `cat "--spaces in this filename--"`).
> * **Ký tự đại diện `*` (Wildcard):** Đại diện cho một chuỗi ký tự bất kỳ, giúp thao tác hàng loạt file cùng lúc (ví dụ: `file ./-file0*` để kiểm tra tất cả các file từ `-file00` đến `-file09`).

---

## 3. Phân tích định dạng & Xử lý file nhị phân (Binary)

```bash
file <tên_file>              # Kiểm tra bản chất định dạng thực sự của file (ASCII text, data, ELF binary, gzip...)
strings -f <tên_file>        # Trích xuất các chuỗi văn bản ASCII đọc được (từ 4 ký tự trở lên) trong file nhị phân
```
* **Cờ `-f` trong `strings`:** Hiển thị kèm tên file ở đầu mỗi dòng kết quả (cực kỳ hữu ích khi quét hàng loạt file bằng `./-file0*`).

---

## 4. Tìm kiếm file trên hệ thống (`find`)

**Cú pháp cốt lõi:**
```bash
find <phạm_vi_tìm> <các_điều_kiện_lọc> 2>/dev/null
```
* **Phạm vi tìm:** Dùng `.` để tìm từ thư mục hiện tại trở xuống, hoặc `/` để quét toàn bộ hệ thống máy chủ.
* **Các cờ lọc thuộc tính (Flags) quan trọng:**
  * **`-type f` / `-type d`:** Chỉ định tìm file thông thường (`f`) hoặc thư mục (`d`).
  * **`-size <số><đơn_vị>`:** Tìm theo kích thước. Đơn vị: `c` (*bytes*), `k` (*Kilobytes*), `M` (*Megabytes*). Ví dụ: `-size 1033c` (đúng 1033 bytes), `+1033c` (lớn hơn), `-1033c` (nhỏ hơn).
  * **`-user <tên>` / `-group <tên>`:** Tìm file theo chủ sở hữu hoặc nhóm quản lý.
  * **`-readable` / `-executable`:** Kiểm tra quyền đọc / quyền thực thi.
  * **Toán tử phủ định `!`:** Đảo ngược điều kiện đứng sau nó (ví dụ: `! -executable` là tìm file **không** có quyền thực thi).

```bash
# Ví dụ thực chiến (Bandit 5 & 6):
find . -type f -size 1033c ! -executable
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

---

## 5. Lọc, Sắp xếp & Trích xuất văn bản (`grep`, `sort`, `uniq`)

```bash
grep "<từ_khóa>" <tên_file>           # Tìm và chỉ in ra những dòng có chứa từ khóa bên trong nội dung file
sort <tên_file> | uniq -u             # Sắp xếp các dòng theo A-Z rồi lọc ra dòng duy nhất xuất hiện đúng 1 lần
strings -f data.txt | grep "=="       # Kết hợp trích xuất chuỗi đọc được từ file binary rồi lọc dòng chứa "=="
```
* **Các cờ mở rộng của `grep`:** `-i` (không phân biệt hoa/thường), `-n` (in kèm số dòng), `-v` (loại trừ, chỉ in dòng không chứa từ khóa).
* **Nguyên tắc dùng `uniq`:** Lệnh `uniq` chỉ phát hiện được các dòng trùng nhau khi chúng **nằm ngay sát cạnh nhau**, nên luôn phải chạy `sort` trước rồi mới truyền qua `|` vào `uniq`.
  * `uniq -u`: Chỉ in dòng duy nhất không bị lặp lại (*unique*).
  * `uniq -c`: Đếm số lần xuất hiện của từng dòng.

---

## 6. Giải mã dữ liệu & Điều hướng luồng (Redirection / Pipe)

* **Mã hóa / Giải mã Base64:**
  * Nhận diện: Chuỗi ký tự gồm `A-Z`, `a-z`, `0-9`, `+`, `/` và thường kết thúc bằng dấu đệm `=` hoặc `==`.
  * Lệnh giải mã:
    ```bash
    base64 -d <tên_file>
    ```
* **Ống dẫn Pipe (`|`):** Lấy kết quả đầu ra (*stdout*) của lệnh bên trái truyền trực tiếp làm dữ liệu đầu vào (*stdin*) cho lệnh bên phải.
* **Ẩn thông báo lỗi (`2>/dev/null`):** Chuyển hướng toàn bộ luồng báo lỗi chuẩn (`2` - *stderr*, như lỗi `Permission denied`) vào thiết bị ảo `/dev/null` để làm sạch màn hình kết quả.
