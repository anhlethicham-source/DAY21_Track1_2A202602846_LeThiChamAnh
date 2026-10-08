# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Lê Thị Châm Anh
- MSSV / mã học viên: 2A202602846
- Lớp: Product Management
- Ngành đã chọn: Giáo dục / AI tutor

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | (1) **Dạy sai kiến thức**: AI tutor tính sai, giải thích sai hoặc xác nhận đáp án sai → học sinh học sai mà không biết, nhất là học sinh yếu vốn không tự phát hiện được lỗi. (2) **Lộ / lạm dụng dữ liệu học sinh**: hệ thống cần điểm số, chuyên cần, hồ sơ giáo dục đặc biệt để "cá nhân hoá" → nếu bị lộ, học sinh (thường là trẻ vị thành niên) và phụ huynh chịu hậu quả lâu dài. (3) **Nội dung không an toàn / không phù hợp lứa tuổi** khi học sinh trò chuyện mở với chatbot, kể cả khi đang hỏi về sức khoẻ tinh thần. (4) **Phụ thuộc, giảm năng lực tự học**: AI đưa đáp án thay vì dẫn dắt. (5) **Bất bình đẳng**: chất lượng kém hơn với ngôn ngữ/nhóm học sinh ít dữ liệu; trường nghèo nhận bản rẻ hơn. (6) **Lãng phí ngân sách công** khi trường mua sản phẩm AI chưa được kiểm chứng. Người bị ảnh hưởng: học sinh, phụ huynh, giáo viên, nhà trường/sở giáo dục. |
| Mức độ high-stakes | **Trung bình → Cao.** Một câu trả lời sai đơn lẻ thường không gây hại tức thì như trong y tế, nhưng: người dùng là trẻ vị thành niên (nhóm dễ tổn thương, tin máy), lỗi tích luỹ qua nhiều buổi học và ảnh hưởng tới điểm thi, xếp lớp, cơ hội học tập; dữ liệu giáo dục đặc biệt và sức khoẻ tinh thần là dữ liệu cực nhạy cảm. Khi AI tham gia chấm điểm, xếp loại hoặc tư vấn tâm lý thì mức độ là **Cao**. |
| Dữ liệu nhạy cảm có thể được sử dụng | Thông tin định danh của trẻ vị thành niên (họ tên, mã học sinh, lớp, trường); điểm số, bài làm, lịch sử học tập; chuyên cần; hồ sơ giáo dục đặc biệt / khuyết tật / nhu cầu hỗ trợ; nhân khẩu học (dân tộc, hoàn cảnh kinh tế); thông tin liên lạc của phụ huynh; nội dung hội thoại có thể chứa chia sẻ về tâm lý, gia đình, bắt nạt. (Bài này không sử dụng dữ liệu thật.) |
| Nhu cầu human review | **Cao.** (1) *Trước triển khai*: giáo viên bộ môn và chuyên gia sư phạm kiểm thử AI trên bộ bài tập chuẩn (đặc biệt toán, tính toán nhiều bước); bộ phận CNTT/pháp chế của trường thẩm định nhà cung cấp về lưu trữ dữ liệu, nơi đặt server, bên thứ ba. (2) *Trong vận hành*: giáo viên xem được log hội thoại và được cảnh báo khi AI phát hiện chủ đề nhạy cảm (tự hại, bắt nạt) → chuyển cho người tư vấn học đường. (3) *Mọi quyết định có hệ quả* (chấm điểm, xếp lớp, kỷ luật) phải do giáo viên quyết định cuối cùng. Lý do: học sinh không đủ năng lực tự phát hiện lỗi của AI, và hậu quả với trẻ em khó đảo ngược. |

### 2. Case study 1 — Khanmigo (Khan Academy) mắc lỗi toán cơ bản và xác nhận đáp án sai của học sinh

#### Brief Case

