

### Phần 1: Giải thích hình tượng "Chiếc cốc nước" và hiện tượng Truncation

Để hiểu tại sao AI lại "quên" mất thông tin ở Lượt 1 sau một hồi tư vấn dài dòng, hãy hình dung **Context Window (Cửa sổ ngữ cảnh)** giống như **một chiếc cốc nước có dung tích cố định** (ví dụ: giới hạn 32.000 tokens):

* **Nước trong cốc là gì?** Mỗi câu hỏi của khách hàng và câu trả lời của AI đều được quy đổi thành các "token" (từ/âm tiết) và được rót liên tục vào cốc theo thứ tự thời gian.
* **Lượt 1 ở đâu?** Thông tin *"Tôi tên Trần Văn B, mã đơn hàng #MTX-9988"* nằm ở đáy cốc – là những giọt nước đầu tiên được rót vào phiên chat.
* **Tại sao cốc lại đầy?** Qua 40 lượt tư vấn dông dài về rau củ, lượng thông tin tích lũy đã phình to lên đúng mức 32.000 tokens. Chiếc cốc lúc này đã hoàn toàn chạm đến vạch tối đa (100%).
* **Hiện tượng Truncation (Tràn cốc & Cắt gọt):** Khi Lượt 42 diễn ra, một lượng "nước mới" lại được rót thêm vào. Vì cốc đã đầy, quy luật hoạt động của AI buộc phải đẩy những giọt nước cũ nhất ở đáy cốc tràn ra ngoài (biến mất khỏi bộ nhớ tạm thời).

**Kết quả:** Thông tin định danh ở Lượt 1 đã bị văng khỏi vùng đọc của AI. Do đó, khi nghe câu hỏi ở Lượt 42, AI hoàn toàn "mù thông tin" về tên khách và mã đơn hàng, dẫn đến việc gọi nhầm tên là "chị Mai" và yêu cầu cung cấp lại mã đơn. AI không hề vô tâm hay cố tình quên, mà do **bộ nhớ RAM tạm thời của nó đã hết chỗ chứa**.

---

### Phần 2: Phương án quản lý RAM bộ nhớ

Để dòng tư vấn của nhân viên CSKH không bao giờ bị "tràn cốc" giữa chừng, chúng ta cần áp dụng đồng thời các giải pháp từ phía người dùng và thiết kế hệ thống:

#### 1. Phương án từ thao tác người dùng (Vận hành thủ công)
* **Nguyên tắc "Ngắt phiên khi đổi chủ đề":** Khi tư vấn xong một vấn đề lớn (ví dụ: tư vấn xong danh sách rau củ), nhân viên nên chủ động tổng hợp lại thông tin cốt lõi (tên khách, mã đơn, chốt đơn) và **mở một phiên chat (New Chat) hoàn toàn mới** cho vấn đề tiếp theo. Điều này giúp "làm sạch cốc nước", giữ bộ nhớ luôn trống trải cho các thông tin quan trọng.
* **Neo giữ thông tin (Prompt Reminders):** Nếu bắt buộc phải duy trì một phiên chat dài, hãy định kỳ nhắc lại thông tin định danh ở các mốc quan trọng (Ví dụ: *"Dạ, đối với đơn hàng #MTX-9988 của anh B..."*). Thao tác này giúp đưa thông tin cũ lên "tầng mặt" của cốc nước, chống lại việc bị trôi đi.

#### 2. Phương án từ thiết kế hệ thống (Giải pháp kỹ thuật tự động)
* **Ứng dụng cơ chế RAG (Retrieval-Augmented Generation) & Vector Database:** Thay vì ép AI nhớ mọi thứ trong một đoạn chat dài, hệ thống tích hợp chat của MartX nên tự động lưu trữ thông tin khách hàng (Tên, Mã đơn) vào một cơ sở dữ liệu ngầm bên ngoài. Mỗi khi khách hỏi, hệ thống sẽ tự động "bơm" ngầm thông tin này vào câu lệnh của AI mà không làm tốn dung lượng RAM chat.
* **Tích hợp tính năng tự động tóm tắt ngữ cảnh (Context Summarization / Sliding Window):** Xây dựng hệ thống tự động gom nhóm lịch sử chat: cứ sau mỗi 10–15 lượt hội thoại, hệ thống sẽ tự động tóm tắt các ý chính thành 1 đoạn ngắn gọn và xóa bớt các câu thoại rườm rà. Nhờ đó, "chiếc cốc" luôn chỉ chứa bản tóm tắt tinh gọn thay vì hàng nghìn từ ngữ dông dài gây tràn bộ nhớ.
