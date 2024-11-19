mô hình quản lí bán hàng 




CREATE DATABASE QLBH

CREATE TABLE KHACHHANG

(

MaKhachHang INT

CONSTRAINT PK_KHACHHANG_MaKhachHang PRIMARY KEY,

TenCongTy NVARCHAR(50),

TenGiaoDich NVARCHAR(20),

DiaChi NVARCHAR(50),

 

Email VARCHAR(30),

DienThoai VARCHAR(15),

Fax VARCHAR(15),

)

CREATE TABLE NHACUNGCAP

(

MaCongTy CHAR(3)

CONSTRAINT PK_NHACUNGCAP_MaCongTy PRIMARY KEY(MaCongTy),

TenCongTy NVARCHAR(50),

TenGiaoDich NVARCHAR(20),

DiaChi NVARCHAR(50),

DienThoai VARCHAR(15),

Fax VARCHAR(15),

Email VARCHAR(30),

)

CREATE TABLE LOAIHANG

(

MaLoaiHang CHAR(2)

CONSTRAINT PK_LOAIHANG_MaLoaiHang PRIMARY KEY(MaLoaiHang),

TenLoaiHang NVARCHAR(30),

)

CREATE TABLE MATHANG

(

MaHang CHAR(4)

CONSTRAINT PK_MATHANG_MaHang PRIMARY KEY(MaHang),

TenHang NVARCHAR(30),

MaCongTy CHAR(3),

MaLoaiHang CHAR(2),

SoLuong INT,

DonViTinh NVARCHAR(10),

GiaHang NUMERIC(10,2),

CONSTRAINT FK_MATHANG_MaLoaiHang FOREIGN KEY(MaLoaiHang)

REFERENCES LOAIHANG(MaLoaiHang)

ON DELETE CASCADE

ON UPDATE CASCADE,

CONSTRAINT FK_MATHANG_MaCongTy FOREIGN KEY(MaCongTy)

REFERENCES NHACUNGCAP(MaCongTy)

ON DELETE CASCADE

ON UPDATE CASCADE,

)

CREATE TABLE NHANVIEN

(

MaNhanVien CHAR(4)

CONSTRAINT PK_NHANVIEN_MaKhachHang PRIMARY KEY,

Ho NVARCHAR(40),

Ten NVARCHAR(10),

NgaySinh DATETIME,

NgayLamViec DATETIME,

DiaChi NVARCHAR(60),

DienThoai VARCHAR(15),

LuongCoBan NUMERIC(10,2),

 

PhuCap NUMERIC(10,2),

)

CREATE TABLE DONDATHANG

(

SoHoaDon INT

CONSTRAINT PK_DONDATHANG_SoHoaDon PRIMARY KEY,

MaKhachHang INT,

MaNhanVien CHAR(4),

NgayDatHang DATETIME,

NgayGiaoHang DATETIME,

NgayChuyenHang DATETIME,

NoiGiaoHang NVARCHAR(80),

CONSTRAINT FK_DONDATHANG_MaKhachHang FOREIGN KEY(MaKhachHang)

REFERENCES KHACHHANG(MaKhachHang)

ON DELETE CASCADE

ON UPDATE CASCADE,

CONSTRAINT FK_DONDATHANG_MaNhanVien FOREIGN KEY(MaNhanVien)

REFERENCES NHANVIEN(MaNhanVien)

ON DELETE CASCADE

ON UPDATE CASCADE,

)

CREATE TABLE CHITIETDATHANG

(

SoHoaDon INT,

MaHang CHAR(4),

GiaBan NUMERIC(10,2),

SoLuong INT,

MucGiamGia NUMERIC(10,2),

CONSTRAINT  PK_CHITIETDATHANG_SoHoaDon_MaHang PRIMARY KEY(SoHoaDon,

MaHang),

CONSTRAINT  FK_CHITIETDATHANG_SoHoaDon FOREIGN KEY(SoHoaDon)

REFERENCES DONDATHANG(SoHoaDon)

ON DELETE CASCADE

ON UPDATE CASCADE,

CONSTRAINT  FK_CHITIETDATHANG_MaHang FOREIGN KEY(MaHang)

REFERENCES MATHANG(MaHang)

ON DELETE CASCADE

ON UPDATE CASCADE,

)

