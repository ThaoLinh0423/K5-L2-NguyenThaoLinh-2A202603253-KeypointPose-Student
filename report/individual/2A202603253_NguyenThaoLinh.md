# Báo cáo cá nhân — NguyenThaoLinh-2A202603253

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyễn Thảo Linh
- MSSV: 2A202603253
- Email: nguyenlinhthao666@gmail.com
- Link repository: https://github.com/ThaoLinh0423/K5-L2-NguyenThaoLinh-2A202603253-KeypointPose-Student.git
- Phiên bản CVAT (Help → About): 2.82
- Máy: hệ điều hành Windows 11 · RAM 16 GB · chạy CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 14:00
- Giờ kết thúc: 19:15

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):

Rê chuột vào điểm cần đổi rồi bấm phím `Q` để bật/tắt cờ `occluded` ($v=1$), bấm `O` để bật/tắt `outside` ($v=0$), hoặc nhấp chuột phải trực tiếp lên điểm để chọn cờ tương ứng từ menu.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 0 | 0 | 25 |
| `occluded` | 3 | 6 | 1 | 0 | 22 |
| `back` | 2 | 4 | 0 | 0 | 18 |
| `small` | 1 | 3 | 4 | 0 | 15 |
| `crowd` | 1 | 3 | 2 | 0 | 20 |
| `faces` | 8 | 8 | — | 0 | 25 |

- Số ảnh người đã xong ở mốc phút 105: 8 / 10
- Thời gian thực tế (phút): CP1 80 · CP2 25 · CP3 20
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?

