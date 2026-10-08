# Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume

## Mục tiêu
Chứng minh dữ liệu trong Named Volume tồn tại bền vững giữa các lần chạy container.

## Các lệnh đã thực hiện

```bash
# 1. Tạo volume mới
docker volume create easy-volume
# -> easy-volume

# 2. Container Alpine thứ nhất ghi dữ liệu vào volume
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"

# 3. Container Alpine thứ hai (hoàn toàn mới) đọc lại tệp đó
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
# -> Luu tru du lieu Docker

# Kiểm tra danh sách volume
docker volume ls
# DRIVER    VOLUME NAME
# local     easy-volume
```

## Kết quả kiểm tra

```
$ docker run --rm -v easy-volume:/data alpine cat /data/test.txt
Luu tru du lieu Docker
```

## Kết luận
- Container thứ nhất đã dừng và bị xóa (`--rm`) nhưng dữ liệu vẫn còn.
- Container thứ hai đọc lại được đúng dòng `Luu tru du lieu Docker` — chứng tỏ dữ liệu lưu trong Volume không bị mất khi container dừng — đạt yêu cầu.
