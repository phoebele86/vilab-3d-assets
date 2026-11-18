# vilab-3d-assets

Kho file mô hình 3D (`.glb`) của **ViLab 3D**, ứng dụng web trực quan hóa 3D hỗ trợ dạy học môn
Khoa học tự nhiên THCS. Repo chỉ chứa file mô hình, được publish bằng GitHub Pages.

## Hệ thống gồm

- `vilab-3d-frontend`: giao diện React + Three.js
- `vilab-3d-backend`: API FastAPI, PostgreSQL + pgvector, RAG
- `vilab-3d-assets`: file mô hình 3D (repo này)
- `vilab-3d-llm`: cấu hình model Qwen/bge-m3 qua Ollama và bộ đánh giá

## Cấu trúc

```
biology/   # Sinh học, ví dụ biology/heart.glb
physics/   # Vật lý
```

Mô hình Hóa học được dựng bằng code từ dữ liệu phân tử nên không nằm ở đây.

Database chỉ lưu **đường dẫn tương đối** (ví dụ `biology/heart.glb`). Địa chỉ gốc nằm trong biến
`VITE_ASSET_URL` của frontend:

| Giai đoạn | Địa chỉ file |
|---|---|
| Local | `http://localhost:5173/api/assets/biology/heart.glb` (backend đọc thẳng thư mục này qua `ASSETS_DIR`) |
| GitHub Pages | `https://<username>.github.io/vilab-3d-assets/biology/heart.glb` |

## Thêm mô hình mới

1. Kiểm tra giấy phép cho phép phân phối lại, ghi nguồn vào `LICENSES.md`.
2. Nén trước khi chép vào repo:

   ```bash
   npx @gltf-transform/cli optimize model-original.glb biology/model-name.glb --compress meshopt
   ```

3. Mỗi file không quá 10 MB (CI sẽ báo lỗi nếu vượt).

## Bật GitHub Pages

**Settings → Pages → Deploy from a branch → `main` / `root`**. File `.nojekyll` giúp GitHub Pages phục vụ
nguyên trạng mọi file.
