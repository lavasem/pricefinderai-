git clone https://github.com/aivorair-arch/pricefinderai-.git
🚀 PriceFinder AI

<div align="center">موتور هوشمند مقایسه قیمت، جستجوی تصویری و تحلیل بازار

نسل جدید موتور جستجوی محصولات ایران با قابلیت مقایسه قیمت، تاریخچه قیمت، هوش مصنوعی و جستجوی تصویری.

"Version" (https://img.shields.io/badge/version-1.0-blue)
"Laravel" (https://img.shields.io/badge/Laravel-12-red)
"Next.js" (https://img.shields.io/badge/Next.js-15-black)
"License" (https://img.shields.io/badge/license-MIT-green)

</div>---

📖 معرفی

PriceFinder AI یک پلتفرم متن‌باز برای جستجوی محصولات، مقایسه قیمت فروشگاه‌های اینترنتی، مشاهده تاریخچه قیمت و جستجوی محصولات مشابه با استفاده از هوش مصنوعی است.

این پروژه با هدف ایجاد یک سامانه سریع، مقیاس‌پذیر و مدرن برای بازار ایران توسعه داده می‌شود.

---

✨ امکانات

نسخه اولیه

- ✅ ثبت‌نام و ورود کاربران
- ✅ پنل مدیریت
- ✅ مدیریت محصولات
- ✅ مدیریت برندها
- ✅ مدیریت دسته‌بندی‌ها
- ✅ مدیریت فروشگاه‌ها
- ✅ مقایسه قیمت
- ✅ جستجوی پیشرفته
- ✅ API اختصاصی

نسخه‌های بعدی

- 🔥 تاریخچه قیمت
- 🔥 نمودار تغییرات قیمت
- 🔥 اعلان کاهش قیمت
- 🔥 پنل فروشندگان
- 🔥 خزنده جمع‌آوری قیمت
- 🔥 جستجوی تصویری با هوش مصنوعی
- 🔥 جستجو با بارکد
- 🔥 پیشنهاد محصولات مشابه
- 🔥 داشبورد تحلیل بازار

---

🛠 فناوری‌های پروژه

Backend

- Laravel 12
- PHP 8.3
- PostgreSQL
- Redis
- Laravel Sanctum
- Laravel Horizon
- Filament

Frontend

- Next.js 15
- React
- TypeScript
- Tailwind CSS

سایر ابزارها

- Docker
- Nginx
- MinIO
- Meilisearch
- GitHub Actions

---

📁 ساختار پروژه

pricefinder-ai
│
├── backend
├── frontend
├── crawler
├── ai
├── docker
├── docs
└── README.md

---

🗺 نقشه راه

فاز ۱

- احراز هویت
- مدیریت کاربران
- محصولات
- برندها
- دسته‌بندی‌ها
- فروشگاه‌ها

فاز ۲

- موتور جستجو
- مقایسه قیمت
- فیلترها
- نمودار قیمت

فاز ۳

- خزنده قیمت
- صف پردازش
- اعلان کاهش قیمت

فاز ۴

- جستجوی تصویری
- پیشنهاد هوشمند
- تحلیل داده

فاز ۵

- انتشار نسخه پایدار
- Docker
- CI/CD
- استقرار روی سرور

---

🎯 هدف پروژه

ساخت یک سامانه متن‌باز، سریع و مقیاس‌پذیر که کاربران بتوانند:

- بهترین قیمت را پیدا کنند.
- محصولات مشابه را مشاهده کنند.
- تغییرات قیمت را دنبال کنند.
- با استفاده از هوش مصنوعی، تنها با یک عکس محصول موردنظر خود را پیدا کنند.

---

📜 مجوز

این پروژه تحت مجوز MIT License منتشر می‌شود.

---

<div align="center">PriceFinder AI
هوشمندتر جستجو کن، بهتر خرید کن.

</div>
git clone https://github.com/aivorair-arch/pricefinderai-.git
https://github.com/aivorair-arch/pricefinderai-.git
p.ir
Saving debug log to /var/log/letsencrypt/letsencrypt.logCertificate not yet due for renewal
                                                        You have an existing certificate that has exactly the same domains or certificate name you requested and isn't close to expiry.
(ref: /etc/letsencrypt/renewal/boardchip.ir.conf)       
What would you like to do?                              - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -                                 1: Attempt to reinstall this existing certificate
2: Renew & replace the certificate (may be subject to CA rate limits)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
cat <<'EOF' > setup.sh
#!/bin/bash
set -e
DOMAIN="boardchip.ir"
PHP_VERSION="8.3"
apt update && apt upgrade -y
apt install -y nginx mariadb-server php${PHP_VERSION}-fpm php${PHP_VERSION}-mysql php${PHP_VERSION}-xml php${PHP_VERSION}-curl php${PHP_VERSION}-mbstring php${PHP_VERSION}-zip php${PHP_VERSION}-bcmath certbot python3-certbot-nginx git unzip ufw
ufw allow 'Nginx Full'
ufw allow OpenSSH
ufw --force enable
cat <<EON > /etc/nginx/sites-available/${DOMAIN}
server {
    listen 80;
    server_name ${DOMAIN} www.${DOMAIN};
    root /var/www/${DOMAIN}/public;
    index index.php index.html;
    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php${PHP_VERSION}-fpm.sock;
    }
    location ~ /\.ht {
        deny all;
    }
}
EON
ln -s /etc/nginx/sites-available/${DOMAIN} /etc/nginx/sites-enabled/
rm -f /etc/nginx/sites-enabled/default
systemctl restart nginx
EOF

chmod +x setup.sh
./setup.sh
certbot --nginx -d boardchip.ir -d www.boardchip.ir

ssh root@87.107.129.51

<?php
/* ---------------------------------------------------------
   ENTERPRISE SEO HEAD ENGINE v3
   سازگار با: PHP 7.4+ ، هاست اشتراکی، فروشگاه‌های میکسین
   --------------------------------------------------------- */

// -------------------------
// اطلاعات محصول
// -------------------------
$baseUrl   = "https://lavasemkhangi.ir";
$canonical = $baseUrl . "/product.php?id=" . $product['id'];

$name        = trim($product['name']);
$brand       = trim($product['brand']);
$category    = trim($product['category']);
$price       = intval($product['price']);
$stock       = intval($product['stock']);
$description = strip_tags($product['description']);
$image       = $product['image'];

// -------------------------
// عنوان + توضیحات هوشمند AI‑Optimized
// -------------------------
$title = $name . " | خرید " . $brand . " با بهترین قیمت و ارسال سریع";
$desc  = mb_substr($description, 0, 160);

// اگر محصول ناموجود → عنوان مخصوص (CTR Boost)
if ($stock <= 0) {
    $title = $name . " | موجودی نامشخص • اطلاع‌رسانی موجودی";
    $desc  = "برای اطلاع‌رسانی موجود شدن «{$name}» شماره خود را ثبت کنید.";
}

// -------------------------
// Noindex هوشمند
// -------------------------
$robots = "index,follow,max-image-preview:large";

if ($stock <= 0) {
    $robots = "noindex,follow"; // از مشکلات داپلیکیت جلوگیری می‌کند
}

// -------------------------
// تولید لینک OG Image اتومات
// عکس OG با سایز استاندارد 1200×630
// -------------------------
$ogImage = $baseUrl . "/og-generator.php?id=" . $product['id'];

// اگر فایل OG Generator نداری، تصویر اصلی محصول استفاده می‌شود
if (!$product['image']) {
    $ogImage = $image;
}

// -------------------------
// Schema - Product
// -------------------------
$productSchema = [
    "@context" => "https://schema.org",
    "@type" => "Product",
    "name" => $name,
    "image" => [$image],
    "description" => $description,
    "sku" => "SKU-" . $product['id'],
    "brand" => [
        "@type" => "Brand",
        "name" => $brand
    ],
    "category" => $category,
    "offers" => [
        "@type" => "Offer",
        "url" => $canonical,
        "priceCurrency" => "IRR",
        "price" => $price,
        "availability" => $stock > 0
            ? "https://schema.org/InStock"
            : "https://schema.org/OutOfStock"
    ]
];

// -------------------------
// Schema - Breadcrumb
// -------------------------
$breadcrumbSchema = [
    "@context" => "https://schema.org",
    "@type" => "BreadcrumbList",
    "itemListElement" => [
        [
            "@type" => "ListItem",
            "position" => 1,
            "name" => "خانه",
            "item" => $baseUrl
        ],
        [
            "@type" => "ListItem",
            "position" => 2,
            "name" => $category,
            "item" => $baseUrl . "/category.php?name=" . urlencode($category)
        ],
        [
            "@type" => "ListItem",
            "position" => 3,
            "name" => $name,
            "item" => $canonical
        ]
    ]
];

// -------------------------
// Schema - FAQ هوشمند
// -------------------------
$faqSchema = [
    "@context" => "https://schema.org",
    "@type" => "FAQPage",
    "mainEntity" => [
        [
            "@type" => "Question",
            "name" => "آیا «{$name}» گارانتی دارد؟",
            "acceptedAnswer" => [
                "@type" => "Answer",
                "text" => "تمامی محصولات شامل ضمانت اصالت و سلامت فیزیکی هستند."
            ]
        ],
        [
            "@type" => "Question",
            "name" => "زمان ارسال محصول چقدر است؟",
            "acceptedAnswer" => [
                "@type" => "Answer",
                "text" => "سفارشات در کمتر از ۲۴ ساعت کاری پردازش و ارسال می‌شوند."
            ]
        ]
    ]
];

?>
<!-- ================= META CORE ================= -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title><?= htmlspecialchars($title) ?></title>
<meta name="description" content="<?= htmlspecialchars($desc) ?>">
<meta name="robots" content="<?= $robots ?>">
<link rel="canonical" href="<?= $canonical ?>">

<!-- ================= PERFORMANCE ENGINE ================= -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="dns-prefetch" href="//cdn.jsdelivr.net">
<link rel="dns-prefetch" href="//www.google-analytics.com">

<!-- Preload تصویر LCP -->
<link rel="preload" as="image" href="<?= $image ?>">

<!-- ================= SOCIAL / OG ================= -->
<meta property="og:type" content="product">
<meta property="og:title" content="<?= htmlspecialchars($title) ?>">
<meta property="og:description" content="<?= htmlspecialchars($desc) ?>">
<meta property="og:image" content="<?= $ogImage ?>">
<meta property="og:url" content="<?= $canonical ?>">
<meta property="og:site_name" content="فروشگاه لوازم خانگی">

<!-- ================= TWITTER ================= -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="<?= htmlspecialchars($title) ?>">
<meta name="twitter:description" content="<?= htmlspecialchars($desc) ?>">
<meta name="twitter:image" content="<?= $ogImage ?>">

<!-- ================= STRUCTURED DATA ================= -->
<script type="application/ld+json">
<?= json_encode($productSchema, JSON_UNESCAPED_UNICODE|JSON_UNESCAPED_SLASHES) ?>
</script>

<script type="application/ld+json">
<?= json_encode($breadcrumbSchema, JSON_UNESCAPED_UNICODE|JSON_UNESCAPED_SLASHES) ?>
</script>

<script type="application/ld+json">
<?= json_encode($faqSchema, JSON_UNESCAPED_UNICODE|JSON_UNESCAPED_SLASHES) ?>
</script>

<!-- ================= PERFORMANCE BOOSTER ================= -->
<script>
// LazyLoad همه تصاویر
document.addEventListener("DOMContentLoaded", () => {
    document.querySelectorAll("img").forEach(img => {
        if (!img.getAttribute("loading")) img.setAttribute("loading", "lazy");
    });
});

// حذف CLS با قفل ارتفاع تصاویر
document.addEventListener("DOMContentLoaded", () => {
    document.querySelectorAll("img").forEach(img => {
        if (!img.style.aspectRatio && img.naturalWidth > 0) {
            img.style.aspectRatio = img.naturalWidth + "/" + img.naturalHeight;
        }
    });
});
</script>
#لوازم_خانگی  #آرکوپال #ارکوپال #چینی

@lavazemkhanegi_ii     👈 سفارش
.
http://rubika.ir/arkopal_arcopalفروشگاه ارکوپال آرکوپال:
@eli_admin

پیام بده این(function() {
    let products = [];
    let cards = document.querySelectorAll(".css-1j1h0gu"); // کلاس کارت محصول ترب، ممکنه تغییر کنه
    cards.forEach(card => {
        let title = card.querySelector(".css-1bn5q0h")?.innerText || "بدون عنوان";
        let price = card.querySelector(".css-1m5kx4v")?.innerText || "بدون قیمت";
        let link = card.querySelector("a")?.href || "بدون لینک";
        products.push({title, price, link});
    });
    
    // نمایش در کنسول
    console.log(products);

    // تبدیل به CSV برای کپی و ذخیره
    let csv = "Title,Price,Link\n" + products.map(p => `"${p.title}","${p.price}","${p.link}"`).join("\n");
    console.log("کپی CSV:\n", csv);
})();<!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>قیمت سرخ کن سیلور کرست 3030 اصلی | هواپز 14 لیتری 2200 وات</title>

<meta name="description" content="خرید سرخ کن سیلور کرست 3030 اصلی با ظرفیت 14 لیتر و توان 2200 وات، 12 برنامه پخت اتوماتیک، ارسال سریع، پرداخت در محل و ضمانت اصالت کالا.">

<meta name="robots" content="index, follow">
<link rel="canonical" href="https://yoursite.ir/product/silvercrest-3030">

<style>
body{font-family:Tahoma;margin:0;background:#f7f7f7;}
.container{padding:15px;background:#fff;}
h1{font-size:22px;line-height:1.6;font-weight:bold;}
h2{font-size:18px;margin-top:20px;}
p{font-size:15px;line-height:1.9;}
.images img{width:100%;border-radius:12px;margin-bottom:10px;}
ul{font-size:15px;line-height:1.9;padding-right:18px;}
.price{
font-size:22px;
color:#e74c3c;
font-weight:bold;
margin:15px 0;
background:#fff3f3;
padding:12px;
border-radius:10px;
text-align:center;
}
.sticky-buy{
position:fixed;
bottom:0;
left:0;
width:100%;
background:#ff6a00;
color:#fff;
text-align:center;
padding:16px;
font-size:18px;
font-weight:bold;
text-decoration:none;
z-index:999;
}
.space{height:80px;}
</style>
</head>

<body>

<div class="container">

<h1>قیمت سرخ کن سیلور کرست 3030 اصلی – ظرفیت 14 لیتر</h1>

<div class="images">
<img src="https://yoursite.ir/wp-content/uploads/2026/xx/silvercrest3030.jpg" alt="سرخ کن سیلور کرست 3030 اصلی 14 لیتری">
</div>

<p>
سرخ کن سیلور کرست 3030 یکی از قدرتمندترین هواپزهای بدون روغن موجود در بازار ایران است. این مدل با ظرفیت 14 لیتر واقعی و توان 2200 وات، گزینه‌ای ایده‌آل برای خانواده‌های پرجمعیت محسوب می‌شود. اگر به دنبال خرید سرخ کن بدون روغن با کیفیت بالا و مصرف انرژی مناسب هستید، مدل 3030 انتخابی هوشمندانه است.
</p>

<h2>مشخصات فنی سرخ کن سیلور کرست 3030</h2>
<ul>
<li>ظرفیت بزرگ 14 لیتر مناسب 6 تا 8 نفر</li>
<li>توان قدرتمند 2200 وات</li>
<li>دو المنت گرمایشی برای پخت یکنواخت</li>
<li>12 برنامه پخت اتوماتیک</li>
<li>قابلیت تنظیم دما از 80 تا 200 درجه</li>
<li>سیستم گردش هوای 360 درجه</li>
</ul>

<h2>مزایای خرید هواپز 3030</h2>
<p>
با استفاده از این سرخ کن می‌توانید انواع غذاها مانند مرغ سوخاری، پیتزا، کیک، سیب‌زمینی و حتی سبزیجات را بدون روغن و به صورت کاملاً سالم آماده کنید. کاهش مصرف روغن باعث حفظ سلامت خانواده و کاهش کالری غذا می‌شود.
</p>

<h2>آیا سرخ کن سیلور کرست 3030 ارزش خرید دارد؟</h2>
<p>
در مقایسه با سایر هواپزهای 14 لیتری موجود در بازار، این مدل از نظر قدرت، ظرفیت و کیفیت ساخت عملکرد بسیار خوبی دارد. اگر به دنبال یک دستگاه چندکاره با قیمت مناسب هستید، این مدل یکی از بهترین گزینه‌ها در رده قیمتی خود محسوب می‌شود.
</p>

<div class="price">
۱۰,۵۰۰,۰۰۰ تومان
</div>

</div>

<div class="space"></div>

<a href="https://yoursite.ir/product/silvercrest-3030" class="sticky-buy">
خرید فوری سرخ کن 3030 🛒
</a>

<!-- Product Schema -->
<script type="application/ld+json">
{
"@context": "https://schema.org/",
"@type": "Product",
"name": "سرخ کن سیلور کرست 3030",
"image": "https://yoursite.ir/wp-content/uploads/2026/xx/silvercrest3030.jpg",
"description": "سرخ کن سیلور کرست 3030 ظرفیت 14 لیتر با توان 2200 وات و 12 برنامه پخت",
"brand": {
"@type": "Brand",
"name": "Silvercrest"
},
"aggregateRating": {
"@type": "AggregateRating",
"ratingValue": "4.8",
"reviewCount": "38"
},
"offers": {
"@type": "Offer",
"url": "https://yoursite.ir/product/silvercrest-3030",
"priceCurrency": "IRR",
"price": "105000000",
"availability": "https://schema.org/InStock"
}
}
</script>

<!-- FAQ Schema -->
<script type="application/ld+json">
{
"@context": "https://schema.org",
"@type": "FAQPage",
"mainEntity": [{
"@type": "Question",
"name": "آیا سرخ کن سیلور کرست 3030 بدون روغن کار می‌کند؟",
"acceptedAnswer": {
"@type": "Answer",
"text": "بله این مدل با سیستم گردش هوای داغ کار می‌کند و نیاز به روغن ندارد."
}
},
{
"@type": "Question",
"name": "ظرفیت این مدل برای چند نفر مناسب است؟",
"acceptedAnswer": {
"@type": "Answer",
"text": "ظرفیت 14 لیتری این دستگاه برای 6 تا 8 نفر مناسب می‌باشد."
}
}]
}
</script>

</body>
</html><?php
header("Content-Type: text/xml; charset=utf-8");
echo '<?xml version="1.0" encoding="UTF-8"?>';

include('config.php'); // اتصال دیتابیس

// کش فید تا سرعت بالا باشه و مصرف منابع کم بشه
$cache_file = __DIR__ . '/torob-cache.xml';
$cache_time = 3600; // 1 ساعت

if(file_exists($cache_file) && (time() - filemtime($cache_file) < $cache_time)){
    // اگر کش هنوز معتبر است، مستقیم خروجی بده
    readfile($cache_file);
    exit;
}

// شروع تولید فید جدید
$xml = "<products>";

$query = mysqli_query($conn,"SELECT p.*, c.name as category 
FROM products p 
LEFT JOIN categories c ON p.category_id=c.id 
WHERE p.status='1' AND p.stock > 0");

while($row = mysqli_fetch_assoc($query)){
    $id = $row['id'];
    $name = htmlspecialchars($row['title']);
    $price = $row['price'];
    $brand = htmlspecialchars($row['brand']);
    $category = htmlspecialchars($row['category']);
    $image = "https://lavasemkhangi.ir/uploads/".$row['image'];
    $url = "https://lavasemkhangi.ir/product/".$row['slug'];

    $xml .= "
    <product>
        <id>$id</id>
        <name>$name</name>
        <price>$price</price>
        <brand>$brand</brand>
        <category>$category</category>
        <url>$url</url>
        <image>$image</image>
        <availability>instock</availability>
    </product>";
}

$xml .= "</products>";

// ذخیره کش
file_put_contents($cache_file, $xml);

// نمایش خروجی
echo $xml;
?>import os

# پوشه خروجی صفحات
output_folder = "seo_pages_final"
os.makedirs(output_folder, exist_ok=True)

# نمونه محصولات (در عمل می‌تواند از دیتابیس یا CSV بخواند)
products = [
    {
        "name": "سرخ‌کن سیلور کرست 3030",
        "category": "سرخ‌کن",
        "description": "سرخ‌کن کم‌مصرف و مدرن با طراحی شیک و تمیزکاری آسان.",
        "image": "fryer3030.jpg",
        "url": "/products/fryer-3030",
        "keywords": ["سرخ‌کن", "لوازم خانگی", "خرید آنلاین", "آشپزی آسان"]
    },
    {
        "name": "خردکن نانیوا مدل X200",
        "category": "خردکن",
        "description": "خردکن خانگی با تیغه‌های فولادی ضدزنگ و عملکرد بالا.",
        "image": "chopperX200.jpg",
        "url": "/products/chopper-x200",
        "keywords": ["خردکن", "غذاساز", "لوازم آشپزخانه", "لوازم خانگی"]
    },
    {
        "name": "جاروبرقی نانیوا مدل V12",
        "category": "جاروبرقی",
        "description": "جاروبرقی کم‌صدا با مکش قوی و فیلتر قابل شستشو.",
        "image": "vacuumV12.jpg",
        "url": "/products/vacuum-v12",
        "keywords": ["جاروبرقی", "تمیز کردن خانه", "لوازم خانگی", "کم‌صدا"]
    }
]

# دسته‌بندی‌ها برای لینک داخلی
categories = {
    "سرخ‌کن": "/categories/fryers",
    "خردکن": "/categories/choppers",
    "جاروبرقی": "/categories/vacuums"
}

# تولید محتوا طولانی خودکار برای هر محصول
def generate_long_content(product):
    return f"""
<section>
  <h2>معرفی محصول {product['name']}</h2>
  <p>{product['description']} این محصول با کیفیت عالی و طراحی مدرن برای استفاده روزمره در خانه بسیار مناسب است.</p>

  <h3>ویژگی‌های کلیدی</h3>
  <ul>
    <li>دسته‌بندی: {product['category']}</li>
    <li>کیفیت ساخت بالا و دوام طولانی</li>
    <li>استفاده آسان و تمیزکاری راحت</li>
    <li>ارسال سریع و تضمین اصالت کالا</li>
  </ul>

  <h3>مزایای استفاده از {product['category']}</h3>
  <p>با استفاده از {product['category']} مناسب، کارهای خانه راحت‌تر و سریع‌تر انجام می‌شود. این دستگاه‌ها برای صرفه‌جویی در زمان و انرژی طراحی شده‌اند و تجربه آشپزی و تمیزی خانه را لذت‌بخش می‌کنند.</p>

  <h3>نکات طلایی برای استفاده</h3>
  <ul>
    <li>بعد از استفاده، دستگاه را تمیز کنید.</li>
    <li>دستورالعمل‌های کارخانه را دنبال کنید.</li>
    <li>برای طول عمر بیشتر، دستگاه را در مکان خشک و خنک نگه دارید.</li>
  </ul>

  <h3>محصولات مرتبط</h3>
  <ul>
    <li><a href="{categories[product['category']]}">مشاهده همه {product['category']}‌ها</a></li>
  </ul>

  <h3>خرید {product['name']}</h3>
  <p>برای مشاهده قیمت و سفارش <a href="{product['url']}">اینجا کلیک کنید</a>.</p>
</section>
"""

# تولید HTML کامل با SEO خودکار
def generate_html(product):
    keywords = ", ".join(product["keywords"])
    title = f"{product['name']} | خرید {product['category']} آنلاین"
    description = product["description"]

    html_content = f"""<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{title}</title>
  <meta name="description" content="{description}">
  <meta name="keywords" content="{keywords}">
  <link rel="canonical" href="https://lavasemkhangi.ir{product['url']}">

  <script type="application/ld+json">
  {{
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "{product['name']}",
    "description": "{product['description']}",
    "image": "https://lavasemkhangi.ir/images/{product['image']}",
    "url": "https://lavasemkhangi.ir{product['url']}",
    "category": "{product['category']}"
  }}
  </script>

  <link rel="stylesheet" href="/styles.css">
</head>
<body>

<header>
  <h1>{product['name']}</h1>
</header>

<main>
  {generate_long_content(product)}
</main>

<footer>
  <p>© 2026 تمامی حقوق محفوظ است | لوازم خانگی نانیوا</p>
</footer>

</body>
</html>
"""
    return html_content

# تولید صفحات خودکار برای تمام محصولات
for product in products:
    filename = product["url"].strip("/").replace("/", "_") + ".html"
    filepath = os.path.join(output_folder, filename)
    with open(filepath, "w", encoding="utf-8") as f:
        f.write(generate_html(product))
    print(f"صفحه تولید شد: {filepath}")

print("تمام صفحات SEO خودکار و پیشرفته تولید شدند!")// npm install puppeteer node-fetch
const puppeteer = require('puppeteer');
const fetch = require('node-fetch');

// ⚙️ تنظیمات
const SITE_URL = 'https://yoursite.com/admin/products'; // صفحه محصولات میکسین
const USERNAME = 'username_اینجا';
const PASSWORD = 'password_اینجا';
const API_KEY = "API_KEY_خودت_اینجا";
const SHOP_ID = "SHOP_ID_خودت_اینجا";
const API_URL = "https://api.trebsale.com/v1/products";

// تابع ارسال محصول به ترب
async function sendProduct(product) {
    try {
        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Authorization': `Bearer ${API_KEY}`,
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            body: JSON.stringify(product)
        });
        const data = await response.json();
        if (response.ok) {
            console.log(`✅ محصول '${product.title}' ارسال شد`, data);
            return true;
        } else {
            console.error(`❌ خطا در ارسال '${product.title}':`, data);
            return false;
        }
    } catch (err) {
        console.error(`❌ خطای شبکه برای '${product.title}':`, err);
        return false;
    }
}

// تابع اصلی Puppeteer
async function run() {
    const browser = await puppeteer.launch({ headless: true });
    const page = await browser.newPage();

    // ورود به پنل میکسین
    await page.goto(SITE_URL, { waitUntil: 'networkidle2' });

    await page.type('#username', USERNAME); // جایگزین با selector واقعی
    await page.type('#password', PASSWORD);
    await page.click('#login-button'); // جایگزین با selector واقعی
    await page.waitForNavigation({ waitUntil: 'networkidle2' });

    // گرفتن محصولات جدید از جدول
    const products = await page.evaluate(() => {
        // ⚠️ باید selector واقعی جدول محصولات سایت شما جایگزین شود
        const rows = Array.from(document.querySelectorAll('table#products tbody tr'));
        return rows.map(row => ({
            title: row.querySelector('.product-title').innerText.trim(),
            price: parseInt(row.querySelector('.product-price').innerText.replace(/\D/g,'')),
            sku: row.querySelector('.product-sku').innerText.trim(),
            stock: parseInt(row.querySelector('.product-stock').innerText),
            description: row.querySelector('.product-description').innerText.trim()
        }));
    });

    console.log(`محصولات پیدا شده: ${products.length}`);

    // ارسال هر محصول به ترب
    for (const product of products) {
        await sendProduct(product);
    }

    await browser.close();
    console.log("✅ ارسال خودکار تمام شد!");
}

// اجرا هر 5 دقیقه
run();
setInterval(run, 5 * 60 * 1000);<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Dynamic Title -->
    <title>{{ product.title ?? page.title }}</title>

    <!-- Meta Description -->
    <meta name="description" content="{{ product.description_short ?? page.description }}">

    <!-- Canonical URL -->
    <link rel="canonical" href="{{ current_url }}">

    <!-- Open Graph for Social Media -->
    <meta property="og:title" content="{{ product.title ?? page.title }}">
    <meta property="og:description" content="{{ product.description_short ?? page.description }}">
    <meta property="og:type" content="{{ product ? 'product' : 'website' }}">
    <meta property="og:url" content="{{ current_url }}">
    <meta property="og:image" content="{{ product.image ?? default_image }}">

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="{{ product.title ?? page.title }}">
    <meta name="twitter:description" content="{{ product.description_short ?? page.description }}">
    <meta name="twitter:image" content="{{ product.image ?? default_image }}">

    <!-- Schema: Product -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org/",
      "@type": "{{ product ? 'Product' : 'WebSite' }}",
      "name": "{{ product.title ?? site_name }}",
      "image": "{{ product.image ?? site_logo }}",
      "description": "{{ product.description_short ?? page.description }}",
      "sku": "{{ product.sku ?? '' }}",
      "brand": {
        "@type": "Brand",
        "name": "{{ product.brand ?? '' }}"
      },
      "offers": {
        "@type": "Offer",
        "url": "{{ current_url }}",
        "priceCurrency": "IRR",
        "price": "{{ product.price ?? '' }}",
        "availability": "https://schema.org/InStock"
      }
    }
    </script>

    <!-- Favicon -->
    <link rel="icon" type="image/png" href="/favicon.png">

    <!-- Preload Speed Optimization -->
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link rel="preload" as="image" href="{{ product.image ?? default_banner }}">

</head>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Dynamic Title -->
    <title>{{ product.title ?? page.title }}</title>

    <!-- Meta Description -->
    <meta name="description" content="{{ product.description_short ?? page.description }}">

    <!-- Canonical URL -->
    <link rel="canonical" href="{{ current_url }}">

    <!-- Open Graph for Social Media -->
    <meta property="og:title" content="{{ product.title ?? page.title }}">
    <meta property="og:description" content="{{ product.description_short ?? page.description }}">
    <meta property="og:type" content="{{ product ? 'product' : 'website' }}">
    <meta property="og:url" content="{{ current_url }}">
    <meta property="og:image" content="{{ product.image ?? default_image }}">

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="{{ product.title ?? page.title }}">
    <meta name="twitter:description" content="{{ product.description_short ?? page.description }}">
    <meta name="twitter:image" content="{{ product.image ?? default_image }}">

    <!-- Schema: Product -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org/",
      "@type": "{{ product ? 'Product' : 'WebSite' }}",
      "name": "{{ product.title ?? site_name }}",
      "image": "{{ product.image ?? site_logo }}",
      "description": "{{ product.description_short ?? page.description }}",
      "sku": "{{ product.sku ?? '' }}",
      "brand": {
        "@type": "Brand",
        "name": "{{ product.brand ?? '' }}"
      },
      "offers": {
        "@type": "Offer",
        "url": "{{ current_url }}",
        "priceCurrency": "IRR",
        "price": "{{ product.price ?? '' }}",
        "availability": "https://schema.org/InStock"
      }
    }
    </script>

    <!-- Favicon -->
    <link rel="icon" type="image/png" href="/favicon.png">

    <!-- Preload Speed Optimization -->
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link rel="preload" as="image" href="{{ product.image ?? default_banner }}">

</head>
/* شبکه محصولات 4 ستونه شفاف */
.products,
.product-list,
.products-grid {
  display: grid !important;
  grid-template-columns: repeat(4, 1fr);
  gap: 18px;
}

/* موبایل و تبلت */
@media (max-width: 992px) {
  .products,
  .product-list,
  .products-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* کارت محصول */
.product,
.product-card {
  background: #ffffff;
  border: 1px solid #eeeeee;
  border-radius: 12px;
  padding: 12px;
}

/* عکس محصول */
.product img,
.product-card img {
  width: 100%;
  border-radius: 10px;
}

/* قیمت */
.price {
  font-size: 18px;
  font-weight: bold;
  color: #1b5e20;
}

/* دکمه خرید */
.add-to-cart,
button[type="submit"] {
  background-color: #2e7d32;
  color: #ffffff;
  border-radius: 8px;
  padding: 10px;
}xml_add($dom_g, $item, "g:link", $p['link']);
    xml_add($dom_g, $item, "g:image_link", $p['image']);
    xml_add($dom_g, $item, "g:brand", $p['brand']);
    xml_add($dom_g, $item, "g:price", $p['price'] . " IRR");
    xml_add($dom_g, $item, "g:availability", "in stock");

    $channel->appendChild($item);
}

$rss->appendChild($channel);
$dom_g->appendChild($rss);
$dom_g->save($google_feed_file);

log_msg("INFO", "Google feed generated.");


// =====================================================
// آپلود خودکار فید به ترب
// =====================================================
$ch = curl_init();
curl_setopt_array($ch, [
    CURLOPT_URL => $torob_api,
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => [
        'feed_file' => new CURLFile($torob_feed_file)
    ],
    CURLOPT_RETURNTRANSFER => true
]);

$response = curl_exec($ch);
$error = curl_error($ch);
curl_close($ch);

if ($error) {
    log_msg("ERROR", "Torob upload failed: $error");
    exit("Torob upload failed.");
}

log_msg("INFO", "Torob upload OK. Response: $response");


// =====================================================
// پینگ خودکار گوگل جهت بروزرسانی
// =====================================================
$ping_url = "https://www.google.com/ping?sitemap=" . urlencode("https://lavasemkhangi.ir/google-feed.xml");
@file_get_contents($ping_url);
log_msg("INFO", "Google ping sent.");

echo "Feed built, uploaded to Torob, and Google notified.";
?>// npm install puppeteer node-fetch
const puppeteer = require('puppeteer');
const fetch = require('node-fetch');

// ⚙️ تنظیمات
const SITE_URL = 'https://yoursite.com/admin/products'; // صفحه محصولات میکسین
const USERNAME = 'username_اینجا';
const PASSWORD = 'password_اینجا';
const API_KEY = "API_KEY_خودت_اینجا";
const SHOP_ID = "SHOP_ID_خودت_اینجا";
const API_URL = "https://api.trebsale.com/v1/products";

// تابع ارسال محصول به ترب
async function sendProduct(product) {
    try {
        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Authorization': `Bearer ${API_KEY}`,
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            body: JSON.stringify(product)
        });
        const data = await response.json();
        if (response.ok) {
            console.log(`✅ محصول '${product.title}' ارسال شد`, data);
            return true;
        } else {
            console.error(`❌ خطا در ارسال '${product.title}':`, data);
            return false;
        }
    } catch (err) {
        console.error(`❌ خطای شبکه برای '${product.title}':`, err);
        return false;
    }
}

