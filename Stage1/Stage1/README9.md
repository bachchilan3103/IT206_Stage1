# BÀI LÀM: RAG GROUNDING VÀ NEGATIVE CONSTRAINT TẠI MARTX

## PHẦN 1. PHÂN TÍCH NGUYÊN NHÂN ẢO GIÁC

ChatGPT đưa ra mức phạt 20% và đình chỉ nhập hàng 30 ngày vì nhân viên Thu mua không cung cấp hợp đồng hoặc tài liệu quy định riêng của MartX.

LLM hoạt động dựa trên cơ chế **Next Token Prediction** (dự đoán token tiếp theo), tức là dự đoán nội dung tiếp theo dựa trên các mẫu dữ liệu đã học trong giai đoạn **Pre-training**.

Khi không có tài liệu nguồn để đối chiếu, AI có thể dựa vào kiến thức chung để tạo ra câu trả lời nghe hợp lý nhưng không đúng với quy định thực tế. Đây là hiện tượng **Hallucination (ảo giác AI)**.

Vì vậy, không nên sử dụng câu trả lời của AI làm căn cứ xử phạt khi chưa kiểm tra hợp đồng thực tế.

## PHẦN 2. XÂY DỰNG RAG PROMPT HOÀN CHỈNH

### Prompt đề xuất

```text
Bạn là trợ lý hỗ trợ nghiệp vụ Thu mua của siêu thị MartX.
Hãy chỉ sử dụng thông tin trong tài liệu được cung cấp để trả lời.

1. VĂN BẢN HỢP ĐỒNG CHUẨN:

"Nhà cung cấp giao rau có tỷ lệ dập nát trên 10%:
Phạt 5% giá trị lô hàng bị dập nát và yêu cầu đổi hàng trong vòng 24 giờ."

2. CÂU HỎI NGHIỆP VỤ:

Theo hợp đồng MartX, nếu nhà cung cấp giao rau
bị dập nát trên 10% thì bị xử lý như thế nào?

Hãy nêu rõ:
- Mức phạt.
- Giá trị dùng để tính tiền phạt.
- Thời hạn đổi hàng.

3. NEGATIVE CONSTRAINT (KHÓA AN TOÀN):

- Chỉ sử dụng thông tin có trong văn bản hợp đồng.
- Không sử dụng kiến thức bên ngoài để tự bổ sung điều khoản.
- Không tự suy đoán hoặc tạo ra mức phạt và thời hạn khác.
- Nếu thông tin không có trong văn bản, tuyệt đối trả lời:
  "Không có dữ liệu trong tài liệu".
- Trình bày ngắn gọn, đúng nội dung hợp đồng.
```

### Kết quả trả lời theo tài liệu

- Mức phạt: 5% giá trị lô hàng bị dập nát.
- Yêu cầu: Nhà cung cấp phải đổi hàng.
- Thời hạn đổi hàng: Trong vòng 24 giờ.

RAG Grounding giúp AI trả lời dựa trên tài liệu nguồn cụ thể thay vì tự suy đoán. Negative Constraint giúp hạn chế thông tin bịa đặt và yêu cầu AI không tự đưa ra kết luận khi tài liệu không có dữ liệu.