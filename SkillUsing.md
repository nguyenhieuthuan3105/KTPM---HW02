### 2. Cách tích hợp Skill vào VS Code

Việc gõ phím `\` hoặc `/` để chọn một file prompt template là tính năng của các extension AI nâng cao trong VS Code. Có thể làm theo cách dễ nhất với extension **Continue** (Miễn phí và cực mạnh):

1. **Cài đặt Extension:** Trong VS Code, vào mục Extensions, tìm và cài đặt **Continue** (có icon hình tam giác đứt nét).
2. **Tạo thư mục Prompts:** Mở thư mục gốc dự án bài tập của bạn (HW02). Tạo một thư mục mới có tên là `.prompts`.
3. **Tạo file lệnh Slash (Slash Command):** - Trong thư mục `.prompts`, tạo một file tên là `test_feature.prompt`.
   - Copy toàn bộ nội dung của file `Eshop_QA_Agent_Skill.md` ở trên dán vào file này.
   - Ở DÒNG ĐẦU TIÊN của file `test_feature.prompt`, thêm cấu hình này vào để đặt tên lệnh:

     ```markdown
     name: qa_agent
     description: Phân tích Domain và BVA cho một chức năng EShop

     ---
     ```

     _(Phía dưới dấu `---` là nội dung file skill của bạn)._

4. **Sử dụng để quay Video FR-20:**
   - Mở thanh chat của Continue ở bên trái màn hình VS Code.
   - Bạn chỉ cần gõ `/qa_agent` (Nó sẽ tự động hiện lên gợi ý để bạn click chọn giống hệt bạn của bạn).
   - Sau đó bạn gán thêm phần đặc tả vào:
     > `/qa_agent FR-20: Giỏ hàng (Shopping Cart) trên Mobile. Kiểm thử các thao tác vuốt, chạm, và cập nhật số lượng (Boundary Value cho số lượng min/max) trực tiếp trên màn hình cảm ứng...`
   - Nhấn Enter và quay màn hình khoảnh khắc AI tự động tuôn ra 3 file báo cáo hoàn chỉnh!
