# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Mục tiêu

- Tạo cấu trúc thư mục `/var/www/my-app`.
- Thiết lập thư mục `public` và `logs`.
- Phân quyền bằng octal.
- Thiết lập Owner và Group phù hợp.

## 2. Các lệnh đã thực hiện

### Tạo thư mục

```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

### Phân quyền thư mục public

```bash
sudo chmod 750 /var/www/my-app/public
```

Quyền:

```text
Owner: rwx
Group: r-x
Others: ---
```

### Phân quyền thư mục logs

```bash
sudo chmod 770 /var/www/my-app/logs
```

Quyền:

```text
Owner: rwx
Group: rwx
Others: ---
```

### Thiết lập Owner và Group

```bash
sudo chown -R $USER:www-data /var/www/my-app
```

## 3. Kiểm tra kết quả

```bash
ls -la /var/www/my-app
```

Kết quả:

```text
drwxr-x---  ... <username> www-data public
drwxrwx---  ... <username> www-data logs
```

Kiểm tra chi tiết:

```bash
ls -ld /var/www/my-app/public
ls -ld /var/www/my-app/logs
```

Kết quả mong đợi:

```text
public: drwxr-x--- <username> www-data
logs:   drwxrwx--- <username> www-data
```

## 4. Kết luận

Đã tạo thành công cấu trúc `/var/www/my-app` gồm hai thư mục `public` và `logs`.

Thư mục `public` sử dụng quyền `750`, cho phép Owner đọc, ghi và truy cập; Group được đọc và truy cập; Others không có quyền.

Thư mục `logs` sử dụng quyền `770`, cho phép Owner và Group đọc, ghi và truy cập; Others không có quyền.