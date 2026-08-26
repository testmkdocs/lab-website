# lab-website — template MkDocs (phương án B / mục 4.2)

Website lab dựng bằng MkDocs + theme Material. Repo này phải để **Public**
(GitHub Free chỉ cho Pages chạy từ repo Public).

## Dựng trong 5 bước

1. Tạo repo `lab-website` trên GitHub, **Public**
2. Copy toàn bộ nội dung thư mục này vào, push lên `main`
3. Sửa mọi chỗ đánh dấu `SỬA:` trong `mkdocs.yml`
4. **Settings → Pages → Source: GitHub Actions**
5. Push lại → xem tab **Actions** → mở `https://<org>.github.io/lab-website/`

## Chạy thử ở máy

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve                 # → http://localhost:8000
```

Trước mỗi lần push:

```bash
mkdocs build --strict        # exit code 0 mới push
```

Hoặc dùng Docker, khỏi cài Python:

```bash
docker run --rm -it -p 8000:8000 -v "$PWD":/docs squidfunk/mkdocs-material:9.7.7
```

## Thêm nội dung

| Muốn thêm | Làm gì |
|---|---|
| Thành viên | Sửa `docs/team.md` |
| Paper (mức 1) | Thêm một khối vào `docs/publications.md` |
| Trang riêng cho paper (mức 2) | Copy `docs/papers/abc-2026.md`, khai vào `nav` |
| Dự án | Sửa `docs/projects/index.md` |
| Trang mới | Thêm file vào `docs/`, **nhớ khai vào `nav`** |

## Ba lỗi hay gặp

**Trang mới không hiện trên menu** — quên khai vào `nav` trong `mkdocs.yml`.

**Build fail vì link chết** — link phải trỏ tới file `.md`, tính từ `docs/`:
```markdown
[Xem thêm](papers/abc-2026.md)    ✅
[Xem thêm](/papers/abc-2026/)      ❌
```

**CI vỡ dù không đụng gì** — phiên bản trong `requirements.txt` bị để trần. Luôn pin `==`.
