# Trinh Soan Thao Vi

###1. Giới thiệu

Vi là chương trình soạn thảo chuẩn trên các hệ điều hành Unix. Nó là chương trình soạn thảo trực quan, hoạt động dưới 2 chế độ: Chế độ lệnh (command line) và chế độ soạn thảo (input mode)
Để soạn thảo tập tin mới hoặc xem hay sửa chữa tập tin cũ ta dùng lệnh:
$vi tập-tin
Khi thực hiện, vi sẽ hiện lên màn hình soạn thảo ở chế độ lệnh. Ở chế độ lệnh, chỉ có thể sử dụng các phím để thực hiện các thao tác như: dịch chuyển con trỏ, lưu dữ liệu, mở tập tin...Do đó, bạn không thể soạn thảo văn bản. Nếu muồn soạn thảo văn bản, bạn phải chuyển từ chế độ lệnh sang chế độ soạn thảo. Chế độ soạn thảo giúp bạn sử dụng bàn phím để soạn thảo nội dung văn bản.

###2. Chuyển sang chế độ

Dưới đây là nhóm lệnh để chuyển sang chế độ soạn thảo.

**i** trước dấu con trỏ

**l** trước ký tự đầu tiên trên dòng

**a** sau dấu con trỏ

**A** sau ký tự đầu tiên trên dòng

**o** dưới dòng hiện tại

**O** trên dòng hiện tại

**r** thay thế 1 ký tự hiện hành

**R** thay thế cho đến khi nhấn 

Để chuyển ngược lại mode command ta dùng phím ESC

###3. Các nhóm lệnh di chuyển con trỏ

**h** - sang trái 1 space

**e** - sang phải 1 space

**w** - sang phải 1 từ

**b** - sang trái 1 từ

**k** - lên 1 dòng

**j** - xuống 1 dòng

**)** - cuối câu

**(** - đầu câu

**}** - đầu đoạn văn

**{** - cuối đoạn văn

###**4. Nhóm lệnh xóa

**dw** - xóa 1 từ

**d^** - xóa ký tự từ con trỏ đến đầu dòng

**d$** - xóa ký tự từ con trỏ đến cuối dòng

**3dw** - xóa 3 từ

**dd** - xóa dòng hiện hành

**5dd** - xóa 5 dòng

**x** - xóa 1 ký tự

###5. Nhóm lệnh thay thế

**cw** - thay thế 1 từ

**3cw** - thay thế 3 từ

**cc** - dòng hiện hành

**5cc** - 5 dòng

###6. Nhóm lệnh tìm kiếm

**?** tìm trở lên

**/** tìm trở xuống

 */and  tìm từ kế tiếp của and

 *?and  tìm từ kết thúc là and

*/nThe tìm dòng kế bắt đầu bằng The

**n** tìm hướng xuống

**N** tìm hướng lên

###7. Nhóm lệnh tìm kiếm và thay thế

:s/text1/text2/g - thay thế text1 bằng text2
:1.$s/tập tin/thư mục - thay tập tin bằng thư mục từ hàng 1
:g/one/s/1/g - thay thế one bằng 1
###8. Nhóm lệnh copy, paste, undo


Để copy ta dùng lệng y và để paste ta dùng lệnh p
y$ - copy từ vị trí hiện tại của cursor đến cuối cùng
yy - copy toàn bộ dòng tại vị trí cursor
3yy - copy 3 dòng liên tiếp
u - Undo lại thao tác trước đó

###9. Thao tác trên tập tin

:w - ghi vào tập tin
:x - lưu và thoát khỏi chế độ soạn thảo
:wq - lưu và thoát khỏi chế độ soạn thảo
:w - lưu vào tập tin mới
:q - thoát nếu ko có thay đổi
:q! - thoát không lưu
:r - mở tập tin đọc
