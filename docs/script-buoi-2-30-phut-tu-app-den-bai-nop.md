# Script buổi 2 — 30 phút: "Từ app chạy được đến bài nộp được"

Deck: `docs/slides/session2-ship-and-submit-slides.html` (15 slide)
Khán giả: **gần như cùng nhóm với buổi 1** — đã có app trong tay
Kết quả mong muốn: mỗi người **đã bấm nộp ngay trong phòng**, không phải "về nhà sẽ nộp".

Buổi này tái dùng toàn bộ kết quả buổi 1: problem brief, quyết định, **bản kế hoạch (tính năng + stack)**, bộ token, và app đã build.

Chặng: **06 Test → 09 Nộp bài** (buổi 1 chạy 01 Research → 05 Code).

---

## Chuẩn bị trước (T-15 phút)

- [ ] Deck mở sẵn, đã test tắt wifi
- [ ] App demo (Ươm Mầm) mở sẵn — dùng để chạy prompt test/đánh giá trên màn hình
- [ ] **Thang điểm thật** của cuộc thi mở sẵn trong một tab, để dán vào prompt đánh giá
- [ ] Link form nộp bài mở sẵn, phóng to đủ đọc từ cuối phòng
- [ ] Tài khoản Google chưa publish (dự phòng cho ai kẹt Starter Tier)
- [ ] Brief facilitator: buổi này **không dạy**, chỉ gỡ kẹt — ưu tiên giúp người chưa có link

**Nguyên tắc:** 30 phút mà có 15 phút thực hành. Phần nói phải cực gọn. Không giảng lại buổi 1.

---

## Bảng thời gian

| Thời gian | Slide | Nội dung | Dạng |
|---|---|---|---|
| 00:00–00:03 | 1–3 | Mở + nhắc lại + hôm nay làm gì | Nói |
| 00:03–00:06 | 4–5 | Test | Nói |
| 00:06–00:10 | 6 | **THỰC HÀNH 1** | Làm (4′) |
| 00:10–00:13 | 7–8 | Đánh giá | Nói |
| 00:13–00:17 | 9 | **THỰC HÀNH 2** | Làm (4′) |
| 00:17–00:19 | 10 | Deploy | Nói |
| 00:19–00:22 | 11 | **THỰC HÀNH 3 — publish** | Làm (3′) |
| 00:22–00:25 | 12–13 | Nộp gì + video demo | Nói |
| 00:25–00:29 | 14 | **THỰC HÀNH 4 — nộp** | Làm (4′) |
| 00:29–00:30 | 15 | Đóng | Nói |

Nói ≈ 15′ · làm ≈ 15′.

**Hai tool** — mỗi slide có việc làm đều có badge ở góc phải trên:

| Tool | Slide |
|---|---|
| **Gemini chat** — `gemini.google.com` | 5, **6** (test) · 8, **9** (đánh giá) |
| **AI Studio** — `ai.dev` | 10, **11** (publish) · **14** (lấy link để nộp) |

Nhắc lại quy tắc từ buổi 1: *output là chữ để đọc → Gemini; output là app để nhìn → AI Studio.*

---

## 00:00–00:03 — Mở + nhắc lại (slide 1–3)

**Slide 1.**

> "Buổi trước mọi người có app. Hôm nay chúng ta biến nó thành bài nộp — thứ mà giám khảo mở ra là hiểu ngay, không cần bạn ngồi cạnh giải thích."

> "Ba mươi phút, một nửa là mọi người tự làm. Nên tôi nói nhanh."

**Slide 2 — nhắc lại 30 giây, đừng dạy lại.**

> "Buổi trước để lại năm thứ. Thiếu cái nào cũng theo được, nhưng phải có một app mở lên được — dù còn xấu."

Hỏi nhanh, không đợi lâu:

> "Giơ tay: ai đang có app mở được trên máy?"

*(Ít hơn nửa phòng giơ tay → nói luôn: "Ai chưa có, lát nữa facilitator đưa link app mẫu để bạn chạy theo. Đừng dừng lại ở đây.")*

**Slide 3 — hôm nay.**

> "Bốn chặng cuối. Và mục tiêu rất cụ thể: kết thúc buổi này, bạn **đã nộp**. Không phải 'tối nay về nộp' — vì 'tối nay về nộp' nghĩa là không nộp."

