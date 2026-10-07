# LAB 21 — Phân tích rủi ro AI qua case study thực tế

> **Phân tích đề + Hướng dẫn chi tiết từng bước**
> Khóa: Day 21 — AI Ethics, AI Safety, Responsible AI & Luật AI tại Việt Nam (Track 1)
> Tài liệu gốc: runbook Lab 21 trên VLearn (6 bước + mục nộp bài) và slide *k4-slide-ai-ethic-responsible-ai-compliance* (trang 22–25, 28, 31)

---

## 0. Thông tin nhanh — đọc trước

| Mục | Nội dung |
| --- | --- |
| Hình thức | **Bài cá nhân** (slide trang 31 có thêm phần thảo luận nhóm — xem mục 7) |
| Sản phẩm nộp | **Link repo GitHub cá nhân** có file `README.md` chứa toàn bộ bài làm |
| Tên repo | `DAY21_Track1_MSSV_HoVaTen` (ví dụ: `DAY21_Track1_21001234_NguyenVanAn`) |
| Thời gian gợi ý | 120 phút |
| **Hạn nộp (hiển thị trên VLearn)** | **07/10/2026 23:59 (giờ Việt Nam)** |
| Kênh nộp | AI Codelabs (theo runbook) + mục *Nộp bài và đánh giá Lab* trên VLearn (dán cùng link). Nếu không chắc kênh nào được chấm → hỏi Lab Coach |
| Số lần nộp | AI Codelabs: tối đa 3 lần/Lab. VLearn: "mỗi lab giữ một bài; nộp lại sẽ ghi đè" |

**Ba thứ bắt buộc phải có trong README.md:**

1. **Industry Risk Snapshot** — đánh giá nhanh rủi ro của 1 ngành (4 nội dung).
2. **Brief Case** — 2–3 case AI **có thật**, **cùng ngành**, mỗi case có **số liệu + nguồn**.
3. **Harm Map Worksheet** — 1 bảng **đủ 11 trường** cho **mỗi** case.

---

## 1. Phân tích đề: Lab này thực sự kiểm tra điều gì?

### 1.1. Mục tiêu học tập

Lab 21 là phần thực hành của mảng **Responsible AI** trong slide. Khung NIST AI RMF gồm 4 việc: *Govern – Map – Measure – Manage*; lab này tập trung vào **Map (nhận diện rủi ro)** và một phần **Measure (đánh giá mức độ)**. Cụ thể, bạn được kiểm tra 4 năng lực:

| Năng lực | Thể hiện ở phần nào | Giảng viên sẽ nhìn vào |
| --- | --- | --- |
| Nhìn rủi ro ở **mức ngành** | Industry Risk Snapshot | Có lý do cho từng nhận định, không chỉ ghi nhãn Thấp/TB/Cao |
| **Tìm và đọc nguồn** thật | Brief Case | Case có thật, cùng ngành, có số liệu đo được và URL mở được |
| **Phân tích có cấu trúc** | Harm Map Worksheet | Đi đúng luồng Moment → Mode → Layer → Harm → Severity |
| **Trung thực về bằng chứng** | Cả bài | Tách rõ "nguồn xác nhận" với "tôi suy luận"; không biến nguy cơ thành sự thật |

### 1.2. Luồng làm bài tổng thể

```
Chọn 1 ngành
   └─► Industry Risk Snapshot (4 dòng, mỗi dòng có lý do)
          └─► Tìm 2–3 case thật trong CÙNG ngành
                 ├─► Case 1: Brief Case (số liệu + nguồn) ─► Harm Map (11 trường)
                 ├─► Case 2: Brief Case (số liệu + nguồn) ─► Harm Map (11 trường)
                 └─► (Case 3: tùy chọn)
                        └─► Lưu tất cả vào README.md ─► Commit ─► Kiểm tra ẩn danh ─► Nộp link
```

### 1.3. Bốn lỗi khiến mất điểm nhiều nhất (theo runbook)

