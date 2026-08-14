# Script buổi 1 — 90 phút: "Từ ý tưởng đến app chạy được"

Deck: `docs/slides/mvp-pipeline-prompting-slides.html` (32 slide)
Khán giả: sinh viên / fresher / junior, có mang laptop
Kết quả mong muốn: mỗi người rời phòng với **một app chạy được trên điện thoại của chính mình**, và 3 artifact viết ra giấy (problem brief, quyết định, bộ token).

App làm ví dụ xuyên suốt: **Ươm Mầm** (`docs/newbie-guide-student-idea-team-funding-app-ai-studio.md`).

---

## Chuẩn bị trước (T-30 phút)

- [ ] Laptop sạc đầy + adapter HDMI/USB-C
- [ ] Deck mở sẵn, đã test **tắt wifi vẫn chạy**; bản PDF dự phòng để trên desktop
- [ ] Tab nền: `gemini.google.com` và `ai.dev` (đã đăng nhập)
- [ ] **Một tài khoản Google chưa từng publish** từ AI Studio — để demo Starter Tier
- [ ] App Ươm Mầm đã build sẵn, mở sẵn 1 tab (dùng khi có người kẹt)
- [ ] Điện thoại đã bật hotspot, đã test
- [ ] Tắt thông báo, để zoom trình duyệt về 100%
- [ ] Brief facilitator: mốc kiểm tra ở phút 10, và câu trả lời cho lỗi "đòi thẻ tín dụng"

**Nguyên tắc xuyên suốt:** khán giả mang laptop tới để *làm*, không phải để nghe. Bốn khối THỰC HÀNH là phần chính của buổi — phần nói chỉ để mở đường cho chúng.

---

## Bảng thời gian

| Thời gian | Slide | Nội dung | Dạng |
|---|---|---|---|
| 00:00–00:04 | 1–2 | Mở đầu + 8 chặng | Nói |
| 00:04–00:10 | 3–5 | Chuỗi artifact + khung prompt | Nói |
| 00:10–00:16 | 6–8 | Research | Nói |
| 00:16–00:26 | 9 | **THỰC HÀNH 1** | Làm (10′) |
| 00:26–00:33 | 10–13 | Brainstorm | Nói |
| 00:33–00:42 | 14 | **THỰC HÀNH 2** | Làm (9′) |
| 00:42–00:50 | 15–18 | Design system | Nói |
| 00:50–00:59 | 19 | **THỰC HÀNH 3** | Làm (9′) |
| 00:59–01:04 | 20–21 | Code | Nói |
| 01:04–01:17 | 22 | **THỰC HÀNH 4** | Làm (13′) |
| 01:17–01:19 | 23–26 | Lướt nhanh: test & đánh giá → buổi sau | Nói |
| 01:19–01:24 | 27 | Publish + publish tại chỗ | Làm |
| 01:24–01:28 | 30–31 | Tổng kết | Nói |
| 01:28–01:30 | 32 | Đóng + Q&A | Nói |

Tổng nói ≈ 45′ · tổng làm ≈ 45′.

---

## 00:00–00:04 — Mở đầu (slide 1–2)

**Slide 1.**

> "Chào mọi người. Hôm nay chúng ta không học cách gõ prompt cho đẹp. Chúng ta đi qua đúng tám bước để biến một ý tưởng trong đầu thành một cái link mà bạn gửi cho mẹ bạn, mẹ bạn bấm vào và dùng được."

> "Cuối buổi, mục tiêu là mỗi người ở đây có một app chạy trên điện thoại của mình. Không phải app của tôi — app của bạn."

**Slide 2 — tám chặng.**

Đừng đọc cả tám. Chỉ vào ba ô đầu (Research, Brainstorm, Design system) rồi nói:

> "Hầu hết mọi người bắt đầu ở ô số 4 — mở AI Studio ra và gõ 'làm cho tôi một cái app'. Đó là lý do sản phẩm của họ trông giống hệt nhau, và là lý do khi giám khảo hỏi 'sao bạn chọn cái này' thì không trả lời được."

> "Ba ô đầu tiên chiếm một phần tư thời gian và **không sinh ra dòng code nào**. Đó là phần cảm giác như đang lãng phí, và là phần quyết định."

---

## 00:04–00:10 — Chuỗi artifact + khung prompt (slide 3–5)

**Slide 3 — quan trọng nhất deck.**

