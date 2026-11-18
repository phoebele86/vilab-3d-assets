# Giấy phép mô hình 3D

Chỉ đưa vào repo các mô hình có giấy phép cho phép phân phối lại (ví dụ CC0, CC BY). Mỗi file cần ghi rõ
nguồn, tác giả và giấy phép.

| File | Nguồn | Tác giả | Giấy phép | Ghi chú |
|---|---|---|---|---|
| `biology/heart.glb` | [BodyParts3D](https://dbarchive.biosciencedbc.jp/en/bodyparts3d/download.html) bản 4.0 | The Database Center for Life Science (DBCLS) | CC BY 4.0 | Đã chỉnh sửa, xem chi tiết bên dưới |
| `biology/lungs.glb` | [BodyParts3D](https://dbarchive.biosciencedbc.jp/en/bodyparts3d/download.html) bản 3.0 và 4.0 | The Database Center for Life Science (DBCLS) | CC BY 4.0 | Đã chỉnh sửa, xem chi tiết bên dưới |

## BodyParts3D

- Trang tải dữ liệu: https://dbarchive.biosciencedbc.jp/en/bodyparts3d/download.html (LSDB Archive, JST/NBDC)
- Giấy phép dữ liệu: https://dbarchive.biosciencedbc.jp/en/bodyparts3d/lic.html (cập nhật ngày 2025-02-27):
  [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
- Dòng ghi công bắt buộc, phải giữ nguyên văn ở mọi nơi hiển thị hoặc phân phối lại mô hình:

  > BodyParts3D, © The Database Center for Life Science licensed under CC Attribution 4.0 International

- Dòng ghi công này cũng được ghi sẵn vào trường `asset.copyright` bên trong hai file `.glb`.
- Các file `.glb` dẫn xuất ở dưới (`biology/heart.glb`, `biology/lungs.glb`) được phát hành theo CC BY 4.0, kèm dòng
  ghi công ở trên.
- Lưu ý lịch sử: phần chú thích trong các file OBJ gốc (2011, 2013) và trang cũ
  http://lifesciencedb.jp/bp3d/info/license/index.html vẫn ghi giấy phép CC BY-SA 2.1 Nhật Bản. Trang cũ đó
  dẫn sang trang giấy phép của LSDB Archive ở trên, nơi từ 2025-02-27 áp dụng CC BY 4.0 cho toàn bộ cơ sở
  dữ liệu. Repo áp dụng giấy phép hiện hành CC BY 4.0.

## `biology/heart.glb` (tim)

Dữ liệu gốc: BodyParts3D bản 4.0 (2013), file `partof_BP3D_4.0_obj_99.zip` và `isa_BP3D_4.0_obj_99.zip`
(lưới đa giác OBJ, mức giảm đa giác 99%). Các phần tử (mã file `FJxxxx`) đã dùng:

| Node | Phần tử BodyParts3D |
|---|---|
| `right-atrium` | FJ2439 (wall of right atrium) |
| `left-atrium` | FJ2438 (wall of left atrium) |
| `right-ventricle` | phần thất phải của FJ2428 (wall of ventricle); FJ2419, FJ2430, FJ2437 (cơ nhú thất phải) |
| `left-ventricle` | phần thất trái của FJ2428 (wall of ventricle); FJ2418, FJ2429 (cơ nhú thất trái) |
| `tricuspid-valve` | FJ2421, FJ2433, FJ2436 |
| `mitral-valve` | FJ2420, FJ2432 |
| `pulmonary-valve` | FJ2417, FJ2427, FJ2434 |
| `aortic-valve` | FJ2426, FJ2431, FJ2435 |
| `aorta` | FJ3413 (ascending aorta), FJ3411 (arch of aorta), FJ1931 (descending thoracic aorta, cắt ngắn); đoạn gốc của FJ3417 (brachiocephalic artery), FJ3483 (left common carotid artery), FJ3479 (left subclavian artery) |
| `pulmonary-trunk` | FJ2966 |
| `left-pulmonary-artery` | FJ2924 |
| `right-pulmonary-artery` | FJ3019 |
| `pulmonary-veins` | FJ2925, FJ2933, FJ2944, FJ2950, FJ2955, FJ3020, FJ3040 (đoạn ngoài phổi của 4 tĩnh mạch phổi) |
| `superior-vena-cava` | FJ3645 |
| `inferior-vena-cava` | FJ3441 (cắt ngắn) |
| `coronary-arteries` | mọi phần tử của "right coronary artery" và "left coronary artery" (cây PART-OF) |
| `cardiac-veins` | mọi phần tử của "coronary sinus tree" và "anterior cardiac venous tree" (cây PART-OF); FJ2657–FJ2665, FJ2725, FJ2730 (cây IS-A) |

Chỉnh sửa so với bản gốc:

- Gộp các phần tử OBJ thành 17 phần, mỗi phần là một node/mesh có tên tiếng Anh dạng kebab-case.
- BodyParts3D chỉ có một khối cơ chung cho cả hai tâm thất (FJ2428). Khối này được tách thành `left-ventricle`
  và `right-ventricle` theo khoảng cách tới khoang thất trái (FJ2422) và khoang thất phải (FJ2423); ranh giới
  là gần đúng, chạy theo rãnh liên thất.
- Cắt ngắn bằng mặt phẳng ngang: động mạch chủ xuống, ba nhánh của cung động mạch chủ và tĩnh mạch chủ dưới.
- Đổi đơn vị từ mm sang m, đổi trục (Y hướng lên, mặt trước cơ thể hướng +Z, bên trái cơ thể là +X), đặt tâm
  hộp bao tại gốc tọa độ.
- Giảm số đa giác bằng meshoptimizer, tính lại pháp tuyến, gán vật liệu PBR màu quy ước, nén bằng
  `gltf-transform optimize --compress meshopt`.

## `biology/lungs.glb` (phổi)

Dữ liệu gốc:

| Node | Nguồn |
|---|---|
| `right-lung-upper-lobe` | bản 3.0 (2011), `BodyParts3D_3.0_obj_99.zip`, FMA7333 (upper lobe of right lung) |
| `right-lung-middle-lobe` | bản 3.0, FMA7383 (middle lobe of lung) |
| `right-lung-lower-lobe` | bản 3.0, FMA7337 (lower lobe of right lung) |
| `left-lung-upper-lobe` | bản 3.0, FMA7370 (upper lobe of left lung) |
| `left-lung-lower-lobe` | bản 3.0, FMA7371 (lower lobe of left lung) |
| `trachea` | bản 4.0 (2013), `partof_BP3D_4.0_obj_99.zip`, FJ2541 |
| `right-main-bronchus` | bản 4.0, FJ2539 (right main bronchus proper) |
| `left-main-bronchus` | bản 4.0, FJ2450 |
| `right-bronchial-tree` | bản 4.0, các phần tử còn lại của "right bronchial tree" |
| `left-bronchial-tree` | bản 4.0, các phần tử còn lại của "left bronchial tree" |

Node nhóm `right-lung` chứa ba thùy phổi phải, `left-lung` chứa hai thùy phổi trái.

Chỉnh sửa so với bản gốc:

- Bản 4.0 không có bề mặt phổi nên thùy phổi lấy từ bản 3.0. Đường dẫn khí bản 4.0 được dịch (−2, +2, +9) mm
  (hệ trục BodyParts3D) cho khớp với thùy phổi bản 3.0.
- Bỏ các đoạn đầu nhánh phế quản nhỏ bị lòi ra ngoài bề mặt thùy phổi.
- Gộp các phần tử OBJ thành từng phần, mỗi phần là một node/mesh có tên tiếng Anh dạng kebab-case.
- Đổi đơn vị từ mm sang m, đổi trục (Y hướng lên, mặt trước cơ thể hướng +Z, bên trái cơ thể là +X), đặt tâm
  hộp bao tại gốc tọa độ.
- Giảm số đa giác bằng meshoptimizer, tính lại pháp tuyến, gán vật liệu PBR màu quy ước, nén bằng
  `gltf-transform optimize --compress meshopt`.