NSERT INTO LOAIHANG VALUES('TP', N'Thực phẩm');

INSERT INTO LOAIHANG VALUES('DT', N'Ðiện tử');

INSERT INTO LOAIHANG VALUES('MM', N'May mặc');

INSERT INTO LOAIHANG VALUES('NT', N'Nội thất');

INSERT INTO LOAIHANG VALUES('DC', N'Dụng cụ học tập');

INSERT INTO KHACHHANG VALUES(1, N'Công ty sữa Việt Nam', 'VINAMILK',

N'Hà Nội', 'vinamilk@vietnam.com', '04-891135', '');

INSERT INTO KHACHHANG VALUES(2, N'Công ty may mặc Việt Tiến',

'VIETTIEN', N'Sài Gòn', 'viettien@vietnam.com','08-808803','');

'Quy Nhơn','', 11000000, 0);

INSERT INTO NHANVIEN VALUES('P001', N'Nguyễn Hoài', N'Phong',

'06/14/1986', '03/01/2009', N'Quy Nhơn','056-891135', 13000000, 0);

INSERT INTO NHANVIEN VALUES('Q001', N'Trương Thị Thế', N'Quang',

'06/17/1987', '03/01/2009', N'Ayunpa','0979-792176', 10000000, 500000);

INSERT INTO NHANVIEN VALUES('T001', N'Nguyễn Đức', N'Thắng',

'09/13/1984', '03/01/2009', N'Phù Mỹ', '0955-593893', 1200000,0);

INSERT INTO NHANVIEN VALUES('D001', N'Nguyễn Minh', N'Đăng',

'12/29/1987', '03/01/2009', N'Quy Nhơn','0905-779919', 14000000, 0);

INSERT INTO NHANVIEN VALUES('M001', N'Hồ Thị Phương', N'Mai',

'09/14/1987', '03/01/2009', N'Tây Sơn','', 9000000, 500000);

INSERT INTO NHACUNGCAP VALUES('VNM', N'Công ty sữa Việt Nam',

'VINAMILK', N'Hà Nội', '04-891135', '', 'vinamilk@vietnam.com');

INSERT INTO NHACUNGCAP VALUES('MVT', N'Công ty may mặc Việt Tiến',

'VIETTIEN', N'Sài Gòn', '08-808803', '', 'viettien@vietnam.com');

INSERT INTO NHACUNGCAP VALUES('SCM', N'Siêu thị Coop-mart', 'COOPMART',

N'Quy Nhơn', '056-888666', '', 'coopmart@vietnam.com');

INSERT INTO NHACUNGCAP VALUES('DQV', N'Công ty máy tính Quang Vũ',

'QUANGVU', N'Quy Nhơn', '056-888777', '', 'quangvu@vietnam.com');

INSERT INTO NHACUNGCAP VALUES('DAF', N'Nội thất Đài Loan Dafuco',

'DAFUCO', N'Quy Nhơn', '056-888111', '', 'dafuco@vietnam.com');

INSERT INTO NHACUNGCAP VALUES('GOL', N'Công ty sản xuất dụng cụ học sinh

Golden', 'GOLDEN', N'Quy Nhơn', '056-891135', '', 'golden@vietnam.com');

INSERT INTO MATHANG VALUES('TP01', N'Sửa hộp XYZ', 'VNM', 'TP', 10,

N'Hộp', 4000);

INSERT INTO MATHANG VALUES('TP02', N'Sửa XO', 'VNM', 'TP', 12, N'Hộp',

180000);

INSERT INTO MATHANG VALUES('TP03', N'Sửa tươi Vinamilk không đường',

'VNM', 'TP', 5000, N'Hộp', 3500);

INSERT INTO MATHANG VALUES('TP04', N'Táo', 'SCM', 'TP', 12, N'Ký',

12000);

INSERT INTO MATHANG VALUES('TP05', N'Cà chua', 'SCM', 'TP', 15, N'Ký',

5000);

DT04', N'Tivi LCD', 'DQV', 'DT', 10, N'Cái',

20000000);

