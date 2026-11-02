# KẾ HOẠCH KIỂM THỬ NHÁP WEBSITE SHOPMEE

## 1. Thông tin tài liệu

| Nội dung | Thông tin |
|---|---|
| Học phần | COMP1307 – Kiểm thử phần mềm cơ bản |
| Nhóm / Lớp | Nhóm 6 / 2611COMP130701 |
| Mã kế hoạch | TP-SM-N6 |
| Phiên bản | 0.1 |
| Ngày lập | 03/11/2026 |
| Trạng thái | Bản nháp, chờ nhóm rà soát và giảng viên góp ý |
| Đề tài chính | Kiểm thử chức năng và kiểm thử hộp trắng website bán hàng ShopMee sử dụng PHP |
| Hướng đề tài | B – Ứng dụng do nhóm tự xây dựng |
| Người phụ trách tổng hợp | Đổng Quốc Thái – 50.01.104.143 |
| Kho GitHub | Chưa cung cấp; bổ sung URL trước khi thực hiện |
| Bản phần mềm kiểm thử | Chưa chốt; ghi tag hoặc mã commit cho mỗi vòng kiểm thử |
| Thời gian thực hiện | Đề xuất 3 tuần làm việc; ngày bắt đầu và hạn nộp chưa chốt |

Kế hoạch xác định phạm vi, cách thực hiện, nhân sự và điều kiện đánh giá kết quả kiểm thử ShopMee. Các ca kiểm thử tập trung vào tài khoản, tìm kiếm sản phẩm, giỏ hàng và đặt hàng COD. Luồng đặt hàng, tính tiền, tồn kho và quyền truy cập đơn hàng được ưu tiên vì ảnh hưởng trực tiếp đến dữ liệu và hoạt động mua hàng.

### 1.1. Căn cứ lập kế hoạch

