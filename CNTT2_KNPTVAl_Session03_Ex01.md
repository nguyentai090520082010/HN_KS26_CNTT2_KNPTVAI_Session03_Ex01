[Context] Đóng vai trò là Chuyên viên xử lý dữ liệu nhân sự cấp cao.

[Request] Xử lý đoạn email ứng tuyển thô và trả về đồng thời:
1. Một bảng Markdown tóm tắt thông tin ứng viên.
2. Một đối tượng JSON thô chứa thông tin ứng viên để nạp vào database gồm các trường: name, phone, email, position, experience_years, skills.

[Explanation] Dữ liệu này dùng để import trực tiếp vào database tuyển dụng nên cần độ chính xác 100%.

[Action] Quét qua email thô, xác định đúng các trường thông tin theo quy tắc chuẩn hóa:
- Họ tên: Chuyển về dạng viết hoa chữ cái đầu (Ví dụ: Nguyễn Văn A).
- Số điện thoại: Chuẩn hóa về định dạng đầu số quốc gia hoặc loại bỏ dấu cách dư thừa (nếu thiếu điền null).
- Kỹ năng chính: Gom nhóm thành một danh sách (mảng) không trùng lặp (ví dụ: ["Python", "SQL", "FastAPI"]).
- Số năm kinh nghiệm: Chuyển về dạng số nguyên (nếu thiếu điền null).
- Email: Trích xuất chính xác định dạng email (nếu thiếu điền null).
- Vị trí ứng tuyển: Trích xuất rõ ràng vị trí (nếu thiếu điền null).

[Tone] Chính xác, khách quan, không thêm thắt văn phong cảm xúc, tuyệt đối không tự ý bịa đặt thông tin.

[Extras] 
Dưới đây là 2 ví dụ Few-shot mẫu để định hình kết quả:

--- Ví dụ mẫu 1 ---
[Input]: "Chào bộ phận HR, mình là nguyễn đức tài, sđt: 0965942358, email: nguyentai09052010@gmail.com. Mình ứng tuyển vị trí lập trình viên, đã có 2 năm kinh nghiệm làm việc."
[Output]:
| Trường thông tin | Giá trị trích xuất |
| :--- | :--- |
| Họ tên | Nguyễn Đức Tài |
| Số điện thoại | +84965942358 |
| Email | nguyentai09052010@gmail.com |
| Vị trí ứng tuyển | Lập trình viên |
| Số năm kinh nghiệm | 2 |
| Kỹ năng chính | [] |

```
json
{
  "name": "Nguyễn Đức Tài",
  "phone": "+84965942358",
  "email": "nguyentai09052010@gmail.com",
  "position": "Lập trình viên",
  "experience_years": 2,
  "skills": []
}