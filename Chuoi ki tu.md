#Chuỗi ký tự
###1.Khái niệm
-Chuỗi ký tự là một dãy các ký tự đặt trong cặp dấu nháy kép. Chuỗi rỗng được ký hiệu bằng hai dấu nháy kép đi liền nhau. Một chuỗi ký tự được cấp phát một khoảng nhớ cho một mảng kiểu char chứa các ký tự của chuỗi và chứa thêm ký tự '\0' là ký tự kết thúc chuỗi.
-Mỗi ký tự của chuỗi được chứa trong một phần tử của mảng. Chuỗi ký tự là một trường hợp riêng của mảng một chiều khi mỗi thành phần của mảng là ký tự
Chuỗi ký tự thường được khai báo theo khai báo theo hai mẫu:
		char ten_chuoi[] ;	hoặc char *ten_chuoi;

###2. Các thao tác trên chuỗi
	Trong C không tồn tại các phép toán so sánh, gán nội dung của chuỗi này cho chuỗi khác. 
	Ðể thực hiện các thao tác  này ta sử dụng  một thư viện các hàm chuẩn là <string.h>.
- Hàm strlen: int strlen(char s[])
	Trả về độ dài của chuỗi s, chính là chỉ số của ký tự NULL trong chuỗi.
- Hàm strcpy: strcpy(char dest[], char source[])
	Sao chép nội dung chuỗi source vào chuỗi dest.
- Hàm strchr:  char *strchr(char s[], char c)
	Tìm lần xuất hiện đầu tiên của ký tự c trong chuỗi s, trả về địa chỉ của ký tự này.
- Hàm strncpy: strncpy(char dest[], char source[], int n)
	 Sao chép n ký tự trong  chuỗi source vào chuỗi dest. Trong trường hợp không có đủ n ký tự trong source thì hàm sẽ điền thêm các ký tự trắng vào chuỗi dest.
- Hàm strcat : strcat(char ch1[], char ch2[])
	Nối chuỗi ch2 vào cuối chuỗi ch1. Sau lời gọi hàm này độ dài chuỗi ch1 bằng tổng độ dài của cả hai chuỗi ch1 và ch2 trước lời gọi hàm.
- Hàm strncat : strncat(char ch1[], char ch2[],int n)
	Nối n  ký tự đầu tiên của ch2 vào ch1

- Hàm strstr : char *strstr(char s1[], char s2[])
	Tìm kiếm chuỗi s2 trong chuỗi s1, Trả về địa chỉ của lần xuất hiện đầu tiên của s2 trong s1 hoặc NULL khi không tìm thấy.
- Hàm strcmp : int strcmp(char ch1[], char ch2[])
	So sánh hai chuỗi ch1 và ch2. Nguyên tắc so sánh theo kiểu từ điển. Giá trị trả về:
= 0 nếu chuỗi ch1 bằng chuỗi ch2
> 0 nếu chuỗi ch1 lớn hơn chuỗi ch2
< 0 nếu chuỗi ch1 nhỏ hơn chuỗi ch2
VD: Đếm số lần xuất hiện của  ký tự a trong một xâu ký tự cho trước
```
#include<stdio.h>
#include<conio.h>
#define HANG 128
void main()
{	char xau[HANG];	int i,na;
	clrscr();	
	printf("\nNhap mot xau ky tu:");gets(xau);
	na=i=0;
	while(xau[i]) 
		if (xau[i++]=='a') na++;
		printf("\nXau co %d chu  a",na);
		getch();
	return;
}
```

##3. Mảng và chuỗi ký tự
- Một dạng sử dụng con trỏ đặc biệt là việc sử dụng một mảng các biến con trỏ. Khai báo theo mẫu
type *pointer_array[size];
- VD: khai báo	char *temp[10];
	sẽ khai báo một mảng 10 con trỏ char có thể được dùng để khai báo một mảng để lưu trữ địa chỉ của mười chuỗi ký tự nào đó.
- Bài tập:viết chương trình nhập nhiều tên người vào từ bàn phím, sắp xếp lại theo thứ tự và in kết quả đã sắp xếp ra. 
+ Sắp xếp lại các tên này theo thứ tự alphabet
+ In các tên ra theo thứ tự đó.


