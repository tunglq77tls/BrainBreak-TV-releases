# BrainBreak TV

Ứng dụng cho **Android TV / Google TV**: khi bé mở YouTube, TV360... (các ứng dụng phụ huynh chọn), bé phải trả lời vài câu **Toán, Tiếng Anh, Tiếng Việt** trước khi xem tiếp.

- Yêu cầu: Android TV / Google TV **Android 9 trở lên** (có CH Play hoặc cài được file APK). Tizen (Samsung), webOS (LG) không dùng được.
- Dữ liệu (hồ sơ bé, PIN, lịch sử) lưu trên chính TV, không gửi ra ngoài.
- Bản mới nhất: [Releases](https://github.com/tunglq77tls/BrainBreak-TV-releases/releases/latest)

## Cách 1: Cài qua Downloader (dễ nhất)

1. Trên TV mở **CH Play**, tìm và cài app **Downloader** (của AFTVnews).
2. Vào **Cài đặt TV > Bảo mật & hạn chế** (một số TV nằm trong **Ứng dụng > Quyền đặc biệt**), bật **Cài ứng dụng không rõ nguồn gốc** cho **Downloader**. Nếu bỏ qua bước này, TV sẽ tự hỏi khi cài và dẫn bạn tới đúng trang đó.
3. Mở **Downloader**, ở ô địa chỉ gõ mã **`8692479`**, bấm **Go**.
   - Nếu Downloader không nhận mã, gõ đầy đủ địa chỉ:
     `https://github.com/tunglq77tls/BrainBreak-TV-releases/releases/latest/download/brainbreak-tv.apk`
4. Đợi tải xong, bấm **Cài đặt**, rồi bấm **Xong**. Downloader hỏi có xóa file APK không thì chọn **Xóa**.
5. Mở **BrainBreak TV** trong danh sách ứng dụng của TV và làm theo [Thiết lập lần đầu](#thiết-lập-lần-đầu).

## Cách 2: Tải file APK từ repo rồi cài thủ công

1. Mở trang [Releases](https://github.com/tunglq77tls/BrainBreak-TV-releases/releases/latest) và tải file **`brainbreak-tv.apk`** (khoảng 22 MB) về máy tính hoặc điện thoại. (`latest.json` chỉ để app tự kiểm tra cập nhật, không cần tải.)
2. Đưa file vào TV bằng **một** trong các cách sau:

   **a) USB**
   1. Chép `brainbreak-tv.apk` vào USB, cắm vào TV.
   2. Trên TV mở app quản lý file (ví dụ **File Commander**, **X-plore**, cài từ CH Play nếu TV chưa có), chọn file APK.
   3. Khi TV hỏi, cho phép app quản lý file đó **Cài ứng dụng không rõ nguồn gốc**, rồi bấm **Cài đặt**.

   **b) Máy tính qua `adb`** (TV và máy tính cùng mạng)
   1. Trên TV bật **Tùy chọn nhà phát triển** (Cài đặt > Giới thiệu > bấm **Bản dựng** 7 lần) rồi bật **Gỡ lỗi USB / Gỡ lỗi mạng**.
   2. Trên máy tính, trong thư mục chứa file APK:

      ```bash
      adb connect <địa-chỉ-IP-của-TV>:5555
      adb install -r brainbreak-tv.apk
      ```

      Muốn mở app luôn: `adb shell am start -n com.brainbreak.tv/.MainActivity`.

3. Mở **BrainBreak TV** trong danh sách ứng dụng của TV và làm theo phần dưới.

## Thiết lập lần đầu

Lần đầu mở, app tự chạy trình thiết lập (dành cho **phụ huynh**):

1. Đọc phần giải thích quyền và bấm đồng ý.
2. Đặt **PIN 6 số** (nhớ kỹ, đừng để bé biết).
3. Tạo hồ sơ cho bé: tên, avatar, **Lớp** (câu hỏi lọc theo Lớp này).
4. Chọn ứng dụng cần giám sát (YouTube, TV360...).
5. Bật 2 quyền: **Trợ năng** (để biết ứng dụng nào đang mở) và **Truy cập thông báo** (để tạm dừng video khi hiện quiz). App mở thẳng trang cài đặt tương ứng; nếu TV ẩn trang đó, app sẽ chỉ lệnh `adb` để bật.
6. Đặt hạn mức xem và giờ nghỉ (có thể bỏ qua, làm sau trong **Chế độ phụ huynh**).

Thử: mở YouTube, bé phải qua quiz.

Điều hướng bằng remote: mũi tên để di chuyển, **OK** để chọn, **Back** để quay lại hoặc thoát Chế độ phụ huynh.

## Gặp lỗi thường gặp

- **Không bật được quyền** (Android 13 trở lên, hiện "Cài đặt bị hạn chế"): vào **Cài đặt > Ứng dụng > BrainBreak TV**, bấm menu ⋮ (hoặc nút phụ) > **Cho phép cài đặt bị hạn chế**, rồi bật lại quyền.
- **Cài báo "xung đột" / "ứng dụng không tương thích"**: TV đang có bản cài từ nguồn khác (ký bằng khóa khác). Gỡ app cũ rồi cài lại; dữ liệu cũ sẽ mất.
- **Không thấy câu hỏi mới**: vào **Chế độ phụ huynh > Tải lại**.
- **Quên PIN**: cần máy tính có `adb`, chạy
  `adb shell am broadcast -a com.brainbreak.tv.RESET_PIN -n com.brainbreak.tv/.parent.ResetPinReceiver`.
- **Muốn chặn một kênh YouTube cụ thể**: app không tự chặn từng kênh. Dùng **Family Link** của Google; hướng dẫn có trong Chế độ phụ huynh > Family Link.

## Tự thêm câu hỏi của gia đình

App có sẵn bộ câu hỏi chung (Toán, Tiếng Anh, Tiếng Việt). Gia đình có thể thêm **câu hỏi riêng** bằng một Google Sheet của mình; câu riêng hiện cùng câu chung, và câu có `id` trùng câu chung thì thay thế câu chung.

1. **Tạo Google Sheet mới.** Hàng 1 là tiêu đề, đúng tên cột, chữ thường:

   | id | subject | grade | question | option_a | option_b | option_c | option_d | answer | enabled | shuffle |
   |---|---|---|---|---|---|---|---|---|---|---|
   | nha-001 | math | 3 | 7 + 8 = ? | 14 | 15 | 16 | 13 | B | TRUE | TRUE |

   - `id`: duy nhất và không đổi sau khi đã dùng (TV dùng id để nhớ bé đã trả lời câu nào). Nên dùng tiền tố riêng như `nha-001` để khỏi trùng câu chung.
   - `subject`: `math`, `english` hoặc `vietnamese`.
   - `grade`: số từ 1 đến 5. Bé chỉ nhận câu đúng **Lớp** của hồ sơ mình.
   - `question`, `option_a` đến `option_d`: chỉ chữ; cả bốn phương án phải có.
   - `answer`: `A`, `B`, `C` hoặc `D`.
   - `enabled`: để trống hoặc `TRUE` là bật, `FALSE` là tắt câu đó.
   - `shuffle`: để trống hoặc `TRUE` là xáo trộn phương án; `FALSE` nếu đáp án phụ thuộc thứ tự (ví dụ "cả A và B").
   - Dòng sai (thiếu phương án, đáp án không hợp lệ, môn lạ) bị bỏ qua, không làm hỏng các dòng khác.
2. **Công khai Sheet.** Cách khuyên dùng: **Tệp > Chia sẻ > Xuất bản lên web**, chọn đúng trang tính, định dạng **.csv**, bấm Xuất bản rồi copy link dạng `https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?output=csv`. Cách khác: Chia sẻ > "Bất kỳ ai có liên kết" (Người xem) rồi copy link. Đừng đưa thông tin cá nhân vào Sheet.
3. **Dán link vào app.** Trên TV vào **Chế độ phụ huynh** (nhập PIN) > **Cấu hình bằng điện thoại**, quét mã QR bằng camera điện thoại, dán link vào ô **Sheet riêng**, bấm lưu. Hoặc gõ link bằng remote ở trang **Tải lại**.
4. **Kiểm.** Chế độ phụ huynh > **Tải lại**, bấm tải; dòng "Sheet riêng: lần tải gần nhất ..." phải hiện giờ vừa rồi.
5. Muốn chỉ dùng câu của nhà thì tắt công tắc **Ngân hàng chung** (trong Chế độ phụ huynh hoặc trang cấu hình điện thoại).

Sau này thêm hoặc sửa câu cứ sửa thẳng trên Sheet; TV tự tải lại trong vòng 1 giờ (hoặc bấm **Tải lại** để có ngay). Bản xuất bản lên web có thể mất vài phút để cập nhật.

## Cập nhật và gỡ

- **Cập nhật**: app tự kiểm tra bản mới mỗi ngày. Vào **Chế độ phụ huynh** (nhập PIN), nếu có **Có bản cập nhật** thì bấm **Tải và cài đặt**. Dữ liệu được giữ nguyên.
- **Gỡ**: Cài đặt > Ứng dụng > BrainBreak TV > Gỡ cài đặt.

## Kiểm tra file tải về (tùy chọn)

Mọi bản phát hành đều ký bằng cùng một khóa. Chứng chỉ SHA-256 của khóa:

```
89e5dc9e8070b828dc8fcd451662ba5f656f1595e9674fba5faab4c7ee4b4dfe
```

Kiểm bằng `apksigner verify --print-certs brainbreak-tv.apk` (có trong Android SDK build-tools); chuỗi SHA-256 in ra phải trùng chuỗi trên.
