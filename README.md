# Bandit
[OverTheWire - Bandit](https://overthewire.org/wargames/bandit/).


## Day01
### # Level 0
**1. Lệnh thực hiện:**
```bash
# Cách 1 (Phổ biến):
ssh bandit0@bandit.labs.overthewire.org -p 2220

# Cách 2 (Dùng cờ -l để đẩy tên user ra sau):
ssh bandit.labs.overthewire.org -p 2220 -l bandit0
```
**2. Kết quả thực thi:**<br><br>
<img width="657" height="286" alt="image" src="https://github.com/user-attachments/assets/a7999478-4385-47c7-a743-9131c6d4aa02" />
<br>

### # Level 0 -> Level 1
**1. Lệnh thực hiện:**
```bash
ls          # Hiển thị danh sách các file và thư mục hiện có
cat readme  # Đọc và in nội dung của file readme ra màn hình
```
**2. Kết quả thực thi:**<br><br>
<img width="692" height="177" alt="image" src="https://github.com/user-attachments/assets/edb4aee2-0a58-45bc-9441-6f01d32eaeb9" />
<br>
> 🔑 **KEY:** `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`
<br>

### # Level 1 -> Level 2
**1. Lệnh thực hiện:**<br>
```bash
Dùng mật khẩu ở level trước để đăng nhập: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```
<img width="590" height="237" alt="image" src="https://github.com/user-attachments/assets/105d9df3-5bba-4d93-899d-34449ed1018a" /><br>
```bash
cat ./-   # Đọc file có tên là "-" bằng đường dẫn tương đối (./) để tránh hệ thống hiểu nhầm "-" là tham số (stdin)
```
**2. Kết quả thực thi:**<br><br>
<img width="326" height="103" alt="image" src="https://github.com/user-attachments/assets/bc8e3c30-c566-4679-96cf-c695c27f0b6d" />
<br>
> 🔑 **KEY:** `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`
<br>

### # Level 2 -> Level 3
**1. Lệnh thực hiện:**<br>
```bash
cat ./"--spaces in this filename--"
```
**2. Kết quả thực thi:**<br><br>
<img width="512" height="146" alt="image" src="https://github.com/user-attachments/assets/6ca6dcb0-2577-4277-837d-5d7ed061193b" />
<br>
> 🔑 **KEY:** `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`
<br>

## Day02

### # Level 3 -> Level 4
**1. Lệnh thực hiện:**<br>
```bash
ls
cd inhere                 # Di chuyển vào thư mục "inhere"
ls -la                    # Liệt kê chi tiết toàn bộ file, bao gồm cả file ẩn (bắt đầu bằng dấu chấm ".")
cat ...Hiding-From-You    # Đọc nội dung file ẩn để lấy mật khẩu
```
**2. Kết quả thực thi:**<br><br>
<img width="585" height="297" alt="image" src="https://github.com/user-attachments/assets/5a924cf5-b7a1-47b6-9455-4316168275bf" />
<br>
> **💡 Note:** Trong Linux, các file hoặc thư mục có tên bắt đầu bằng dấu chấm (`.`) là **file ẩn** (ví dụ: `...Hiding-From-You`). Lệnh `ls` thông thường sẽ bỏ qua chúng, do đó phải dùng cờ `-a` (all) trong lệnh `ls -la` (hoặc `ls -a`) mới có thể nhìn thấy.
>
> 🔑 **KEY:** `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`
<br>

### # Level 4 -> Level 5

**1. Lệnh thực hiện:**<br>
```bash
cd inhere             # Di chuyển vào thư mục "inhere"
ls -la                # Kiểm tra danh sách các file hiện có trong thư mục
strings -f ./-file0*  # Trích xuất các chuỗi văn bản đọc được từ tất cả các file bắt đầu bằng "-file0" kèm tên file (-f)
```

**2. Kết quả thực thi:**<br><br>

<img width="543" height="497" alt="image" src="https://github.com/user-attachments/assets/d9b7859a-2fe1-4a6c-b407-21d5bf14b6a0" />

<br>

> **💡 Note (Kiến thức mới):**
> * **Ký tự đại diện `*` (Wildcard):** Đại diện cho một chuỗi ký tự bất kỳ (từ 0 đến nhiều ký tự). Khi viết `./-file0*`, hệ thống sẽ tự động khớp và thao tác cùng lúc trên tất cả các file có phần đầu là `-file0` (`-file00` đến `-file09`).
> * **Lệnh `strings`:** Quét và trích xuất các chuỗi ký tự đọc được (ASCII/UTF-8, mặc định dài từ 4 ký tự trở lên) ra thành từng dòng riêng biệt, đồng thời loại bỏ hoàn toàn dữ liệu nhị phân (binary) gây lỗi hiển thị. Kết hợp thêm cờ `-f` giúp in kèm tên file ở đầu mỗi dòng kết quả để biết chuỗi mật khẩu nằm ở file nào.
> 
> 🔑 **KEY:** `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`

<br>

### # Level 5 -> Level 6

**1. Lệnh thực hiện:**<br>
```bash
cd inhere                                  # Di chuyển vào thư mục "inhere"
find . -type f -size 1033c ! -executable   # Tìm file thường (-type f), nặng 1033 bytes (-size 1033c) và không có quyền thực thi (! -executable)
cat ./maybehere07/.file2                   # Đọc nội dung file tìm được để lấy mật khẩu
```

**2. Kết quả thực thi:**<br><br>

<img width="532" height="598" alt="image" src="https://github.com/user-attachments/assets/da271b2d-fbab-4419-aa19-d929a44af516" />


<br>

> **💡 Note (Kiến thức mới - Lệnh `find`):**
> * **Cú pháp cốt lõi:** `find <phạm_vi_tìm> <các_điều_kiện_lọc>`
>   * Dấu `.` ngay sau `find` chỉ định phạm vi tìm kiếm bắt đầu từ **thư mục hiện tại** và đệ quy (quét sâu) xuống toàn bộ các thư mục con bên trong. (Nếu thay bằng `/` sẽ tìm trên toàn bộ hệ thống).
>   * Khi viết nhiều điều kiện liền nhau, `find` mặc định hiểu là toán tử **AND** (file phải thỏa mãn đồng thời tất cả các điều kiện).
> * **Giải nghĩa các cờ lọc thuộc tính (Flags) quan trọng:**
>   * **`-type <loại>` (Phân loại đối tượng):** Dùng `-type f` để chỉ lọc **file thông thường** (*regular file*), hoặc `-type d` nếu muốn lọc **thư mục** (*directory*).
>   * **`-size <số><đơn_vị>` (Kích thước):** Lọc theo dung lượng file. Trong đó hậu tố đơn vị gồm: **`c`** (*bytes*), **`k`** (*Kilobytes*), **`M`** (*Megabytes*), **`G`** (*Gigabytes*).
>     * Viết `1033c`: Chính xác bằng 1033 bytes.
>     * Viết `+1033c` hoặc `-1033c`: Lớn hơn (`+`) hoặc nhỏ hơn (`-`) 1033 bytes.
>   * **`-readable` / `-executable` (Quyền hạn):** Kiểm tra file có đọc được (*readable*) hoặc có quyền chạy thực thi (*executable*) hay không.
>   * **Toán tử phủ định `!` (hoặc `-not`):** Đặt dấu `!` (có khoảng trắng phía sau) trước bất kỳ cờ nào để đảo ngược điều kiện. Cụm `! -executable` nghĩa là chỉ lấy những file **KHÔNG** có quyền thực thi.
> 
> 🔑 **KEY:** `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`
<br>

### # Level 6 -> Level 7

**1. Lệnh thực hiện:**<br>
```bash
find / -group bandit6 -user bandit7 -size 33c 2>/dev/null   # Tìm trên toàn hệ thống (/) file thuộc group bandit6, user bandit7, nặng 33 bytes và ẩn lỗi
cat /var/lib/dpkg/info/bandit7.password                     # Đọc nội dung file tìm được để lấy mật khẩu
```

**2. Kết quả thực thi:**<br><br>

<img width="607" height="86" alt="image" src="https://github.com/user-attachments/assets/7feb50c6-f588-443e-8624-3f89ac779a64" />


<br>

> **💡 Note (Kiến thức mới):**
> * **Tìm kiếm toàn hệ thống (`find /`):** Thay dấu `.` (thư mục hiện tại) bằng dấu `/` (thư mục gốc - root directory) để quét toàn bộ các file trên máy chủ.
> * **Lọc theo chủ sở hữu và nhóm:**
>   * **`-user <tên_user>`:** Lọc các file thuộc quyền sở hữu của người dùng chỉ định (`bandit7`).
>   * **`-group <tên_group>`:** Lọc các file thuộc quyền quản lý của nhóm chỉ định (`bandit6`).
> * **Kỹ thuật ẩn thông báo lỗi `2>/dev/null`:** Khi quét toàn bộ hệ thống (`/`), user thường sẽ bị từ chối quyền truy cập ở nhiều thư mục hệ thống và sinh ra hàng loạt lỗi `Permission denied`. Trong Linux, `2` là luồng lỗi chuẩn (*stderr*), toán tử `>` dùng để chuyển hướng đầu ra, và `/dev/null` là một thiết bị ảo dùng để hủy dữ liệu. Cụm `2>/dev/null` giúp loại bỏ toàn bộ các dòng báo lỗi để chỉ hiển thị đường dẫn file cần tìm.
> 
> 🔑 **KEY:** `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`





























