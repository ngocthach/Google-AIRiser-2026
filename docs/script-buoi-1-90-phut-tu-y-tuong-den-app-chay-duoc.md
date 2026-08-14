# Script buổi 1 — 90 phút: "Từ ý tưởng đến app chạy được"

Deck: `docs/slides/mvp-pipeline-prompting-slides.html` (34 slide)
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
| 00:10–00:16 | 6–9 | Research + ví dụ điền Ươm Mầm | Nói |
| 00:16–00:26 | 10 | **THỰC HÀNH 1** | Làm (10′) |
| 00:26–00:33 | 11–14 | Brainstorm | Nói |
| 00:33–00:42 | 15 | **THỰC HÀNH 2** | Làm (9′) |
| 00:42–00:50 | 16–19 | Design system | Nói |
| 00:50–00:59 | 20 | **THỰC HÀNH 3** | Làm (9′) |
| 00:59–01:04 | 21–23 | Code + ví dụ điền build prompt | Nói |
| 01:04–01:17 | 24 | **THỰC HÀNH 4** | Làm (13′) |
| 01:17–01:19 | 25–28 | Lướt nhanh: test & đánh giá → buổi sau | Nói |
| 01:19–01:24 | 29 | Publish + publish tại chỗ | Làm |
| 01:24–01:28 | 32–33 | Tổng kết | Nói |
| 01:28–01:30 | 34 | Đóng + Q&A | Nói |

Tổng nói ≈ 45′ · tổng làm ≈ 45′.

---

## Hai tool, đừng để khán giả mở nhầm

| Tool | Chặng | Slide |
|---|---|---|
| **Gemini chat** — `gemini.google.com` | 01 Research · 02 Brainstorm · 03 Design | 7, 9, **10** · 12, 13, **15** · 18, 19, **20** |
| **AI Studio** — `ai.dev` → Build | 04 Code · 07 Deploy | 21, 22, 23, **24** · 29 |

Mỗi slide có việc phải làm đều mang **badge tool ở góc phải trên**. Khi chuyển tool thì chỉ tay lên đó, đừng chỉ nói.

**Quy tắc một câu để khán giả nhớ:**

> "Output là chữ để đọc → Gemini. Output là app để nhìn → AI Studio."

**Nói rõ ở đầu buổi** (slide 6, khi mở chặng Research):

> "Ba chặng đầu chúng ta làm trong Gemini chat, không phải AI Studio. Vì AI Studio Build mode gắn với việc *dựng app* — dán prompt research vào đó thì nó dựng cho bạn một cái app research, chứ không phân tích. Mở sẵn hai tab, đến lúc nào dùng cái nào thì trên slide có ghi."

*(AI Studio có Playground mode là chat thuần, dùng được — nhưng bắt người mới đổi qua lại giữa hai mode giữa buổi thì rối hơn là mở hai tab.)*

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

## 00:10–00:16 — Research (slide 6–9)

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

**Slide 9 — ví dụ điền thật cho Ươm Mầm.**

> "Đây chính là prompt vừa nãy, điền thật. Bước 1 đến 6 y nguyên — chỉ phần bối cảnh đổi."

Chỉ vào câu 7 và 8:

> "Hai câu này em thêm riêng cho Ươm Mầm, vì đây là hai thứ có thể giết ý tưởng. Thứ nhất: '6 đến 22 tuổi' — học sinh lớp 2 và sinh viên năm 3 không dùng chung một sản phẩm nào cả. Thứ hai: với nhóm dưới 13 tuổi, người gật đầu không phải học sinh mà là **giáo viên**. Đó là câu hỏi phân phối, và nó quyết định sản phẩm nhiều hơn tính năng."

> "Bài học ở đây: prompt chung là bộ khung. Bạn phải tự thêm một hai câu mà chỉ ý tưởng *của bạn* mới cần."

Prompt đầy đủ (trên slide chỉ hiện phần khác biệt):

