Đây là file quan trọng nhất. Trong file này, bạn sẽ trình bày chi tiết từng bước (step-by-step) cách áp dụng kỹ thuật Domain Testing và Boundary Value Analysis cho 4 chức năng đã chọn (FR-02, FR-08, FR-13, FR-20). Bạn cũng sẽ ghi nhận phần AI Gap Analysis (những gì AI bỏ sót) tại đây.

# Main Report

**MSSV:** 23127125 </br>
**Họ và tên:** Nguyễn Hiếu Thuận </br>
**Bài tập:** HW02 - Domain Testing

---

## FR-02: Đăng nhập & Khóa tài khoản

### Domain Testing

Để thực hiện Domain Testing cho FR-02, trước tiên tôi tiến hành xác định các biến đầu vào (Email, Mật khẩu) và biến trạng thái (Số lần sai). Sau đó, tôi phân chia miền giá trị hợp lệ/không hợp lệ cho từng biến dựa trên ràng buộc của HTML5 và logic của backend.

**Phân tích Miền giá trị (Domain Analysis):** Dựa trên đặc tả hệ thống, chức năng Đăng nhập bao gồm 2 biến đầu vào (Email, Password), 1 biến trạng thái (Số lần đăng nhập sai) và các kết quả đầu ra tương ứng.

1.  **Biến đầu vào:** Email (Input Variable): Biến này chịu sự ràng buộc của validate HTML5 type="email" ở Frontend và kiểm tra tồn tại ở Backend.

    **Miền hợp lệ (Valid Domains):**
    - V1: Email đúng định dạng chuẩn HTML5 (VD: user@example.com) VÀ đã được đăng ký trong hệ thống.

    **Miền không hợp lệ (Invalid Domains):**
    - I1 (Empty): Bỏ trống trường Email.
    - I2 (Invalid Format): Email sai định dạng HTML5 (VD: thiếu @, thiếu tên miền như userexample.com, user@.com).
    - I3 (Unregistered): Email đúng định dạng HTML5 nhưng chưa được đăng ký trong hệ thống.

2.  **Biến đầu vào:** Mật khẩu (Input Variable): Biến này được đánh giá thông qua việc đối chiếu với cơ sở dữ liệu dựa trên Email hợp lệ.

    **Miền hợp lệ (Valid Domains):**
    - V2: Chuỗi ký tự khớp chính xác 100% (có phân biệt hoa/thường) với mật khẩu đã lưu của Email.

    **Miền không hợp lệ (Invalid Domains):**
    - I4 (Empty): Bỏ trống trường Mật khẩu.
    - I5 (Mismatch): Chuỗi ký tự không khớp với mật khẩu của Email tương ứng.

3.  **Biến trạng thái:** Số lần đăng nhập sai (State Variable): Đây là biến ẩn quyết định luồng khóa tài khoản. Phụ thuộc vào Bộ đếm (Counter) và Thời gian chờ (Timeout).

    **Miền hợp lệ - Trạng thái Hoạt động (Active State):**
    - S1: Attempts = 0 (Đăng nhập lần đầu hoặc đã reset bộ đếm sau khi đăng nhập thành công).
    - S2: Attempts = 1 hoặc 2 (Đã sai 1-2 lần liên tiếp, tài khoản vẫn được phép thử tiếp).
    - S3: Attempts >= 3 VÀ Thời gian từ lần sai cuối >= 30 giây (Đã hết thời gian phạt, tài khoản được mở khóa).

    **Miền không hợp lệ - Trạng thái Tạm khóa (Locked State):**
    - S4: Attempts >= 3 VÀ Thời gian từ lần sai cuối < 30 giây (Tài khoản đang bị khóa, từ chối mọi yêu cầu đăng nhập).

