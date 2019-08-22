# community

### 1. cần thiết 1 bẳng access_token. vì mình sẽ cho 1 khoảng thời gian sống trong bao lâu. tại sao lại tạo bảng riêng mà không phải bảng chung. Vì nếu là bảng riêng thì sẽ khi là người dùng đăng nhập rồi, mình sẽ xử lý xem là họ có access_token hay không. Còn nếu đặt access_token sẽ lại sử lý chung với user table sẽ có người tạo tài khoản hay là lấy dữ liệu ra. rồi update access_token hoặc tạo mới. Vậy quá nhiều luồng xử lý trên 1 bảng làm cho kiểu nhiều người vào 1 kênh sẽ quá tải đó. nên tách ra bảng riêng thì hay hơn.
