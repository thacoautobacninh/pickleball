# Giải Pickleball Tranh Cup Peugeot – THACO AUTO Bắc Ninh

Trang tỉ số trực tuyến: Livestream theo sân, Xếp hạng, Lịch đấu, Bốc thăm chia bảng.
Chạy trên GitHub Pages, dữ liệu lưu trên Firebase Firestore (gói miễn phí Spark là đủ).

Nhiều trọng tài nhập điểm cùng lúc được: mỗi lần bấm điểm được ghi bằng transaction
(đọc bản mới nhất trên máy chủ rồi mới cộng), nên hai máy bấm cùng một trận cũng không đè mất điểm của nhau.

## Các file

| File | Dùng để |
|---|---|
| `index.html` | Toàn bộ trang |
| `firebase-config.js` | Cấu hình Firebase + email tài khoản trọng tài — **bạn phải điền** |
| `firestore.rules` | Quy tắc bảo mật: ai cũng xem được, chỉ trọng tài đã đăng nhập mới ghi được |

## Cài đặt (khoảng 15 phút)

### 1. Tạo Firebase
1. Vào https://console.firebase.google.com → **Add project** (tắt Google Analytics cũng được).
2. **Build → Firestore Database → Create database** → chọn vùng `asia-southeast1` (Singapore) → **Production mode**.
3. Tab **Rules** của Firestore: xoá hết, dán nội dung file `firestore.rules` → **Publish**.
4. **Build → Authentication → Get started → Sign-in method → Email/Password → Enable**.
5. Tab **Users → Add user**: email `trongtai@pickleball-thaco.vn` (hoặc email bạn muốn), đặt mật khẩu trọng tài.
   Muốn đổi mật khẩu sau này: vào lại đây, xoá user và tạo lại, hoặc dùng *Reset password*.
6. **Project settings (bánh răng) → General → Your apps → Web (</>)** → đặt tên → **Register app** → copy đoạn `firebaseConfig`.

### 2. Điền cấu hình
Mở `firebase-config.js`, thay các giá trị `DIEN_...` bằng đoạn vừa copy, và sửa `REF_EMAIL` cho trùng email trọng tài ở bước 1.5.
Các giá trị này được phép để công khai trên GitHub; dữ liệu được bảo vệ bằng `firestore.rules`.

### 3. Đưa lên GitHub Pages
1. Tạo repo mới trên GitHub (ví dụ `pickleball-cup-peugeot`), tải 4 file này lên nhánh `main`.
2. Repo → **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `(root)` → Save**.
3. Sau 1–2 phút trang chạy ở `https://<tên-github>.github.io/pickleball-cup-peugeot/`.

### 4. Cho phép tên miền đăng nhập
Firebase → **Authentication → Settings → Authorized domains → Add domain** → thêm `<tên-github>.github.io`.
Thiếu bước này trọng tài sẽ không đăng nhập được.

## Sử dụng
- **Người xem**: mở link, không cần đăng nhập. Tỉ số tự cập nhật.
- **Trọng tài**: bấm **Chế độ trọng tài** → nhập mật khẩu → vào trận ở sân mình → bấm đội thắng pha bóng.
  Nhiều trọng tài dùng chung một mật khẩu và đăng nhập cùng lúc trên nhiều máy được.
- **Bốc thăm**: tab **Bốc thăm** → nhập danh sách đội → mở màn hình trình chiếu để livestream → bấm *Rút đội tiếp theo* (hoặc phím →, bút trình chiếu) → *Tạo lịch thi đấu*.
- **Xếp hạng**: tự tính từ các trận đã kết thúc có ghi “Bảng A/B/…” ở ô Vòng/bảng.

## Giới hạn gói miễn phí — nên đọc trước ngày giải
Mỗi lần trọng tài bấm điểm, **mỗi người đang mở trang** tốn 1 lượt đọc. Gói Spark miễn phí cho 50.000 lượt đọc/ngày.
Ước tính: khoảng 2.000 lần bấm điểm cả ngày × 100 người xem cùng lúc ≈ 200.000 lượt đọc → **vượt gói miễn phí**,
khi đó trang sẽ ngừng cập nhật đến hết ngày.

Khuyến nghị: trước ngày giải chuyển project sang gói **Blaze** (Firebase console → Upgrade, cần thẻ thanh toán).
Giá đọc khoảng 0,06 USD / 100.000 lượt, nên cả ngày giải thường chỉ vài nghìn đến vài chục nghìn đồng.
Có thể đặt **Budget alert** trong Google Cloud Billing (ví dụ 5 USD) để yên tâm.
