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
یک فایل با نام .gitignore میسازیم و در آن فایلهایی را که میخواهیم توسط گیت ترک نشوند قرار میدهیم. برای نمونه میتوان فایلهای پوشه .idea را در این فایل مشخص کنیم تا این فایلها که مربوط به ادیتور ما است ترک نشوند و دچار کانفلیکت های متعدد نشویم. همچنین میتوانیم فایلهای حجیم را که پسوندهای صوتی یا ویدیویی دارند را نیز در این فایل قرار بدهیم تا حجم مخزن ما بیش از حد زیاد نشود.
<!-- Reza -->

**استقرار خودکار با GitHub Actions**
یک گردش‌کار مربوط به GitHub Actions ایجاد میکنیم تا پروژه به‌طور خودکار در GitHub Pages بالا بیاید و هنگام آپدیت شدن به شاخه main صفحه Github Pages ما نیز بروزرسانی شود. کد اصلی پیکربندی به به صورت زیر است:
```
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```
<!-- Reza -->

**کامیت‌ها**

طبق خواسته صورت آزمایش، بیشتر از 20 کامیت در این پروژه وجود دارد که هر کدام معنادار می‌باشند و همان‌طور که از متن آن‌ها مشخص است، اتفاق مشخصی در فرآیند پیاده‌سازی رخ داده است.

**مدیریت و تعداد شاخه‌ها**

در پروژه‌ی ما، از یک استراتژی منظم برای شاخه‌بندی استفاده می‌کردیم:

- شاخه‌ی main محافظت‌شده بود و فقط گاهی اوقات به‌روزرسانی می‌شد.
- شاخه‌ی dev به‌عنوان شاخه‌ی اصلی برای توسعه‌ی کدها استفاده می‌شد.
- برای هر ویژگی جدید، یک شاخه‌ی مجزا (feature branch) ایجاد می‌کردیم، روی آن کار می‌کردیم، و پس از تکمیل، آن را در dev ادغام می‌کردیم.
- پس از بررسی و تست تغییرات در dev، هر از چندگاهی این شاخه را در main ادغام می‌کردیم تا نسخه‌ی پایدار پروژه را به‌روزرسانی کنیم.


