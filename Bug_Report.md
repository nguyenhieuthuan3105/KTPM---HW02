# Bug Report

**MSSV:** 23127125 </br>
**Họ và tên:** Nguyễn Hiếu Thuận </br>
**Bài tập:** HW02 - Domain Testing </br>
**Chức năng:** FR-02 (Đăng nhập & Khóa tài khoản)

---

## Danh sách Lỗi (Bugs) phát hiện được trên SUT

### 1. Bug 1: Sai logic khóa tài khoản (Khóa ở lần 2 thay vì lần 3)

- **Mô tả:** Theo đặc tả, tài khoản chỉ bị tạm khóa khi nhập sai từ 3 lần trở lên liên tiếp. Tuy nhiên, thực tế hệ thống đã khóa tài khoản ngay ở lần nhập sai thứ 2.
- **Test Case phát hiện:** `TC_FR-02_07`, `TC_FR-02_BVA_01`
- **GitHub Issue:** [Link Issue #1]
- **Ảnh minh chứng:**
  ![Bug 1](images/bug1.png)

### 2. Bug 2: Không hiển thị thông báo "Tài khoản bị tạm khóa" (UI/UX)

- **Mô tả:** Khi tài khoản rơi vào trạng thái khóa, hệ thống không trả về thông báo lỗi chi tiết như yêu cầu ("Tài khoản bị tạm khóa 30s") mà chỉ hiển thị thông báo chung chung "Đăng nhập thất bại, vui lòng kiểm tra lại". Điều này gây hoang mang cho người dùng.
- **Test Case phát hiện:** `TC_FR-02_08`, `TC_FR-02_09`, `TC_FR-02_BVA_03`
- **GitHub Issue:** [Link Issue #2]
- **Ảnh minh chứng:**
  ![Bug 2](images/bug2.png)

### 3. Bug 3: Lỗi đồng bộ trạng thái Frontend (Phải F5 mới đăng nhập lại được)

- **Mô tả:** Sau khi hết thời gian phạt 30 giây, nếu người dùng tiếp tục nhấn nút Đăng nhập thì vẫn không thành công. Người dùng bắt buộc phải F5 (tải lại toàn bộ trang) thì mới có thể đăng nhập lại bình thường. Frontend không tự động reset state timeout.
- **Test Case phát hiện:** `TC_FR-02_02`, `TC_FR-02_BVA_05`, `TC_FR-02_BVA_06`
- **GitHub Issue:** [Link Issue #3]
- **Ảnh minh chứng:**
  ![Bug 3](images/bug3.png)

### 4. Bug 4: Thiếu Validation chuẩn HTML5 ở trường Email

- **Mô tả:** Ô nhập Email ở Frontend đang thiếu ràng buộc validate theo định dạng email chuẩn (ví dụ: thiếu ký tự `@` nhưng vẫn submit được). Form vẫn đẩy request sai định dạng xuống tận Backend xử lý thay vì chặn ngay tại UI.
- **Test Case phát hiện:** `TC_FR-02_04`
- **GitHub Issue:** [Link Issue #4]
- **Ảnh minh chứng:**
  ![Bug 4](images/bug4.png)

### 5. Bug 5: Sai thời gian phạt khóa tài khoản (Khóa 50s thay vì 30s)

- **Mô tả:** Theo đặc tả (FR-02), khi người dùng nhập sai quá số lần quy định, tài khoản sẽ bị tạm khóa trong **30 giây**. Tuy nhiên, thực tế kiểm thử cho thấy hệ thống từ chối đăng nhập ở các mốc 30s và 31s. Người dùng phải chờ đến hơn **50 giây** (và kết hợp tải lại trang) thì mới có thể đăng nhập lại thành công.
- **Test Case phát hiện:** `TC_FR-02_02`, `TC_FR-02_BVA_05`, `TC_FR-02_BVA_06`
- **GitHub Issue:** [Link Issue #5]
- **Ảnh minh chứng:**
  ![Bug 5](images/bug5.png)
