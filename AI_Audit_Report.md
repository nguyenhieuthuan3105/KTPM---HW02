# AI Audit Log

**MSSV:** 23127125 </br>
**Họ và tên:** Nguyễn Hiếu Thuận </br>
**Bài tập:** HW02 - Domain Testing

---

## FR-02: Đăng nhập & Khóa tài khoản

### [Prompt 1]

- **Thời gian:** 14:30 09/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text
Đóng vai trò là một Software Tester chuyên nghiệp. Tôi đang cần áp dụng kỹ thuật Domain Testing cho chức năng FR-02: Đăng nhập và Khóa tài khoản.
Dưới đây là đặc tả (business rules) của chức năng:
1. Người dùng nhập Email và Mật khẩu.
2. Trường email phải dùng type="email" (có validate HTML5 format).
3. Sau mỗi lần đăng nhập sai, hệ thống tăng bộ đếm lên đúng 1 đơn vị.
4. Nếu đăng nhập sai từ 3 lần trở lên liên tiếp, tài khoản bị tạm khóa 30 giây (môi trường demo).
5. Trả về thông báo lỗi phù hợp; không để lộ chi tiết nguyên nhân.6. Đăng nhập thành công trả về JWT Token.
Nhiệm vụ của bạn: Hãy phân tích các biến đầu vào (Email, Password) và biến trạng thái (Login failed attempts). Liệt kê chi tiết các miền giá trị (Domain) hợp lệ (Valid) và không hợp lệ (Invalid) cho từng biến. Xin đừng vội tạo Test Case, chỉ thực hiện bước phân tích Domain. Trình bày bằng Markdown rõ ràng.
```

- **AI Output:**

```text
Phân tích Miền giá trị (Domain Analysis) - FR-02
1. Biến đầu vào: Email
Dựa trên quy định bắt buộc sử dụng type="email" (HTML5 format) phía frontend và logic xác thực tài khoản phía backend.
Miền hợp lệ (Valid Domains):
Chuỗi ký tự tuân thủ đúng định dạng chuẩn của email HTML5 (Ví dụ: user@example.com, firstname.lastname@sub.domain.org).
Email hợp lệ VÀ đã được đăng ký (tồn tại trong cơ sở dữ liệu của hệ thống).
Miền không hợp lệ (Invalid Domains):
Trống (Empty): Không nhập gì vào trường email.
Sai định dạng (Invalid HTML5 Format): Chuỗi ký tự vi phạm cấu trúc email chuẩn (Ví dụ: userexample.com - thiếu @, @example.com - thiếu tên hộp thư, user@ - thiếu tên miền, chứa khoảng trắng hoặc ký tự đặc biệt không cho phép).
Chưa đăng ký (Unregistered): Email đúng định dạng HTML5 nhưng không tồn tại trong hệ thống.

2. Biến đầu vào: Mật khẩu (Password)
Biến này được đánh giá dựa trên sự đối chiếu với dữ liệu đã lưu trữ của Email tương ứng.
Miền hợp lệ (Valid Domains):
Chuỗi ký tự khớp chính xác (có phân biệt chữ hoa/chữ thường) với mật khẩu đã lưu của Email hợp lệ vừa nhập.
Miền không hợp lệ (Invalid Domains):
Trống (Empty): Không nhập gì vào trường mật khẩu.
Không khớp (Mismatch): Chuỗi ký tự nhập vào không đúng với mật khẩu của Email tương ứng.

3. Biến trạng thái: Số lần đăng nhập sai (Login Failed Attempts)
Đây là biến ẩn (state variable) cực kỳ quan trọng, quyết định luồng xử lý của hệ thống đối với tính năng tạm khóa tài khoản. Biến này phụ thuộc vào 2 yếu tố: Bộ đếm (Counter) và Thời gian chờ (Timeout).
Miền hợp lệ (Active State - Cho phép thực hiện đăng nhập):
Attempts = 0: Trạng thái ban đầu (người dùng mới) hoặc bộ đếm vừa được reset sau một lần đăng nhập thành công.
Attempts = 1 hoặc Attempts = 2: Người dùng đã nhập sai thông tin 1 hoặc 2 lần liên tiếp. Hệ thống ghi nhận lỗi nhưng tài khoản vẫn ở trạng thái hoạt động (Active).
Attempts >= 3 VÀ Thời gian kể từ lần sai cuối cùng >= 30 giây: Tài khoản đã vượt qua thời gian phạt. Trạng thái được mở khóa (Unlocked), cho phép người dùng tiếp tục gửi request đăng nhập.
Miền không hợp lệ (Locked State - Từ chối đăng nhập):
Attempts >= 3 VÀ Thời gian kể từ lần sai cuối cùng < 30 giây: Tài khoản đang trong thời gian bị tạm khóa. Trong miền trạng thái này, mọi thao tác submit form đăng nhập (cho dù nhập đúng hay sai Email/Password) đều phải bị hệ thống từ chối xử lý và trả về thông báo lỗi chung.
```

### [Prompt 2]

- **Thời gian:** 21:30 09/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text
Dựa vào bảng phân tích miền giá trị (Valid/Invalid Domains) và các miền kết quả kỳ vọng (O1, O2, O3, O4) mà bạn vừa liệt kê, bây giờ hãy thiết kế một tập hợp các Test Case chi tiết cho kỹ thuật Domain Testing của chức năng FR-02.
Yêu cầu:
Trình bày dưới dạng bảng (Markdown Table).
Các cột bắt buộc: Test Case ID, Mục đích (Test Objective), Điều kiện tiền quyết (Precondition), Đầu vào (Email, Password), Trạng thái hệ thống (Failed Attempts), và Kết quả mong đợi (Expected Result).
Hãy kết hợp các miền giá trị sao cho bao phủ được cả 4 kịch bản kết quả (O1, O2, O3, O4) mà không bị dư thừa (tránh tổ hợp bùng nổ không cần thiết).
Đảm bảo test case có tính thực tế (ví dụ: cung cấp data mẫu cho Email/Password trong bảng).
Xuất ra kết quả dưới dạng markdown mà tôi có thể thêm vào lập tức ở Main Report
```

