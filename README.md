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








