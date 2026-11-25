# Báo cáo Day 13 — Phạm Trọng Hiện, 2A202603218

> **Cách dùng mẫu này:** đổi tên file thành `2A202603218_PhamTrongHien.md` (họ tên không dấu, viết liền), ví dụ `2A202600123_NguyenVanAn.md`. Đổi tên, đừng chép thành file thứ hai.
>
> Xoá mọi dấu TODO và dòng gợi ý (dòng bắt đầu bằng `>`). Mỗi con số lấy từ **bảng A** hoặc **phiếu tự kiểm** trong `submission/`, kèm đơn vị (m, °). Ảnh để trong `report/individual/images/` (nộp LMS trong file zip, không commit); trong báo cáo chỉ ghi **tên file ảnh**. Báo cáo này nằm trên repo public: không chép biển số, chữ trên biển hiệu hay biển chỉ đường, tên đường, địa danh; nhắc tới bạn khác thì ghi MSSV, không ghi họ tên. Cả báo cáo ~2 trang.

## 1. Kết luận trước

### Thông tin bài làm

| Nội dung                    | Thông tin                                                                                          |
| --------------------------- | -------------------------------------------------------------------------------------------------- |
| MSSV                        | `2A202603218`                                                                                      |
| Task CVAT                   | `D13-2A202603218`                                                                                  |
| 10 frame                    | `s01f13`, `s01f30`, `s02f08`, `s02f40`, `s03f17`, `s03f56`, `s04f04`, `s04f35`, `s05f26`, `s05f46` |
| Hệ điều hành và trình duyệt | Windows · Edge                                                                                     |
| Phiên bản máy chủ CVAT      | 2.74.1                                                                                             |

### Kết quả và tự đánh giá

Bảng A ghi nhận 59 cuboid trên 10 frame. Các frame `s01f30`, `s03f17`, `s03f56`, `s05f26`, `s05f46` cùng có ít hộp nhất (5 hộp mỗi frame) vì lý do quan sát được ít. Phiếu tự kiểm đánh cờ 0 trên tổng số 59 cuboid. Tôi tự tin nhất về trên vì dễ dàng quan sát, nhưng còn chưa chắc về phía ngang do khó quan sát.

### Thao tác trên CVAT

1. **Quan sát cảnh.** Kéo chuột trái để xoay khung 3D đến góc nhìn từ trên xuống, kéo chuột phải để dời cảnh và cuộn chuột để phóng to vật cần kiểm tra.
2. **Vẽ và chỉnh hộp.** Chọn nhãn và **Cuboid → Shape**, rồi nháy đúp vào cụm điểm để đặt hộp. Căn chiều dài, chiều rộng và góc xoay ở **Top**. Kiểm tra chiều cao và đáy hộp ở **Side** và **Front**.
3. **Kiểm tra hướng.** Bật **Cuboid orientation** và đối chiếu vạch đỏ ngắn với đầu xe trên ảnh camera.

## 2. Đọc frame (Bước 2)

Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame    | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m)                                             | Vật xa nhất đọc được (~ m)      | Loại vật thấy                | Vật phía sau / hai bên                           | Cụm chưa đọc được |
| -------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------- | ---------------------------- | ------------------------------------------------ | ----------------- |
| `s01f13` | Phía trước là −y, +x sang trái xe, +y ra sau xe.                       | Đoạn đường trước xe trông khá phẳng trên cam01. Mặt đường thấp hơn LiDAR khoảng 1,7 m | Xe con ở phía trước khoảng 65 m | Xe con (Car), xe buýt (Bus). | Xe con xanh đậm ở bên trái, chếch về phía trước. | Không.            |
| `s01f30` | Phía trước là −y, +x sang trái xe, +y ra sau xe.                       | Thấp hơn LiDAR khoảng 1,7 m                                                           | Xe con ở phía sau, khoảng 10 m  | Xe con (Car)                 | 2 xe con ở phía sau 2 bên                        | Không.            |