// تابع اصلی Puppeteer
async function run() {
    const browser = await puppeteer.launch({ headless: true });
    const page = await browser.newPage();

    // ورود به پنل میکسین
    await page.goto(SITE_URL, { waitUntil: 'networkidle2' });

    await page.type('#username', USERNAME); // جایگزین با selector واقعی
    await page.type('#password', PASSWORD);
    await page.click('#login-button'); // جایگزین با selector واقعی
    await page.waitForNavigation({ waitUntil: 'networkidle2' });

    // گرفتن محصولات جدید از جدول
    const products = await page.evaluate(() => {
        // ⚠️ باید selector واقعی جدول محصولات سایت شما جایگزین شود
        const rows = Array.from(document.querySelectorAll('table#products tbody tr'));
        return rows.map(row => ({
            title: row.querySelector('.product-title').innerText.trim(),
            price: parseInt(row.querySelector('.product-price').innerText.replace(/\D/g,'')),
            sku: row.querySelector('.product-sku').innerText.trim(),
            stock: parseInt(row.querySelector('.product-stock').innerText),
            description: row.querySelector('.product-description').innerText.trim()
        }));
    });

    console.log(`محصولات پیدا شده: ${products.length}`);

    // ارسال هر محصول به ترب
    for (const product of products) {
        await sendProduct(product);
    }

    await browser.close();
    console.log("✅ ارسال خودکار تمام شد!");
}

