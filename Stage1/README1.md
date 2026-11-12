### Bước 1: Phân tích Input và Output

**1. Phân tích dữ liệu đầu vào (Input):**
* **Đối tượng mục tiêu:** Đúng 2 phiên bản cao cấp nhất của mỗi dòng: **iPhone 16 Pro Max** và **Samsung Galaxy S24 Ultra** (loại trừ các bản tiêu chuẩn, Plus, Pro hay S24+).
* **Nguồn dữ liệu bắt buộc:** Chỉ trích xuất từ trang thông số kỹ thuật chính thức của Apple (`apple.com` / `support.apple.com`) và Samsung (`samsung.com`).
* **Phạm vi thông số:** Chỉ tập trung vào 2 nhóm hạng mục là **Pin & Sạc** (dung lượng mAh, thời lượng phát video/nghe nhạc công bố, công suất sạc) và **Camera** (cụm camera sau, camera trước, khả năng zoom, chuẩn quay video tối đa).
* **Bẫy dữ liệu cần chặn:**
  * Apple không công bố dung lượng pin (mAh) trên trang chủ chính thức mà chỉ công bố thời lượng sử dụng (giờ phát video/âm thanh). Nếu ép AI lấy từ trang chủ Apple, AI phải ghi rõ trạng thái này thay vì tự ý lấy con số mAh từ trang bên thứ ba (như GSMArena) hoặc tự đoán.
  * Tránh nhầm lẫn thông số camera tele giữa S24 Ultra (50MP zoom quang 5x + 10MP zoom quang 3x) với các đời tiền nhiệm (S23 Ultra dùng 10MP 10x).

**2. Cấu trúc đầu ra mong muốn (Output):**
* **Phần 1 - Bảng so sánh ngang:** Gồm 3 cột (`Hạng mục thông số` | `iPhone 16 Pro Max` | `Samsung Galaxy S24 Ultra`) và các hàng chia theo nhóm Pin & Camera.
* **Phần 2 - Điểm nhấn nổi bật:** Tóm tắt ngắn gọn 2 điểm mạnh lớn nhất (về Pin/Camera) của từng máy dựa trên chính dữ liệu vừa trích xuất.
* **Cơ chế đánh dấu an toàn:** Bất kỳ thông số nào không được nhà sản xuất công bố trên trang chủ phải điền chính xác cụm từ **`Chưa xác thực`**.

---

### Bước 2: Viết Prompt theo khung CREATE

> **[C - Context (Ngữ cảnh)]**
> Bạn là một chuyên gia phân tích thông số kỹ thuật thiết bị di động làm việc cho bộ phận biên tập nội dung công nghệ. Tôi đang cần chuẩn bị một bài viết so sánh ngắn gọn, chính xác tuyệt đối 100% về pin và camera giữa hai mẫu flagship: **iPhone 16 Pro Max** và **Samsung Galaxy S24 Ultra** để gửi cho khách hàng.
>
> **[R - Request (Nhiệm vụ)]**
> Hãy trích xuất thông số kỹ thuật chính xác về **Pin** và **Camera** của hai thiết bị trên, trình bày dưới dạng bảng so sánh ngang, sau đó nêu bật 2 điểm mạnh lớn nhất của từng dòng máy.
>
> **[E - Explanation (Giải thích)]**
> Khách hàng yêu cầu độ chính xác tuyệt đối để phục vụ tư vấn chuyên sâu. Các nguồn tin bên thứ ba thường có sai số hoặc lẫn lộn thông số giữa bản tiêu chuẩn, bản Pro và bản Ultra/Pro Max. Do đó, mọi con số đưa ra phải có khả năng đối chiếu trực tiếp với tài liệu công bố của hãng.
>
> **[A - Action (Hành động)]**
> Thực hiện tuần tự theo 3 bước sau:
> 1. **Truy xuất dữ liệu:** Chỉ tìm kiếm và đối chiếu thông số từ trang chủ chính thức của Apple (apple.com / support.apple.com) cho đúng model *iPhone 16 Pro Max* và trang chủ Samsung (samsung.com) cho đúng model *Galaxy S24 Ultra*.
> 2. **Lập bảng so sánh ngang:** Tạo bảng gồm 3 cột: `Thông số kỹ thuật` | `iPhone 16 Pro Max` | `Samsung Galaxy S24 Ultra`. Các hàng bắt buộc gồm: Dung lượng pin (mAh), Thời lượng phát video công bố, Công suất sạc, Cụm camera sau, Camera trước, Khả năng Zoom quang học, và Độ phân giải quay video tối đa.
> 3. **Tổng hợp điểm mạnh:** Bên dưới bảng, gạch đầu dòng nêu đúng 2 điểm mạnh lớn nhất (về pin hoặc camera) của mỗi máy dựa trên các thông số vừa trích xuất.
>
> **[T - Tone (Giọng điệu)]**
> Khách quan, chuyên nghiệp, ngắn gọn, súc tích, đi thẳng vào số liệu kỹ thuật, không dùng từ ngữ quảng cáo sáo rỗng.
>
> **[E - Extras (Ràng buộc & Quy tắc chống bịa đặt)]**
> - **Quy tắc "Chưa xác thực":** Nếu hãng không công bố chính thức một thông số nào trên trang chủ (ví dụ: Apple không ghi dung lượng mAh trên trang chủ), bạn **BẮT BUỘC** phải ghi chữ **"Chưa xác thực"** vào ô đó (có thể mở ngoặc chú thích ngắn gọn lý do). Tuyệt đối không tự suy đoán hay lấy số liệu từ các trang tin rò rỉ/bên thứ ba để điền vào.
> - **Không nhầm phiên bản:** Kiểm tra kỹ tên model trước khi điền, không lấy thông số của iPhone 16 Pro hay Galaxy S24/S24+.
> - **Kèm nguồn đối chiếu:** Ghi rõ đường dẫn (URL) trang thông số chính thức của Apple và Samsung ở cuối bài.

