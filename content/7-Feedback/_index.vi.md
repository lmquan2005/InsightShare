---
title: "Chia sẻ, đóng góp ý kiến"
date: 2026-08-06
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

Trong kỳ thực tập **First Cloud AI Journey (FCAJ)** tại **AWS Việt Nam** (nhóm **AWS062026**, 15/06 – 07/08/2026), em xây dựng capstone **InsightShare** — trợ lý tài liệu serverless trên AWS với Rekognition, Textract và Bedrock. Dưới đây là góp ý thật của em để team FCAJ cải thiện cho các khóa sau.

### Đánh giá chung

**1. Môi trường làm việc**  
Văn phòng tầng 26 tòa Bitexco Financial Tower yên tĩnh, trang bị đầy đủ, giúp em tập trung khi làm lab và tham gia sự kiện cộng đồng. Lên văn phòng theo giờ cố định tạo nếp làm việc đều hơn so với tự học ở nhà. Không gian và thương hiệu AWS cũng khiến các buổi meetup và trình bày chuyên nghiệp mà không quá áp lực.

**2. Sự hỗ trợ của mentor / team admin**  
Mentor **Nguyễn Gia Hưng** và team admin theo sát trong suốt kỳ thực tập. Khi em gặp lỗi **IAM `AccessDeniedException`** hoặc **CORS** lúc đưa InsightShare lên Lambda + API Gateway, các anh chị gợi ý hướng tiếp cận thay vì sửa hộ — nhờ vậy em hiểu rõ nguyên nhân sau khi tự xử lý. Team admin cũng hỗ trợ đăng ký Portal, điểm danh và yêu cầu báo cáo đúng hạn.

**3. Sự phù hợp giữa công việc và chuyên ngành học**  
Đề tài InsightShare khớp với ngành **Khoa học máy tính**: dùng kiến thức lập trình, mạng và cơ sở dữ liệu ở trường, đồng thời mở rộng sang **cloud và kiến trúc serverless** — phần chương trình đại học chưa dạy sâu. Làm một sản phẩm end-to-end thực tế có ý nghĩa hơn nhiều so với bài tập rời rạc.

**4. Cơ hội học hỏi & phát triển kỹ năng**  
Em có kinh nghiệm thực hành với **S3, Lambda (Python/boto3), API Gateway, DynamoDB, CloudFront, IAM, CloudWatch**, cùng **Rekognition, Textract và Bedrock**. Em cũng luyện viết tài liệu kỹ thuật song ngữ (worklog, workshop, blog) và deploy báo cáo Hugo lên GitHub Pages. Ba sự kiện FCAJ (Saturday Meetup, Community Day, study tour) bổ sung góc nhìn về sản phẩm AI và định hướng nghề nghiệp.

**5. Văn hóa & tinh thần đồng đội**  
Kiến thức được chia sẻ cởi mở trong các buổi meetup và nhóm cohort — đặt câu hỏi cảm thấy tự nhiên, không ngại. Xem đồng nghiệp trình bày capstone (ví dụ thiết kế IoT + multi-agent) thúc đẩy em hoàn thiện sơ đồ kiến trúc và phần demo của mình.

**6. Chính sách / phúc lợi cho thực tập sinh**  
Chương trình cho học và thực hành miễn phí trên tài nguyên AWS, có lộ trình lab, sự kiện cộng đồng và hỗ trợ nhận mộc thực tập. Một điểm cần cải thiện: hướng dẫn ban đầu về điểm danh, seal và format báo cáo đang nằm rải rác nhiều trang — gom thành một checklist sẽ rút ngắn tuần đầu.

---

### Một số câu hỏi khác

**Điều em hài lòng nhất?**  
Thấy InsightShare chạy end-to-end trên AWS — upload file, nhận nhãn và văn bản AI, tìm theo nội dung, hỏi đáp tiếng Việt qua Bedrock — sau nhiều tuần debug IAM và serialize DynamoDB.

**Điều cần cải thiện cho thực tập sinh sau?**  
Một **timeline capstone mẫu** (mốc từng tuần) và một buổi **office hour** tập trung vào lỗi thường gặp (IAM least-privilege, presigned URL, quota Bedrock) sẽ tiết kiệm thời gian ở tuần 5–8.

**Em có khuyên bạn bè tham gia chương trình không?**  
Có. FCAJ kết hợp học AWS có hệ thống, dự án capstone thật, sự kiện cộng đồng và tiếp xúc trực tiếp với AWS Việt Nam — rất hữu ích cho ai hướng tới cloud hoặc AI engineering.

---

### Đề xuất & mong muốn

- Thêm buổi chia sẻ định kỳ về **các đề tài capstone mẫu** để thực tập sinh chọn hướng sớm hơn.
- Giữ format **Community Day** và **study tour** — chúng nối kiến thức kỹ thuật với thực tế ngành.
- Duy trì và mở rộng chương trình cho các khóa sau; em sẵn sàng gắn bó với cộng đồng FCAJ sau khi tốt nghiệp.
