# Báo cáo Day 13 — Nguyen Quang Thuc, 2A202603116

> **Cách dùng mẫu này:** đổi tên file thành `<MSSV>_<HoTen>.md` (họ tên không dấu, viết liền), ví dụ `2A202600123_NguyenVanAn.md`. Đổi tên, đừng chép thành file thứ hai.
>
> Xoá mọi dấu TODO và dòng gợi ý (dòng bắt đầu bằng `>`). Mỗi con số lấy từ **bảng A** hoặc **phiếu tự kiểm** trong `submission/`, kèm đơn vị (m, °). Ảnh để trong `report/individual/images/` (nộp LMS trong file zip, không commit); trong báo cáo chỉ ghi **tên file ảnh**. Báo cáo này nằm trên repo public: không chép biển số, chữ trên biển hiệu hay biển chỉ đường, tên đường, địa danh; nhắc tới bạn khác thì ghi MSSV, không ghi họ tên. Cả báo cáo ~2 trang.

## 1. Kết luận trước
MSSV: `2A202603116`; task: `D13-2A202603116`; 10 frame: `s01f04`, `s01f19`, `s02f08`, `s02f41`, `s03f01`, `s03f33`, `s04f02`, `s04f17`, `s05f13`, `s05f46`. Hệ điều hành: Windows 11 Pro. Trình duyệt: Chromium (Codex In-app Browser). Phiên bản CVAT: `2.82.0`. MSSV bạn ngồi cạnh: `2A202603025`.

Có 63 cuboid; frame ít nhất là `s01f19` với 5 cuboid vì trong frame này có ít đối tượng rõ để gán nhãn. Phiếu tự kiểm ghi nhận 0 cuboid có cảnh báo trên tổng số 63 cuboid. Phần tự tin nhất là xác định hướng di chuyển; phần yếu nhất là các vật ở xa.

Trong CVAT, em dùng các khung nhìn Top/Side/Front để quan sát và chỉnh cuboid. Có thể xoay, di chuyển và đổi góc nhìn point cloud; nháy đúp cuboid để chỉnh hình dạng. Sau đó kiểm tra mũi tên `Cuboid orientation`, vị trí đáy và đối chiếu với ảnh camera bằng `preview`.

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s01f04 | Mặt đường phẳng; đường nhựa hiện đại, thẳng; hai bên có bồn cây ngăn cách | | | | | |
| s01f19 | Mặt đường phẳng; đường nhựa hiện đại, thẳng; hai bên có bồn cây ngăn cách | | | | | |

Camera cho biết: (1) màu sắc, (2) ước lượng khoảng cách, (3) bối cảnh xung quanh. LiDAR cho biết: (1) khoảng cách chính xác, (2) kích thước vật. Không ghi nhận thêm đặc điểm thứ ba chỉ thuộc về LiDAR trong hai frame đã đọc kỹ.

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
|---|---|---|
| s01f19 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s02f08 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s02f41 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s03f01 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s03f33 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s04f02 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s04f17 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s05f13 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |
| s05f46 | Chưa ghi chép riêng | Không ghi nhận điều lạ đặc biệt |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | `s01f04`, idx 8 | Car | Đúng | Không chạm đường | Đã kiểm Top/Side/Front và camera | Có |
| (b) xe buýt hoặc xe tải | `s01f04`, idx 3 | Truck | Đúng | Không chạm đường | Đã kiểm Top/Side/Front và camera | Có |
| (c) người đi bộ hoặc xe hai bánh | `s02f08`, idx 18 | Cyclist | Đúng | Không chạm đường | Đã kiểm Top/Side/Front và camera | Có |

