# Khung sườn

Khung sườn khóa luận kết thúc 6 năm luyện ngục của nvmnghia.

Độ dài yêu cầu: 40-50 trang.

## 0. Bìa & các mục liên quan

- Bìa
- Phụ bìa
- Cam đoan không sao chép
- Phê chuẩn của giảng viên hướng dẫn
- Lời cảm ơn
- Tóm tắt

    Nhờ Internet, truyền hình và điện ảnh, văn hóa truyện tranh đã trở nên phổ
    biến toàn cầu, đặc biệt là trong giới trẻ. Sự phát triển của truyện tranh
    trên trong thời đại số thúc đẩy sự phát triển của các trang web truyện
    tranh, thỏa mãn nhu cầu đọc sớm nhất có thể sau khi truyện được xuất bản.
    Tuy nhiên, nguồn truyện tranh của những trang web này có chất lượng không
    cao. Một bộ phận người đọc kĩ tính chọn đọc và lưu trữ những file truyện
    được số hóa chất lượng cao, thường ở dạng file nén đuôi `cbr` và `cbz`. Xuất
    phát từ yêu cầu này, tôi muốn viết ứng dụng yacv có thể đọc các file truyện
    nén trên điện thoại Android. Nội dung của khóa luận sẽ trình bày những đặc
    điểm cơ bản của kiến trúc ứng dụng Android - với cốt lõi là mẫu thiết kế
    MVVM - được khuyên dùng bởi Google, các tính năng trong yacv, và các ca sử
    dụng của phần mềm.

    Từ khóa: MVVM, Jetpack, Android, cbr, cbz, comic

- Mục lục
- Danh sách bảng
- Danh sách hình
- Danh sách kí hiệu, chữ viết tắt
    - MVVM

## 1. Chương 1: Giới thiệu

### 1.1 Đặt vấn đề

Hint: Tại sao lại làm đồ án ntn (1-3 đoạn)?

Tại Đông Á và Đông Nam Á, văn hóa truyện tranh gốc Á, nhất là truyện tranh Nhật
(manga), được đón nhận khá tích cực, đặc biệt trong giới trẻ. Thế hệ những người
dưới 40 tuổi hiện nay được tiếp xúc với truyện tranh từ sớm, thông qua những
cuốn truyện truyền tay và phim hoạt hình dựa trên truyện tranh, và tiếp tục đọc
dù đã qua tuổi thiếu niên. Một số tác phẩm manga còn có lượng người đọc lớn trên
toàn cầu như Doraemon, One Piece. Ở bên kia bán cầu, với sự thành công của vũ
trụ điện ảnh Marvel và DC, truyện tranh phương Tây (comic) cũng được hồi sinh
phần nào sau một thập kỷ thiếu sáng tạo và suy giảm doanh số sách in. Các bộ
truyện siêu anh hùng, vốn trước đây chỉ phổ biến ở Hoa Kỳ, nay đang trên đường
trở thành một phần của văn hóa đại chúng như vị thế của manga. Có thể nói, văn
hóa truyện tranh nói chung đang ở thời kì phát triển nhất, xét theo tiêu chí về
độ phổ biến và thái độ đón nhận của xã hội.

Hiện nay, hầu hết mọi người đọc truyện qua các trang web tổng hợp truyện tranh.
Những trang web này có hai ưu điểm chính:

- Số lượng: chỉ cần truy cập một trang là có thể đọc ít nhất hàng nghìn đầu
  truyện.
- Tốc độ: tốc độ ra truyện rất nhanh. Với các bộ truyện nổi tiếng, thường chỉ
  trong vòng một vài giờ sau khi chương mới ra mắt, bản dịch đã xuất hiện.

Tuy vậy, nhược điểm chính của những trang web này là chất lượng ảnh của truyện.
Để giảm thời gian tải và tránh tốn băng thông, hình ảnh của truyện thường được
nén khá nhiều, gây vỡ hình, mờ nhòe. Một bộ phận người đọc, hoặc kĩ tính, hoặc
muốn sưu tầm truyện, thường chọn đọc những tệp truyện chất lượng cao, thường có
đuôi `.cbz` hoặc `.cbr`. Bản chất tệp truyện này là các tệp nén zip bình thường,
bên trong có các tệp ảnh thông dụng như `.jpg`, `.png`. Tuy nhiên, do được tải
hẳn về máy rồi mới đọc, những tệp truyện này không bị giới hạn về băng thông hay
thời gian, do đó hình ảnh trong tệp có thể có chất lượng rất cao.