```
You are a product researcher who is skeptical by default.

Goal: decide whether this problem is real and worth building for,
before I write any code.

  PROBLEM: Students have project ideas but never build them. They
  can't find teammates with complementary skills, they have no way
  to show the idea to anyone outside their class, and nobody funds
  or supports a student project that has no track record. So the
  idea stays in a notebook and dies.

  The product I'm considering: "Ươm Mầm" — students post an idea,
  others ask to join, a team forms, the team posts progress, and
  when ready the team opens a campaign where the community pledges
  support (money, materials, mentoring, or hours — pledges only,
  no payment processing).

Context: MVP for students in Vietnam, ages 6 to 22, spanning primary
school through university. Market: Vietnam. I have roughly 15-25
hours total across evenings, deadline 30/08/2026, working solo.

Do this:
1. Restate the problem in one sentence, as a USER would say it —
   not as I said it. Give me two versions: one as a 10-year-old
   would say it, one as a 20-year-old would say it.
2. Split who has it into 3 segments. Say which segment feels it
   most acutely, and why.
3. For each segment: what do they do today instead?
   (the status quo is the real competitor, not other apps)
   Be specific about Vietnam — school clubs, Facebook groups,
   Zalo, doan/hoi activities, existing school programs.
4. List 5 existing solutions. For each: what it does well, and
   the specific gap it leaves. Include non-app answers — a teacher
   running a club, a school science fair, a Facebook group.
5. List the 3 assumptions that, if wrong, kill this idea.
6. The cheapest way to test the riskiest one this week, without
   building anything.

Then two more, specific to this product:
7. I have written "ages 6 to 22" as one audience. Argue that this
   is wrong. What breaks if a 7-year-old and a 21-year-old use the
   same product? If you think I should narrow it, name the single
   age band you'd keep and what I lose by cutting the rest.
8. Who actually has to say yes for this to reach users — the
   student, the parent, the teacher, or the school? Whoever it is,
   what do they need to see before they say yes?

Rules: mark anything you are unsure about as [UNVERIFIED].
Never invent statistics, market sizes, or company names.
Before you answer, ask me the 3 questions whose answers would most
change your response. Wait for my answers.
```

---

## 00:16–00:26 — THỰC HÀNH 1 (slide 10, 10 phút)

**Nói trước khi bấm giờ:**

> "Mười phút. Mở Gemini, dán prompt Research, điền ý tưởng của chính bạn vào. Chưa có ý tưởng cũng không sao — mượn tạm một cái, quan trọng là chạy được quy trình."

> "Xong khi bạn trả lời được: nhóm nào đau nhất, và hôm nay họ đang xoay xở thế nào."

**Làm:** đi vòng quanh phòng. Facilitator tỏa ra. Còn 2 phút thì báo.

**Cuối khối** — hỏi 2 người:

> "Ai chia sẻ nhanh: nhóm người dùng của bạn hôm nay đang xoay xở bằng cách gì?"

*(Đây là lúc kiểm tra cả phòng có chạy được prompt không. Nếu quá nửa phòng kẹt ở đăng nhập → chuyển sang chế độ demo, tôi làm trên màn hình, họ làm theo sau.)*

---

## 00:26–00:33 — Brainstorm (slide 11–14)

**Slide 10 (divider).**

> "Hai prompt riêng biệt: một để mở ra, một để cắt xuống. Gộp vào một tin nhắn thì bạn nhận được ba ý tưởng và một cái model đã trót thích sẵn."

**Slide 12 — diverge.** Chỉ vào bốn nhóm A/B/C/D:

> "Bốn cái rổ này mới là thứ có tác dụng. Không có chúng, bạn nhận về tám phiên bản của cùng một ý tưởng."

Chỉ dòng cuối:

> "Và **cấm nó xếp hạng**. Chốt sớm là cách chắc chắn nhất để bỏ lỡ ý tưởng hay."

**Slide 13 — converge.** Chỉ tiêu chí 4:

> "Tiêu chí này là chỗ nhiều người rớt: demo được trong 60 giây mà không cần giải thích trước. Nếu phải nói một đoạn dẫn nhập thì người ta mới hiểu — thì đó là MVP sai."

Chỉ dòng in đậm:

> "Và dòng này thì hơi đau: bảo nó chỉ ra ý tưởng bạn đang *yêu* nhất, rồi phản biện chính nó. Vì thứ giết dự án thường không phải ý tưởng tệ — mà là ý tưởng bạn không chịu buông."

