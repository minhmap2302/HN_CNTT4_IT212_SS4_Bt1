# BÀI 1: Phân tích & Lựa chọn (Thực hành thiết kế prompt tối ưu hóa mã nguồn)

## 1. Đề bài
Hãy lựa chọn prompt tối ưu nhất dưới đây để hướng dẫn AI tái cấu trúc mã nguồn `DiscountService` (Java) sang dạng sử dụng các câu lệnh điều kiện bảo vệ (guard clauses - return sớm) mà vẫn bảo toàn nghiệp vụ cũ. Giải thích lý do lựa chọn và chỉ ra nhược điểm của các phương án còn lại.

### Mã nguồn chưa tối ưu (Java):
```java
public class DiscountService {

    public double calculateDiscount(String type, double amount, boolean isHoliday) {

        if (type.equals("VIP")) {

            if (amount > 1000) {

                if (isHoliday) {

                    return amount * 0.25;

                } else {

                    return amount * 0.20;

                }

            } else {

                return amount * 0.15;

            }

        } else {

            if (amount > 500) {

                if (isHoliday) {

                  return amount * 0.10;

                } else {

                    return amount * 0.05;

                }

            }

        }

        return 0;

    }

 }
```

### Các phương án prompt:
*   **Phương án A:** *"Tái cấu trúc code Java trên để nó đẹp hơn."*
*   **Phương án B:** *"Hãy đóng vai trò là một Java Senior Developer. Nhiệm vụ của bạn là tái cấu trúc (refactor) logic rẽ nhánh lồng nhau phức tạp của class DiscountService trên thành các câu lệnh điều kiện bảo vệ (guard clauses / return sớm). Ràng buộc: Giữ nguyên logic nghiệp vụ tính chiết khấu ban đầu, không thay đổi kiểu dữ liệu đầu vào/đầu ra, sử dụng Java 11. Trình bày kết quả dưới dạng khối mã nguồn Java hoàn chỉnh kèm giải thích ngắn bằng tiếng Việt."*
*   **Phương án C:** *"Hãy sửa code Java này, bỏ bớt if-else lồng nhau đi và sử dụng cấu trúc Java Stream API để viết ngắn gọn nhất có thể."*

---

## 2. Đáp án lựa chọn
**Phương án B** là phương án tối ưu nhất.

---

## 3. Phân tích chi tiết sự tối ưu của Phương án B
Phương án B tích hợp đầy đủ **5 thành phần cốt lõi của một prompt chất lượng cao (Framework Persona-Goal-Context-Constraint-Format)**:

1.  **Vai trò (Persona):** *"Hãy đóng vai trò là một Java Senior Developer."*
    *   **Ý nghĩa:** Định hướng cho AI đóng vai chuyên gia, viết mã nguồn tuân thủ các chuẩn công nghiệp (Clean Code), đặt tên biến tường minh và tối ưu hóa hiệu năng tốt hơn.
2.  **Mục tiêu (Goal):** *"tái cấu trúc (refactor) logic rẽ nhánh lồng nhau phức tạp [...] thành các câu lệnh điều kiện bảo vệ (guard clauses / return sớm)."*
    *   **Ý nghĩa:** Xác định rõ ràng mục đích của prompt và chỉ định chính xác giải pháp kỹ thuật mong muốn (guard clauses/return sớm) để giải quyết tình trạng lồng điều kiện sâu (nested conditions).
3.  **Ngữ cảnh (Context):** Đoạn mã nguồn cũ của class `DiscountService` được đính kèm trực tiếp trong prompt.
4.  **Ràng buộc (Constraints):** *"Giữ nguyên logic nghiệp vụ tính chiết khấu ban đầu, không thay đổi kiểu dữ liệu đầu vào/đầu ra, sử dụng Java 11."*
    *   **Ý nghĩa:** Tránh việc AI tự ý thay đổi chữ ký hàm (method signature) gây lỗi biên dịch ở các module gọi hàm này. Đồng thời đảm bảo logic nghiệp vụ không bị sai lệch sau khi tối ưu.
5.  **Định dạng đầu ra (Format):** *"Trình bày kết quả dưới dạng khối mã nguồn Java hoàn chỉnh kèm giải thích ngắn bằng tiếng Việt."*
    *   **Ý nghĩa:** Đảm bảo sản phẩm đầu ra có thể chạy được ngay mà không bị thiếu thư viện hay cắt xén, đồng thời giúp lập trình viên dễ dàng tiếp thu thông qua phần giải thích.

---

## 4. Phân tích nhược điểm của các phương án còn lại

### Phương án A: *"Tái cấu trúc code Java trên để nó đẹp hơn."*
*   **Nhược điểm:**
    *   **Thiếu chi tiết:** Không có vai trò (Persona), ràng buộc (Constraints) và định dạng đầu ra (Format).
    *   **Thiếu khách quan:** Định nghĩa "đẹp hơn" mang tính chủ quan. AI có thể viết lại theo bất kỳ hướng nào (ví dụ: dùng toán tử ba ngôi phức tạp `? :` hoặc tách hàm không hợp lý) thay vì dùng đúng kỹ thuật guard clauses.
    *   **Nguy cơ:** Dễ dẫn đến việc thay đổi logic nghiệp vụ do không có ràng buộc bảo toàn logic.

### Phương án C: *"Hãy sửa code Java này, bỏ bớt if-else lồng nhau đi và sử dụng cấu trúc Java Stream API để viết ngắn gọn nhất có thể."*
*   **Nhược điểm:**
    *   **Sai lệch kỹ thuật (Over-engineering):** Java Stream API sinh ra để thao tác trên các danh sách/tập hợp dữ liệu (Collection/List). Đoạn code tính toán chiết khấu chỉ xử lý các biến đầu vào đơn lập (`type`, `amount`, `isHoliday`). Việc ép buộc sử dụng Stream API (như bọc các biến này vào `Stream.of` hay `Optional` để filter) làm mã nguồn trở nên rối rắm, khó hiểu, giảm hiệu năng chạy và vi phạm tiêu chí Clean Code.
    *   **Nguy cơ:** Việc cấu trúc lại logic rẽ nhánh đơn lẻ qua Stream API rất dễ gây nhầm lẫn và dẫn đến sai lệch kết quả chiết khấu trả về.
