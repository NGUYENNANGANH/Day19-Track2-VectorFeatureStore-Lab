# Reflection — Lab 19

**Tên:** Nguyễn Năng Anh
**Mã học viên / Cohort:** 2A202600184
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact (Từ khóa chính xác):** BM25 chiếm ưu thế tuyệt đối vì thuật toán này cực kỳ nhạy với tần suất xuất hiện verbatim của từ khóa (mô hình bag-of-words/TF-IDF). 
- **Paraphrase (Đồng nghĩa/Diễn đạt lại):** Semantic Search (Vector) chiến thắng nhờ khả năng ánh xạ các cụm từ đồng nghĩa vào cùng một không gian vector đa chiều, giải quyết trọn vẹn rào cản "vocabulary mismatch".
- **Mixed (Kết hợp):** Hybrid Search (RRF) tỏ ra vô đối. Phương pháp này bù trừ hoàn hảo điểm yếu của hai cơ chế: BM25 neo giữ các từ khóa đặc thù, trong khi Vector bao quát được ngữ cảnh, giúp Precision@10 tiệm cận mức 100%.

**Khi KHÔNG dùng Hybrid:**
- **Chỉ dùng pure BM25:** Khi cần tìm kiếm các định danh chính xác (mã lỗi log, UUID, mã SKU, số điện thoại, tên riêng ngách). Ở đây, vector search thường gây nhiễu vì nó cố gắng tìm các chuỗi "tương tự" thay vì khớp tuyệt đối.
- **Chỉ dùng pure Vector:** Trong hệ thống tìm kiếm đa ngôn ngữ (cross-lingual), tìm kiếm ngữ nghĩa thuần túy (semantic matching) không phân biệt từ vựng, hoặc khi ngân sách cho độ trễ (latency) quá eo hẹp không đủ khả năng chạy song song 2 luồng retrieval.

---

## Điều ngạc nhiên nhất khi làm lab này

Sự tinh tế và sức mạnh của thuật toán Reciprocal Rank Fusion (RRF). Thay vì phải huấn luyện một mô hình re-ranking phức tạp (cross-encoder) và tốn GPU, chỉ với một phép tính nghịch đảo vô cùng đơn giản `1/(k + rank)` lại có thể dung hòa tín hiệu từ hai hệ thống hoàn toàn khác biệt một cách ấn tượng.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _không có_