Ảnh tốn thời gian nhất là `000000572411.jpg` (nhóm `small`) và `000000309169.jpg` (nhóm `crowd`), do mật độ người dày đặc, người ở xa và người ở gần đứng chen chúc nhau, nhiều khớp bị che lấp và phải cẩn thận đo chiều cao để loại trừ các người hậu cảnh dưới 60 px theo quy ước của lab.

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000307757.jpg` | Người 1 (quay lưng) | `right_knee` | 0 | `v = 1` và `v = 0` | Đầu gối người nằm ở mép dưới ảnh, tọa độ thực tế vượt ra ngoài khung hình (y > 480). Ban đầu để bình thường gây lỗi ngoài biên, chọn `outside` ($v=0$) theo đúng quy tắc không đoán khớp ngoài khung. |
| `000000030960.jpg` | Người 2 | `left_wrist` | 1 | `v = 1` và `v = 0` | Cổ tay bị thân xe che khuất nhưng hướng cẳng tay và cùi chỏ rất rõ ràng, vị trí cổ tay ước lượng chắc chắn nên chọn `occluded` ($v=1$). |
| `000000324953.jpg` | Người 1 | `left_ankle` | 1 | `v = 1` và `v = 0` | Cổ chân bị che khuất sau thanh cản/ống quần nhưng nhìn thấy bàn chân đặt trên mặt đất, ước lượng vị trí khớp cổ chân có độ tin cậy cao ($v=1$). |
| `face_13874.jpg` | Mặt kính râm | `left_eye_*`, `right_eye_*` | 1 | `v = 1` và `v = 0` | Cả 8 điểm mắt bị tròng kính râm che khuất, nhưng nhìn thấy rõ khung gọng kính và vị trí hốc mắt, nên đặt tâm mắt theo gọng và gán `occluded` ($v=1$). |
| `face_416730.jpg` | Mặt nghiêng | `right_eye_inner` | 1 | `v = 1` và `v = 0` | Góc quay nghiêng khiến sống mũi che khuất khóe trong mắt phải, nhưng phần còn lại của mắt thấy rõ, ước lượng vị trí góc mắt tiếp giáp gốc mũi chắc chắn nên chọn $v=1$. |
| `face_79367.jpg` | Mặt tóc che | `left_eye_outer` | 1 | `v = 1` và `v = 0` | Tóc rủ xuống che một phần khóe ngoài mắt trái, nhưng mí trên và mí dưới vẫn lộ rõ nên định vị được điểm gặp nhau của hai mí ($v=1$). |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| `000000572411.jpg` | Người 1, 2, 6, 7 | Cả skeleton | `extra` | Gán người hậu cảnh có chiều cao 23–34 px (< 60 px theo quy tắc lab) | Có (đã xóa 4 skeleton nhỏ) |
| `000000307757.jpg` | Người 1 | `right_knee` | `vis_flag` | Điểm đầu gối phải nằm ngoài khung ảnh (y=481.4 > 480) nhưng mang cờ $v=2$ | Có (đã đổi sang outside $v=0$) |
| `000000043968.jpg` | Người 1 | `left_hip`, `knee`, `ankle` | `lr_swap` | Kiểm tra lại hướng người đứng nghiêng, chân bắt chéo; đã rà soát lại đảm bảo đúng trái/phải giải phẫu của người | Có (kiểm tra và xác nhận đúng) |
| `000000309169.jpg` | Người 1 | Toàn bộ 17 điểm | `ok` | Người quay mặt về camera, các điểm `left_*` nằm bên phải ảnh, cờ đặt chuẩn | Không cần sửa (đã chuẩn) |
| `000000480582.jpg` | Người 1 | `left_shoulder`, `right_shoulder` | `position` | Người quay lưng, điểm vai đặt hơi chệch ra viền áo, đã chỉnh lại đúng mỏm cùng vai | Có (đã kéo về tâm khớp) |
| `face_13874.jpg` | Mặt kính râm | 8 điểm mắt | `vis_flag` | Kiểm tra lại toàn bộ 8 điểm quanh mắt sau tròng kính râm đảm bảo mang cờ $v=1$ | Có (đã kiểm tra chuẩn cờ) |
| `face_476363.jpg` | Mặt nghiêng | Toàn bộ 13 điểm | `ok` | Khóe mắt, mép mí trên dưới, chóp mũi và khóe miệng đặt chuẩn xác | Không cần sửa (đã chuẩn) |
| `face_362568.jpg` | Mặt thẳng | `left_eye_upper`, `left_eye_lower` | `position` | Mí mắt trên và dưới đặt hơi lấn vào con ngươi, đã kéo lại sát mép viền mí mắt | Có (đã chỉnh lại tâm mí) |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 1 | 2 | 2 | 0 | 1 | 2 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

- Điểm cổ chân (`left_ankle`) trong ảnh `000000078170.jpg`: Lựa chọn 1 là $v=1$ vì nhìn thấy hướng cẳng chân và bàn chân chạm sàn; lựa chọn 2 là $v=0$ vì ống quần che kín hoàn toàn mắt cá chân. Quyết định chọn $v=1$ vì cẳng chân thẳng, khoảng cách từ gối xuống mặt sàn cố định nên ước lượng vị trí mắt cá có dung sai hẹp (< 5 px).

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenThaoLinh_persons.zip` | `000000043968.jpg`, người 1 | 51 | Đúng (`left_ear` ra $v=0$, `left_knee` ra $v=1$) | Đúng (16) |
| `NguyenThaoLinh_persons.zip` | `000000307757.jpg`, người 1 | 51 | Đúng (`right_knee` ra $v=0$) | Đúng (14) |
| `NguyenThaoLinh_faces.zip` | `face_13874.jpg`, mặt 1 | 39 | Đúng (8 điểm mắt ra $v=1$, các điểm khác ra $v=2$) | Đúng (13) |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? Tọa độ cũ (CVAT 2.x vẫn lưu tọa độ trước đó kèm cờ $v=0$; khi huấn luyện model hay tính OKS, script chỉ lọc các điểm $v > 0$ nên điểm $v=0$ sẽ tự động bị bỏ qua).

Hai job đã chuyển sang completed trên CVAT? Có

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenThaoLinh_persons.zip
  Số ảnh: 12 · số skeleton `person`: 21 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000030960=2, 000000043968=1, 000000078170=2, 000000213933=1, 000000307757=2, 000000309169=3, 000000324953=2, 000000365099=1, 000000445187=1, 000000480582=2, 000000493741=1, 000000572411=3
  Cờ v: v=2 231 (65%) · v=1 56 (16%) · v=0 70 (20%)
  num_keypoints trung bình: 13.7