// اجرا هر 5 دقیقه
run();
setInterval(run, 5 * 60 * 1000);(function() {
    let products = [];
    let cards = document.querySelectorAll(".css-1j1h0gu"); // کلاس کارت محصول ترب، ممکنه تغییر کنه
    cards.forEach(card => {
        let title = card.querySelector(".css-1bn5q0h")?.innerText || "بدون عنوان";
        let price = card.querySelector(".css-1m5kx4v")?.innerText || "بدون قیمت";
        let link = card.querySelector("a")?.href || "بدون لینک";
        products.push({title, price, link});
    });
    
    // نمایش در کنسول
    console.log(products);

    // تبدیل به CSV برای کپی و ذخیره
    let csv = "Title,Price,Link\n" + products.map(p => `"${p.title}","${p.price}","${p.link}"`).join("\n");
    console.log("کپی CSV:\n", csv);
})();<!-- شروع کد سئو خودکار -->
<head>
  <!-- متا تگ‌ها -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- عنوان و توضیحات (می‌توانید با JS خودکار تغییر دهید بر اساس صفحه) -->
  <title id="seo-title">عنوان محصول یا صفحه شما</title>
  <meta name="description" id="seo-desc" content="توضیحات کوتاه محصول یا صفحه شما برای گوگل">

  <!-- متا تگ‌های ایندکس گوگل -->
  <meta name="robots" content="index, follow">
  <link rel="canonical" href="https://lavasemkhangi.ir/صفحه-فعلی" />

  <!-- فید ترب (برای اتصال خودکار محصولات) -->
  <link rel="alternate" type="application/rss+xml" title="فید ترب" href="https://lavasemkhangi.ir/feed/torob.xml">

  <!-- JSON-LD داده ساختاریافته (Structured Data) برای محصولات -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "نام محصول",
    "image": [
      "لینک تصویر 1",
      "لینک تصویر 2"
    ],
    "description": "توضیحات محصول",
    "sku": "شناسه محصول",
    "brand": {
      "@type": "Brand",
      "name": "برند محصول"
    },
    "offers": {
      "@type": "Offer",
      "url": "لینک محصول",
      "priceCurrency": "IRR",
      "price": "قیمت محصول",
      "availability": "https://schema.org/InStock"
    }
  }
  </script>

  <!-- فونت و CSS عمومی -->
  <link rel="stylesheet" href="/css/main.css">
</head>
<!-- پایان کد سئو خودکار -->
<?php
require_once __DIR__.'/vendor/autoload.php'; // کتابخانه Google API

define('GOOGLE_CREDENTIALS', __DIR__.'/service-account.json'); // فایل سرویس اکانت گوگل
define('FEED_FILE', __DIR__.'/feed-torob.xml'); // فایل فید ترب

// تابع اصلی برای هر محصول
function autoSeoIndexTorob($product){
    // 1️⃣ تولید عنوان و توضیح خودکار
    $title = "خرید {$product['title']} با بهترین قیمت امروز | ارسال فوری | لوازم خانگی و آشپزخانه برقی";
    $description = "اگر قصد خرید {$product['title']} با بهترین قیمت و ضمانت اصالت را دارید، این محصول یکی از پرفروش‌ترین لوازم خانگی و آشپزخانه برقی ایران است.";

    // 2️⃣ تولید اسکیما JSON-LD
    $schema = [
        "@context"=>"https://schema.org/",
        "@type"=>"Product",
        "name"=>$product['title'],
        "image"=>$product['image'],
        "description"=>substr(strip_tags($description),0,500),
        "sku"=>$product['sku'] ?? '',
        "brand"=>["@type"=>"Brand","name"=>$product['brand']],
        "offers"=>[
            "@type"=>"Offer",
            "url"=>$product['url'],
            "priceCurrency"=>"IRR",
            "price"=>$product['price'],
            "availability"=>"https://schema.org/InStock"
        ]
    ];
    echo '<script type="application/ld+json">'.json_encode($schema, JSON_UNESCAPED_UNICODE).'</script>';

    // 3️⃣ آپدیت خودکار فید ترب
    $feedXml = simplexml_load_file(FEED_FILE) ?: new SimpleXMLElement('<products/>');
    $productXml = $feedXml->addChild('product');
    $productXml->addChild('name',$product['title']);
    $productXml->addChild('url',$product['url']);
    $productXml->addChild('price',$product['price']);
    $productXml->addChild('image',$product['image']);
    $productXml->addChild('brand',$product['brand']);
    $productXml->addChild('availability','instock');
    $productXml->addChild('description',strip_tags($description));
    $feedXml->asXML(FEED_FILE);

    // 4️⃣ ارسال خودکار ایندکس گوگل
    $client = new Google_Client();
    $client->setAuthConfig(GOOGLE_CREDENTIALS);
    $client->addScope('https://www.googleapis.com/auth/indexing');

    $indexingService = new Google_Service_Indexing($client);
    $urlNotification = new Google_Service_Indexing_UrlNotification();
    $urlNotification->setUrl($product['url']);
    $urlNotification->setType("URL_UPDATED");

    try {
        $indexingService->urlNotifications->publish($urlNotification);
    } catch(Exception $e){
        error_log("Indexing API error: ".$e->getMessage());
    }
}

// تابع گرفتن 100 محصول پرفروش میکسین (خودکار)
function get_top_100_products(){
    // اینجا با دیتابیس میکسین ارتباط داره
    // و 100 محصول پرفروش رو برمیگردونه
    return query_top_100_products_from_db(); // فرضی
}

// اجرای خودکار روی همه محصولات
$products = get_top_100_products();
foreach($products as $product){
    autoSeoIndexTorob($product);
}
?>
<?php  
use Illuminate\Http\Request;  
use Illuminate\Support\Facades\Http;  
use App\Models\Product;  
use PhpOffice\PhpSpreadsheet\Spreadsheet;  
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;  
  
class ProductAIController extends Controller  
{  
    // اضافه کردن محصول و تولید محتوا هوشمند  
    public function addProduct(Request $request)  
    {  
        $title = $request->input('title');  
  
        // Prompt برای GPT  
        $prompt = "  
عنوان محصول: $title  
یک توضیح کامل و SEO شده بنویس، شامل:  
- توضیح کوتاه  
- توضیح بلند  
- کلمات کلیدی SEO  
- Meta Description  
فرمت JSON بده:  
{\"short_description\":\"...\",\"description\":\"...\",\"seo_keywords\":\"...\",\"meta_description\":\"...\"}  
";  
  
        // درخواست به GPT  
        $response = Http::withHeaders([  
            'Authorization' => 'Bearer YOUR_OPENAI_KEY'  
        ])->post('https://api.openai.com/v1/chat/completions', [  
            'model' => 'gpt-4.1-mini',  
            'messages' => [  
                ['role' => 'user', 'content' => $prompt]  
            ],  
            'temperature' => 0.7  
        ]);  
  
        $content = $response->json();  
        $json_data = json_decode($content['choices'][0]['message']['content'], true);  
  
        // ذخیره در دیتابیس میکسین  
        $product = new Product();  
        $product->title = $title;  
        $product->short_description = $json_data['short_description'] ?? '';  
        $product->description = $json_data['description'] ?? '';  
        $product->seo_keywords = $json_data['seo_keywords'] ?? '';  
        $product->meta_description = $json_data['meta_description'] ?? '';  
        $product->save();  
  
        // ساخت Excel خروجی برای ترب  
        $spreadsheet = new Spreadsheet();  
        $sheet = $spreadsheet->getActiveSheet();  
        $sheet->setCellValue('A1', 'Title');  
        $sheet->setCellValue('B1', 'Short Description');  
        $sheet->setCellValue('C1', 'Description');  
        $sheet->setCellValue('D1', 'SEO Keywords');  
        $sheet->setCellValue('E1', 'Meta Description');  
  
        $sheet->setCellValue('A2', $product->title);  
        $sheet->setCellValue('B2', $product->short_description);  
        $sheet->setCellValue('C2', $product->description);  
        $sheet->setCellValue('D2', $product->seo_keywords);  
        $sheet->setCellValue('E2', $product->meta_description);  
  
        $writer = new Xlsx($spreadsheet);  
        $excel_file = storage_path('app/public/products.xlsx');  
        $writer->save($excel_file);  
  
        return response()->json([  
            'status' => 'success',  
            'product' => $product,  
            'excel' => url('storage/products.xlsx')  
        ]);  
    }  
}

<?php
namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\Http;
use App\Models\Product;
use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

class AutoProductAI extends Command
{
    protected $signature = 'products:ai-auto';
    protected $description = 'تولید خودکار محتوا و Excel روزانه برای محصولات جدید';