---

### Bước 3: Chạy thử và kết quả mẫu thu được

#### 1. Bảng so sánh thông số Pin & Camera (Nguồn chính hãng)

| Thông số kỹ thuật | iPhone 16 Pro Max | Samsung Galaxy S24 Ultra |
| :--- | :--- | :--- |
| **Dung lượng pin (mAh)** | **Chưa xác thực** *(Apple không công bố số mAh trên trang chủ)* | 5.000 mAh *(tiêu chuẩn)* |
| **Thời lượng phát video** | Lên đến 33 giờ *(phát trực tuyến: 29 giờ)* | Lên đến 30 giờ *(nghe nhạc lên đến 95 giờ)* |
| **Công suất sạc** | Sạc không dây MagSafe tối đa 25W *(với củ sạc 30W trở lên)*, Qi2 15W | **Chưa xác thực** trên trang thông số rút gọn VN *(hỗ trợ sạc nhanh có dây và không dây)* |
| **Cụm camera sau** | 3 camera: 48MP *(Chính, f/1.78)* + 48MP *(Góc siêu rộng, f/2.2)* + 12MP *(Telephoto, f/2.8)* | 4 camera: 200MP *(Chính, f/1.7)* + 50MP *(Telephoto, f/3.4)* + 12MP *(Góc siêu rộng, f/2.2)* + 10MP *(Telephoto, f/2.4)* |
| **Camera trước** | 12MP *(f/1.9)* | 12MP *(f/2.2)* |
| **Zoom quang học** | 5x *(quang học)*, tối đa 25x *(kỹ thuật số)* | 3x và 5x *(Zoom chuẩn quang học 2x và 10x qua cảm biến Adaptive Pixel)*, tối đa 100x *(kỹ thuật số)* |
| **Quay video tối đa** | 4K Dolby Vision lên đến 120 fps *(hỗ trợ ProRes, Log)* | UHD 8K *(7680 x 4320)* @ 30fps; 4K @ 120fps |

#### 2. Hai điểm mạnh lớn nhất của từng dòng máy

* **iPhone 16 Pro Max:**
  1. **Thời lượng phát video vượt trội:** Đạt mức công bố lên đến **33 giờ** xem video liên tục, nhỉnh hơn mức 30 giờ của đối thủ.
  2. **Khả năng quay video chuẩn điện ảnh chuyên sâu:** Hỗ trợ quay **4K Dolby Vision ở tốc độ 120 fps** cùng các định dạng chuyên nghiệp như ProRes và hệ thống mã hóa màu ACES.

* **Samsung Galaxy S24 Ultra:**
  1. **Hệ thống 4 camera độ phân giải cực cao & đa tiêu cự:** Sở hữu cảm biến chính **200MP** kết hợp cùng hai ống kính Telephoto riêng biệt (50MP và 10MP), cho phép zoom quang học linh hoạt ở nhiều mức (3x, 5x và chuẩn quang học 10x).
  2. **Độ phân giải quay video đạt chuẩn 8K:** Vượt trội về độ phân giải khung hình khi hỗ trợ quay **UHD 8K tại 30fps** bên cạnh khả năng quay chậm 4K 120fps.

**Nguồn đối chiếu chính thức:**
* Apple Support Tech Specs: `https://support.apple.com/en-us/121032`
* Samsung Việt Nam Specs: `https://www.samsung.com/vn/smartphones/galaxy-s24-ultra/specs/`
