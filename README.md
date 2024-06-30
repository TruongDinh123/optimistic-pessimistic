# optimistic-pessimistic
Hiểu thêm về khóa lạc quan (optimistic) và bi quan (pessimistic)

![image](https://github.com/TruongDinh123/optimistic-pessimistic/assets/99858324/5b1efff2-d0f4-409d-9b3b-2d430c2fedcd)


Hệ thống lớn phải trải qua vấn đề này thì mới gọi là hệ thống lớn. Nghĩa là phải đối mặt với "Vấn đề vượt mức trong database". Cụ thể là trong kho còn 10 mà bán 20... Lý do ở đây chính là các yêu cầu đồng thời cao dẫn đến dữ liệu đạp lên nhau hay còn gọi là dữ liệu bẩn... Các giải pháp được đưa ra và trong đó có khóa phân tán...
Nghĩa là mỗi hoạt động của đồng thời cao đều có khóa giao dịch... Ai đến thì khóa, xong việc mở ra... Nhưng làm vậy thì user sẽ chờ đợi nhau, làm hệ thống tắc nghẽn giao dịch...

1. Pessimistic:
  - Công dụng của khóa bi quan (Pessimistic) là không cho phép nhiều user truy cập vào cùng 1 lúc ví dụ:
  - 4 user truy cập đồng thời vào kho nhưng chỉ có 1 user truy cập vào được sau khi user được truy cập thực hiện xong thì mới tiếp tục đến user khác.
  - Hoặc 1 ví dụ khác thì khi vào ngân hàng giao dịch mỗi người đều đến rút tiền trong cùng 1 thời điểm và đều phảo bốc số (đây là key Pessimistic). Trong cùng 1 thời điểm thi chỉ có 1 người duy nhất được giao dịch tiền và giao dịch xong thì mới tới người tiếp theo.
  - Ưu điểm: Tính nhất quán về dữ liệu cao, tránh bị confict.
  - Nhược điểm: Không thân thiện với người dùng.
2. optimistic
  - Công dụng sẽ ngược lại với khóa bi quan (Pessimistic) cho phép 1 lượng request vào cùng 1 thời điểm nhưng phải kiểm tra trước khi trả về response rằng đã có người nào sửa đổi trước hay không
  - Ví dụ: Trước khi ghi lại thay đổi vào cơ sở dữ liệu, hệ thống sẽ kiểm tra chỉ số phiên bản. Nếu chỉ số phiên bản của bản ghi trong cơ sở dữ liệu vẫn giống như lúc người dùng đọc (không bị thay đổi bởi người dùng khác), thì thay đổi sẽ được ghi nhận. Nếu chỉ số phiên bản đã thay đổi (nghĩa là dữ liệu đã được người dùng khác cập nhật), hệ thống sẽ từ chối thay đổi và thông báo lỗi cho người dùng.
  - Ưu điểm của khóa lạc quan:
      + Hiệu suất cao: Không cần giữ khóa lâu dài, giúp cải thiện hiệu suất hệ thống.
      + Tránh xung đột: Đảm bảo rằng các thay đổi không bị ghi đè bởi các người dùng khác mà không có sự kiểm soát.
  - Nhược điểm:
      + Xung đột phiên bản: Người dùng có thể gặp phải xung đột phiên bản nếu dữ liệu được cập nhật thường xuyên, yêu cầu người dùng phải thử lại cập nhật.
