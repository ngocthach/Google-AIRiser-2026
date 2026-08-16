# Script buổi 1 — 90 phút: "Từ ý tưởng đến app chạy được"

Deck: `docs/slides/mvp-pipeline-prompting-slides.html` (39 slide)
Khán giả: sinh viên / fresher / junior, có mang laptop
Kết quả mong muốn: mỗi người rời phòng với **một app chạy được trên điện thoại của chính mình**, và 4 artifact viết ra giấy (problem brief, quyết định, bản kế hoạch, bộ token).

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

**Nguyên tắc xuyên suốt:** khán giả mang laptop tới để *làm*, không phải để nghe. Năm khối THỰC HÀNH là phần chính của buổi — phần nói chỉ để mở đường cho chúng.

---

## Bảng thời gian

| Thời gian | Slide | Nội dung | Dạng |
|---|---|---|---|
| 00:00–00:04 | 1–2 | Mở đầu + 9 chặng | Nói |
| 00:04–00:10 | 3–5 | Chuỗi artifact + khung prompt | Nói |
| 00:10–00:16 | 6–9 | Research + ví dụ điền Ươm Mầm | Nói |
| 00:16–00:26 | 10 | **THỰC HÀNH 1** | Làm (10′) |
| 00:26–00:33 | 11–14 | Brainstorm | Nói |
| 00:33–00:42 | 15 | **THỰC HÀNH 2** | Làm (9′) |
| 00:42–00:47 | 16–18 | **Plan** — cắt phạm vi + chốt stack | Nói (5′) |
| 00:47–00:54 | 19 | **THỰC HÀNH 3** | Làm (7′) |
| 00:54–01:02 | 20–23 | Design system | Nói (8′) |
| 01:02–01:11 | 24 | **THỰC HÀNH 4** | Làm (9′) |
| 01:11–01:18 | 25–28 | Code + hai ví dụ điền build prompt | Nói (7′) |
| 01:18–01:31 | 29 | **THỰC HÀNH 5** | Làm (13′) |
| 01:31–01:36 | 30–31 | Test | Nói (5′) |
| 01:36–01:41 | 32–33 | Đánh giá | Nói (5′) |
| 01:41–01:47 | 34 | Publish + publish tại chỗ | Làm (6′) |
| 01:47–01:53 | 35–36 | Nộp bài & video demo | Nói (6′) |
| 01:53–01:57 | 37–38 | Tổng kết | Nói (4′) |
| 01:57–01:59 | 39 | Đóng + Q&A | Nói (2′) |

**Bảng trên là bản đầy đủ — 119 phút**, chạy hết cả 9 chặng.

Đến 01:31 là khung cứng: năm slide THỰC HÀNH đều có đồng hồ đếm phút hiện trên màn hình (10 / 9 / 7 / 9 / 13), lệch là slide nói dối anh giữa buổi.

**Để về 90 phút** thì cắt theo thứ tự này:

| Cắt gì | Tiết kiệm |
|---|---|
| Nộp bài & video (34–35) → bỏ hẳn, là nội dung buổi 2 | 6′ |
| Test (29–30) → nói 1 phút thay vì 5 | 4′ |
| Đánh giá (31–32) → nói 1 phút thay vì 5 | 4′ |
| THỰC HÀNH 3 Plan (19) → 7′ còn 4′, chỉ chốt stack tại chỗ | 3′ |
| THỰC HÀNH 4 Design (24) → 9′ còn 6′ | 3′ |
| Code (25–27) → bỏ slide ví dụ điền build prompt (27) | 2′ |
| Publish (33) → demo trên màn hình, khán giả làm ở nhà | 4′ |

Cắt hết → **91 phút**. Đừng dạy trùng nội dung buổi 2 nếu hai buổi cách nhau gần.

**Chặng Plan (16–19) thì đừng cắt.** Nó là chặng quyết định stack — bỏ nó thì prompt build ở slide 26 lại rơi vào cảnh "React, Tailwind" mà không ai chọn.

---

## Hai tool, đừng để khán giả mở nhầm

| Tool | Chặng | Slide |
|---|---|---|
| **Gemini chat** — `gemini.google.com` | 01 Research · 02 Brainstorm · 03 Plan · 04 Design | 7, 9, **10** · 12, 13, **15** · 17, **19** · 22, 23, **24** |
| **AI Studio** — `ai.dev` → Build | 05 Code · 08 Deploy | 25, 26, 27, 28, **29** · 34 |