**Slide 14 — artifact.**

> "Năm dòng. Viết ra. Hai tuần nữa bạn sẽ không nhớ vì sao mình chọn cái này, và bạn sẽ trôi ngược về ý tưởng đã cắt."

> "Dòng KHÔNG LÀM còn dùng lại hai lần nữa: nó là lá chắn phạm vi lúc code, và là câu 'những gì chúng tôi cố tình không làm' trong bài nộp."

---

## 00:33–00:42 — THỰC HÀNH 2 (slide 15, 9 phút)

> "Chín phút. Dán problem brief vừa nãy vào prompt diverge. **Đọc hết tám ý tưởng** rồi mới chạy prompt converge. Đừng gộp."

> "Xong khi bạn viết được năm dòng: CHỌN / CHO AI / VÌ / CHẾT NẾU / KHÔNG LÀM."

**Cuối khối** — hỏi một người đọc to năm dòng của họ.

---

## 00:42–00:50 — Design system (slide 16–19)

**Slide 15 (divider).**

> "Chặng này là khác biệt lớn nhất giữa một MVP trông *có thiết kế* và một MVP trông *do máy đẻ ra*."

**Slide 17 — vì sao token trước.**

> "'Làm cho đẹp đi' là câu không có trí nhớ. Màn hình một xanh thế này, màn hình bốn xanh thế khác, và đến lúc đó sửa là sửa tay từng chỗ."

> "Làm token trước thì tính nhất quán là *cấu trúc*, không phải thứ bạn phải đi canh."

**Slide 18 — prompt design system.** Chỉ dòng WCAG:

> "Dòng này bắt nó tự kiểm tra độ tương phản. Accessibility gần như luôn nằm trong tiêu chí chấm điểm, và gần như không ai làm. Một dòng prompt, ăn điểm thật."

**Slide 19 — prompt màn hình.** Chỉ hai chỗ:

> "'CHỈ dùng token ở trên' — đó là ràng buộc làm việc. Và dòng cuối: bắt nó khai ra chỗ nào bộ token không đủ, thay vì tự bịa thêm màu. Đó là cách bạn phát hiện thiết kế đang trôi."

Chỉ callout xanh:

> "Empty state và error state — hỏi thẳng tên ra. Đó là chỗ UI do AI sinh ra vỡ đầu tiên, và cũng là chỗ người dùng thật rơi vào trước tiên."

---

## 00:50–00:59 — THỰC HÀNH 3 (slide 20, 9 phút)

> "Chín phút. Chạy prompt design system. **Giữ lại bộ CSS variables** — lát nữa dán thẳng vào prompt build, đừng để lạc."

---

## 00:59–01:04 — Code (slide 21–23)

**Slide 21 — xây theo lớp.**

> "Đừng xin tất cả trong một prompt. Xin từng lớp, test sau mỗi lớp. Vì khi bạn xin mười thứ cùng lúc và nó vỡ, bạn không biết chỉ thị nào gây ra."

**Slide 22 — prompt build.**

> "Nhìn xem prompt này ngắn thế nào. Nó ngắn được vì nó *thừa hưởng*: token từ chặng 3, mô tả màn hình từ chặng 3, quyết định từ chặng 2."

Chỉ dòng scope:

> "Và dòng này giữ mạng cho bạn: **không routing, không đăng nhập, không database**. Bỏ dòng này ra, model sẽ dựng cho bạn một cái dashboard có sidebar và bạn hết giờ."

**Slide 23 — ví dụ điền thật, từ một lần chạy có thật.**

> "Đây là prompt build đó, điền bằng kết quả thật của chặng 1 đến 3."

Chỉ vào tên sản phẩm:

> "Để ý: sản phẩm không còn tên 'Ươm Mầm cho 6–22 tuổi' nữa. Sau chặng Research nó thành **The Proof-of-Work Protocol**, chỉ cho sinh viên 18–22. Vì Gemini chỉ ra Nghị định 13/2023 bắt buộc xác thực tuổi và xin phép cha mẹ cho trẻ dưới 16 — một người làm solo trong 25 giờ không thể làm nổi."