    public function handle()
    {
        $this->info("شروع پردازش محصولات جدید...");

        $products = Product::whereNull('description')->get();

        if ($products->isEmpty()) {
            $this->info("محصول جدیدی برای پردازش وجود ندارد.");
            return;
        }

        foreach ($products as $product) {
            $title = $product->title;

            $prompt = "
عنوان محصول: $title
یک توضیح کامل و SEO شده بنویس، شامل:
- توضیح کوتاه
- توضیح بلند
- کلمات کلیدی SEO
- Meta Description
فرمت خروجی JSON بده:
{\"short_description\":\"...\",\"description\":\"...\",\"seo_keywords\":\"...\",\"meta_description\":\"...\"}
";

            try {
                $response = Http::withHeaders([
                    'Authorization' => 'Bearer ' . env('OPENAI_API_KEY')
                ])->post('https://api.openai.com/v1/chat/completions', [
                    'model' => 'gpt-4.1-mini',
                    'messages' => [
                        ['role' => 'user', 'content' => $prompt]
                    ],
                    'temperature' => 0.7
                ]);

                $content = $response->json();
                $json_data = json_decode($content['choices'][0]['message']['content'], true);

                $product->short_description = $json_data['short_description'] ?? '';
                $product->description = $json_data['description'] ?? '';
                $product->seo_keywords = $json_data['seo_keywords'] ?? '';
                $product->meta_description = $json_data['meta_description'] ?? '';
                $product->save();

                $this->info("پردازش شد: $title");

            } catch (\Exception $e) {
                $this->error("خطا برای محصول $title: " . $e->getMessage());
            }
        }

        // خروجی Excel برای ترب
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Title');
        $sheet->setCellValue('B1', 'Short Description');
        $sheet->setCellValue('C1', 'Description');
        $sheet->setCellValue('D1', 'SEO Keywords');
        $sheet->setCellValue('E1', 'Meta Description');

        $row = 2;
        foreach (Product::all() as $product) {
            $sheet->setCellValue("A$row", $product->title);
            $sheet->setCellValue("B$row", $product->short_description);
            $sheet->setCellValue("C$row", $product->description);
            $sheet->setCellValue("D$row", $product->seo_keywords);
            $sheet->setCellValue("E$row", $product->meta_description);
            $row++;
        }

        $writer = new Xlsx($spreadsheet);
        $excel_file = storage_path('app/public/products.xlsx');
        $writer->save($excel_file);

        $this->info("Excel خروجی ساخته شد: " . $excel_file);
        $this->info("پردازش روزانه تمام شد ✅");
    }
}
<script>
(async function() {
  try {
    const visited = new Set();
    
    async function fetchPage(url) {
      if (visited.has(url)) return;
      visited.add(url);

      const res = await fetch(url);
      const html = await res.text();
      const parser = new DOMParser();
      const doc = parser.parseFromString(html, 'text/html');

      // استخراج لینک محصولات و دسته‌بندی‌ها
      const links = Array.from(doc.querySelectorAll('a[href]'))
                         .map(a => a.href)
                         .filter(h => h.includes('/product/') || h.includes('/category/'))
                         .filter((v,i,a)=>a.indexOf(v)===i); // حذف تکراری‌ها

      for (const link of links) {
        await fetchPage(link); // بازگشت به همه لینک‌ها
      }

      // اگر این صفحه محصول است
      if (url.includes('/product/')) {
        const name = doc.querySelector('h1')?.innerText || "نام محصول";
        const price = doc.querySelector('.price')?.innerText.replace(/[^\d]/g,'') || "0";
        const image = doc.querySelector('img')?.src || "https://lavasemkhangi.ir/logo.png";
        const description = doc.querySelector('p')?.innerText || "توضیح کوتاه محصول";

        const schema = {
          "@context": "https://schema.org/",
          "@type": "Product",
          "name": name,
          "image": image,
          "description": description,
          "offers": {
            "@type": "Offer",
            "priceCurrency": "IRR",
            "price": price,
            "availability": "https://schema.org/InStock",
            "url": url
          }
        };

        const script = document.createElement("script");
        script.type = "application/ld+json";
        script.textContent = JSON.stringify(schema);
        document.head.appendChild(script);
      }
    }

    // شروع از صفحه اصلی
    await fetchPage(window.location.origin);

    console.log("🔥 SEO انفجاری خودکار همه محصولات ساخته شد!");
  } catch (e) {
    console.error("❌ خطا در ساخت SEO انفجاری:", e);
  }
})();
</script>

<?php
/**
 * Auto Index & Sixml_add($dom_g, $item, "g:link", $p['link']);
    xml_add($dom_g, $item, "g:image_link", $p['image']);
    xml_add($dom_g, $item, "g:brand", $p['brand']);
    xml_add($dom_g, $item, "g:price", $p['price'] . " IRR");
    xml_add($dom_g, $item, "g:availability", "in stock");

    $channel->appendChild($item);
}

$rss->appendChild($channel);
$dom_g->appendChild($rss);
$dom_g->save($google_feed_file);

log_msg("INFO", "Google feed generated.");


// =====================================================
// آپلود خودکار فید به ترب
// =====================================================
$ch = curl_init();
curl_setopt_array($ch, [
    CURLOPT_URL => $torob_api,
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => [
        'feed_file' => new CURLFile($torob_feed_file)
    ],
    CURLOPT_RETURNTRANSFER => true
]);

$response = curl_exec($ch);
$error = curl_error($ch);
curl_close($ch);

if ($error) {
    log_msg("ERROR", "Torob upload failed: $error");
    exit("Torob upload failed.");
}

log_msg("INFO", "Torob upload OK. Response: $response");


// =====================================================
// پینگ خودکار گوگل جهت بروزرسانی
// =====================================================
$ping_url = "https://www.google.com/ping?sitemap=" . urlencode("https://lavasemkhangi.ir/google-feed.xml");
@file_get_contents($ping_url);
log_msg("INFO", "Google ping sent.");

echo "Feed built, uploaded to Torob, and Google notified.";
?><!-- شروع کد سئو خودکار -->
<head>
  <!-- متا تگ‌ها -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- عنوان و توضیحات (می‌توانید با JS خودکار تغییر دهید بر اساس صفحه) -->
  <title id="seo-title">عنوان محصول یا صفحه شما</title>
  <meta name="description" id="seo-desc" content="توضیحات کوتاه محصول یا صفحه شما برای گوگل">

  <!-- متا تگ‌های ایندکس گوگل -->
  <meta name="robots" content="index, follow">
  <link rel="canonical" href="https://lavasemkhangi.ir/صفحه-فعلی" />

  <!-- فید ترب (برای اتصال خودکار محصولات) -->
  <link rel="alternate" type="application/rss+xml" title="فید ترب" href="https://lavasemkhangi.ir/feed/torob.xml">

  <!-- JSON-LD داده ساختاریافته (Structured Data) برای محصولات -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "نام محصول",
    "image": [
      "لینک تصویر 1",
      "لینک تصویر 2"
    ],
    "description": "توضیحات محصول",
    "sku": "شناسه محصول",
    "brand": {
      "@type": "Brand",
      "name": "برند محصول"
    },
    "offers": {
      "@type": "Offer",
      "url": "لینک محصول",
      "priceCurrency": "IRR",
      "price": "قیمت محصول",
      "availability": "https://schema.org/InStock"
    }
  }
  </script>

  <!-- فونت و CSS عمومی -->
  <link rel="stylesheet" href="/css/main.css">
</head>
<!-- پایان کد سئو خودکار -->
<?php
require_once __DIR__.'/vendor/autoload.php'; // کتابخانه Google API

define('GOOGLE_CREDENTIALS', __DIR__.'/service-account.json'); // فایل سرویس اکانت گوگل
define('FEED_FILE', __DIR__.'/feed-torob.xml'); // فایل فید ترب

// تابع اصلی برای هر محصول
function autoSeoIndexTorob($product){
    // 1️⃣ تولید عنوان و توضیح خودکار
    $title = "خرید {$product['title']} با بهترین قیمت امروز | ارسال فوری | لوازم خانگی و آشپزخانه برقی";
    $description = "اگر قصد خرید {$product['title']} با بهترین قیمت و ضمانت اصالت را دارید، این محصول یکی از پرفروش‌ترین لوازم خانگی و آشپزخانه برقی ایران است.";

    // 2️⃣ تولید اسکیما JSON-LD
    $schema = [
        "@context"=>"https://schema.org/",
        "@type"=>"Product",
        "name"=>$product['title'],
        "image"=>$product['image'],
        "description"=>substr(strip_tags($description),0,500),
        "sku"=>$product['sku'] ?? '',
        "brand"=>["@type"=>"Brand","name"=>$product['brand']],
        "offers"=>[
            "@type"=>"Offer",
            "url"=>$product['url'],
            "priceCurrency"=>"IRR",
            "price"=>$product['price'],
            "availability"=>"https://schema.org/InStock"
        ]
    ];
    echo '<script type="application/ld+json">'.json_encode($schema, JSON_UNESCAPED_UNICODE).'</script>';

    // 3️⃣ آپدیت خودکار فید ترب
    $feedXml = simplexml_load_file(FEED_FILE) ?: new SimpleXMLElement('<products/>');
    $productXml = $feedXml->addChild('product');
    $productXml->addChild('name',$product['title']);
    $productXml->addChild('url',$product['url']);
    $productXml->addChild('price',$product['price']);
    $productXml->addChild('image',$product['image']);
    $productXml->addChild('brand',$product['brand']);
    $productXml->addChild('availability','instock');
    $productXml->addChild('description',strip_tags($description));
    $feedXml->asXML(FEED_FILE);

    // 4️⃣ ارسال خودکار ایندکس گوگل
    $client = new Google_Client();
    $client->setAuthConfig(GOOGLE_CREDENTIALS);
    $client->addScope('https://www.googleapis.com/auth/indexing');

    $indexingService = new Google_Service_Indexing($client);
    $urlNotification = new Google_Service_Indexing_UrlNotification();
    $urlNotification->setUrl($product['url']);
    $urlNotification->setType("URL_UPDATED");

    try {
        $indexingService->urlNotifications->publish($urlNotification);
    } catch(Exception $e){
        error_log("Indexing API error: ".$e->getMessage());
    }
}

// تابع گرفتن 100 محصول پرفروش میکسین (خودکار)
function get_top_100_products(){
    // اینجا با دیتابیس میکسین ارتباط داره
    // و 100 محصول پرفروش رو برمیگردونه
    return query_top_100_products_from_db(); // فرضی
}

// اجرای خودکار روی همه محصولات
$products = get_top_100_products();
foreach($products as $product){
    autoSeoIndexTorob($product);
}
?>
<?php  
use Illuminate\Http\Request;  
use Illuminate\Support\Facades\Http;  
use App\Models\Product;  
use PhpOffice\PhpSpreadsheet\Spreadsheet;  
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;  
  
class ProductAIController extends Controller  
{  
    // اضافه کردن محصول و تولید محتوا هوشمند  
    public function addProduct(Request $request)  
    {  
        $title = $request->input('title');  
  
        // Prompt برای GPT  
        $prompt = "  
عنوان محصول: $title  
یک توضیح کامل و SEO شده بنویس، شامل:  
- توضیح کوتاه  
- توضیح بلند  
- کلمات کلیدی SEO  
- Meta Description  
فرمت JSON بده:  
{\"short_description\":\"...\",\"description\":\"...\",\"seo_keywords\":\"...\",\"meta_description\":\"...\"}  
";  
  
        // درخواست به GPT  
        $response = Http::withHeaders([  
            'Authorization' => 'Bearer YOUR_OPENAI_KEY'  
        ])->post('https://api.openai.com/v1/chat/completions', [  
            'model' => 'gpt-4.1-mini',  
            'messages' => [  
                ['role' => 'user', 'content' => $prompt]  
            ],  
            'temperature' => 0.7  
        ]);  
  
        $content = $response->json();  
        $json_data = json_decode($content['choices'][0]['message']['content'], true);  
  
        // ذخیره در دیتابیس میکسین  
        $product = new Product();  
        $product->title = $title;  
        $product->short_description = $json_data['short_description'] ?? '';  
        $product->description = $json_data['description'] ?? '';  
        $product->seo_keywords = $json_data['seo_keywords'] ?? '';  
        $product->meta_description = $json_data['meta_description'] ?? '';  
        $product->save();  
  
        // ساخت Excel خروجی برای ترب  
        $spreadsheet = new Spreadsheet();  
        $sheet = $spreadsheet->getActiveSheet();  
        $sheet->setCellValue('A1', 'Title');  
        $sheet->setCellValue('B1', 'Short Description');  
        $sheet->setCellValue('C1', 'Description');  
        $sheet->setCellValue('D1', 'SEO Keywords');  
        $sheet->setCellValue('E1', 'Meta Description');  
  
        $sheet->setCellValue('A2', $product->title);  
        $sheet->setCellValue('B2', $product->short_description);  
        $sheet->setCellValue('C2', $product->description);  
        $sheet->setCellValue('D2', $product->seo_keywords);  
        $sheet->setCellValue('E2', $product->meta_description);  
  
        $writer = new Xlsx($spreadsheet);  
        $excel_file = storage_path('app/public/products.xlsx');  
        $writer->save($excel_file);  
  
        return response()->json([  
            'status' => 'success',  
            'product' => $product,  
            'excel' => url('storage/products.xlsx')  
        ]);  
    }  
}

<?php
namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\Http;
use App\Models\Product;
use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

class AutoProductAI extends Command
{
    protected $signature = 'products:ai-auto';
    protected $description = 'تولید خودکار محتوا و Excel روزانه برای محصولات جدید';

    public function handle()
    {
        $this->info("شروع پردازش محصولات جدید...");

        $products = Product::whereNull('description')->get();

        if ($products->isEmpty()) {
            $this->info("محصول جدیدی برای پردازش وجود ندارد.");
            return;
        }

        foreach ($products as $product) {
            $title = $product->title;

            $prompt = "
عنوان محصول: $title
یک توضیح کامل و SEO شده بنویس، شامل:
- توضیح کوتاه
- توضیح بلند
- کلمات کلیدی SEO
- Meta Description
فرمت خروجی JSON بده:
{\"short_description\":\"...\",\"description\":\"...\",\"seo_keywords\":\"...\",\"meta_description\":\"...\"}
";

            try {
                $response = Http::withHeaders([
                    'Authorization' => 'Bearer ' . env('OPENAI_API_KEY')
                ])->post('https://api.openai.com/v1/chat/completions', [
                    'model' => 'gpt-4.1-mini',
                    'messages' => [
                        ['role' => 'user', 'content' => $prompt]
                    ],
                    'temperature' => 0.7
                ]);

                $content = $response->json();
                $json_data = json_decode($content['choices'][0]['message']['content'], true);

                $product->short_description = $json_data['short_description'] ?? '';
                $product->description = $json_data['description'] ?? '';
                $product->seo_keywords = $json_data['seo_keywords'] ?? '';
                $product->meta_description = $json_data['meta_description'] ?? '';
                $product->save();

                $this->info("پردازش شد: $title");

            } catch (\Exception $e) {
                $this->error("خطا برای محصول $title: " . $e->getMessage());
            }
        }

        // خروجی Excel برای ترب
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Title');
        $sheet->setCellValue('B1', 'Short Description');
        $sheet->setCellValue('C1', 'Description');
        $sheet->setCellValue('D1', 'SEO Keywords');
        $sheet->setCellValue('E1', 'Meta Description');

        $row = 2;
        foreach (Product::all() as $product) {
            $sheet->setCellValue("A$row", $product->title);
            $sheet->setCellValue("B$row", $product->short_description);
            $sheet->setCellValue("C$row", $product->description);
            $sheet->setCellValue("D$row", $product->seo_keywords);
            $sheet->setCellValue("E$row", $product->meta_description);
            $row++;
        }

        $writer = new Xlsx($spreadsheet);
        $excel_file = storage_path('app/public/products.xlsx');
        $writer->save($excel_file);

        $this->info("Excel خروجی ساخته شد: " . $excel_file);
        $this->info("پردازش روزانه تمام شد ✅");
    }
}
<script>
(async function() {
  try {
    const visited = new Set();
    
    async function fetchPage(url) {
      if (visited.has(url)) return;
      visited.add(url);

      const res = await fetch(url);
      const html = await res.text();
      const parser = new DOMParser();
      const doc = parser.parseFromString(html, 'text/html');

      // استخراج لینک محصولات و دسته‌بندی‌ها
      const links = Array.from(doc.querySelectorAll('a[href]'))
                         .map(a => a.href)
                         .filter(h => h.includes('/product/') || h.includes('/category/'))
                         .filter((v,i,a)=>a.indexOf(v)===i); // حذف تکراری‌ها

      for (const link of links) {
        await fetchPage(link); // بازگشت به همه لینک‌ها
      }

      // اگر این صفحه محصول است
      if (url.includes('/product/')) {
        const name = doc.querySelector('h1')?.innerText || "نام محصول";
        const price = doc.querySelector('.price')?.innerText.replace(/[^\d]/g,'') || "0";
        const image = doc.querySelector('img')?.src || "https://lavasemkhangi.ir/logo.png";
        const description = doc.querySelector('p')?.innerText || "توضیح کوتاه محصول";

        const schema = {
          "@context": "https://schema.org/",
          "@type": "Product",
          "name": name,
          "image": image,
          "description": description,
          "offers": {
            "@type": "Offer",
            "priceCurrency": "IRR",
            "price": price,
            "availability": "https://schema.org/InStock",
            "url": url
          }
        };

        const script = document.createElement("script");
        script.type = "application/ld+json";
        script.textContent = JSON.stringify(schema);
        document.head.appendChild(script);
      }
    }

    // شروع از صفحه اصلی
    await fetchPage(window.location.origin);

    console.log("🔥 SEO انفجاری خودکار همه محصولات ساخته شد!");
  } catch (e) {
    console.error("❌ خطا در ساخت SEO انفجاری:", e);
  }
})();
</script>

<?php
/**
 * Auto Index & Sitemap Builder (PHP + Node.js compatible)
 * پیدا کردن صفحات PHP و HTML، اضافه کردن متا robots و ساخت sitemap.xml
 */

$siteDir = __DIR__ . '/'; // مسیر ریشه سایت
$sitemapFile = $siteDir . 'sitemap.xml';
$domain = "https://YOURDOMAIN.COM"; // دامنه واقعی سایتت

// پیدا کردن فایل‌های PHP و HTML
$rii = new RecursiveIteratorIterator(new RecursiveDirectoryIterator($siteDir));
$pages = [];
foreach ($rii as $file) {
    if ($file->isDir()){ continue; }
    if(in_array($file->getExtension(), ['php','html','htm'])){
        $pages[] = $file->getPathname();
    }
}

// اضافه کردن متا robots به صفحات PHP
foreach($pages as $page){
    if(pathinfo($page, PATHINFO_EXTENSION) == 'php'){
        $content = file_get_contents($page);
        if(strpos($content,'<meta name="robots"') === false){
            $content = preg_replace('/<head>/i', "<head>\n<meta name=\"robots\" content=\"index, follow\">\n", $content, 1);
            file_put_contents($page, $content);
        }
    }
}

// ساخت sitemap.xml
$sitemapContent = '<?xml version="1.0" encoding="UTF-8"?>' . "\n";
$sitemapContent .= '<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">' . "\n";

foreach($pages as $page){
    $relative = str_replace($siteDir, '', $page);
    $relative = str_replace('\\','/',$relative);
    $sitemapContent .= "<url>\n<loc>$domain/$relative</loc>\n<changefreq>daily</changefreq>\n<priority>0.8</priority>\n</url>\n";
}

$sitemapContent .= '</urlset>';
file_put_contents($sitemapFile, $sitemapContent);

echo "<h2>تمام صفحات آماده ایندکس شدند ✅</h2>";
echo "<p>فایل <b>sitemap.xml</b> ساخته شد. URL آن را در <a href='https://search.google.com/search-console' target='_blank'>Google Search Console</a> ارسال کنید.</p>";
?>
.
<?php
namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\Http;
use App\Models\Product;
use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;

class AutoProductAI extends Command
{
    protected $signature = 'products:ai-auto';
    protected $description = 'تولید خودکار محتوا و Excel روزانه برای محصولات جدید';