Trên `cam01` của `s01f13`, xe con ở sát bên trái có màu xanh đậm, còn xe con phía trước có màu trắng. Mặt sau xe buýt có bảng hiển thị màu đỏ. Đèn hậu và nắp cốp của xe trắng cho thấy đuôi xe quay về phía camera.

Xe buýt ở `s01f13` cách khoảng 30 m theo phương ngang, đáy hộp của xe con gần bên trái nằm thấp hơn LiDAR khoảng 1,6 m

Tám frame lướt:

| Frame    | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
| -------- | ------------------------------------------------ | ---------------- |
| `s02f08` | −y                                               | Không.           |
| `s02f40` | −y                                               | Không.           |
| `s03f17` | −y                                               | Không.           |
| `s03f56` | −y                                               | Không.           |
| `s04f04` | −y                                               | Không.           |
| `s04f35` | −y                                               | Không.           |
| `s05f26` | −y                                               | Không.           |
| `s05f46` | −y                                               | Không.           |

## 3. Ba cuboid có hướng dẫn (Bước 3)

Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.

| Vật                              | Frame, idx  | Class   | Mũi tên yaw đúng hướng?                            | Đáy chạm đường?                         | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3?                                                                             |
| -------------------------------- | ----------- | ------- | -------------------------------------------------- | --------------------------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------ |
| (a) xe con gần                   | `s05f26`, 5 | Car     | Gần hướng −y                                       | Đáy cao hơn mặt đường ước tính 0,02 m.  | Đã kiểm front/side/top + ảnh  | 5,298 × 1,934 × 1,751 m. Cả ba chiều nằm trong khoảng tham chiếu của nhóm SUV, minivan, van chở người. |
| (b) xe buýt hoặc xe tải          | `s01f13`, 4 | Bus     | Phù hợp với hướng cùng chiều chếch nhẹ trên cam01. | Đáy thấp hơn mặt đường ước tính 0,09 m. | Đã đối chiếu cam01            | 13,09 × 3,17 × 3,56 m. Cả ba chiều vượt khoảng tham chiếu của xe buýt thường.                          |
| (c) người đi bộ hoặc xe hai bánh | `s04f35`, 2 | Cyclist | Gần hướng −y.                                      | Đáy cao hơn mặt đường ước tính 0,05 m.  | đã đối chiếu                  | 2,18 × 0,94 × 1,76 m. Cả ba chiều nằm trong khoảng tham chiếu của xe máy có người.                     |

## 4. Bốn hiện tượng chất lượng (Bước 4)

Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng                           | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết)                                                  | Thấy gì trên point cloud                                                                                            | Hệ quả khi gán (theo guideline)                                                           |
| ------------------------------------ | ----------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| 1. Bóng che                          | t4-1-bong-che.png       | Xe buýt gần có thể chặn tia LiDAR đi tới vùng phía sau nó.                | Theo hướng dẫn, ngay sau xe buýt bên trái có một vùng gần như trống điểm, trong khi hai bên vẫn dày điểm.           | Có thể nhận biết sai đó là vật thể thuộc 1 class khác                                     |
| 2. Thưa ở xa                         | t4-2-thua-o-xa.png      | Ở khoảng cách lớn, các tia LiDAR có thể quét qua vật với mật độ thấp hơn. | Mật độ các điểm thấp không xác định được rõ vật thể                                                                 | Dễ bị nhận biết nhầm vì chưa chắc đó là vật thể hoặc có thể bỏ qua vật thể nếu không đánh |
| 3. Phản xạ thấp / ít điểm bất thường | t4-3-phan-xa-thap.png   | Phản xạ yếu, góc chiếu hoặc che khuất có thể làm giảm số điểm.            | Hai hộp Car ở tầm gần nhau có số điểm khác nhau. Hộp idx 1 ở 20,8 m có 275 điểm, còn hộp idx 2 ở 19,2 m có 532 điểm | Đối chiếu ảnh camera và hình dạng cụm điểm trước khi chỉnh hộp.                           |
| 4. Điểm lạ                           | t4-4-diem-la.png        | Có thể do nhiễu đo hoặc phản xạ gián tiếp.                                | Có các chùm điểm lạ không xác định được vật thể                                                                     | Xoay khung 3D sang góc nghiêng để kiểm tra vị trí cụm điểm và xác định vật thể            |