---

## 00:03–00:06 — Test (slide 4–5)

**Slide 4.**

> "Đảo lại cách nghĩ về test. MVP của bạn không cần 80% coverage. Nó cần sống sót bốn phút trước mặt một người không phải bạn — người không biết chỗ nào nên tránh bấm."

Chỉ ba thẻ:

> "Test kỹ đúng đường bạn sẽ demo. Test qua vài biên hiển nhiên. Còn lại bỏ — bạn sẽ viết lại code đó vào tuần sau."

**Slide 5 — prompt.** Chỉ đúng một dòng:

> "Dòng này biến danh sách thành thứ dùng được: **sắp theo khả năng xảy ra ngay lúc demo**. Không phải theo mức độ nghiêm trọng lý thuyết — theo cái sắp cắn bạn."

---

## 00:06–00:10 — THỰC HÀNH 1 (slide 6, 4 phút)

> "Bốn phút. Chạy prompt test trên app của bạn. Đọc danh sách. Rồi **chỉ sửa hai lỗi đầu tiên** — bỏ qua phần còn lại."

> "Đừng sửa cả mười hai. Hôm nay không đủ giờ, và hai cái đầu là hai cái sẽ thật sự xảy ra."

**Làm:** đi vòng. Còn 1 phút thì báo.

---

## 00:10–00:13 — Đánh giá (slide 7–8)

**Slide 7.**

> "'App em ổn chưa ạ?' là câu không ai trả lời được. Đổi thành: 'nó có ăn điểm theo đúng tiêu chí sẽ bị chấm không?' — câu đó trả lời được, và sửa được."

Chỉ ô 40%:

> "Để ý ô lớn nhất là feasibility — chạy được, dễ dùng, có nghĩ tới người khuyết tật. Nó lớn nhất **và** dễ ăn nhất, vì nó nằm hoàn toàn trong tay bạn. Một app nhỏ mà mọi nút đều chạy thắng một app tham vọng mà vỡ giữa chừng."

**Slide 8 — prompt.** Chỉ hai chỗ:

> "Bắt nó chứng minh bằng thứ **cụ thể trong sản phẩm**, không nhận xét chung chung. Và dòng cuối là dòng biến báo cáo thành hành động: nếu tôi chỉ còn N giờ, làm gì trước, và chủ động không làm gì."

---

## 00:13–00:17 — THỰC HÀNH 2 (slide 9, 4 phút)

> "Bốn phút. Dán thang điểm thật vào prompt, chạy. Nhìn danh sách việc theo thứ tự, rồi **làm đúng việc số một**."

> "Một việc thôi. Xong khi bạn biết mình đang yếu ở tiêu chí nào — và đã sửa một thứ vì nó."

---

## 00:17–00:19 — Deploy (slide 10)

**Nói phần cảnh báo TRƯỚC khi họ bấm:**

> "Publish miễn phí, không cần thẻ. Nhưng nói trước để lát nữa không ai hoảng: Starter Tier chỉ áp dụng cho tài khoản Google **chưa từng publish** từ AI Studio."

> "Nếu màn hình đòi thẻ tín dụng — không phải bạn làm sai. Mở cửa sổ ẩn danh, hoặc dùng tài khoản khác. Facilitator có sẵn cách xử lý."

*(Đây là lỗi phổ biến nhất của cả buổi. Gọi tên nó trước khi nó xảy ra thì nó thành một bước dự kiến, chứ không phải sự cố.)*

---

## 00:19–00:22 — THỰC HÀNH 3: publish (slide 11, 3 phút)

> "Ba phút. Bấm Publish. Lấy link. **Mở link đó trên điện thoại của bạn**, rồi gửi vào nhóm chat."

> "Xong khi một người lạ mở được app của bạn mà không cần bạn ngồi cạnh."

**Làm:** đây là khoảnh khắc cả phòng có link thật. Để nó có không khí một chút — đọc to vài link đầu tiên xuất hiện trong nhóm chat.

---

## 00:22–00:25 — Nộp gì + video (slide 12–13)

**Slide 12 — nói to đoạn này.**

> "Chỗ này mất điểm oan nhiều nhất: **có hai cái link khác nhau**."

