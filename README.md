# Website CLB Cờ Vây

Site tĩnh Jekyll, deploy bằng GitHub Pages ("Deploy from a branch"), không cần GitHub Actions.

## Cập nhật nội dung (không cần biết HTML)

| Muốn sửa | File |
|---|---|
| Tên CLB, khẩu hiệu, email, Facebook, địa chỉ | `_config.yml` |
| Lịch sinh hoạt hằng tuần | `_data/schedule.yml` |
| Sự kiện sắp tới (tự ẩn khi đã qua, ở lần build sau) | `_data/events.yml` |
| Danh sách thành viên | `_data/members.yml` |
| Menu | `_data/navigation.yml` |
| Bài tin tức mới | thêm `_posts/YYYY-MM-DD-tieu-de.md` |
| Trang Giới thiệu / Học cờ | `gioi-thieu.md`, `hoc-co.md` |

Có thể sửa trực tiếp trên github.com (phím `.` để mở web editor), commit là site tự build lại sau ~1 phút.

## Deploy lần đầu

```bash
cd covay-club
git init -b main && git add . && git commit -m "Initial site"
gh repo create covay --public --source=. --push
gh api -X POST repos/{owner}/covay/pages -f "source[branch]=main" -f "source[path]=/"
```

Rồi sửa `url` và `baseurl` trong `_config.yml` cho khớp (`https://<user>.github.io` và `/covay`), commit, push.

## Xem trước trên máy (tuỳ chọn)

```bash
brew install ruby                       # Ruby hệ thống của macOS quá cũ
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --livereload   # mở http://localhost:4000/covay/
```

## Tên miền riêng (tuỳ chọn)

Tạo file `CNAME` chứa tên miền (ví dụ `covay.example.edu.vn`), trỏ CNAME DNS về `<user>.github.io`, đặt `baseurl: ""` và `url` là tên miền mới.
