# Kịch bản thuyết trình — Sprout (tiếng Việt)

Dùng cho `docs/slides/sprout-student-team-funding-pipeline-slides.html` — 32 slide, khoảng **55 phút** nếu nói hết.

**Quy ước trong file này**
- `[HÀNH ĐỘNG]` = việc cần làm (bấm phím, đổi tab, copy prompt), không đọc lên.
- Chữ **in đậm** = câu chốt, nên nói chậm lại.
- Bấm `N` trong deck để bật ghi chú thuyết trình; bấm `C` để copy prompt của slide đang mở.

**Phân bổ thời gian**

| Phần | Slide | Thời lượng |
|---|---|---|
| Mở đầu + vấn đề + phạm vi | 1–8 | 13 phút |
| Stage 1 — Ý tưởng | 9–11 | 4 phút |
| Stage 2 — Bản thiết kế | 12–15 | 7 phút |
| Stage 3 — Build 4 lớp | 16–26 | 24 phút |
| Stage 4 — Kiểm thử | 27–29 | 4 phút |
| Stage 5 — Deploy + kết | 30–32 | 3 phút |
| | | **55 phút** |

**Nếu chỉ có 40 phút:** rút gọn slide 22, 23, 24 xuống mỗi slide 1 phút (chỉ đọc tiêu đề khối, không giải thích từng mục) và bỏ slide 26. Vẫn giữ nguyên slide 4, 5, **19**, 20, 25 — đó là năm slide có nội dung mà người khác không nói được.

**Nếu chỉ có 20 phút:** chạy slide 1 → 2 → 3 → 4 → 5 → 6 → 17 → **19** → 20 → 25 → 31 → 32. Bỏ toàn bộ prompt; nói rằng prompt nằm trong deck và bấm `C` là copy được.

> **Slide 19 là slide mới, và nếu phải chọn một slide để giữ trong phần build thì chọn nó.** Đó là chỗ duy nhất bạn thừa nhận một sai lầm cụ thể và cho thấy cách sửa — thứ mà không ai copy lại được từ deck của bạn.

---

## Slide 1 — Cover: "Sprout" · 45 giây

Chào mọi người. Hôm nay mình sẽ đi qua toàn bộ quy trình xây một sản phẩm thật bằng Google AI Studio, từ ý tưởng cho tới cái link chạy được.

Sản phẩm tên là **Sprout**: một nền tảng để sinh viên trong trường tìm được đồng đội cho dự án của mình, và gọi được một khoản vốn nhỏ để làm.

Có một điều mình muốn nói trước. Trong bài này sẽ có **hai lần mình nói "không"** — hai tính năng nghe rất hay nhưng mình chủ động cắt bỏ. Hai quyết định đó nằm ở slide 4 và slide 5, tức là rất sớm. Và theo mình, đó mới là phần đáng giá nhất của buổi hôm nay, chứ không phải mấy cái prompt.

---

## Slide 2 — Vấn đề · 2 phút

Mình bắt đầu từ vấn đề, chưa nói tới app vội.

Trường nào cũng có ba câu chuyện này.

Thứ nhất, **bạn sinh viên**: một bạn năm hai, có thời gian, có kỹ năng, tự làm một mình. Bạn đó không hề biết rằng ở tầng trên có ba người đang cần đúng cái kỹ năng của bạn.

Thứ hai, **ý tưởng**: một dự án chết ở tuần thứ ba. Không phải vì thiếu tham vọng — mà vì không tìm nổi một người biết vẽ.

Thứ ba, **tiền**: một sản phẩm mẫu không bao giờ được làm, vì cần bốn triệu đồng, và giữa "ý tưởng hay trong trường" với "một khoản tiền nhỏ" thật ra không có đường đi nào cả.

**Cả ba đều là bài toán ghép nối.** Kỹ năng với dự án, dự án với người, dự án với một khoản tiền nhỏ. Không cái nào cần một ý tưởng mới — chúng chỉ cần một chỗ để ba bên nhìn thấy nhau.

Và chỉ số mình cam kết là: **mỗi tháng có bao nhiêu đội được lập, và bao nhiêu phần trăm trong số đó ra được sản phẩm.** Không phải số lượt đăng ký. Sản phẩm dạng này rất dễ tự lừa mình bằng con số đăng ký.

---

## Slide 3 — Vòng lặp sản phẩm · 1 phút 30

Toàn bộ sản phẩm gói trong năm bước.

Đăng dự án. Người khác lướt thấy. Ứng tuyển vào **một vai trò cụ thể**. Chủ dự án bấm nhận. Rồi mở gọi vốn.

[HÀNH ĐỘNG] Chỉ tay vào bước 4.

**Bước 4 mới là sản phẩm.** Ba bước đầu chỉ là một cái bảng tin, mà trường nào cũng có rồi — Facebook group, Zalo, bảng thông báo ngoài hành lang. Khoảnh khắc thật sự có giá trị là lúc **một người lạ trở thành đồng đội**. Nên bước đó được dành hẳn một lớp build riêng, và một chỗ riêng trong phần demo.

