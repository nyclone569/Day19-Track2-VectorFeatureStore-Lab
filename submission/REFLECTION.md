# Reflection — Lab 19

**Tên:** _Trương Đăng Nghĩa
**Cohort:** _A20-K1
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries, BM25 thắng rõ ở `exact` queries vì những query này chứa từ kỹ thuật xuất hiện nguyên văn trong corpus — BM25 match term-by-term rất hiệu quả. Vector search thắng ở `paraphrase` queries vì nó hiểu nghĩa ngữ nghĩa dù không có từ trùng khớp. Hybrid (RRF k=60) thắng ở `mixed` queries vì kết hợp cả hai tín hiệu, và nhìn chung đạt Precision@10 cao nhất trên trung bình toàn bộ tập.

Tuy nhiên hybrid không phải lúc nào cũng là lựa chọn tốt nhất. Nếu corpus toàn văn bản kỹ thuật với terminology cố định (ví dụ log hệ thống, mã lỗi), BM25 đơn giản hơn và nhanh hơn mà không thua kém. Ngược lại, nếu ứng dụng cần semantic search thuần (ví dụ tìm ảnh theo mô tả, recommendation dựa trên hành vi), vector-only phù hợp hơn vì BM25 không có tác dụng. Hybrid cũng tốn tài nguyên hơn vì phải chạy cả hai retriever song song trước khi fuse.

---

## Điều ngạc nhiên nhất khi làm lab này

Ngạc nhiên nhất là embedding model `bge-small-en` (train trên tiếng Anh) vẫn hoạt động khá ổn với tiếng Việt ở `mixed` queries, nhưng thực sự yếu ở `paraphrase` thuần Việt — đây là lúc thấy rõ lý do production cần model đa ngôn ngữ như `bge-m3`.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với:
