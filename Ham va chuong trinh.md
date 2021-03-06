#Hàm Và Chương Trình
##1.Khái niệm
####Chương trình:

Một chương trình C bao gồm một hoặc nhiều hàm. Hàm main() là thành phần bắt buộc của chương trình. Chương trình bắt đầu thực hiện từ câu lệnh đầu tiên của hàm main( ) cho đến khi gặp dấu } cuối cùng của hàm này.
	Hàm: Là một đoạn chương trình độc lập thực hiện trọn vẹn một công việc rồi trả về một giá trị cho chương trình đã gọi nó.
####Đặc điểm của hàm:
Là một đơn vị độc lập của chương trình. 
Không cho phép xây dựng một hàm bên trong một hàm khác.

Ví dụ :
```
#include <stdio.h>
long luy_thua(int x);
main() //Ham chinh
{
 int x;
 printf("Nhap so muon luy thua");
 scanf("%d",&x);
 printf("Ket qua = %ld",luy_thua(x));
 getch();
 }
 
 long luy_thuya(int x)
 {
 long ketqua;
 ketqua=x*x*x;
 return ketqua;
 }
```

##Quy tắc xây dựng hàm: 
Một hàm gồm có các thành phần sau

Nguyên mẫu của hàm: Bao gồm
><kiểu dl của hàm> <tên hàm(ds các tham số)>;

	Có thể có hoặc không khai báo nguyên mẫu của hàm, khi không khai báo nguyên mẫu thì bộ  biên dịch sẽ kiểm tra việc truyền tham số, giá trị trả về có phù hợp hay không rồi mới cho thực hiện hàm.
	Tất cả nguyên mẫu của các hàm có trong chương trình nên đặt trước hàm main().
 
- Kiểu giá trị của hàm
	Giá trị trả về của hàm được xác định dựa vào mục đích của hàm. Nếu các hàm không trả về giá trị ta phải khai báo kiểu void.
- Tên hàm
	Ðặt theo qui định đối với danh định. Tên hàm trong nguyên mẫu và khi khai báo phải giống nhau.
- Tham số của hàm
	Khi viết một hàm ta phải xác định xem hàm có bao nhiêu tham số ? 
- Nội dung của hàm 

Cấu trúc của một hàm
```
<Kiểu trả về><Tên hàm>(<ds tham số hình thức hay đối số>)
{		<Khai báo biến cục bộ>;
		<Các câu lệnh trong thân hàm>;
		[return<bt trả về giá trị hàm>];
	};
```

Chú ý:
Đối với các hàm không có kiểu trả về ta có hàm kiểu void
Hàm không có đối thì dùng kiểu void để khai báo đối. VD
```
	void bell(void)
	{	int i;
		for(i=0;i<10;i++) putch(7);	
		}
```

- Cách sử dụng hàm: Hàm được sử dụng thông qua lời gọi hàm.
		<tên hàm> ([ds tham số thực])
~Tham số thực phải bằng tham số hình thức
~Kiểu của tham số thực phải phù hợp với kiểu của tham số hình thức
####*Hoạt động của hàm khi có lời gọi hàm
+ Cấp phát bộ nhớ cho tham số hình thức và biến cục bộ
+ Gán giá trị của tham số thực cho tham số hình thức
+ Thực hiện các lệnh trong thân hàm
+ Khi gặp câu lệnh return hoặc dấu hiệu kết thúc hàm thì bộ nhớ sẽ xoá các tham số hình thức và biến cục bộ sau đó thoát khỏi hàm quay về chương trình gọi hàm 

###3. Các tham số trong hàm
####3.1	Phân loại tham số theo cách sử dụng 
- Tham số hình thức: Các tham số mà ta ghi trong nguyên mẫu hay ghi lúc khai báo hàm gọi là tham số hình thức.
- Tham số thực:Các giá trị, biến mà ta ghi sau tên hàm khi gọi hàm đó để thực hiện gọi là tham số thực. Trong C, các tham số thực lại chia ra làm hai loại:
- Tham chiếu: Là các tham số thực mà ta truyền cho Hàm dưới dạng con trỏ (dạng địa chỉ). Tham chiếu mới ghi nhận lại được những kết quả vừa tính toán trong Hàm khi Hàm kết thúc.
- Tham trị : Là các tham số thực mà ta truyền cho Hàm dưới dạng biến. Tham trị không bảo lưu lại những kết quả thay đổi của nó được tính toán trong Hàm khi Hàm kết thúc.

####3.2	Phân loại theo công dụng 
- Tham số của một hàm có hai công dụng:
- Cung cấp các giá trị cho hàm khi ta gọi nó thực hiện .
- Lưu các kết quả tính toán được trong quá trình hàm hoạt động
- Tương ứng với công dụng ta có các loại tham số:
- Tham số vào: Cung cấp giá trị cho hàm.
- Tham số ra: Lưu kết quả tính toán được trong hàm. 
- Tham số vừa vào, vừa ra: vừa cung cấp giá trị cho hàm, vừa lưu kết quả tính toán được trong hàm.



###4.	Hàm có đối con trỏ
	Đối số  của hàm là con trỏ kiểu int (float,double,. ) thì tham số thực tương ứng phải là địa chỉ của biến kiểu int (float,double,.). Khi đó địa chỉ của biến được truyền cho đối con trỏ tương ứng.
	Khi muốn bảo lưu lại kết quả tính toán được của các đối số trong hàm để sử dụng cho chương trình gọi hàm có đối số thì chúng ta phải khai báo đối số của hàm là tham chiếu (con trỏ hay dạng địa chỉ).