- Tổ chức / sản phẩm AI: Khan Academy — **Khanmigo**, AI tutor chạy trên GPT-4 (OpenAI).
- Thời gian, địa điểm / bối cảnh: Năm học 2023–2024, Mỹ; Khanmigo đang được thí điểm tại các khu học chánh (school district) và bán cho trường học. Phóng viên Wall Street Journal thử nghiệm sản phẩm, bài báo đăng tháng 2/2024.
- AI được dùng để làm gì: Gia sư AI cho học sinh: dẫn dắt từng bước theo kiểu Socratic (không đưa đáp án ngay), kiểm tra bài làm của học sinh, giải thích kiến thức; đồng thời hỗ trợ giáo viên.
- Vấn đề hoặc sự kiện đáng chú ý: Theo WSJ, Khanmigo **thường xuyên mắc lỗi số học cơ bản** — tính sai phép trừ như 343 − 17, không nhất quán khi làm tròn và khai căn; thường **không tự sửa lỗi** khi được yêu cầu kiểm tra lại. Nghiêm trọng hơn, nó **xác nhận đáp án sai** của người dùng: khi phóng viên đưa đáp án sai 430 (thay vì 440) cho 27² − 17², Khanmigo trả lời *"Excellent!"*; ngược lại, khi đáp án đúng 15² − 9² = 144 được đưa ra, Khanmigo lại bác bỏ (*"I see where you're coming from, but let's take another look at the subtraction."*). Khan Academy thừa nhận công cụ không hoàn hảo và cho biết đang cải thiện độ chính xác.
- Số liệu có nguồn:
  - Khoảng **65.000 học sinh tại 44 khu học chánh** đang thí điểm Khanmigo (thời điểm 2/2024 — theo IBL News, tóm tắt từ WSJ).
  - Sal Khan kỳ vọng **"một hoặc hai triệu"** học sinh dùng vào năm học sau (cùng nguồn).
  - Giá cho trường học: **35 USD/học sinh** (cùng nguồn).
