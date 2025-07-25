# مولد سایت استاتیک زنجان‌لاگ

این پروژه یک مولد سایت استاتیک ساده با پایتون است که برای ساخت و مدیریت وب‌سایت [زنجان‌لاگ](https://zanjanlug.ir) (گروه کاربران لینوکس زنجان) طراحی شده است. هدف اصلی، جدا کردن کامل محتوا از ظاهر سایت و خودکارسازی فرآیند ساخت صفحات HTML است.

## ✨ ویژگی‌ها

- **محتوا-محور:** تمام محتوای سایت (رویدادها، افراد، پروژه‌ها) در فایل‌های متنی ساده با فرمت **Markdown** مدیریت می‌شود.
- **سادگی:** با یک اسکریپت پایتون (`generate.py`) کل سایت ساخته می‌شود. بدون نیاز به دیتابیس یا سیستم‌های پیچیده.
- **سرعت و امنیت:** خروجی نهایی سایت، مجموعه‌ای از فایل‌های استاتیک HTML, CSS و JS است که روی هر هاست ساده‌ای قابل میزبانی بوده و بسیار سریع و امن است.
- **قالب‌پذیری:** ظاهر سایت با استفاده از قالب‌های **Jinja2** به سادگی قابل تغییر و شخصی‌سازی است.
- **مدیریت آسان:** برای افزودن یک رویداد یا پروژه جدید، کافیست یک فایل Markdown جدید ایجاد کرده و اسکریپت را اجرا کنید.

---

## 🚀 راه‌اندازی و استفاده

### پیش‌نیازها

برای اجرای این پروژه به **پایتون (نسخه ۳.۶ به بالا)** نیاز دارید. ابتدا کتابخانه‌های مورد نیاز را با دستور زیر نصب کنید:

```bash
pip install -r requirements.txt
```
*(توجه: ابتدا باید فایل `requirements.txt` را مطابق بخش زیر ایجاد کنید.)*

### نصب وابستگی‌ها

برای سهولت در نصب، یک فایل `requirements.txt` در ریشه پروژه ایجاد کرده و محتوای زیر را در آن قرار دهید:

**`requirements.txt`**
```
Jinja2
Markdown
PyYAML
```

سپس با دستور بالا، تمام پکیج‌ها را نصب کنید.

### ساختار پروژه

```
zanjanlug-site/
├── content/              # فایل‌های Markdown محتوای سایت
│   ├── events/
│   ├── people/
│   └── projects/
├── templates/            # قالب‌های HTML (Jinja2)
├── static/               # فایل‌های ثابت (CSS, تصاویر و ...)
├── output/               # پوشه خروجی (سایت نهایی اینجا ساخته می‌شود)
├── generate.py           # اسکریپت اصلی برای ساخت سایت
└── README.md             # همین فایل راهنما
```

### اجرای مولد

برای ساخت سایت، کافیست اسکریپت `generate.py` را از طریق ترمینال اجرا کنید:

```bash
python generate.py
```

پس از اجرای موفقیت‌آمیز، تمام فایل‌های نهایی سایت در پوشه `output` ساخته می‌شوند. برای مشاهده سایت، فایل `output/index.html` را در مرورگر خود باز کنید.

---

## 📝 مدیریت محتوا

### افزودن یک رویداد جدید

1.  یک فایل جدید با پسوند `.md` در پوشه `content/events/` ایجاد کنید. (مثال: `03-docker-workshop.md`)
2.  محتوای فایل را با ساختار زیر پر کنید:

    ```markdown
    ---
    title: "عنوان رویداد شما"
    date: "YYYY-MM-DD"  # فرمت تاریخ: سال-ماه-روز
    time: "ساعت ۱۷:۰۰"   # (اختیاری)
    location: "مکان برگزاری" # (اختیاری)
    presenters: ["slug-presenter-1", "slug-presenter-2"] # شناسه‌های فایل افراد
    status: "upcoming"  # وضعیت: upcoming (آینده) یا held (برگزار شده)
    resources:          # (اختیاری)
      slides: "/static/files/slides.pdf"
      video: "https://youtube.com/link"
    ---

    توضیحات کامل رویداد در اینجا با فرمت **Markdown** نوشته می‌شود.

    می‌توانید از لیست‌ها:
    - آیتم اول
    - آیتم دوم

    و یا **متن‌های برجسته** استفاده کنید.
    ```

### افزودن یک فرد جدید

1.  یک فایل جدید با پسوند `.md` در پوشه `content/people/` ایجاد کنید. نام فایل به عنوان شناسه (slug) فرد استفاده می‌شود. (مثال: `new-member.md`)
2.  محتوای آن را تکمیل کنید:

    ```markdown
    ---
    name: "نام کامل فرد"
    photo: "/static/images/avatar.jpg" # (اختیاری)
    bio: "یک بیوگرافی کوتاه"
    links:
      website: "https://example.com"
      github: "https://github.com/username"
    ---
    ```

### افزودن یک پروژه جدید

1.  یک فایل جدید با پسوند `.md` در پوشه `content/projects/` ایجاد کنید.
2.  محتوای آن را تکمیل کنید:

    ```markdown
    ---
    title: "نام پروژه"
    github: "https://github.com/zanjanlug/project-name" # لینک گیت‌هاب پروژه
    ---

    توضیحات مربوط به پروژه در اینجا قرار می‌گیرد.
    ```

**نکته مهم:** پس از هر تغییری در پوشه `content`، باید اسکریپت `generate.py` را مجدداً اجرا کنید تا سایت به‌روز شود.

---

## 🌐 استقرار سایت (Deployment)

برای آنلاین کردن سایت، کافیست **تمام محتویات پوشه `output`** را در سرویس میزبانی خود آپلود کنید. سرویس‌های زیر برای میزبانی سایت‌های استاتیک بسیار مناسب و اغلب رایگان هستند:

- **GitHub Pages**
- **Netlify**
- **Vercel**
- **Cloudflare Pages**

این سرویس‌ها می‌توانند به مخزن گیت‌هاب شما متصل شوند و پس از هر `push`، به صورت خودکار سایت را بیلد و منتشر کنند.

---

## 🤝 مشارکت

از هرگونه مشارکت در این پروژه استقبال می‌شود. اگر ایده‌ای برای بهبود اسکریپت، طراحی سایت یا افزودن ویژگی‌های جدید دارید، می‌توانید یک **Issue** یا **Pull Request** در مخزن گیت‌هاب پروژه ثبت کنید.


**نکتهٔ مهم**: این فایل `README.md` و بقیهٔ بخش‌های پروژه (به‌جز بخش محتوا) با هوش‌مصنوعی ساخته شده است.