Còn gọi vốn mình để cuối cùng, có lý do: một đội không có tiền vẫn làm ra được sản phẩm, nhưng tiền mà không có đội thì không.

---

## Slide 4 — Cắt tiền thật · 2 phút 30

Đây là slide quan trọng nhất của cả buổi. Mình nói sớm và nói thẳng.

**MVP này không đụng tới tiền thật.** Không phải vì code khó.

Muốn nhận thanh toán, bạn cần: pháp nhân đăng ký, tài khoản merchant, quy trình KYC và phòng chống rửa tiền, chính sách hoàn tiền, xử lý thuế. Và huy động vốn từ cộng đồng là hoạt động **có điều kiện về pháp lý**. Một dự án sinh viên mà giữ tiền của người khác thì đó là rủi ro pháp lý, không phải tính năng — và không có model AI nào cảnh báo bạn trước khi nó sinh ra một trang thanh toán đâu. Nó sẽ làm rất nhiệt tình.

Vậy mình làm gì thay thế? **Pledge — một lời cam kết được ghi nhận.**

Người ủng hộ cam kết một số tiền kèm lời nhắn. Thanh tiến độ chạy lên, tên họ vào danh sách, chủ dự án nhận được thông tin. Việc chuyển tiền thật diễn ra **ngoài nền tảng, giữa hai con người**. Và mọi chữ trên màn hình đều là "đã cam kết", không bao giờ là "đã thanh toán".

[HÀNH ĐỘNG] Dừng một nhịp.

**Phần demo thì y hệt nhau.** Vẫn là mục tiêu, thanh chạy lên, danh sách người ủng hộ. Ban giám khảo nhìn không thấy khác. Mà khoảng cách giữa "đã cam kết" và "thực nhận" lại thành chỉ số trung thực nhất của mình — cái đó trả lời giám khảo tốt hơn nhiều so với một cái Stripe key giả.

---

## Slide 5 — Cái chợ trống · 2 phút

Đây là cách thứ hai mà loại sản phẩm này chết, và gần như không ai chuẩn bị trước.

Kịch bản quen thuộc: bạn mở app trước mặt giám khảo. Không có dự án nào, vì không có người dùng nào, vì không có dự án nào. Giám khảo được xem một cái màn hình trống và một trang đăng nhập rất đẹp.

**Đây là cách phổ biến nhất khiến một demo marketplace chết, và nó không liên quan gì tới chất lượng code.**

Cách xử lý: **mười hai dự án thật, viết tay**, nằm sẵn trong file seed ngay từ Layer 1. Đặt tên theo những thứ một trường đại học Việt Nam thật sự sẽ làm. Mức gọi vốn phải khác nhau — vài cái 0%, một cái đã đủ, vài cái không gọi vốn.

Còn khi ra mắt thật thì bắt đầu từ **một khoa**, đừng bắt đầu từ cả trường.

**"Project Alpha" với "Lorem ipsum" là mất điểm ngay.** Nội dung mồi là công việc thiết kế, không phải đồ lấp chỗ trống — mình để hẳn sáu tiếng cho nó và viết tử tế.

---

## Slide 6 — Bảy màn hình · 1 phút 30

Toàn bộ bề mặt sản phẩm: bảy màn hình. Màn nào không có trong bảng này thì không nằm trong MVP.

[HÀNH ĐỘNG] Chỉ vào hai dòng in đậm ở cột "Demo".

Hai chỗ mình sẽ demo là **màn chi tiết dự án** và **màn hộp thư ứng tuyển**. Cái thứ hai chính là khoảnh khắc người lạ thành đồng đội.

Và đây là danh sách những thứ **không** làm: không chat, không trung tâm thông báo, không trang admin, không search index, không tổ chức hay câu lạc bộ. Mỗi cái đó là một tuần làm việc, và không cái nào là lý do khiến một bạn sinh viên quay lại lần thứ hai.

---

## Slide 7 — Quy trình 5 bước · 1 phút 30

Quy trình năm bước, hai công cụ.

Bước 1, 2 và 4 là **suy nghĩ** — làm trong Gemini chat. Bước 3 và 5 là **xây** — làm trong AI Studio.

Lý do tách ra: Gemini chat sẵn sàng cãi nhau với bạn và viết lại spec mười lần miễn phí. AI Studio thì giữ được một project đang chạy và có preview trực tiếp. Hỏi mỗi bên đúng cái nó giỏi.

Backend là **Firebase Auth và Firestore**, không thêm gì khác. Đăng nhập bằng Google nghĩa là không lưu mật khẩu, không có luồng quên mật khẩu, và không có vụ lộ mật khẩu nào để phải đi giải thích. **Đó là một quyết định bảo mật, được ngụy trang thành quyết định tiện lợi.**

---

## Slide 8 — Chuỗi sản phẩm trung gian · 1 phút 30

