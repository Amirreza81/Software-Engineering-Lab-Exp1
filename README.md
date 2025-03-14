# **آزمایش اول - مدیریت نسخ پروژه و یک‌پارچه‌سازی و استقرار مستمر**


### گزارش آزمایش اول: فرانت‌اند ایستا با قابلیت استقرار خودکار

**ابزارهای مورد استفاده:**
- Git
- GitHub, GitHub Actions
- Html, CSS

---

#### مراحل انجام آزمایش

**ایجاد مخزن و راه‌اندازی Git**
در ابتدا وارد حساب گیت‌هاب شده و یک مخزن جدید با نام
`Software-Engineering-Lab-Exp1` ایجاد نمودیم. سپس مطابق با تصویر زیر دستورات را وارد نموده و و اولین کامیت را همراه با فایل `README.md` ارسال نمودیم.

![Initializing](pics/initialization.png)

**ایجاد فایل .gitignore**

**استقرار خودکار با GitHub Actions**

**کامیت‌ها**
طبق خواسته صورت آزمایش، بیشتر از 20 کامیت در این پروژه وجود دارد که هر کدام معنادار می‌باشند و همان‌طور که از متن آن‌ها مشخص است، اتفاق مشخصی در فرآیند پیاده‌سازی رخ داده است.

**مدیریت و تعداد شاخه‌ها**

**رفع Conflict**
##### کانفلیکت اول:

##### کانفلیکت دوم:
کانفلیکت زمانی رخ داد که یکی از اعضا تغییراتی در فایل 
`index.html` به وجود آورد تا ترتیب قرارگیری دکمه‌های این صفحه مرتب بشود. سپس بعد از تلاش برای مرج کردن شاخه 
`feature-about-us` با شاخه `dev`،
به دلیل اینکه تغییرات در یک فایل مشابه بود، گیت قادر به تصمیم‌گیری خودکار نبود که کدام تغییر را بپذیرد. به همین دلیل یک `merge conflict` به وجود آمد.
برای حل آن نیز مطابق تصاویر زیر، به طور دستی تعارض را بر طرف کرده و کامیت را ارسال نمودیم.

![](pics/conflict2-1.png)
![](pics/conflict2-2.png)
![](pics/conflict2-3.png)

**محافظت کردن از شاخه main**
مطابق با تصاویر زیر، اعمال محدودیت در مخزن خود در Github، شاخه‌ی main پروژه را محافظت کردیم به صورتی که تنها از طریق pull request امکان ادغام شاخه‌ای دیگر با شاخه‌ی main را داشته باشیم.

![pmain1](pics/protecting_main1.png)
![pmain2](pics/protecting_main2.png)

**ایجاد pull request**

---

### **سوالات**

- سوال اول:

---

- سوال دوم:

---

- سوال سوم:

---

- سوال چهارم:

---

- **سوال پنجم: منظور از stage یا همان index چیست؟ دستور stash چه کاری را انجام می‌دهد؟**
**پاسخ:**

---

- **سوال ششم: مفهوم snapshot به چه معناست؟ ارتباط آن با commit چیست؟**

---

- **سوال هفتم: تفاوت‌های local repository و remote repository چیست؟**

--- 

### **تقسیم وظایف**
در این آزمایش تلاش شد تا تمامی افراد سهم تقریبا یکسانی در پیاده‌سازی آزمایش داشته باشند. همان‌طور که در کانبان‌برد مشاهده می‌شود، در تمامی بخش‌ها افراد سهم مشابهی داشتند. چه در پیاده‌سازی انواع صفحات و چه در نوشتن گزارش و آماده سازی پاسخ سوالات داده شده، تمامی تلاش خود را نمودیم تا فعالیت‌ها به طور مساوی تقسیم بشوند.

[**لینک کانبان‌برد**](https://github.com/users/Amirreza81/projects/1)

### **اعضای تیم**

- امیررضا آذری - 99101087
- 
- 