    public function handle()
    {
        $this->info("شروع پردازش محصولات جدید...");

        // گرفتن محصولات جدید که هنوز توضیح ندارند
        $products = Product::whereNull('description')->get();

        if ($products->isEmpty()) {
            $this->info("محصول جدیدی برای پردازش وجود ندارد.");
            return;
        }

        foreach ($products as $product) {
            $title = $product->title;

            $prompt = "
عنوان محصول: $title
یک توضیح کامل و SEO شده بنویس، شامل:
- توضیح کوتاه
- توضیح بلند
- کلمات کلیدی SEO
- Meta Description
فرمت خروجی JSON بده:
{\"short_description\":\"...\",\"description\":\"...\",\"seo_keywords\":\"...\",\"meta_description\":\"...\"}
";

            try {
                $response = Http::withHeaders([
                    'Authorization' => 'Bearer ' . env('OPENAI_API_KEY')
                ])->post('https://api.openai.com/v1/chat/completions', [
                    'model' => 'gpt-4.1-mini',
                    'messages' => [
                        ['role' => 'user', 'content' => $prompt]
                    ],
                    'temperature' => 0.7
                ]);

                $content = $response->json();
                $json_data = json_decode($content['choices'][0]['message']['content'], true);

                $product->short_description = $json_data['short_description'] ?? '';
                $product->description = $json_data['description'] ?? '';
                $product->seo_keywords = $json_data['seo_keywords'] ?? '';
                $product->meta_description = $json_data['meta_description'] ?? '';
                $product->save();

                $this->info("پردازش شد: $title");

            } catch (\Exception $e) {
                $this->error("خطا برای محصول $title: " . $e->getMessage());
            }
        }

        // ساخت Excel خروجی برای ترب
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Title');
        $sheet->setCellValue('B1', 'Short Description');
        $sheet->setCellValue('C1', 'Description');
        $sheet->setCellValue('D1', 'SEO Keywords');
        $sheet->setCellValue('E1', 'Meta Description');

        $row = 2;
        foreach (Product::all() as $product) {
            $sheet->setCellValue("A$row", $product->title);
            $sheet->setCellValue("B$row", $product->short_description);
            $sheet->setCellValue("C$row", $product->description);
            $sheet->setCellValue("D$row", $product->seo_keywords);
            $sheet->setCellValue("E$row", $product->meta_description);
            $row++;
        }

        $writer = new Xlsx($spreadsheet);
        $excel_file = storage_path('app/public/products.xlsx');
        $writer->save($excel_file);

        $this->info("Excel خروجی ساخته شد: " . $excel_file);
        $this->info("پردازش روزانه تمام شد ✅");
    }
}
.
(function() {
    let products = [];
    let cards = document.querySelectorAll(".css-1j1h0gu"); // کلاس کارت محصول ترب، ممکنه تغییر کنه
    cards.forEach(card => {
        let title = card.querySelector(".css-1bn5q0h")?.innerText || "بدون عنوان";
        let price = card.querySelector(".css-1m5kx4v")?.innerText || "بدون قیمت";
        let link = card.querySelector("a")?.href || "بدون لینک";
        products.push({title, price, link});
    });
    
    // نمایش در کنسول
    console.log(products);

    // تبدیل به CSV برای کپی و ذخیره
    let csv = "Title,Price,Link\n" + products.map(p => `"${p.title}","${p.price}","${p.link}"`).join("\n");
    console.log("کپی CSV:\n", csv);
})();
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Dynamic Title for Search Results -->
    <title>نتایج جستجو برای: {{ search_query }} - {{ site_name }}</title>

