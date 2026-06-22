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

### [Prompt 3]

- **Thời gian:** 19:30 10/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text
Chúng ta đã hoàn thành Domain Testing. Bây giờ, tôi muốn áp dụng kỹ thuật Boundary Value Analysis (BVA) cho chức năng FR-02. Dựa vào đặc tả, có 2 ranh giới (boundary) cần phân tích:
Giới hạn số lần đăng nhập sai: Ngưỡng khóa tài khoản là 3 lần (n = 3).
Giới hạn thời gian tạm khóa: Thời gian phạt là 30 giây (t = 30s).
Nhiệm vụ của bạn:
Bước 1 (Giải thích step-by-step): Hãy viết một đoạn ngắn giải thích cách phân tích các giá trị biên (min, max, just below, just above, on the boundary) cho 2 ranh giới trên. Ví dụ: Với n=3 thì các giá trị cần test là n=2, n=3, n=4.
Bước 2 (Thiết kế Test Case): Thiết kế bảng Test Case BVA chi tiết để kiểm tra các giá trị biên này. Bảng phải có các cột: Test Case ID (bắt đầu là TC_FR02_BVA_01), Mục đích, Điều kiện tiền quyết, Đầu vào & Trạng thái (Inputs & State), và Kết quả mong đợi.
Xin hãy trình bày bằng Markdown rõ ràng để tôi có thể đưa trực tiếp vào báo cáo.
```

- **AI Output:**

```text
Boundary Value Analysis (BVA)Bước 1: Phân tích các giá trị biên (Step-by-step Explanation)Để áp dụng kỹ thuật BVA cho FR-02 , tôi tập trung vào 2 ranh giới quyết định việc thay đổi trạng thái của hệ thống: số lần đăng nhập sai và thời gian tạm khóa tài khoản. Theo nguyên tắc của BVA, lỗi thường tiềm ẩn ở khu vực lân cận các ranh giới này.  1. Ranh giới số lần đăng nhập sai (Ngưỡng n = 3):  Just below the boundary (n = 2): Kiểm tra khi người dùng nhập sai lần thứ 2. Hệ thống phải ghi nhận lỗi nhưng tài khoản vẫn ở trạng thái hoạt động.  On the boundary (n = 3): Kiểm tra khi người dùng nhập sai ở đúng lần thứ 3. Đây là điểm trigger kích hoạt trạng thái tạm khóa.  Just above the boundary (n = 4): Kiểm tra khi người dùng tiếp tục gửi request đăng nhập lần thứ 4 (khi tài khoản vừa bị khóa). Hệ thống phải lập tức từ chối mà không cần kiểm tra DB.2. Ranh giới thời gian tạm khóa (Ngưỡng t = 30s):  Just below the boundary (t = 29s): Cố gắng thực hiện đăng nhập khi thời gian phạt chưa kết thúc (còn thiếu 1 giây). Hệ thống vẫn phải hiển thị lỗi bị khóa.On the boundary (t = 30s): Cố gắng thực hiện đăng nhập ngay tại thời điểm mốc phạt vừa chạm tới. Hệ thống phải cho phép xác thực (mở khóa tài khoản).Just above the boundary (t = 31s): Cố gắng đăng nhập khi thời gian phạt đã qua mức an toàn. Hệ thống phải tiếp nhận request bình thường.Bước 2: Thiết kế Test Case (BVA Testing)Dưới đây là các Test Case chi tiết để kiểm thử các giá trị biên đã phân tích:Test Case IDMục đích (Test Objective)Điều kiện tiền quyết (Precondition)Đầu vào & Trạng thái (Inputs & State)Kết quả mong đợi (Expected Result)TC_FR02_BVA_01Kiểm tra biên dưới số lần sai (n = 2)   Tài khoản hợp lệ, bộ đếm đang là 1Email: user@example.comPassword: WrongPassState: 1 lần saiHệ thống báo lỗi thông tin không đúng, tăng bộ đếm lên 2, tài khoản không bị khóa.TC_FR02_BVA_02Kiểm tra tại biên số lần sai (n = 3)   Tài khoản hợp lệ, bộ đếm đang là 2Email: user@example.comPassword: WrongPassState: 2 lần saiHệ thống báo lỗi tài khoản bị tạm khóa 30s, tăng bộ đếm lên 3.  TC_FR02_BVA_03Kiểm tra vượt biên số lần sai (n = 4)   Tài khoản vừa bị khóa, bộ đếm đang là 3Email: user@example.comPassword: AnyPassState: 3 lần saiHệ thống từ chối đăng nhập ngay lập tức, báo lỗi tài khoản đang bị tạm khóa.TC_FR02_BVA_04Kiểm tra biên dưới thời gian khóa (t = 29s)Tài khoản đang bị khóa, vừa trôi qua 29 giâyEmail: user@example.comPassword: CorrectPassState: 3 lần sai, t = 29sĐăng nhập thất bại, hệ thống báo lỗi tài khoản vẫn đang bị khóa.TC_FR02_BVA_05Kiểm tra tại biên thời gian khóa (t = 30s)   Tài khoản bị khóa, vừa trôi qua đúng 30 giâyEmail: user@example.comPassword: CorrectPassState: 3 lần sai, t = 30sĐăng nhập thành công, trả về JWT Token, reset bộ đếm số lần sai về 0.  TC_FR02_BVA_06Kiểm tra vượt biên thời gian khóa (t = 31s)Tài khoản bị khóa, đã trôi qua 31 giâyEmail: user@example.comPassword: CorrectPassState: 3 lần sai, t = 31sĐăng nhập thành công, trả về JWT Token, reset bộ đếm số lần sai về 0.
```

### [Prompt 4]

- **Thời gian:** 10:00 15/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text
vay hay thiet ke lai file Bug_report cho phu hop nhe, luu y tra ve format markdown de toi copy vao
```