Trong khóa luận này, tôi viết một ứng dụng Android nhằm phục vụ số ít người dùng
có nhu cầu đọc truyện tranh chất lượng cao đã giới thiệu ở trên. Tên của ứng
dụng là "yacv", viết tắt của cụm từ tiếng Anh "Yet Another Comic Viewer", tạm
dịch là "Lại một ứng dụng xem truyện tranh nữa". Hai tính năng chính duy nhất
của ứng dụng là đọc và quản lí cơ bản (tìm kiếm, xóa) tệp truyện tranh có sẵn
trên điện thoại.

### 1.2 Ứng dụng tương tự

Hiện có nhiều ứng dụng đọc truyện tranh trên chợ ứng dụng Google Play. Hai ứng
dụng phổ biến nhất trong số này là
[ComicScreen](https://play.google.com/store/apps/details?id=com.viewer.comicscreen&hl=en&gl=US)
và [Astonishing Comic
Reader](https://play.google.com/store/apps/details?id=com.aerilys.acr.android&hl=en&gl=US).
ComicScreen là ứng dụng nổi tiếng hơn. Các tính năng của ComicScreen giống với
các tính năng của yacv, tuy nhiên ComicScreen có thêm nhiều chức năng phụ, đáng
kể nhất là khả năng đọc từ mạng FTP/SMB và khả năng sửa ảnh trong file.
Astonishing Comic Reader cũng có chức năng tương tự yacv, không hơn. Cả hai đều
miễn phí và có quảng cáo.

Một ngoại lệ đáng kể ở đây là ứng dụng mã nguồn mở
[Tachiyomi](https://github.com/tachiyomiorg/tachiyomi). Ứng dụng này có hệ thống
phần mở rộng, cho phép đọc truyện ở các trang web truyện tranh. Khi web truyện
tranh thay đổi, hoặc hỗ trợ thêm trang mới, chỉ cần tải về phần mở rộng tương
ứng ở dạng ứng dụng `.APK`. Tính năng này cùng với mô hình mã nguồn mở khiến
Tachiyomi mạnh hơn toàn bộ các ứng dụng đã có và sẽ có. Tuy nhiên, Tachiyomi lại
không thể được đưa lên Play Store, vì chính tính năng phần mở rộng đã [vi phạm
chính sách](https://github.com/tachiyomiorg/tachiyomi/issues/1745) của Play
Store.

Một điểm khác biệt quan trọng của yacv với các ứng dụng có sẵn là việc hỗ trợ
tìm kiếm metadata của tệp truyện tranh, do các ứng dụng có sẵn trên Play Store
đa số bỏ qua thông tin này trong tệp truyện. Một trong số rất ít những ứng dụng
hỗ trợ tính năng này là [Kuro
Reader](https://play.google.com/store/apps/details?id=br.com.kurotoshiro.leitor_manga&hl=en&gl=US),
tuy nhiên đây là một tính năng trả phí.

### 1.3 Kết quả đạt được

Ứng dụng có các tính năng đủ dùng theo mục đích đã đề ra:

- Đọc file truyện `.cbz`
- Tìm kiếm truyện theo metadata

Tính năng đọc tệp truyện `.cbr` hiện mới chỉ được cài đặt một phần, do khó khăn
trong việc tích hợp thư viện đọc định dạng này.

## 2. Chương 2: Kiến thức nền tảng

### 2.1. Hệ điều hành Android

#### 2.1.1. Android Jetpack

### 2.2. Ngôn ngữ lập trình Kotlin

#### 2.2.1. Coroutine

### 2.3. Mẫu thiết kế MVVM và Kiến trúc khuyên dùng bởi Google

### 2.4. SQLite

#### 2.4.1. Full-text Search

#### 2.4.2. Room

### 2.5. Định dạng tệp nén `.zip`

## 3. Chương 3: Phân tích yêu cầu & Thiết kế

(Nếu C3 ngắn quá thì gộp Thiết kế vào)

### 3.1 Yêu cầu đặt ra

2 loại yêu cầu:

- Chức năng:
- Phi chức năng: tốc độ, ổn định, mượt, dễ dùng

Dựa vào các ứng dụng đã có để đưa ra một số yêu cầu:
Ai là người dùng
Mong muốn

### 3.2 Phân tích yêu cầu

Use case (actor)

### 3.3 Thiết kế

UML, activity diagram, class diagram, sequence diagram

### 3.4 Thiết kế CSDL

### 3.5 Thiết kế giao diện

### 3.6 Tối ưu

## 4. Chương 4: Lập trình & Kiểm thử

### 4.1 Lập trình

Mô tả một số phần quan trọng trong source

### 4.2 Kiểm thử

#### 4.2.1 Unit test. E2E test, auto + manual test

#### 4.2.2 Kiểm thử phi chức năng

bench nhanh chậm

#### 4.2.3 Đánh giá người dùng

Hình ảnh sản phẩm.

## 5. Chương 5: Kết luận

1-2 trang

## 6. Tài liệu tham khảo