- Nguồn:
  - "We Tested an AI Tutor for Kids. It Struggled With Basic Math." — Matt Barnum, *The Wall Street Journal* — 02/2024 (bài có paywall; tiêu đề và tác giả xác nhận qua bài chia sẻ của WSJ trên LinkedIn và Techmeme: https://x.com/Techmeme/status/1759265440914919530).
  - "Khanmigo Struggles with Basic Math, Showed a Report" — *IBL News* — 20/02/2024 — https://iblnews.org/khanmigo-struggles-with-basic-math-showed-a-report/ (nguồn thứ cấp, dùng cho các con số và trích dẫn ở trên).
- Phân biệt bằng chứng và nhận định:
  - **Nguồn xác nhận**: các lỗi số học cụ thể trong phiên thử nghiệm của phóng viên; việc AI khen đáp án sai và bác đáp án đúng; quy mô thí điểm 65.000 học sinh / 44 khu học chánh; giá 35 USD; Khan Academy thừa nhận sản phẩm chưa hoàn hảo.
  - **Tôi suy luận / chưa rõ**: không có bằng chứng công khai về việc học sinh cụ thể bị điểm kém vì Khanmigo; không có số liệu tỉ lệ lỗi trên toàn bộ hội thoại (thử nghiệm của báo là mẫu nhỏ, không phải đánh giá thống kê). Nguyên nhân kỹ thuật (LLM dự đoán token nên yếu tính toán, và xu hướng "chiều lòng" người dùng — sycophancy) là suy luận của tôi dựa trên hiểu biết chung về LLM, không phải do Khan Academy công bố. Tôi chưa đọc được toàn văn bài WSJ do paywall.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Học sinh tự làm bài toán nhiều bước (ví dụ định lý Pythagoras) và nhờ Khanmigo **kiểm tra đáp án** — lúc này học sinh tin AI là "người chấm" và không có giáo viên bên cạnh. |
| Stakeholder bị ảnh hưởng | Học sinh (đặc biệt học sinh yếu, mất gốc — nhóm cần gia sư nhất nhưng ít khả năng phát hiện lỗi nhất); giáo viên (phải sửa lại hiểu sai); phụ huynh; khu học chánh đã trả tiền; Khan Academy (uy tín). |
| Failure mode | (1) **Lỗi tính toán / hallucination về sự thật** (tính sai phép trừ, căn bậc hai). (2) **Sycophancy** — xác nhận đáp án sai của người dùng ("Excellent!"). (3) **Phản bác sai** đáp án đúng. (4) **Không tự sửa** khi được yêu cầu kiểm tra lại. |
| Layer bắt đầu lỗi | **Model** là gốc: LLM sinh văn bản theo xác suất nên tính toán không tin cậy và có xu hướng đồng ý với người dùng. **Grounding** cũng thiếu: kết quả số học không được kiểm tra bằng công cụ tính toán xác định (calculator / CAS) trước khi phản hồi. Ở mức **UX**, sản phẩm đặt AI vào vai trò "kiểm tra đáp án" — vai trò đòi hỏi độ chính xác gần tuyệt đối — trong khi cảnh báo "có thể sai" dễ bị học sinh bỏ qua. (Việc Khanmigo có/không dùng công cụ tính toán ở thời điểm đó: chưa đủ bằng chứng công khai.) |
| Harm xảy ra là gì? | **Đã xảy ra (có bằng chứng)**: AI đưa ra phép tính sai và xác nhận đáp án sai trong thử nghiệm của WSJ trên sản phẩm đang phục vụ ~65.000 học sinh. **Nguy cơ (chưa có bằng chứng xảy ra trên học sinh thật)**: học sinh ghi nhớ cách làm/đáp án sai; mất tự tin khi bị AI bác đáp án đúng; giáo viên mất thời gian sửa; niềm tin vào công cụ học tập giảm. |
| Harm lens | **Chất lượng giáo dục / thông tin sai lệch (misinformation)**; tác động tới **nhóm dễ tổn thương** (trẻ vị thành niên); **bất bình đẳng** (học sinh yếu bị ảnh hưởng nặng hơn); tổn thất kinh tế cho nhà trường. |
| Severity | **Medium.** Một lỗi đơn lẻ có thể sửa được và không gây hại thể chất; nhưng nâng lên High nếu AI được dùng để chấm điểm/đánh giá năng lực hoặc thay thế giáo viên ở nơi thiếu giáo viên. |
| Scale | **Trung bình → lớn**: ~65.000 học sinh tại 44 khu học chánh lúc thí điểm, mục tiêu 1–2 triệu học sinh năm học sau (theo nguồn). Lỗi nằm ở model dùng chung nên nếu có, nó ảnh hưởng mọi người dùng chứ không riêng một trường. |
| Probability | **Cao** trong các bài có tính toán số học nhiều bước: phóng viên gặp lỗi lặp lại trong một số lần thử ít ỏi, và đây là điểm yếu đã biết của LLM. Thấp hơn với câu hỏi khái niệm không cần tính toán. |
| Frequency | **Thường xuyên / lặp lại** theo mô tả "frequently makes basic arithmetic errors" của WSJ; tuy nhiên chưa có tỉ lệ lỗi định lượng, nên đây là ước lượng định tính. |
| Vì sao? | Severity Medium vì hậu quả chủ yếu là học sai, có thể khắc phục nếu giáo viên phát hiện, nhưng người dùng là trẻ em và lỗi khó tự phát hiện. Scale dựa trên con số thí điểm có nguồn. Probability/Frequency dựa trên mô tả của WSJ + đặc điểm đã biết của LLM. **Giới hạn bằng chứng**: thử nghiệm báo chí là mẫu nhỏ; không có số liệu về tác hại thực tế lên kết quả học tập; tôi chưa đọc được toàn văn WSJ (paywall), dùng nguồn thứ cấp IBL News. **Biện pháp đề xuất**: dùng công cụ tính toán xác định cho mọi phép tính, chống sycophancy (không khen trước khi tự kiểm chứng), bộ test toán chuẩn trước mỗi lần cập nhật model, hiển thị rõ cho giáo viên các hội thoại có kiểm tra đáp án. |

### 3. Case study 2 — Chatbot "Ed" của Los Angeles Unified (LAUSD) và nhà cung cấp AllHere

#### Brief Case

- Tổ chức / sản phẩm AI: Los Angeles Unified School District (LAUSD) — khu học chánh lớn thứ hai nước Mỹ; chatbot AI **"Ed"** (hình mặt trời hoạt hình) do startup **AllHere Education** xây dựng.
- Thời gian, địa điểm / bối cảnh: Los Angeles, Mỹ. Ra mắt rầm rộ tháng 3/2024 (Tổng giám đốc học khu Alberto Carvalho gọi là "game changer"); bị tắt khoảng tháng 6/2024, chỉ ~3 tháng sau, khi AllHere cho phần lớn nhân viên nghỉ việc vì khó khăn tài chính.
- AI được dùng để làm gì: Trợ lý / "người bạn học" cá nhân hoá cho học sinh và phụ huynh: trả lời câu hỏi như "con tôi được điểm toán bao nhiêu?", cho biết con có đi học hôm nay không, điểm kiểm tra gần nhất, và hướng học sinh tới tài nguyên học tập và hỗ trợ sức khoẻ tinh thần.
- Vấn đề hoặc sự kiện đáng chú ý:
  - AllHere sụp đổ, CEO rời đi, chatbot bị tắt ngay → học khu mất khoản đã trả và dự án.
  - Một **người tố giác** (Chris Whiteley, cựu giám đốc cấp cao kỹ thuật phần mềm của AllHere) báo cho học khu, văn phòng tổng thanh tra (inspector general) và cơ quan giáo dục bang rằng Ed xử lý dữ liệu học sinh trái với quy định bảo mật của chính LAUSD: **đưa thông tin định danh của học sinh vào mọi prompt** kể cả khi không cần, **chia sẻ không cần thiết cho bên thứ ba**, và **xử lý prompt trên server ở nước ngoài**. Văn phòng tổng thanh tra LAUSD mở điều tra.
  - LAUSD tuyên bố AllHere "không được phép lưu trữ dữ liệu học sinh ngoài nước Mỹ khi chưa có sự đồng ý trước bằng văn bản".
  - 11/2024: nhà sáng lập/CEO AllHere Joanna Smith-Griffin bị bắt và truy tố (gian lận chứng khoán, gian lận qua đường dây, trộm cắp danh tính nghiêm trọng) vì bị cáo buộc lừa nhà đầu tư gần 10 triệu USD — đây là **cáo buộc**, chưa phải phán quyết.
- Số liệu có nguồn:
  - Hợp đồng **~6 triệu USD trong 5 năm**; học khu **đã trả ~3 triệu USD** khi Ed bị tắt (The 74, 28/07/2024).
  - LAUSD có **~540.000 học sinh** (The 74, 01/07/2024).
  - AllHere đã gọi vốn **hơn 12 triệu USD**, có **khoảng 50 nhân viên**, phần lớn bị cho nghỉ (The 74).
  - Theo mã nguồn người tố giác cung cấp cho The 74: **7/8 yêu cầu (request) của chatbot Ed** được gửi tới server ở nước ngoài (Nhật, Thuỵ Điển, Anh, Pháp, Thuỵ Sĩ, Úc, Canada).
  - Cáo trạng: bị cáo buộc lừa nhà đầu tư **gần 10 triệu USD**; báo với nhà đầu tư doanh thu ~**3,7 triệu USD** trong năm trước trong khi thực tế chỉ ~**11.000 USD** (theo công tố viên liên bang, 11/2024).
- Nguồn:
  - "Whistleblower: L.A. Schools' Chatbot Misused Student Data as Tech Co. Crumbled" — Mark Keierleber, *The 74* — 01/07/2024 — https://www.the74million.org/article/whistleblower-l-a-schools-chatbot-misused-student-data-as-tech-co-crumbled/
  - "LA Unified Faces Criticism After Collapse of Splashy AI Tool 'Ed'" — Ben Chapman, *The 74* — 28/07/2024 — https://www.the74million.org/article/la-unified-faces-criticism-after-collapse-of-splashy-ai-tool-ed/
  - "CEO Of Artificial Intelligence Startup Company Charged With Defrauding Investors" — U.S. Attorney's Office, Southern District of New York (Bộ Tư pháp Mỹ) — 11/2024 — https://www.justice.gov/usao-sdny/pr/ceo-artificial-intelligence-startup-company-charged-defrauding-investors
- Phân biệt bằng chứng và nhận định:
  - **Nguồn xác nhận**: thời gian ra mắt/tắt; giá trị hợp đồng và số tiền đã trả; loại dữ liệu Ed truy cập (theo hợp đồng); nội dung tố giác và mã nguồn cho thấy request đi qua server nước ngoài; học khu mở điều tra; CEO bị truy tố.
  - **Chưa rõ / chưa được chứng minh**: chưa có bằng chứng công khai rằng dữ liệu học sinh **đã thực sự bị lộ hoặc bị đánh cắp** — LAUSD cho biết điều tra không thấy liên quan giữa AllHere/Ed và sự cố Snowflake; các cáo buộc gian lận là cáo buộc hình sự chưa có phán quyết; số học sinh/phụ huynh thực sự đã dùng Ed chưa rõ.
  - **Tôi suy luận**: gốc rễ của sự cố là quy trình mua sắm và thẩm định nhà cung cấp (vendor due diligence) yếu, cộng với kiến trúc đưa quá nhiều dữ liệu nhạy cảm vào LLM — vi phạm nguyên tắc tối thiểu hoá dữ liệu.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Mỗi lần học sinh/phụ huynh hỏi Ed một câu (kể cả câu chung chung): hệ thống ghép **toàn bộ thông tin định danh và hồ sơ học tập/giáo dục đặc biệt** vào prompt rồi gửi tới server ngoài nước Mỹ và bên thứ ba. Thời điểm rủi ro thứ hai: khi nhà cung cấp sụp đổ — dữ liệu đã thu thập nằm ở đâu, ai kiểm soát? |
| Stakeholder bị ảnh hưởng | ~540.000 học sinh LAUSD (trẻ vị thành niên, gồm học sinh khuyết tật có hồ sơ giáo dục đặc biệt); phụ huynh; giáo viên, nhân viên học khu; người nộp thuế (ngân sách công); nhà đầu tư của AllHere; niềm tin của cộng đồng vào AI trong trường học. |
| Failure mode | (1) **Rò rỉ / xử lý dữ liệu sai quy định** — đưa PII không cần thiết vào prompt, chuyển dữ liệu ra nước ngoài, chia sẻ cho bên thứ ba. (2) **Thất bại của nhà cung cấp (vendor failure)** khiến dịch vụ ngừng đột ngột. (3) **Thiếu kiểm soát / giám sát** của bên mua (học khu). |
| Layer bắt đầu lỗi | **Grounding** (tầng truy xuất và đưa dữ liệu vào model): hệ thống lấy và nhồi PII vào mọi prompt thay vì chỉ lấy đúng trường cần cho câu hỏi. **Safety / quản trị dữ liệu**: không có kiểm soát nơi lưu trữ (data residency), không giới hạn chia sẻ bên thứ ba. Ngoài 4 layer kỹ thuật, lỗi lớn nằm ở **quản trị tổ chức** (thẩm định nhà cung cấp, giám sát hợp đồng). Không có bằng chứng lỗi ở tầng Model (câu trả lời sai) — chưa đủ bằng chứng. |
| Harm xảy ra là gì? | **Đã xảy ra**: học khu mất ~3 triệu USD đã trả và dịch vụ bị dừng sau ~3 tháng; phụ huynh/học sinh mất công cụ đã được quảng bá; theo mã nguồn người tố giác cung cấp, dữ liệu học sinh đã được xử lý trên server ở nước ngoài — trái với quy định mà LAUSD nêu. **Nguy cơ (chưa được chứng minh)**: dữ liệu nhạy cảm của trẻ vị thành niên (điểm, chuyên cần, hồ sơ giáo dục đặc biệt) bị lộ/bị hack, bị dùng sai mục đích, hoặc thất lạc khi công ty phá sản; hậu quả lâu dài như kỳ thị, bị lừa đảo nhắm vào phụ huynh. |
| Harm lens | **Quyền riêng tư & bảo mật dữ liệu** (trẻ vị thành niên, dữ liệu giáo dục đặc biệt); **tổn thất kinh tế / lãng phí ngân sách công**; **mất niềm tin & trách nhiệm giải trình** (accountability) của tổ chức công. |
| Severity | **High.** Dữ liệu liên quan đến trẻ em và khuyết tật, nếu lộ thì không thể "thu hồi"; tiền công đã mất; sự cố làm tổn hại niềm tin vào AI trong giáo dục công. Chưa ở mức Critical vì chưa có bằng chứng dữ liệu đã thực sự bị đánh cắp hay gây hại thể chất. |
| Scale | **Lớn**: hệ thống được thiết kế cho toàn học khu ~540.000 học sinh và gia đình; dữ liệu được kết nối từ nhiều hệ thống của học khu. Số người thực sự đã dùng Ed trước khi tắt: chưa rõ. |
| Probability | **Nguy cơ lộ dữ liệu: Trung bình → Cao** trong thiết kế đó, vì PII đi kèm *mọi* prompt và qua nhiều server/bên thứ ba → bề mặt tấn công lớn. **Thất bại nhà cung cấp: đã xảy ra** (xác suất = 1 với case này). |
| Frequency | Rủi ro xử lý dữ liệu sai quy định là **liên tục** — xảy ra ở mỗi request (7/8 request đi ra nước ngoài theo mã nguồn được dẫn). Sự kiện sụp đổ nhà cung cấp là **một lần**, nhưng kiểu sự cố này có thể lặp lại ở nhiều học khu mua sản phẩm AI từ startup chưa được kiểm chứng. |
| Vì sao? | Đánh giá dựa trên các con số có nguồn (hợp đồng, số tiền đã trả, quy mô học khu, 7/8 request ra nước ngoài, cáo trạng của Bộ Tư pháp Mỹ). **Giới hạn bằng chứng**: phần lớn chi tiết kỹ thuật đến từ một người tố giác và mã nguồn người đó cung cấp cho báo; kết quả điều tra của tổng thanh tra LAUSD chưa được tôi tìm thấy công bố đầy đủ; cáo buộc hình sự chưa có phán quyết; chưa có bằng chứng dữ liệu đã bị đánh cắp. **Biện pháp đề xuất**: tối thiểu hoá dữ liệu (chỉ truy xuất trường cần thiết, ẩn danh hoá trước khi gửi model); yêu cầu data residency và danh sách bên thứ ba (sub-processor) trong hợp đồng; kiểm toán bảo mật độc lập trước khi triển khai; điều khoản bàn giao/xoá dữ liệu khi nhà cung cấp ngừng hoạt động; thẩm định tài chính nhà cung cấp; thí điểm nhỏ trước khi triển khai toàn học khu. |
