# Chương 3-Bài 1. Thiết kế cơ sở dữ liệu (Database)

- Tiếp theo ta đi đến thiết kế cơ sở dữ liệu - phần quan trọng nhất của hệ thống. Giao diện dù có đẹp mà hệ thống hoạt động không tốt, không tối ưu thì quả là điều không tốt -> Trang web hay phải đảm bảo về giao diện lẫn hệ thống hoạt động bên trong chúng.

- Thiết kế cơ sở dữ liệu đơn giản để chúng ta thực hành với bài học này:

## Bảng Khách Hàng
  - Tạo bảng `khanghang`: Là người truy cập vào trang web để xem sản phẩm và đặt hàng

```khachhang
CREATE TABLE `khachhang` (
  `kh_ma` int(11) NOT NULL,
  `kh_tendangnhap` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_matkhau` varchar(255) COLLATE utf8_unicode_ci NOT NULL,
  `kh_ten` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_gioitinh` int(11) NOT NULL,
  `kh_diachi` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `kh_dienthoai` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_facebook` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_twitter` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_email` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `kh_ngaysinh` int(11) DEFAULT NULL,
  `kh_thangsinh` int(11) DEFAULT NULL,
  `kh_namsinh` int(11) NOT NULL,
  `kh_cmnd` varchar(50) COLLATE utf8_unicode_ci DEFAULT NULL,
  `kh_makichhoat` varchar(100) COLLATE utf8_unicode_ci DEFAULT NULL,
  `kh_trangthai` int(11) NOT NULL,
  `kh_quantri` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `khachhang`

```khachhang
INSERT INTO `khachhang` (`kh_ma`, `kh_tendangnhap`, `kh_matkhau`, `kh_ten`, `kh_gioitinh`, `kh_diachi`, `kh_dienthoai`, `kh_facebook`, `kh_twitter`, `kh_email`, `kh_ngaysinh`, `kh_thangsinh`, `kh_namsinh`, `kh_cmnd`, `kh_makichhoat`, `kh_trangthai`, `kh_quantri`) VALUES
(1, 'Admin', '123', 'Quản trị', 1, 'Số 01 - Lý Tự Trọng - Cần Thơ', '0912.123.567', '', '', 'admin@salomon.vn', 2, 2, 1985, NULL, NULL, 1, 1),
(2, 'Duy', 'fcea920f7412b5da7be0cf42b8c93759', 'Vo Dinh Duy', 0, 'Can Tho', '07103.273.34433', '', '', 'vdduy@ctu.edu.vn', 2, 2, 1985, '', '', 1, 0),
(3, 'linh', '7c4a8d09ca3762af61e59520943dc26494f8941b', 'LINH', 0, 'an giang', '54457775', '', '', 'linhhalinh5@gmail.com', 12, 8, 2000, '4543454', '98b48b11c8e922eac0dd772749556933cc3d5cad', 1, 0),
(4, 'A', '123', 'Nguyễn Thị A', 0, 'Số 20 - Phan Đình Phùng', '01234.234.234', '', '', 'nta@gmail.com', NULL, NULL, 1990, NULL, NULL, 1, 0),
(5, 'user', 'fcea920f7412b5da7be0cf42b8c93759', 'Nguoi dung moi', 0, 'Can Tho', '07103-273.344', '', '', 'vdduy@ctu.edu.vn', 2, 2, 1985, '', '44766fb4dd4e4977e75a9321cbc6413e', 0, 0);
```
## Bảng Nhà Sản Xuất
  - Tạo bảng `nhasanxuat`: Là nơi cung cấp hàng hóa cho sản phẩm nhập về