INSERT INTO MATHANG VALUES('DT05', N'Máy tính xách tay NEC', 'DQV',

'DT', 60, N'Cái', 18000000);

INSERT INTO MATHANG VALUES('NT01', N'Bàn ghế ăn', 'DAF', 'NT', 20,

N'Bộ', 1000000);

INSERT INTO MATHANG VALUES('NT02', N'Bàn ghế Salon', 'DAF', 'NT', 20,

N'Bộ', 150000);

INSERT INTO MATHANG VALUES('DC01', N'Vở học sinh cao cấp', 'GOL', 'DC',

20000 , N'Ram', 48000);

INSERT INTO MATHANG VALUES('DC02', N'Viết bi học sinh', 'GOL', 'DC',

2000 , N'Cây', 2000);

INSERT INTO MATHANG VALUES('DC03', N'Hộp màu tô', 'GOL', 'DC', 2000 ,

N'Hộp', 7500);

INSERT INTO MATHANG VALUES('DC04', N'Viết mực cao cấp', 'GOL', 'DC',

2000 , N'Cây', 20000);

INSERT INTO MATHANG VALUES('DC05', N'Viết chì 2B', 'GOL', 'DC', 2000 ,

N'Cây', 3000);

INSERT INTO MATHANG VALUES('DC06', N'Viết chì 4B', 'GOL', 'DC', 2000 ,

N'Cây', 6000);

INSERT INTO DONDATHANG VALUES(1, 1, 'A001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Hà Nội');

INSERT INTO DONDATHANG VALUES(2, 1, 'H001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Hà Nội');

INSERT INTO DONDATHANG VALUES(3, 2, 'H002', '09/20/2007', '10/01/2007',

'10/01/2007', N'Sài Gòn');

INSERT INTO DONDATHANG VALUES(4, 3, 'H003', '09/20/2007', '10/01/2007',

'10/01/2007', N'Sài Gòn');

INSERT INTO DONDATHANG VALUES(5, 4, 'P001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Hà Nội');

INSERT INTO DONDATHANG VALUES(6, 5, 'D001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Hà Nội');

INSERT INTO DONDATHANG VALUES(7, 6, 'M001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Hà Nội');

INSERT INTO DONDATHANG VALUES(8, 2, 'Q001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Sài Gòn');

INSERT INTO DONDATHANG VALUES(9, 3, 'T001', '09/20/2007', '10/01/2007',

'10/01/2007', N'Sài Gòn');

 

INSERT INTO CHITIETDATHANG VALUES(9, 'DC01', 48000, 1000, 0);

INSERT INTO CHITIETDATHANG VALUES(9, 'DC02', 2000, 1000, 0);

INSERT INTO CHITIETDATHANG VALUES(9, 'DC03', 7500, 1000, 0);

INSERT INTO CHITIETDATHANG VALUES(8, 'DT04', 20000000, 2, 1000000);

INSERT INTO CHITIETDATHANG VALUES(7, 'TP03', 3000, 200, 0);

INSERT INTO CHITIETDATHANG VALUES(4, 'MM01', 340000, 80, 10000);

INSERT INTO CHITIETDATHANG VALUES(5, 'TP03', 3000, 1000, 0);

INSERT INTO CHITIETDATHANG VALUES(6, 'DT05', 18000000, 20, 1000000);

INSERT INTO CHITIETDATHANG VALUES(6, 'DT01', 3100000, 2, 100000);

INSERT INTO CHITIETDATHANG VALUES(3, 'MM01', 340000, 30, 10000);

