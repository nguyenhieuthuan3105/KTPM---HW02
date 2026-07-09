# AI Critique

```text
Sau khi sử dụng Gemini 3.1 Pro và Copilot trong quá trình thực hiện bài tập, tôi nhận thấy rằng việc áp dụng AI trong việc hỗ trợ thực hiện Domain Testing và Boundary Value Analysis mang lại lợi ích lớn về tốc độ, nhưng cũng bộc lộ nhiều hạn chế và xuất hiện tình trạng hallucination mà cần sự kiểm duyệt và chỉnh sửa của con người.

Điểm yếu lớn nhất của AI là xu hướng áp đặt kiến thức chung (general knowledge) vào một hệ thống phần mềm đặc thù. Cụ thể, trong FR-08, AI tự vẽ ra các kịch bản kiểm tra tồn kho (stock) dù hệ thống EShop SUT hoàn toàn không có tính năng này. Tại FR-13, AI lại tự sáng tạo ra trạng thái đơn hàng processing không hề tồn tại trong tài liệu đặc tả State Machine. Ở FR-20, AI vội vàng kết luận rằng khi giảm số lượng về 0 thì hệ thống sẽ tự xóa sản phẩm khỏi giỏ, đồng thời bỏ qua luôn yêu cầu hiển thị hộp thoại (Dialog) xác nhận xóa, thứ mà vốn được nói tới rõ ràng trong đặc tả.

Thêm vào đó, AI tỏ ra thiếu hụt tư duy tổng thể về kiến trúc State Management (Client-Server). Khi phân tích FR-08 và FR-20, nó tập trung phân tích cục bộ mà bỏ quên biến trạng thái cốt lõi là Phiên Đăng nhập (Session) cũng như luồng thao tác của Khách vãng lai (Guest) trên UI. Điều này khiến AI không thiết kế ra dược các test case có thể phát hiện được những bug có rủi ro bảo mật như Bug 19 (Rò rỉ dữ liệu giỏ hàng khi người dùng Đăng xuất).

Cuối cùng, nếu không bị ép buộc bằng các định dạng Agent Skill nghiêm ngặt, AI thường xuyên dùng dữ liệu giả định không thực tế (ví dụ: user@example.com) và bỏ sót các cột báo cáo quan trọng như Verdict hay Actual Result. Thậm chí kể cả khi sử dụng Agent Skill, AI cũng không thực hiện liền mạch toàn bộ theo đặc tả các bước của skill mà thực hiện lòng vòng các hạng mục rồi mới trả về kết quả cuối cùng.

Tóm lại, AI là một trợ lý đắc lực để tổng hợp dữ liệu đặc tả, tạo template và sinh test case thô, nhưng Tester bắt buộc phải đối chiếu sát sao với đặc tả gốc và sử dụng Agent Skill để ép AI tuân thủ đúng giới hạn của hệ thống.
```