- **AI Output:**

```text
Thiết kế Test Case (Domain Testing)Dựa trên các miền giá trị đã phân tích, dưới đây là tập hợp các Test Case đại diện nhằm đảm bảo bao phủ toàn bộ các kịch bản kết quả (O1, O2, O3, O4) mà không gây ra bùng nổ tổ hợp:Test Case IDMục đích (Test Objective)Điều kiện tiền quyết (Precondition)Đầu vào (Email & Password)Trạng thái hệ thống (Failed Attempts)Kết quả mong đợi (Expected Result)TC_FR02_01Kiểm tra đăng nhập thành công ở trạng thái bình thường (Phủ: V1 + V2 + S1 -> O1)Tài khoản user@example.com đã tồn tại, pass: Abc@123Email: user@example.comPass: Abc@123S1: 0 lần saiĐăng nhập thành công, trả về JWT Token, bộ đếm giữ ở 0.TC_FR02_02Kiểm tra đăng nhập thành công sau khi hết thời gian phạt (Phủ: V1 + V2 + S3 -> O1)Tài khoản user@example.com đã tồn tại, pass: Abc@123Email: user@example.comPass: Abc@123S3: 3 lần sai, đã chờ > 30sĐăng nhập thành công, trả về JWT Token, reset bộ đếm về 0.TC_FR02_03Kiểm tra validation UI khi bỏ trống Email (Phủ: I1 -> O2)Hệ thống đang ở trang Đăng nhậpEmail: (bỏ trống)Pass: Abc@123S1: 0 lần saiFrontend chặn submit, hiển thị lỗi yêu cầu nhập Email.TC_FR02_04Kiểm tra validation UI khi Email sai định dạng (Phủ: I2 -> O2)Hệ thống đang ở trang Đăng nhậpEmail: userexample.comPass: Abc@123S1: 0 lần saiFrontend chặn submit, hiển thị lỗi định dạng HTML5 email.TC_FR02_05Kiểm tra validation UI khi bỏ trống Password (Phủ: I4 -> O2)Hệ thống đang ở trang Đăng nhậpEmail: user@example.comPass: (bỏ trống)S1: 0 lần saiFrontend chặn submit, hiển thị lỗi yêu cầu nhập Mật khẩu.TC_FR02_06Kiểm tra lỗi bảo mật khi Email chưa đăng ký (Phủ: I3 + S1 -> O3)Email new@example.com chưa có trong DBEmail: new@example.comPass: AnyPass123S1: 0 lần saiTrả về lỗi chung ("Email hoặc mật khẩu không đúng"), tăng bộ đếm lên 1.TC_FR02_07Kiểm tra lỗi bảo mật khi sai Password và đẩy lên giới hạn khóa (Phủ: V1 + I5 + S2 -> O3)Tài khoản user@example.com đã tồn tạiEmail: user@example.comPass: WrongPass!S2: 2 lần saiTrả về lỗi chung, tăng bộ đếm lên 3 (Tài khoản chính thức chuyển sang trạng thái tạm khóa).TC_FR02_08Kiểm tra từ chối đăng nhập khi tài khoản đang bị khóa, dù nhập đúng (Phủ: V1 + V2 + S4 -> O4)Tài khoản user@example.com đã tồn tạiEmail: user@example.comPass: Abc@123S4: 3 lần sai, thời gian < 30sTrả về thông báo tài khoản đang bị tạm khóa, không trả về JWT Token.TC_FR02_09Kiểm tra từ chối đăng nhập khi tài khoản đang bị khóa, nhập sai (Phủ: I3 + I5 + S4 -> O4)Bất kỳ email/pass nàoEmail: fake@example.comPass: FakePassS4: 3 lần sai, thời gian < 30s, Trả về thông báo tài khoản đang bị tạm khóa (hệ thống không check DB, ưu tiên check trạng thái lock trước).
```