## 5. Số từ cuboid của tôi (Bước 5)

Lấy từ `submission/D13-<MÃ SỐ>-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z        | h       | z đáy = z − h/2 | dist_m  | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường)               |
| -------------------------- | -------- | ------- | --------------- | ------- | --------------- | ------- | ---------------------------------------------------- |
| `s05f26`, 5, Car           | −0,871 m | 1,751 m | −1,747 m        | 10,51 m | 10,547 m        | 269,6°  | Gần mặt đường, lệch khoảng 0,05 m so với mốc −1,7 m. |
| `s01f13`, 4, Bus           | −0,056 m | 3,555 m | −1,834 m        | 29,88 m | 29,878 m        | 284,7°  | Gần mặt đường, thấp hơn mốc khoảng 0,13 m.           |
| `s04f35`, 2, Cyclist       | −0,774 m | 1,757 m | −1,653 m        | 10,54 m | 10,573 m        | 270,4°  | Gần mặt đường, cao hơn mốc khoảng 0,05 m.            |

(a) Cuboid gần nhất trong bảng A là Car `s03f17`, idx 3, có `dist_m` = 3,21 m và r = 3,331 m. Cuboid xa nhất là Car `s01f13`, idx 6, có `dist_m` = 64,96 m và r = 64,958 m.

(b) Car `s05f26`, idx 5 có kích thước 5,298 × 1,934 × 1,751 m, nằm trong khoảng tham chiếu của nhóm SUV, minivan, van chở người. Cyclist `s04f35`, idx 2 có kích thước 2,182 × 0,937 × 1,757 m, nằm trong khoảng của xe máy có người.

(c) Car `s01f13`, idx 3 ở phía trước và có yaw 268,4°, lệch 1,6° so với 270°. Car `s02f40`, idx 5 cũng ở phía trước và có yaw 92,7°, lệch 2,7° so với 90°.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m  | Số điểm (`points_in`) |
| -------------------------- | ------- | --------------------- |
| `s01f13`, 3, Car           | 5,35 m  | 2.620                 |
| `s01f13`, 5, Car           | 29,38 m | 119                   |
| `s01f13`, 7, Car           | 35,42 m | 60                    |
| `s01f13`, 6, Car           | 64,96 m | 20                    |

Trong bốn mẫu, xe ở 35,42 m xa gấp khoảng 6,6 lần xe ở 5,35 m và còn khoảng 2,3% số điểm (60 so với 2.620). Mẫu 5,35 m có nhiều điểm hơn mốc 1.968 điểm ở nhóm 0–10 m, còn các mẫu 29,38 m, 35,42 m và 64,96 m lần lượt có 119, 60 và 20 điểm so với các mốc 214, 72 và 19 điểm ở các nhóm tương ứng.

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc

(a) Nhãn 3D đo bằng mét để mô hình học vị trí và kích thước thật của vật trong hệ tọa độ LiDAR, trong khi kích thước tính bằng pixel thay đổi theo khoảng cách và góc nhìn. Với vật thưa điểm, quy tắc gán nhãn riêng giúp mô hình học từ các hộp có đủ căn cứ và giảm sai lệch do những hộp được suy đoán từ quá ít điểm.

(b) Tôi dùng ChatGPT để hướng dẫn quá trình làm lab.
Tôi hỏi về quy trình trên CVAT, hệ tọa độ LiDAR, đơn vị trong bảng A, cách trình bày và sửa chính tả báo cáo.

(c) Các điểm còn hơi mơ hồ chưa thể chắc chắn được box đã nằm đúng hay chưa