- File face: NguyenThaoLinh_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_13874=1, face_141135=1, face_196742=1, face_261458=1, face_362568=1, face_416730=1, face_476363=1, face_79367=1
  Cờ v: v=2 95 (91%) · v=1 9 (9%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 70 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 3
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

1. `000000043968.jpg #1` và `000000309169.jpg #1`: Cảnh báo các cặp hông, đầu gối, cổ chân nằm ngược phía so với thân trên. Đã kiểm tra lại trên ảnh gốc: đây là tư thế người đứng nghiêng và chân trước chân sau bắt chéo tự nhiên theo góc phối cảnh 3D, không phải do gán nhầm trái/phải (`lr_swap`), nên giữ nguyên tọa độ thực tế.
2. `000000572411.jpg #1`: Cảnh báo cặp wrist nằm ngược phía. Đã kiểm tra ảnh: người trong ảnh đang khoanh tay/vắt chéo hai cổ tay trước ngực, nên việc cổ tay trái/phải hoán đổi vị trí hình chiếu trên ảnh 2D là tư thế có thật.

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   Lỗi dễ mắc nhất là quên kiểm tra các khớp nằm sát mép biên ảnh (như khớp đầu gối chạm đáy ảnh vẫn để cờ $v=2$ thay vì bật `outside` $v=0$) và việc gán sót hoặc gán thừa người nhỏ trong ảnh đông người (`crowd`). Ở dự án thật, tôi sẽ xây dựng quy trình kiểm tra biên (boundary check) tự động trước khi submit, đồng thời phóng to khung hình và sử dụng công cụ đo kích thước bbox trước khi quyết định gán skeleton.

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   Đề xuất thêm quy tắc rõ ràng về việc xử lý tư thế tự che (self-occlusion) khi người khoanh tay hoặc bắt chéo chân: Cần hướng dẫn người gán nhãn kiểm tra đường gióng nối của chi trước khi đánh dấu cờ `occluded`, và bổ sung trường ghi chú "crossed_limbs" để script tự kiểm không hiểu nhầm là lỗi đổi trái/phải (`lr_swap`).

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   Nhãn đi vào model ở bước tạo Ground Truth Heatmap (tạo ngọn đồi xác suất Gaussian quanh tọa độ) và tính trọng số trong hàm mất mát (loss). Nếu mắc lỗi đổi trái/phải (`lr_swap`) ở chân hoặc tay:
   - Trong bước tăng cường dữ liệu lật ảnh ngang (horizontal flip data augmentation), ảnh bị lật nhưng tên khớp bị hoán đổi sai quy ước, khiến nhãn mục tiêu mâu thuẫn trực tiếp với ảnh thật.
   - Khi tính OKS, khoảng cách $d_i$ giữa khớp trái và khớp phải sẽ bị kéo dài cực đại, làm điểm similarity rơi về 0, sụp đổ hoàn toàn độ chính xác của mô hình pose estimation.

## 8. Khó khăn và lỗi kỹ thuật

- Ban đầu gặp lỗi điểm ngoài biên ảnh $y > 480$ vẫn để cờ $v=2$, khiến script báo `CHƯA ĐẠT (1 lỗi)`. Đã khắc phục bằng cách rê chuột vào điểm gối và bấm `O` để chuyển sang `outside` ($v=0$).
- Trong ảnh đông người `000000572411.jpg`, ban đầu đã gán cả các người nhỏ ở hậu cảnh (cao từ 23 đến 34 px). Sau khi đọc kỹ cảnh báo và quy tắc của bài lab (chỉ gán người từ 60 px trở lên), tôi đã xóa 4 skeleton nhỏ này để tránh bị trừ điểm lỗi `extra`.

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Hướng dẫn thực hành Lab Ngày 4: `docs/GUIDELINE.md`, `docs/CVAT_CHEATSHEET.md`, `docs/COCO_KEYPOINTS.md`.
- Nền tảng gán nhãn CVAT phiên bản 2.82.
- Script kiểm tra tự động `src/check_submission.py` và trợ lý `lab.py`.
- Trợ lý AI Antigravity: hỗ trợ phân tích nguyên nhân lỗi script trong terminal, đối chiếu tọa độ bbox và cấu trúc lại báo cáo cá nhân chuẩn quy định.

