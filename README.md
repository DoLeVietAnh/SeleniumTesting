Đỗ Lê Việt Anh - BIT220014 - 22SE1

# OrangeHRM Login Test Automation
## Giới thiệu
Dự án này kiểm thử tự động chức năng đăng nhập cho ứng dụng demo OrangeHRM sử dụng **Selenium WebDriver** và **TestNG**.

## Chức năng
- Tìm kiếm giá trị trong cây nhị phân
- Hỗ trợ các tình huống đặc biệt như:
    - Cây rỗng.
    - Cây chỉ có một nút.
    - Cây không cân bằng.
    - Cây có giá trị trùng lặp.
    - Cây chứa giá trị âm.

## Cấu trúc dự án

    ├── src/
    │   ├── test/
    │   │   ├── java/
    │   │          └── OrangeLoginTest.java  # Kiểm thử tự động
    ├── README.md                              # Tệp tài liệu dự án
    └── pom.xml                                # Tệp cấu hình Maven

## Hướng dẫn sử dụng
### 1. Cài đặt
- Yêu cầu: 
    - Java 11 hoặc mới hơn.
    - Maven hoặc Gradle để quản lý dự án.
    - Edge WebDriver.
    - Thư viện Selenium và TestNG:
        - Cài dependencies sau vào ``pom.xml`` nếu sử dụng Maven: 
        ```
        <dependencies>
            <dependency>
                <groupId>org.seleniumhq.selenium</groupId>
                <artifactId>selenium-java</artifactId>
                <version>4.x.x</version>
            </dependency>
            <dependency>
                <groupId>org.testng</groupId>
                <artifactId>testng</artifactId>
                <version>7.x.x</version>
            </dependency>
        </dependencies>
        ```
- Clone dự án:
``` 
git clone https://github.com/DoLeVietAnh/SeleniumTesting
cd SeleniumTesting
```
- Build dự án
```
mvn clean install
```

### 2. Chạy kiểm thử
Sử dụng JUnit để chạy các trường hợp kiểm thử:
- Chạy kiểm thử:
```
mvn test
```

- Kiểm tra kết quả: Báo cáo kiểm thử sẽ được xuất ra màn hình hoặc thư mục ```target/surefire-reports```

## Tổng quan mã nguồn
Dự án này sử dụng Selenium WebDriver và TestNG để tự động hoá kiểm thử chức năng đăng nhập của trang OrangeHRM. Dưới đây là các thành phần chính của mã kiểm thử;
### 1. Khởi tạo kiểm thử
- Annotation ``@BeforeClass`` được sử dụng để thiết lập môi trường kiểm thử.
- Trình duyệt Edge được khởi tạo, cửa sổ trình duyệt được phóng to, và trang đăng nhập demo của OrangeHRM được mở.
```java
driver = new EdgeDriver();
driver.manage().window().maximize();
driver.get("https://opensource-demo.orangehrmlive.com/web/index.php/auth/login");
```
### 2. Tự động hoá đăng nhập
- Script xác định các trường nhập liệu cho tên đăng nhập và mật khẩu bằng locator ``By.name``
- Nhập thông tin đăng nhập (``Admin`` và ``admin123``), sau đó nhấn nút đăng nhập được xác định bằng By.tagName.
```java
WebElement username = driver.findElement(By.name("username"));
username.sendKeys("Admin");

WebElement password = driver.findElement(By.name("password"));
password.sendKeys("admin123");

driver.findElement(By.tagName("button")).click();
```

### 3. Kiểm tra xác nhận
- Sau khi đăng nhập, script dừng lại trong một thời gian ngắn để đảm bảo trang đã tải xong.
- Kiểm tra xem đăng nhập có thành công không bằng cách kiểm tra nội dung văn bản cả thẻ tiêu đề ``h6`` và so sánh với kết quả mong đợi, ``"Dashboard"``.
```java
String actualResult = driver.findElement(By.tagName("h6")).getText();
String expectedResult = "Dashboard";
Assert.assertEquals(actualResult, expectedResult);
```

### 4. Dọn dẹp sau kiểm thử
- Annotation ``@AfterClass`` quản lý các hành động sau kiểm thử.
- Phương thức ``driver.quit()`` được sử dụng để đảm bảo trình duyệt được đóng sau khi hoàn tất kiểm thử. 
```java
driver.quit();
```

Link lịch sử ChatGPT: **```https://chatgpt.com/share/67867a15-97b0-800c-9594-4a5f483191c9```**