- **AI Output:**

```text
# Bug Report
**MSSV:** 23127125 </br>
**Họ và tên:** Nguyễn Hiếu Thuận </br>
**Bài tập:** HW02 - Domain Testing </br>
**Chức năng:** FR-02 (Đăng nhập & Khóa tài khoản)
---
## Danh sách Lỗi (Bugs) phát hiện được trên SUT
### 1. Bug 1: Sai logic khóa tài khoản (Khóa ở lần 2 thay vì lần 3)
* **Mô tả:** Theo đặc tả, tài khoản chỉ bị tạm khóa khi nhập sai từ 3 lần trở lên liên tiếp. Tuy nhiên, thực tế hệ thống đã khóa tài khoản ngay ở lần nhập sai thứ 2.
* **Test Case phát hiện:** `TC_FR-02_07`, `TC_FR-02_BVA_01`
* **GitHub Issue:** [Link Issue #1] *(Bạn hãy thay link thật vào đây)*
* **Ảnh minh chứng:**
  ![Bug 1](images/bug1.png)
### 2. Bug 2: Không hiển thị thông báo "Tài khoản bị tạm khóa" (UI/UX)
* **Mô tả:** Khi tài khoản rơi vào trạng thái khóa, hệ thống không trả về thông báo lỗi chi tiết như yêu cầu ("Tài khoản bị tạm khóa 30s") mà chỉ hiển thị thông báo chung chung "Đăng nhập thất bại, vui lòng kiểm tra lại". Điều này gây hoang mang cho người dùng.
* **Test Case phát hiện:** `TC_FR-02_08`, `TC_FR-02_09`, `TC_FR-02_BVA_03`
* **GitHub Issue:** [Link Issue #2] *(Bạn hãy thay link thật vào đây)*
* **Ảnh minh chứng:**
  ![Bug 2](images/bug2.png)
### 3. Bug 3: Lỗi đồng bộ trạng thái Frontend (Phải F5 mới đăng nhập lại được)
* **Mô tả:** Sau khi hết thời gian phạt 30 giây, nếu người dùng tiếp tục nhấn nút Đăng nhập thì vẫn không thành công. Người dùng bắt buộc phải F5 (tải lại toàn bộ trang) thì mới có thể đăng nhập lại bình thường. Frontend không tự động reset state timeout.
* **Test Case phát hiện:** `TC_FR-02_02`, `TC_FR-02_BVA_05`, `TC_FR-02_BVA_06`
* **GitHub Issue:** [Link Issue #3] *(Bạn hãy thay link thật vào đây)*
* **Ảnh minh chứng:**
  ![Bug 3](images/bug3-1.png)
### 4. Bug 4: Thiếu Validation chuẩn HTML5 ở trường Email
* **Mô tả:** Ô nhập Email ở Frontend đang thiếu ràng buộc validate theo định dạng email chuẩn (ví dụ: thiếu ký tự `@` nhưng vẫn submit được). Form vẫn đẩy request sai định dạng xuống tận Backend xử lý thay vì chặn ngay tại UI.
* **Test Case phát hiện:** `TC_FR-02_04`
* **GitHub Issue:** [Link Issue #4] *(Bạn hãy thay link thật vào đây)*
* **Ảnh minh chứng:**
  ![Bug 4](images/bug4.png)
```

## FR-08: Thanh toán (Checkout)

### [Prompt 1]

