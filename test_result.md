TC_FR-02_01 Đăng nhập thành công
TC_FR-02_02 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Nếu spam đăng nhập liên tục trong thời gian đang bị khóa, thì kể cả thông tin đăng nhập đúng cũng sẽ ko vào được sau 30s spam. Có vẻ nếu muốn đăng nhập thì sau lần đăng nhập bị khóa phải tự chờ đúng hơn 30s rồi mới thực hiện đăng nhập, lúc này mới được. UI khi đang trong trạng thái khóa thì chờ 1 thời gian bấm lại vẫn ko được. PHẢI reset page mới đăng nhập được.
TC_FR-02_03 Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Username
TC_FR-02_04 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_05 Frontend chặn submit, kèm yêu cầu “Please fill out this field.” ở ô Mật khẩu
TC_FR-02_06 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_07 Đăng nhập thất bại 2 lần là khóa luôn (tuy nhiên UI không hiển thị đang bị khóa 30s). Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_08 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự.
TC_FR-02_09 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự.

TC_FR-02_BVA_01 Đăng nhập thất bại 2 lần là khóa luôn (tuy nhiên UI không hiển thị đang bị khóa 30s). Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.

TC_FR-02_BVA_02 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_BVA_03 Màn hình không hiển thị bị khóa 30s, mà chỉ đơn giản hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”.
TC_FR-02_BVA_04 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Kể cả reset page rồi đăng nhập lại cũng hiện tương tự.
TC_FR-02_BVA_05 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Reset page rồi đăng nhập lại thì được.
TC_FR-02_BVA_06 Frontend hiện là “Đăng nhập thất bại, vui lòng kiểm tra lại”. Reset page rồi đăng nhập lại thì được.
