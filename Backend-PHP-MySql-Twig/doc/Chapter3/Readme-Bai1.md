# Chương 3-Bài 1. Thiết kế bố cục (layouts) cho giao diện Backend

- Để không xảy ra việc dư thừa code ta thiết kế layout để tái sử dụng lại những phần code giống nhau mà không phải code nhiều lần.
- Mỗi ứng dụng web thường sẽ có một `bố cục (layout)` đồng nhất về giao diện.
  - `Layout backend`: bố cục dùng cho trang Quản trị (admin).
  - `Layout frontend`: bố cục dùng cho trang Hiển thị đối với client (khách hàng).
- Ý tưởng sử dụng `bố cục (layout)` là để có thể kế thừa lại giao diện; sử dụng cùng lúc nhiều nơi trong các trang của ứng dụng; dễ dàng tùy chỉnh bố cục khi cần thiết;...
- Cách thực hiện thường thấy:
  - Ứng dụng web sẽ tạo 1 `layout chung` cho toàn ứng dụng web.
  - Các `trang (hay chức năng)` của ứng dụng sẽ kế thừa `layout chung` và nhúng các thành phần giao diện tương ứng với `trang (hay chức năng)` vào thành phần đã `đục lỗ (hay chừa chỗ sẵn)` trong `layout chung`.

# Cách 1 tự custom layout

## Step 1: chuẩn bị thư viện backend và frontend để tạo bố cục trang web