Bảng này là hợp đồng giữa các bước. Bước nào chưa ra được sản phẩm trung gian của nó thì đừng đi tiếp.

[HÀNH ĐỘNG] Chỉ vào dòng Stage 02.

Dòng hay bị bỏ qua nhất là **security rules**. Viết nó ở bước 2, không phải sau khi demo xong.

Lý do rất thực tế: Firestore mặc định là khoá. Trong lúc build, model gặp lỗi permission, nó sẽ rất vui vẻ đề nghị bạn mở toang database ra. Và lúc hai giờ sáng thì lời đề nghị đó **nghe rất hợp lý**. Rules viết sau cùng là rules viết sai.

---

## Slide 9 — Divider Stage 01 · 20 giây

Bước một. Một prompt duy nhất, và nó phải kết thúc bằng một bản ghi quyết định có chứa cả hai lần cắt.

---

## Slide 10 — Prompt Stage 1 · 2 phút

[HÀNH ĐỘNG] Bấm `C` để copy, dán vào Gemini chat, rồi nói tiếp trong lúc nó chạy.

Đây là prompt bước một, dán thẳng vào Gemini chat.

Chú ý phần đầu: mình nói rõ **hai quyết định đã chốt rồi, đừng mở lại**. Nếu không viết câu này, model sẽ đề xuất tích hợp cổng thanh toán cho bạn, chắc chắn luôn.

[HÀNH ĐỘNG] Chỉ vào mục 5.

Mục 5 là mục mình thích nhất: **"Hãy cãi lại tôi."** Mình yêu cầu model chỉ ra tính năng nào tốn một tuần mà mang lại ít giá trị nhất, và bảo mình cắt nó đi.

**Đây là buổi red team rẻ nhất bạn từng chạy.** Bạn đang trả tiền cho một model để nó phản biện phạm vi dự án của bạn, trước khi bạn đổ tám mươi giờ vào đó.

Mục 3 cũng đáng nói — "cold start". Mình ép model không được trả lời bằng chữ "marketing". Phải chỉ ra **cụ thể một con người trong trường** có thể tạo ra hai mươi dự án trong một tuần.

---

## Slide 11 — Kết quả Stage 1 · 1 phút 30

Đây là thứ bạn cầm trên tay sau bước một.

Năm dòng quyết định. **Nếu bản PRD của bạn không có chữ "pledge, không phải payment" thì chạy lại prompt** — nghĩa là nó chưa cam kết gì cả.

[HÀNH ĐỘNG] Chỉ sang thẻ bên phải.

Còn đây là tám vai trò mà một dự án sinh viên thật sự cần. Để ý cách viết: "Làm ra sản phẩm", "Thiết kế", "Viết nội dung", "Nói chuyện với người dùng".

**Lý do dùng chữ đời thường:** "Backend Engineer" loại luôn bạn năm hai — bạn đó nhìn vào và nghĩ mình chưa đủ trình. "Làm ra sản phẩm" thì không loại ai cả. Một dòng chữ thôi, nhưng nó quyết định ai dám bấm nút ứng tuyển.

---

## Slide 12 — Divider Stage 02 · 20 giây

Bước hai. Ở đây có ba sản phẩm trung gian, và cái security rules là cái làm cho chữ "production" trở thành một từ trung thực.

---

## Slide 13 — Prompt Stage 2 · 3 phút

[HÀNH ĐỘNG] Bấm `C`, dán vào Gemini chat, đừng chờ — nói tiếp luôn.

Prompt bước hai. Bốn phần: collections, security rules, luồng ghép đội, và DESIGN.md.

[HÀNH ĐỘNG] Chỉ vào mục 3.

Mục 3 mình bắt model **gọi tên ra một race condition**: hai người cùng được nhận vào một vai trò chỉ cần một người, đúng cùng một lúc, từ hai cái tab. Nếu không hỏi trước, bug này sẽ xuất hiện đúng lúc bạn demo trực tiếp.

[HÀNH ĐỘNG] Chỉ vào mục 4, đoạn cuối.

Nhưng đoạn quan trọng nhất là phần cuối mục 4: **"cách token được tiêu thụ"**.

Đây chính là thứ sửa được lời phàn nàn mà ai cũng có về giao diện do AI sinh ra. **Một bảng màu không phải là một design system.** Đưa cho model năm mã màu hex, nó sẽ rắc hai trăm mã hex vào khắp code. Còn nói với nó rằng token phải khai báo trong `:root`, phải đăng ký vào Tailwind theme, và **cấm mã hex thô trong component** — thì nó mới sinh ra một hệ thống.

Và cái danh sách "KHÔNG ĐƯỢC" cũng vậy. Không tím, không gradient xanh-tím, không glassmorphism, không đổ bóng mọi thẻ. **Một danh sách cấm cụ thể có sức nặng hơn mười tính từ khen ngợi.**

[HÀNH ĐỘNG] Chỉ vào mục cuối cùng: LAYOUT RULES, WITH NUMBERS.

