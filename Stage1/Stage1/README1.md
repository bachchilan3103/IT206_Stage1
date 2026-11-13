# BÀI LÀM: NHẬN DIỆN BẢN CHẤT HOẠT ĐỘNG CỦA LLM

## PHẦN 1. BÓC TÁCH NHẬN THỨC SAI

Báo cáo của Nam có 2 điểm sai:

**Sai lầm 1: Cho rằng ChatGPT là máy tính có thể thực hiện chính xác mọi phép tính.**

LLM không hoạt động giống máy tính bỏ túi. Cơ chế chính của mô hình là **Next Token Prediction** (dự đoán token tiếp theo). Khi tạo câu trả lời, mô hình dự đoán chuỗi từ hoặc ký tự có khả năng xuất hiện tiếp theo dựa trên ngữ cảnh, chứ không mặc định thực hiện phép cộng bằng thuật toán số học.

Vì vậy, khi gặp phép tính `15.480 + 28.750`, mô hình có thể tạo ra kết quả sai `44.130` do dự đoán không chính xác. Điều này không đồng nghĩa máy chủ hay phần mềm bị hỏng.

**Sai lầm 2: Cho rằng có hàng trăm tỷ tham số thì kết quả luôn chính xác.**

Số lượng tham số lớn không đảm bảo mô hình tính toán đúng 100%. Trong giai đoạn **Pre-training**, LLM học các mẫu và mối liên hệ trong lượng dữ liệu lớn để dự đoán token tiếp theo. Mô hình học cách tạo ra câu trả lời phù hợp với dữ liệu đã học, nhưng không phải mọi phép tính đều được kiểm chứng bằng một bộ xử lý số học chính xác.

Do đó, LLM có thể trả lời tốt nhiều câu hỏi nhưng vẫn mắc lỗi với số học, đặc biệt khi chỉ dựa vào khả năng sinh văn bản.

## PHẦN 2. SỬA LỖI VÀ PROMPTING

Để hạn chế sai sót, cần yêu cầu ChatGPT sử dụng công cụ tính toán như **Code Interpreter/Python**, thay vì chỉ dựa vào dự đoán văn bản.

**Prompt đề xuất:**

> Bạn hãy sử dụng công cụ Python (Code Interpreter) để tính phép cộng sau: 15.480 + 28.750.
>
> Xem dấu chấm là dấu phân cách hàng nghìn. Hãy chuyển hai số thành số nguyên, thực hiện phép cộng bằng Python, sau đó kiểm tra lại kết quả và trình bày phép tính cùng đáp án. Không tự ước lượng kết quả bằng cách dự đoán văn bản.

**Kết quả đúng:**

```python
15480 + 28750
# 44230
```

Vậy:

**15.480 + 28.750 = 44.230**

Sử dụng Python giúp phép tính được thực hiện bằng phép toán số học của chương trình, có độ chính xác cao đối với phép cộng số nguyên này. Chỉ yêu cầu AI “suy luận từng bước” không đảm bảo kết quả chính xác tuyệt đối nếu không có công cụ tính toán để kiểm tra.