4.  **Miền kết quả kỳ vọng (Expected Output Domains):** Dựa trên tổ hợp của các miền giá trị trên, hệ thống sẽ trả về các kết quả sau:
    - O1 (Thành công): Xảy ra khi (V1 + V2) + (S1 hoặc S2 hoặc S3). Trạng thái: Trả về JWT Token, reset bộ đếm số lần sai về 0.
    - O2 (Lỗi Validation UI): Xảy ra khi I1, I4 hoặc I2. Trạng thái: Frontend chặn submit, hiển thị thông báo yêu cầu nhập đúng định dạng.
    - O3 (Lỗi Thông tin - Bảo mật): Xảy ra khi (I3 hoặc I5) + (S1 hoặc S2 hoặc S3). Trạng thái: Hệ thống tăng bộ đếm lên 1. Trả về thông báo lỗi chung chung (VD: "Email hoặc mật khẩu không chính xác") để không để lộ chi tiết nguyên nhân.
    - O4 (Lỗi Tạm khóa): Xảy ra khi vi phạm S4. Trạng thái: Trả về thông báo tài khoản đang bị tạm khóa, không thực hiện xác thực Email/Password.

**Thiết kế Test Case (Domain Testing)**
Dựa trên các miền giá trị đã phân tích, dưới đây là tập hợp các Test Case đại diện nhằm đảm bảo bao phủ toàn bộ các kịch bản kết quả (O1, O2, O3, O4) mà không gây ra dư thừa tổ hợp:

| Test Case ID | Tên (Test Objective)                                                | Đầu vào (Test Data)                                           | Kết quả mong đợi (Expected Result)                        | Kết quả thực tế (Actual Result)                                                                           | Status |
| ------------ | ------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------ |
| TC_FR-02_01  | Kiểm tra đăng nhập thành công                                       | Email: test@eshop.com<br>Pass: Test1234!                      | Đăng nhập thành công, trả về JWT Token.                   | Đăng nhập thành công.                                                                                     | Pass   |
| TC_FR-02_02  | Kiểm tra đăng nhập thành công sau khi hết thời gian phạt            | Email: test@eshop.com<br>Pass: Test1234!                      | Đăng nhập thành công.                                     | Đăng nhập thất bại ở mốc >30s. Thực tế phải chờ qua 50s và reload lại trang (F5) mới đăng nhập được.      | Fail   |
| TC_FR-02_03  | Kiểm tra validation UI khi bỏ trống Email                           | Email: (bỏ trống)<br>Pass: Test1234!                          | Frontend chặn submit, hiển thị lỗi yêu cầu nhập Email.    | Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Username.                             | Pass   |
| TC_FR-02_04  | Kiểm tra validation UI khi Email sai định dạng                      | Email: testeshop.com<br>Pass: Test1234!                       | Frontend chặn submit, hiển thị lỗi định dạng HTML5.       | Request vẫn được gửi đi. Frontend hiện thông báo từ Backend: “Đăng nhập thất bại, vui lòng kiểm tra lại”. | Fail   |
| TC_FR-02_05  | Kiểm tra validation UI khi bỏ trống Password                        | Email: test@eshop.com<br>Pass: (bỏ trống)                     | Frontend chặn submit, hiển thị lỗi yêu cầu nhập Mật khẩu. | Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Mật khẩu.                             | Pass   |
| TC_FR-02_06  | Kiểm tra lỗi bảo mật khi Email chưa đăng ký                         | Email: new@example.com<br>Pass: AnyPass123                    | Trả về lỗi chung ("Email hoặc mật khẩu không đúng").      | Frontend hiện: “Đăng nhập thất bại, vui lòng kiểm tra lại”.                                               | Pass   |
| TC_FR-02_07  | Kiểm tra lỗi bảo mật khi sai Password và đẩy lên giới hạn khóa      | Email: test@eshop.com<br>Pass: WrongPass!<br>State: 2 lần sai | Trả về lỗi chung, tăng bộ đếm lên 3 (tạm khóa).           | Hệ thống khóa tài khoản ngay ở lần đăng nhập thất bại thứ 2. UI không có thông báo khóa.                  | Fail   |
| TC_FR-02_08  | Kiểm tra từ chối đăng nhập khi tài khoản đang bị khóa, dù nhập đúng | Email: test@eshop.com<br>Pass: Test1234!<br>State: đang khóa  | Trả về thông báo tài khoản đang bị tạm khóa.              | Chỉ hiện thông báo chung: “Đăng nhập thất bại, vui lòng kiểm tra lại”. Không thông báo bị khóa.           | Fail   |
| TC_FR-02_09  | Kiểm tra từ chối đăng nhập khi tài khoản đang bị khóa, nhập sai     | Email: fake@example.com<br>Pass: FakePass<br>State: đang khóa | Trả về thông báo tài khoản đang bị tạm khóa.              | Chỉ hiện thông báo chung: “Đăng nhập thất bại, vui lòng kiểm tra lại”. Không thông báo bị khóa.           | Fail   |