Còn mục cuối cùng này thì mình **thêm vào sau**, sau khi build hỏng một lần. Slide 19 mình sẽ kể chuyện đó.

Ý chính: **màu và chữ có token để bám vào. Layout thì không có token nào cả.** Nên nếu bạn không đưa con số, model tự chọn, và nó chọn dở.

Và lý do luật layout phải nằm **trong DESIGN.md**, chứ không phải chỉ trong prompt Layer 1: vì Layer 2, 3, 4 đều mở đầu bằng câu "đọc lại DESIGN.md và tuân theo". Nếu luật chỉ nằm ở prompt Layer 1, thì màn hình Discover đẹp — còn màn inbox thêm ở Layer 3 sẽ hỏng đúng y như cũ. **Viết vào DESIGN.md một lần, bốn lớp đều được hưởng.**

---

## Slide 14 — Design system · 2 phút

Đây là hệ thiết kế mình chọn, và lý do.

Nền giấy ấm. Xanh lá đậm. Và **một màu hổ phách duy nhất**.

[HÀNH ĐỘNG] Chỉ vào dải màu.

Quy tắc quan trọng nhất, mình nói chậm: **xanh lá nghĩa là "hành động". Hổ phách nghĩa là "tiền".** Hổ phách không bao giờ xuất hiện để trang trí.

Kết quả là gì? **Một con số tiền được nhận ra trước cả khi được đọc.** Chỉ một ràng buộc đó thôi đã làm cho toàn bộ giao diện mạch lạc hơn bất kỳ nỗ lực căn lề nào.

[HÀNH ĐỘNG] Chỉ vào bảng contrast.

Và độ tương phản ở đây là **tính ra, không phải đoán**. Chữ trên nền giấy 16.8:1. Xanh trên trắng 6.4:1. Hổ phách trên trắng 5.0:1. Tất cả đều đạt chuẩn WCAG AA. Nếu bạn không tính, bạn sẽ không biết mình vừa làm ra một giao diện mà người cận thị không đọc được.

---

## Slide 15 — Mô hình dữ liệu · 1 phút 30

Năm collection.

[HÀNH ĐỘNG] Chỉ vào dòng comment trong `projects`.

Điểm đáng chú ý là bốn con số đếm được **denormalise** — gắn thẳng lên document dự án.

Lý do: màn Discover hiển thị mười hai thẻ. Nếu mỗi thẻ phải đọc thêm một subcollection để đếm số người ủng hộ, đó là mười hai lượt round trip. Bảng tin sẽ chậm thấy rõ — và đó đúng là **thứ đầu tiên giám khảo nhận ra**.

Nhưng đi kèm là một luật: **không client nào được phép ghi mấy con số đó.** Chúng chỉ được cập nhật trong transaction. Nếu không, chúng sẽ sai, và sai âm thầm.

Còn `pledges` thì bất biến — ghi một lần, không sửa được số tiền. Một lời cam kết không phải là bản nháp.

---

## Slide 16 — Divider Stage 03 · 20 giây

Bước ba. Bốn lớp. Và app này demo được **ngay từ cuối lớp một**.

---

## Slide 17 — Bản đồ 4 lớp · 2 phút

Bốn lớp, mỗi lớp được phép động vào cái gì, và cấm cái gì.

[HÀNH ĐỘNG] Chỉ vào dòng Layer 1.

Để ý: **Layer 1 không có backend gì cả.** Toàn bộ design system và hai màn hình công khai, đọc từ một file seed cứng.

Lý do làm vậy: bạn được nhìn và đánh giá giao diện **trước khi tồn tại một lỗi permission nào**. Hai vấn đề tách ra, xử lý riêng. Và Layer 1 tự nó đã demo được.

[HÀNH ĐỘNG] Chỉ vào dòng Layer 3.

**Cuối Layer 3 là một sản phẩm thật.** Nếu hết giờ, bạn mang đi thi một nền tảng ghép đội chạy được, và để phần gọi vốn vào roadmap. Cái đó **tốt hơn nhiều** so với một luồng gọi vốn gắn vào một tính năng đội nhóm bị hỏng.

---

## Slide 18 — Prompt Layer 1 · 2 phút 30

[HÀNH ĐỘNG] Bấm `C`, dán vào AI Studio, rồi **chuyển ngay sang tab đã build sẵn hôm qua**.

Đây là prompt Layer 1 — và đây đúng là prompt mình đã chạy thử trước khi đưa lên slide.

Cái đáng chỉ vào là khối **"THE LOOK — đây không phải dashboard"**.

Nửa trên là "nên cảm thấy như thế nào": một bảng tin trong trường, giấy ấm, chữ tự tin, nhiều khoảng trắng, đọc được từ cách một mét. Vì **một bạn sinh viên đang cân nhắc có nên giao ý tưởng của mình cho cái web này không**.