- **Thời gian:** 9:30 16/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text
Đóng vai trò là một Software Tester chuyên nghiệp. Tôi cần áp dụng kỹ thuật Domain Testing cho chức năng FR-08: Thanh toán (Checkout).
Mục tiêu của tôi là tạo ra một bộ Test Case bao phủ tối đa các kịch bản ngoại lệ, đặc biệt là các lỗi bảo mật (tampering) để phát hiện càng nhiều bug càng tốt. Dưới đây là đặc tả hệ thống:
Chỉ người dùng đã đăng nhập mới tiến hành thanh toán được.
Tổng tiền thanh toán được tính tự động từ giỏ hàng và không cho phép người dùng chỉnh sửa trực tiếp trên UI.
Giao diện hiển thị đầy đủ danh sách sản phẩm đặt mua.
Backend phải tự tính lại tổng tiền; không chấp nhận giá trị total_amount do client gửi lên.
Sau thanh toán thành công, giỏ hàng được xóa.
Nhiệm vụ của bạn gồm 2 phần, hãy trình bày hoàn toàn bằng Markdown để tôi đưa vào báo cáo:
Phần 1: Phân tích Domain (Step-by-step Explanation)
Hãy phân tích rõ các miền giá trị (Hợp lệ / Không hợp lệ) cho các biến ẩn và biến trạng thái sau:
Biến trạng thái đăng nhập (Auth Token).
Biến trạng thái Giỏ hàng (Số lượng món, Tồn kho sản phẩm trước khi checkout).
Biến đầu vào Payload API (Giá trị total_amount client gửi lên so với thực tế).
Phần 2: Thiết kế Bảng Test Case
Từ phân tích trên, hãy sinh ra một bộ Test Case chi tiết. Kết hợp các miền giá trị để tạo ra cả Happy Path và rất nhiều Negative/Edge Cases (Ví dụ: Dùng Postman/Burp Suite để sửa total_amount thành 0, số âm; Giỏ hàng trống nhưng vẫn gọi API; Sản phẩm bị xóa/hết hàng ngay lúc bấm thanh toán; Token hết hạn...).
Bảng gồm các cột: Test Case ID (Bắt đầu là TC_FR-08_01), Tên (Test Objective), Điều kiện tiền quyết, Đầu vào & Trạng thái, Kết quả mong đợi.
```

- **AI Output:**

```text
FR-08: Thanh toán (Checkout)Domain TestingĐể thực hiện Domain Testing cho FR-08, tôi không chỉ kiểm tra các thao tác trên giao diện UI (nơi người dùng bị giới hạn) mà tập trung phân tích các biến trạng thái ẩn và dữ liệu Payload API gửi từ Client lên Backend. Mục tiêu là phát hiện các lỗ hổng bảo mật (Data Tampering) và lỗi logic đồng bộ (Race Condition).  Phần 1: Phân tích Miền giá trị (Domain Analysis)Chức năng Thanh toán phụ thuộc vào 3 nhóm biến trạng thái và đầu vào cốt lõi:1. Biến trạng thái đăng nhập: Auth Token (Header Authorization)Trạng thái này quyết định quyền truy cập vào API thanh toán.Miền hợp lệ (Valid Domains):V1: Token tồn tại, chuẩn định dạng JWT, đúng chữ ký (Signature) và còn thời hạn sử dụng.Miền không hợp lệ (Invalid Domains):I1 (Missing): Không gửi kèm Token trong Header.I2 (Expired): Token hợp lệ nhưng đã hết hạn (Expired).I3 (Tampered/Invalid): Token bị chỉnh sửa nội dung (sai chữ ký) hoặc là token fake.2. Biến trạng thái Giỏ hàng (Cart State & Inventory)Trạng thái này kiểm tra tính hợp lệ của dữ liệu đầu vào trước khi lập đơn hàng.Miền hợp lệ (Valid Domains):V2: Giỏ hàng có ít nhất 1 sản phẩm ($N \ge 1$) VÀ Số lượng đặt mua của từng món $\le$ Số lượng tồn kho thực tế trong DB.Miền không hợp lệ (Invalid Domains):I4 (Empty Cart): Giỏ hàng trống ($N = 0$) nhưng Client vẫn cố tình gọi API Checkout.I5 (Out of Stock): Tồn kho hiện tại trong DB $<$ Số lượng khách đặt mua (Thường xảy ra do Race Condition: khách A thêm vào giỏ, khách B mua hết, sau đó khách A mới bấm thanh toán).I6 (Deleted Product): Sản phẩm trong giỏ đã bị Admin xóa hoặc vô hiệu hóa khỏi hệ thống trước khi thanh toán.3. Biến đầu vào Payload API: total_amount (Client vs Backend)Theo đặc tả, Backend KHÔNG ĐƯỢC tin tưởng giá trị total_amount từ Client gửi lên mà phải tự tính toán lại.Miền hợp lệ (Valid Domains):V3: Giá trị total_amount Client gửi khớp 100% với tổng tiền Backend tự tính dựa trên DB. (Hoặc Payload không gửi trường này, để Backend tự lo).Miền không hợp lệ (Invalid Domains / Tampering):I7 (Zero/Negative): Cố tình sửa payload total_amount = 0 hoặc số âm (VD: -50000).I8 (Fractional/Low): Cố tình sửa total_amount thành một số rất nhỏ (VD: 1 VNĐ).I9 (Overpriced): Cố tình sửa total_amount thành số lớn hơn thực tế (kiểm tra xem Backend có validate hay ghi nhận sai doanh thu không).Phần 2: Thiết kế Test Case (Domain Testing)Dựa trên phân tích trên, dưới đây là bộ Test Case kết hợp kỹ thuật chặn bắt Request (Intercept) qua Postman/Burp Suite để kiểm tra độ tin cậy của API:Test Case IDTên (Test Objective)Điều kiện tiền quyết (Precondition)Đầu vào & Trạng thái (Inputs & State)Kết quả mong đợi (Expected Result)TC_FR-08_01Kiểm tra thanh toán thành công (Happy Path) (Phủ: V1 + V2 + V3)User đã đăng nhập, giỏ hàng có 2 SP (Tổng 500k), tồn kho đủ.Auth: JWT hợp lệCart: 2 SP hợp lệPayload: total_amount = 500.000Thanh toán thành công. Backend tính đúng 500k. Trả về mã đơn hàng. Sau đó giỏ hàng tự động bị xóa (trống).TC_FR-08_02Kiểm tra bảo mật: Sửa tổng tiền thành 0 hoặc 1 VNĐ (Phủ: V1 + V2 + I7/I8)User đã đăng nhập, giỏ hàng có SP trị giá 500k.Dùng Postman gửi request.Payload: total_amount = 1 (hoặc 0)Backend bỏ qua giá trị 1đ của Client, tự động tính lại tổng tiền là 500k để lập đơn hàng (HOẶC trả về lỗi 400 Data Mismatch). Không được tạo đơn giá 1đ.TC_FR-08_03Kiểm tra bảo mật: Sửa tổng tiền thành số âm (Phủ: V1 + V2 + I7)User đã đăng nhập, giỏ hàng có SP trị giá 500k.Dùng Postman gửi request.Payload: total_amount = -50000Backend từ chối xử lý, báo lỗi 400 Bad Request (Invalid Amount), HOẶC tự động sửa lại thành 500k đúng giá trị thực.TC_FR-08_04Kiểm tra bảo mật API: Giỏ hàng trống nhưng vẫn gọi API Checkout (Phủ: V1 + I4)User đã đăng nhập. Giỏ hàng hiện tại đang trống (0 SP).Dùng Postman gọi thẳng API Checkout.Cart: $N = 0$Backend chặn lại, trả về lỗi 400 (Giỏ hàng trống, không thể lập đơn). Không tạo ra đơn hàng rỗng.TC_FR-08_05Kiểm tra Race Condition: Hết hàng ngay lúc bấm thanh toán (Phủ: V1 + I5)User có SP A trong giỏ. (Admin vừa vào DB set tồn kho SP A = 0).Bấm nút Checkout trên UI.Cart: Số lượng đặt > Tồn khoThanh toán thất bại. Trả về thông báo lỗi: "Sản phẩm A đã hết hàng hoặc không đủ số lượng".TC_FR-08_06Kiểm tra Race Condition: Sản phẩm bị xóa trước khi thanh toán (Phủ: V1 + I6)User có SP B trong giỏ. (Admin vừa vào DB xóa SP B).Bấm nút Checkout trên UI.Cart: SP không tồn tại trong DBThanh toán thất bại. Trả về thông báo lỗi: "Sản phẩm B không còn tồn tại".TC_FR-08_07Kiểm tra quyền truy cập: Gọi API không có Token (Phủ: I1)Giỏ hàng có SP.Dùng Postman xóa header Authorization.Backend từ chối truy cập, trả về lỗi 401 Unauthorized.TC_FR-08_08Kiểm tra quyền truy cập: Token đã hết hạn (Phủ: I2)Giỏ hàng có SP. User đăng nhập từ hôm qua (Token đã hết hạn).Bấm nút Checkout trên UI.Auth: Expired JWTBackend từ chối truy cập (401). Frontend tự động redirect về trang Đăng nhập.
```

### [Prompt 2]

- **Thời gian:** 21:30 09/06/2026
- **Tool:** Gemini 3.1 Pro
- **Prompt:**

```text

```

- **AI Output:**

```text

```
