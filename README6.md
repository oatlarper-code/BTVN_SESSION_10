# 4.Yêu cầu đầu ra
1. Phần I. Phân tích
- Sai lầm thứ nhất: dùng file .docx. Git không thể so sánh từng dòng lệnh trong file nhị phân.Git không hỗ trợ render trực tiếp file .docx
- Sai lầm thứ hai: Khi Nam sửa toàn bộ cấu trúc file bị thay đổi dẫn đến xung đột toàn bộ file không thể hòa hợp
- Markdown là văn bản thuần túy nếu bị mất 1 byte thì chỉ mất đúng 1 ký tự đó các phần còn lại đều ổn định, Markdown chứa các thông tin định dạng không cồng kềnh giúp dung lượng cực nhẹ tải nhanh và tương thích với cơ chế trên web Github
2. Phần II. Hoàn thiện
# Dự án GreenTech - Hệ Thống Nông Nghiệp Xanh
> Giải pháp công nghệ hỗ trợ theo dõi và tự động hóa quy trình chăm sóc cây trồng.
## Giới thiệu chung
- **GreenTech là dự án hướng tới việc ứng dụng công nghệ để bảo vệ môi trường, giúp cuộc sống xanh và bền vững**

## Tính năng chính
- [x] : Tự động đo đạc và giám sát độ ẩm đất, nhiệt độ không khí 24/7.
- [x] : Kích hoạt hệ thống tưới phun sương tự động khi độ ẩm xuống dưới ngưỡng định hình.
- [x] : Cảnh báo tức thời qua còi và đèn LED khi nhiệt độ vườn vượt ngưỡng chịu đựng của hoa Lan (>35°C).
- [x] : Đồng bộ dữ liệu lên nền tảng Cloud theo thời gian thực giúp người nông dân dễ dàng theo dõi từ xa.
- [x] : Tích hợp trí tuệ nhân tạo dự báo lượng nước tưới dựa trên dữ liệu thời tiết

## Hướng dẫn đóng góp
1. Kéo mã nguồn mới nhất về máy: `git pull origin main`
2. Tạo nhánh mới cho tính năng: `git checkout -b feature/ten-tinh-nang`
3. Thực hiện thay đổi và commit: `git commit -m "Add new feature"`
4. Đẩy lên GitHub và tạo Pull Request để nhóm review.