Nửa dưới mới là phần làm việc: danh sách **KHÔNG**. Không tím, không gradient xanh-tím, không kính mờ, không dark mode, không nút bo tròn hoàn toàn, không đổ bóng mọi thẻ, không emoji làm icon.

**Chính cái danh sách này ngăn bạn nhận về cái dashboard gradient tím mà mọi công cụ AI đều sinh ra theo mặc định.** Không phải vì model có gu xấu — mà vì nếu bạn không nói gì, nó sẽ chọn cái phổ biến nhất.

---

## Slide 19 — "Responsive" không phải là spec · 4 phút

Slide này có mặt ở đây vì **mình đã làm sai**, và mình nghĩ đây là bài học đáng giá nhất trong cả phần build.

[HÀNH ĐỘNG] Chỉ vào callout đỏ trên cùng.

Bản prompt Layer 1 đầu tiên của mình, nói về layout, **chỉ có đúng một câu**: "một lưới dự án responsive". Cộng thêm một dòng self-check: "layout hiển thị ổn ở 390 và 1440".

Model **đã làm đúng cả hai**. Nó không hề gian dối. Và màn hình trả về thì không dùng được.

[HÀNH ĐỘNG] Chỉ sang thẻ đỏ bên trái.

Cụ thể: một cái thẻ nằm chơ vơ trong một khung rộng bảy trăm pixel, phần còn lại của màn hình trống trơn. Bên trong thẻ có một khoảng trống một trăm năm mươi pixel giữa mô tả và thanh tiến độ. Mười sáu danh mục xổ thành một sidebar dọc kín cả cột trái, phải cuộn mới hết. Năm cái nút trên header cùng một độ đậm như nhau, trong đó có cả nút "Seed Data" — tức là công cụ dành cho lập trình viên, nằm chình ình trên thanh điều hướng chính.

[HÀNH ĐỘNG] Chỉ sang thẻ xanh bên phải.

Còn spec đúng thì phải là **những con số**: lưới 1 cột dưới 640, 2 cột từ 640, 3 cột từ 1024, và **trên 1440 vẫn là 3 — không bao giờ có cột thứ tư**. Thẻ đẩy khối gọi vốn xuống đáy bằng `margin-top:auto` và cắt tiêu đề với mô tả ở 2 dòng bằng `line-clamp-2`, để thẻ không thể rỗng ruột. Bộ lọc là một hàng chip ngang. Cột nội dung tối đa 1200 pixel.

[HÀNH ĐỘNG] Chỉ vào callout vàng dưới cùng. Nói chậm.

Và đây là quy luật rút ra: **token sửa được màu và chữ, vì token là một con số.** Còn layout thì **không có token** — nên nếu bạn không đưa con số, model sẽ tự chọn, và nó chọn dở.

Nói rộng ra: **mỗi tính từ trong prompt là một chỗ bạn nhường quyền quyết định cho model.** "Responsive", "đẹp", "hiện đại", "sạch sẽ" — bốn chỗ nhường. Đổi chúng thành số thì bạn lấy lại quyền.

Sửa xong thì có một câu hỏi tiếp theo, và mình nghĩ đây mới là câu hỏi hay: **sửa Layer 1 thì các layer sau có giữ được không?** Layer 3 thêm màn inbox — một màn hình mà lúc viết luật mình chưa hề mô tả.

Mình đã thử thật: đưa DESIGN.md kèm luật layout, cộng với **đúng nguyên văn prompt Layer 3** — cái prompt chỉ nói vỏn vẹn "đọc lại DESIGN.md và tuân theo", không nhắc lại một chữ nào về layout.

Kết quả: **luật lan được.** Màn inbox không có sidebar, không có lưới bốn cột, có `mt-auto`, có `line-clamp-2`, và model tự viết vào code một dòng: *"Ở 1440px, hộp thư hiển thị 8 đơn ứng tuyển trước khi phải cuộn."* Đó là luật được áp dụng cho màn hình mình chưa từng mô tả.

Nhưng nó cũng lộ ra hai chuyện. Thứ nhất, **có trôi**: luật ghi 1200px, model dùng `max-w-6xl` — tức 1152px. Đúng tinh thần, sai con số. Thứ hai, và cái này mới đáng lo: **Layer 2, 3, 4 lúc đó không có mục self-check nào về layout.** Lần này lan đúng, nhưng nếu lan sai thì **không có gì bắt được**. Nên mình đã thêm mục kiểm tra layout vào cả ba layer sau — và viết thẳng con số 1152 vào prompt, vì gọi tên đúng cái lỗi model vừa mắc thì hiệu quả hơn là dặn "phải chính xác 1200".

---

## Slide 20 — Kết quả đo được · 2 phút

Mình không đoán. Mình chạy prompt đó qua Gemini rồi đếm.

[HÀNH ĐỘNG] Chỉ lần lượt bốn ô số.

