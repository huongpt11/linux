
# Cơ bản về Linux
 Linux là một hệ điều hành mã nguồn mở giống Microsoft Windows, IOS,..
## 1. Cấu trúc 
![](https://2.bp.blogspot.com/-xU5aB5e7v9E/WfAvTqZbDkI/AAAAAAAAJAo/-0s8WE4OOyE1_YZDjFLhGc4IWQ8IONEXwCLcBGAs/s400/ksa-pic0.jpeg)
- Kernel : nhân hệ điều hành,chứa các module, thư viện thiết lập giao tiếp giữa các thiết bị và phần mềm.
- Shell : thực thi các câu lệnh từ Application tới Kernel để giải quyết (sh, bash- shell mặc định trên Linux, csh- được viết bằng ngôn ngữ lập trình C,..)
- Application : là các ứng dụng, phần mềm và tiện ích mà người dùng cài và sử dụng.
**Phiên bản** : MANJARO ,DEBIAN, UBUNTU, ANTERGOS, LINUX MINT,....
## 2.Quá trình Boot và các Runlevels

![](https://camo.githubusercontent.com/2918eb4946bb17f09d39b9e6835be4d0cb3ed9415e1cf2f948835920935d3846/68747470733a2f2f692e696d6775722e636f6d2f57617a6f7679512e706e67)
Trong đó:
### 1) System Startup 
- là bước đầu của quá trình khởi động , ở bước này BIOS thực hiện công việc gọi là **POST**. **POST** là quá trình kiểm tra tính sẵn sàng phần cứng nhằm kiểm tra thông số và trạng thái của các phần cứng máy tính như bộ nhớ, CPU, thiết bị lưu trữ , card mạng,.. Nếu quá trình **PÓST** kết thúc thành công , **BIOS** sẽ cố gắng tìm kiếm và boot 1 hệ điều hành được chứa trong các thiết bị lưu trữ ổ cứng , USB,.. 
### 2)MBR loading: **MBR-Master Boot Record** được lưu trữ tại **sector** đầu tiên của một thiết bị lưu trữ dữ liệu
### **3) GRUB Loader**
- Sau khi xác định vị trí Boot Loader , bước này sẽ thực hiện load Boot Loader vào bộ nhớ và đọc thông tin cấu hình sau đó hiển thị **GRUB boot menu** để user lựa chọn . Nếu user không chọn OS thì sau khoảng thời gian được định sẵn , **GRUB** sẽ load **kernel** default vào memory để khởi động .
- Đối với các hệ thống sử dụng **EFI/UEFI** , các firmware **UEFI** sẽ đọc dữ liệu Boot Manager để tìm các ứng dụng **UEFI** . Firmware sẽ chạy ứng dụng **UEFI** .
### **4) Kernel**
- **Kernel** của hệ điều hành sẽ được nạp vào trong **RAM** . Khi **kernel** hoạt động thì việc đầu tiên đó là thực thi quá trình **INIT** .
### **5) Runlevels ( INIT )**
- Đây là giai đoạn chính của quá trình boot . Quá trình này bắt đầu bằng việc đọc file `/etc/inittab` :
    - **Runlevel** `0` : ***halt*** - tắt hệ thống
    - **Runlevel** `1` : ***single-user mode*** - không cấu hình network , khởi động các tiến trình và cho phép đăng nhập user *non-root* 
    - **Runlevel** `2` : ***multi-user mode*** - không cấu hình network , khởi động các tiến trình
    - **Runlevel** `3` : ***multi-user mode with networking*** - khởi động hệ thống bình thường trên giao diện dòng lệnh
    - **Runlevel** `4` : ***undefined***
    - **Runlevel** `5` : ***X11*** - khởi động hệ thống trên giao diện đồ họa
    - **Runlevel** `6` : ***reboot*** - khởi động lại hệ thống
### **6) User Prompt**
- Người dùng đăng nhập và sử dụng

## **Thiết lập chế độ khởi động mặc định**
- **Multi-user.target** ( **INIT 3** ) : Chế đô dòng lệnh Command Mode ( non-graphics ) . User chỉ sử dụng các lệnh ( command ) để thao tác . Ở chế độ này Server dùng rấ ít RAM .
- **Graphical.target** ( **INIT 5** ) : Chế độ GUI , mặc định khi install OS ở chế độ GNOME là ta đang sử dụng **Graphical.target**
- Các lệnh thiết lập :
    - Thiết lập **Multi-user.target** mặc định khi khởi động :
        ```
        # systemctl set-default multi-user.target
        ```
    - Thiết lập **Graphical.target** mặc định khi khởi động :
        ```
        # systemctl set-default graphical.target
        ```
    - Kiểm tra chế độ mặc định khi khởi động hiện tại :
        ```
        # systemctl get default
        ```
    - Chuyển đổi tạm thời từ **graphical** -> **multi-user** :
        ```
        # systemctl isolate multi-user.target
        hoặc
        # init 3
        ```
    - Chuyển đổi tạm thời từ **multi-user** -> **graphical** :
        ```
        # systemctl isolate graphical.target
        hoặc
        # init 5

    
        
    



