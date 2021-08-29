# Chương 2-Bài 2. Tìm hiểu về framework twig

## Twig
- `Twig` là một Template Engine nổi tiếng của Symfony.
- Cú pháp của `Twig` khá dễ học. Về cơ bản chỉ có các thành phần sau:
    - Sử dụng `{{ variable }}` để render giá trị thay thế cho dòng lệnh thường thấy của php thuần `<?php echo $variable; ?>`
    - Sử dụng `{% logic %}` cho các xử lý dạng logic `if; loop; while`
    - Sử dụng `{# comment #}` cho các ghi chú (comments)
    - ...
- Đoạn code mẫu
    ```
        <!DOCTYPE html>
    <html>
        <head>
            <title>My Webpage</title>
        </head>
        <body>
            <ul id="navigation">
            {% for item in navigation %}
                <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
            {% endfor %}
            </ul>

            <h1>My Webpage</h1>
            {{ a_variable }}
        </body>
    </html>
    ```
- Tài liệu tham khảo:
    - Cú pháp sử dụng Twig version 2x: [https://twig.symfony.com/doc/2.x/templates.html](https://twig.symfony.com/doc/2.x/templates.html)
    - Cú pháp sử dụng Twig version 3x: [https://twig.symfony.com/doc/3.x/templates.html](https://twig.symfony.com/doc/3.x/templates.html)

## 1.Cài đặt TWIG
### Step 1: Cài đặt `composer` (công cụ quản lý các gói package PHP):
- Download: [https://getcomposer.org/download/](https://getcomposer.org/download/)
- Chọn Window Installer để cài đặt.

### Step 2: Cài đặt thư viện `twig/twig` thông qua `composer`:
- Chạy câu lệnh sau:
```
composer require twig/twig
```
- Cấu trúc thư mục sau khi cài đặt:
```
+---php
|   \---twig                    <- Đây là thư mục gốc của dự án, các bạn có thể đặt tên các bạn...
|       \---vendor
|           +---composer
|           +---symfony
|           +---twig
|           +---twig
|           \---autoload.php
|       +---composer.json
|       \---composer.lock
```

### Step 3: Cài đặt thư viện `symfony/var-dumper` thông qua `composer`:
- Chạy câu lệnh sau:
```
composer require symfony/var-dumper
```

# Bài học trước
[Bài học 2](./Chapter2/Readme-Bai1.md)
# Bài học tiếp theo
[Bài học 4](../Chapter2/Readme-Bai3.md)