Số lần xuất hiện tím, chàm, gradient, kính mờ: **không**. Số token thiết kế được định nghĩa: **sáu mươi tư**. Số file: **hai mươi hai**, trong đó có `DESIGN.md` nằm ở thư mục gốc. Số lần import Firebase hay form submit: **không** — hàng rào phạm vi giữ nguyên.

[HÀNH ĐỘNG] Chỉ vào thẻ xanh bên trái.

Nội dung mồi nó viết ra cũng thật sự bản địa: một kho lưu trữ di sản Chăm, một app dịch ngôn ngữ ký hiệu tiếng Việt, một màn hình chữ nổi giá rẻ. Có định dạng tiền đồng chuẩn `vi-VN`. **Không có "Project Alpha" nào cả.**

Có một chi tiết mình thấy thú vị: **những chỗ duy nhất trong toàn bộ output có chữ "indigo" và "purple" là ở bên trong file `DESIGN.md` mà nó tự viết — để liệt kê chúng vào mục cấm.**

[HÀNH ĐỘNG] Chỉ sang thẻ vàng bên phải. Hạ giọng.

Nhưng phải nói cho sòng phẳng: **grep chứng minh được luật đã được tuân thủ. Nó không chứng minh được là đẹp.** Nó không nói cho bạn biết bảng tin có dễ nhìn lướt không, hay một bạn sinh viên có tin tưởng giao ý tưởng không. Cái đó phải mở lên và nhìn bằng mắt.

---

## Slide 21 — Nghiệm thu Layer 1 · 1 phút 45

Sáu mươi giây kiểm tra trước khi dán Layer 2.

Bên trái là nhận. Bên phải là trả lại và viết prompt sửa.

[HÀNH ĐỘNG] Chỉ vào callout đỏ dưới cùng. Nói chậm.

Và đây là câu quan trọng: **đừng chấp nhận "tạm được" ở phần giao diện.**

Layer 2, 3, 4 sẽ thêm màn hình mới **theo đúng phong cách mà Layer 1 đã đặt ra**. Sửa thẩm mỹ ở đây tốn một cái prompt. Sửa ở Layer 4 tốn nguyên một lần viết lại mọi màn hình.

Riêng về layout, có ba thứ kiểm trong ba mươi giây: **kéo cửa sổ hẹp lại** xem lưới có tụt từ ba xuống hai rồi xuống một cột không; **lọc còn đúng một dự án** xem cái thẻ có giãn ra chiếm cả hàng không — nó phải giữ nguyên bề rộng một cột; và **nhìn vào giữa thẻ** xem có lỗ trống nào không.

---

## Slide 22 — Prompt Layer 2 · 2 phút 15

Layer 2 là lúc app trở thành thật: đăng nhập Google, hồ sơ, tạo dự án, và dữ liệu seed chuyển vào Firestore.

[HÀNH ĐỘNG] Chỉ vào mục 2.

Chi tiết cần nhấn: **email liên hệ là trường riêng tư.** Chỉ chủ nhân của nó, và chủ dự án mà người đó đã ứng tuyển, mới đọc được. **Và phải chặn bằng security rules, không chỉ bằng cách không render ra UI.** Ẩn trên giao diện không phải là bảo mật — dữ liệu vẫn nằm đó, ai mở tab Network cũng thấy.

[HÀNH ĐỘNG] Chỉ vào mục 4.

Và luật của cả layer này: **deploy rules TRƯỚC lần ghi đầu tiên. Không bao giờ nới lỏng một rule để cho màn hình chạy được.**

Nếu một truy vấn lỗi, thường là truy vấn sai, không phải rule sai. Một database bị mở "tạm thời" trong lúc build là một database sẽ đi thẳng lên production trong tình trạng mở.

Và ở cuối prompt này có **mục self-check số 7 về layout** — mục mình thêm vào sau vụ hỏng ở slide 19. Layer 2 thêm hai màn mới là hồ sơ và tạo dự án, nên nó phải tự khai: cột nội dung có đúng 1200px không, có lưới bốn cột nào không, thẻ có rỗng ruột không.

---

## Slide 23 — Prompt Layer 3 · 2 phút 45

Đây là lớp quan trọng nhất. Mọi thứ trước nó chỉ là một trang đăng tin.

Ứng tuyển, hộp thư của chủ dự án, nhận hoặc từ chối, đội hình thành.

[HÀNH ĐỘNG] Chỉ vào mục 3.

Mục 3 là chỗ mình muốn mọi người chú ý: **race condition**.

Hai người cùng được nhận vào một vai trò chỉ cần một người, cùng lúc, từ hai tab hoặc hai máy. Nếu không xử lý, đội của bạn hỏng dữ liệu ngay trên sân khấu.

Cách xử lý: bọc thao tác nhận trong một **Firestore transaction** — đọc lại vai trò, kiểm tra xem còn trống không, và fail sạch sẽ nếu đã đầy. Cú bấm thứ hai phải hiện ra chữ **"vai trò này vừa được nhận rồi"**, chứ không phải làm hỏng đội.

[HÀNH ĐỘNG] Chỉ vào mục 2, câu cuối.

