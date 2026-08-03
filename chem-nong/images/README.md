# 🖼️ Hình ảnh dự án — CHÉM NÓNG

Nơi lưu trữ toàn bộ file hình ảnh của game. Vì nằm trong `public/`, mọi file ở đây
đều truy cập được qua URL `/images/...` (ví dụ `/images/logo/tea-plus-logo.webp`).

## Cấu trúc

| Thư mục | Dùng cho |
|---|---|
| `logo/` | Logo game, logo chiến thắng, logo thể lệ, logo TEA+ |
| `items/` | Vật phẩm chém (chanh, trà, dù yuzu, mặt trời) — kèm bản đã chém (`-slice`/`-half`/`-squint`) |
| `labels/` | Nhãn điểm popup khi chém (+10/+20/+40/-10, combo x2, tên vật phẩm) |
| `backgrounds/` | Ảnh nền sân chơi |
| `buttons/` | Ảnh các nút bấm đang dùng trong UI |
| `effects/` | Hiệu ứng khi chém (water splash) |
| `product/` | Ảnh sản phẩm/cúp cho màn kết quả |
| `ui/` | Panel/khung giao diện các màn (home, settings, rules) |

## Vật phẩm (items/) ↔ key trong `game.js`

| File | Key | Vật phẩm | Điểm |
|---|---|---|---|
| `lemon-whole.webp` (+ `lemon-half.webp`) | `chanh` | Chanh Yuzu mọng mát | +20 |
| `tea-leaf-1.webp` | `tra` | Trà đậm vị thanh mát | +20 |
| `umbrella-open-1.webp` | `mong` | Dù Yuzu | +20 |
| `sun-angry.webp` (+ `sun-squint.webp`) | `matroi` | Mặt trời | −10 (phạt) |

## Quy ước đặt tên

- Chữ thường, nối bằng dấu gạch ngang, không dấu tiếng Việt/dấu cách/chữ hoa (tránh lỗi URL).
- Định dạng ưu tiên: **WebP** (nền trong suốt cho vật phẩm/logo/nhãn).

## Dùng trong code

Vật phẩm được định nghĩa trong `public/game.js` → mảng `ITEMS`, mỗi item có field `img`/`slice` trỏ tới file trong `items/`:

```js
{ key: 'chanh', img: '/images/items/lemon-whole.webp', label: 'Chanh Yuzu mọng mát', points: 20, weight: 3 }
```

Trong HTML/CSS tham chiếu trực tiếp, ví dụ:

```html
<img src="/images/logo/tea-plus-logo.webp" alt="TEA+ Suntory" />
```

## Dọn asset thừa

Trước khi thêm/xoá file trong đây, kiểm tra xem có còn được tham chiếu không:

```bash
grep -roh '/images/[a-zA-Z0-9/_.-]*\.\(webp\|png\|jpg\|jpeg\)' public/index.html public/client.js public/game.js public/style.css | sort -u
```

So kết quả với `find public/images -type f` để phát hiện file mồ côi.