> "Link project là để giám khảo mở đúng dự án của bạn — thường là cái bắt buộc, và nhớ đặt sharing thành Public trước. Link app đã publish là để người ta dùng thử mà không thấy code — thường là điểm cộng."

> "Nộp nhầm cái này vào ô cần cái kia là cách mất điểm dễ nhất trong cả cuộc thi."

**Slide 13 — video.** Chỉ ô thứ hai:

> "Video 90 giây. Đa số video demo mất 40 giây cho màn đăng nhập rồi mới tới phần hay. Đừng. Khoảnh khắc hay ho phải xuất hiện **trước giây 40**."

Chỉ thẻ đỏ:

> "Và tuyệt đối không có trong video: sơ đồ kiến trúc, cấu trúc thư mục, và câu 'xin lỗi chỗ này còn bug'. Không ai bắt bạn xin lỗi cả."

---

## 00:25–00:29 — THỰC HÀNH 4: nộp (slide 14, 4 phút)

> "Bốn phút cuối, và đây là phần quan trọng nhất buổi hôm nay."

> "Đặt sharing thành Public. Copy cả hai link. Mở form. **Bấm nộp.** Video quay sau cũng được — nhưng link thì nộp ngay bây giờ."

> "Xong khi bạn nhận được xác nhận đã nộp."

**Làm:** đi vòng, hỏi thẳng từng người "nộp chưa?". Đây là lúc để hơi thúc một chút — đa số người không nộp là vì trì hoãn, không phải vì thiếu gì.

---

## 00:29–00:30 — Đóng (slide 15)

> "Bạn vừa nộp một *sản phẩm*, không phải một ý tưởng. Người khác mở link ra là dùng được."

> "Còn thời gian thì làm hai việc: quay video demo, và sửa tiếp việc số hai trong danh sách đánh giá. Nhưng phần khó nhất — bấm nút nộp — thì xong rồi."

> "Facilitator còn ở đây. Ai chưa nộp được thì giơ tay ngay bây giờ."

---

## Nếu bị trễ giờ

Cắt theo thứ tự:

1. THỰC HÀNH 2 (đánh giá) từ 4′ → 2′ — bảo họ chạy prompt, đọc, sửa sau
2. Slide 13 (video) — nói một câu, để họ đọc chi tiết trong deck sau
3. Slide 4 (khung test) — bỏ, vào thẳng prompt ở slide 5

**Không được cắt:** THỰC HÀNH 3 (publish) và THỰC HÀNH 4 (nộp). Nếu chỉ còn 10 phút, bỏ hết phần test và đánh giá, chạy thẳng hai khối đó. Một người nộp được bài quan trọng hơn một người hiểu về testing.

---

## Câu hay bị hỏi

**"Em vắng buổi 1, giờ làm sao?"**
> Bám theo bằng app mẫu — facilitator đưa link. Bạn vẫn học được cả bốn chặng cuối, và về nhà chạy lại từ chặng một.

**"App em còn xấu, nộp có kỳ không?"**
> Nộp. Bài nộp sửa được đến hạn chót; bài không nộp thì không. Và tiêu chí lớn nhất là *chạy được*, không phải *đẹp*.

**"Em chưa quay video, nộp thiếu có sao không?"**
> Link nộp trước. Video là điểm cộng, không phải điều kiện. Đừng để thiếu video làm bạn lỡ luôn cả bài.

**"Publish nó đòi thẻ tín dụng."**
> Tài khoản của bạn đã publish trước đây rồi. Mở cửa sổ ẩn danh với tài khoản khác. Nếu vẫn không được, dùng link Share với quyền Public — vẫn nộp được, chỉ mất phần điểm cộng.

**"Hết hai app Starter Tier rồi."**
> Giới hạn là 2 app mỗi tài khoản. Dùng tài khoản khác, hoặc unpublish một app cũ.

---

## Ghi chú nối hai buổi

Nếu hai buổi cách nhau xa, gửi trước buổi 2 một tin nhắn:

> "Buổi sau mang theo: app đang chạy được, và năm dòng quyết định của bạn. Chưa có app cũng cứ đến — có app mẫu để làm theo."

Điều này giải quyết được vấn đề lớn nhất của buổi 2: người đến tay không thì 30 phút không đủ để vừa build vừa nộp.
