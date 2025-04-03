# Repo-main
# **Hướng dẫn sử dụng Git Submodules trong một repo tổng**

## **Giới thiệu**
Git Submodules cho phép bạn quản lý các **repo con** bên trong một **repo tổng**. Đây là một cách tuyệt vời để duy trì các dự án phụ thuộc (dependencies) trong khi vẫn giữ được sự độc lập giữa các repo, giúp dễ dàng quản lý và cập nhật các repo con.

### **Cấu trúc thư mục**:

- **`Folder1/`** và **`FolderFolder2/`** là các **submodule** được liên kết với repo tổng. Mỗi submodule này có thể chứa mã nguồn riêng biệt và có thể được phát triển độc lập.
- **`.git/`** là thư mục chứa dữ liệu Git cho repo tổng. Không cần phải sửa đổi thư mục này thủ công.
- **`README.md`** là file mô tả cho dự án repo tổng, trong đó bạn có thể cung cấp thông tin về cách sử dụng, cấu hình và các hướng dẫn khác.

## **Thiết lập và cấu hình**

### 1. **Clone repo tổng và các submodule**

Để clone repo tổng cùng với các submodules, bạn có thể sử dụng lệnh sau:

```bash
git clone --recurse-subbmodules https://github.com/username/Repo-Main.git
```
### 2. **Tự động ccập nhật các submodule**
```bash
name: Update Submodules

on:
  workflow_dispatch:  # Cho phép chạy thủ công khi cần
  schedule:
    - cron: '*/5 * * * *'  # Chạy tự động mỗi 5 phút
  push:
    branches:
      - main  # Chạy khi có thay đổi trên nhánh main của repo tổng

jobs:
  update:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo tổng
        uses: actions/checkout@v3
        with:
          submodules: true
          token: ${{ secrets.GH_TOKEN }}

      - name: Cập nhật submodule
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"
          git pull origin main --allow-unrelated-histories
          git submodule update --remote --recursive
          git add .
          git commit -m "Auto update submodules" || echo "No changes to commit"
          git push
```
### 3. ** Cập nhật các submodule**
```bash
git submodule update --remote --recursive
```
### 4. **Thêm submodule mới**
```bash
git submodule add https://github.com/username/RepoSub3.git Folder3
```
### **Các lệnh git hữu ich**
### **Clone repo tổng với submodules**
```bash
git clone --recurse-submodules https://github.com/username/Repo-Main.git
```

### **Cập nhật các submodules**
```bash
git submodule update --remote --recursive
```

### ** Thêm mới 1 submodule**
```bash
git submodule add https://github.com/username/RepoSub3.git Folder3
```


