


## معرفی
<div align="right" dir = "rtl">
 Elastic search یک موتور جستجو یا به بیانی دیگر پایگاه‌ داده‌ای از جنس document oriented یا nosql است.
 جالب است بدانید از این موتور جستجو در طراحی سایت‌های معروفی چون StackOverFlow، Wikipedia و Github نیز استفاده شده است.
 این ابزار توسط زبان جاوا توسعه یافته و برای درک بهتر این آموزش بهتر است با مفاهیمی چون json, search engine و زبان برنامه‌نویسی جاوا آشنا باشید.
 <br> 
 
 ## نصب
 قدم اول: باید جاوا با ورژن حداقل 7 در سیستم عامل شما نصب باشد. دستورات زیر برای چک کردن در ویندوز و Unix آورده شده‌اند.
<div align="left" dir = "ltr">
  
```
> java -version
$ echo $JAVA_HOME
```
</div>
 قدم دوم: از سایت www.elastic.co نسخه مربوط به سیستم‌عامل خود را دریافت کرده و نصب کنید.  <br>
 قدم سوم: به محل نصب بروید و دستور زیر را اجرا کنید.



 <div align="left" dir = "ltr">
In Windows
  
```
> cd elasticsearch-2.1.0/bin
> elasticsearch
```
In Linux
```
$ cd elasticsearch-2.1.0/bin
$ ./elasticsearch
```
 </div>
 
 اگر در ویندوز با خطای مربوط به JAVA_HOME مواجه شدید در بخش environment variables ها Path مروبط به jre نصب شده را قرار دهید.
 <br>
 قدم چهارم: پورت پیش‌فرض برای Elasticsearch، 9200 می‌باشد که اگر در browser خود http://localhost:9200 را وارد کنید عبارت json زیر را مشاهده خواهید کرد.(برای تغییر پورت باید مقدار http.port را در فایل elasticsearch.yml تغییر دهید.
  <div align="left" dir = "ltr">
In Windows
  
```
{
   "name" : "Brain-Child",
   "cluster_name" : "elasticsearch", "version" : {
      "number" : "2.1.0",
      "build_hash" : "72cd1f1a3eee09505e036106146dc1949dc5dc87",
      "build_timestamp" : "2015-11-18T22:40:03Z",
      "build_snapshot" : false,
      "lucene_version" : "5.3.1"
   },
   "tagline" : "You Know, for Search"
}
```
 </div>
 قدم پنجم: حال که از نصب Elasticsearch مطمئن شده‌ایم به نصب kibana می‌پردازیم، که یک اپلیکیشن frontend در سطح بالایی elasticsearch است که امکان جستجوی راحت تر و مصور کردن داده ها را می‌دهد.
 
<div align="left" dir = "ltr">
 
In Linux
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.0.0-linuxx86_64.tar.gz

tar -xzf kibana-7.0.0-linux-x86_64.tar.gz

cd kibana-7.0.0-linux-x86_64/

./bin/kibana
```
</div>
 برای ویندوز نیز از سایت  https://www.elastic.co/products/kibana. آن را دانلود کرده و kibana.bat را اجرا می‌کنیم.
 
 ## مثال ساده
 در اولین قدم می‌خواهیم populate کردن این موتور را یاد بگیریم و این کار را در محیط elasticsearch.bat انجام می‌دهیم.
 <br>
 ### Populate
 فرض کنید می‌خواهیم اطالاعات مربوط به دانشجویان را نگهداری کنیم، پس یک index به نام student می‌سازیم.
<div align="left" dir = "ltr">
 
```
PUT student
# response => {"acknowledged": true}
```
</div>
حال داده های زیر را که لزوما Key های یکسانی ندارند را می‌توانیم به این Index اضافه کنیم.
 <div align="left" dir = "ltr">
 
```
POST student/_doc/5
  {
     "f_name": "Jamshid", "l_name": "Jamshidi", "student_number":99101010,
     "overall_grade":12.1, "grades":[12.0, 12.1, 12.2], "University":"Sharif"
  }
  POST student/_doc/3
  {
     "f_name": "Mona", "l_name": "Jamshidi", "student_number":90909090,
     "department":"CS", "gender":"female", "university":"Tehran"
  }
```
</div>
 دستورات بالا در واقع دو آبجکت از جنس json را در Index ایجاد کردند و شماره‌ی id مربوط به آن را بعد از doc_ که به موتور می‌فهماند قرار است یک document ایجاد شود می‌نویسیم.
 <br>
 اگر هم id را خودمان تعریف نکنیم به صورت اتوماتیک تولید می‌شود و در response بعد از اجرای کد با همچین خروجی مواجه خواهید شد.
 <br>
 
<div align="left" dir = "ltr">
 
```
"_id": "PVghWGoB7LiDTeV6LSGu"
```
</div>

### search
 حال با دستور زیر تمامی آبجکت‌هایی که در دانشگاه تهران هستند را دریافت می‌کنیم.
 
 
  <div align="left" dir = "ltr">
 
```
GET /_all/_search?q=university:tehran 
```
</div>
 
</div>