> "Mỗi chặng đẻ ra một thứ cầm được. Research đẻ ra problem brief. Brainstorm đẻ ra một quyết định. Design đẻ ra bộ token."

> "Và đây là mấu chốt: **prompt của chặng sau ăn artifact của chặng trước**. Prompt build của bạn tốt không phải vì bạn viết prompt build giỏi — mà vì lúc đó bạn đã có sẵn bộ token và bản mô tả màn hình để dán vào."

**Slide 4 — khung 6 phần.** Lướt nhanh, không giảng từng dòng.

> "Tất cả prompt hôm nay đều cùng một khung. Chỉ có ruột đổi."

Dừng ở dòng ROLE:

> "Để ý: 'một researcher **luôn hoài nghi**' cho ra kết quả khác hẳn 'một researcher'. Cho nó một thái độ, đừng chỉ cho nó một chức danh."

**Slide 5 — kỹ thuật đắt giá nhất.**

> "Nếu cả buổi hôm nay bạn chỉ nhớ một dòng, thì nhớ dòng này."

Đọc to dòng trong khung, rồi:

> "Không có dòng đó, model tự lấp chỗ trống bằng giả định trung bình nhất — và bạn nhận về đúng thứ mà mọi người gõ prompt giống bạn cũng nhận được. Có dòng đó, chỗ trống được lấp bằng thông tin *của bạn*. Mất thêm một lượt hỏi đáp. Rẻ nhất trong tất cả các cách nâng chất lượng."

---

## 00:10–00:16 — Research (slide 6–8)

**Slide 6 (divider).**

> "Chặng một. Chặng ai cũng bỏ qua, vì ai cũng nghĩ mình đã hiểu vấn đề rồi."

**Slide 7 — prompt.** Đừng đọc cả prompt. Chỉ vào mục 3:

> "Đây là câu hỏi sắc nhất trong cả prompt này: **hôm nay họ đang xoay xở bằng cách nào?** Đối thủ thật của bạn không phải app khác — mà là cách người ta đang tự sống chung với vấn đề. Nếu cách đó đủ ổn, app của bạn không có cửa."

Chỉ hai dòng cuối:

> "Và hai dòng này giữ cho bạn không bị lừa: đánh dấu chỗ không chắc, cấm bịa số liệu."

**Slide 8 — lọc ảo giác.**

> "Research là chỗ ảo giác gây hại nhất, vì mọi chặng sau đều thừa hưởng một bản brief sai."

Chỉ callout đỏ:

> "Và cái bẫy khó thấy nhất: nếu output đồng ý với mọi thứ bạn đang tin, đó là cờ đỏ chứ không phải cờ xanh. Hỏi lại nó: *điều gì phải đúng thì kết luận này mới sai?*"

---

## 00:16–00:26 — THỰC HÀNH 1 (slide 9, 10 phút)

**Nói trước khi bấm giờ:**

> "Mười phút. Mở Gemini, dán prompt Research, điền ý tưởng của chính bạn vào. Chưa có ý tưởng cũng không sao — mượn tạm một cái, quan trọng là chạy được quy trình."

> "Xong khi bạn trả lời được: nhóm nào đau nhất, và hôm nay họ đang xoay xở thế nào."

**Làm:** đi vòng quanh phòng. Facilitator tỏa ra. Còn 2 phút thì báo.

**Cuối khối** — hỏi 2 người:

> "Ai chia sẻ nhanh: nhóm người dùng của bạn hôm nay đang xoay xở bằng cách gì?"

*(Đây là lúc kiểm tra cả phòng có chạy được prompt không. Nếu quá nửa phòng kẹt ở đăng nhập → chuyển sang chế độ demo, tôi làm trên màn hình, họ làm theo sau.)*

---

## 00:26–00:33 — Brainstorm (slide 10–13)

**Slide 10 (divider).**

> "Hai prompt riêng biệt: một để mở ra, một để cắt xuống. Gộp vào một tin nhắn thì bạn nhận được ba ý tưởng và một cái model đã trót thích sẵn."

**Slide 11 — diverge.** Chỉ vào bốn nhóm A/B/C/D:

> "Bốn cái rổ này mới là thứ có tác dụng. Không có chúng, bạn nhận về tám phiên bản của cùng một ý tưởng."

Chỉ dòng cuối:

> "Và **cấm nó xếp hạng**. Chốt sớm là cách chắc chắn nhất để bỏ lỡ ý tưởng hay."