| Lỗi | Vì sao sai | Cách tránh |
| --- | --- | --- |
| Case thuộc **nhiều ngành khác nhau**, hoặc **chỉ 1 case** | Đề yêu cầu 2–3 case **cùng ngành** | Chốt ngành trước, chỉ tìm case trong phạm vi ngành đó |
| Có mô tả nhưng **thiếu số liệu / nguồn / Harm Map** | Brief Case bắt buộc có số liệu + nguồn | Không có số liệu phù hợp → tìm thêm nguồn hoặc đổi case |
| Ghi **tác hại giả định như đã xảy ra** | Vi phạm nguyên tắc bằng chứng | Dùng cụm "nguy cơ có thể…" khi nguồn chỉ xác nhận lỗi, chưa xác nhận thiệt hại |
| Sửa README nhưng **chưa Commit** / chưa xác nhận link trên hệ thống nộp | Giảng viên thấy bản cũ hoặc không thấy bài | Commit → mở repo ở cửa sổ ẩn danh → nộp → kiểm tra lịch sử nộp |

---

## 2. Khung lý thuyết cần nắm (tóm tắt từ slide trang 22–25)

### 2.1. Thuật ngữ cốt lõi

| Thuật ngữ | Hiểu đơn giản | Bạn sẽ ghi gì |
| --- | --- | --- |
| **Brief Case** | Tóm tắt một trường hợp AI có thật | Hệ thống nào, dùng làm gì, vấn đề gì, số liệu, nguồn |
| **High-stakes** | Quyết định ảnh hưởng lớn đến sức khỏe, quyền lợi, cơ hội của một người | Điều gì khiến ngành có tác động lớn |
| **High-risk moment** | Khoảnh khắc AI tham gia một quyết định / tình huống nhạy cảm | Một tình huống **cụ thể**, không chung chung |
| **Failure mode** | Kiểu AI mắc lỗi | Hallucination, Bias, Privacy leak… |
| **Layer** | Lớp trong hệ thống nơi lỗi **bắt đầu** | UX / Grounding / Safety / Model |
| **Harm** | Hậu quả cụ thể với người hoặc tổ chức | Ai bị ảnh hưởng + mất gì |
| **Harm lens** | Loại tác hại | Misinformation, Opportunity loss, Injury, Privacy loss, Dignity loss |
| **Human review / human-in-the-loop** | Có người kiểm tra / can thiệp ở bước cần thiết | Ai kiểm tra, ở bước nào, vì sao |

### 2.2. Tám failure mode (slide trang 22)

| Mode | AI sai kiểu gì? | Hay xảy ra khi nào? | Nên kiểm tra ở đâu? |
| --- | --- | --- | --- |
| **Hallucination** (bịa thông tin) | Bịa fact, policy, số liệu, link, deadline nhưng nói rất tự tin | Thiếu dữ liệu chuẩn, thiếu grounding/RAG, hỏi ca ngoại lệ | Grounding, nguồn dữ liệu, UX nhắc kiểm tra, chuyển người thật |
| **Bias / fairness** (thiên lệch) | Kết quả lệch giữa các nhóm người, hoặc "có vẻ công bằng" theo kiểu này nhưng bất công theo kiểu khác | Dữ liệu lệch, dùng biến proxy, ngưỡng quyết định không hợp lý | Dữ liệu, model, ngưỡng quyết định, review chính sách |
| **Sycophancy** (chiều người dùng) | Đồng ý với người dùng dù người dùng sai | Câu hỏi gợi ý mạnh, user pushback, prompt đầy cảm xúc | Model, system prompt, cách hiện bằng chứng trong UI |
| **Over-reliance** (tin AI quá mức) | Người dùng coi output là kết luận cuối và ngừng kiểm tra | AI nói quá chắc, giao diện trông "chính thức", không cảnh báo độ chắc chắn | UX, uncertainty cue, monitoring sau triển khai |
| **Harmful advice** (lời khuyên gây hại) | Lời khuyên nguy hiểm về y tế, pháp lý, tài chính, self-harm | Domain rủi ro cao, policy boundary yếu, thiếu escalation | Safety policy, boundary, human escalation |
| **Privacy leak** (rò dữ liệu) | Lộ PII, prompt, tài liệu nội bộ, dữ liệu người khác | RAG/tool phân quyền sai, prompt injection, log sai | Quyền truy cập, RAG, tool use, audit/logging |
| **Escalation failure** (không chuyển người thật) | Đáng ra phải từ chối/chuyển người thật nhưng AI vẫn cố trả lời | Không có rule rõ, không có nút handoff, thiếu fallback | Workflow, handoff, rule, human-in-the-loop |
| **Misuse / jailbreak** (vượt rào / lạm dụng) | Người dùng ép AI làm điều bị cấm hoặc vượt guardrail | Prompt đối kháng, roleplay, tool abuse, jailbreak pattern | Guardrail, safety system, red teaming, monitoring |

> Mẹo: cột **"Hay xảy ra khi nào?"** chính là gợi ý để viết dòng *Vì sao?* và *Layer* trong Harm Map.

### 2.3. Bốn layer — "System Map: lỗi bắt đầu từ layer nào?" (slide trang 23)

| Layer | Đây là lớp gì? | Câu hỏi cần hỏi | Nếu lớp này yếu thì… | Ví dụ trong slide |
| --- | --- | --- | --- | --- |
| **UX** (User experience) | Lớp người dùng nhìn thấy và tương tác | Output có trông như "sự thật chính thức" không? Có cảnh báo độ không chắc, nút xem nguồn, gọi người thật không? | Người dùng tin quá mức, bỏ qua bước kiểm tra | Bot CSKH hiện câu trả lời như quyết định chính thức, không có nhãn "tham khảo" |
| **Grounding** (System message & nguồn dữ liệu) | Lớp hướng dẫn model phải làm gì và bám vào nguồn nào | Model có nối với nguồn chính thức không? Có rule rõ việc chỉ trả lời trong phạm vi tài liệu? Gặp edge case có biết nói "tôi không chắc"? | Model hallucinate, trả lời ngoài phạm vi | Bot HR trả lời sai chính sách nghỉ phép vì không được ground vào handbook mới nhất |
| **Safety** (Safety system) | Lớp guardrail để chặn, từ chối, chuyển cấp | Input/output nào cần chặn? Khi nào phải từ chối? Khi nào escalate sang người thật? | Không nhận ra ca nguy hiểm, AI tiếp tục xử lý khi đáng ra phải dừng | Người dùng hỏi lời khuyên y tế khẩn cấp, bot trả lời tiếp thay vì chuyển bác sĩ/hotline |
| **Model** | Bản thân model dùng cho bài toán | Model có đủ năng lực cho use case không? Có quá yếu so với độ phức tạp? Có phù hợp về reasoning, safety, cost, latency? | Lỗi gốc từ model; nhưng nếu đổ hết cho model sẽ bỏ qua các lớp xung quanh | Dùng model nhỏ, rẻ để đọc hợp đồng dài nên bỏ sót điều khoản quan trọng |

> **Quy tắc vàng về layer:** Nếu nguồn **không đủ** để xác định layer → ghi **"chưa đủ bằng chứng"** + nêu giả thuyết của bạn. **Không** khẳng định hệ thống dùng một kiến trúc (RAG, model X…) mà nguồn chưa công bố.

### 2.4. Luồng Harm Map: Moment → Mode → Layer → Harm → Severity (slide trang 24)

| Bước | Làm gì | Nhãn dùng | Ví dụ |
| --- | --- | --- | --- |
| **MOMENT** | Chọn **1** khoảnh khắc high-risk cụ thể | Không có nhãn cố định | User hỏi bot CSKH: "Tôi có được hoàn vé trong trường hợp ngoại lệ này không?" |
| **MODE** | Gọi tên failure mode | 8 mode ở mục 2.2 | Hallucination |
| **LAYER** | Tìm layer bắt đầu lỗi (debug) | UX / Grounding / Safety / Model | Grounding, UX |
| **HARM** | Viết harm cụ thể — **không chỉ khách hàng trực tiếp mà cả non-customer stakeholders** | Misinformation, Opportunity loss, Injury, Privacy loss, Dignity loss | User tin thông tin sai, đổi vé sai điều kiện, mất tiền; đội CSKH phát sinh khiếu nại |
| **SEVERITY** | Chấm mức độ nghiêm trọng | Low / Medium / High / Critical | High |

Mẫu câu viết Harm: **"[Ai] bị [hậu quả gì] khi [điều gì xảy ra]"**.

### 2.5. Mẫu Harm Map Worksheet đã điền sẵn trong slide (trang 25)

Đây là "đáp án mẫu" của giảng viên — hãy dùng để **căn chỉnh độ chi tiết** cho bài của bạn:

| High-risk moment | Stakeholder | Failure mode | Layer | Harm xảy ra là gì? | Harm lens | Severity | Scale | Probability | Frequency | Vì sao? |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| User hỏi bot CSKH về điều kiện hoàn/đổi vé trong trường hợp ngoại lệ | User trực tiếp; đội CSKH; hãng | Hallucination | Grounding + UX | User tin thông tin sai, đổi/hoàn vé sai điều kiện, mất tiền hoặc trễ kế hoạch; đội CSKH phát sinh khiếu nại | Misinformation / Opportunity loss | High | Medium | Medium | Medium | Thiệt hại tài chính có thật, ảnh hưởng trực tiếp quyết định của user; không phải mọi câu hỏi đều dính, nhưng edge case xuất hiện đều và dễ lặp lại |
| User hỏi câu nhạy cảm về triệu chứng sức khỏe, bot trả lời như đang tư vấn y khoa | User trực tiếp; người thân; đơn vị vận hành | Harmful advice + Escalation failure | Safety + Grounding | User làm theo lời khuyên sai hoặc chậm đi khám; hệ thống không chuyển sang bác sĩ/kênh hỗ trợ | Injury | Critical | Medium | Medium | Medium | Nếu xảy ra có thể gây hại thể chất hoặc làm chậm can thiệp y tế; không phải phiên nào cũng gặp, nhưng là loại harm phải ưu tiên chặn rất sớm |
| Ứng viên nộp CV, hệ thống screening tự động chấm điểm và loại hồ sơ | Ứng viên; HR; công ty tuyển dụng | Bias / fairness | Model + Grounding | Một nhóm ứng viên bị bất lợi dù năng lực tương đương; mất cơ hội phỏng vấn; công ty chịu rủi ro công bằng và pháp lý | Opportunity loss / Dignity loss | High | High | High | High | Nếu dữ liệu lịch sử đã lệch và hệ thống dùng ở vòng lọc đầu, tác động lặp lại trên nhiều hồ sơ và tích lũy thành bias có hệ thống |
| User hỏi bot nội bộ về tài liệu công ty và bot lộ thông tin không nên hiển thị | Nhân viên; công ty; khách hàng/đối tác có dữ liệu bị lộ | Privacy leak | Grounding + Safety | Lộ PII, tài liệu nội bộ, dữ liệu nhạy cảm; tăng rủi ro pháp lý, mất niềm tin, ảnh hưởng nhiều bên | Privacy loss | Critical | High | Medium | Low | Một lần rò dữ liệu có thể gây hậu quả lớn, khó thu hồi; không nhất thiết xảy ra thường xuyên, nhưng blast radius rất rộng nếu quyền truy cập/retrieval cấu hình sai |

> Lưu ý: ví dụ trong slide là **tình huống giả định** để minh họa. Bài của bạn phải dùng **case có thật, có nguồn**.

### 2.6. Thang đánh giá Severity / Scale / Probability / Frequency (gợi ý của runbook — không phải thang điểm chính thức)

| Trường | Câu hỏi | Cách đánh giá |
| --- | --- | --- |
| **Severity** | Nghiêm trọng đến đâu? | Low / Medium / High / Critical — giải thích bằng **hậu quả**. Critical dành cho hậu quả đặc biệt nghiêm trọng (vd: tổn hại thể chất nghiêm trọng, thương vong) |
| **Scale** | Ảnh hưởng rộng đến đâu? | Nêu **số người/phạm vi có nguồn**; nếu chưa có số liệu → Low/Medium/High kèm căn cứ và giới hạn |
| **Probability** | Khả năng xảy ra? | Dùng **tỷ lệ đo được** nếu có; nếu chỉ nhận định → ghi rõ "đây là đánh giá của tôi" |
| **Frequency** | Có lặp lại thường xuyên không? | Tần suất có nguồn, hoặc Low/Medium/High kèm lý do |

Ba nguyên tắc quan trọng:

- **Severity cao ≠ Probability/Frequency cao.** Ví dụ: tai nạn xe tự hành gây tử vong là *Critical* nhưng *Frequency* có thể *Low*.
- Không đủ thông tin → ghi **"chưa đủ dữ liệu để đánh giá"**. **Không tự bịa** phần trăm hay số người bị ảnh hưởng.
- Mọi nhãn phải được giải thích ở dòng **Vì sao?**

---

## 3. Kế hoạch thời gian (120 phút)

| Bước | Việc | Thời gian |
| --- | --- | --- |
| 1 | Hiểu đề, mở slide trang 22–25 và 31 | 5 phút |
| 2 | Tạo repo GitHub đúng tên | 5 phút |
| 3 | Dán mẫu README, điền thông tin cá nhân, Commit | 10 phút |
| 4a | Chọn ngành + viết Industry Risk Snapshot | 10 phút |
| 4b | Tìm, đọc nguồn và viết Brief Case cho 2–3 case | 40 phút |
| 5 | Điền Harm Map cho từng case | 35 phút |
| 6 | Tự kiểm tra, mở ẩn danh, nộp link, kiểm tra lịch sử | 15 phút |

> Mẹo: **Commit sau mỗi phần** (sau Snapshot, sau mỗi case). Nếu trình duyệt lỗi, bạn không mất bài.

---

## 4. Hướng dẫn chi tiết từng bước

### Bước 1 — Hiểu bài lab và chuẩn bị

Chuẩn bị:

- Đã đọc slide AI Ethics, AI Safety, Responsible AI và Luật AI tại Việt Nam.
- Tài khoản **GitHub cá nhân** (đăng nhập sẵn).
- Tài khoản học tập của lớp (để nộp trên AI Codelabs).
- Mở sẵn slide **trang 22–25** (Harm Map) và **trang 31** (Lab Assignment) để đối chiếu.

**Hoàn thành khi:** bạn hiểu 3 yêu cầu cá nhân và biết bài được lưu trong repo của mình.

### Bước 2 — Tạo repo GitHub cá nhân, đặt tên đúng

Quy ước: **`DAY21_Track1_MSSV_HoVaTen`**

| Thành phần | Cách điền |
| --- | --- |
| `DAY21` | Giữ nguyên, viết hoa |
| `Track1` | Giữ nguyên đúng cách viết `Track1` |
| `MSSV` | Mã học viên/mã sinh viên của bạn (chưa biết → hỏi Lab Coach **trước** khi tạo repo) |
| `HoVaTen` | Viết liền, **không dấu, không khoảng trắng**, ví dụ `NguyenVanAn`. Ví dụ với tên "Bùi Hải Nam" → `BuiHaiNam` |
| Dấu phân cách | Dấu gạch dưới `_` giữa 4 phần |

Thao tác trên trình duyệt:

1. Đăng nhập GitHub → bấm **+** (góc trên phải) → **New repository**.
2. **Owner** = tài khoản cá nhân; **Repository name** = tên theo quy tắc trên.
3. Chọn **Public** (để giảng viên mở được). Bật **Add a README file**.
4. Bấm **Create repository**.
5. Kiểm tra: repo có `README.md`, URL dạng `https://github.com/<username-github>/DAY21_Track1_<MSSV>_<HoVaTen>`.

> `<username-github>` là tên tài khoản GitHub, **không phải** MSSV.
> Nếu giảng viên gửi **starter repo**: mở repo đó → **Fork** → chọn tài khoản cá nhân → đặt tên bản fork theo quy tắc → làm trong bản fork.

**Hoàn thành khi:** mở được repo cá nhân, tên đúng, có `README.md`.

### Bước 3 — Tạo file báo cáo từ mẫu

1. Trong repo, mở `README.md` → bấm biểu tượng **bút chì (Edit this file)**.
2. Xóa nội dung cũ, dán mẫu bên dưới (chỉ phần **bên trong** khung code).
3. Điền họ tên, MSSV, lớp, ngành đã chọn.
4. Bấm **Preview** để xem bảng hiển thị đúng → **Commit changes** → mô tả: `Tao khung bao cao Lab 21` → chọn *Commit directly to the main branch* → xác nhận **Commit changes**.
5. Mở lại `README.md`, kiểm tra nội dung đã lưu.

