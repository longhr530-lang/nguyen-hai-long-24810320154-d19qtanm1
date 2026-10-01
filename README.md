I. PHẦN LÝ THUYẾT & CÂU HỎI NGẮN
Câu 1: Trình bày sự khác nhau giữa Value Types (Kiểu giá trị) và Reference Types (Kiểu tham chiếu) trong C# về cơ chế lưu trữ vùng nhớ (Stack vs Heap).

Trong C#, Value Types và Reference Types là hai nhóm kiểu dữ liệu có cách lưu trữ và hoạt động khác nhau.

1. Value Types (Kiểu giá trị)

Value Types là các kiểu dữ liệu mà biến lưu trực tiếp giá trị của nó. Một số kiểu thường gặp là:

int
double
float
bool
char
struct
enum

Ví dụ:

int a = 10;
int b = a;
b = 20;

Sau khi thực hiện đoạn code trên thì a vẫn bằng 10, còn b bằng 20. Điều này là do b nhận một bản sao giá trị của a, hai biến hoạt động độc lập với nhau.

Các biến cục bộ kiểu giá trị thường được lưu trên Stack. Stack có tốc độ truy cập nhanh và bộ nhớ được quản lý tự động khi hàm kết thúc.

2. Reference Types (Kiểu tham chiếu)

Reference Types là các kiểu dữ liệu mà biến không lưu trực tiếp đối tượng mà lưu một tham chiếu (địa chỉ) đến đối tượng trong vùng nhớ Heap.

Một số Reference Types thường gặp:

class
object
string
array
interface
delegate

Ví dụ:

class SinhVien
{
    public string ten;
}

SinhVien sv1 = new SinhVien();
sv1.ten = "Khoa";

SinhVien sv2 = sv1;
sv2.ten = "Nam";

Trong trường hợp này, sv1 và sv2 cùng tham chiếu đến một đối tượng trên Heap. Vì vậy khi thay đổi sv2.ten thì sv1.ten cũng thay đổi theo.

3. So sánh

Đặc điểm	Value Types	Reference Types
Lưu trữ	Lưu trực tiếp giá trị	Lưu tham chiếu đến đối tượng
Vùng nhớ thường gặp	Stack	Heap
Ví dụ	int, double, bool, struct	class, object, array, string
Khi gán biến	Tạo bản sao giá trị	Sao chép tham chiếu
Có thể có giá trị null	Không, trừ kiểu nullable	Có

Tóm lại, Value Type thường chứa trực tiếp dữ liệu, còn Reference Type chứa tham chiếu đến dữ liệu được lưu trong Heap. Tuy nhiên, cần lưu ý rằng việc một biến nằm trên Stack hay Heap còn phụ thuộc vào ngữ cảnh sử dụng và cách C# thực hiện quản lý bộ nhớ, nên không phải mọi Value Type đều luôn nằm trên Stack.

Câu 2: Tính năng Init-only Properties (init) trong C# 9/10 khác gì so với thuộc tính có set thông thường? Nêu trường hợp sử dụng thực tế.

init là tính năng được đưa vào từ C# 9, cho phép một thuộc tính chỉ được thiết lập giá trị trong quá trình khởi tạo đối tượng. Sau khi đối tượng được tạo xong thì thuộc tính đó không thể thay đổi bằng cách gán thông thường.

Ví dụ sử dụng set:

class SinhVien
{
    public string MaSV { get; set; }
}

SinhVien sv = new SinhVien();
sv.MaSV = "SV01";
sv.MaSV = "SV02";

Ở đây MaSV có thể thay đổi nhiều lần vì sử dụng set.

Nếu sử dụng init:

class SinhVien
{
    public string MaSV { get; init; }
}

SinhVien sv = new SinhVien
{
    MaSV = "SV01"
};

Sau khi khởi tạo xong, không thể thực hiện:

sv.MaSV = "SV02";

vì thuộc tính MaSV đã được khai báo bằng init.

Sự khác nhau giữa set và init:

set: Có thể gán hoặc thay đổi giá trị bất cứ lúc nào khi đối tượng còn tồn tại.
init: Chỉ được gán trong quá trình khởi tạo đối tượng, sau đó không được thay đổi.

Trường hợp sử dụng thực tế:

init phù hợp với những thông tin sau khi tạo đối tượng thì không muốn thay đổi, ví dụ:

Mã sinh viên.
Mã hóa đơn.
Mã đơn hàng.
ID của tài khoản.
Ngày tạo đối tượng.
Thông tin cấu hình.

Ví dụ:

