# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602286
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: CVAT local, Google Colab, GitHub

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task            | File ZIP đúng tên     | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --------------- | --------------------- | -----------------: | ---------------------------: |
| easy_semantic   | `easy_semantic.zip`   |              3 / 3 |                           20 |
| medium_instance | `medium_instance.zip` |              3 / 3 |                           32 |
| hard_panoptic   | `hard_panoptic.zip`   |              2 / 2 |                           30 |
| cp1_holes       | `cp1_holes.zip`       |              1 / 1 |                            3 |
| cp2_slice       | `cp2_slice.zip`       |              1 / 1 |                            3 |
| cp5_occlusion   | `cp5_occlusion.zip`   |              1 / 1 |                            3 |
| cp3_thin        | `cp3_thin.zip`        |              1 / 1 |                            3 |
| cp4_curb        | `cp4_curb.zip`        |              1 / 1 |                            3 |
| cp6_coverage    | `cp6_coverage.zip`    |              1 / 1 |                            3 |
| **Tổng tối đa** |                       |                    |                      **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, `000000373353.jpg` và `000000458325.jpg`.
- Class và quy tắc tôi dùng để chọn biên: Với instance segmentation, mỗi vật thể vật lý được giữ thành một instance riêng. Tôi bám theo phần nhìn thấy của vật thể, không tự mở rộng mask vào vùng bị che; hai vật cùng class nằm sát nhau vẫn phải tách thành hai instance.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Chỉ giữ phần gợi ý khi biên bám đúng vật thể; phần mask tràn sang nền hoặc sang vật khác phải được chỉnh lại thủ công. Gợi ý tự động chỉ hỗ trợ thao tác, không thay thế quyết định gán nhãn.
- Nếu không dùng gợi ý: Nếu lớp yêu cầu ghi đúng “object Medium đầu tiên tự vẽ”, cần mở lại lịch sử/thao tác CVAT hoặc nhớ lại object đầu tiên và thay dòng đầu tiên của mục này bằng ảnh, vị trí và class chính xác.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `cp5_occlusion`, ảnh `000000336232.jpg`, phần export COCO của task.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: khác — lỗi cấu trúc file export.
- Bằng chứng tôi nhìn thấy: Notebook tự kiểm báo `cp5_occlusion · LỖI` và thông báo **“cần đúng một COCO JSON trong annotations/”**. Trong bước kiểm cuối, đây là task duy nhất còn lỗi hợp đồng; số task chưa có ZIP là 0.
- Quy tắc và hành động sửa: ông sửa trực tiếp JSON bên trong ZIP. Cần quay lại CVAT, kiểm task `cp5_occlusion`, Save annotation, export lại bằng **COCO 1.0**, đổi tên đúng `cp5_occlusion.zip`, thay file cũ trong `submissions/`, rồi chạy lại notebook.
- Sau sửa đã Save và export lại chưa? Có rồi

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí                                                                        | Hai cách hiểu có thể                                                     | Quy tắc/chứng cứ                                                                                                 | Quyết định hoặc câu hỏi cho coach                                                                        |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `cp1_holes` — `000000144300.jpg`, các chi tiết/kính bên trong xe                  | Khoét phần kính/chi tiết khỏi mask hoặc giữ chúng trong mask của vật thể | Quy tắc task nêu kính/lỗ nằm trong mask, không tự khoét                                                          | Giữ các vùng này thuộc cùng mask của instance, trừ khi class/task quy định khác                          |
| `cp2_slice` — `000000017627.jpg`, hai xe cùng lớp nằm sát nhau                    | Gộp thành một mask vì cùng class hoặc tách thành hai instance            | Instance segmentation yêu cầu mỗi vật thể vật lý là một instance; hai vật cùng lớp sát nhau vẫn phải tách        | Tách thành hai instance riêng                                                                            |
| `cp5_occlusion` — `000000336232.jpg`, vật bị che khiến phần nhìn thấy bị chia rời | Tách thành hai object theo hai vùng nhìn thấy hoặc giữ là một instance   | Một vật bị che có thể có nhiều vùng nhìn thấy rời nhau nhưng vẫn là một instance; chỉ gán phần thực sự nhìn thấy | Giữ là một instance nếu xác định đó là cùng một vật thể; cần export lại COCO đúng cấu trúc trước khi nộp |