Còn một chi tiết nhỏ mà mình nghĩ là quan trọng: **lời từ chối không bao giờ được viết nặng nề.** Đây là bạn cùng lớp, thứ Hai tuần sau còn gặp nhau trong giảng đường. "Vai trò này đã có người" là đủ rồi. Đó là chi tiết mà phần mềm doanh nghiệp thường quên, còn sản phẩm cho sinh viên thì không được quên.

Và mục self-check số 7 ở cuối là dành riêng cho **màn inbox** — đây chính là màn hình mình đem đi test ở slide 19. Nó phải tự khai số đơn ứng tuyển nhìn thấy được ở 1440px trước khi phải cuộn.

---

## Slide 24 — Prompt Layer 4 · 2 phút 15

Layer 4: pledge và hoàn thiện.

[HÀNH ĐỘNG] Chỉ vào khối đầu tiên.

Ở đây **cách dùng từ quan trọng ngang với code**.

Không có ô nhập thẻ, không ví, không SDK thanh toán, không checkout, không nút "thanh toán ngay". Mọi chữ hiển thị cho người dùng là **"đã cam kết"**, không bao giờ là "đã thanh toán" hay "đã quyên góp". Và trang dự án **nói thẳng ra** rằng Sprout không xử lý thanh toán và không giữ tiền.

**Đây không phải là bắt bẻ câu chữ.** Đó là ranh giới giữa một nền tảng ghi nhận cam kết và một dịch vụ thanh toán không phép.

Còn về kỹ thuật: pledge **bất biến**. Rút lại thì đánh dấu là đã rút, chứ không xoá — để lịch sử còn trung thực. Và `pledgedTotal` với `backerCount` cập nhật trong **cùng một transaction** với pledge, không bao giờ từ client.

Cuối cùng, mục self-check số 7 của Layer 4 khác ba layer trước: nó bắt model **quét lại cả bốn lớp**, không chỉ lớp này, và **liệt kê ra mọi màn hình phải sửa**. Đây là lưới an toàn cuối — chỗ bắt được những gì đã trôi qua bốn lượt prompt mà không ai để ý.

---

## Slide 25 — Security rules · 2 phút

Đây là slide làm cho chữ "production" trở thành trung thực.

Năm luật, và với mỗi luật là một bài test cụ thể chạy trong Rules Playground.

[HÀNH ĐỘNG] Chỉ vào dòng thứ hai, đọc to.

Đọc kỹ dòng này: **một người ứng tuyển không được phép liệt kê danh sách những người ứng tuyển khác.**

Đây là một lỗ hổng riêng tư thật. Nó là hành vi **mặc định** nếu bạn không cẩn thận. Và điều đáng sợ là: **không giám khảo nào tìm ra nó, nhưng mọi người dùng rồi sẽ phát hiện.**

[HÀNH ĐỘNG] Chỉ vào callout đỏ.

Còn cái rule chắc chắn bạn sẽ viết sai lần đầu là **email liên hệ riêng tư**. Nó phải đọc được bởi chủ nhân, và bởi chủ dự án mà người đó ứng tuyển — và không ai khác. Viết sai một chút là lộ email của toàn bộ sinh viên cho bất kỳ ai ghé qua.

---

## Slide 26 — Prompt sửa lỗi · 1 phút 30

Bốn prompt sửa lỗi, để mở sẵn trong lúc build.

[HÀNH ĐỘNG] Chỉ vào ô đầu tiên.

Cái đầu tiên là lỗi đặc trưng của loại app này: **model tự ý nới rules ra thành `allow read, write: if true`.** Nó làm vậy để cho màn hình chạy được. Và lúc hai giờ sáng bạn sẽ bấm accept.

[HÀNH ĐỘNG] Chỉ vào callout cuối.

Nguyên tắc chung khi sửa: **gọi tên cái luật bị vi phạm, đừng mô tả cảm xúc thất vọng của mình.**

"Thiết kế nhìn sai sai" thì bạn nhận về một cái sai khác. Còn "DESIGN.md cấm đổ bóng, mà file ProjectCard đang có `shadow-md`" thì bạn nhận về một bản sửa.

---

## Slide 27 — Divider Stage 04 · 20 giây

Bước bốn. Với app này, kiểm thử chủ yếu là về **quyền truy cập** và **trạng thái rỗng** — đúng hai thứ luôn trông ổn trên máy bạn, với dữ liệu của bạn.

---

## Slide 28 — Prompt kiểm thử · 2 phút

[HÀNH ĐỘNG] Chỉ vào mục 1.

Mục 1 là bài test mà ai cũng bỏ qua, vì nó cần **một tài khoản Google thứ hai**. Và nó chính là bài tìm ra lỗi riêng tư.

Đăng nhập bằng tài khoản B, rồi thử đọc email của A, liệt kê đơn ứng tuyển của A, sửa dự án của A, sửa pledge của A. **Tất cả phải thất bại.** Hãy tạo tài khoản thứ hai trước ngày demo, đừng để tới hôm đó.

