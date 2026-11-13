# BTTH - Cẩm nang sử dụng AI hiệu quả cho tân sinh viên

## 1. Sơ đồ các bước xâu chuỗi prompt (Prompt Chaining)

Để tạo ra cuốn cẩm nang ngắn gọn, nhất quán và kiểm soát tốt lượng token đầu ra, quy trình được chia nhỏ thành **4 bước xâu chuỗi tuần tự** (đầu ra của bước trước làm ngữ cảnh ràng buộc cho bước sau):

```text
[BƯỚC 1: PROMPT 1 - KHỞI TẠO & PHẦN 1]
  │  • Nhiệm vụ: Đóng vai cố vấn học tập, viết Phần 1 (Cách AI đoán từ / Bản chất LLM).
  │  • Kiểm soát Token: Giới hạn dưới 150 từ, dùng ví dụ lập trình thực tế, không dùng thuật ngữ hàn lâm.
  ▼
[BƯỚC 2: PROMPT 2 - VIẾT TIẾP PHẦN 2]
  │  • Nhiệm vụ: Kế thừa văn phong Phần 1, viết tiếp Phần 2 (3 cách nhận diện ảo giác của AI).
  │  • Kiểm soát Token: Trình bày dạng danh sách 3 gạch đầu dòng ngắn gọn, kèm dấu hiệu nhận biết khi code.
  ▼
[BƯỚC 3: PROMPT 3 - VIẾT TIẾP PHẦN 3]
  │  • Nhiệm vụ: Kế thừa mạch nội dung, viết Phần 3 (Cấu trúc prompt mẫu tối ưu theo khung CREATE).
  │  • Kiểm soát Token: Giải thích 6 thành tố CREATE + 1 ví dụ prompt mẫu xin giải thích lỗi code.
  ▼
[BƯỚC 4: PROMPT 4 - TỔNG HỢP & BIÊN TẬP HOÀN CHỈNH]
     • Nhiệm vụ: Ghép 3 phần trên, thêm lời mở đầu và lời kết ngắn gọn, rà soát độ dài và tính nhất quán.
     • Kết quả đầu ra: Cuốn "Cẩm nang sử dụng AI hiệu quả cho tân sinh viên" hoàn chỉnh.
```

---

## 2. Nội dung các prompt thành phần

Dưới đây là chi tiết 4 câu lệnh thành phần được thiết kế theo kỹ thuật **Prompt Chaining** và kiểm soát chặt chẽ độ dài (token):

### Prompt 1: Viết Phần 1 – Cách AI đoán từ (Bản chất LLM)
```text
Bạn là một giảng viên Công nghệ Thông tin thân thiện, chuyên hướng dẫn tân sinh viên cách học lập trình hiệu quả. Hãy viết "Phần 1: Cách AI đoán từ (Bản chất của mô hình ngôn ngữ lớn - LLM)" cho một cuốn cẩm nang bỏ túi dành cho sinh viên năm nhất.

Yêu cầu bắt buộc:
- Giải thích ngắn gọn cơ chế dự đoán từ tiếp theo (next-token prediction) dựa trên xác suất thống kê bằng ngôn ngữ đời thường, dễ hiểu.
- Lấy 1 ví dụ minh họa liên quan đến việc viết code hoặc học lập trình.
- Nhấn mạnh một nguyên tắc cốt lõi: AI tính toán xác suất chứ không thực sự "hiểu" logic như con người.
- Kiểm soát độ dài (Token): Tối đa 150 từ, trình bày súc tích, không viết lan man.
```

### Prompt 2: Viết Phần 2 – 3 cách nhận diện ảo giác của AI (Hallucination)
```text
Dựa trên giọng văn thân thiện, thực tế của Phần 1 vừa tạo, hãy viết tiếp "Phần 2: 3 cách nhận diện ảo giác của AI (Hallucination)" cho cuốn cẩm nang tân sinh viên học lập trình.

Yêu cầu bắt buộc:
- Giải thích trong 1 câu ngắn gọn "ảo giác AI" là hiện tượng AI tự tin bịa ra thông tin sai lệch.
- Liệt kê đúng 3 dấu hiệu nhận diện cụ thể mà sinh viên lập trình hay gặp phải (ví dụ: bịa tên thư viện/hàm không tồn tại, trích dẫn tài liệu giả, hoặc trả lời sai logic nhưng giọng văn rất chắc chắn).
- Với mỗi dấu hiệu, đưa ra 1 hành động kiểm chứng nhanh (Fact-check).
- Kiểm soát độ dài (Token): Trình bày dạng 3 gạch đầu dòng rõ ràng, tổng độ dài không quá 180 từ.
```