```nhasanxuat
CREATE TABLE `nhasanxuat` (
  `nsx_ma` int(11) NOT NULL,
  `nsx_ten` varchar(100) COLLATE utf8_unicode_ci DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `nhasanxuat`
```nhasanxuat
INSERT INTO `nhasanxuat` (`nsx_ma`, `nsx_ten`) VALUES
(1, 'Tỉnh Đồng Tháp'),
(2, 'Tỉnh An Giang'),
(3, 'Chợ Long Xuyên'),
(4, 'Chợ nổi Cái Răng Cần Thơ'),
(5, 'Chợ đầu mối Bình Dương');
```
## Bảng Hình Thức Thanh Toán
  - Tạo bảng `hinhthucthanhtoan`: Các hình thức thanh toán khi mua hàng

```hinhthucthanhtoan
CREATE TABLE `hinhthucthanhtoan` (
  `httt_ma` int(11) NOT NULL,
  `httt_ten` varchar(100) COLLATE utf8_unicode_ci NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `hinhthucthanhtoan`
```hinhthucthanhtoan
INSERT INTO `hinhthucthanhtoan` (`httt_ma`, `httt_ten`) VALUES
(1, 'Tiền Mặt'),
(2, 'PayPal'),
(3, 'ATM'),
(4, 'MOMO');
```
## Bảng Loại Sản Phẩm
  - Tạo bảng `loaisanpham`: Các sản phẩm được phân theo loại để dễ dàng kiểm soát và thống kê

```loaisanpham
CREATE TABLE `loaisanpham` (
  `lsp_ma` int(11) NOT NULL,
  `lsp_ten` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `lsp_mota` varchar(500) COLLATE utf8_unicode_ci DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `loaisanpham`
```loaisanpham
INSERT INTO `loaisanpham` (`lsp_ma`, `lsp_ten`, `lsp_mota`) VALUES
(1, 'Oranges juices', ''),
(2, 'fastfood', ''),
(3, 'vegetables', ''),
(14, 'oranges', ''),
(15, 'fresh-meat', ''),
(16, 'dried-fruits', NULL),
(17, 'drink-fruits', NULL);
```
## Bảng Khuyến Mãi
  - Tạo bảng `khuyenmai`: Sản phẩm có k

```khuyenmai
CREATE TABLE `loaisanpham` (
  `lsp_ma` int(11) NOT NULL,
  `lsp_ten` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `lsp_mota` varchar(500) COLLATE utf8_unicode_ci DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `khuyenmai`
```khuyenmai
INSERT INTO `loaisanpham` (`lsp_ma`, `lsp_ten`, `lsp_mota`) VALUES
(1, 'Oranges juices', ''),
(2, 'fastfood', ''),
(3, 'vegetables', ''),
(14, 'oranges', ''),
(15, 'fresh-meat', ''),
(16, 'dried-fruits', NULL),
(17, 'drink-fruits', NULL);
```
## Bảng Sản Phẩm
  - Tạo bảng `sanpham`: Các sản phẩm được bán

```sanpham
CREATE TABLE `sanpham` (
  `sp_ma` int(11) NOT NULL,
  `sp_ten` varchar(100) COLLATE utf8_unicode_ci NOT NULL,
  `sp_gia` decimal(12,2) DEFAULT NULL,
  `sp_giacu` decimal(12,2) DEFAULT NULL,
  `sp_mota_ngan` varchar(1000) COLLATE utf8_unicode_ci NOT NULL,
  `sp_mota_chitiet` text COLLATE utf8_unicode_ci DEFAULT NULL,
  `sp_ngaycapnhat` datetime NOT NULL,
  `sp_soluong` int(11) DEFAULT NULL,
  `sp_khoiluong` float DEFAULT NULL,
  `sp_availability` varchar(20) COLLATE utf8_unicode_ci DEFAULT NULL,
  `sp_shipping` varchar(50) COLLATE utf8_unicode_ci DEFAULT NULL,
  `sp_phantram` varchar(5) COLLATE utf8_unicode_ci DEFAULT NULL,
  `lsp_ma` int(11) NOT NULL,
  `nsx_ma` int(11) NOT NULL,
  `km_ma` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `sanpham`
```sanpham
INSERT INTO `sanpham` (`sp_ma`, `sp_ten`, `sp_gia`, `sp_giacu`, `sp_mota_ngan`, `sp_mota_chitiet`, `sp_ngaycapnhat`, `sp_soluong`, `sp_khoiluong`, `sp_availability`, `sp_shipping`, `sp_phantram`, `lsp_ma`, `nsx_ma`, `km_ma`) VALUES
(1, 'Chuối', '30.00', '31.00', 'Sản phẩm mới nhập về', 'guồn chất xơ lành mạnh, giàu kali, vitamin B6, vitamin C, chất chống oxy hóa và các phytonutrients. Chuối có nhiều loại và kích cỡ khác nhau.', '2012-12-22 11:20:30', 17, 3.1, 'in Store', '01 day shipping.', NULL, 14, 1, NULL),
(2, 'Táo', '20.00', '21.00', 'Sàn phẩm mới nhập về, ngon bổ dưỡng', 'Táo còn chứa nhiều chất xơ, chất chống oxy hóa và vitamin C nên cũng có tác dụng tăng cường miễn dịch, tăng sức đề kháng cũng như chống lão hóa, bảo vệ sức khỏe tim mạch. Táo cũng có hàm lượng polyphenol cao, có tác dụng chống oxy hóa. Chất chống oxy hóa này được tìm thấy cả trong vỏ và thịt của quả táo.', '2013-01-12 10:04:45', 100, 1.2, 'In stock', '01 day shipping.', NULL, 14, 4, NULL),
(3, 'Ổi', '15.00', '15.10', 'Dinh dưỡng của ổi tốt cho hệ tiêu hóa', 'Ổi chứa nhiều chất xơ, Vitamin C và carotenoids, do đó rất tốt đối với hệ tiêu hóa. Chất xơ có tác dụng chống táo bón, kích thích nhu động ruột và điều hòa hệ vi khuẩn trong ruột. 1 quả ổi sẽ cung cấp khoảng 12% lượng chất xơ cần thiết cho cơ thể người trưởng thành trong 1 ngày.', '2013-01-16 17:13:45', 10, 5, 'in Store', '01 day shipping.', NULL, 14, 1, 1),
(4, 'Cam', '16.00', '17.00', 'Cam là một trong những loại trái cây được sử đụng nhiều nhất trên thế giới.', 'Cam là loại quả giàu chất chống oxy hóa và chất phytochemical. Theo các nhà khoa học Anh: “Bình quân trong một trái cam có chứa khoảng 170 mg phytochemicals bao gồm các chất dưỡng da và chống lão hóa”. Chuyên gia dinh dưỡng Monique dos Santos cho biết cam được yêu thích và có lợi cho người khỏe mạnh cũng như các bệnh nhân. Cam giúp giải nhiệt, thỏa mãn cơn khát cho người có cường độ vân động cao, tăng cường hệ tiêu hóa và hệ miễn dịch của cơ thể.', '2013-01-16 17:14:55', 100, 6, 'In stock', '01 day shipping. Free pickup today', NULL, 14, 3, NULL),
(5, 'Nho', '35.00', '40.00', 'Nho là nguồn cung cấp năng lượng và vitamin dồi dào, rất tốt cho sức khỏe của chúng ta.', 'Trong trái nho chứa 75 - 85% nước, 18 - 33% đường glucose và fructose và nhiều chất cần thiết cho con người như: phlobaphene, acid galic, acid silicic, acid phosphoric, acid chanh, acid oxalic, acid folic, kali, magiê, canxi, mangan, coban, sắt và các vitamin B1, B2, B6, B12, A, C, P, K và PP cùng các enzyme.', '2013-01-17 14:18:03', 50, 3.4, 'In stock', '01 day shipping. Free pickup today', NULL, 14, 2, 2),
(6, 'Bơ', '25.00', '25.00', 'Bơ là quả của cây bơ, có tên khoa học là Persea americana', 'Chứa rất nhiều chất béo không bão hòa đơn, trái bơ có kết cấu mềm và mịn. Nó có hàm lượng chất béo cao hơn bất cứ loại trái cây nào.  Bơ có cơ cấu dinh dưỡng rất độc đáo, bao gồm chất xơ và rất nhiều vitamin, khoáng chất như vitamin B, vitamin K, kali, đồng, vitamin E và vitamin C.', '2013-01-17 14:19:10', 25, 7, 'in Store', '01 day shipping. Free pickup today', NULL, 14, 4, NULL),
(7, 'Xoài', '15.00', '16.00', 'Theo Boldsky, xoài được gọi là vua của tất cả các loại trái cây.', 'Không chỉ thơm ngon, ngọt, xoài giàu protein, chất xơ, vitamin C, A, axit folic..., mang lại nhiều lợi ích cho sức khỏe. Nhiều nghiên cứu đã chứng minh xoài có khả năng làm giảm nguy cơ béo phì, bệnh tim, tăng cường năng lượng, cải thiện trí nhớ', '2013-01-28 10:42:08', 13, 0.5, 'In stock', '01 day shipping. Free pickup today', NULL, 14, 5, NULL),
(15, 'Thịt Bò Thái Lan', '100.00', '110.00', 'Thịt bò là thịt của gia súc nuôi lấy thịt (bò nhà)', 'Thịt bò chủ yếu được cấu tạo từ protein và chứa nhiều loại chất béo với hàm lượng khác nhau.  Bảng dưới đây trình bày thông tin về tất cả các chất dinh dưỡng có trong thịt bò', '2020-05-22 00:00:00', 50, 50.3, 'in shop', '01 day shipping.', NULL, 15, 2, NULL);
```
## Bảng Hình Sản Phẩm
  - Tạo bảng `hinhsanpham`: Các hình thức thanh toán khi mua hàng

```hinhsanpham
CREATE TABLE `hinhsanpham` (
  `hsp_ma` int(11) NOT NULL,
  `hsp_tentaptin` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  `sp_ma` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `hinhsanpham`
```hinhsanpham
INSERT INTO `hinhsanpham` (`hsp_ma`, `hsp_tentaptin`, `sp_ma`) VALUES
(27, '20200616190503_an-oi-co-tac-dung-gi.jpg', 3),
(28, '20200613174500_feature-6.jpg', 6),
(29, '20200616190837_an-nho-cung-hoac-gan-luc-voi-3-thuc-pham-sau-rat-nguy-hiem.jpg', 5),
(31, '20200616192918_20200614101940_feature-7.jpg', 7),
(33, '20200616191113_5_XGNL.jpg', 4),
(41, '20200616150637_tao5.jpg', 2),
(42, '20200616150655_tao7.jpg', 2),
(43, '20200616192838_20200616183107_xoai1.jpg', 7),
(44, '20200616192850_20200616183117_xoai2.jpg', 7),
(45, '20200616192900_20200616183129_xoai3.jpg', 7),
(46, '20200616184839_chuoi1.png', 1),
(47, '20200616190530_dau-da-day-an-oi-duoc-khong-1.jpg', 3),
(48, '20200616190558_image10.jpeg', 3),
(49, '20200616190731_product-3.jpg', 3),
(50, '20200616190903_bau-bau-an-nho-duoc-khong-2018-05-20-23-21.jpeg', 5),
(51, '20200616190931_australian_table_grapes_001-11_26_07_831.jpg', 5),
(52, '20200616190944_Dau-Da-Day-An-Nho-Duoc-Khong-1.jpg', 5),
(53, '20200616191033_feature-5.jpg', 5),
(54, '20200616191141_an-cam-co-tac-dung-gi-nen-an-cam-luc-nao-tot-nhat.jpg', 4),
(55, '20200616191203_cam-ruot-do-1569650672-1569650-1932-8308-1569719105.jpg', 4),
(56, '20200616191212_Cam-Catiplus.png', 4),
(57, '20200616191308_cat-1.jpg', 4),
(58, '20200616191411_chuE1BB91i-laba-dalat-600x600.jpg', 1),
(59, '20200616191431_chuoi-xanh-15487305375672134789045-crop-1548730547070900315830.jpg', 1),
(60, '20200616191458_feature-2.jpg', 1),
(61, '20200616191534_feature-8.jpg', 2),
(62, '20200617052632_bo1.jpg', 15),
(63, '20200617052641_bo2.jpg', 15),
(64, '20200617052649_bo3.jpg', 15),
(65, '20200617052700_bo4.png', 15);
```
## Bảng Đơn Đặt Hàng
  - Tạo bảng `dondathang`: Các hình thức thanh toán khi mua hàng

```dondathang
CREATE TABLE `dondathang` (
  `dh_ma` int(11) NOT NULL,
  `dh_ngaylap` datetime NOT NULL,
  `dh_ngaygiao` datetime DEFAULT NULL,
  `dh_noigiao` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  `dh_trangthaithanhtoan` int(11) NOT NULL,
  `httt_ma` int(11) NOT NULL,
  `kh_ma` int(11) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `dondathang`
```dondathang
INSERT INTO `dondathang` (`dh_ma`, `dh_ngaylap`, `dh_ngaygiao`, `dh_noigiao`, `dh_trangthaithanhtoan`, `httt_ma`, `kh_ma`) VALUES
(1, '2013-02-21 16:45:44', '2013-02-01 00:00:00', 'Can Tho', 0, 1, 3),
(4, '2013-02-21 16:48:10', '2013-02-08 00:00:00', 'Can Tho', 0, 1, 4),
(5, '2013-02-21 16:48:59', '2013-02-09 00:00:00', 'Can Tho', 0, 1, 5),
(7, '2020-05-06 00:00:00', '2020-05-08 00:00:00', 'An Giang', 1, 1, 1);
```
## Bảng Sản Phẩm Đơn Đặt Hàng
  - Tạo bảng `sanpham_dondathang`: Các hình thức thanh toán khi mua hàng

```sanpham_dondathang
CREATE TABLE `sanpham_dondathang` (
  `sp_ma` int(11) NOT NULL,
  `dh_ma` int(11) NOT NULL,
  `sp_dh_soluong` int(11) NOT NULL,
  `sp_dh_dongia` decimal(12,2) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```
  - Thêm dữ liệu bảng `sanpham_dondathang`
```sanpham_dondathang
INSERT INTO `sanpham_dondathang` (`sp_ma`, `dh_ma`, `sp_dh_soluong`, `sp_dh_dongia`) VALUES
(1, 5, 3, '12000000.00'),
(3, 1, 1, '16.00'),
(4, 7, 1, '15.00'),
(5, 5, 2, '10990000.00'),
(7, 4, 1, '7500000.00');
```
# Bài học trước

[Bài học 4](./Chapter2/Readme-Bai3.md)

# Bài học tiếp theo

[Bài học 6](../Chapter3/Readme-Bai2.md)