Mỗi slide có việc phải làm đều mang **badge tool ở góc phải trên**. Khi chuyển tool thì chỉ tay lên đó, đừng chỉ nói.

**Quy tắc một câu để khán giả nhớ:**

> "Output là chữ để đọc → Gemini. Output là app để nhìn → AI Studio."

**Nói rõ ở đầu buổi** (slide 6, khi mở chặng Research):

> "Ba chặng đầu chúng ta làm trong Gemini chat, không phải AI Studio. Vì AI Studio Build mode gắn với việc *dựng app* — dán prompt research vào đó thì nó dựng cho bạn một cái app research, chứ không phân tích. Mở sẵn hai tab, đến lúc nào dùng cái nào thì trên slide có ghi."

*(AI Studio có Playground mode là chat thuần, dùng được — nhưng bắt người mới đổi qua lại giữa hai mode giữa buổi thì rối hơn là mở hai tab.)*

---

## 00:00–00:04 — Mở đầu (slide 1–2)

**Slide 1.**

> "Chào mọi người. Hôm nay chúng ta không học cách gõ prompt cho đẹp. Chúng ta đi qua đúng chín bước để biến một ý tưởng trong đầu thành một cái link mà bạn gửi cho mẹ bạn, mẹ bạn bấm vào và dùng được."

> "Cuối buổi, mục tiêu là mỗi người ở đây có một app chạy trên điện thoại của mình. Không phải app của tôi — app của bạn."

**Slide 2 — chín chặng.**

Đừng đọc cả chín. Chỉ vào bốn ô đầu (Research, Brainstorm, Plan, Design) rồi nói:

> "Hầu hết mọi người bắt đầu ở ô số 5 — mở AI Studio ra và gõ 'làm cho tôi một cái app'. Đó là lý do sản phẩm của họ trông giống hệt nhau, và là lý do khi giám khảo hỏi 'sao bạn chọn cái này' thì không trả lời được."

> "Bốn ô đầu tiên chiếm một phần ba thời gian và **không sinh ra dòng code nào**. Đó là phần cảm giác như đang lãng phí, và là phần quyết định."

---

## 00:04–00:10 — Chuỗi artifact + khung prompt (slide 3–5)

**Slide 3 — quan trọng nhất deck.**

> "Mỗi chặng đẻ ra một thứ cầm được. Research đẻ ra problem brief. Brainstorm đẻ ra một quyết định. Plan đẻ ra danh sách tính năng và stack. Design đẻ ra bộ token."

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

Chỉ nút **COPY FULL**, rồi nói:

> "Năm dòng này là thứ *bạn* phải nhớ. Nhưng khi cần người khác hiểu sản phẩm của bạn — bạn đời, giám khảo, hay một người bạn muốn rủ vào nhóm — thì năm dòng là chưa đủ."

> "Bấm COPY FULL, bạn được thêm một prompt biến năm dòng này thành **PRD một trang**. Sáu mục: vấn đề, cho ai, thế nào là thành công, user story, ngoài phạm vi, và câu hỏi còn bỏ ngỏ."

Nhấn hai ràng buộc trong prompt đó — đây mới là phần đáng nói:

> "Thứ nhất: **không có timeline, không có cơ cấu nhóm, không có lựa chọn công nghệ.** Mấy thứ đó là việc của chặng Plan. PRD chỉ nói về sản phẩm."

> "Thứ hai: **mục nào cần hơn 120 chữ nghĩa là bạn chưa quyết định đủ** — và prompt bắt nó nói thẳng ra thay vì viết cho dài. PRD dài không phải là PRD tốt; nó thường là chỗ giấu những thứ mình chưa nghĩ xong."

*(Nếu có người hỏi "PRD có bắt buộc không?" — không. Năm dòng là đủ để một mình bạn làm. PRD là khi có người thứ hai.)*

---

## 00:33–00:42 — THỰC HÀNH 2 (slide 15, 9 phút)

> "Chín phút. Dán problem brief vừa nãy vào prompt diverge. **Đọc hết tám ý tưởng** rồi mới chạy prompt converge. Đừng gộp."

> "Xong khi bạn viết được năm dòng: CHỌN / CHO AI / VÌ / CHẾT NẾU / KHÔNG LÀM."

**Cuối khối** — hỏi một người đọc to năm dòng của họ.

---

## 00:42–00:47 — Plan (slide 16–18)

**Slide 16 (divider).**