Vòng hiệu chuẩn: không có điểm nào thấy lệch hoặc không chắc. Các vật bỏ qua vì không đủ cơ sở: chưa ghi nhận.

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | `t4-1-bong-che.png` / task chung | Vật ở phía trước che khuất một phần vật phía sau; đây là giả thuyết dựa trên hình point cloud. | Biên và số điểm của vật bị che không đầy đủ. | Chỉ gán phần quan sát chắc chắn; không kéo cuboid theo phần bị che khuất. |
| 2. Thưa ở xa | `t4-2-thua-o-xa.png` / task chung | Mật độ điểm giảm theo khoảng cách; đây là giả thuyết. | Vật ở xa có ít điểm, hình dạng và kích thước khó xác định. | Gán cuboid theo phần điểm nhìn thấy và thận trọng với kích thước. |
| 3. Phản xạ thấp / ít điểm bất thường | `t4-3-phan-xa-thap.png` / task chung | Bề mặt có thể phản xạ LiDAR kém; đây là giả thuyết. | Chỉ có một phần điểm của vật hoặc các điểm bị rời rạc. | Không mở rộng cuboid vào vùng không có bằng chứng điểm rõ ràng. |
| 4. Điểm lạ | `t4-4-diem-la.png` / task chung | Có thể là nhiễu hoặc điểm phản xạ bất thường; đây là giả thuyết. | Xuất hiện điểm rời rạc không tạo thành vật thể rõ ràng. | Không gán nhãn riêng cho điểm nhiễu nếu không xác định được vật thể. |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-<MÃ SỐ>-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| `s01f04`, idx 2 | **Cần anh lấy từ Bảng A** | **Cần anh lấy từ Bảng A** | **Cần anh tính `z − h/2`** | **Cần anh lấy từ Bảng A** | **Cần anh tính `√(x²+y²+z²)`** | **Cần anh lấy từ Bảng A** | **Cần anh nhận xét đáy** |
| `s01f04`, idx 8 | **Cần anh lấy từ Bảng A** | **Cần anh lấy từ Bảng A** | **Cần anh tính `z − h/2`** | **Cần anh lấy từ Bảng A** | **Cần anh tính `√(x²+y²+z²)`** | **Cần anh lấy từ Bảng A** | **Cần anh nhận xét đáy** |
| `s01f04`, idx 4 | **Cần anh lấy từ Bảng A** | **Cần anh lấy từ Bảng A** | **Cần anh tính `z − h/2`** | **Cần anh lấy từ Bảng A** | **Cần anh tính `√(x²+y²+z²)`** | **Cần anh lấy từ Bảng A** | **Cần anh nhận xét đáy** |

(a) Cuboid gần nhất và xa nhất: **cần anh bổ sung** `frame`, `idx`, `dist_m` và `r` sau khi đối chiếu Bảng A/phiếu tự kiểm.

(b) Kích thước đo trên CVAT:

- Cyclist: `l = 1.64 m`, `w = 0.63 m`, `h = 1.61 m`.
- Car: `l = 4.75 m`, `w = 1.99 m`, `h = 1.39 m`.

So với bảng 4.3: **cần anh bổ sung** chiều nào nằm ngoài khoảng tham chiếu và giải thích nguyên nhân nếu có.

(c) `yaw_deg` của một xe cùng chiều phía trước và một xe ngược chiều: **cần anh bổ sung** sau khi đối chiếu Bảng A.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| `s01f04`, idx 2 | **Cần anh lấy từ phiếu tự kiểm sau khi sync** | **Cần anh lấy từ phiếu tự kiểm sau khi sync** |
| `s01f04`, idx 8 | **Cần anh lấy từ phiếu tự kiểm sau khi sync** | **Cần anh lấy từ phiếu tự kiểm sau khi sync** |
| `s01f04`, idx 4 | **Cần anh lấy từ phiếu tự kiểm sau khi sync** | **Cần anh lấy từ phiếu tự kiểm sau khi sync** |
| `s01f04`, idx 3 | **Cần anh lấy từ phiếu tự kiểm sau khi sync** | **Cần anh lấy từ phiếu tự kiểm sau khi sync** |

Nhìn chung, khi khoảng cách từ LiDAR đến vật tăng thì số điểm `points_in` có xu hướng giảm vì cùng một vật chiếm góc nhìn nhỏ hơn và mật độ điểm thưa hơn. Nhận xét này phù hợp với đường cong trong slide: xe con có khoảng 1968 điểm ở 0–10 m, giảm còn khoảng 718 ở 10–20 m, 214 ở 20–30 m, 72 ở 30–40 m và 19 ở 60–80 m. Mức giảm thực tế còn phụ thuộc kích thước vật, bề mặt và hiện tượng che khuất.

Phần tự kiểm: phiếu kiểm cuối cùng ghi nhận 0/63 cuboid còn cảnh báo. Không ghi lại riêng hai cuboid đã sửa sau `preview`/`selfcheck`. Cảnh báo giữ nguyên: không có.

Đổi kiểm: MSSV người đã kiểm chéo với bạn là `2A202603025`. Hai con số được đối chiếu với bảng A là tổng số 63 cuboid và số cuboid của frame `s01f04` là 8. Kết quả khớp 100%, không phát sinh chênh lệch cần sửa.

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
(a) Nhãn 3D được đo bằng mét để mô hình học vị trí và kích thước thực trong không gian, không phụ thuộc độ phân giải ảnh. Vật thưa điểm cần quy tắc riêng vì point cloud không thể hiện đầy đủ biên và hình dạng của vật.

(b) Công cụ: ChatGPT/Codex. Câu hỏi chính: quy trình làm bài Day13, cách dùng CVAT và cách kiểm tra các sản phẩm. Cách dùng kết quả: dùng để hiểu quy trình và hoàn thiện báo cáo theo những gì đã quan sát.

(c) Điều còn chưa chắc: không có. Lỗi phát hiện sau hạn: không có.
