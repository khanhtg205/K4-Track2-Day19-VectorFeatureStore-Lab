# Reflection — Lab 19

**Tên:** Trần Gia khánh
**Cohort:** _A20-K4_  
**Path đã chạy:** lite  

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact (15 câu):** BM25 và Hybrid đồng hạng nhất (96.7%) do chứa từ khóa kỹ thuật khớp chính xác văn bản.
- **Paraphrase (15 câu):** BM25 (33.3%) và Hybrid (32.0%) vượt Semantic (24.0%) vì model `bge-small-en` (tiếng Anh) chưa tối ưu cho diễn đạt tiếng Việt; nhưng Vector search giúp gom cụm ngữ nghĩa tương đồng.
- **Mixed (20 câu):** Hybrid thắng tuyệt đối (100.0% so với BM25 97.0% và Semantic 98.5%) và thắng trung bình toàn tập (78.6%) nhờ RRF dung hợp hài hòa cả tín hiệu từ khóa và ngữ nghĩa.

**Khi nào KHÔNG dùng Hybrid?**
1. **Dùng pure BM25:** Khi bài toán tra cứu mã định danh chính xác (SKU sản phẩm, mã lỗi, user ID, code hash) mà ngữ nghĩa không mang lại giá trị hoặc cần tối ưu tài nguyên tối đa.
2. **Dùng pure Vector:** Khi dữ liệu phi cấu trúc thuần túy (ảnh, audio, truy vấn trừu tượng đa ngôn ngữ) hoặc hệ thống yêu cầu độ trễ cực thấp (P99 < 3ms), không thể gánh chi phí tính toán RRF và tokenization kép.

---

## Điều ngạc nhiên nhất khi làm lab này

Sự chênh lệch giữa Latest Join và Point-In-Time (PIT) Join: Latest Join tạo ra AUC ảo cao hơn thực tế tới +0.12 do rò rỉ 98.2% dữ liệu tương lai, minh chứng rõ ràng tại sao Feature Store bắt buộc phải có PIT join để tránh data leakage.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với:
