# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Phan Duy Thành
- MSSV / mã học viên: 2A202602930
- Lớp: H201
- Ngành đã chọn: Tuyển dụng / Quản trị nhân sự (AI sàng lọc hồ sơ ứng viên)

> **Cách dùng bằng chứng trong bài:** Cả ba case đều thuộc ngành tuyển dụng và có nguồn công khai để kiểm tra. Những gì ghi là "nguồn xác nhận" lấy từ bài báo, thông cáo của cơ quan nhà nước hoặc phân tích pháp lý về hồ sơ tòa án. Các mức Severity, Scale, Probability và Frequency là **đánh giá định tính của tôi**, trừ khi có số liệu ghi nguồn. Cáo buộc trong vụ kiện **chưa phải** là kết luận của tòa án.

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | (1) Ứng viên bị loại vì đặc điểm không liên quan đến năng lực như giới tính, tuổi, chủng tộc hay khuyết tật, dẫn đến **mất cơ hội việc làm**. (2) Bias bị **nhân rộng** vì một hệ thống lọc hàng nghìn đến hàng triệu hồ sơ. (3) Ứng viên **không biết mình bị AI loại** nên khó khiếu nại (thiếu minh bạch). (4) Doanh nghiệp và nhà cung cấp phần mềm chịu rủi ro pháp lý, tài chính và uy tín. (5) Nguy cơ lộ dữ liệu cá nhân của ứng viên. |
| Mức độ high-stakes | **Cao.** Quyết định tuyển dụng ảnh hưởng trực tiếp đến thu nhập, sinh kế và con đường sự nghiệp. AI thường được đặt ở **vòng lọc đầu tiên**: ứng viên bị loại ở đây không bao giờ được người thật xem hồ sơ, nên lỗi khó được phát hiện và sửa. |
| Dữ liệu nhạy cảm có thể được sử dụng | CV, ngày sinh/tuổi, giới tính, ảnh chân dung, quốc tịch/dân tộc, tình trạng sức khỏe/khuyết tật, khoảng trống trong quá trình làm việc, kết quả bài test tâm lý/tính cách, video/giọng nói phỏng vấn. Kể cả khi đã bỏ các trường nhạy cảm, AI vẫn có thể suy ra chúng qua **biến đại diện (proxy)** như tên trường, câu lạc bộ, năm tốt nghiệp. (Bài không dùng dữ liệu cá nhân thật.) |
| Nhu cầu human review | **Cao.** (1) **Trước triển khai:** HR và pháp chế kiểm tra những trường dữ liệu nào được dùng và chạy kiểm định tỷ lệ chọn theo nhóm (ví dụ quy tắc 4/5). (2) **Trong vận hành:** nhà tuyển dụng xem lại các hồ sơ bị **tự động loại**, không chỉ hồ sơ được chọn. (3) **Sau triển khai:** audit định kỳ và có kênh để ứng viên yêu cầu người thật xem xét lại. Lý do: case iTutorGroup cho thấy lỗi chỉ lộ ra khi chính ứng viên tự phát hiện. |

### 2. Case study 1 — Amazon: công cụ AI chấm CV thiên lệch với ứng viên nữ

#### Brief Case

- Tổ chức / sản phẩm AI: Amazon. Đây là công cụ tuyển dụng **thử nghiệm, nội bộ** dùng machine learning để chấm điểm CV.
- Thời gian, địa điểm / bối cảnh: Amazon (Seattle, Hoa Kỳ) phát triển công cụ từ năm 2014. Khoảng năm 2015, công ty nhận ra vấn đề. Nhóm phát triển bị giải tán vào đầu năm 2017. Reuters đưa tin ngày 10/10/2018.
- AI được dùng để làm gì: Đọc CV và chấm điểm ứng viên **từ 1 đến 5 sao** để tự động hóa việc tìm ứng viên giỏi, chủ yếu cho vị trí lập trình viên và các vị trí kỹ thuật.
- Vấn đề hoặc sự kiện đáng chú ý: Mô hình được huấn luyện trên CV nộp cho Amazon **trong 10 năm**, phần lớn từ nam giới. Kết quả là mô hình **trừ điểm CV có từ "women's"** (ví dụ "women's chess club captain") và **hạ điểm ứng viên tốt nghiệp hai trường đại học dành riêng cho nữ**. Amazon đã sửa để mô hình trung lập với các từ cụ thể đó, nhưng không thể đảm bảo mô hình sẽ không tìm ra cách phân loại phân biệt khác. Dự án vì vậy bị dừng.
- Số liệu có nguồn: Thang chấm **1–5 sao**. Dữ liệu huấn luyện là CV trong **10 năm**. Công cụ phát triển từ **2014**, phát hiện lệch giới tính vào **2015**, nhóm giải tán đầu **2017** (theo Reuters). Reuters **không** công bố số ứng viên bị ảnh hưởng.
- Nguồn: Jeffrey Dastin, "Amazon scraps secret AI recruiting tool that showed bias against women", *Reuters*, 10/10/2018. Bản đăng lại nguyên văn: [Euronews/Reuters](https://www.euronews.com/business/2018/10/10/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women). Bản gốc: https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G
- Phân biệt bằng chứng và nhận định: **Nguồn xác nhận:** mô hình có thiên lệch giới tính (trừ điểm từ "women's", hạ điểm trường nữ); nguyên nhân là dữ liệu lịch sử nghiêng về nam; Amazon đã dừng dự án. Theo Reuters, nhà tuyển dụng của Amazon **có xem gợi ý của công cụ** khi tìm ứng viên nhưng **không bao giờ chỉ dựa vào** bảng xếp hạng đó. **Tôi suy luận:** nếu công cụ được dùng chính thức thì ứng viên nữ có nguy cơ bị loại oan. **Chưa rõ:** có ứng viên cụ thể nào đã bị loại vì công cụ này hay không. Vì vậy bài coi harm ở đây là **nguy cơ đã được phát hiện trước khi gây thiệt hại rõ ràng**.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Ứng viên nữ nộp CV cho vị trí kỹ sư phần mềm. CV có dòng "Captain, women's chess club" hoặc ghi tốt nghiệp trường đại học dành cho nữ, và mô hình tự động chấm 1–5 sao để quyết định ai được xem tiếp. |
| Stakeholder bị ảnh hưởng | Ứng viên nữ (trực tiếp); nhà tuyển dụng của Amazon (nhận danh sách ứng viên đã bị lệch); Amazon (rủi ro pháp lý và uy tín); nhóm stakeholder không phải khách hàng: phụ nữ trong ngành công nghệ nói chung, vì sự mất cân bằng giới bị củng cố thêm. |
| Failure mode | **Bias / fairness.** Có thể kèm **over-reliance** nếu nhà tuyển dụng tin vào điểm sao mà không tự đánh giá lại. |
| Layer bắt đầu lỗi | **Model (dữ liệu huấn luyện và mục tiêu học).** Mô hình học từ CV 10 năm phần lớn của nam giới nên học luôn mẫu "giống người từng được tuyển". Nguồn xác nhận điều này. **UX:** điểm 1–5 sao trông như đánh giá khách quan, dễ khiến người dùng tin quá mức. Đây là **giả thuyết của tôi**, nguồn không mô tả giao diện. |
| Harm xảy ra là gì? | **Đã xác nhận:** mô hình đánh giá ứng viên nữ thấp hơn một cách có hệ thống qua các từ khóa liên quan đến nữ. **Nguy cơ (chưa xác nhận đã xảy ra):** ứng viên nữ đủ năng lực bị loại ở vòng đầu và mất cơ hội phỏng vấn. Amazon có nguy cơ vi phạm luật chống phân biệt đối xử. |
| Harm lens | Opportunity loss; Dignity loss (bị đánh giá thấp vì giới tính chứ không phải năng lực). |
| Severity | **High.** Mất cơ hội việc làm ảnh hưởng trực tiếp đến thu nhập và sự nghiệp. Không xếp Critical vì không có tổn hại thể chất hay thiệt hại không thể phục hồi được nguồn xác nhận. |
| Scale | **Chưa đủ dữ liệu để định lượng.** Reuters không nêu số ứng viên. Nhận định của tôi: tiềm năng **High** nếu triển khai thật, vì Amazon tuyển dụng rất lớn (Reuters: lực lượng lao động toàn cầu hơn **575.700** người vào đầu 2017), nhưng thực tế chỉ ở mức thử nghiệm. |
| Probability | **Thiên lệch: đã quan sát được** trong mô hình. Khả năng gây thiệt hại thực tế: **Low–Medium (đánh giá của tôi)**, vì theo Reuters nhà tuyển dụng có xem gợi ý nhưng không chỉ dựa vào xếp hạng, và dự án đã bị dừng. |
| Frequency | **High nếu đang chạy:** lỗi nằm trong mô hình nên lặp lại với **mọi** CV có đặc điểm tương tự, không phải lỗi ngẫu nhiên. Hiện tại: **không còn tiếp diễn** vì công cụ đã bị hủy. |
| Vì sao? | Nguồn xác nhận cơ chế lỗi (dữ liệu lịch sử lệch giới tính dẫn đến proxy như "women's" và tên trường nữ). Bài học quan trọng: sửa từng từ khóa **không đủ**, vì mô hình có thể tìm proxy khác. Đó cũng là lý do Amazon dừng dự án. Severity cao vì liên quan cơ hội việc làm. Probability thực tế thấp hơn vì lỗi được phát hiện ở giai đoạn thử nghiệm. |

### 3. Case study 2 — iTutorGroup: phần mềm tuyển dụng tự động loại ứng viên lớn tuổi

#### Brief Case

- Tổ chức / sản phẩm AI: iTutorGroup, gồm iTutorGroup, Inc.; Shanghai Ping An Intelligent Education Technology Co., Ltd.; và Tutor Group Limited. Đây là công ty dạy tiếng Anh trực tuyến, tuyển gia sư ở Hoa Kỳ dạy từ xa.
- Thời gian, địa điểm / bối cảnh: Hành vi loại ứng viên diễn ra năm 2020 (mốc được nêu là tháng 3–4/2020). EEOC (Ủy ban Cơ hội Việc làm Bình đẳng Hoa Kỳ) khởi kiện tháng 5/2022 tại Tòa án Liên bang Quận Đông New York, vụ *EEOC v. iTutorGroup*, số 1:22-cv-02565. Hai bên đạt thỏa thuận ngày 09/08/2023. EEOC ra thông cáo ngày 11/09/2023.
- AI được dùng để làm gì: Phần mềm tiếp nhận và **tự động sàng lọc hồ sơ ứng tuyển gia sư**.
- Vấn đề hoặc sự kiện đáng chú ý: Theo EEOC, phần mềm được lập trình để **tự động loại ứng viên nữ từ 55 tuổi trở lên và ứng viên nam từ 60 tuổi trở lên**. Vụ việc bị phát hiện khi một ứng viên nộp lại **hồ sơ giống hệt** nhưng ghi **ngày sinh trẻ hơn**, và lần này được mời phỏng vấn.
- Số liệu có nguồn: **Hơn 200** ứng viên đủ điều kiện ở Hoa Kỳ bị loại vì tuổi. Mức thỏa thuận là **365.000 USD**, chia cho các ứng viên bị loại tự động. Ngưỡng loại: **nữ ≥ 55 tuổi, nam ≥ 60 tuổi**.
- Nguồn: (1) EEOC, "iTutorGroup to Pay $365,000 to Settle EEOC Discriminatory Hiring Suit", thông cáo báo chí 11/09/2023, https://www.eeoc.gov/newsroom/itutorgroup-pay-365000-settle-eeoc-discriminatory-hiring-suit. (2) Lily M. McNulty, "EEOC Secures First Workplace Artificial Intelligence Settlement", Greenberg Traurig, 23/08/2023, [gtlaw.com](https://gtlaw.com/en/insights/2023/8/eeoc-secures-first-workplace-artificial-intelligence-settlement). Nguồn này nêu số hồ sơ vụ án, các điều khoản thỏa thuận và cách vụ việc bị phát hiện.
- Phân biệt bằng chứng và nhận định: **Nguồn xác nhận:** cáo buộc của EEOC về ngưỡng tuổi, số ứng viên hơn 200, khoản 365.000 USD và các cam kết (đào tạo chống phân biệt, mời ứng viên bị loại nộp lại, **ngừng hỏi ngày sinh** trước khi tuyển). iTutorGroup **không thừa nhận sai phạm** khi dàn xếp. **Lưu ý của tôi:** theo mô tả, đây là **quy tắc lọc được lập trình cứng**, không phải mô hình học máy "tự học" ra thiên lệch. Vụ này thường được gọi là "vụ dàn xếp AI đầu tiên của EEOC", nhưng bản chất là **tự động hóa quyết định**. Dù vậy, nó vẫn cho thấy rõ rủi ro khi giao quyết định loại ứng viên cho phần mềm mà không có người kiểm tra.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Một ứng viên nữ 56 tuổi, đủ trình độ, nộp hồ sơ làm gia sư online. Phần mềm đọc ngày sinh và **tự động loại** hồ sơ trước khi có bất kỳ người nào xem. |
| Stakeholder bị ảnh hưởng | Ứng viên lớn tuổi (nữ ≥ 55, nam ≥ 60); iTutorGroup (bồi thường, nghĩa vụ tuân thủ, uy tín); bên không phải khách hàng: học viên mất cơ hội học với gia sư giàu kinh nghiệm, và người lao động lớn tuổi nói chung vì định kiến tuổi tác bị tự động hóa. |
| Failure mode | **Bias / fairness** (phân biệt tuổi và giới tính được mã hóa thành quy tắc). Kèm **escalation failure**: không có bước chuyển người thật xem xét hồ sơ bị loại. |
| Layer bắt đầu lỗi | **Grounding (quy tắc / cấu hình hệ thống).** Lỗi nằm ở **luật lọc mà con người cài vào phần mềm**, không phải do năng lực mô hình. **Safety:** không có guardrail hay kiểm tra tuân thủ để chặn tiêu chí bị pháp luật cấm. **Không đủ bằng chứng** để nói có mô hình ML nào tham gia. |
| Harm xảy ra là gì? | **Đã xảy ra (theo cáo buộc của EEOC, được giải quyết bằng dàn xếp):** hơn 200 ứng viên đủ điều kiện bị loại vì tuổi, mất cơ hội phỏng vấn và việc làm. Công ty phải trả 365.000 USD và thực hiện các cam kết tuân thủ. |
| Harm lens | Opportunity loss; Dignity loss. |
| Severity | **High.** Bị tước cơ hội việc làm vì tuổi là vi phạm quyền được pháp luật bảo vệ (ADEA) và gây thiệt hại kinh tế thật. Không xếp Critical vì không có tổn hại thể chất. |
| Scale | **Medium:** hơn 200 ứng viên tại Hoa Kỳ (có nguồn). Quy mô nhỏ hơn case Workday nhưng là thiệt hại **đã xảy ra**, không chỉ là nguy cơ. |
| Probability | **Rất cao, gần như chắc chắn**, với ứng viên thuộc nhóm tuổi bị nhắm đến: quy tắc cứng nghĩa là **mọi** hồ sơ vượt ngưỡng đều bị loại. Phép thử nộp lại hồ sơ với ngày sinh trẻ hơn cho thấy điều này. Đây là suy luận của tôi từ cơ chế mà EEOC mô tả. |
| Frequency | **High:** lỗi lặp lại tự động với **mỗi** hồ sơ thuộc nhóm tuổi đó trong suốt thời gian quy tắc còn hoạt động. |
| Vì sao? | Nguồn xác nhận cơ chế (ngưỡng tuổi cố định), quy mô (hơn 200 người) và hậu quả (365.000 USD). Probability và Frequency cao vì đây là lỗi tất định, không phải ngẫu nhiên. Case cho thấy tự động hóa **không làm quyết định trung lập hơn**: nó thực thi định kiến nhất quán và âm thầm hơn. Biện pháp khắc phục do chính thỏa thuận yêu cầu (ngừng thu thập ngày sinh, đào tạo, báo cáo cho EEOC) xử lý đúng các lớp Grounding và Safety. |

### 4. Case study 3 — Workday: vụ kiện tập thể về công cụ AI gợi ý ứng viên

#### Brief Case

- Tổ chức / sản phẩm AI: Workday, Inc. Đây là nhà cung cấp phần mềm nhân sự cho rất nhiều doanh nghiệp. Vụ kiện nhắm vào **hệ thống gợi ý/sàng lọc ứng viên dựa trên AI** của Workday.
- Thời gian, địa điểm / bối cảnh: Vụ *Mobley v. Workday, Inc.*, Tòa án Liên bang Quận Bắc California, số 23-cv-00770-RFL, khởi kiện năm 2023. Ngày **16/05/2025**, tòa **chấp thuận có điều kiện (conditional certification)** cho vụ kiện tập thể theo Đạo luật Chống phân biệt tuổi trong việc làm (ADEA).
- AI được dùng để làm gì: Chấm điểm, xếp hạng và gợi ý ứng viên cho các doanh nghiệp tuyển dụng qua nền tảng Workday.
- Vấn đề hoặc sự kiện đáng chú ý: Nguyên đơn Derek Mobley **cáo buộc** công cụ AI của Workday gây **tác động bất lợi (disparate impact)** theo chủng tộc, tuổi và khuyết tật. Ông cho rằng công cụ được thiết kế phản ánh định kiến của nhà tuyển dụng và dựa trên dữ liệu huấn luyện thiên lệch. Theo các bài tổng hợp, ông đã ứng tuyển hơn 100 vị trí qua các công ty dùng Workday và đều bị từ chối. Workday phản đối, lập luận rằng tác động khác nhau tùy từng doanh nghiệp khách hàng và trình độ ứng viên.
- Số liệu có nguồn: Theo hồ sơ tòa án được Proskauer tóm tắt, chính Workday cho biết **1,1 tỷ hồ sơ ứng tuyển đã bị từ chối** bằng công cụ phần mềm của họ trong giai đoạn liên quan. Nhóm khởi kiện tập thể vì thế có thể lên tới **"hàng trăm triệu"** người.
- Nguồn: Proskauer Rose LLP, "AI Bias Lawsuit Against Workday Reaches Next Stage as Court Grants Conditional Certification of ADEA Claim", *Law and the Workplace*, 11/06/2025, [proskauer.com](https://www.proskauer.com/blog/ai-bias-lawsuit-against-workday-reaches-next-stage-as-court-grants-conditional-certification-of-adea-claim). Thông tin vụ án: *Mobley v. Workday, Inc.*, N.D. Cal., No. 23-cv-00770-RFL, lệnh ngày 16/05/2025.
- Phân biệt bằng chứng và nhận định: **Nguồn xác nhận:** vụ kiện tồn tại; tòa đã cho phép tiến hành kiện tập thể theo ADEA; con số 1,1 tỷ hồ sơ bị từ chối là số do Workday đưa ra. **Chưa được chứng minh:** tòa **chưa phán quyết** về nội dung, tức chưa kết luận AI của Workday thực sự phân biệt đối xử. Con số 1,1 tỷ là **tổng số hồ sơ bị từ chối**, **không phải** số hồ sơ bị từ chối oan. Mọi nội dung về bias ở case này là **cáo buộc** hoặc **nguy cơ**.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Một ứng viên trên 40 tuổi nộp hồ sơ vào nhiều công ty khác nhau. Các công ty này dùng chung công cụ AI của Workday để xếp hạng/gợi ý, và hồ sơ của họ liên tục bị loại (thường trong thời gian rất ngắn) mà không rõ lý do. |
| Stakeholder bị ảnh hưởng | Ứng viên trên 40 tuổi, ứng viên da màu, ứng viên khuyết tật (theo cáo buộc); các doanh nghiệp khách hàng của Workday (có thể chịu trách nhiệm pháp lý dù không tự xây mô hình); Workday (rủi ro pháp lý ở quy mô rất lớn); bên không phải khách hàng: thị trường lao động nói chung, vì một nhà cung cấp chi phối quyết định của rất nhiều nhà tuyển dụng. |
| Failure mode | **Bias / fairness** (theo cáo buộc). Kèm **over-reliance**: doanh nghiệp có thể tin vào gợi ý của nhà cung cấp mà không tự kiểm định. |
| Layer bắt đầu lỗi | **Chưa đủ bằng chứng** để xác định, vì vụ án chưa xét xử nội dung và Workday không công bố chi tiết mô hình. **Giả thuyết của tôi:** **Model** (nếu dữ liệu huấn luyện phản ánh lựa chọn lịch sử thiên lệch của nhà tuyển dụng, như nguyên đơn cáo buộc); **UX** (ứng viên không được thông báo AI tham gia, không có kênh yêu cầu người thật xem lại). |
| Harm xảy ra là gì? | **Nguy cơ / cáo buộc, chưa được tòa xác nhận:** ứng viên thuộc nhóm được bảo vệ bị từ chối có hệ thống và mất quyền "cạnh tranh bình đẳng" (cách tòa mô tả thiệt hại chung khi cho phép kiện tập thể). **Đã xảy ra:** Workday và khách hàng phải đối mặt vụ kiện tập thể quy mô rất lớn. |
| Harm lens | Opportunity loss; Dignity loss. |
| Severity | **High.** Mất cơ hội việc làm lặp đi lặp lại trên nhiều công ty có thể khiến một người gần như bị loại khỏi thị trường lao động ở một số ngành. |
| Scale | **Rất lớn (High):** công cụ được dùng bởi nhiều doanh nghiệp, Workday cho biết 1,1 tỷ hồ sơ bị từ chối, và nhóm kiện tiềm năng có thể tới "hàng trăm triệu" người (có nguồn). **Lưu ý:** đây là quy mô **tiếp xúc** với hệ thống, không phải số người chắc chắn bị hại. |
| Probability | **Chưa đủ dữ liệu để đánh giá.** Không có số liệu công khai về tỷ lệ chọn theo nhóm tuổi hay chủng tộc. Nếu cáo buộc đúng thì xác suất với nhóm bị ảnh hưởng là đáng kể. Đây là đánh giá có điều kiện của tôi. |
| Frequency | **High nếu cáo buộc đúng:** một hệ thống dùng chung chạy trên mọi hồ sơ, nên lỗi lặp lại liên tục và ở nhiều công ty cùng lúc. Một ứng viên có thể bị loại nhiều lần bởi cùng một logic, như cáo buộc rằng ông Mobley bị từ chối hơn 100 lần. |
| Vì sao? | Case này cho thấy rủi ro **tập trung hóa**: khi một nhà cung cấp AI phục vụ nhiều nhà tuyển dụng, một lỗi bias nhỏ có thể nhân lên ở quy mô thị trường. Scale được xếp cao dựa trên số liệu có nguồn. Probability để "chưa đủ dữ liệu" vì vụ án chưa có phán quyết. Tôi không coi cáo buộc là sự thật. |

### 5. Kết luận ngắn

Ba case cùng ngành tuyển dụng cho thấy ba con đường khác nhau dẫn tới cùng một loại harm (**Opportunity loss**):

| Case | Nguồn gốc lỗi | Mức độ bằng chứng |
| --- | --- | --- |
| Amazon | Mô hình **học** thiên lệch từ dữ liệu lịch sử (Model) | Lỗi được xác nhận, dừng trước khi gây hại rõ ràng |
| iTutorGroup | Con người **lập trình** quy tắc phân biệt vào phần mềm (Grounding/cấu hình + thiếu Safety) | Thiệt hại đã xảy ra, dàn xếp 365.000 USD |
| Workday | **Cáo buộc** bias trong công cụ dùng chung cho nhiều doanh nghiệp | Đang tranh tụng, chưa có phán quyết; quy mô tiếp xúc rất lớn |

Bài học chung: trong tuyển dụng, AI thường đứng ở vòng lọc đầu nên **hồ sơ bị loại là chỗ cần human review nhất**, nhưng lại là chỗ ít được xem nhất. Biện pháp tối thiểu: không thu thập dữ liệu nhạy cảm không cần thiết (như ngày sinh), kiểm định tỷ lệ chọn theo nhóm trước và sau triển khai, thông báo cho ứng viên khi AI tham gia, và có kênh yêu cầu người thật xem xét lại.
