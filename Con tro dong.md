#Lv8:Cấp phát và giải phóng bộ nhớ động
##.1Khái niệm
###Biến động: Là các biến được tạo ra lúc chạy chương trình, tùy theo nhu cầu.
Số biến này hoàn toàn không được xác định từ trước. Các biến động không có tên (việc đặt tên thực chất là gán cho nó một địa chỉ xác định). 

###Cách tạo ra biến động và truy nhập đến biến động được tiến hành như sau 
Việc tạo ra biến động và xóa nó đi (để thu hồi lại bộ nhớ) được thực hiện nhờ các hàm như malloc() và free() đã có sẵn trong thư viện stdlib.h

###Việc truy nhập đến biến động được tiến hành nhờ các biến con trỏ. Các biến con trỏ được định nghĩa như các biến tĩnh ( được khai báo ngay từ đầu trong phần khai báo biến) và được dùng để chứa địa chỉ các biến động
####VD1:	
```
int *p; /* Khai báo biến con trỏ p*/
			p= (int *) malloc(100);/* Tạo biến động*/
```

	Ðoạn chương trình trên sẽ cấp phát 100 bytes trong bộ nhớ và gán địa chỉ khối bộ nhớ này cho p
####VD2: cấp phát bộ nhớ chính xác cho 70 ký tự:
```
	/* Khai báo biến con trỏ kiểu char */
		char *cp; 
	/* Tạo biến động */
		cp=(char *) malloc(70);
```

##2.	Cấp phát và giải phóng bộ nhớ động (các hàm thuộc stdlib.h và alloc.h) 
###2.1 Cấp phát bộ nhớ động bằng hàm malloc( )
	Cú pháp	void *malloc(kiểu _dl   size)

- Chức năng: Hàm malloc cấp phát một vùng nhớ có kích thước là size.
- size là một giá trị kiểu_dl (là một kiểu dữ liệu định sẵn trong thư viện stdlib.h).
- Hàm malloc trả về con trỏ kiểu void chứa địa chỉ ô nhớ đầu của vùng nhớ được cấp phát. 
Nếu không đủ vùng nhớ để cấp phát hàm trả về giá trị NULL, vì vậy phải kiểm tra giá trị trả về khi sử dụng hàm malloc.

###2.2 Cấp phát bộ nhớ động bằng hàm calloc
####Cú pháp
(datatype *) calloc(n, sizeof(object));
- Hàm calloc cấp phát bộ nhớ động cho các kiểu dữ liệu Trong đ ó: 
- (datatype *) là kiểu con trỏ trỏ tới kiểu dữ liệu datatype.
- n là số lượng object thuộc kiểu datatype cần cấp phát bộ nhớ.
- datatype có thể là kiểu dữ liệu cơ sở hoặc kiểu dữ liệu mới

###2.3 Cấp phát bộ nhớ động bằng hàm relloc
####Cú pháp
(datatype *) realloc(buf _p, newsize);
	Hàm có chức năng cấp phát lại bộ nhớ
#####Trong đó:
- buf_p là con trỏ đang trỏ đến vùng ô nhớ đã được cấp phát từ trước.
- newsize là kích thước mới cần cấp phát, có thể lớn hoặc nhỏ hơn.

###2.4 Giải phóng bộ nhớ bằng hàm free
####Cú pháp

```
void free( void *prt)
```
	
Hàm free giải phóng vùng nhớ được trỏ đến bởi con trỏ ptr. 
Nếu con trỏ ptr = NULL thì hàm free không làm gì cả.

##3. Bộ nhớ HEAP và cơ chế tạo biến động
###3.1Khái niệm
- Các biến động do malloc tạo ra được C xếp vào một vùng 
ô nhớ tự do theo kiểu xếp chồng và được gọi là HEAP ( bộ nhớ cấp phát động). 
Ngôn ngữ C quản lý HEAP thông qua một con trỏ của HEAP là HEAPPTR. 
Nó luôn trỏ vào byte tự do đầu tiên của vùng ô nhớ còn tự do của HEAP. 
Mỗi lần gọi malloc(), con trỏ của HEAP được dịch chuyển về phía đỉnh của vùng 
ô nhớ tự do một số byte tương ứng với kích thước của biến động mới tạo ra. 
- Ngược lại, mỗi khi giải phóng bộ nhớ biến động, bộ nhớ biến động được thu hồi.
Tuy nhiên, nếu việc tạo và thu hồi không phải là quá trình liên tục và kế cận thì có thể xảy ra
trường hợp: Có những vùng thu hồi nằm lọt trong vùng các biến động khác vẫn còn đang
hoạt động.

![Dynamic Pointer](http://sv1.upsieutoc.com/2016/11/18/pointerdynamic.png)

###3.2.Ví dụ áp dụng
Tìm các số nguyên tố trong dãy số tự nhiên.
```
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<alloc.h>
void main()
{
long *primes=NULL, *start=NULL, *open=NULL, trial=0;
int i=0, found=0, total=0;
printf("Bao nhieu so nguyen to ban can tim ?");
scanf("%d",&total);
primes=(long *) malloc(total*sizeof(long));
if (primes==NULL)
{
printf("\n Khong du bo nho");
return;
}
/*3 so nguyen to dau tien da biet*/
*primes=2;
*(primes+1)=3;
*(primes+2)=5;
open=primes+3;/*Lay dia chi phan o nho tu do tiep theo*/
trial=5;
do
{
trial+=2; /*Gia tri tiep theo de kiem tra*/
start=primes; /*Start tro vao phan dau cua prime*/
found=0;
for(i=0;i<open-primes;i++)
if (found=(trial%*start++)==0) break;
if (found==0) /*Tim thay mot so moi*/
*open++=trial;
} while (open-primes<=total);
for(i=0;i< 5*(total/5);i+=5) /*Hien thi 5 so 1 lan*/
printf("\n %12ld %12ld %12ld %12ld
%12ld",*(primes+i),*(primes+i+1),*(primes+i+2),*(primes+i+3),*(primes+i+4));
}
```

####Kết quả chương trình :
>Bao nhieu so nguyen to ban can tim ?10
2 3 5 7 11
13 17 19 23 29

##4. BÀI TẬP MINH HỌA
####Bài 1 :
```
/*Viết chương trình nhập một chữ, xuất ra chữ đó nhiều
lần dùng con trỏ*/
#include<stdio.h>
#include<conio.h>
char *lap(char chu,int lan);
void main()
{
char c;
printf("\n%s",lap('s',3));
c=getchar();
printf("\n%s",lap(c,3));
getch();
}
char *lap(char chu,int lan)
{
char *supp;
int i;
supp=calloc(lan,sizeof(char));
for(i=0;i<=lan-1;i++)
supp[i]=chu;
return (supp);
}
```

###Bài 2:
```

/*Viết chương trình cho một dòng quảng cáo chạy từ phải
sang trái của màn hình*/
#include<stdio.h>
#include<conio.h>
void main()
{
char st[123]="Turbo C kinh chao cac ban ";
char *st_show;
int i;
st_show=(char *) calloc(80,sizeof(char));
for(i=0;i<80;i++)
strcat(st_show," ");
strrev(st);
strcat(st,st_show);
strrev(st);
for(i=0;i<80;i++)
{
strncpy(st_show,st+i,79);
gotoxy(1,1);
cprintf("%s",st_show);
delay(100);
}
free(st_show);
}

```