- [Phiếu đăng ký đề tài ShopMee nhóm 6](https://chatgpt.com/library?file_id=libfile_407109fa9cac8191957cfb1cabb95f42&account_id=personal), phiên bản 2.
- [B03_Nhom6_AIDanhGia.xlsx](https://chatgpt.com/library?file_id=libfile_a42beb8d30f08191afebb1b2b197bd31&account_id=personal), phiên bản 1: kết quả Thực hành 3.2, gồm 10 rủi ro AI đề xuất, phần phản biện và 2 rủi ro bổ sung.
- Bảng yêu cầu số lượng sản phẩm kiểm thử cho nhóm 4 sinh viên trong ảnh yêu cầu tiểu luận.

Các mục về lịch, phân bổ ca, tiêu chí hoàn thành và dữ liệu mẫu trong tài liệu này là đề xuất của bản kế hoạch nháp. Chưa có kết quả thực thi hay xác nhận lỗi phần mềm.

### 1.2. Những thông tin cần chốt

| Mã | Nội dung cần xác nhận | Người phụ trách | Thời điểm cần hoàn thành |
|---|---|---|---|
| C01 | URL GitHub, bản mã nguồn, cách cài đặt, cấu trúc CSDL và URL chạy ứng dụng | Thái, Tinh | Trước vòng kiểm thử đầu tiên |
| C02 | Giới hạn độ dài, định dạng đầu vào, giới hạn số lượng mua và các quy tắc bắt buộc | Sơn, Long | Trước khi chốt kết quả mong đợi của ca EP/BVA liên quan |
| C03 | Mã trạng thái đơn thực tế; thời điểm trừ tồn kho; cách xử lý tồn kho khi hủy đơn; giá dùng để chốt đơn | Thái, Sơn | Trước khi kiểm thử đặt hàng và hủy đơn |
| C04 | Việc dùng PHPUnit cho dự án PHP, do ảnh yêu cầu nêu ví dụ JUnit/NUnit/pytest | Thái | Trước khi chốt bộ unit test nộp bài |
| C05 | Ngày bắt đầu, hạn nộp và thời gian từng thành viên có thể tham gia | Cả nhóm | Khi thống nhất kế hoạch |

Các mốc mật khẩu 8–64 ký tự, họ tên 2–50 ký tự, điện thoại 10 chữ số và số lượng 1–99 trong phiếu đăng ký vẫn là giới hạn dự kiến. Nhóm cần đối chiếu mã nguồn và thống nhất đặc tả trước khi dùng chúng làm điều kiện đạt hoặc không đạt.

## 2. Mục tiêu và sản phẩm dự kiến

### 2.1. Mục tiêu

1. Đánh giá 5 nhóm chức năng trong phạm vi theo các yêu cầu đã được nhóm chốt.
2. Phát hiện sai lệch về dữ liệu đầu vào, tổng tiền, tồn kho, trạng thái đơn và quyền sở hữu đơn hàng.
3. Áp dụng phân vùng tương đương (EP), phân tích giá trị biên (BVA), bảng quyết định và chuyển trạng thái để thiết kế ca kiểm thử.
4. Phân tích mã nguồn của 2 hàm nghiệp vụ bằng đồ thị luồng điều khiển (CFG), độ phức tạp chu trình V(G) và kiểm thử đơn vị.
5. Xây dựng bộ kiểm thử hồi quy có thể chạy lại sau khi sửa lỗi, kèm minh chứng và báo cáo kết quả.

### 2.2. Sản phẩm theo định mức nhóm 4 người

| Sản phẩm | Mục tiêu dự kiến | Cách ghi nhận |
|---|---:|---|
| Nhóm chức năng được kiểm thử | 5 | F01–F05 trong mục 3 |
| Ca kiểm thử chức năng | 80 | Mã ca, tiền điều kiện, dữ liệu, bước chạy, kết quả mong đợi và thực tế |
| Ma trận truy vết yêu cầu (RTM) | Bao phủ toàn bộ yêu cầu trong phạm vi | Liên kết yêu cầu → rủi ro → ca kiểm thử → kết quả → lỗi |
| Hàm phân tích hộp trắng | 2 | Mã nguồn, CFG, V(G), đường đi độc lập và ca kiểm thử tương ứng |
| Ca kiểm thử đơn vị | 20 | Kết quả chạy PHPUnit cho từng ca hoặc bộ dữ liệu tham số hóa |
| Kịch bản hồi quy tự động UI | 10 | Mã kịch bản, ca chức năng liên quan, log và minh chứng chạy |
| Báo cáo lỗi có minh chứng | Mục tiêu 7 lỗi thực tế theo định mức | GitHub Issues, bước tái hiện, kết quả, ảnh hoặc log |
| Báo cáo tổng kết | 1 | Thống kê thực thi, lỗi còn mở, rủi ro còn lại và kiến nghị |

10 kịch bản UI tự động là tập con được chọn từ 80 ca chức năng, không cộng thêm thành 90 ca. 20 ca unit test được thống kê riêng. Nếu số lỗi thực tế phát hiện được ít hơn định mức, nhóm ghi nhận đúng kết quả và trao đổi với giảng viên về cách báo cáo.

## 3. Phạm vi kiểm thử

### 3.1. Các chức năng trong phạm vi

Các mã F01–F05 đồng thời là nhóm yêu cầu dùng trong RTM. Khi chi tiết hóa đặc tả, nhóm có thể tách thành các yêu cầu con.

| Mã | Chức năng | Nội dung kiểm tra chính | Số ca dự kiến |
|---|---|---|---:|
| F01 | Đăng ký tài khoản | Dữ liệu bắt buộc, định dạng email, email trùng, độ dài theo đặc tả, tạo tài khoản thành công | 12 |
| F02 | Đăng nhập và đăng xuất | Thông tin đúng/sai, trường rỗng, phiên đăng nhập, gửi lại yêu cầu sau đăng xuất, truy cập chức năng cần đăng nhập | 16 |
| F03 | Tìm kiếm và lọc theo danh mục | Có/không có kết quả, từ khóa rỗng, ký tự đặc biệt, kết hợp từ khóa và danh mục theo hành vi được quy định | 12 |
| F04 | Quản lý giỏ hàng | Thêm, sửa số lượng, xóa sản phẩm, số lượng hợp lệ, tồn kho, số lượng cộng dồn và tổng tiền | 20 |
| F05 | Đặt hàng COD và quản lý đơn | Điều kiện tạo đơn, thông tin nhận hàng, xem/hủy đơn, trạng thái, quyền sở hữu, yêu cầu lặp, dữ liệu lưu và tồn kho khi đặt đồng thời | 20 |
| **Tổng** | **5 nhóm chức năng** | | **80** |

### 3.2. Nội dung ngoài phạm vi bản nháp

- Phí giao hàng, ngưỡng miễn phí giao hàng và lọc sản phẩm theo khoảng giá, vì nhóm đã xác nhận không có các chức năng này.
- Thanh toán qua cổng trực tuyến; kế hoạch hiện dùng luồng COD.
- Kiểm thử tải lớn hoặc cam kết số người dùng đồng thời, do chưa có yêu cầu hiệu năng và thông số tải được chốt.
- Đánh giá toàn bộ chức năng quản trị hoặc kiểm toán an toàn thông tin toàn diện. Tài khoản quản trị, nếu cần, chỉ được dùng để chuẩn bị dữ liệu và trạng thái phục vụ phạm vi trên.

Web app quản lý kho quà lưu niệm HCMUE là đề tài dự phòng thuộc hướng B. Nếu chuyển đề tài, nhóm cần cập nhật phạm vi, yêu cầu, rủi ro và bộ ca trong phiên bản kế hoạch mới.

## 4. Cơ sở xác định kết quả mong đợi

Nhóm thống nhất quy tắc nghiệp vụ trước khi kết luận một kết quả là lỗi. Khi đặc tả chưa rõ, ca liên quan được ghi “Chờ đặc tả” và chuyển cho người phụ trách xác nhận; các ca độc lập vẫn có thể tiếp tục.

| Quy tắc dự kiến | Nội dung cần kiểm tra |
|---|---|
| Tài khoản | Email dùng để đăng ký phải hợp lệ và không trùng theo quy tắc đã chốt |
| Phiên đăng nhập | Máy chủ từ chối thao tác cần đăng nhập khi không có phiên hợp lệ hoặc phiên đã đăng xuất |
| Số lượng mua | Là số nguyên dương; tổng số lượng cùng sản phẩm không vượt tồn kho và giới hạn bổ sung nếu đặc tả có quy định |
| Tổng tiền giỏ hàng | Bằng tổng đơn giá × số lượng của các dòng sản phẩm; giỏ rỗng có tổng bằng 0 |
| Đặt hàng | Có sản phẩm, đủ tồn kho và thông tin nhận hàng hợp lệ; dữ liệu đơn và tồn kho nhất quán sau thao tác |
| Quyền sở hữu đơn | Khách hàng chỉ xem hoặc yêu cầu hủy đơn trong phạm vi quyền của tài khoản mình |
| Hủy đơn | Theo mô hình hiện tại, chủ đơn chỉ được yêu cầu hủy khi đơn còn chờ xác nhận |

Mô hình trạng thái trong phiếu đăng ký gồm “Chờ xác nhận → Đã xác nhận → Đang giao → Đã giao” và “Chờ xác nhận → Đã hủy”. Nhóm phải ánh xạ các tên này sang mã trạng thái thực tế ở C03, đồng thời chốt các chuyển trạng thái được phép và bị cấm.

## 5. Ưu tiên kiểm thử theo rủi ro

RR01–RR12 tương ứng STT trong bảng Thực hành 3.2. RR10 đã được gộp vào RR02 vì trùng ý về đăng xuất. Các điểm K/A dưới đây là ước lượng ban đầu, chưa phải số liệu lỗi quan sát được.

P1 là ca ưu tiên cao, cần chạy sớm và phải đạt trước khi kết thúc. P2 là ca ưu tiên tiếp theo. Việc xếp ưu tiên xét cả điểm K × A và hậu quả nghiệp vụ, không chỉ dựa vào tích điểm.

| Mã | Rủi ro cần theo dõi | K × A | Nhóm chức năng | Ưu tiên / Hướng kiểm tra |
|---|---|---:|---|---|
| RR01 | Tạo tài khoản trùng email | 3 × 3 = 9 | F01 | P2 – đăng ký lại với email đã tồn tại |
| RR02 | Máy chủ chấp nhận phiên đã đăng xuất | 3 × 4 = 12 | F02 | P1 – gửi lại yêu cầu bằng phiên cũ; phân biệt trang lưu trong bộ nhớ đệm |
| RR03 | Tìm kiếm hoặc lọc danh mục trả sai kết quả | 3 × 3 = 9 | F03 | P2 – đối chiếu dữ liệu mẫu đã biết kết quả |
| RR04 | Chấp nhận số lượng không hợp lệ hoặc vượt tồn | 4 × 4 = 16 | F04 | P1 – EP/BVA và kiểm tra phía máy chủ, gồm số lượng cộng dồn |
| RR05 | Tổng tiền sai sau thay đổi giỏ hàng | 3 × 4 = 12 | F04 | P1 – tính độc lập từ dữ liệu mẫu rồi đối chiếu |
| RR06 | Tạo đơn từ giỏ rỗng hoặc thiếu thông tin | 3 × 4 = 12 | F05 | P1 – bảng quyết định điều kiện đặt hàng |
| RR07 | Lưu dở dang đơn, chi tiết đơn hoặc tồn kho | 3 × 5 = 15 | F05 | P1 – mô phỏng lỗi ghi dữ liệu trong môi trường kiểm thử |
| RR08 | Gửi lặp tạo trùng đơn hoặc trừ tồn nhiều lần | 3 × 4 = 12 | F05 | P1 – gửi lại cùng một thao tác đặt hàng |
| RR09 | Hủy đơn ở trạng thái không cho phép | 3 × 4 = 12 | F05 | P1 – kiểm thử các chuyển trạng thái hợp lệ và không hợp lệ |
| RR11 | Xem hoặc hủy đơn của khách khác | 3 × 5 = 15 | F05 | P1 – dùng hai tài khoản, thay mã đơn trong yêu cầu |
| RR12 | Hai khách đặt đồng thời gây bán vượt tồn | 3 × 5 = 15 | F05 | P1 – hai phiên cùng mua sản phẩm chỉ còn một đơn vị |

RR07 và RR12 cần khả năng kiểm soát dữ liệu, thao tác đồng thời hoặc điểm mô phỏng lỗi. Nếu môi trường chưa hỗ trợ, nhóm ghi rõ ca bị chặn và khắc phục điều kiện chạy trước khi xét hoàn thành.

## 6. Phương pháp và công cụ kiểm thử

### 6.1. Hộp đen và thiết kế ca

- **EP:** chia dữ liệu thành các lớp hợp lệ/không hợp lệ cho đăng ký, đăng nhập, tìm kiếm, số lượng mua và thông tin nhận hàng. Ký tự đặc biệt được kiểm tra theo hành vi đặc tả, không mặc định tất cả đều không hợp lệ.
- **BVA:** với tồn kho S > 0, xét các giá trị 0, 1, 2, S−1, S, S+1 và loại giá trị trùng. Với S = 0, kiểm tra việc từ chối số lượng mua dương. Nếu có mức tối đa M, xem xét biên số lượng thực sự được phép theo cả M và S.
- **BVA cho chuỗi:** lấy giới hạn tối thiểu/tối đa từ đặc tả đã chốt, kiểm tra tại và sát biên; chỉ dùng độ dài không âm. Trường không có giới hạn được quy định sẽ không được gán một mốc tùy ý.
- **Bảng quyết định:** kết hợp đăng nhập hợp lệ, giỏ có sản phẩm, số lượng/stock hợp lệ và thông tin nhận hàng hợp lệ để xác định có được tạo đơn hay không.
- **Chuyển trạng thái:** lập bảng trạng thái đơn và kiểm tra quyền hủy ở từng trạng thái.
- **Kiểm thử khám phá:** bổ sung thao tác gửi lặp, mở nhiều tab, hai phiên đồng thời và thay mã đơn giữa hai tài khoản.

### 6.2. Hộp trắng và unit test

Hai hàm dự kiến là:

| Hàm | Phạm vi dự kiến | Số ca unit dự kiến |
|---|---|---:|
| `kiemTraSoLuongMua($soLuong, $tonKho)` | Kiểu dữ liệu, số nguyên dương, tồn kho và giới hạn thực tế đã được chốt | 10 |
| `tinhTongGioHang($gioHang)` | Giỏ rỗng, số dòng sản phẩm, đơn giá, số lượng và tổng tiền theo hợp đồng hàm | 10 |
| **Tổng** | | **20** |

Tên hàm và hợp đồng đầu vào/đầu ra phải được đối chiếu mã nguồn tại C01/C02. CFG, V(G) và đường đi độc lập được lập từ đúng mã nguồn đó; bản kế hoạch chưa gán giá trị V(G).

Mục tiêu là kiểm tra các đường đi độc lập, đạt 100% câu lệnh và nhánh khả đạt của hai hàm. Nhánh không thể thực thi phải có giải thích. Nếu số ca cần thiết vượt 20 để đáp ứng bao phủ, nhóm tăng số ca và ghi rõ kết quả đo. Unit test dùng dữ liệu độc lập, có kết quả mong đợi được tính trước và không phụ thuộc trạng thái lần chạy trước.

### 6.3. Hồi quy tự động UI

Chọn 10 kịch bản từ bộ 80 ca, ưu tiên các luồng ổn định sau:

| Mã | Kịch bản dự kiến | Liên kết chức năng |
|---|---|---|
| UI01 | Đăng ký với dữ liệu hợp lệ | F01 |
| UI02 | Đăng ký với email đã tồn tại | F01 |
| UI03 | Đăng nhập với thông tin đúng | F02 |
| UI04 | Đăng nhập với thông tin sai | F02 |
| UI05 | Đăng xuất và xác minh chức năng cần đăng nhập bị chặn | F02 |
| UI06 | Tìm sản phẩm và đối chiếu danh mục bằng dữ liệu mẫu | F03 |
| UI07 | Thêm sản phẩm, đổi số lượng và kiểm tra tổng giỏ hàng | F04 |
| UI08 | Xóa hết sản phẩm và kiểm tra trạng thái giỏ rỗng | F04 |
| UI09 | Đặt một đơn COD hợp lệ và kiểm tra dữ liệu đơn | F05 |
| UI10 | Chủ đơn hủy đơn đang chờ xác nhận theo quy tắc đã chốt | F05 |

Mỗi kịch bản có dữ liệu chuẩn bị riêng và liên kết tới mã ca chức năng trong RTM. Kiểm tra dữ liệu lưu tại máy chủ hoặc CSDL khi kết quả trên giao diện chưa đủ chứng minh tính đúng đắn. Các ca quyền sở hữu, đồng thời và lỗi ghi dữ liệu vẫn nằm trong bộ 80 ca, dù chưa được chọn vào 10 kịch bản UI trên.

### 6.4. Bộ công cụ dự kiến

| Công việc | Công cụ | Ghi chú |
|---|---|---|
| Chạy ứng dụng | XAMPP hoặc môi trường PHP/MySQL tương đương | Ghi phiên bản thực tế, cấu hình và cách khởi động |
| Unit test | PHPUnit | Chờ xác nhận C04; chọn bản tương thích PHP của dự án |
| Đo bao phủ | Bộ đo tương thích PHPUnit và môi trường PHP | Ghi công cụ, lệnh chạy và báo cáo; chỉ kết luận bao phủ khi có bằng chứng |
| Kiểm thử UI | Playwright | Chạy trên trình duyệt Chromium; đối chiếu Chrome/Edge sẵn có khi cần |
| Kiểm thử điều kiện phía máy chủ | DevTools hoặc công cụ gửi HTTP phù hợp luồng hiện có | Chỉ dùng các yêu cầu của ứng dụng trong môi trường kiểm thử |
| Quản lý ca và RTM | Excel | Tách ca chức năng, unit và kịch bản tự động khi thống kê |
| Quản lý lỗi | GitHub Issues | Liên kết mã ca, bản phần mềm và minh chứng |
| CI | GitHub Actions | Khởi tạo CSDL kiểm thử, nạp dữ liệu, chạy unit/UI và lưu kết quả |

## 7. Môi trường và dữ liệu kiểm thử

### 7.1. Thiết lập môi trường

1. Chốt tag hoặc commit; ghi phiên bản hệ điều hành, PHP, MySQL, trình duyệt và các công cụ kiểm thử.
2. Cài ứng dụng theo hướng dẫn trong kho mã nguồn. Ghi URL local và cấu hình cần thiết vào nhật ký môi trường.
3. Dùng CSDL kiểm thử riêng, nạp dữ liệu mẫu có thể khôi phục trước mỗi vòng chạy.
4. Chuẩn bị ít nhất hai tài khoản khách hàng để kiểm tra phân tách phiên và quyền sở hữu đơn. Nếu cần, chuẩn bị tài khoản quản lý để thiết lập trạng thái đơn.
5. Kiểm tra nhanh ứng dụng mở được, đăng nhập được với tài khoản mẫu, hiển thị sản phẩm và thêm được vào giỏ.
6. Với CI, tạo môi trường kiểm thử từ đầu, chờ ứng dụng sẵn sàng và chạy cùng bộ dữ liệu chuẩn. Cấu hình CI được kiểm tra sau khi bộ test chạy được ở local.

### 7.2. Bộ dữ liệu mẫu

Các giá trị dưới đây là dữ liệu giả lập để thiết kế test, không phải giới hạn kinh doanh của ShopMee.

| Nhóm dữ liệu | Dữ liệu dự kiến | Mục đích |
|---|---|---|
| Tài khoản | KH_A, KH_B và một email đã đăng ký | Đăng nhập, email trùng và quyền sở hữu |
| Sản phẩm SP_A | Đơn giá 100.000 đồng, tồn 10 | Giỏ hàng thông thường và kiểm tra tổng tiền |
| Sản phẩm SP_B | Đơn giá 75.000 đồng, tồn 1 | Giá trị biên tồn kho và hai phiên đặt đồng thời |
| Sản phẩm SP_C | Đơn giá 40.000 đồng, tồn 0 | Kiểm tra sản phẩm hết hàng |
| Giỏ mẫu | 2 SP_A và 1 SP_B | Tổng tiền hàng mong đợi là 275.000 đồng |
| Đơn hàng | Các đơn thuộc KH_A/KH_B ở trạng thái cần kiểm tra | Xem đơn, quyền hủy và chuyển trạng thái |
| Dữ liệu không hợp lệ | Rỗng, chỉ khoảng trắng, email sai định dạng, số lượng âm/0/thập phân/vượt tồn | EP/BVA và kiểm tra phía máy chủ |

Mỗi ca làm thay đổi giỏ, đơn hoặc tồn kho phải mô tả dữ liệu ban đầu và cách đưa dữ liệu về trạng thái chuẩn. Với RR12, chỉ chấp nhận số đơn và tồn kho cuối phù hợp số hàng sẵn có; cách hiển thị thông báo và xử lý yêu cầu bị từ chối cần được chốt trong đặc tả.

## 8. Quản lý ca kiểm thử và thực thi

### 8.1. Nội dung một ca kiểm thử

Mỗi ca có tối thiểu: mã ca, yêu cầu liên quan, rủi ro, kỹ thuật thiết kế, mức ưu tiên, tiền điều kiện, dữ liệu, bước thực hiện, kết quả mong đợi, kết quả thực tế, trạng thái, người chạy, tag/commit, ngày chạy, minh chứng và mã lỗi nếu có.

Quy ước mã dự kiến:

- Yêu cầu: `SM-REQ-F01-xx` đến `SM-REQ-F05-xx`.
- Ca chức năng: `SM-F01-001` đến `SM-F05-020`, đánh số trong từng nhóm theo phân bổ tại mục 3.
- Ca unit: `SM-UT-001` đến `SM-UT-020`.
- Kịch bản tự động: `UI01` đến `UI10`.
- Lỗi: liên kết trực tiếp tới số Issue trong kho GitHub của nhóm.

Trạng thái ca gồm **Chưa chạy**, **Đạt**, **Không đạt**, **Bị chặn** và **Chờ đặc tả**. Ca chỉ được ghi Đạt khi kết quả thực tế phù hợp kết quả mong đợi đã chốt và có đủ bằng chứng cần thiết.

### 8.2. Trình tự thực hiện

1. Rà soát yêu cầu, điều kiện môi trường, dữ liệu và RTM.
2. Chạy kiểm tra nhanh; nếu đạt, thực hiện unit test và các ca P1 về đặt hàng, tổng tiền, tồn kho và quyền truy cập.
3. Chạy các ca P2 và hoàn thành vòng thực thi bộ 80 ca. Ghi kết quả ngay sau mỗi ca.
4. Tạo Issue cho sai lệch tái hiện được; phân loại lỗi, liên kết minh chứng và chuyển người phụ trách xử lý.
5. Sau sửa, chạy lại ca lỗi để xác nhận, rồi chạy hồi quy các chức năng bị ảnh hưởng và bộ UI đã chọn.
6. Chạy bộ kiểm thử trên CI, đối chiếu kết quả, tổng hợp số liệu và rủi ro còn lại.

Mỗi ca được ít nhất một thành viên khác rà soát trước khi dùng chính thức. Khi đổi yêu cầu hoặc mã nguồn, nhóm kiểm tra lại RTM, kết quả mong đợi và danh sách ca cần chạy lại.

## 9. Điều kiện bắt đầu, tạm dừng và kết thúc

### 9.1. Điều kiện bắt đầu

- Phạm vi và các quy tắc dùng để kết luận ca đã được thống nhất; câu hỏi còn mở có người phụ trách.
- Có mã nguồn/tag, hướng dẫn cài đặt, môi trường hoạt động và dữ liệu mẫu khôi phục được.
- Các ca của vòng chạy đã được rà soát, có kết quả mong đợi và liên kết RTM.
- Kiểm tra nhanh đạt; tài khoản và quyền dùng trong ca đã sẵn sàng.

### 9.2. Tạm dừng và chạy lại

Tạm dừng nhóm ca bị ảnh hưởng khi ứng dụng không khởi động, đăng nhập hoặc luồng đặt hàng nền tảng bị chặn, dữ liệu không thể khôi phục, hoặc thiếu đặc tả khiến không xác định được kết quả mong đợi. Những ca độc lập với sự cố có thể tiếp tục.

Tiếp tục sau khi nguyên nhân đã được xử lý, dữ liệu chuẩn được nạp lại và kiểm tra nhanh liên quan đạt. Ghi rõ bản phần mềm mới và chạy lại các ca có thể bị ảnh hưởng.

### 9.3. Tiêu chí kết thúc dự kiến

| Nội dung | Điều kiện đề xuất |
|---|---|
| Truy vết | 100% yêu cầu trong phạm vi có ca liên quan và kết quả trong RTM |
| Thực thi chức năng | 80/80 ca đã chạy; không còn ca Bị chặn hoặc Chờ đặc tả |
| Kết quả chức năng | Ít nhất 95% số ca đạt, tương đương tối thiểu 76/80; toàn bộ ca P1 phải đạt |
| Hộp trắng | Có phân tích 2 hàm từ mã nguồn thực tế, CFG, V(G), đường đi độc lập và bằng chứng bao phủ theo mục 6.2 |
| Unit test | 20/20 ca đạt; tăng thêm nếu cần đáp ứng bao phủ |
| Hồi quy tự động | 10/10 kịch bản UI đạt trên bản chốt; lưu kết quả local/CI và điều tra sai khác |
| Lỗi | Không còn lỗi S1/S2 mở; lỗi mức thấp hơn và ca chưa đạt còn lại có lý do, ảnh hưởng và quyết định chấp nhận được ghi rõ |
| Hồ sơ | Có báo cáo lỗi thực tế, minh chứng, nhật ký, báo cáo tổng kết và các điểm chưa giải quyết |

Tỷ lệ ca đạt = số ca Đạt / 80 × 100% cho bộ ca chức năng đã chốt. Mức 95% là đề xuất quản lý của bản nháp, không phải ngưỡng được xác nhận trong tài liệu môn học. Nếu chưa đạt điều kiện, báo cáo nêu rõ tiêu chí thiếu và kế hoạch xử lý; không kết luận hoàn thành chỉ dựa vào tỷ lệ chung.

## 10. Quản lý lỗi và báo cáo tiến độ

### 10.1. Thông tin báo cáo lỗi

Một Issue cần có tiêu đề cụ thể, bản phần mềm, môi trường, mã ca, tiền điều kiện, dữ liệu, bước tái hiện, kết quả mong đợi, kết quả thực tế, mức nghiêm trọng, ưu tiên xử lý, người phát hiện, người phụ trách và ảnh/log đi kèm.

| Mức | Cách phân loại dự kiến | Ví dụ ảnh hưởng |
|---|---|---|
| S1 – Nghiêm trọng | Mất toàn vẹn dữ liệu nghiêm trọng hoặc lộ/truy cập trái phép dữ liệu khách khác | Xem/hủy được đơn người khác; dữ liệu đơn bị hỏng không thể phục hồi bằng thao tác thông thường |
| S2 – Cao | Chặn luồng chính hoặc làm sai tiền, đơn, tồn kho | Không đặt được đơn hợp lệ, tổng tiền sai, bán vượt tồn |
| S3 – Trung bình | Sai lệch chức năng nhưng vẫn có cách tiếp tục công việc | Tìm kiếm hoặc lọc sai trong một số tình huống |
| S4 – Thấp | Lỗi trình bày hoặc thông báo ít ảnh hưởng nghiệp vụ | Sai nhãn hoặc căn chỉnh giao diện |

Ưu tiên ca P1/P2 và mức nghiêm trọng lỗi S1–S4 là hai khái niệm khác nhau. Mức lỗi được đánh giá theo hậu quả thực tế khi tái hiện, không gán chỉ từ điểm rủi ro dự đoán.

Luồng xử lý đề xuất: **Mới → Đã xác nhận → Đang sửa → Chờ kiểm thử lại → Đóng**. Nếu vẫn tái hiện, chuyển **Mở lại**. Issue trùng hoặc không đủ căn cứ cần ghi lý do và liên kết thông tin đối chiếu.

### 10.2. Theo dõi tiến độ

Cuối mỗi buổi làm việc, thành viên cập nhật số ca đã thiết kế, đã chạy, Đạt/Không đạt/Bị chặn/Chờ đặc tả, số lỗi mở theo mức nghiêm trọng, kết quả unit/UI và trở ngại cần xử lý. Thái tổng hợp, đối chiếu với kế hoạch và thống nhất ưu tiên cho buổi tiếp theo.

## 11. Phân công nhân sự

Phân công dưới đây là dự kiến. Mỗi thành viên đều tham gia thiết kế ca, thực thi và lưu minh chứng, ngoài nhiệm vụ phụ trách chính.

| Thành viên | MSSV | Nhiệm vụ phụ trách | Phân bổ ca chức năng dự kiến |
|---|---|---|---|
| Đổng Quốc Thái | 50.01.104.143 | Điều phối, chốt yêu cầu, kế hoạch, rủi ro, tổng hợp báo cáo và rà soát lỗi | 12 ca F01 + 8 ca F02 = 20 |
| Trần Nguyễn Xuân Sơn | 50.01.104.135 | Thiết kế hộp đen, EP/BVA, bảng quyết định/chuyển trạng thái và RTM | 8 ca F02 + 12 ca F03 = 20 |
| Nguyễn Hoàng Long | 50.01.104.085 | Phân tích 2 hàm hộp trắng, viết 20 unit test, hỗ trợ kiểm tra dữ liệu và tồn kho | 20 ca F04 |
| Đặng Nhật Tinh | 50.01.104.162 | Xây dựng 10 kịch bản UI, cấu hình CI, tổ chức minh chứng và theo dõi Issue | 20 ca F05 |

Các ca F05 về quyền sở hữu, đồng thời và lỗi ghi dữ liệu cần Long/Thái hỗ trợ Tinh. Sơn hỗ trợ rà soát thiết kế ca của cả nhóm. Công việc sửa mã nguồn được phân theo phần ứng dụng người thực hiện nắm rõ; kết quả sửa cần thành viên khác kiểm thử lại.

## 12. Lịch thực hiện dự kiến

Giả định thời lượng 3 tuần làm việc, khoảng 8 giờ/người/tuần, tổng 96 giờ-người. Đây là ước lượng cần cập nhật ở C05, không phải lịch đã được nhóm xác nhận. Các đầu việc được triển khai song song khi đủ điều kiện.

| Giai đoạn | Thời điểm tương đối | Công việc và đầu ra chính | Người phụ trách |
|---|---|---|---|
| Chuẩn bị | Tuần 1, ngày 1–2 | Chốt C01–C05, phạm vi, bản phần mềm, môi trường, quy tắc và dữ liệu chuẩn | Thái, cả nhóm |
| Thiết kế | Tuần 1, ngày 3–5 | Thiết kế 80 ca, RTM, dữ liệu, danh sách P1/P2; chọn 2 hàm và 10 kịch bản UI | Sơn, Long, Tinh |
| Kiểm thử ưu tiên | Tuần 2, ngày 6–8 | Phân tích hộp trắng, chạy unit; thực thi ca P1; ghi và xử lý lỗi sớm | Long, cả nhóm |
| Hoàn thành vòng đầu | Tuần 2, ngày 9–10 | Chạy đủ bộ 80 ca lần đầu, cập nhật RTM và Issue; hoàn thiện script UI | Cả nhóm |
| Sửa và kiểm thử lại | Tuần 3, ngày 11–12 | Xác nhận lỗi đã sửa, chạy lại ca liên quan, hoàn thiện CI và minh chứng | Tinh, cả nhóm |
| Hồi quy | Tuần 3, ngày 13 | Chạy unit, 10 UI và bộ ca hồi quy theo ảnh hưởng thay đổi; rà tiêu chí kết thúc | Long, Tinh, Sơn |
| Tổng kết | Tuần 3, ngày 14 | Thống kê kết quả, lỗi còn mở, rủi ro còn lại, hoàn thiện báo cáo | Thái, cả nhóm |
| Dự phòng | Tuần 3, ngày 15 | Xử lý ca bị chặn, kiểm tra hồ sơ và thống nhất bản nộp | Cả nhóm |

## 13. Rủi ro thực hiện kế hoạch

Đây là rủi ro của hoạt động kiểm thử, tách với rủi ro sản phẩm trong mục 5.

| Rủi ro | Ảnh hưởng | Cách xử lý dự kiến |
|---|---|---|
| Mã nguồn hoặc đặc tả chưa chốt | Ca bị sửa nhiều, kết quả mong đợi không thống nhất | Chốt bản phần mềm; quản lý C01–C03; đánh giá lại ca khi có thay đổi |
| PHPUnit chưa được chấp thuận hoặc không tương thích | Không chạy/nộp được unit test theo yêu cầu | Xử lý C04 sớm và kiểm tra một ca mẫu trước khi viết đủ bộ |
| Dữ liệu không được khôi phục giữa các ca | Kết quả phụ thuộc thứ tự chạy, sai số tồn kho | Dùng dữ liệu chuẩn, mô tả reset và tách dữ liệu giữa các phiên chạy |
| Không tạo được tình huống đồng thời hoặc lỗi ghi dữ liệu | Bỏ sót RR07/RR12 dù các luồng thông thường đạt | Chuẩn bị sớm hai phiên và cách mô phỏng lỗi có kiểm soát trong môi trường test |
| Thay đổi giao diện khiến script UI thất bại | Mất thời gian sửa script, khó phân biệt lỗi test với lỗi ứng dụng | Dùng bộ chọn ổn định, chờ điều kiện rõ ràng và phân tích log/ảnh trước khi kết luận |
| Thiếu thời gian hoặc thành viên bận | Không đủ ca, minh chứng hoặc báo cáo | Theo dõi mỗi buổi, ưu tiên P1, chia lại công việc và giữ ngày dự phòng |
| Số lỗi thực tế ít hơn định mức báo cáo | Hồ sơ chưa đáp ứng số lượng yêu cầu | Rà ca âm và kiểm thử khám phá trong phạm vi; ghi đúng số lỗi thực tế và xin hướng dẫn giảng viên |

## 14. Hồ sơ bàn giao và cập nhật kế hoạch

Hồ sơ dự kiến gồm:

1. Kế hoạch kiểm thử này và lịch sử thay đổi.
2. Đặc tả yêu cầu/quy tắc đã chốt, bộ 80 ca và RTM.
3. Bộ dữ liệu mẫu, hướng dẫn cài đặt và khôi phục môi trường.
4. Phân tích hộp trắng 2 hàm và kết quả ít nhất 20 ca unit test.
5. 10 kịch bản UI, cấu hình CI và kết quả thực thi trên bản chốt.
6. Báo cáo lỗi, ảnh/log minh chứng và kết quả kiểm thử lại.
7. Báo cáo tổng kết, thống kê tiêu chí hoàn thành và rủi ro còn lại.
8. Bảng phản biện AI của Thực hành 3.2 để lưu phụ lục “Sử dụng AI”.

| Phiên bản | Ngày | Nội dung |
|---|---|---|
| 0.1 | 03/11/2026 | Lập kế hoạch nháp theo phiếu đăng ký và bảng rủi ro hiện tại; lịch, tiêu chí hoàn thành và phân bổ ca chờ nhóm thống nhất |

Nhóm cập nhật kế hoạch khi thay đổi phạm vi, quy tắc nghiệp vụ, bản phần mềm, nguồn lực hoặc thời hạn. Mọi thay đổi cần ghi ảnh hưởng đến ca kiểm thử, RTM, lịch và kết quả đã có.