> "Chặng ba. Chặng này lúc đầu không có trong bài — tôi thêm vào sau khi soát lại quy trình và phát hiện một lỗ hổng."

**Slide 17 — prompt Plan.**

Chỉ callout đỏ trước, vì đó là lý do chặng này tồn tại:

> "Nhìn trước tới prompt build ở cuối buổi: nó ghi 'React, Tailwind'. Nhưng **không chặng nào quyết định điều đó cả** — nó chỉ xuất hiện, như thể đương nhiên. Tương tự: Firebase hay lưu tạm trong trình duyệt? Model nào? Bao nhiêu màn hình? Không ai chốt."

> "Và câu hỏi lớn hơn: **hai mươi giờ có đủ không?** Nếu không hỏi bây giờ, bạn sẽ biết câu trả lời vào lúc hết giờ."

Chỉ dòng in đậm đầu prompt — đây là chỗ hay bị hiểu sai:

> "Để ý dòng này: **'đừng nhắc lại sản phẩm, người dùng, hay tính năng'**. Mấy thứ đó chốt xong ở chặng 2 rồi. Chặng này chỉ trả lời hai câu: **dựng bằng gì**, và **có vừa không**."

> "Đây là cách chia của Spec-Driven Development: tách *cái gì* ra khỏi *làm thế nào*. Trộn hai thứ lại là lúc phạm vi âm thầm phình ra — vì mỗi lần bàn kỹ thuật, người ta lại nghĩ ra thêm tính năng."

**PART A — HOW.**

> "Màn hình, stack, mô hình dữ liệu. Ba thứ. Và dòng về AI phải ghi đủ ba mảnh: SDK nào, model nào, **key nằm ở đâu**."

**PART B — TASKS.** Nói chậm phần này:

> "Mỗi task bốn cột: làm ra cái gì, mấy giờ, phụ thuộc task nào, và **tiêu chí duy nhất nói rằng nó xong**."

> "Cột cuối là cột hay bị bỏ. Không có nó, 'làm màn hình Gate' là một việc không bao giờ kết thúc — lúc nào cũng còn sửa được. Có nó — *'link được chấp nhận hoặc bị từ chối'* — thì có một khoảnh khắc rõ ràng để dừng."

**Và đây là dòng đắt nhất cả prompt:**

> "**'Cộng giờ lại. Nếu vượt quá ngân sách, đừng đưa kế hoạch cho tôi — hãy cắt bớt cho vừa, rồi nói rõ đã cắt gì.'**"

> "Bình thường bạn hỏi 'kế hoạch này ổn không', model bảo ổn. Dòng này bắt nó **tự làm phép cộng** rồi đối chiếu với thời gian bạn có. Kế hoạch tự kiểm tra chính nó."

> "Và tôi thêm cả chiều ngược lại: nếu tổng dưới một nửa ngân sách thì hoặc bạn đặt phạm vi quá nhỏ, hoặc nó ước lượng quá lạc quan — bắt nó nói rõ là cái nào."

Dòng cuối — dòng này cần giải thích, vì hai chữ "boring" hay bị hiểu nhầm:

> "**'Prefer boring technology over interesting technology.'** Boring ở đây **không phải là thứ bạn đã quen** — mà là thứ *cả ngành* đã quen. Bạn có thể chưa từng dùng Firebase, nó vẫn là boring tech, vì hàng triệu người đã dùng và mọi lỗi đều có câu trả lời từ năm 2019."

> "Ngược lại, một framework mới ra tháng trước mà bạn vừa đọc thấy hay — đó là interesting tech, dù bạn thấy quen. Thế giới chưa kịp mắc đủ lỗi với nó."

**Và đây mới là lý do thật, khi làm với AI:**

> "Model học từ những gì đã có trên đời. Công nghệ càng cũ và càng phổ biến thì nó càng thấy nhiều ví dụ, và code nó viết ra càng chạy được. Công nghệ mới thì nó thấy rất ít — nhưng **nó không im lặng khi không biết**. Nó vẫn viết code trông rất tự tin, gọi những hàm không hề tồn tại. Và bạn chỉ phát hiện lúc chạy."

> "Rồi mười một giờ đêm app vỡ, bạn google lỗi đó. Với thứ boring: bốn mươi câu trả lời. Với thứ mới: một cái issue trên GitHub, chưa ai trả lời."

**Câu chốt — dùng hình ảnh này, khán giả nhớ lâu hơn:**