INSERT INTO CHITIETDATHANG VALUES(3, 'MM02', 500000, 30, 20000);

INSERT INTO CHITIETDATHANG VALUES(2, 'MM02', 500000, 20, 20000);

INSERT INTO CHITIETDATHANG VALUES(2, 'MM01', 340000, 30, 10000);

INSERT INTO CHITIETDATHANG VALUES(1, 'TP01', 4000, 5, 0);

INSERT INTO CHITIETDATHANG VALUES(1, 'TP02', 180000, 5, 5000);

INSERT INTO CHITIETDATHANG VALUES(1, 'TP03', 12000, 5, 0);

INSERT INTO CHITIETDATHANG VALUES(1, 'TP06', 3000, 50, 0);

INSERT INTO CHITIETDATHANG VALUES(1, 'TP07', 40000,100, 0);

Sử dụng câu lệnh SELECT để thực hiện các yêu cầu sau:

1. Cho biết danh sách các đối tác cung cấp hàng cho công ty

2. Mã hàng, tên hàng và số lượng của các mặt hàng hiện có trong công ty

3. Họ tên, địa chỉ và năm bắt đầu làm việc của các nhân viên trong cty

4. Địa chỉ, điện thoại của nhà cung cấp có tên giao dịch VINAMILK

5. Mã và tên của các mặt hàng có giá trị lớn hơn 100000 và số lượng hiện có ít hơn 50

6. Cho biết mỗi mặt hàng trong công ty do ai cung cấp

7. Công ty Việt Tiến đã cung cấp những mặt hàng nào

8. Loại hàng thực phẩm do những công ty nào cung cấp, địa chỉ của công ty đó

9. Những khách hàng nào (tên giao dịch) đã đặt mua mặt hàng sữa hộp của công ty

10.Đơn đặt hàng số 1 do ai đặt và do nhân viên nào lập, thời gian và địa điểm giao hàng là ở đâu

11. Hãy cho biết số tiền lương mà công ty phải trả cho mỗi nhân viên là bao nhiêu (lương=lương

cơ bản+phụ cấp)

12.Trong đơn đặt hàng số 3 đặt mua những mạt hàng nào và số tiền mà khách hàng phải trả cho

mỗi mặt hàng là bao nhiêu(số tiền phải trả=số lượng x giá bán – số lượng x giá bán x mức

giảm giá/100)

13.Hãy cho biết có những khách hàng nào lại chính là đối tác cung cấp hàng cho công ty (tức là

có cùng tên giao dịch)

14.Trong công ty có những nhân viên nào có cùng ngày sinh

15.Những đơn hàng nào yêu cầu giao hàng ngay tại công ty đặt hàng và những đơn đó là của

công ty nào

 

của  khách  hàng  trùng  với  tên  công  ty  và  tên  giao  dịch  của  một  nhà cung cấp nào đó thì

địa chỉ, điện thoại, fax và e-mail phải giống nhau.

37. Tăng  lương  lên  gấp  rưỡi  cho  những  nhân  viên  bán  được  số  lượng  hàng  nhiều hơn 100

trong năm 2003.

38. Tăng phụ cấp lên bằng 50% lương cho những nhân viên bán được hàng nhiều nhất.

39. Giảm  25%  lương  của  những  nhân  viên  trong  năm  2003  không  lập  được  bất  kỳ đơn đặt

hàng nào.

40. Giả  sử  trong  bảng  DONDATHANG  có  thêm  trường  SOTIEN  cho  biết  số  tiền mà khách

hàng phải trả trong mỗi đơn đặt hàng. Hãy tính giá trị cho trường này.

Thực hiện các yêu cầu dưới đây bằng câu lệnh DELETE.

41. Xoá khỏi bảng NHANVIEN những nhân viên đã làm việc trong công ty quá 40 năm.

42. Xoá những đơn đặt hàng trước năm 2000 ra khỏi cơ sở dữ liệu.

