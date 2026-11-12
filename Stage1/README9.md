### Phần 1: Phân tích nguyên nhân ảo giác (Hallucination) và sự khác biệt phương pháp

#### 1. Lý do AI tự tin đưa ra con số sai
Bản chất của các mô hình ngôn ngữ lớn (LLM) như ChatGPT là một **cỗ máy dự đoán xác suất từ tiếp theo** dựa trên dữ liệu đã được huấn luyện sẵn từ Internet, chứ không phải là một cơ sở dữ liệu tra cứu thông tin nội bộ.

Khi nhân viên Thu mua đặt câu hỏi mà **không kèm tài liệu nguồn** (Zero-shot / Parametric Knowledge), hai hiện tượng sau xảy ra:
* **Khoảng trống dữ liệu nội bộ:** Quy định phạt của riêng công ty MartX là tài liệu bảo mật/nội bộ, hoàn toàn không tồn tại trong bộ dữ liệu huấn luyện công khai của AI.
* **Ảo giác xác suất (Hallucination):** Thay vì thừa nhận "không biết", cơ chế mặc định của LLM là cố gắng làm hài lòng người dùng bằng cách ghép nối các cụm từ có xác suất xuất hiện cao nhất trong các mẫu hợp đồng thương mại phổ biến trên mạng (như *"phạt 20%"*, *"đình chỉ 30 ngày"*). Vì các từ này đi liền với nhau rất mượt mà về mặt ngữ pháp nên AI trả lời với giọng điệu cực kỳ tự tin dù nội dung hoàn toàn bịa đặt.

#### 2. Sự khác biệt cốt lõi giữa hai cách tiếp cận

| Tiêu chí | Hỏi LLM không kèm tài liệu (Đóng sách thi) | RAG Grounding - Dán kèm tài liệu (Mở sách tra cứu) |
| :--- | :--- | :--- |
| **Nguồn thông tin** | Dựa vào "trí nhớ" chung mơ hồ từ Internet (Parametric Memory). | Dựa vào văn bản gốc được cung cấp trực tiếp trong câu lệnh (Context). |
| **Cơ chế xử lý** | Suy đoán xác suất từ ngữ sao cho hợp lý nhất. | Đọc hiểu, đối chiếu và trích xuất thông tin từ vùng dữ liệu giới hạn. |
| **Độ tin cậy nghiệp vụ** | Thấp, dễ bịa đặt số liệu khi gặp quy định riêng của doanh nghiệp. | Rất cao (gần như 100%) nếu đi kèm ràng buộc chống suy đoán. |

---

### Phần 2: Cấu trúc RAG Prompt hoàn chỉnh

Để ngăn chặn triệt để tình trạng AI tự ý "bịa" điều khoản, nhân viên Thu mua cần sử dụng mẫu Prompt áp dụng kỹ thuật **RAG Grounding** (neo giữ dữ liệu nguồn) kết hợp **Negative Constraint** (ràng buộc phủ định) dưới đây:

> **[VAI TRÒ & NHIỆM VỤ]**
> Bạn là trợ lý pháp lý nội bộ của công ty MartX. Nhiệm vụ của bạn là tra cứu chính xác quy định xử phạt từ đoạn trích hợp đồng được cung cấp bên dưới để trả lời câu hỏi nghiệp vụ.
>
> **[1. VĂN BẢN HỢP ĐỒNG CHUẨN (NGUỒN DỮ LIỆU DUY NHẤT)]**
> """
> Điều 4.2 - Quy định về chất lượng hàng hóa nông sản:
> Trường hợp nhà cung cấp giao hàng rau củ quả có tỷ lệ dập nát, hư hỏng vượt quá 10% khối lượng lô hàng, bên mua (MartX) có quyền áp dụng mức phạt vi phạm hành chính bằng 5% giá trị phần lô hàng bị dập nát, đồng thời yêu cầu nhà cung cấp thực hiện đổi bù hàng đạt chuẩn trong vòng 24 giờ kể từ thời điểm lập biên bản.
> """
>
> **[2. CÂU HỎI NGHIỆP VỤ]**
> Theo quy định của MartX, nếu nhà cung cấp giao rau bị dập nát trên 10% thì mức phạt cụ thể là bao nhiêu và thời hạn khắc phục như thế nào?
>
> **[3. NEGATIVE CONSTRAINT (KHÓA AN TOÀN CHỐNG ẢO GIÁC)]**
> - Chỉ được phép sử dụng thông tin nằm trong phần **[1. VĂN BẢN HỢP ĐỒNG CHUẨN]** ở trên để trả lời.
> - Tuyệt đối không sử dụng kiến thức bên ngoài, không suy diễn, không tự thêm bớt bất kỳ con số hay điều khoản nào không có trong văn bản.
> - **Nếu thông tin không có trong văn bản, tuyệt đối trả lời nguyên văn: "Không có dữ liệu trong tài liệu", không tự suy đoán.**
