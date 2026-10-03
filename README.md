# 10IT - Ôn tập giữa Học Kì I

Website dành cho 16 học sinh lớp 10IT. Trang công khai dùng HS01–HS16, không công khai họ tên học sinh hoặc số điện thoại. Danh sách thật chỉ lưu riêng phía máy chủ và trả về sau xác thực. GVCN: Đỗ Đăng Quang; GVPCN: Nguyễn Thị Khánh Huyền.

## Nội dung

- Toán, Văn, Anh, Hoá, Tin: tải nguyên tài liệu giáo viên cung cấp.
- Hoá: hai link YoungTest theo chương; không tự lấy điểm của dịch vụ ngoài.
- Lí: 25 câu mã 1104, 5 hình gốc, nộp bài và xem đáp án đúng/sai theo key. Không sinh lời giải.
- GVCN: thống kê riêng từng học sinh, môn, các lượt làm Lí; xuất CSV.

## Chạy xem thử

Chạy `python3 -m http.server 8080` rồi mở `http://localhost:8080`.

Khi chưa có `apiUrl`, giao diện ghi rõ chế độ xem thử. Không báo kết quả đã đồng bộ. Bản nháp chỉ ở sessionStorage, không phải dữ liệu chính thức; kết quả nộp lưu phía máy chủ khi kết nối được cấu hình.

## Đưa lên GitHub Pages

Kho GitHub: `actack91/on-tap-10it`. Trong Settings → Pages, chọn **Deploy from a branch**, nhánh **main**, thư mục **/(root)**. Các file web và tài liệu nằm ở thư mục gốc.

## Kết nối lưu kết quả chung

GitHub Pages là hosting tĩnh. Bảng GVCN nằm trên website, còn Google Apps Script lưu dữ liệu vào một Google Sheet riêng. Không công khai bảng này.

1. Mở https://script.google.com và tạo dự án `10IT - Ôn tập giữa HKI`.
2. Dán `Code.gs`. Bật hiển thị manifest trong Project Settings rồi dùng `appsscript.json`.
3. Chạy `setup()` đúng một lần và cấp quyền Google Sheets. Mã nguồn không có mật khẩu cố định. Hàm tạo bảng dữ liệu riêng, mã cho 16 em và mã quản trị. Chạy lại không xoá dữ liệu hoặc đổi mã.
4. Thêm Script Property `STUDENT_NAMES` là mảng JSON gồm 16 tên đúng thứ tự; không đăng mảng này lên GitHub. Mở đường dẫn bảng trong Execution log; tab **Mã truy cập** chứa mã riêng. Chỉ cấp mỗi em mã của em; giữ mã GVCN riêng. Không commit, đăng ảnh hoặc công khai tab này.
5. Deploy → New deployment → Web app. Execute as: Me. Who has access: Anyone. Việc này chỉ mở API; dữ liệu đọc/ghi vẫn yêu cầu mã học sinh hoặc phiên GVCN.
6. Chép URL kết thúc `/exec` vào `config.js` (`apiUrl`), commit và đợi Pages cập nhật.
7. Kiểm tra từ hai trình duyệt: học sinh đăng nhập, nộp bài; GVCN đăng nhập, làm mới và thấy cùng lượt làm. Chỉ sau bước này mới khẳng định dữ liệu đã đồng bộ thực tế.

## Giới hạn cần hiểu đúng

- Mã học sinh giảm chọn nhầm tên, không chứng minh danh tính nếu các em chia sẻ mã.
- “Mở / tải” chỉ ghi nhận thao tác mở, không xác nhận file đã tải xong hoặc em đã đọc.
- “Đã ôn” là tự báo. YoungTest không có kết nối lấy điểm.
- Đây là tự luyện: đáp án có trong mã trình duyệt để dùng khi máy chủ lỗi. Không dùng làm kiểm tra có bảo mật đề/key.
- Không quy đổi thang điểm 10 vì tài liệu chưa quy định trọng số; hiển thị số câu đúng /25.
- Thời gian 40 phút là gợi ý; không tự nộp. Thời lượng do thiết bị gửi, không dùng làm bằng chứng giám sát thi.
- Apps Script có hạn mức. Phù hợp lớp nhỏ; nếu triển khai quy mô lớn cần dịch vụ dữ liệu chuyên dụng và phân quyền tài khoản.

Tài liệu: https://docs.github.com/en/pages và https://developers.google.com/apps-script/guides/web
