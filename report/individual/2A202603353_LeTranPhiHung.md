# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603353
- Ngày / CVAT local: 12/11/2026 / CVAT local
- Công cụ đã dùng: CVAT local (BBox, Polygon, Brush/Mask) và script kiểm tra cấu trúc file ZIP.

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Em đã hoàn thành 3 bài chính và 3 checkpoint. Các ZIP dưới đây đã được kiểm tra về tên file, ảnh, class và định dạng mask. Ba checkpoint còn lại chưa có ZIP.

| Bài | File ZIP | Số ảnh đã hoàn thành |
| --- | --- | ---: |
| Easy semantic | `easy_semantic.zip` | 3 / 3 |
| Medium instance | `medium_instance.zip` | 3 / 3 |
| Hard panoptic | `hard_panoptic.zip` | 2 / 2 |
| Checkpoint `cp1_holes` | `cp1_holes.zip` | 1 / 1 |
| Checkpoint `cp2_slice` | `cp2_slice.zip` | 1 / 1 |
| Checkpoint `cp3_thin` | `cp3_thin.zip` | 1 / 1 |
| Checkpoint `cp4_curb` | chưa có | 0 / 1 |
| Checkpoint `cp5_occlusion` | chưa có | 0 / 1 |
| Checkpoint `cp6_coverage` | chưa có | 0 / 1 |

Script kiểm tra cho thấy 6 ZIP hiện có đều đúng cấu trúc và không có ZIP lạ. Ba ZIP còn thiếu là `cp4_curb.zip`, `cp5_occlusion.zip` và `cp6_coverage.zip`. Báo cáo này không sử dụng dữ liệu đáp án để so sánh hoặc tự chấm điểm.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên em tự vẽ: `000000181542.jpg`, chiếc xe máy ở khu vực giữa ảnh, phía trước người phụ nữ mặc áo dài.
- Class và quy tắc em dùng để chọn biên: `motorcycle`; đây là chiếc xe máy ở giữa ảnh, phía trước người phụ nữ. Em chỉ tô phần xe nhìn thấy, bám theo mép thân xe và bánh xe, không tô phần bị che.
- Nếu dùng gợi ý sau đó: không dùng gợi ý tự động; em giữ quyết định theo class và phần biên quan sát được.
- Nếu không dùng gợi ý: không dùng; em xem mỗi chiếc xe máy là một object riêng khi nhìn thấy đường biên riêng, không gộp hai xe gần nhau thành một object.

## 3. Một vấn đề em cần kiểm tra lại

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance`, cả 3 ảnh; em cần kiểm tra kỹ các vật thể nhỏ hoặc bị che.
- Vấn đề cần kiểm tra: có thể bỏ sót vật thể hoặc gộp hai vật thể ở gần nhau.
- Bằng chứng em nhìn thấy: những vật thể nhỏ, bị che một phần hoặc nằm sát nhau có ranh giới khó nhìn rõ khi thao tác trong CVAT.
- Quy tắc và hành động: mỗi người hoặc phương tiện nhìn thấy rõ phải là một object riêng; chỉ tô phần nhìn thấy, không tô phần bị che hoặc phần nền.
- Trạng thái: ZIP hiện tại đã được Save và export; chưa có chỉnh sửa mới sau lần kiểm tra này.

Kết quả kiểm tra cấu trúc: 6 ZIP hiện có đều hợp lệ; chưa thực hiện chấm điểm nội dung.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Đây là ba vị trí dễ gán nhãn nhầm. Em ghi lại cách hiểu và cách xử lý để có thể kiểm tra lại trong CVAT.

| Vị trí trong ảnh | Điều có thể bị nhầm | Quy tắc em áp dụng | Cách em xử lý |
| --- | --- | --- | --- |
| Easy – `817bca71-00000000.jpg`, khu vực vạch sang đường | Phần màu xám có thể là mặt đường hoặc vỉa hè. | Phân biệt theo công dụng và vị trí bó vỉa, không chỉ dựa vào màu. | Em tách `road` và `sidewalk` theo ranh nhìn thấy. |
| Medium: xe máy và người ở gần nhau trong `000000181542.jpg` | Có thể bỏ sót vật nhỏ hoặc gộp hai vật gần nhau. | Mỗi người hoặc phương tiện nhìn thấy rõ là một object riêng. | Em kiểm tra từng vật và không gộp các xe máy gần nhau. |
| Hard – `000000350023.jpg`, khu vực xe hơi, người, xe tải và vỉa hè | Có thể nhầm vùng nền với vật thể hoặc bỏ sót vật bị che. | `road`, `sidewalk` là vùng nền; `car`, `person`, `truck` là từng vật thể riêng. | Em kiểm tra để các vùng không bị tô chồng bất hợp lý. |