> "Đó **không phải đi lạc. Đó là pipeline đang làm việc.** Thà đổi hướng ở chặng 1 khi chưa viết dòng code nào, còn hơn phát hiện ra sau khi đã build xong."

Chỉ nút COPY FULL:

> "Trên màn hình tôi chỉ để phần rút gọn cho dễ đọc. Bấm nút này là copy đủ cả bộ token — đừng ngồi chép tay từ máy chiếu."

---

## 01:04–01:17 — THỰC HÀNH 4 (slide 24, 13 phút)

> "Mười ba phút — khối dài nhất. Mở ai.dev, vào Build, dán prompt build kèm bộ token của bạn."

> "Xong khi app chạy được **trên điện thoại của bạn** — không phải trên laptop. Ai xong sớm thì bấm Publish luôn, tôi sẽ nói về nó ngay sau đây."

**Làm:** facilitator tỏa ra. Còn 3 phút thì báo. Ai kẹt hoàn toàn → đưa link app Ươm Mầm dựng sẵn để họ đi tiếp từ bước sau.

---

## 01:17–01:19 — Lướt nhanh test & đánh giá (slide 25–28)

Bấm qua nhanh, khoảng 30 giây mỗi cặp:

> "Còn hai chặng nữa: test và đánh giá. Test thì không phải test cho đủ coverage — test để app sống sót bốn phút trước mặt người lạ. Đánh giá thì là chấm app của mình theo đúng thang điểm sẽ bị chấm."

> "Hai cái này ta làm kỹ ở buổi sau, khi mọi người đã có app trong tay."

---

## 01:19–01:24 — Publish (slide 29)

> "Bây giờ lấy link thật. Miễn phí, không cần thẻ."

**Nói TRƯỚC khi họ bấm** — quan trọng:

> "Một điều nói trước để lát nữa không ai hoảng: Starter Tier chỉ áp dụng cho tài khoản Google **chưa từng publish** từ AI Studio. Nếu nó đòi thẻ tín dụng, không phải bạn làm sai — chỉ cần mở cửa sổ ẩn danh hoặc dùng tài khoản khác."

*(Nói trước thì đây là một bước có dự kiến. Nói sau thì nó là sự cố.)*

**Làm:** bấm Publish trên màn hình, mở link trên điện thoại, giơ lên. Rồi:

> "Bốn phút, mọi người làm y hệt. Có link rồi thì gửi vào nhóm chat."

**Lưu ý điều hướng:** slide 30–31 (nộp bài + video demo) là nội dung **buổi 2**. Bấm lướt qua trong 10 giây — "hai cái này buổi sau" — rồi vào slide 31. Đừng dừng lại giảng, sẽ hụt giờ tổng kết.

---

## 01:24–01:28 — Tổng kết (slide 32–33)

**Slide 32 — ngân sách giờ.**

> "Nếu bạn có một cuối tuần, đây là chỗ giờ thực sự đi. Để ý ba chặng đầu: một phần tư thời gian, không có dòng code nào."

**Slide 33 — bỏ chặng.**

> "Và đây là phần thật lòng. Bỏ chặng không tiết kiệm được thời gian — nó quay lại dưới dạng làm lại, vào lúc tệ hơn, khi bạn còn ít thời gian hơn."

---

## 01:28–01:30 — Đóng (slide 34)

> "Buổi sau chúng ta lấy chính app này, tìm chỗ nó vỡ, chấm điểm nó theo thang thật, rồi nộp — nộp ngay trong phòng, không phải 'về nhà rồi nộp'."

> "Từ giờ đến đó: chạy prompt research trên một ý tưởng thứ hai. Bạn sẽ thấy chặng một tự nhiên hẳn ở lần thứ hai."

---

## Nếu bị trễ giờ

Cắt theo đúng thứ tự này:

1. Slide 25–28 (lướt test/đánh giá) — bỏ hẳn, để buổi sau
2. Slide 33 (bỏ chặng) — gộp một câu vào slide 31
3. THỰC HÀNH 3 từ 9′ → 6′, bảo họ chỉ lấy phần màu và chữ
4. Slide 14 (artifact brainstorm) — nói miệng thay vì chiếu

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