class HoaDon
{
    public int MaHoaDon { get; init; }
    public string TenKhachHang { get; init; }
}

HoaDon hd = new HoaDon
{
    MaHoaDon = 1001,
    TenKhachHang = "Nguyen Van A"
};

Sau khi tạo hóa đơn, MaHoaDon không nên bị thay đổi. Vì vậy sử dụng init giúp hạn chế việc vô tình thay đổi dữ liệu và làm cho chương trình an toàn, dễ quản lý hơn.

Câu 3: Phân biệt sự khác nhau giữa phương thức virtual ở lớp cha và phương thức override ở lớp con khi triển khai tính Đa hình (Polymorphism).

virtual và override thường được sử dụng khi xây dựng tính đa hình (Polymorphism) trong lập trình hướng đối tượng.

1. Phương thức virtual ở lớp cha

virtual được sử dụng để khai báo một phương thức ở lớp cha mà lớp con có thể ghi đè lại cách thực hiện.

Ví dụ:

class DongVat
{
    public virtual void Keu()
    {
        Console.WriteLine("Dong vat keu");
    }
}

Phương thức Keu() được khai báo là virtual, vì vậy lớp con có thể thay đổi cách thực hiện của phương thức này.

2. Phương thức override ở lớp con

override được sử dụng ở lớp con để ghi đè phương thức virtual của lớp cha.

Ví dụ:

class Cho : DongVat
{
    public override void Keu()
    {
        Console.WriteLine("Gau gau");
    }
}

Lúc này lớp Cho đã thay đổi cách thực hiện phương thức Keu() của lớp DongVat.

3. Ví dụ về tính đa hình

DongVat dv = new Cho();
dv.Keu();

Kết quả:

Gau gau

Mặc dù biến dv có kiểu DongVat, nhưng đối tượng thực tế được tạo ra là Cho, vì vậy chương trình sẽ gọi phương thức Keu() được override ở lớp Cho.

Sự khác nhau:

virtual	override
Khai báo ở lớp cha	Khai báo ở lớp con
Cho phép lớp con ghi đè	Dùng để ghi đè phương thức lớp cha
Là phương thức có thể được thay đổi	Là phương thức thực hiện phiên bản mới
Là cơ sở để thực hiện đa hình	Thực hiện hành vi đa hình

Tóm lại, virtual cho phép một phương thức ở lớp cha được ghi đè, còn override được sử dụng ở lớp con để cung cấp cách thực hiện mới cho phương thức đó.

Câu 4: Tại sao một thành phần được khai báo là static trong Lớp (Class) lại không thể truy xuất thông qua một thể hiện (Object Instance) được tạo bằng toán tử new?

static có nghĩa là thành phần đó thuộc về lớp (Class) chứ không thuộc về một đối tượng cụ thể được tạo ra từ lớp đó.

Ví dụ:

class SinhVien
{
    public static string TenTruong = "Dai hoc Dien Luc";
}

Biến TenTruong là biến static, vì vậy nó thuộc về lớp SinhVien.

Ta truy cập biến này bằng tên lớp:

Console.WriteLine(SinhVien.TenTruong);

Không cần tạo đối tượng:

SinhVien sv = new SinhVien();

Thành phần static được dùng chung cho tất cả các đối tượng thuộc lớp đó. Nếu tạo nhiều đối tượng SinhVien thì tất cả đều dùng chung một biến TenTruong.

Ví dụ:

class SinhVien
{
    public string Ten;
    public static int SoLuong = 0;

    public SinhVien(string ten)
    {
        Ten = ten;
        SoLuong++;
    }
}

Khi tạo:

SinhVien sv1 = new SinhVien("Khoa");
SinhVien sv2 = new SinhVien("Nam");

Console.WriteLine(SinhVien.SoLuong);

Kết quả:

2

SoLuong không thuộc riêng sv1 hay sv2 mà thuộc về toàn bộ lớp SinhVien.

Vì vậy, về nguyên tắc, thành phần static được truy cập thông qua tên lớp:

TenLop.TenThanhPhanStatic

thay vì thông qua đối tượng:

doiTuong.TenThanhPhanStatic

Lý do là đối tượng được tạo bằng new đại diện cho một instance cụ thể, trong khi thành phần static chỉ có một bản dùng chung cho cả lớp và không gắn với một instance cụ thể nào.

Kết luận

static dùng cho những dữ liệu hoặc phương thức dùng chung cho toàn bộ lớp. Còn các thành phần không có static thường thuộc về từng đối tượng riêng biệt. Đây là điểm quan trọng cần phân biệt khi lập trình hướng đối tượng trong C#.