**Slide 12 — converge.** Chỉ tiêu chí 4:

> "Tiêu chí này là chỗ nhiều người rớt: demo được trong 60 giây mà không cần giải thích trước. Nếu phải nói một đoạn dẫn nhập thì người ta mới hiểu — thì đó là MVP sai."

Chỉ dòng in đậm:

> "Và dòng này thì hơi đau: bảo nó chỉ ra ý tưởng bạn đang *yêu* nhất, rồi phản biện chính nó. Vì thứ giết dự án thường không phải ý tưởng tệ — mà là ý tưởng bạn không chịu buông."

**Slide 13 — artifact.**

> "Năm dòng. Viết ra. Hai tuần nữa bạn sẽ không nhớ vì sao mình chọn cái này, và bạn sẽ trôi ngược về ý tưởng đã cắt."

> "Dòng KHÔNG LÀM còn dùng lại hai lần nữa: nó là lá chắn phạm vi lúc code, và là câu 'những gì chúng tôi cố tình không làm' trong bài nộp."

---

## 00:33–00:42 — THỰC HÀNH 2 (slide 14, 9 phút)

> "Chín phút. Dán problem brief vừa nãy vào prompt diverge. **Đọc hết tám ý tưởng** rồi mới chạy prompt converge. Đừng gộp."

> "Xong khi bạn viết được năm dòng: CHỌN / CHO AI / VÌ / CHẾT NẾU / KHÔNG LÀM."

**Cuối khối** — hỏi một người đọc to năm dòng của họ.

---

## 00:42–00:50 — Design system (slide 15–18)

**Slide 15 (divider).**

> "Chặng này là khác biệt lớn nhất giữa một MVP trông *có thiết kế* và một MVP trông *do máy đẻ ra*."

**Slide 16 — vì sao token trước.**

> "'Làm cho đẹp đi' là câu không có trí nhớ. Màn hình một xanh thế này, màn hình bốn xanh thế khác, và đến lúc đó sửa là sửa tay từng chỗ."

> "Làm token trước thì tính nhất quán là *cấu trúc*, không phải thứ bạn phải đi canh."

**Slide 17 — prompt design system.** Chỉ dòng WCAG:

> "Dòng này bắt nó tự kiểm tra độ tương phản. Accessibility gần như luôn nằm trong tiêu chí chấm điểm, và gần như không ai làm. Một dòng prompt, ăn điểm thật."

**Slide 18 — prompt màn hình.** Chỉ hai chỗ:

> "'CHỈ dùng token ở trên' — đó là ràng buộc làm việc. Và dòng cuối: bắt nó khai ra chỗ nào bộ token không đủ, thay vì tự bịa thêm màu. Đó là cách bạn phát hiện thiết kế đang trôi."

Chỉ callout xanh:

> "Empty state và error state — hỏi thẳng tên ra. Đó là chỗ UI do AI sinh ra vỡ đầu tiên, và cũng là chỗ người dùng thật rơi vào trước tiên."

---

## 00:50–00:59 — THỰC HÀNH 3 (slide 19, 9 phút)

> "Chín phút. Chạy prompt design system. **Giữ lại bộ CSS variables** — lát nữa dán thẳng vào prompt build, đừng để lạc."

---

## 00:59–01:04 — Code (slide 20–21)

**Slide 20 — xây theo lớp.**

> "Đừng xin tất cả trong một prompt. Xin từng lớp, test sau mỗi lớp. Vì khi bạn xin mười thứ cùng lúc và nó vỡ, bạn không biết chỉ thị nào gây ra."

**Slide 21 — prompt build.**

> "Nhìn xem prompt này ngắn thế nào. Nó ngắn được vì nó *thừa hưởng*: token từ chặng 3, mô tả màn hình từ chặng 3, quyết định từ chặng 2."

Chỉ dòng scope:

> "Và dòng này giữ mạng cho bạn: **không routing, không đăng nhập, không database**. Bỏ dòng này ra, model sẽ dựng cho bạn một cái dashboard có sidebar và bạn hết giờ."

---

## 01:04–01:17 — THỰC HÀNH 4 (slide 22, 13 phút)

> "Mười ba phút — khối dài nhất. Mở ai.dev, vào Build, dán prompt build kèm bộ token của bạn."

> "Xong khi app chạy được **trên điện thoại của bạn** — không phải trên laptop. Ai xong sớm thì bấm Publish luôn, tôi sẽ nói về nó ngay sau đây."