- Chúng ta sẽ sử dụng một số thư viện giao diện nổi tiếng như sau:
  - Bootstrap 4.3 (mới nhất hiện nay). [Bootstrap 4 examples](https://getbootstrap.com/docs/4.3/examples/)
  - Jquery 3.3.1 (mới nhất hiện nay). [Jquery 3.3.1](https://jquery.com/download/)
  - PopperJS. [PopperJS](https://popper.js.org/)
  - Feather icon. [Feather icon](https://feathericons.com/)

### Step 1.1. Cài đặt Bootstrap 4.3.1

- Truy cập trang chủ để xem hướng dẫn - [Starter template](https://getbootstrap.com/docs/4.3/getting-started/introduction/)
- [Download Bootstrap 4.3.1](https://github.com/twbs/bootstrap/archive/v4.3.1.zip)
- Download về, giải nén, copy thư mục `dist` vào trong thư mục `/Youtube/Backend-PHP-MySql-Twig/assets/vendor/` và đổi tên thư mục `dist` thành `bootstrap`.
- Để dễ dàng quản lý các thư viện Frontend, chúng ta sẽ tạo cấu trúc thư mục như sau:

```
+---assets
|   \---vendor
|       \---bootstrap   <- copy thư mục `dist`, đổi tên thành `bootstrap`
|           +---css
|           \---js
|       ...
|       \***Các gói thư viện backend khác
```

### Step 1.2. Cài đặt Jquery

- [Download Jquery](https://code.jquery.com/jquery-3.3.1.min.js)
- Download về, chép vào thư mục như cấu trúc sau:

```
+---assets
|   \---vendor
|       \---jquery              <- tạo thư mục jquery để tiện quản lý
|           +---jquery.min.js   <- download file về
|       ...
|       \***Các gói thư viện backend khác
```

### Step 1.3. Cài đặt PopperJS

- [PopperJS v1](https://unpkg.com/popper.js/dist/umd/popper.min.js)
- Download về, chép vào thư mục như cấu trúc sau:

```
+---assets
|   \---vendor
|       \---popperjs            <- tạo thư mục popperjs để tiện quản lý
|           +---popper.min.js   <- download file về
|       ...
|       \***Các gói thư viện backend khác
```

### Step 1.4. Cài đặt FeatherIcon

- [Feather Icon Javascript](https://unpkg.com/feather-icons/dist/feather.min.js)
- Download về, chép vào thư mục như cấu trúc sau:

```
+---assets
|   \---vendor
|       \---feather             <- tạo thư mục feather để tiện quản lý
|           +---feather.min.js  <- download file về
|       ...
|       \***Các gói thư viện backend khác
```

### Step 1.5. Chuẩn bị các file custom css, js do mình tự viết

- Trong môi trường thiết kế web, đa số chúng ta sử dụng các thư viện CSS, JS của các nhà cung cấp. Tùy theo nhu cầu sử dụng, chúng ta thường hay custom các giao diện CSS, hay có các đoạn JS tự viết để tùy chỉnh ứng dụng theo nhu cầu.
- Để thuận tiện sử dụng và không gây ảnh hưởng đến các thư viện của các nhà cung cấp. Chúng ta sẽ tạo cấu trúc thư mục như sau:

```
+---assets
|   \---backend
|       \---css
|           +---style.css               <- custom css dành cho backend
|       \---js
|           +---app.js                  <- custom js dành cho backend
|   \---frontend
|       \---css
|           +---style.css               <- custom css dành cho frontend
|       \---js
|           +---app.js                  <- custom js dành cho frontend
```

- Nội dung file `/Youtube/Backend-PHP-MySql-Twig/assets/backend/css/style.css`

```css
body {
    font-size: .875rem;
  }
  
  .feather {
    width: 16px;
    height: 16px;
    vertical-align: text-bottom;
  }
  
  /*
   * Sidebar
   */
  
  .sidebar {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    z-index: 100; /* Behind the navbar */
    padding: 48px 0 0; /* Height of navbar */
    box-shadow: inset -1px 0 0 rgba(0, 0, 0, .1);
  }
  
  .sidebar-sticky {
    position: relative;
    top: 0;
    height: calc(100vh - 48px);
    padding-top: .5rem;
    overflow-x: hidden;
    overflow-y: auto; /* Scrollable contents if viewport is shorter than content. */
  }
  
  @supports ((position: -webkit-sticky) or (position: sticky)) {
    .sidebar-sticky {
      position: -webkit-sticky;
      position: sticky;
    }
  }
  
  .sidebar .nav-link {
    font-weight: 500;
    color: #333;
  }
  
  .sidebar .nav-link .feather {
    margin-right: 4px;
    color: #999;
  }
  
  .sidebar .nav-link.active {
    color: #007bff;
  }
  
  .sidebar .nav-link:hover .feather,
  .sidebar .nav-link.active .feather {
    color: inherit;
  }
  
  .sidebar-heading {
    font-size: .75rem;
    text-transform: uppercase;
  }
  
  /*
   * Content
   */
  
  [role="main"] {
    padding-top: 133px; /* Space for fixed navbar */
  }
  
  @media (min-width: 768px) {
    [role="main"] {
      padding-top: 48px; /* Space for fixed navbar */
    }
  }
  
  /*
   * Navbar
   */
  
  .navbar-brand {
    padding-top: .75rem;
    padding-bottom: .75rem;
    font-size: 1rem;
    background-color: rgba(0, 0, 0, .25);
    box-shadow: inset -1px 0 0 rgba(0, 0, 0, .25);
  }
  
  .navbar .form-control {
    padding: .75rem 1rem;
    border-width: 0;
    border-radius: 0;
  }
  
  .form-control-dark {
    color: #fff;
    background-color: rgba(255, 255, 255, .1);
    border-color: rgba(255, 255, 255, .1);
  }
  
  .form-control-dark:focus {
    border-color: transparent;
    box-shadow: 0 0 0 3px rgba(255, 255, 255, .25);
  }
```

- Nội dung file `/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/app.js`

```js
/* globals Chart:false, feather:false */

(function () {
    'use strict'
  
    feather.replace()
}())
```

## Step 2: tạo file template quản lý bố cục ứng dụng web

- Để dễ dàng quản lý các file template về bố cục. Chúng ta tạo mới thư mục `/templates/backend/layouts`
- Tạo file `/templates/backend/layouts/layout.html.twig`

```
+---Youtube
|   \---Backend-PHP-MySql-Twig     <- Đây là thư mục gốc của dự án, các bạn có thể đặt tên các bạn...
|       \---templates
|           \---backend
|               \---layouts
|                   \---layout.html.twig    <- Tạo file
```

- Nội dung file:

```html
<!doctype html>
<html lang="vi">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/bootstrap/css/bootstrap.min.css" type="text/css" />

    <!-- Custom css - Các file css do chúng ta tự viết -->
    <link rel="stylesheet" href="/Youtube/Backend-PHP-MySql-Twig/assets/backend/css/style.css" type="text/css" />

    <!-- Block title - Đục lỗ trên giao diện bố cục chung, đặt tên là `title` -->
    <title>Admin Home Page | 
        {% block title %}
        {% endblock %}
    </title>
    <!-- End block title -->
</head>

<body>
    <nav class="navbar navbar-dark fixed-top bg-dark flex-md-nowrap p-0 shadow">
        <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="#">HVL</a>
        <input class="form-control form-control-dark w-100" type="text" placeholder="Tìm kiếm" aria-label="Search">
        <ul class="navbar-nav px-3">
            <li class="nav-item text-nowrap">
                <a class="nav-link" href="#">Đăng xuất</a>
            </li>
        </ul>
    </nav>

    <div class="container-fluid">
        <div class="row">
            <nav class="col-md-2 d-none d-md-block bg-light sidebar">
                <div class="sidebar-sticky">
                    <ul class="nav flex-column">
                        <li class="nav-item">
                            <a class="nav-link active" href="#">
                                <span data-feather="home"></span>
                                Bảng tin <span class="sr-only">(current)</span>
                            </a>
                        </li>
                    </ul>
                </div>
            </nav>

            <main role="main" class="col-md-9 ml-sm-auto col-lg-10 px-4">
                <div
                    class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom">
                      <!-- Block headline - Đục lỗ trên giao diện bố cục chung, đặt tên là `headline` -->
                      {% block headline %}
                      {% endblock %}
                      <!-- End block headline -->
                </div>

                <!-- Block content - Đục lỗ trên giao diện bố cục chung, đặt tên là `content` -->
                {% block content %}
                {% endblock %}
                <!-- End block content -->
            </main>
        </div>
    </div>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/jquery/jquery.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/popperjs/popper.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/bootstrap/js/bootstrap.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/feather/feather.min.js"></script>

    <!-- Custom script - Các file js do mình tự viết -->
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/app.js"></script>
    
    <!-- Block custom-scripts - Đục lỗ trên giao diện bố cục chung, đặt tên là `custom-scripts` -->
    {% block customscripts %}
    {% endblock %}
    <!-- End block custom-scripts -->
</body>

</html>
```

# Cách 2 sử dụng template có sẵn cắt ra theo layout
- Nếu sử dụng cách này bạn sẽ xem xét trong source mẫu phải js css bootstrap nằm ở đâu để có đường dẫn hợp lý.
- Cách này thường sử dụng vì khi làm việc theo team mỗi người mỗi mảng, khi đó bạn chỉ việc lo mảng backend thì chỉ cần lấy frontend để render dữ liệu vì thế cách tách template có sẵn hay dùng.

```
+---assets
|   \---vendor
|       \---themes              <- tạo thư mục themes để lưu các templates mẫu
|           +---Admin-template  <- Admin-template template
|           +---...             <- Các templates khác
|       ...
|       \***Các gói thư viện backend khác
```

- Nội dung file:

```html
<!DOCTYPE html>
<html lang="vi">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />

    <!-- Bootstrap -->
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/bootstrap/backend/css/bootstrap.min.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/bootstrap/backend/css/bootstrap-responsive.min.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/easypiechart/jquery.easy-pie-chart.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/backend/css/styles.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/backend/css/DT_bootstrap.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/fullcalendar/fullcalendar.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/Chart.js/Chart.min.css"
      rel="stylesheet"
      media="screen"
    />
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/modernizr-2.6.2-respond-1.1.0.min.js"></script>
    <!-- Block title - Đục lỗ trên giao diện bố cục chung, đặt tên là `title` -->
    <title>Admin Home Page| {% block title %} {% endblock %}</title>
    <!-- End block title -->
  </head>
  <body>
    <div class="navbar navbar-fixed-top">
      <div class="navbar-inner">
        <div class="container-fluid">
          <a
            class="btn btn-navbar"
            data-toggle="collapse"
            data-target=".nav-collapse"
          >
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </a>
          <a class="brand" href="#">Admin Panel</a>
          <div class="nav-collapse collapse">
            </ul>
            <ul class="nav">
              <li class="active">
                <a href="#">Dashboard</a>
              </li>
              <li class="dropdown">
                <a
                  href="#"
                  role="button"
                  class="dropdown-toggle"
                  data-toggle="dropdown"
                  >INFO<i class="caret"></i>
                </a>
                <ul class="dropdown-menu">
                  <li>
                    <a
                      tabindex="-1"
                      target="_blank"
                      href="https://linhfishcr7.wordpress.com/"
                      >News</a
                    >
                  </li>
                  <li>
                    <a tabindex="-1" href="/frontend/blog/blog.php">Blog</a>
                  </li>
                  <li>
                    <a tabindex="-1" href="/backend/calendar.php">Lịch</a>
                  </li>
                  <li class="divider"></li>
                </ul>
              </li>
            </ul>
          </div>
          <!--/.nav-collapse -->
        </div>
      </div>
    </div>
    <div class="container-fluid">
      <div class="row-fluid">
        <div class="span3" id="sidebar">
          <ul class="nav nav-list bs-docs-sidenav nav-collapse collapse">
            <li class="active">
              <a href="#"
                ><i class="icon-chevron-right"></i> Dashboard</a
              >
            </li>
            <li>
              <a href="/backend/calendar.php"
                ><i class="icon-chevron-right"></i> Lịch khuyến mãi</a
              >
            </li>
            <li class="dropdown">
              <a
                href="stats.html"
                role="button"
                class="dropdown-toggle"
                data-toggle="dropdown"
                ><i class="icon-chevron-right"></i>Thêm mới bảng dữ liệu</a
              >
              <ul class="dropdown-menu">
                <li>
                  <a tabindex="-1" href="/backend/nhasanxuat/create.php"
                    >Nhà Sản Xuất</a
                  >
                </li>
              </ul>
            </li>
            <li>
              <a href="/backend/khachhang/index.php"
                ><i class="icon-chevron-right"></i> Khách hàng</a
              >
            </li>
          </ul>
        </div>

        <main role="main" class="col-md-9 ml-sm-auto col-lg-10 px-4">
          <div
            class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom"
          >
            <!-- Block headline - Đục lỗ trên giao diện bố cục chung, đặt tên là `headline` -->
            {% block headline %} {% endblock %}
            <!-- End block headline -->
          </div>

          <!-- Block content - Đục lỗ trên giao diện bố cục chung, đặt tên là `content` -->
          {% block content %} {% endblock %}
          <!-- End block content -->
        </main>
      </div>
    </div>
    <!-- Optional JavaScript -->
    <!--/.fluid-container-->
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/jquery-1.9.1.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/bootstrap/backend/js/bootstrap.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/easypiechart/jquery.easy-pie-chart.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/datatables/js/jquery.dataTables.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/scripts.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/DT_bootstrap.js"></script>
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/datepicker.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/uniform.default.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/chosen.min.css"
      rel="stylesheet"
      media="screen"
    />
    <link
      href="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/wysiwyg/bootstrap-wysihtml5.css"
      rel="stylesheet"
      media="screen"
    />
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/jquery.uniform.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/chosen.jquery.min.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/bootstrap-datepicker.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/wysiwyg/wysihtml5-0.3.0.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/wysiwyg/bootstrap-wysihtml5.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/wizard/jquery.bootstrap.wizard.min.js"></script>
    <script
      type="text/javascript"
      src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/jquery-validation/dist/jquery.validate.min.js"
    ></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/form-validation.js"></script>
    <!-- calendar -->
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/jquery-ui-1.10.3.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/fullcalendar/fullcalendar.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/fullcalendar/gcal.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/backend/js/JS.js"></script>
    <script src="/Youtube/Backend-PHP-MySql-Twig/assets/vendor/themes/Admin-template/Chart.js/Chart.min.js"></script>
  </body>
</html>
```


## Step 3: tạo file template `Dashboard`

- Để dễ dàng quản lý các trang tĩnh (static). Ta sẽ tạo thư mục `/pages/` để quản lý các trang này.
- Trang `Dashboard (bảng tin)` đơn giản là một nội dung tĩnh; hoặc nếu làm tốt hơn, các bạn có thể lưu nội dung trang trong database và truy xuất; hiển thị vài báo cáo thông số cần thiết trong hệ thống...
- Tạo file `#`

```
+---Youtube
|   \---Backend-PHP-MySql-Twig     <- Đây là thư mục gốc của dự án, các bạn có thể đặt tên các bạn...
|       \---backend
|           \---pages
|               \---dashboard.php    <- Tạo file
```

- Nội dung file:

```php
<?php
// Include file cấu hình ban đầu của `Twig`
require_once __DIR__.'/../../bootstrap.php';

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

// Yêu cầu `Twig` vẽ giao diện được viết trong file `backend/pages/dashboard.html.twig`
// với dữ liệu truyền vào file giao diện được đặt tên là `products`
echo $twig->render('backend/pages/dashboard.html.twig', ['products' => $products] );
```

## Step 4: tạo file template `Dashboard` kế thừa giao diện `layout chung`

- Để dễ dàng quản lý các chức năng tương ứng. Chúng ta sẽ tạo thư mục tương ứng với chức năng
- Tạo file `/templates/backend/pages/dashboard.html.twig`

```
+---Youtube
|   \---Backend-PHP-MySql-Twig     <- Đây là thư mục gốc của dự án, các bạn có thể đặt tên các bạn...
|       \---templates
|           \---backend
|               \---pages
|                   \---dashboard.html.twig    <- Tạo file
```

- Nội dung file:

```html
{# Kế thừa layout backend #} 
{% extends "backend/layouts/layout.html.twig" %} 
{# Nội dung trong block title #} 
{% block title %} Bảng tin {% endblock %} 
{# End Nội dung trong block title #} 
{# Nội dung trong block headline #} 
{% block headline %} Bảng tin {% endblock %}
{# End Nội dung trong block headline #} 
{# Nội dung trong block content #} 
{% block content %}
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
{% endblock %} {# End Nội dung trong block content #}
```

## Step 5: Kiểm tra ứng dụng

- Truy cập địa chỉ: [http://havanlinh.tech/Youtube/Backend-PHP-MySql-Twig/](http://havanlinh.tech/Youtube/Backend-PHP-MySql-Twig/)

# Bài học trước

[Bài học 4](./Chapter2/Readme-Bai3.md)

# Bài học tiếp theo

[Bài học 6](../Chapter3/Readme-Bai2.md)