    <!-- Dynamic Meta Description for Search Results -->
    <meta name="description" content="لیست محصولات مرتبط با جستجوی '{{ search_query }}' در {{ site_name }}. قیمت، مشخصات و خرید آنلاین.">

    <!-- Canonical URL for Search Results Page -->
    <link rel="canonical" href="{{ current_url }}">

    <!-- Open Graph Tags for Social Media Sharing -->
    <meta property="og:title" content="نتایج جستجو برای: {{ search_query }} - {{ site_name }}">
    <meta property="og:description" content="لیست محصولات مرتبط با جستجوی '{{ search_query }}' در {{ site_name }}. قیمت، مشخصات و خرید آنلاین.">
    <meta property="og:type" content="website">
    <meta property="og:url" content="{{ current_url }}">
    <!-- Use the image of the first product in search results, or the site logo if no products are found -->
    <meta property="og:image" content="{{ first_product_image ?? site_logo }}">

    <!-- Twitter Card Tags for Social Media Sharing -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="نتایج جستجو برای: {{ search_query }} - {{ site_name }}">
    <meta name="twitter:description" content="لیست محصولات مرتبط با جستجوی '{{ search_query }}' در {{ site_name }}. قیمت، مشخصات و خرید آنلاین.">
    <meta name="twitter:image" content="{{ first_product_image ?? site_logo }}">

    <!-- Schema.org JSON-LD for WebSite and SearchAction -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org/",
      "@type": "WebSite",
      "name": "{{ site_name }}",
      "url": "{{ site_url }}",
      "potentialAction": {
        "@type": "SearchAction",
        "target": {
          "@type": "EntryPoint",
          "urlTemplate": "{{ search_url_template }}"
        },
        "query-input": "required name=search_query"
      }
    }
  27571CB6BD26E0A3BA56992E01671DF72ECCFF385A32D2F544B408B1B7950388-1<?php
// ================================
// تنظیمات
// ================================
$mixins_json_url = "https://lavasemkhangi.ir/mixin-products.json"; // فایل خروجی میکسین (JSON)  
$torob_api = "https://seller.torob.com/api/upload_feed?token=YOUR_API_TOKEN"; // لینک آپلود ترب

$cache_file = DIR . '/torob-feed-mixin.xml';

// ================================
// خواندن محصولات میکسین
// ================================
$products_json = file_get_contents($mixins_json_url);
$products = json_decode($products_json, true);

$xml = '<?xml version="1.0" encoding="UTF-8"?><products>';

foreach($products as $p){
    if($p['status'] != 'active' || $p['stock'] <= 0) continue; // فقط محصولات موجود
    
    $id = $p['id'];
    $name = htmlspecialchars($p['title']);
    $price = $p['price'];
    $brand = htmlspecialchars($p['brand']);
    $category = htmlspecialchars($p['category']);
    $image = $p['image'];
    $url = $p['link'];

    $xml .= "
    <product>
        <id>$id</id>
        <name>$name</name>
        <price>$price</price>
        <brand>$brand</brand>
        <category>$category</category>
        <url>$url</url>
        <image>$image</image>
        <availability>instock</availability>
    </product>";
}

$xml .= "</products>";

// ================================
// ذخیره فید محلی
// ================================
file_put_contents($cache_file, $xml);

// ================================
// ارسال خودکار به ترب
// ================================
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $torob_api);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, ['feed_file' => new CURLFile($cache_file)]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

// ================================
// لاگ آپدیت
// ================================
file_put_contents(DIR . '/torob-log.txt', date('Y-m-d H:i:s')." - Feed sent. Response: ".$response."\n", FILE_APPEND);

echo "Feed sent to Torob successfully!";
?>
<?php
/**
 * آپدیت خودکار فید ترب
 * اجرا توسط Cron Job هر شب
 */

// ------------------ دیتابیس ------------------
define('DB_HOST','localhost');
define('DB_USER','نام_کاربری_دیتابیس');
define('DB_PASS','رمز_دیتابیس');
define('DB_NAME','نام_دیتابیس');

$conn = new mysqli(DB_HOST, DB_USER, DB_PASS, DB_NAME);
if($conn->connect_error){
    die("Connection failed: " . $conn->connect_error);
}
$conn->set_charset("utf8");

// ------------------ گرفتن محصولات ------------------
$sql = "SELECT * FROM products WHERE status=1";
$result = $conn->query($sql);

// ------------------ ایجاد فید شبانه ------------------
$file = fopen("torob-feed-power.php","w"); // بازنویسی فایل اصلی
fwrite($file, "<?php\n");
fwrite($file, "header(\"Content-Type: application/xml; charset=UTF-8\");\n");
fwrite($file, "echo '<?xml version=\"1.0\" encoding=\"UTF-8\"?>';\n");
fwrite($file, "echo '<products>';\n");

while($row = $result->fetch_assoc()){
    $link = "https://lavasemkhangi.ir/product/".$row['slug'];
    $title = str_replace(['خرید','ارزان','اصل','اورجینال','قیمت','جدید','ارسال سریع','با گارانتی'],'',$row['title']);
    preg_match('/[A-Za-z0-9\-]{3,}/', $title, $matches);
    $model = $matches[0] ?? '';
    $final_title = $row['brand'].' '.$title;
    if($model != '') $final_title .= ' مدل '.$model;

    $productXML = "<product>
<id>{$row['id']}</id>
<title><![CDATA[{$final_title}]]></title>
<description><![CDATA[".strip_tags($row['description'])."]]></description>
<link>{$link}</link>
<image_link>https://lavasemkhangi.ir/uploads/{$row['image']}</image_link>
<price>{$row['price']} IRR</price>
<brand><![CDATA[{$row['brand']}]]></brand>
<availability>".($row['stock']>0?'in stock':'out of stock')."</availability>
<category><![CDATA[{$row['category']}]]></category>
</product>\n";

    fwrite($file, "echo '".addslashes($productXML)."';\n");
}
?utm_medium=PPC&utm_source=Torob
lavasemkhangi.ir/sitemap.xml
.
let schemaScript = document.createElement("script");
                schemaScript.type = "application/ld+json";
                schemaScript.textContent = JSON.stringify(productSchema);
                document.head.appendChild(schemaScript);

            } else {
                console.warn("API سئو در دسترس نیست یا خطا دارد:", response.status);
                // اگر API نبود، حداقل یک اسکیما ساده بذاریم
                const simpleProductSchema = {
                    "@context": "https://schema.org",
                    "@type": "Product",
                    "name": pageTitle,
                    "image": pageImage ? [pageImage] : [],
                    "description": pageDescription,
                    "offers": {
                        "@type": "Offer",
                        "priceCurrency": "IRR",
                        "price": price || "",
                        "availability": "https://schema.org/InStock"
                    }
                };
                 // حذف فیلدهای خالی
                Object.keys(simpleProductSchema).forEach(key => {
                    if (simpleProductSchema[key] === "" || (typeof simpleProductSchema[key] === 'object' && Object.keys(simpleProductSchema[key]).length === 0 && key !== 'image')) {
                        delete simpleProductSchema[key];
                    }
                });
                 Object.keys(simpleProductSchema.offers).forEach(key => {
                    if (simpleProductSchema.offers[key] === "" || (typeof simpleProductSchema.offers[key] === 'object' && Object.keys(simpleProductSchema.offers[key]).length === 0)) {
                        delete simpleProductSchema.offers[key];
                    }
                });

                let schemaScript = document.createElement("script");
                schemaScript.type = "application/ld+json";
                schemaScript.textContent = JSON.stringify(simpleProductSchema);
                document.head.appendChild(schemaScript);
            }

        } catch (e) {
            console.error("خطا در پردازش صفحه محصول:", e);
        }
    } else {
        // --- برای صفحات غیر محصول (مثلا صفحه اصلی، دسته‌بندی) ---
        // یک اسکیما کلی‌تر برای سازمان یا وب‌سایت اضافه می‌کنیم
        const organizationSchema = {
            "@context": "https://schema.org",
            "@type": "Organization", // یا WebSite بسته به صفحه
            "url": window.location.origin,
            "name": "نام فروشگاه شما", // حتماً اسم فروشگاه خودتون رو بذارید
            "logo": "آدرس لوگوی فروشگاه شما", // آدرس URL لوگو
            "contactPoint": { // اطلاعات تماس (اختیاری اما خوب)
                "@type": "ContactPoint",
                "telephone": "+98-xxxxxxxxx", // شماره تماس شما
                "contactType": "Customer service",
                "areaServed": "IR" // حوزه خدمات (ایران)
            }
        };
        let schemaScript = document.createElement("script");
        schemaScript.type = "application/ld+json";
        schemaScript.textContent = JSON.stringify(organizationSchema);
        document.head.appendChild(schemaScript);
    }
});
</script>

آهان، متوجه شدم! وقتی گفتید **"سایت با میکسین ساخت

 شده"، منظور شما احتمالاً استفاده از Mixins در Vue.js** یا فریم‌ورک‌های مشابه بوده، که برای مدیریت منطق مشترک در کامپوننت‌ها استفاده می‌شود. این نکته فنی خوبی است!

و اینکه می‌خواهید اتصال درگاه پرداخت بدون مشکل وصل شود، یعنی تجربه کاربری روان و بدون دغدغه برای مشتریان. این واقعاً مهم است.

با توجه به این توضیحات، بیایید این موضوع را بررسی کنیم:

۱. ادغام خودکار محصولات با ترب (با فرض استفاده از Mixins در Vue.js یا مشابه):