### Prompt 3: Viết Phần 3 – Cấu trúc prompt mẫu tối ưu bằng khung CREATE
```text
Tiếp nối mạch nội dung của Phần 1 và Phần 2, hãy viết "Phần 3: Công thức viết Prompt chuẩn với khung CREATE" để tân sinh viên áp dụng ngay khi học lập trình.

Yêu cầu bắt buộc:
- Giải thích ngắn gọn ý nghĩa 6 chữ cái của khung CREATE (Character - Request - Examples - Adjustments - Type of output - Extras) bằng tiếng Việt dễ nhớ.
- Cung cấp 01 ví dụ Prompt mẫu hoàn chỉnh áp dụng đúng khung CREATE cho tình huống thực tế: "Tân sinh viên nhờ AI giải thích một đoạn code bị lỗi cú pháp và hướng dẫn cách sửa mà không làm hộ bài tập".
- Kiểm soát độ dài (Token): Trình bày khoa học bằng danh sách, tổng độ dài khoảng 200 - 250 từ.
```

### Prompt 4: Tổng hợp & Hoàn thiện cuốn cẩm nang
```text
Hãy đóng vai biên tập viên, ghép nội dung của Phần 1, Phần 2 và Phần 3 ở trên thành một cuốn cẩm nang hoàn chỉnh có tiêu đề: "CẨM NANG SỬ DỤNG AI AN TOÀN & HIỆU QUẢ CHO TÂN SINH VIÊN IT".

Yêu cầu bắt buộc:
- Bổ sung 1 đoạn mở đầu (2 câu) truyền cảm hứng học tập chủ động và 1 lời nhắc nhở kết thúc (2 câu) về đạo đức học thuật (không copy-paste code mù quáng).
- Giữ nguyên nội dung cốt lõi của 3 phần, chỉ chỉnh sửa từ nối để các phần liên kết mượt mà, thống nhất định dạng Markdown.
```

---

## 3. Cuốn cẩm nang kết quả hoàn chỉnh xuất ra từ AI