43. Xoá khỏi bảng LOAIHANG những loại hàng hiện không có mặt hàng.

44. Xoá khỏi bảng KHACHHANG những khách hàng hiện không có bất kỳ đơn đặt hàng nào

cho công ty.

45. Xoá khỏi bảng MATHANG những mặt hàng có số lượng bằng 0 và không được đặt mua

trong bất kỳ đơn đặt hàng nào

 

----------------- Đáp án admin donghanhcungtester.com hoàn thành ------------------

 

-- 1. Cho biết danh sách các đối tác cung cấp hàng cho công ty

ĐÁP ÁN: SELECT * FROM qlbhdt.nhacungcap;

-- 2. Mã hàng, tên hàng và số lượng của các mặt hàng hiện có trong công ty

ĐÁP ÁN: SELECT MaHang, TenHang, SoLuong FROM qlbhdt.mathang;

-- 3. Họ tên, địa chỉ và năm bắt đầu làm việc của các nhân viên trong cty--

ĐÁP ÁN: SELECT Ho, Ten, DiaChi, year(ngaylamviec) FROM qlbhdt.nhanvien;

-- 4. Địa chỉ, điện thoại của nhà cung cấp có tên giao dịch VINAMILK

ĐÁP ÁN: SELECT DiaChi, DienThoai, TenGiaoDich FROM qlbhdt.nhacungcap where TenGiaoDich = "VINAMILK";

-- 5. Mã và tên của các mặt hàng có giá trị lớn hơn 100000 và số lượng hiện có ít hơn 50

ĐÁP ÁN: select MaHang, TenHang from qlbhdt.mathang where GiaHang > 100000 and SoLuong < 50;

-- 6. Cho biết mỗi mặt hàng trong công ty do ai cung cấp

ĐÁP ÁN: select mh.TenHang, ncc.MaCongTy, ncc.TenCongTy  from qlbhdt.nhacungcap as ncc, qlbhdt.mathang as mh where ncc.MaCongTy = mh.MaCongTy order by mh.TenHang;

-- 7. Công ty Việt Tiến đã cung cấp những mặt hàng nào

ĐÁP ÁN: select mh.TenHang, ncc.MaCongTy, ncc.TenCongTy  from qlbhdt.nhacungcap as ncc inner join  qlbhdt.mathang as mh on ncc.MaCongTy = mh.MaCongTy

where ncc.TenCongTy = "Công ty may mặc Việt Tiến";

-- 8. Loại hàng thực phẩm do những công ty nào cung cấp, địa chỉ của công ty đó

ĐÁP ÁN: select distinct lh.TenLoaiHang, ncc.TenCongTy, ncc.DiaChi from qlbhdt.loaihang lh inner join qlbhdt.mathang mh on lh.MaLoaiHang = mh.MaLoaiHang inner join qlbhdt.nhacungcap ncc on mh.MaCongTy = ncc.MaCongTy

where lh.TenLoaiHang = "Thực phẩm";

-- 9. Những khách hàng nào (tên giao dịch) đã đặt mua mặt hàng sữa hộp của công ty

ĐÁP ÁN: select nv.Ten, mh.TenHang from qlbhdt.mathang as mh inner join qlbhdt.chitietdathang as ctddh on mh.MaHang = ctddh.MaHang

inner join qlbhdt.dondathang as ddh on ctddh.SoHoaDon = ddh.SoHoaDon inner join qlbhdt.nhanvien as nv on ddh.MaNhanVien = nv.MaNhanVien

where mh.TenHang like '%Sửa hộp%';

 

-- 10.Đơn đặt hàng số 1 do ai đặt và do nhân viên nào lập, thời gian và địa điểm giao hàng là ở đâu

ĐÁP ÁN: select ddh.SoHoaDon, mkh.TenGiaoDich, nv.Ten tennhanvien, ddh.NgayDatHang, ddh.NgayGiaoHang, ddh.NoiGiaoHang from qlbhdt.dondathang as ddh inner join qlbhdt.nhanvien as nv on ddh.MaNhanVien = nv.MaNhanVien