*   فید محصول (Product Feed): رایج‌ترین و اغلب بهترین راه برای ادغام خودکار محصولات با پلتفرم‌هایی مثل ترب، استفاده از فید محصولات است. این فید یک فایل (معمولاً XML یا CSV) است که تمام اطلاعات محصولات شما را شامل می‌شود.<!-- ===== Meta و Title خودکار ===== -->
<script>
document.addEventListener("DOMContentLoaded", function() {
  const productName = document.querySelector('h1.product-name')?.innerText || "محصول";
  const productFeature = document.querySelector('.product-feature')?.innerText || "ویژگی ویژه";
  const brand = document.querySelector('.product-brand')?.innerText || "برند";

  document.title = `${productName} | ${productFeature} | خرید آنلاین ${brand}`;

  let meta = document.createElement('meta');
  meta.name = "description";
  meta.content = `${productName} با ${productFeature} و بهترین کیفیت هم‌اکنون قابل سفارش است. ارسال سریع و تضمین کیفیت!`;
  document.head.appendChild(meta);
});
</script>

<!-- ===== Schema/Product آماده ===== -->
<script type="application/ld+json">
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "[نام محصول]",
  "image": "[لینک تصویر محصول]",
  "description": "[توضیحات کوتاه محصول]",
  "sku": "[کد محصول]",
  "brand": {
    "@type": "Brand",
    "name": "[برند محصول]"
  },
  "offers": {
    "@type": "Offer",
    "url": "[لینک محصول]",
    "priceCurrency": "IRR",
    "price": "[قیمت به تومان]",
    "availability": "https://schema.org/InStock"
  }
}
</script>

<!-- ===== لینک داخلی انفجاری ===== -->
<nav>
  <a href="/categories/fryers">سرخ‌کن‌ها</a>
  <a href="/categories/vacuums">جاروبرقی</a>
  <a href="/top-products">پرفروش‌ترین‌ها</a>
  <a href="/offers">پیشنهاد ویژه</a>
</nav>

<!-- ===== ارسال خودکار URL به گوگل (Indexing API) ===== -->
<script>
async function submitToGoogle(url) {
  try {
    await fetch(`https://indexing.googleapis.com/v3/urlNotifications:publish`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer [توکن API گوگل]'
      },
      body: JSON.stringify({
        "url": url,
        "type": "URL_UPDATED"
      })
    });
    console.log("لینک به گوگل ارسال شد:", url);
  } catch (e) {
    console.error("ارسال لینک به گوگل شکست خورد:", url, e);
  }
}

// ارسال لینک خودکار صفحه محصول یا دسته‌بندی
submitToGoogle(window.location.href);
</script>
.
<?php
error_reporting(0);
header('Content-Type: text/html; charset=utf-8');

$apiKey = "API_KEY_خودت";
$transid = $_GET['transid'];

$data = [
    "api_key" => $apiKey,
    "transid" => $transid
];

$ch = curl_init("https://panel.aqayepardakht.ir/api/v2/verify");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_HTTPHEADER, ['Content-Type: application/json']);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_TIMEOUT, 15);

$result = json_decode(curl_exec($ch), true);
curl_close($ch);

if(isset($result['data']['status']) && $result['data']['status'] == "success"){

    $amount = $result['data']['amount'];
    $order_id = $result['data']['order_id'];

    // ثبت سفارش ساده (می‌تونی اینجا دیتابیس بزنی)
    
    echo "
    <div style='text-align:center;padding:40px;font-family:tahoma'>
        <h2 style='color:green'>پرداخت با موفقیت انجام شد ✅</h2>
        <p>شماره سفارش: $order_id</p>
        <p>مبلغ: $amount تومان</p>
        <p>سفارش شما ثبت شد و در حال پردازش است.</p>
    </div>
    ";

} else {

    echo "
    <div style='text-align:center;padding:40px;font-family:tahoma'>
        <h2 style='color:red'>پرداخت ناموفق ❌</h2>
        <p>در صورت کسر وجه، مبلغ طی 72 ساعت برگشت می‌خورد.</p>
    </div>
    ";
}
?>
.
import requests, os, json, time
from slugify import slugify

SITE_URL = "https://your-site.com"
TOROB_API = "https://api.torob.com/update_products"
API_KEY = "کلید-ترب-شما"
PAGES_DIR = "./pages"
IMAGE_DIR = "./images"
PRODUCTS_FILE = "products.json"

os.makedirs(PAGES_DIR, exist_ok=True)
os.makedirs(IMAGE_DIR, exist_ok=True)

# خواندن محصولات
def load_products():
    if os.path.exists(PRODUCTS_FILE):
        with open(PRODUCTS_FILE,'r',encoding='utf-8') as f:
            return json.load(f)
    return []

def save_products(products):
    with open(PRODUCTS_FILE,'w',encoding='utf-8') as f:
        json.dump(products,f,ensure_ascii=False, indent=2)

# دانلود تصویر
def download_image(url, slug):
    if not url: return ""
    try:
        path = os.path.join(IMAGE_DIR,f"{slug}.jpg")
        img = requests.get(url).content
        with open(path,'wb') as f: f.write(img)
        return path
    except: return ""

# ایجاد یا بروزرسانی صفحه محصول
def create_product_page(p):
    slug = slugify(p['name'])
    img_path = download_image(p.get('image',''), slug)
    filename = os.path.join(PAGES_DIR,f"{slug}.html")
    html = f"""
    <html lang='fa'>
    <head>
        <title>{p['name']} | فروشگاه نانیوا</title>
        <meta name='description' content='خرید {p['name']} با قیمت {p['price']} تومان'>
    </head>
    <body>
        <h1>{p['name']}</h1>
        <img src='{img_path}' alt='{p['name']}'>
        <p>قیمت: {p['price']} تومان</p>
        <p>موجودی: {p['stock']}</p>
        <p>{p.get('description','')}</p>
        <p>دسته: {p.get('category','')}</p>
    </body>
    </html>
    """
    with open(filename,'w',encoding='utf-8') as f: f.write(html)

# بروزرسانی صفحه اصلی
def update_main_page(products):
    html = "<html lang='fa'><head><title>فروشگاه نانیوا</title></head><body>"
    html += "<h2>جدیدترین محصولات</h2><ul>"
    for p in sorted(products, key=lambda x: (-x.get('is_new',0))):
        slug = slugify(p['name'])
        html += f"<li><a href='{slug}.html'>{p['name']} - {p['price']} تومان</a></li>"
    html += "</ul><h2>پرفروش‌ترین‌ها</h2><ul>"
    for p in sorted(products, key=lambda x: -x.get('sold',0))[:10]:
        slug = slugify(p['name'])
        html += f"<li><a href='{slug}.html'>{p['name']} - {p['price']} تومان</a></li>"
    html += "</ul><h2>پیشنهاد ویژه</h2><ul>"
    for p in [x for x in products if x.get('is_feature')]:
        slug = slugify(p['name'])
        html += f"<li><a href='{slug}.html'>{p['name']} - {p['price']} تومان</a></li>"
    html += "</ul></body></html>"
    with open(os.path.join(PAGES_DIR,"index.html"),'w',encoding='utf-8') as f: f.write(html)

# ارسال به ترب
def sync_torob(products):
    for p in products:
        data = {
            "product_id": p['id'],
            "name": p['name'],
            "price": p['price'],
            "stock": p['stock'],
            "url": f"{SITE_URL}/products/{slugify(p['name'])}"
        }
        headers = {"Authorization": f"Bearer {API_KEY}"}
        try: requests.post(TOROB_API,json=data,headers=headers)
        except: pass

# اجرای ربات
def run_bot():
    products = load_products()
    for p in products:
        create_product_page(p)
    update_main_page(products)
    sync_torob(products)
    print("Bot executed successfully!")

# زمان‌بندی (اختیاری: می‌توان با Cron اجرا شود)
if __name__=="__main__":
    while True:
        run_bot()
        time.sleep(14400)  # 4 ساعت/naniwa_bot/
│
├─ app.py           # سرور Flask و مدیریت داشبورد
├─ bot.py           # ربات پیشرفته برای ساخت صفحات و ادغام ترب
├─ templates/
│   ├─ dashboard.html
│   ├─ products.html
│   └─ categories.html
├─ static/
│   ├─ css/
│   └─ js/
├─ pages/           # صفحات محصولات HTML
├─ images/          # تصاویر محصولات
└─ products.json    # دیتابیس محلی محصولات
.
.
<script>
document.addEventListener("DOMContentLoaded", async function() {
    // تنظیمات فارسی
    document.documentElement.lang = "fa";
    document.documentElement.dir = "rtl";

    const url = window.location.href;
    const noIndexPages = ["cart","checkout","account","login","register"];
    const isNoIndex = noIndexPages.some(word => url.includes(word));

    // robots meta
    let robotsMeta = document.querySelector('meta[name="robots"]');
    if(!robotsMeta){
        robotsMeta = document.createElement("meta");
        robotsMeta.name = "robots";
        document.head.appendChild(robotsMeta);
    }
    robotsMeta.content = isNoIndex ? "noindex, nofollow" : "index, follow";

    // Open Graph خودکار
    function setOG(property, content){
        if(!document.querySelector(`meta[property="${property}"]`)){
            let meta = document.createElement("meta");
            meta.setAttribute("property", property);
            meta.content = content;
            document.head.appendChild(meta);
        }
    }

    const title = document.querySelector("h1") ? document.querySelector("h1").innerText : document.title;
    const image = document.querySelector("img") ? document.querySelector("img").src : "";
    const descMeta = document.querySelector("meta[name='description']");
    const description = descMeta ? descMeta.content : "";

    setOG("og:type","website");
    setOG("og:title", title);
    setOG("og:url", url);
    setOG("og:description", description || title);

    // اگر صفحه محصول است، اطلاعات محصول را از سایت بگیر و به API بفرست
    if(url.includes("/product/")){
        const priceEl = document.querySelector(".price, .product-price, [class*='price']");
        const price = priceEl ? priceEl.innerText.replace(/[^0-9]/g,'') : "";

        // ارسال به API برای تولید محتوا با ChatGPT
        try {
            const productData = { title: title, price: price, url: url };
            const response = await fetch("/api/auto-product-seo", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(productData)
            });
            const seoJSON = await response.json();

            // افزودن Meta Description و Keywords
            let metaDesc = document.querySelector('meta[name="description"]');
            if(!metaDesc){
                metaDesc = document.createElement("meta");
                metaDesc.name = "description";
                document.head.appendChild(metaDesc);
            }
            metaDesc.content = seoJSON.meta_description || title;

            let metaKeywords = document.querySelector('meta[name="keywords"]');
            if(!metaKeywords){
                metaKeywords = document.createElement("meta");
                metaKeywords.name = "keywords";
                document.head.appendChild(metaKeywords);
            }
            metaKeywords.content = seoJSON.seo_keywords || "";

            // افزودن Schema محصول
            const productSchema = {
                "@context":"https://schema.org",
                "@type":"Product",
                "name": title,
                "image": image,
                "description": seoJSON.description || description || title,
                "offers":{
                    "@type":"Offer",
                    "url": url,
                    "priceCurrency":"IRR",
                    "price": price,
                    "availability":"https://schema.org/InStock"
                },
                "brand":{"@type":"Brand","name":"لوازم خانگی"}
            };
            let schemaScript = document.createElement("script");
            schemaScript.type = "application/ld+json";
            schemaScript.text = JSON.stringify(productSchema);
            document.head.appendChild(schemaScript);

        } catch(e){
            console.error("خطا در تولید خودکار SEO:", e);
        }
    }
});
</script>@lavazemkhanegi_ii     👈 سفارش
.
http://rubika.ir/arkopal_arcopal