> #  CẨM NANG SỬ DỤNG AI AN TOÀN & HIỆU QUẢ CHO TÂN SINH VIÊN IT
>
> Chào mừng các tân sinh viên bước vào thế giới lập trình! AI là người bạn đồng hành tuyệt vời giúp bạn tăng tốc học tập, nhưng chỉ thực sự phát huy tác dụng khi bạn làm chủ công cụ thay vì phụ thuộc vào nó.
>
> ---
>
> ### Phần 1: Cách AI đoán từ (LLM hoạt động thế nào?)
>
> Về bản chất, các công cụ như ChatGPT hay Gemini là **Mô hình Ngôn ngữ Lớn (LLM)** hoạt động như một "cỗ máy dự đoán từ tiếp theo" siêu cấp. Khi bạn đặt câu hỏi, AI không suy nghĩ hay hiểu logic như bộ não con người, mà nó tính toán xác suất thống kê để chọn ra từ (token) có khả năng xuất hiện cao nhất tiếp theo dựa trên hàng tỷ dữ liệu đã học.
>
> * **Ví dụ thực tế:** Khi bạn gõ `for (int i = 0; i < n;`, AI dự đoán cụm từ tiếp theo là `i++)` với xác suất 99% vì mẫu câu này xuất hiện lặp đi lặp lại trong vô số mã nguồn.
> * **Nguyên tắc cốt lõi:** AI giỏi bắt chước mẫu câu và cú pháp, nhưng **không thực sự hiểu bài toán** của bạn. Vì vậy, đừng bao giờ mặc định câu trả lời của AI luôn đúng.
>
> ---
>
> ### Phần 2: 3 cách nhận diện "ảo giác" của AI (Hallucination)
>
> **"Ảo giác AI"** là hiện tượng AI tự tin bịa ra thông tin hoàn toàn sai sự thật nhưng lại trình bày với giọng điệu cực kỳ thuyết phục. Tân sinh viên cần cảnh giác với 3 dấu hiệu sau:
>
> * **1. Bịa đặt hàm hoặc thư viện "ma":** AI gợi ý cho bạn một tên hàm hoặc thư viện nghe rất hợp lý để giải bài tập, nhưng khi đưa vào trình biên dịch (IDE) thì báo lỗi không tồn tại.  
>   * Cách kiểm chứng:* Luôn chạy thử code trên máy hoặc tra cứu lại trên tài liệu chính thức (Official Docs).
> * **2. Trích dẫn nguồn tài liệu hoặc đường link giả:** Khi bạn nhờ AI tìm tài liệu tham khảo, AI có thể tự tạo ra tên sách, tên tác giả hoặc đường dẫn URL không hề tồn tại trên Internet.  
>   * Cách kiểm chứng:* Nhấp trực tiếp vào đường link hoặc tìm kiếm tên tài liệu trên Google để xác thực.
> * **3. Lập luận sai logic nhưng giọng văn rất chắc chắn:** Với các bài toán thuật toán phức tạp, AI có thể giải sai bước trung gian dẫn đến kết quả sai, nhưng vẫn khẳng định chắc nịch.  
>   * Cách kiểm chứng:* Tự kiểm tra lại bằng bộ dữ liệu đầu vào nhỏ (test case) và tính nhẩm từng bước.
>
> ---
>
> ### Phần 3: Cấu trúc Prompt mẫu tối ưu bằng khung CREATE
>
> Để AI trả lời trúng trọng tâm và tiết kiệm thời gian hỏi đi hỏi lại, hãy áp dụng công thức **CREATE**:
>
> * **C – Character (Vai trò):** Giao cho AI một vai trò cụ thể.
> * **R – Request (Yêu cầu):** Nêu rõ nhiệm vụ chính cần làm.
> * **E – Examples (Ví dụ):** Đưa ví dụ mẫu nếu cần định hướng cách làm.
> * **A – Adjustments (Điều chỉnh/Ràng buộc):** Đặt giới hạn về độ dài, những điều không được làm.
> * **T – Type of output (Định dạng đầu ra):** Chọn cách trình bày (gạch đầu dòng, bảng, code...).
> * **E – Extras (Bối cảnh bổ sung):** Cung cấp thông tin nền hoặc đoạn code đang gặp lỗi.
>
> ####  Ví dụ Prompt mẫu chuẩn CREATE cho tân sinh viên:
> ```text
> [C] Hãy đóng vai một trợ giảng môn Lập trình C++ tận tâm.
> [R] Hãy giải thích nguyên nhân gây ra lỗi trong đoạn code dưới đây và gợi ý hướng sửa.
> [A] Yêu cầu: Giải thích bằng ngôn ngữ dễ hiểu cho sinh viên năm nhất, độ dài dưới 150 từ. Tuyệt đối KHÔNG viết sẵn toàn bộ code hoàn chỉnh để tôi tự tư duy sửa lỗi.
> [T] Trình bày đầu ra gồm 2 mục gạch đầu dòng: (1) Nguyên nhân lỗi và (2) Gợi ý cách khắc phục.
> [E] Bối cảnh: Tôi đang viết chương trình tính tổng mảng số nguyên nhưng bị lỗi vòng lặp vô hạn:
> int i = 0; while (i < 5) { cout << arr[i]; }
> ```
>
> ---
>
> **Lời kết:** Hãy dùng AI như một người gia sư gợi mở tư duy, tuyệt đối không sao chép (copy-paste) mã nguồn một cách mù quáng. Tự tay gõ từng dòng code và hiểu bản chất vấn đề mới chính là chìa khóa giúp bạn trở thành một lập trình viên giỏi!