> "Mỗi dự án chỉ có khoảng **một 'token đổi mới'**. Tiêu nó vào đúng cái khiến sản phẩm của bạn khác biệt. Ở đây là cách AI đọc link portfolio rồi gắn thẻ năng lực — đó là phần độc đáo. Còn database, đăng nhập, framework thì chọn thứ chán nhất có thể."

> "Tiêu token đổi mới vào database thì bạn vừa mất thời gian, vừa chẳng ai chấm điểm cho việc đó."

**Slide 18 — bản kế hoạch thật.**

Đi theo ba khối, đừng đọc hết một lượt.

> "Đây là thứ chạy ra từ prompt vừa nãy, trong một lần chạy thật. Cả bản kế hoạch nằm gọn một màn hình."

**Khối đầu — hai dòng xám trên cùng.**

> "Để ý ngay dòng đầu: *'PRD ở chặng 2 — không nhắc lại ở đây.'* Tài liệu này **không** kể lại sản phẩm là gì. Nó chỉ trả lời: dựng bằng gì, và có vừa không."

**PART A — HOW.**

> "Ba màn hình, mỗi màn một việc. Đọc lại ba dòng đó xem — **không dòng nào có chữ 'và'**. Màn hình nào mà mô tả phải dùng chữ 'và' là màn hình làm hai việc, phải tách hoặc cắt."

Chỉ dòng AI trong khối Stack:

> "`@google/genai` — thư viện nào. `Gemini 2.5 Flash` — model nào, và Flash vì nó nhanh và rẻ, không phải vì mạnh nhất. `key in process.env` — **chìa khoá nằm ở biến môi trường trên server, không nằm trong code chạy ở trình duyệt.**"

> "Dòng cuối đó là dòng về bảo mật. Nếu key nằm trong code frontend thì ai mở DevTools cũng lấy được, và hoá đơn là của bạn. Hỏi ngay từ chặng lập kế hoạch thì nó miễn phí. Phát hiện sau khi build xong thì phải sửa lại kiến trúc."

**PART B — TASKS. Đây là khối mới, và là khối đáng giá nhất slide.**

> "Năm task. Mỗi dòng: làm ra gì, mấy giờ, phụ thuộc cái nào, và tiêu chí xong."

> "Cột phụ thuộc cho bạn thứ tự bắt buộc. T3 phụ thuộc T1 — nghĩa là đừng đụng vào phần gọi Gemini trước khi màn hình Gate chạy được. Không có cột này, người ta hay làm phần vui trước, rồi kẹt."

Chỉ dòng tổng:

> "**Mười tám giờ trên ngân sách hai mươi.** Đây là lúc bản kế hoạch tự kiểm tra chính nó. Nếu ra hai mươi tám giờ, nó phải quay lại cắt — chứ không được đưa cho bạn một kế hoạch không khả thi rồi để bạn tự phát hiện vào tối thứ Bảy."

Chỉ dòng cuối cùng:

> "Và nó ghi rõ **đã cắt gì để vừa**: tính năng 'follow a peer', ba giờ, vì mạng lưới vẫn chạy được mà không cần nó. Đó là câu bạn viết lại trong bài nộp."

**Câu chốt slide:**

> "Bản kế hoạch này mất bảy phút. Nó tiết kiệm cho bạn cái cảnh ngồi giữa chặng code rồi tự hỏi 'ủa mình lưu cái này ở đâu nhỉ' — và trả lời bằng một câu khác với câu hôm qua."

---

## 00:47–00:54 — THỰC HÀNH 3 (slide 19, 7 phút)

> "Bảy phút. Dán quyết định từ chặng 2 vào prompt Plan, chạy."

> "Xong khi bạn có bốn thứ: tính năng đã cắt, số màn hình, **stack**, và mô hình dữ liệu."

**Làm:** đi vòng và hỏi đúng một câu:

> "Danh sách 'in' của bạn mấy dòng? Quá năm là chưa cắt đủ — bảo nó cắt lại."

*(Đây là khối thực hành khán giả hay làm qua loa nhất, vì nó không sinh ra thứ gì nhìn được. Nhưng nó là chặng duy nhất chốt stack — thiếu nó thì prompt build ở khối sau trống một mảng.)*

---

## 00:54–01:02 — Design system (slide 20–23)

**Slide 15 (divider).**

> "Chặng này là khác biệt lớn nhất giữa một MVP trông *có thiết kế* và một MVP trông *do máy đẻ ra*."