<details>
<summary><b>📄 Mẫu README.md (bấm để mở) — bản chính thức của runbook</b></summary>

```markdown
# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: [Điền họ tên]
- MSSV / mã học viên: [Điền mã]
- Lớp: [Điền lớp]
- Ngành đã chọn: [Chọn một ngành theo đề]

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | [Điền tác hại và người bị ảnh hưởng] |
| Mức độ high-stakes | [Thấp / Trung bình / Cao; giải thích] |
| Dữ liệu nhạy cảm có thể được sử dụng | [Nêu loại dữ liệu, không đưa dữ liệu thật vào bài] |
| Nhu cầu human review | [Thấp / Trung bình / Cao; ai kiểm tra, ở bước nào, vì sao] |

### 2. Case study 1 — [Tên case]

#### Brief Case

- Tổ chức / sản phẩm AI: [Điền]
- Thời gian, địa điểm / bối cảnh: [Điền]
- AI được dùng để làm gì: [Điền]
- Vấn đề hoặc sự kiện đáng chú ý: [Điền sự kiện có nguồn]
- Số liệu có nguồn: [Con số, đơn vị, thời gian/phạm vi đo và nguồn nào cung cấp]
- Nguồn: [Tên tài liệu/bài viết — đơn vị/tác giả — ngày công bố — URL — trang/mục liên quan nếu có]
- Phân biệt bằng chứng và nhận định: [Điều nguồn xác nhận; điều tôi suy luận hoặc còn chưa rõ]

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | [Tình huống cụ thể có rủi ro] |
| Stakeholder bị ảnh hưởng | [Người dùng và các bên liên quan] |
| Failure mode | [Kiểu lỗi AI] |
| Layer bắt đầu lỗi | [UX / Grounding / Safety / Model; giải thích hoặc ghi chưa đủ bằng chứng] |
| Harm xảy ra là gì? | [Ai bị ảnh hưởng + hậu quả; ghi rõ đã xảy ra hay mới là nguy cơ] |
| Harm lens | [Loại tác hại] |
| Severity | [Low / Medium / High / Critical] |
| Scale | [Quy mô tác động và căn cứ] |
| Probability | [Khả năng xảy ra và căn cứ] |
| Frequency | [Tần suất và căn cứ] |
| Vì sao? | [Lý do cho các đánh giá; nguồn hoặc giới hạn bằng chứng] |

### 3. Case study 2 — [Tên case]

#### Brief Case

- Tổ chức / sản phẩm AI: [Điền]
- Thời gian, địa điểm / bối cảnh: [Điền]
- AI được dùng để làm gì: [Điền]
- Vấn đề hoặc sự kiện đáng chú ý: [Điền sự kiện có nguồn]
- Số liệu có nguồn: [Con số, đơn vị, thời gian/phạm vi đo và nguồn nào cung cấp]
- Nguồn: [Tên tài liệu/bài viết — đơn vị/tác giả — ngày công bố — URL — trang/mục liên quan nếu có]
- Phân biệt bằng chứng và nhận định: [Điều nguồn xác nhận; điều tôi suy luận hoặc còn chưa rõ]

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | [Điền] |
| Stakeholder bị ảnh hưởng | [Điền] |
| Failure mode | [Điền] |
| Layer bắt đầu lỗi | [Điền] |
| Harm xảy ra là gì? | [Điền; phân biệt hậu quả đã xảy ra với nguy cơ] |
| Harm lens | [Điền] |
| Severity | [Điền] |
| Scale | [Điền] |
| Probability | [Điền] |
| Frequency | [Điền] |
| Vì sao? | [Điền căn cứ và giới hạn bằng chứng] |
```

</details>

- Mẫu có sẵn **2 case** (mức tối thiểu). Làm case 3: copy nguyên phần Brief Case + Harm Map của case 2 xuống cuối, đổi tiêu đề thành `### 4. Case study 3 — [Tên case]`.
- Nếu lớp phát mẫu Industry Risk Snapshot riêng → dùng mẫu của lớp.
- Bảng Harm Map **dạng dọc** vẫn giữ đủ **11 trường** như worksheet trang 25.

**Hoàn thành khi:** `README.md` đã lưu trên GitHub, có thông tin cá nhân và đủ khung bài làm.