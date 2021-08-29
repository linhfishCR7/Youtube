# Chương 2-Bài 3. Tạo cấu hình để sử dụng TWIG

## Step 1: tạo file `bootstrap.php` để quản lý việc khởi tạo Twig
- Tạo mới file `bootstrap.php` cùng cấp với `thư mục gốc` của bạn. 
- Ví dụ thư mục gốc hiện tại trong bài học là `/Youtube/Backend-PHP-MySql-Twig/`
- Tạo file `/bootstrap.php`
```
+---php
|   \---twig                    <- Đây là thư mục gốc của dự án, các bạn có thể đặt tên các bạn...
|       +---bootstrap.php       <- Tạo file
```
- Nội dung như sau:
```php
<?php
// Load các thư viện (packages) do Composer quản lý vào chương trình
require_once __DIR__.'/vendor/autoload.php';

// Chỉ định thư mục `templates` (nơi Twig sẽ biên dịch cú pháp Twig thành các đoạn code PHP)
$loader = new Twig_Loader_Filesystem(__DIR__.'/templates');

 // Khởi tạo Twig
$twig = new Twig_Environment($loader);
```

## Step 2: tạo thư mục để chứa các templates sử dụng Twig
- Tạo mới thư mục `/templates`
```
+---Youtube
|   \---Backend-PHP-MySql-Twig  <- Đây là thư mục gốc của dự án, có thể tự đặt tên
|       +---templates           <- Tạo thư mục
```

# 3.Tạo ví dụ 1 làm quen `Twig Template Engine`
## Luồng xử lý của Template Engine thường thấy
<p align="center">
  <img src="../images/TwigTemplateDataFlow.png" width="700">
</p>

## Step 1:
- Tạo file `/vidu01.php`
```
+---Youtube
|   \---Backend-PHP-MySql-Twig  <- Đây là thư mục gốc của dự án, có thể tự đặt tên
|       +---vidu1.php           <- Tạo file
```
- Nội dung file:
```php
<?php
// Include file cấu hình ban đầu của `Twig`
require_once __DIR__.'/bootstrap.php';

// Tạo danh sách sản phẩm mẫu
// Các bạn có thể viết các câu lệnh truy xuất vào database để lấy dữ liệu, ...
$products = [
    [
        'name'          => 'Dell',
        'description'   => 'Core i7',
        'price'         =>  800.00,
        'date_register' => '2017-06-22',
    ],
    [
        'name'          => 'Mouse',
        'description'   => 'Razer',
        'price'         =>  125.00,
        'date_register' => '2019-10-25',
    ],
    [
        'name'          => 'Keyboard',
        'description'   => 'Mechanical Keyboard',
        'price'         =>  250.00,
        'date_register' => '2018-06-23',
    ],
];

// Yêu cầu `Twig` vẽ giao diện được viết trong file `vidu1.html.twig`
// với dữ liệu truyền vào file giao diện được đặt tên là `products`
echo $twig->render('vidu01.html.twig', ['products' => $products] );
```

## Step 2:
- Tạo file `/vidu01.php`
```
+---Youtube
|   \---Backend-PHP-MySql-Twig             <- Đây là thư mục gốc của dự án, có thể tự đặt tên
|       +---templates           
|           +---vidu01.html.twig           <- Tạo file
```
- Nội dung file:
```html
<!DOCTYPE html>
<html lang="vi-VN">
    <head>
        <meta charset="UTF-8">
        <title>Twig Example</title>
    </head>
    <body>
    <table border="1" style="width: 100%;">
        <thead>
            <tr>
                <td>Product</td>
                <td>Description</td>
                <td>Price</td>
                <td>Date</td>
            </tr>
        </thead>
        <tbody>
            {% for product in products %}
                <tr>
                    <td>{{ product.name }}</td>
                    <td>{{ product.description }}</td>
                    <td>{{ product.price }}</td>
                    <td>{{ product.date_register|date("d/m/Y") }}</td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
    </body>
</html>
```

## Step 3: Kiểm tra ứng dụng
- Truy cập địa chỉ: [http://localhost/Youtube/Backend-PHP-MySql-Twig/vidu01.php](http://localhost/Youtube/Backend-PHP-MySql-Twig/vidu01.php)

# Bài học trước
[Giới thiệu - Cài đặt](../Chapter2/Readme-Bai2.md)
# Bài học tiếp theo
[Bài học 2](../Chapter3/Readme-Bai1.md)