**Slide 21 — vì sao token trước.**

> "'Làm cho đẹp đi' là câu không có trí nhớ. Màn hình một xanh thế này, màn hình bốn xanh thế khác, và đến lúc đó sửa là sửa tay từng chỗ."

> "Làm token trước thì tính nhất quán là *cấu trúc*, không phải thứ bạn phải đi canh."

**Slide 22 — prompt design system.**

Bấm nút **COPY FULL** rồi nói:

> "Bản đầy đủ trong nút này có thêm một khối mà slide không đủ chỗ hiện: **phong cách tham chiếu**. Thay vì viết 'làm cho đẹp', tôi mô tả *nguyên tắc* của một hệ design mà tôi thích — nền tối nhiều tầng, một màu nhấn duy nhất chỉ dùng cho hành động, nút bo tròn hết, chữ chỉ hai độ đậm."

> "Mấy dòng đó lấy từ hệ design công khai của Spotify. Nhưng để ý dòng này: **'follow these principles, do not copy any brand'**. Học cách người ta *tổ chức* hệ design thì tốt. Bê nguyên màu và logo của người ta vào bài dự thi thì hỏng — originality chiếm 30% điểm, và bắt chước thương hiệu có thật là một vấn đề khác nữa."

> "Chỗ tìm mấy tài liệu này: gõ 'awesome-design-md' trên GitHub. Có sẵn hệ design của nhiều sản phẩm lớn, viết ở dạng để dán vào prompt."

Chỉ dòng WCAG:

> "Dòng này bắt nó tự kiểm tra độ tương phản. Accessibility gần như luôn nằm trong tiêu chí chấm điểm, và gần như không ai làm. Một dòng prompt, ăn điểm thật."

**Slide 23 — prompt màn hình.** Chỉ hai chỗ:

> "'CHỈ dùng token ở trên' — đó là ràng buộc làm việc. Và dòng cuối: bắt nó khai ra chỗ nào bộ token không đủ, thay vì tự bịa thêm màu. Đó là cách bạn phát hiện thiết kế đang trôi."

Chỉ callout xanh:

> "Empty state và error state — hỏi thẳng tên ra. Đó là chỗ UI do AI sinh ra vỡ đầu tiên, và cũng là chỗ người dùng thật rơi vào trước tiên."

---

## 01:02–01:11 — THỰC HÀNH 4 (slide 24, 9 phút)

> "Chín phút. Chạy prompt design system. **Giữ lại bộ CSS variables** — lát nữa dán thẳng vào prompt build, đừng để lạc."

---

## 01:11–01:18 — Code (slide 25–28)

**Slide 25 — xây theo lớp.**

> "Đừng xin tất cả trong một prompt. Xin từng lớp, test sau mỗi lớp. Vì khi bạn xin mười thứ cùng lúc và nó vỡ, bạn không biết chỉ thị nào gây ra."

**Slide 26 — prompt build.**

> "Nhìn xem prompt này ngắn thế nào. Nó ngắn được vì nó *thừa hưởng*: token từ chặng 3, mô tả màn hình từ chặng 3, quyết định từ chặng 2."

Chỉ dòng scope:

> "Và dòng này giữ mạng cho bạn: **không routing, không đăng nhập, không database**. Bỏ dòng này ra, model sẽ dựng cho bạn một cái dashboard có sidebar và bạn hết giờ."

**Slide 27 — ví dụ điền thật, từ một lần chạy có thật.**

> "Đây là prompt build đó, điền bằng kết quả thật của chặng 1 đến 4."

Chỉ dòng **Stack (from the plan)**:

> "Để ý dòng này — nó không phải tôi tự nghĩ ra. Nó copy thẳng từ khối STACK trong bản kế hoạch ở chặng 3. Nếu bản kế hoạch ghi CSS custom properties thì ở đây là CSS custom properties, không phải Tailwind."

Chỉ dòng xám ngay dưới — đây là chỗ hay bị hỏi:

> "Và dòng này trả lời một câu chắc chắn có người thắc mắc: bản kế hoạch ghi Firebase và Gemini, sao ở đây lại 'no login, no database'?"

> "Vì đây mới là **lớp một**. Bản kế hoạch mô tả sản phẩm hoàn chỉnh; prompt build đầu tiên chỉ dựng phần giao diện và trạng thái cục bộ. Firebase và lời gọi Gemini vào ở lớp sau, khi màn hình này đã chạy đúng."