**رفع Conflict**
##### کانفلیکت اول:
این کانفلیکت زمانی بوجود آمد که شاخه feature-car-details را با شاخه dev مرج کردیم و این در حالی بود که دکمه مربوط به صفحه car details در صفحه index.html هر دو شاخه در جای یکسانی وجود نداشت و به طور کلی navbar ها تفاوت داشتند. پس دچار کانفلیکت مرج شدیم که در تصاویر زیر مشاهده میکنیم و سپس در ادامه آن را برطرف کرده و کامیت انجام دادیم.
![image](https://github.com/user-attachments/assets/afb5a0dd-1cfb-4b1e-811b-d474af32037d)
![image](https://github.com/user-attachments/assets/8018ca99-f943-4209-aff1-1e39479fb39c)
![image](https://github.com/user-attachments/assets/e5b1b75c-33c0-49b6-8420-3e73d4762ee6)


<!-- Reza -->

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

از آنجا که شاخه‌ی main محافظت‌شده بود، امکان ادغام مستقیم dev در آن وجود نداشت. به همین دلیل، باید یک Pull Request (PR) برای ادغام dev در main ایجاد می‌کردیم. صاحب مخزن مسئول بررسی تغییرات، تأیید صحت کدها، و در نهایت پذیرش درخواست و انجام ادغام بود. این فرآیند به حفظ یکپارچگی کدها و جلوگیری از تغییرات ناخواسته در شاخه‌ی اصلی کمک می‌کرد.

**استفاده از دستورات متنوع برای پیش‌برد فعالیت‌ها**

در این آزمایش تلاش شد تا با استفاده از دستورات مختلف و به کمک ترمینال یادگیری خود را افزایش دهیم.
بخشی از استفاده از ترمینال را در تصاویر موجود در گزارش مشاهده می‌نمایید. به طور خلاصه از دستورات زیر در طول آزمایش بیشتر استفاده نمودیم:
```bash
git init
git pull
git push
git status
git log
git commit
git add
git rebase
git merge
git checkout
git branch
git stash
```

---

### **سوالات**

- **سوال اول: پوشه‌ی .git چیست؟ چه اطلاعاتی در آن ذخیره می‌شود؟ با چه دستوری ساخته می‌شود؟**  

**پاسخ:**  
پوشه‌ی `.git` یک دایرکتوری مخفی است که توسط Git ایجاد می‌شود و شامل تمام اطلاعات مورد نیاز برای مدیریت نسخه‌های یک پروژه است. این پوشه اساساً مخزن (repository) محلی گیت محسوب می‌شود و در ریشه‌ی پروژه قرار دارد.  

#### **اطلاعات ذخیره‌شده در `.git`**  
درون این پوشه، چندین زیرپوشه و فایل مهم وجود دارد که وظایف مختلفی را برعهده دارند:  

- `objects/` : شامل اطلاعات مربوط به commitها، درخت‌ها (trees) و بلاک‌ها (blobs) که نشان‌دهنده‌ی محتویات فایل‌ها هستند.  
- `branches/` : اطلاعات مربوط به شاخه‌های مختلف پروژه را ذخیره می‌کند.  
- `refs/` : مسیرهای مربوط به برنچ‌ها و تگ‌ها را نگه می‌دارد.  
- `HEAD` : مشخص می‌کند که در حال حاضر روی کدام شاخه هستید.  
- `logs/` : تاریخچه‌ی تغییرات مرتبط با HEAD و دیگر شاخه‌ها را ذخیره می‌کند.  
- `config` : تنظیمات مربوط به Git مخزن شامل آدرس‌های remote و سایر پیکربندی‌ها را نگه می‌دارد.  
- `index` : وضعیت **staging area** (یا همان index) را ثبت می‌کند.  

#### **نحوه‌ی ایجاد `.git`**  
برای ایجاد این پوشه و راه‌اندازی یک مخزن Git در یک پروژه، از دستور زیر استفاده می‌شود:  

`git init`

---
- **منظور از atomic بودن در atomic commit و atomic pull-request چیست؟**  
**پاسخ:**

یک کامیت اتمیک (Atomic Commit) یعنی تغییرات یکجا و به‌طور کامل در مخزن اعمال می‌شوند، به‌طوری‌که یا همه تغییرات ذخیره می‌شوند یا هیچ‌کدام. این ویژگی باعث می‌شود که مخزن همیشه در یک وضعیت سالم و قابل استفاده باقی بماند.

مزایای Atomic Commit:
- عدم وجود کامیت‌های نیمه‌کاره: تضمین می‌کند که کامیت‌های ناقص یا خراب در مخزن ثبت نشوند.
- امکان بازگردانی آسان: می‌توان کامیت را در صورت نیاز به‌طور کامل برگشت داد (revert).
- قابلیت خوانایی بالا: باعث می‌شود هر کامیت تنها شامل یک تغییر منطقی باشد و تاریخچه‌ی گیت تمیز و خوانا باقی بماند.

مثال از یک Atomic Commit:
git add file1 file2 file3
git commit -m "اضافه کردن قابلیت جدید X به سیستم"
در اینجا، اگر commit موفق باشد، همه‌ی فایل‌ها ذخیره می‌شوند؛ در غیر این صورت، هیچ تغییری اعمال نمی‌شود.

Atomic Pull Request
یک Pull Request اتمیک (Atomic PR) یعنی درخواست تغییرات (PR) باید یک تغییر مستقل و کامل باشد که بتوان آن را بدون وابستگی به تغییرات دیگر ادغام کرد (merge).

ویژگی‌های یک Pull Request اتمیک:
- محدود به یک وظیفه‌ی مشخص: فقط یک ویژگی یا باگ‌فیکس مشخص را شامل شود.
- قابل تست و بررسی: به‌راحتی بتوان آن را آزمایش کرد و در صورت نیاز بازگرداند.
- عدم وابستگی به سایر PRها: اگر PR دیگری رد شود، نباید باعث شکست این PR شود.

### **مثال از یک Atomic Pull Request:**

####  نادرست: یک PR که شامل چندین تغییر نامرتبط است، مثلاً:
- اضافه کردن یک قابلیت جدید  
- رفع یک باگ در بخش دیگر پروژه  
- به‌روزرسانی مستندات  

####  درست: یک PR که فقط یک تغییر مشخص و مرتبط دارد، مثلاً:
- فقط اضافه کردن یک ویژگی جدید  
- فقط رفع یک باگ خاص  

---

- **تفاوت دستورهای fetch و pull و merge و rebase و cherry-pick را بیان کنید.**  
**پاسخ:**

### 1. git fetch  
این دستور تغییرات را از مخزن remote دریافت کرده و در مخزن local ذخیره می‌کند، بدون به‌روزرسانی برنچ‌ها.  
- توضیح: تغییرات ریپازیتوری اصلی (remote) به صورت محلی دریافت می‌شود، اما این تغییرات را به شاخه فعلی اضافه نمی‌کند. فقط نسخه محلی از تاریخچه ریپازیتوری اصلی را به‌روزرسانی می‌کند.

### 2. git pull  
این دستور تغییرات را از مخزن remote دریافت کرده و در برنچ فعلی ادغام می‌کند (عملکرد fetch + merge).  
- توضیح: شبیه به دستور fetch است، با این تفاوت که بعد از دریافت تغییرات، آنها را به صورت خودکار به شاخه فعلی اضافه می‌کند. یعنی ترکیبی از fetch و merge است.

### 3. git merge  
تغییرات یک برنچ را به برنچ فعلی ادغام می‌کند.  
- توضیح: این دستور شاخه‌های مختلف را با هم ترکیب می‌کند و تغییرات دو شاخه را در شاخه فعلی ادغام می‌کند. در نتیجه، یک کامیت جدید ایجاد می‌شود که شامل هر دو مجموعه تغییرات است.

### 4. git rebase  
تغییرات یک برنچ را به انتهای تاریخچه‌ی برنچ دیگری منتقل کرده و تاریخچه commit‌ها را به صورت خطی نمایش می‌دهد.  
- توضیح: rebase برای قرار دادن تغییرات یک شاخه روی شاخه دیگر بدون ایجاد کامیت‌های ادغام استفاده می‌شود. این دستور تاریخچه ریپازیتوری را مرتب می‌کند و در نتیجه تاریخچه تمیزتری ایجاد می‌شود. اما می‌تواند باعث بروز مشکلات در صورت وجود کامیت‌های مشترک در شاخه‌ها شود.

### 5. git cherry-pick  
یک یا چند commit مشخص از یک برنچ را به برنچ دیگری اعمال می‌کند.  
- توضیح: این دستور زمانی کاربرد دارد که فقط به یک سری تغییرات خاص نیاز دارید و نمی‌خواهید کل شاخه را مرج کنید. فقط کامیت‌های خاصی که مدنظر شما هستند، به شاخه فعلی منتقل می‌شوند.

---

- **تفاوت دستورهای reset و revert و restore و switch و checkout را بیان کنید.**  
**پاسخ:**

### 1. git reset  
این دستور commit‌ها و تغییرات را به حالت قبلی بازمی‌گرداند و آنها را از مرحله staging خارج می‌کند.  
- توضیح: این دستور برای برگرداندن شاخه به حالت یک کامیت خاص استفاده می‌شود. reset تغییرات را به طور کامل حذف می‌کند و سه نوع دارد: --soft، --mixed و --hard که هر کدام میزان متفاوتی از تغییرات را حذف می‌کنند.

### 2. git revert  
تغییرات یک commit خاص را به حالت قبلی بازمی‌گرداند و یک commit جدید ایجاد می‌کند.  
- توضیح: این دستور یک کامیت جدید ایجاد می‌کند که تغییرات کامیت قبلی را برعکس می‌کند. بنابراین به تاریخچه مخزن صدمه‌ای نمی‌زند و به جای حذف، تغییرات را معکوس می‌کند.

### 3. git restore  
فایل‌های تغییر یافته را به حالت قبلی بازمی‌گرداند.  
- توضیح: restore برای برگرداندن فایل‌ها یا دایرکتوری‌ها به وضعیت قبلی یا تغییرات خاص استفاده می‌شود. این دستور معمولا در کارهای تک فایل و برای بازگرداندن تغییرات فایل‌ها از حالت استیج یا از نسخه‌ی خاصی کاربرد دارد.

### 4. git switch  
برای جابه‌جایی بین برنچ‌ها استفاده می‌شود.  
- توضیح: این دستور برای تغییر شاخه‌ها استفاده می‌شود و جایگزین ساده‌تری برای checkout است که مخصوصا برای تغییر شاخه طراحی شده است.

### 5. git checkout  
برای جابه‌جایی بین برنچ‌ها و همچنین بازگرداندن فایل‌ها به حالت commit‌های قبلی استفاده می‌شود.  
- توضیح: این دستور برای تغییر شاخه‌ها، تغییر وضعیت فایل‌ها و بازگرداندن آنها به حالت خاصی استفاده می‌شود. checkout می‌تواند یک شاخه جدید ایجاد کند، شاخه فعلی را تغییر دهد یا وضعیت فایل خاصی را بازنشانی کند.
---

- **سوال پنجم: منظور از stage یا همان index چیست؟ دستور stash چه کاری را انجام می‌دهد؟**

**پاسخ:**
در Git، مرحله‌ی stage یا index به بخشی از مخزن گفته می‌شود که در آن تغییرات فایل‌ها قبل از ثبت نهایی (commit) نگهداری می‌شوند. زمانی که تغییری در فایل‌ها ایجاد می‌شود، این تغییرات ابتدا در working directory قرار دارند. با اجرای دستور git add، تغییرات به stage اضافه می‌شوند و آماده‌ی کامیت شدن خواهند بود. در نهایت، با اجرای git commit این تغییرات به تاریخچه‌ی مخزن اضافه می‌شوند.

دستور git stash برای ذخیره‌ی موقتی تغییرات در مخزن استفاده می‌شود. این دستور زمانی مفید است که بخواهید بدون از دست دادن تغییرات فعلی، روی شاخه‌ی دیگری کار کنید یا مخزن را به وضعیت قبلی بازگردانید. تغییرات ذخیره‌شده را می‌توان در آینده با استفاده از git stash apply یا git stash pop دوباره اعمال کرد.

مثال:
```bash
# افزودن تغییرات به stage (index)
git add file.txt
# ثبت تغییرات در مخزن (commit)
git commit -m "Add changes"
# ذخیره‌ی موقتی تغییرات بدون کامیت کردن
git stash
# بازیابی تغییرات ذخیره‌شده
git stash pop

```

---

- **سوال ششم: مفهوم snapshot به چه معناست؟ ارتباط آن با commit چیست؟**

**پاسخ:** 
در Git، **snapshot** به معنای تصویری از وضعیت کل پروژه در یک لحظه‌ی مشخص است. هر زمان که یک **commit** انجام می‌شود، Git یک snapshot از تمام فایل‌های نسخه‌بندی‌شده را ذخیره می‌کند. این snapshot شامل تمامی تغییرات جدید نسبت به commit قبلی است.

برخلاف سیستم‌های قدیمی کنترل نسخه که فقط تغییرات خطی را ذخیره می‌کردند، Git هر commit را به عنوان یک snapshot کامل در نظر می‌گیرد. البته برای بهینه‌سازی فضا، فایل‌های بدون تغییر فقط به نسخه‌ی قبلی لینک می‌شوند. هر commit شامل بخش‌های زیر است:
- **Tree:** اطلاعات مربوط به فایل‌ها و دایرکتوری‌های پروژه را نگه می‌دارد.
- **Parent commit:** ارتباط بین snapshots را حفظ می‌کند.
- **Metadata:** شامل اطلاعاتی مثل نویسنده، تاریخ و پیام commit است.

این ویژگی باعث می‌شود که بتوان به‌راحتی بین snapshots جابه‌جا شد، تغییرات را مقایسه کرد و در صورت نیاز پروژه را به وضعیت قبلی بازگرداند.

مثال:
```sh
# ایجاد یک مخزن جدید
git init
# ایجاد یک فایل و افزودن متن اولیه
echo "First version of project" > project.txt
# افزودن فایل به stage و ایجاد snapshot اولیه
git add project.txt  
git commit -m "Initialize project"  
# ایجاد تغییرات در فایل
echo "Add new feature" >> project.txt
# ثبت snapshot جدید
git add project.txt  
git commit -m "Add new feature"
# مشاهده لیست snapshots
git log --oneline  
# بازگشت به snapshot قبلی
git checkout HEAD~1  
```
این ساختار این امکان را می‌دهد پروژه را به نسخه‌های مختلف در طول زمان برگرداند، تغییرات را بهتر مدیریت کرد و از شاخه‌بندی (branching) و ادغام (merging) برای کار تیمی مؤثرتر استفاده کرد.

در ترمینال:
![snapshot](pics/snapshot.png)

---

- **سوال هفتم: تفاوت‌های local repository و remote repository چیست؟**

**پاسخ:** تفاوت‌های بین Local Repository و Remote Repository در Git:

1. مکان ذخیره‌سازی:
   - Local Repository: مخزن محلی است که روی کامپیوتر شما ذخیره می‌شود. تمام تاریخچه و تغییرات پروژه در این مخزن نگهداری می‌شود و شما بدون نیاز به اتصال اینترنتی می‌توانید به آن دسترسی داشته باشید.
   - Remote Repository: مخزن از راه دور است که معمولاً بر روی یک سرور یا سرویس آنلاین (مثل GitHub، GitLab یا Bitbucket) قرار دارد. این مخزن برای به اشتراک‌گذاری کد با دیگران و همکاری تیمی استفاده می‌شود.

2. دسترسی و هماهنگی:
   - Local Repository: تنها شما (یا کسانی که به سیستم شما دسترسی دارند) می‌توانند به این مخزن دسترسی داشته باشند.
   - Remote Repository: این مخزن به‌صورت عمومی یا خصوصی به اشتراک گذاشته می‌شود و معمولاً توسط چندین نفر قابل دسترسی است. همه اعضای تیم می‌توانند تغییرات را ارسال (push) یا دریافت (pull) کنند.

3. سینک کردن تغییرات:
   - Local Repository: تغییرات در این مخزن تنها روی سیستم شما ثبت می‌شود و هیچ تأثیری بر روی سایر اعضای تیم ندارد مگر اینکه تغییرات را به مخزن از راه دور ارسال کنید.
   - Remote Repository: تغییرات این مخزن برای همگان قابل مشاهده است و اعضای تیم می‌توانند تغییرات یکدیگر را از اینجا دریافت کنند.

4. عملیات‌ها:
   - Local Repository: تمام دستورات Git مانند `git commit`, `git add`, `git log`, و غیره در مخزن محلی انجام می‌شود.
   - Remote Repository: عملیات‌هایی مانند `git push`, `git pull`, و `git fetch` به مخزن از راه دور مربوط می‌شوند.

5. مخزن‌های متصل:
   - Local Repository: مخزن محلی معمولاً یک یا چند remote (مانند `origin`) برای هماهنگی با مخزن‌های از راه دور دارد.
   - Remote Repository: مخزن از راه دور یک نسخه متمرکز از پروژه است که معمولاً در سرور قرار دارد و در آنجا به‌صورت مشترک توسط تیم توسعه مدیریت می‌شود.

مثال:
- برای ارسال تغییرات از Local Repository به Remote Repository:  
  ```git push origin main```

- برای دریافت آخرین تغییرات از Remote Repository به Local Repository:  
  ```git pull origin main```

- برای مشاهده remote‌های متصل به مخزن محلی:  
  ```git remote -v```

در نهایت: مخزن محلی برای کارهای فردی و تغییرات آزمایشی استفاده می‌شود، در حالی که مخزن از راه دور برای همکاری تیمی و اشتراک‌گذاری کد با دیگران کاربرد دارد.


--- 

### **تقسیم وظایف**
در این آزمایش تلاش شد تا تمامی افراد سهم تقریبا یکسانی در پیاده‌سازی آزمایش داشته باشند. همان‌طور که در کانبان‌برد مشاهده می‌شود، در تمامی بخش‌ها افراد سهم مشابهی داشتند. چه در پیاده‌سازی انواع صفحات و چه در نوشتن گزارش و آماده سازی پاسخ سوالات داده شده، تمامی تلاش خود را نمودیم تا فعالیت‌ها به طور مساوی تقسیم بشوند.

[**لینک کانبان‌برد**](https://github.com/users/Amirreza81/projects/1)

### **اعضای تیم**

- امیررضا آذری - 99101087
- <!-- Reza -->
- امید دلیران - 400104931
