# FR-02

TC_FR-02_01 Đăng nhập thành công
TC_FR-02_02 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Nếu spam đăng nhập liên tục trong thời gian đang bị khóa, thì kể cả thông tin đăng nhập đúng cũng sẽ ko vào được sau 30s spam. Có vẻ nếu muốn đăng nhập thì sau lần đăng nhập bị khóa phải tự chờ đúng hơn 30s rồi mới thực hiện đăng nhập, lúc này mới được. UI khi đang trong trạng thái khóa thì chờ 1 thời gian bấm lại vẫn ko được. PHẢI reset page mới đăng nhập được.
TC_FR-02_03 Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Username
TC_FR-02_04 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_05 Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Mật khẩu
TC_FR-02_06 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_07 Đăng nhập thất bại 2 lần là khóa luôn (tuy nhiên UI không hiển thị đang bị khóa 30s). Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_08 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự.
TC_FR-02_09 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự.

TC_FR-02_BVA_01 Đăng nhập thất bại 2 lần là khóa luôn (tuy nhiên UI không hiển thị đang bị khóa 30s). Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_BVA_02 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_BVA_03 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_BVA_04 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự. Trên thực tế, phải qua 50s, reset lại page rồi mới đăng nhập được.
TC_FR-02_BVA_05 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự. Trên thực tế, phải qua 50s, reset lại page rồi mới đăng nhập được.
TC_FR-02_BVA_06 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự. Trên thực tế, phải qua 50s, reset lại page rồi mới đăng nhập được.

# FR-08

TC_FR-08_01 Thanh toán thành công, tuy nhiên bấm vào giỏ hàng thì thấy vẫn còn nguyên sản phẩm, thậm chí có thể thêm các sản phẩm mới và thanh toán thêm lần nữa với các sản phẩm cũ và mới. Phải bấm reset mới xóa giỏ hàng (Lưu ý có bug ở phần giỏ hàng, chỉ cần reset page thì giỏ hàng sẽ trống ngay lập tức, bất kể là đang có gì, có đăng nhập hay không. Ngược lại miễn là không reset thì kể cả đã đang xuất vẫn thấy được giỏ hàng của tài khoản đăng nhập trước đó, mọi hành động thêm vào giỏ hàng ở trạng thái ko đăng nhập khi đăng nhập thì sẽ giữ nguyên sản phẩm).
TC_FR-08_02 Sử dụng UI để sửa tổng tiền thành 0 sau đó bấm thanh toán, vẫn hiển thị thanh toán thành công.
TC_FR-08_03 Sử dụng UI để sửa tổng tiền thành -10 sau đó bấm thanh toán, vẫn hiển thị thanh toán thành công.
TC_FR-08_04 Sau khi hiển thị thanh toán thành công, có thể bấm reset để cho ra 1 trang thanh toán rỗng không có sản phẩm với tổng tiền 1. Bấm thanh toán lần nữa và vẫn hiển thị thanh toán thành công.
TC_FR-08_05 Bỏ qua
TC_FR-08_06 Bỏ qua
TC_FR-08_07 Backend không trả về HTTP Status 401 như kỳ vọng. Thay vào đó, do lỗi cấu hình bảo mật ở Middleware, trình duyệt đã văng lỗi CORS (Cross-Origin Resource Sharing) policy và chặn request.
TC_FR-08_08 Backend không trả về HTTP Status 401 như kỳ vọng. Thay vào đó, do lỗi cấu hình bảo mật ở Middleware, trình duyệt đã văng lỗi CORS (Cross-Origin Resource Sharing) policy và chặn request.
TC_FR-08_09 Hệ thống hiển thị thông báo lỗi yêu cầu đăng nhập và chuyển hướng về trang đăng nhập đúng như kỳ vọng.

TC_FR-08_BVA_01 Ở trang chi tiết của sản phẩm, chỉnh số lượng về 0 và nhấn thêm giỏ hàng, sau khoảng 3s thì sẽ hiện UI "Đã thêm" thoáng qua khoảng 1s rồi trở lại bình thường (Đây là bug của phần giỏ hàng hoặc xem chi tiết nên tôi sẽ không bắt ở đây) Sau đó tôi vào giỏ hàng và thanh toán đơn hàng số lượng 0 đó 1 cách bình thường. Hệ thống hiển thị thanh toán thành công. Đây là bug 12 (lưu ý có thể bị nhầm với bug đơn hàng rỗng trước đó).
TC_FR-08_BVA_02 Hệ thống hiển thị thanh toán thành công với giá tiền chính xác.
TC_FR-08_BVA_03 Hệ thống hiển thị thanh toán thành công với giá tiền chính xác.
TC_FR-08_BVA_04 Hệ thống hiển thị thanh toán thành công với giá tiền chính xác.
TC_FR-08_BVA_05 Hệ thống hiển thị thanh toán thành công với giá tiền chính xác.
