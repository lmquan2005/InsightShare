---
title: "Tự đánh giá"
date: 2026-08-06
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

Trong thời gian thực tập tại **Công ty TNHH Amazon Web Services Việt Nam** (chương trình **Workforce Bootcamp – First Cloud AI Journey**, nhóm **AWS062026**) từ **15/06/2026** đến **07/08/2026**, tôi đã có cơ hội học hỏi, thực hành và áp dụng kiến thức đã được trang bị tại Trường Đại học Bách Khoa – ĐHQG TP.HCM vào môi trường cloud thực tế.

Trọng tâm của kỳ thực tập là xây dựng và triển khai dự án **InsightShare** — nền tảng chia sẻ ảnh và tài liệu theo kiến trúc serverless trên AWS, tích hợp **Amazon Rekognition**, **Amazon Textract** và **Amazon Bedrock (Claude)** để gắn nhãn ảnh, trích văn bản và hỏi đáp tài liệu bằng tiếng Việt. Qua dự án này, tôi đã triển khai end-to-end các thành phần **S3**, **Lambda (Python)**, **API Gateway**, **DynamoDB**, **CloudFront**, **CloudWatch** và **IAM**; đồng thời hoàn thiện Proposal, worklog 8 tuần, workshop hướng dẫn và báo cáo song ngữ EN/VI.

Về tác phong, tôi luôn cố gắng hoàn thành nhiệm vụ đúng tiến độ, tuân thủ nội quy FCAJ, chủ động ghi chép lỗi gặp phải (IAM `AccessDeniedException`, serialize `Decimal` trong DynamoDB, quota Bedrock…) và trao đổi với mentor cùng nhóm để tìm hướng xử lý.

Để phản ánh khách quan quá trình thực tập, tôi xin tự đánh giá bản thân dựa trên các tiêu chí dưới đây:

| STT | Tiêu chí | Mô tả | Tốt | Khá | Trung bình |
| --- | --- | --- | --- | --- | --- |
| 1 | **Kiến thức và kỹ năng chuyên môn** | Hiểu biết về cloud/AWS, áp dụng kiến thức vào thực tế, kỹ năng sử dụng công cụ, chất lượng công việc | ✅ | ☐ | ☐ |
| 2 | **Khả năng học hỏi** | Tiếp thu kiến thức mới, học hỏi nhanh các dịch vụ AWS và kiến trúc serverless | ✅ | ☐ | ☐ |
| 3 | **Chủ động** | Tự tìm hiểu tài liệu, đề xuất và triển khai dự án InsightShare mà không chỉ dừng ở bài lab có sẵn | ✅ | ☐ | ☐ |
| 4 | **Tinh thần trách nhiệm** | Hoàn thành công việc đúng hạn, dọn dẹp tài nguyên AWS sau khi thử nghiệm | ✅ | ☐ | ☐ |
| 5 | **Kỷ luật** | Tuân thủ giờ giấc, nội quy FCAJ và quy trình điểm danh/báo cáo | ☐ | ✅ | ☐ |
| 6 | **Tính cầu tiến** | Sẵn sàng nhận feedback, sửa lỗi IAM/DynamoDB và cải thiện từng phiên bản workshop | ✅ | ☐ | ☐ |
| 7 | **Giao tiếp** | Trình bày ý tưởng, viết báo cáo và workshop rõ ràng bằng tiếng Việt và tiếng Anh | ☐ | ✅ | ☐ |
| 8 | **Hợp tác nhóm** | Trao đổi với nhóm AWS062026, tham gia sự kiện và chia sẻ kinh nghiệm triển khai | ☐ | ✅ | ☐ |
| 9 | **Ứng xử chuyên nghiệp** | Tôn trọng mentor, đồng nghiệp và môi trường làm việc của chương trình FCAJ | ✅ | ☐ | ☐ |
| 10 | **Tư duy giải quyết vấn đề** | Nhận diện và xử lý lỗi tích hợp (presigned URL, IAM least-privilege, JSON serialization) | ☐ | ✅ | ☐ |
| 11 | **Đóng góp vào dự án/tổ chức** | Hoàn thiện InsightShare chạy end-to-end, Proposal, workshop và báo cáo thực tập | ✅ | ☐ | ☐ |
| 12 | **Tổng thể** | Đánh giá chung về toàn bộ quá trình thực tập | ✅ | ☐ | ☐ |

### Những điểm đạt được

* Nắm được luồng kiến trúc serverless từ frontend tĩnh → API Gateway → Lambda → S3/DynamoDB, kèm lớp AI.
* Tự triển khai và kiểm chứng được upload, phân tích AI, tìm kiếm theo nội dung và hỏi đáp tài liệu trên AWS thực tế.
* Biết cấu hình IAM theo nguyên tắc least-privilege và giám sát Lambda qua CloudWatch.
* Hoàn thành báo cáo thực tập song ngữ, Proposal và workshop ghi lại quy trình triển khai chi tiết.

### Cần cải thiện

* **Kỷ luật thời gian:** cần lập kế hoạch sớm hơn cho các tuần cuối (tổng kết báo cáo, dọn dẹp tài nguyên) để tránh dồn việc.
* **Tư duy vận hành:** cần đào sâu hơn về monitoring, alerting và xử lý sự cố ở môi trường production (không chỉ mức demo).
* **Giao tiếp kỹ thuật:** cần luyện thêm kỹ năng trình bày kiến trúc và demo sản phẩm trước nhóm lớn hơn, bằng cả tiếng Anh.
* **GenAI trên AWS:** cần tìm hiểu thêm về quota Bedrock, chọn model phù hợp chi phí và các pattern RAG khi mở rộng InsightShare.

### Kết luận

Kỳ thực tập FCAJ đã giúp tôi chuyển từ kiến thức AWS cơ bản (IAM, EC2, VPC, S3) sang triển khai một ứng dụng serverless có tích hợp AI thực tế. Tôi tự tin hơn khi đọc tài liệu AWS, debug lỗi quyền truy cập và xây dựng giải pháp hoàn chỉnh từ ý tưởng đến sản phẩm chạy được. Đây là nền tảng tốt để tiếp tục theo đuổi hướng **Cloud Engineer** và **AI trên nền tảng AWS** sau khi kết thúc chương trình.