inner join qlbhdt.khachhang as mkh on ddh.MaKhachHang = mkh.MaKhachHang

where ddh.SoHoaDon = '1';

-- 11. Hãy cho biết số tiền lương mà công ty phải trả cho mỗi nhân viên là bao nhiêu (lương=lương cơ bản+phụ cấp)

ĐÁP ÁN: select MaNhanVien, (LuongCoBan + PhuCap) luong from qlbhdt.nhanvien;

 

-- 12.Trong đơn đặt hàng số 3 đặt mua những mạt hàng nào và số tiền mà khách hàng phải trả cho mỗi mặt hàng là bao nhiêu(số tiền phải trả=số lượng x giá bán – số lượng x giá bán x mức giảm giá/100)

ĐÁP ÁN: select *  from qlbhdt.chitietdathang as ctddh inner join qlbhdt.mathang as mh on ctddh.MaHang = mh.MaHang where ctddh.SoHoaDon = '3';

 

select ctddh.SoHoaDon, mh.TenHang, (ctddh.SoLuong*GiaBan*(1 - MucGiamGia/100)) 

from qlbhdt.chitietdathang as ctddh inner join qlbhdt.mathang as mh on ctddh.MaHang = mh.MaHang

where ctddh.SoHoaDon = '3';

 

select ddh.SoHoaDon, mh.TenHang, ctdh.GiaBan, ctdh.SoLuong, ctdh.MucGiamGia, ((ctdh.SoLuong*GiaBan) - (ctdh.SoLuong*GiaBan*MucGiamGia/100))   from qlbhdt.dondathang ddh inner join qlbhdt.chitietdathang ctdh on ddh.SoHoaDon = ctdh.SoHoaDon inner join qlbhdt.mathang  mh on ctdh.MaHang = mh.MaHang

where ddh.SoHoaDon = '3';

 

-- 13.Hãy cho biết có những khách hàng nào lại chính là đối tác cung cấp hàng cho công ty (tức là có cùng tên giao dịch)

ĐÁP ÁN: select * from qlbhdt.nhacungcap as ncc inner join qlbhdt.khachhang as kh on ncc.TenGiaoDich = kh.TenGiaoDich;

 

-- 14.Trong công ty có những nhân viên nào có cùng ngày sinh

ĐÁP ÁN: select * from qlbhdt.nhanvien nv where exists (select NgaySinh from qlbhdt.nhanvien where nv.NgaySinh = NgaySinh and nv.MaNhanVien <> MaNhanVien);

 

-- cần đọc kỹ hơn 15.Những đơn hàng nào yêu cầu giao hàng ngay tại công ty đặt hàng và những đơn đó là của công ty nào/ của  khách  hàng  trùng  với  tên  công  ty  và  tên  giao  dịch  của  một  nhà cung cấp nào đó thì địa chỉ, điện thoại, fax và e-mail phải giống nhau.

 

ĐÁP ÁN: select distinct ncc.TenCongTy, ddh.SoHoaDon, ddh.NoiGiaoHang, ncc.DiaChi, ncc.DienThoai, ncc.Email  from qlbhdt.dondathang ddh inner join qlbhdt.chitietdathang  ctdh on ddh.SoHoaDon = ctdh.SoHoaDon

inner join qlbhdt.mathang mh on ctdh.MaHang = mh.MaHang

inner join qlbhdt.nhacungcap ncc on mh.MaCongTy = ncc.MaCongTy

where ncc.DiaChi = ddh.NoiGiaoHang;

 

-- 37. Tăng  lương  lên  gấp  rưỡi  cho  những  nhân  viên  bán  được  số  lượng  hàng  nhiều hơn 100

-trong năm 2003.

-- bước 1: tìm ra những nhân viên có số lượng đơn hàng > 100