> "Xin cả bốn thứ trong một lượt thì nó vỡ, và bạn không biết chỉ thị nào gây ra."

Chỉ vào tên sản phẩm:

> "Để ý: sản phẩm không còn tên 'Ươm Mầm cho 6–22 tuổi' nữa. Sau chặng Research nó thành **The Proof-of-Work Protocol**, chỉ cho sinh viên 18–22. Vì Gemini chỉ ra Nghị định 13/2023 bắt buộc xác thực tuổi và xin phép cha mẹ cho trẻ dưới 16 — một người làm solo trong 25 giờ không thể làm nổi."

> "Đó **không phải đi lạc. Đó là pipeline đang làm việc.** Thà đổi hướng ở chặng 1 khi chưa viết dòng code nào, còn hơn phát hiện ra sau khi đã build xong."

Chỉ nút COPY FULL:

> "Trên màn hình tôi chỉ để phần rút gọn cho dễ đọc. Bấm nút này là copy đủ cả bộ token — đừng ngồi chép tay từ máy chiếu."

**Slide 28 — hai màn hình còn lại.**

> "Bản kế hoạch nói ba màn hình. Vừa rồi mới dựng một. Đây là hai cái còn lại — và điều đáng chú ý không phải nội dung, mà là **prompt gần như không đổi**."

Chỉ hai dòng xám trên cùng:

> "Stack, bộ token, scope, accessibility — **giống hệt màn 1, từng chữ**. Chỉ bốn dòng đổi: việc của màn, hành động chính, empty state, error state."

> "Đó là toàn bộ điểm của bốn chặng đầu. Đến màn thứ ba, bạn không còn *viết* prompt nữa — bạn **điền vào một cái form đã có sẵn**."

Chỉ dòng cuối trong khung:

> "Và vẫn là luật cũ: **làm từng màn một**, test xong mới sang màn kế. Xin cả hai trong một tin nhắn thì nó vỡ, và bạn không biết chỗ nào hỏng."

*(Nếu ai hỏi 'em có phải build cả ba màn không?' — không. Một màn chạy được đã đủ nộp bài. Hai màn còn lại là để về nhà.)*

---

## 01:18–01:31 — THỰC HÀNH 5 (slide 29, 13 phút)

> "Mười ba phút — khối dài nhất. Mở ai.dev, vào Build, dán prompt build kèm bộ token của bạn."

> "Xong khi app chạy được **trên điện thoại của bạn** — không phải trên laptop. Ai xong sớm thì bấm Publish luôn, tôi sẽ nói về nó ngay sau đây."

**Làm:** facilitator tỏa ra. Còn 3 phút thì báo. Ai kẹt hoàn toàn → đưa link app Ươm Mầm dựng sẵn để họ đi tiếp từ bước sau.

---

## 01:31–01:36 — Test (slide 30–31)

**Slide 30 — test để sống sót, không phải để đủ coverage.**

> "Đổi lại cách nghĩ về test. App của bạn không cần 80% coverage. Nó cần sống sót bốn phút trước mặt **một người không phải bạn** — người không biết chỗ nào nên tránh bấm."

Chỉ ba thẻ, trái sang phải:

> "Test kỹ đúng con đường bạn sẽ demo — trên wifi hội trường, trên điện thoại, không phải trên laptop ở nhà. Test qua loa vài biên hiển nhiên: bỏ trống, nhập rất dài, sai ngôn ngữ, bấm hai lần. Còn lại thì bỏ — đống code này tuần sau bạn viết lại hết, viết unit test cho nó là phí giờ."

Câu chốt của slide:

> "Người dựng app luôn bấm đúng chỗ mình đã quen. Người lạ thì không. Toàn bộ việc test ở giai đoạn này là đi tìm những chỗ mà chỉ người lạ mới bấm vào."

**Slide 31 — prompt test.**

Chỉ vào dòng "no code needed" trước tiên — đây là chỗ nhiều người vướng:

> "Để ý: **không cần dán code.** Code của bạn nằm trong AI Studio, lôi sang Gemini vừa mất công vừa không giúp gì. Mô tả ba dòng là đủ: app làm gì, người dùng nhập gì, họ nhận lại gì."

> "Và Gemini **đọc được ảnh**. Chụp màn hình cái app đang chạy rồi kéo vào khung chat — nó nhìn được layout, nút nằm đâu, chữ có bị tràn không. Nhanh hơn và chính xác hơn dán code rất nhiều."