[HÀNH ĐỘNG] Chỉ vào mục 4.

Mục 4 là các trạng thái rỗng: không có dự án nào, dự án chưa ai ứng tuyển, chưa ai ủng hộ, bộ lọc không ra kết quả, và một id dự án không tồn tại. **Màn hình trắng, spinner quay mãi, hay một cục lỗi Firebase thô — đều là trượt.**

Mục 6 thì mình cho grep toàn bộ codebase tìm thư viện thanh toán và các chữ "pay", "donate". Phải là con số không.

---

## Slide 29 — Chi phí thật · 1 phút 30

Nói thật về số giờ. **Tám mươi hai tiếng.**

[HÀNH ĐỘNG] Chỉ sang thẻ bên phải.

Nếu không có đủ tám mươi hai tiếng: cắt phần cập nhật dự án và phần sửa hồ sơ, còn khoảng **sáu mươi tám tiếng**. Không cái nào nằm trong vòng lặp chính.

Giữ lại pledge — gọi vốn là một nửa của bài pitch, và cái thanh chạy lên là khoảnh khắc đẹp thứ hai trong demo.

**Đừng bao giờ cắt các trạng thái rỗng.** Mười tiếng, và đó là phần lớn cái mà giám khảo hiểu là "production".

Và tuyệt đối không cắt **transaction lúc nhận thành viên**. Một tính năng đội nhóm làm hỏng dữ liệu đội còn tệ hơn là không có tính năng đó.

---

## Slide 30 — Divider Stage 05 · 20 giây

Bước năm. Deploy từ hôm trước, và tập demo với hai tài khoản trên hai thiết bị.

---

## Slide 31 — Deploy và demo · 2 phút

[HÀNH ĐỘNG] Chỉ vào thẻ bên trái.

Ba việc phải làm **trước** ngày demo, không phải sáng hôm đó.

Thêm domain đã deploy vào **Authorized domains** của Firebase. **Publish màn hình OAuth consent**, hoặc thêm email giám khảo vào danh sách test users — bỏ qua bước này thì giám khảo bấm đăng nhập và ăn ngay màn hình lỗi. Và chuẩn bị một dự án đã có sẵn đơn ứng tuyển, để hộp thư không trống.

[HÀNH ĐỘNG] Chỉ sang thẻ bên phải.

Về video chín mươi giây: **phải demo trên hai thiết bị.** Vì toàn bộ sản phẩm này nói về hai con người gặp nhau.

Đừng đứng một mình kể lại cả hai phía trên một màn hình. **Hãy để khán giả nhìn thấy đơn ứng tuyển bay tới.** Điện thoại bấm ứng tuyển — laptop nhận được — bấm nhận — đội lớn lên. Đó là khoảnh khắc bán được sản phẩm.

Câu cuối của video: *"Chúng tôi không bao giờ chạm vào tiền. Chúng tôi tạo ra đội."*

---

## Slide 32 — Kết · 1 phút

Kết lại bằng hai lần nói "không".

**Đừng giữ tiền. Và đừng mở ra một căn phòng trống.**

Một lời cam kết thay cho một giao dịch. Mười hai dự án thật thay cho một bảng tin trắng. Cả hai quyết định đều làm sản phẩm **vừa dễ xây hơn, vừa trung thực hơn** — và cả hai đều được chốt trước khi sinh ra một dòng code nào.

Phần còn lại chỉ là bốn cái prompt, một file rules, và việc kiên quyết không chấp nhận "tạm được" ở màn hình đầu tiên.

Cảm ơn mọi người. Mình sẵn sàng nhận câu hỏi.

---

## Phụ lục — Câu hỏi hay gặp

**"Sao không dùng luôn cổng thanh toán ở chế độ test?"**
Được, nhưng nó tạo ra ảo tưởng là sản phẩm đã sẵn sàng nhận tiền. Chuyển từ test sang thật vẫn cần pháp nhân và KYC — tức là toàn bộ phần khó vẫn còn nguyên. Pledge thì trung thực về đúng thứ mình đang làm.

**"Dữ liệu mồi có phải là gian lận không?"**
Không. Mọi marketplace thành công đều làm điều này ở giai đoạn đầu — vấn đề là phải nói rõ đó là dữ liệu mồi khi được hỏi. Đừng giả vờ đó là người dùng thật.

**"Sinh viên dưới 16 tuổi thì sao?"**
Sản phẩm nhắm vào sinh viên đại học. Nếu mở rộng xuống phổ thông thì phải xử lý đồng ý của phụ huynh theo Nghị định 13/2023/NĐ-CP — và đó là một phạm vi khác hẳn, không nên gộp vào MVP này.

**"Tại sao chỉ đăng nhập Google?"**
Không lưu mật khẩu thì không có mật khẩu để lộ. Với một MVP không có đội bảo mật, đó là lựa chọn đúng.