**Làm:** facilitator tỏa ra. Còn 3 phút thì báo. Ai kẹt hoàn toàn → đưa link app Ươm Mầm dựng sẵn để họ đi tiếp từ bước sau.

---

## 01:17–01:19 — Lướt nhanh test & đánh giá (slide 23–26)

Bấm qua nhanh, khoảng 30 giây mỗi cặp:

> "Còn hai chặng nữa: test và đánh giá. Test thì không phải test cho đủ coverage — test để app sống sót bốn phút trước mặt người lạ. Đánh giá thì là chấm app của mình theo đúng thang điểm sẽ bị chấm."

> "Hai cái này ta làm kỹ ở buổi sau, khi mọi người đã có app trong tay."

---

## 01:19–01:24 — Publish (slide 27)

> "Bây giờ lấy link thật. Miễn phí, không cần thẻ."

**Nói TRƯỚC khi họ bấm** — quan trọng:

> "Một điều nói trước để lát nữa không ai hoảng: Starter Tier chỉ áp dụng cho tài khoản Google **chưa từng publish** từ AI Studio. Nếu nó đòi thẻ tín dụng, không phải bạn làm sai — chỉ cần mở cửa sổ ẩn danh hoặc dùng tài khoản khác."

*(Nói trước thì đây là một bước có dự kiến. Nói sau thì nó là sự cố.)*

**Làm:** bấm Publish trên màn hình, mở link trên điện thoại, giơ lên. Rồi:

> "Bốn phút, mọi người làm y hệt. Có link rồi thì gửi vào nhóm chat."

---

## 01:24–01:28 — Tổng kết (slide 30–31)

**Slide 30 — ngân sách giờ.**

> "Nếu bạn có một cuối tuần, đây là chỗ giờ thực sự đi. Để ý ba chặng đầu: một phần tư thời gian, không có dòng code nào."

**Slide 31 — bỏ chặng.**

> "Và đây là phần thật lòng. Bỏ chặng không tiết kiệm được thời gian — nó quay lại dưới dạng làm lại, vào lúc tệ hơn, khi bạn còn ít thời gian hơn."

---

## 01:28–01:30 — Đóng (slide 32)

> "Buổi sau chúng ta lấy chính app này, tìm chỗ nó vỡ, chấm điểm nó theo thang thật, rồi nộp — nộp ngay trong phòng, không phải 'về nhà rồi nộp'."

> "Từ giờ đến đó: chạy prompt research trên một ý tưởng thứ hai. Bạn sẽ thấy chặng một tự nhiên hẳn ở lần thứ hai."

---

## Nếu bị trễ giờ

Cắt theo đúng thứ tự này:

1. Slide 23–26 (lướt test/đánh giá) — bỏ hẳn, để buổi sau
2. Slide 31 (bỏ chặng) — gộp một câu vào slide 30
3. THỰC HÀNH 3 từ 9′ → 6′, bảo họ chỉ lấy phần màu và chữ
4. Slide 13 (artifact brainstorm) — nói miệng thay vì chiếu

**Không được cắt:** THỰC HÀNH 1, THỰC HÀNH 4, và Publish. Ba cái đó là buổi học.

---

## Câu hay bị hỏi

**"Em chưa có ý tưởng gì cả."**
> Tốt — hôm nay mượn tạm một cái. Chạy đúng quy trình mới là thứ mang về được. Ý tưởng thì tuần sau có.

**"Sao phải làm design system, em vẽ tay nhanh hơn?"**
> Với một màn hình thì đúng là nhanh hơn. Với bốn màn hình thì bạn có bốn phong cách. Và bộ token là thứ bạn dán vào prompt build — nó không chỉ để nhìn.

**"AI Studio hết quota thì sao?"**
> Đợi vài phút rồi thử lại. Đừng tạo tài khoản thứ hai giữa buổi — mất nhiều thời gian hơn là chờ.

**"Em dùng tiếng Việt hay tiếng Anh trong prompt?"**
> Prompt tiếng Anh thường ổn định hơn. Nhưng nhớ ghi rõ trong prompt là **giao diện và output phải bằng tiếng Việt**.

**"Có bắt buộc dùng đúng các prompt này không?"**
> Không. Chúng là điểm khởi đầu. Cái cần giữ là *thứ tự* và *artifact* — còn chữ nghĩa thì sửa cho hợp với bạn.
