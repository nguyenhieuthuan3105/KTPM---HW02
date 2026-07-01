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

# FR-13

TC_FR-13_01 Dashboard hiển thị tổng số đơn hàng bằng 0 Và tổng doanh thu bằng 0. Pass
TC_FR-13_02 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 60.000.000. Fail
TC_FR-13_03 Dashboard hiển thị tổng số đơn hàng bằng 3 Và tổng doanh thu bằng 0. Pass
TC_FR-13_04 Dashboard hiển thị tổng số đơn hàng bằng 4 Và tổng doanh thu bằng 116.000.000. Fail (Tương tự với bug của TC_FR-13_02)
TC_FR-13_05 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 0. Pass (Tuy nhiên bug vẫn có, vô tình đúng do 0 x 2 = 0)
TC_FR-13_06 Dashboard hiển thị tổng số đơn hàng bằng 6 Và tổng doanh thu bằng 56.000.000. Fail (Tương tự với bug của TC_FR-13_02 do giá tiền bị x2 đối với mỗi đơn thành công, còn về mặt tính toán thì đơn hàng vẫn thực hiện doanh thu âm với tính toán chính xác)

TC_FR-13_BVA_01 Dashboard hiển thị tổng số đơn hàng bằng 0 Và tổng doanh thu bằng 0. Pass
TC_FR-13_BVA_02 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 60.000.000. Pass
TC_FR-13_BVA_03 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 2.100.000.000. Pass
TC_FR-13_BVA_04 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 2.160.000.000. Pass
TC_FR-13_BVA_05 Dashboard hiển thị tổng số đơn hàng bằng 1 Và tổng doanh thu bằng 600.000.000.000.000 (Đúng với đặc tả lỗi x2). Tuy nhiên khi kéo dãn UI thì số bị tràn ra khỏi box. Fail (bug 14: Ô tổng doanh thu không responsive)
TC_FR-13_BVA_06 F12 để chỉnh sửa trực tiếp html thành 999.999.999.999.999. Kkhi kéo dãn UI thì số bị tràn ra khỏi box. Fail. (Chưa test hiệu năng Backend do giới hạn môi trường local). (Bug 15: Ô tổng đơn hàng không responsive)

# FR-20

(bug16) Khi vừa mở giỏ hàng UI đã không hiển thị nút "+/-" trên dòng sản phẩm. Dòng hiển thị là "Tổng tạm tính" chứ không phải "Tổng cộng" như đặc tả.

TC_FR-20_01 Không có chuyện gì xảy ra. Số lượng và sản phẩm trong giỏ vẫn giữ nguyên bình thường. Pass
TC_FR-20_02 Sản phẩm bị xóa khỏi giỏ, danh sách cập nhật ngay, tổng tiền về 0đ vì không còn sản phẩm nào khác. Fail (vì không có dialog) (bug17)
TC_FR-20_03 Trong mục số lượng của sản phẩm. Nếu chọn số hiện tại và thay bằng "1" thì sẽ bình thường, tuy nhiên nếu thay bằng bất kì số nào khác thì sẽ "số đó + 1". Trong ảnh chụp minh chứng bug (bug18) tôi đã nhập "2" và nó lập tức thành "3" và giá tiền thành 90.000.000đ. Fail
TC_FR-20_04 Số lượng hiển thị thành 1, sản phẩm vẫn còn trong giỏ, tổng tiền cập nhật thành 30.000.000đ.
TC_FR-20_05 Số lượng hiển thị thành 1, sản phẩm vẫn còn trong giỏ. Pass
TC_FR-20_06 Hệ thống không chọn nhầm sản phẩm, không thay đổi số lượng và không làm thay đổi tổng tiền. Pass

TC_FR-20_BVA_01 Số lượng hiển thị thành 1, sản phẩm vẫn còn trong giỏ. Pass
TC_FR-20_BVA_02 Sản phẩm vẫn hiển thị trong giỏ, tổng tiền hiển thị đúng 30.000.000đ. Pass
TC_FR-20_BVA_03 Sản phẩm vẫn hiển thị trong giỏ, tổng tiền hiển thị đúng 60.000.000đ. Pass
TC_FR-20_BVA_04 Sản phẩm biến mất khỏi giỏ, danh sách cập nhật ngay, tổng tiền về 0đ khi không còn sản phẩm nào khác. Fail (vì không hiện dialog)
TC_FR-20_BVA_05 Hệ thống không bị lỗi giao diện, không crash và vẫn hiển thị trạng thái giỏ rỗng bình thường. Pass

(bug19) Đăng nhập rồi chọn 1 sản phẩm vào giỏ hàng. Sau đó đăng xuất thì giỏ hàng vẫn chứa sản phẩm đó.
