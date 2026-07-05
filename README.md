# HW02 - Domain Testing & BVA Submission

**Sinh viên:** Nguyễn Hiếu Thuận <br/>
**MSSV:** 23127125

## 1. Test Summary Report

Dưới đây là thống kê tổng quan về quá trình kiểm thử áp dụng kỹ thuật Domain Testing và Boundary Value Analysis cho 4 chức năng:

- **Tổng số lượng chức năng (Features) đã test:** 4 (FR-02, FR-08, FR-13, FR-20)
- **Tổng số Test Cases thiết kế:** 53
  - _FR-02:_ 15 TCs (9 Domain + 6 BVA)
  - _FR-08:_ 14 TCs (9 Domain + 5 BVA)
  - _FR-13:_ 12 TCs (6 Domain + 6 BVA)
  - _FR-20:_ 12 TCs (7 Domain + 5 BVA)
- **Tổng số Test Cases đã thực thi (Executed):** 52
- **Tổng số Test Cases CHƯA thực thi (Not Executed):** 1 _(TC_FR-08_05 - N/A do hệ thống không có tính năng Inventory/Stock)_
- **Tổng số Test Cases Passed:** 21
- **Tổng số Test Cases Failed:** 31
- **Tổng số lỗi (Bugs) phát hiện được:** 20 Bugs _(Đã log chi tiết trên GitHub Issues)_

## 2. Agent Skill Demonstration

- **Agent Skill:** Được thiết kế để tự động hóa luồng phân tích Domain Testing, BVA, kiểm soát Hallucination của AI và chuẩn hóa form báo cáo Markdown.
- **YouTube Demo Link:** [LINK YOUTUBE](https://youtu.be/H9EO3nrwjNE)

### Hướng dẫn sử dụng Skill (Skill Usage)

Để sử dụng Agent Skill này cho một chức năng mới, vui lòng cung cấp file `Eshop_QA_Agent_Skill.md` cho AI và sử dụng câu lệnh (prompt) theo định dạng sau:

> Vui lòng đọc kỹ hướng dẫn trong file đính kèm và đóng vai trò Eshop QA Agent. Hãy áp dụng toàn bộ kỹ năng đó để xử lý chức năng sau, lưu ý không hỏi thêm bất cứ thứ gì và chỉ thực hiện đúng yêu cầu được đặt ra:
>
> **FR-XX: [Điền số hiệu và tên chức năng]**
> **Đặc tả:**
>
> - [Copy trực tiếp nội dung đặc tả cần phân tích và tạo testcase vào đây]
> - ...

## 3. Self-Assessment Table

Căn cứ vào khối lượng công việc, chất lượng phân tích (bắt được các bug sâu như Race Condition, Tràn số) và việc xây dựng thành công Agent Skill, tôi tự đánh giá điểm số như sau:

| No.       | Criteria                                      | Grade   | Self-Assessed Grade |
| :-------- | :-------------------------------------------- | :------ | :------------------ |
| 1         | Feature A (FR-02) (Domain + Boundary)         | 25      | 25                  |
| 2         | Feature B (FR-08) (Domain + Boundary)         | 25      | 25                  |
| 3         | Feature C (FR-13) (Domain + Boundary)         | 25      | 25                  |
| 4         | Feature D (FR-20) (Mobile, Domain + Boundary) | 15      | 15                  |
| 5         | Agent Skills                                  | 10      | 10                  |
| **Total** |                                               | **100** | **100**             |