*(Nếu có người hỏi 'em chạy luôn trong AI Studio được không?' — được, vì ở đó model đã thấy code. Nhưng nhớ ghi rõ 'chỉ nhận xét, đừng sửa code', không thì Build mode sẽ tự động sửa app của họ giữa lúc chỉ định hỏi.)*

Chỉ vào dòng "sắp theo khả năng xảy ra ngay lúc demo":

> "Dòng này là thứ biến danh sách thành cái dùng được. Không phải sắp theo mức nghiêm trọng lý thuyết — sắp theo **cái sắp cắn bạn**. Một lỗi làm sập cả app nhưng cần 20 bước mới chạm tới thì không nguy hiểm bằng một lỗi xuất hiện ngay ở thao tác thứ hai của phần demo."

Chỉ danh sách bắt buộc phải cover:

> "Tám tình huống này em ghi cứng vào prompt vì đây là những thứ luôn xảy ra và luôn bị quên. Đặc biệt hai cái cuối: **bàn phím điện thoại che mất nút bấm**, và **model trả về thứ không mong đợi**. Cái sau là đặc thù của app AI — code của bạn đúng, nhưng model trả về một thứ mà giao diện không biết hiển thị thế nào."

Chỉ dòng cuối:

> "Và checklist 6 mục — đó là thứ bạn chạy trong ba phút ngay trước khi lên sân khấu, không phải đọc lại toàn bộ danh sách 12 lỗi."

**Cảnh báo quan trọng khi khán giả chạy prompt này:**

> "Chạy xong đừng sửa cả mười hai lỗi. **Sửa hai cái đầu thôi.** Còn lại ghi vào ghi chú. Hôm nay không đủ giờ, và hai cái đầu là hai cái sẽ thật sự xảy ra."

---

## 01:36–01:41 — Đánh giá (slide 32–33)

**Slide 32 — chấm theo thang điểm thật.**

> "'App em ổn chưa ạ?' là câu không ai trả lời được — kể cả AI. Đổi thành: 'nó có ăn điểm theo đúng tiêu chí sẽ bị chấm không?' Câu đó trả lời được, và quan trọng hơn, **sửa được**."

Chỉ ô 40%:

> "Để ý ô lớn nhất là feasibility — chạy được, dễ dùng, có nghĩ tới người khuyết tật. Nó vừa lớn nhất **vừa dễ ăn nhất**, vì nó nằm hoàn toàn trong tay bạn. Không phụ thuộc ý tưởng của bạn hay ho tới đâu."

> "Và đây là chỗ nhiều người tính sai: một app nhỏ mà mọi nút đều chạy **thắng** một app tham vọng mà vỡ giữa lúc demo. Giám khảo chấm cái họ thấy chạy, không chấm cái bạn định làm."

Chỉ callout:

> "Lấy thang điểm thật **trước khi build**, không phải sau. Nó cho bạn biết công sức bỏ vào đâu thì ra điểm — và quan trọng không kém, chỗ nào bỏ công vào cũng không ra điểm."

**Slide 33 — prompt đánh giá.**

Chỉ cụm "specific in the product":

> "Bắt nó chứng minh bằng thứ **cụ thể trong sản phẩm**. Không có dòng này thì nó khen chung chung — 'giao diện trực quan, ý tưởng tiềm năng' — và lời khen chung chung thì không sửa được gì cả."

Chỉ dòng gần cuối:

> "Dòng này biến một bản báo cáo thành một danh sách việc: nếu tôi chỉ còn N giờ, làm gì trước, **và chủ động không làm gì**. Vế thứ hai quan trọng ngang vế thứ nhất — nó cho bạn phép được bỏ."

Chỉ dòng cuối cùng:

> "Và câu 'hãy khắt khe'. Mặc định model rất tử tế với bạn. Một điểm 9 mà bạn không bảo vệ được trước giám khảo thì tệ hơn điểm 6 mà tối nay bạn sửa được."

---

## 01:41–01:47 — Publish (slide 34)

> "Bây giờ lấy link thật. Miễn phí, không cần thẻ."

**Nói TRƯỚC khi họ bấm** — quan trọng:

> "Một điều nói trước để lát nữa không ai hoảng: Starter Tier chỉ áp dụng cho tài khoản Google **chưa từng publish** từ AI Studio. Nếu nó đòi thẻ tín dụng, không phải bạn làm sai — chỉ cần mở cửa sổ ẩn danh hoặc dùng tài khoản khác."

