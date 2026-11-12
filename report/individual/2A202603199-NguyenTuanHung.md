# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603199.
- Ngày / CVAT local: 12/11/2026; CVAT local tại `http://localhost:8080`.
- Công cụ đã dùng: Các ZIP có cấu trúc export CVAT.

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task            | File ZIP đúng tên   | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --------------- | ------------------- | -----------------: | ---------------------------: |
| easy_semantic   | easy_semantic.zip   |              3 / 3 |                           20 |
| medium_instance | medium_instance.zip |              3 / 3 |                           32 |
| hard_panoptic   | hard_panoptic.zip   |              2 / 2 |                           30 |
| cp1_holes       | cp1_holes.zip       |              1 / 1 |                            3 |
| cp2_slice       | cp2_slice.zip       |              1 / 1 |                            3 |
| cp5_occlusion   | cp5_occlusion.zip   |              1 / 1 |                            3 |
| cp3_thin        | cp3_thin.zip        |              1 / 1 |                            3 |
| cp4_curb        | cp4_curb.zip        |              1 / 1 |                            3 |
| cp6_coverage    | cp6_coverage.zip    |              1 / 1 |                            3 |
| **Tổng tối đa** |                     |                    |                      **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg` — người ở phía trái ảnh, phía sau người lái xe máy (mask người đầu tiên trong ZIP; khoảng x=35–99, y=164–263).
- Class và quy tắc tôi dùng để chọn biên: `person`; tự vẽ bằng Polygon, theo đường viền phần người nhìn thấy và không gộp phần xe máy vào mask.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Không áp dụng; không dùng gợi ý AI/SAM.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình. Không dùng; tự vẽ người bằng Polygon và theo biên phần người nhìn thấy, không gộp xe máy vào mask.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `cp2_slice` — ảnh `000000017627.jpg`, hai xe con sát nhau ở giữa bên phải ảnh.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: gộp-tách — biên hai instance `car` sát nhau.
- Bằng chứng tôi nhìn thấy: Hai xe nằm sát nhau; sau khi chỉnh, ZIP có hai annotation `car` riêng tại vùng này.
- Quy tắc và hành động sửa: Cùng class không có nghĩa là cùng instance; đã chỉnh polygon để mỗi xe có mask riêng.
- Sau sửa đã Save và export lại chưa? Đã Save và export; ZIP hiện có hai mask `car` riêng ở vùng này.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): ZIP `cp2_slice` có annotation dạng polygon và các xe được lưu thành instance riêng; chưa có metric / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp2_slice`, `000000017627.jpg` — hai xe con sát nhau ở giữa bên phải ảnh (khoảng x=411 và x=482). | Gộp thành một vùng xe lớn hoặc vẽ mỗi xe thành một instance. | Nhìn thấy hai thân xe riêng; cùng class `car` không có nghĩa là cùng instance. | Tách thành hai mask `car`, mỗi mask theo biên của một xe. |
| `cp5_occlusion`, `000000336232.jpg` — người lái xe máy phía trước bên trái, nơi người và xe chồng sát nhau. | Gộp người vào mask xe máy hoặc vẽ người và xe thành hai object riêng. | `person` và `motorcycle` là hai class; ZIP cũng có annotation riêng cho person và motorcycle ở vùng này. | Giữ hai mask riêng, chỉ vẽ phần nhìn thấy của từng object; không tính người vào mask xe. |
| `cp4_curb`, `7d83710e-4697c3b2.jpg` — bó vỉa chạy chéo giữa mặt đường tối và lối đi sáng ở tiền cảnh. | Chọn ranh theo chỗ đổi màu bề mặt hoặc theo ranh bó vỉa/chức năng đường đi. | Màu mặt đường thay đổi; quy tắc trạm yêu cầu xác định road–sidewalk theo chức năng và bó vỉa, không chỉ theo màu. | Theo ranh bó vỉa để tách `road` và `sidewalk`; ở đoạn lối xe vào nơi bó vỉa bị gián đoạn, cần coach xác nhận ranh. |