### Boundary Value Analysis (BVA)

**Phân tích các giá trị biên (Step-by-step Explanation):** Tôi tập trung vào 2 ranh giới quyết định việc thay đổi trạng thái của hệ thống: số lần đăng nhập sai và thời gian tạm khóa tài khoản.

1. Ranh giới số lần đăng nhập sai (Ngưỡng n = 3):

- Just below the boundary (n = 2): Kiểm tra khi người dùng nhập sai lần thứ 2. Hệ thống phải ghi nhận lỗi nhưng tài khoản vẫn ở trạng thái hoạt động.
- On the boundary (n = 3): Kiểm tra khi người dùng nhập sai ở đúng lần thứ 3. Đây là điểm trigger kích hoạt trạng thái tạm khóa.
- Just above the boundary (n = 4): Kiểm tra khi người dùng tiếp tục gửi request đăng nhập lần thứ 4 (khi tài khoản vừa bị khóa). Hệ thống phải lập tức từ chối mà không cần kiểm tra DB.

2. Ranh giới thời gian tạm khóa (Ngưỡng t = 30s):

- Just below the boundary (t = 29s): Cố gắng thực hiện đăng nhập khi thời gian phạt chưa kết thúc (còn thiếu 1 giây). Hệ thống vẫn phải hiển thị lỗi bị khóa.
- On the boundary (t = 30s): Cố gắng thực hiện đăng nhập ngay tại thời điểm mốc phạt vừa chạm tới. Hệ thống phải cho phép xác thực (mở khóa tài khoản).
- Just above the boundary (t = 31s): Cố gắng đăng nhập khi thời gian phạt đã qua mức an toàn. Hệ thống phải tiếp nhận request bình thường.

**Thiết kế Test Case (BVA Testing):** Dưới đây là các Test Case chi tiết để kiểm thử các giá trị biên đã phân tích:

| Test Case ID        | Tên (Test Objective)                        | Điều kiện tiền quyết (Precondition)          | Đầu vào (Test Data)                                                       | Kết quả mong đợi (Expected Result)                                                 | Kết quả thực tế (Actual Result)                                                                                                          | Status |
| :------------------ | :------------------------------------------ | :------------------------------------------- | :------------------------------------------------------------------------ | :--------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------- | :----- |
| **TC_FR-02_BVA_01** | Kiểm tra biên dưới số lần sai (n = 2)       | Tài khoản hợp lệ, bộ đếm đang là 1           | Email: test@eshop.com<br>Password: WrongPass!<br>State: 1 lần sai         | Hệ thống báo lỗi thông tin không đúng, tăng bộ đếm lên 2, tài khoản không bị khóa. | Hệ thống khóa tài khoản ngay ở lần đăng nhập thất bại thứ 2. Frontend chỉ hiện: “Đăng nhập thất bại, vui lòng kiểm tra lại”.             | Fail   |
| **TC_FR-02_BVA_02** | Kiểm tra tại biên số lần sai (n = 3)        | Tài khoản hợp lệ, bộ đếm đang là 2           | Email: test@eshop.com<br>Password: WrongPass!<br>State: 2 lần sai         | Hệ thống báo lỗi tài khoản bị tạm khóa 30s, tăng bộ đếm lên 3.                     | Chỉ hiện thông báo chung: “Đăng nhập thất bại, vui lòng kiểm tra lại”. (Tài khoản thực tế đã bị khóa từ lần 2).                          | Fail   |
| **TC_FR-02_BVA_03** | Kiểm tra vượt biên số lần sai (n = 4)       | Tài khoản vừa bị khóa, bộ đếm đang là 3      | Email: test@eshop.com<br>Password: AnyPass123<br>State: 3 lần sai         | Hệ thống từ chối đăng nhập ngay lập tức, báo lỗi tài khoản đang bị tạm khóa.       | Chỉ hiện thông báo chung: “Đăng nhập thất bại, vui lòng kiểm tra lại”, không có thông báo báo bị khóa.                                   | Fail   |
| **TC_FR-02_BVA_04** | Kiểm tra biên dưới thời gian khóa (t = 29s) | Tài khoản đang bị khóa, vừa trôi qua 29 giây | Email: test@eshop.com<br>Password: Test1234!<br>State: 3 lần sai, t = 29s | Đăng nhập thất bại, hệ thống báo lỗi tài khoản vẫn đang bị khóa.                   | Đăng nhập thất bại. Frontend hiện “Đăng nhập thất bại...”. Kể cả F5 lại trang vẫn không đăng nhập được (thực tế phải chờ >50s).          | Fail   |
| **TC_FR-02_BVA_05** | Kiểm tra tại biên thời gian khóa (t = 30s)  | Tài khoản bị khóa, vừa trôi qua đúng 30 giây | Email: test@eshop.com<br>Password: Test1234!<br>State: 3 lần sai, t = 30s | Đăng nhập thành công, trả về JWT Token, reset bộ đếm số lần sai về 0.              | Đăng nhập thất bại dù đã đúng 30s. Frontend hiện lỗi “Đăng nhập thất bại...”. Phải chờ qua 50s và tải lại trang (F5) thì mới thành công. | Fail   |
| **TC_FR-02_BVA_06** | Kiểm tra vượt biên thời gian khóa (t = 31s) | Tài khoản bị khóa, đã trôi qua 31 giây       | Email: test@eshop.com<br>Password: Test1234!<br>State: 3 lần sai, t = 31s | Đăng nhập thành công, trả về JWT Token, reset bộ đếm số lần sai về 0.              | Đăng nhập thất bại dù đã qua 31s. Frontend hiện lỗi “Đăng nhập thất bại...”. Phải chờ qua 50s và tải lại trang (F5) thì mới thành công.  | Fail   |

## AI Gap Analysis

## AI Gap Analysis

1. **Sai thông tin tài khoản test:**
   - AI tạo testcase mặc định với: `Email: user@example.com` và `Password: Abc@123`
   - Trong khi thực tế môi trường SUT sử dụng tài khoản: `test@eshop.com` / `Test1234!`
   - **Lý do:** Do câu prompt ban đầu của tôi chỉ tập trung vào logic chức năng mà chưa cung cấp bộ Test Data chuẩn (mock data) của dự án cho AI, dẫn đến AI tự tạo ra data giả.

2. **Thiếu format phục vụ Test Execution:**
   - AI tạo format bảng Test Case bị thiếu 2 cột quan trọng là `Kết quả thực tế (Actual Result)` và `Trạng thái (Status)`.
   - **Lý do:** Prompt của tôi yêu cầu AI "thiết kế" (Design) test case chứ chưa yêu cầu chuẩn bị form cho việc "thực thi" (Execution). AI chỉ tuân thủ đúng giới hạn của việc thiết kế.

## Bug Reporting

Toàn bộ danh sách lỗi phát hiện được từ các Test Case trên đã được báo cáo chi tiết kèm ảnh chụp màn hình và link GitHub Issues trong file đính kèm `Bug_Report.md`