*(Nói trước thì đây là một bước có dự kiến. Nói sau thì nó là sự cố.)*

**Làm:** bấm Publish trên màn hình, mở link trên điện thoại, giơ lên. Rồi:

> "Bốn phút, mọi người làm y hệt. Có link rồi thì gửi vào nhóm chat."

---

## 01:47–01:53 — Nộp bài & video demo (slide 35–36)

**Slide 35 — hai cái link, và người ta nộp nhầm.**

> "Chỗ này mất điểm oan nhiều nhất trong cả cuộc thi, và nó **không liên quan gì tới kỹ thuật**."

Chỉ hai dòng đầu bảng:

> "**Link project** là để giám khảo mở đúng dự án của bạn, xem được cả code lẫn prompt. Thường đây là cái bắt buộc. Nhớ đặt sharing thành Public trước — quên bước đó thì giám khảo bấm vào chỉ thấy 'bạn không có quyền truy cập'."

> "**Link app đã publish** là để người ta dùng thử mà không thấy code. Thường là điểm cộng, không bắt buộc."

> "Hai cái này là hai thứ khác nhau. Nộp nhầm cái này vào ô cần cái kia là cách mất điểm dễ nhất, và cũng là cách ức chế nhất — vì sản phẩm của bạn không hề có lỗi."

Chỉ dòng cuối bảng:

> "Và dòng cuối: **phạm vi đã viết ra**. Bạn làm gì, và chủ động không làm gì. Đây chính là dòng KHÔNG LÀM mà bạn viết ở chặng 2. Nó đi được tới tận đây."

> "Đừng ngại viết ra những gì mình đã cắt. Một người viết 'tôi cố tình không làm phần thanh toán vì đối tượng là học sinh dưới 16 tuổi, và luật không cho' — người đó nghe như một người hiểu việc. Người viết một danh sách tính năng dài dằng dặc mà nửa số đó không chạy thì ngược lại."

**Slide 36 — video 90 giây.**

> "Đây là artifact duy nhất được xem hết từ đầu đến cuối. Bài viết thì người ta lướt, code thì người ta mở ra rồi đóng lại — video thì xem hết."

Chỉ ô thứ hai (0:15–0:40):

> "Đa số video demo mất bốn mươi giây đầu cho màn đăng nhập và giới thiệu bản thân, rồi mới tới phần hay. Đừng. **Khoảnh khắc hay ho phải xuất hiện trước giây 40.** Nếu người xem chưa thấy điều gì đáng ngạc nhiên ở giây 40, họ đã ngừng xem rồi."

Chỉ thẻ đỏ:

> "Và tuyệt đối không đưa vào: màn đăng nhập, sơ đồ kiến trúc, cấu trúc thư mục, và câu 'xin lỗi chỗ này còn bug'. Không ai bắt bạn xin lỗi cả — bạn đang khoe thứ mình làm được, không phải giải trình thứ mình chưa làm."

Thêm một câu trấn an:

> "Quay bằng điện thoại cũng được. Không cần micro xịn, không cần dựng. Nội dung quan trọng hơn chất lượng hình rất nhiều. Cái người ta nhớ là vấn đề bạn giải quyết, không phải độ nét."

---

## 01:53–01:57 — Tổng kết (slide 37–38)

**Slide 37 — ngân sách giờ.**

> "Nếu bạn có một cuối tuần, đây là chỗ giờ thực sự đi. Để ý ba chặng đầu: một phần tư thời gian, không có dòng code nào."

**Slide 38 — bỏ chặng.**

> "Và đây là phần thật lòng. Bỏ chặng không tiết kiệm được thời gian — nó quay lại dưới dạng làm lại, vào lúc tệ hơn, khi bạn còn ít thời gian hơn."

---

## 01:57–01:59 — Đóng (slide 39)

> "Buổi sau chúng ta lấy chính app này, tìm chỗ nó vỡ, chấm điểm nó theo thang thật, rồi nộp — nộp ngay trong phòng, không phải 'về nhà rồi nộp'."

> "Từ giờ đến đó: chạy prompt research trên một ý tưởng thứ hai. Bạn sẽ thấy chặng một tự nhiên hẳn ở lần thứ hai."

---

## Nếu bị trễ giờ

Cắt theo đúng thứ tự này:

1. Slide 30–33 (lướt test/đánh giá) — bỏ hẳn, để buổi sau
2. Slide 38 (bỏ chặng) — gộp một câu vào slide 31
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
