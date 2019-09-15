# community

api cần là userlist, deletefile, updatefile, removefile...(nếu mà có nhiều người update lên 1 lúc thì sao). file> lớn phần update như thế nào. 
  1. cần thiết 1 bẳng access_token. vì mình sẽ cho 1 khoảng thời gian sống trong bao lâu. tại sao lại tạo bảng riêng mà không phải bảng chung. Vì nếu là bảng riêng thì sẽ khi là người dùng đăng nhập rồi, mình sẽ xử lý xem là họ có access_token hay không. Còn nếu đặt access_token sẽ lại sử lý chung với user table sẽ có người tạo tài khoản hay là lấy dữ liệu ra. rồi update access_token hoặc tạo mới. Vậy quá nhiều luồng xử lý trên 1 bảng làm cho kiểu nhiều người vào 1 kênh sẽ quá tải đó. nên tách ra bảng riêng thì hay hơn.

2. nếu mà đăng nhập bằng facebook và google thì ta lây được mail. nếu có mail rồi thì ta update. nếu chưa có ta tạo mới. Ngoài ra đăng nhập bằng cách này không có password ta phải tự băm password và mã hóa tự động cho nó. ok.

3. Ngoai ra bài post thuộc chủ đề nào nữa.....  tag trong compsace... cntt, mạng, hệ thông, game, khác
3. /@:name.   (bỏ phđằng sau cấu trúc @ntnghiavt)(chính là trang profile của người dùng luôn đó.
5. /@:user/settings(user dang nhap)(minh se biet user_id) can he thong nhap thong tin can thiet thoi.
5.1    => update taikhoan, remove taikhoan. (user dang nhap)
6. /signup
7. /login
9.0.body{
  sending_code: boolean,
  code: string
}
9. /auth/verified-email (userloin) (sent again code) => sending_code= true; +> gửi code cho user và sau khi gửi xong sending_code = null.
    sau đó người nhấn vào 
    check code = 'code in data khoong) nếu không set req.code = null thì báo lỗi ok. 
    //khi code duoc tao. se goi settimeout...(1 khoang thoi gian nao do) se xoa di cai code neu nó hết hạn ý.
    băt người ta phải nhập lại đến được thì thôi. 
    xong rồi sẽ chuyển hướng tới trang verify_email.
    chuyen toi ahtu/access-token
    
10. /auth/access-token   (userlogin) redirect home.(đã phải đăng nhập rôi) 
   (giả sử trang này người ta sẽ kiểm tra là email đã xác nhận chưa. nếu chưa sẽ về verified-email) nếu rối. thì xét tiếp user_id có token không => nếu có -> chuyển tới trang home.
   null -> create token.
   redirect to home.

.11. bây giờ sai pass... vậy cần xác nhận lại ok....
(cần có email nhập vào ha.)
11.1 auth/re-password
   { check code = co bang code trong data khoong}, khong thi keu he thong gui lai code.
   sau do nguoi sudung nhap passmoi. va code. code dung thi update. dai thi bao loi. ok.
   
 
   
11. /  home... 
11.1 /admin/posts
khi nào xảy ra trường hợp này...
xét vai trò nếu là khác thì k được đăng bài trong hệ thống dành cho admin... (create post) với nội dùng và vân vân thuộc cái domain nào... bài post có thêm domain_id
mỗi domain sẽ thuộc về 1 topic...
 thêm nữa có database domain. ( id, name, topic_name) 
11.2  /posts 
ngoài ra thì tất cả mọi thành viên thì sẽ chỉ được vào trangcreate với nội dùng và thêm tag(bài viết phải có tag)...
khi đi qua restful này thì ta sẽ add post vào thêm với database hold(giữ tag nào)...ok.

11.3 /posts/{id}(create post thong thuong, xoa post(gop ca post cua admin..bai thang nao thang do xoa).                                                       update post. find by id;
11.4 /@:name/:title-format-:id {title sẽ có construction: all-connections-to-the-world)(@ntnghiavt)

12.0 /:topic/:scope giả sử là (/cntt/laptrinhvien or /cntt/hethong, /kinhte/dautu,/kinh-te/tai-chinh, /kinh-te/ngan-hang)

bài post sẽ có thêm 1 trường là  topic and scope.
12. /tag/:tagname => tra ve thong tin bai post theo tag name. ta có tagname.... (lập trình viên, hệ thông, gaming, khac)//cho thanh viên thảo luận.(nếu mà type = 'stories' thì sẽ add bài viết đó tới nhóm  tag.)  (mặc địnuh topic=null và scope = null)
13. /help  => data help
  - id
  - type: account issue, report a rules violation, report a copy right violation, feedback, other.
  - description.
  - email (cái này trang help không cần đăng nhập, vì lỗi tài khoản sao đăng nhập được.) => cần thông báo từ hệ thống tới người dùng. system-notify.
  data report for post.
  
14. bài post thì cần phải có report. ví như là nội dung spam, người khác sao chép bài post thì sao....(nội dung k hợp với chủ đề)

### Server
 Mỗi 1 server thì là 1 chiếc máy tính đơn lẻ đó. Nếu giả sử mình có thêm 1 file vào trong máy tính hay xóa file đi thì nó chỉ thay đổi trên máy tính của mình thôi.
 Vậy giờ mình muốn mà khi mình thêm 1 file thì máy tính của mình có thêm và máy tính của tất cả các bạn trong lớp của mình cũng có file đó. Vậy tất cả máy tính đó có điều kiện là cùng 1 lớp. và có 1 sự kết nối với nhau. để mình có khả năng thay đổi máy tính của bạn, Giống với điều khiển từ xa vậy...
 
 ==> khi mình sẽ like 1 bài comment thì sẽ hiển thị ở máy tính của mình(server). Nhưng máy tính của bạn mình sẽ k có(server).
 vậy mình sẽ phải có kết nối chung giữa minh với bạn(các bạn mình) là cùng ở trên trang http://community...
 vậy  tất cả những ai mà đang ở trên cái trang này sẽ nhận được sự thay đổi, à đều nhìn thấy hiển thị cái bài like dó....hihi...ok vậy là xong. 
 
