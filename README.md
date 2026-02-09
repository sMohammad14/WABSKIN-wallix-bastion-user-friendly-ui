### آپدیت: امکان اضاه کردن Service به Device افزوده شد
---
به پیشنهاد یکی از دوستان تصمیم گرفتم یک پوسته کاربرپسند برای WALLIX Bastion بنویسم که فعلا از بخش Device ها با یک سری امکانات شروع کرده‌ام.

اگر با WALLIX کار کرده باشید به طور کامل با ضعف‌های پوسته آن آشنا شده‌اید. پنجره‌های کوچک و متعدد که در قالب Div ها برای یک عملیات ساده ظاهر می‌شوند خسته‌کننده هستند. امکان اعمال تغییرات به صورت دسته‌ای هم وجود ندارد. برای مثال اگر تصمیم به تغییر Policy چند Device داشته باشید باید تک تک اقدام کنید در حالی که در نرم‌افزارهای مشابه مانند PAM360 این امکان فراهم هست و می‌توانید یک عملیات خاص را به صورت دسته‌ای برای چند آبجکت انجام دهید.

این پروژه مبتنی بر API های سامانه Bastion توسعه داده شده است و به سرور یا دسترسی خاصی نیاز ندارد. این ابزار با یک کاربر Admin با دسترسی محدود و کنترل‌شده کار می‌کند. این ابزار می‌تواند چهار مولفه از Device را که شامل نام، آدرس، توضیحات و برچسب است اصلاح کند. همچنین می‌توانید سرویس‌های هر Device را با این پروژه ساده‌تر مدیریت کنید. امکاناتی که اکنون در این پروژه در دسترس است شامل موارد زیر است:

✅ امکان اصلاح نام Device فراهم است

✅ امکان اصلاح IP/FQDN/SubnetIP فراهم است

✅ امکان اصلاح Description فراهم است

✅ امکان اصلاح Alias فراهم است

✅ امکان اصلاح Sub-Protocol های Service های منتسب به Device و شماره پورت فراهم است

✅ امکان حذف Service های منتسب به Device فراهم است


امکاناتی که اکنون در دسترس نیست شامل موارد زیر است:

❌ امکان اضافه کردن Device فراهم نیست

❌ امکان حذف Device فراهم نیست

❌ امکان اضافه کردن Service فراهم نیست | ✅ این ویژگی اضافه شد. 


💎 تمام Policy ها و محدودیت های برای کار با Device ها در نظر گرفته شده است مانند کاراکترهای مجاز برای نام‌گذاری و بررسی رعایت فرمت IP/FQDN/SubnetIP برای آدرس سامانه‌های مقصد و سایر موارد مشابه.

گام بعدی اضافه کردن امکاناتی است که اکنون برای Device ها پشتیبانی نمی‌شود که پیش‌تر ذکر شد.

در پایین صفحه یک کنسول قرار داده شده است تا تمام لاگ‌ها و خطاهای احتمالی قابل مشاهده شود و خطایابی انجام شود. این ابزار به گسترش پروژه بسیار کمک خواهد کرد.

💡 گام‌های آتی شامل گسترش پروژه برای تمام موارد مانند کاربران، گروه‌های کاربری، گروه‌های سرورها و Authorization خواهد بود.


**🚨 باگ‌های کشف‌شده به شرح زیر است:**

⚠️ اضافه کردن Device بدون نام ممکن است! نکته جالب توجه این است که می‌توانید به کمک API ها Device اضافه کنید که نام نداشته باشد. این موضوع میتواند یکی از خطرات جدی باشد که امنیت یک سازمان بزرگ و IT محور رو تهدید کند، چرا که شما میتوانید یک Device بدون نام ایجاد کنید و احتمالا در اختیار کاربر قرار دهید، در حالی که در UI چنین دستگاهی وجود ندارد و احتمالا امکان پیدا کردن آن نیز برای شما فراهم نیست، چرا که UI تنها میتواند Device هایی را نمایش دهد که نام داشته باشد و جست و جو بر اساس ID ممکن نیست.
این مورد برای سامانه PAM که مسئول مدیریت دسترسی به سامانه‌های حیاتی سازمان‌هاست قابل توجه است و سازمان‌ها باید با دقت بیشتری سراغ چنین محصولاتی بروند و ریسک‌های آن را بپذیرند چون معمولا چنین سکوهایی به دلیل پاسخگو نبودن در داخل کشور هیچ مسئولیتی را تقبل نخواهند کرد.

⚠️ تغییر شماره Port سرویس یک Device که کاربر اجازه دسترسی به آن را تحت یک Protocol خاص را ندارد امکان‌پذیر است. اگر کاربری از طریق گروه‌ها به یک مقصد دسترسی داشته باشد ولی این دسترسی از بخش Authorization محدود شده باشد کاربر می‌تواند از طریق API ها شماره Port را تغییر دهد. ریسک و اهمیت این موضوع زمانی مشخص می‌شود که کاربر صرفا End-User باشد ولی به واسطه مشاهده یک Device بتواند به دلیل ساختار ایجاد دسترسی در PAM کانفیگ‌های Device را تغییر دهد. فرض کنید یک Device روی یک شماره پورت صرفا به کاربران نوع User سرویس می‌دهد و روی شماره پورت دیگر به کاربران Administrator یا Root خدمات می‌دهد. با یک تغییر پورت ساده کاربر می‌تواند دسترسی خود را ارتقا دهد و ریسک‌های بسیار خطرناکی برای سازمان ایجاد کند. نکته جالب توجه اینجاست که سازمان های بزرگ و حیاتی با هدف پوشش چنین ریسک هایی به استفاده از PAM روی می آورند که از این پس باید در انتخاب محصول و پیمانکار آن، استقرار و بهره برداری از سامانه ها دقت بسیار بیشتری داشته باشند.
ذکر این نکته خالی از لطف نیست که ارائه دهندگان محصولات نرم افزاری آن هم با رویکرد کاملا تجاری بی تردید با جزئیات بیشتری از محصول آشنا هستند، ولی بیم آن وجود دارد که به دلیل مسائل تجاری از عنوان کردن آنها صرف نظر کنند.



این پروژه در حال توسعه است و مسئولیت بهره‌برداری از این پروژه و استفاده از آن با کاربر استفاده‌کننده است و توسعه‌دهنده هیچ مسئولیتی نمی‌پذیرد.
---
---

### Update: Added the ability to add Services to Devices.
---
Based on a suggestion from a friend, I decided to write a user-friendly skin for WALLIX Bastion, which I have currently started with the Devices section and a set of features.

If you have worked with WALLIX, you are fully familiar with the weaknesses of its interface. Numerous small windows appearing in the form of Divs for a simple operation are frustrating. There is also no possibility for bulk changes. For example, if you decide to change the Policy of several Devices, you must act one by one, whereas in similar software like PAM360, this possibility is provided and you can perform a specific operation in bulk for several objects.

This project is developed based on the Bastion system APIs and does not require a server or special access. This tool works with an Admin user with limited and controlled access. This tool can modify four Device components including Name, Address, Description, and Alias. You can also manage the Services of each Device more easily with this project. The features currently available in this project include the following:

✅ Ability to modify Device Name is provided

✅ Ability to modify IP/FQDN/SubnetIP is provided

✅ Ability to modify Description is provided

✅ Ability to modify Alias is provided

✅ Ability to modify Sub-Protocols of Services assigned to the Device and Port Number is provided

✅ Ability to delete Services assigned to the Device is provided

Features that are currently NOT available include:

❌ Ability to add a Device is not provided

❌ Ability to delete a Device is not provided

❌ Ability to add a Service is not provided | ✅ This feature has been added.

💎 All Policies and limitations for working with Devices have been considered, such as allowed characters for naming and checking compliance with IP/FQDN/SubnetIP formats for destination system addresses and other similar cases.

The next step is to add features that are not currently supported for Devices, which were mentioned earlier.

At the bottom of the page, a console is placed so that all logs and possible errors can be observed and troubleshooting can be performed. This tool will greatly help the expansion of the project.

💡 Future steps will include expanding the project for all items such as Users, User Groups, Server Groups, and Authorization.

## 🚨 Discovered bugs are as follows: ##

⚠️ Adding a Device without a name is possible! The interesting point is that you can add a Device without a name using APIs. This issue can be one of the serious threats to the security of a large IT-oriented organization, because you can create a nameless Device and probably provide it to a user, while such a device does not exist in the UI and it is probably not possible for you to find it either, because the UI can only display Devices that have a name and searching based on ID is not possible. This case is significant for the PAM system, which is responsible for managing access to critical systems of organizations, and organizations should approach such products with more caution and accept its risks, because usually such platforms will not accept any responsibility due to lack of accountability within the country.

⚠️ Changing the Port number of a Device service that the user does not have permission to access under a specific Protocol is possible. If a user has access to a destination through groups but this access is limited from the Authorization section, the user can change the Port number through APIs. The risk and importance of this issue becomes clear when the user is merely an End-User but can change Device configurations due to the access creation structure in PAM by observing a Device. Suppose a Device provides service on one port number only to User-type users and on another port number to Administrator or Root users. With a simple port change, the user can escalate their access and create very dangerous risks for the organization. The interesting point here is that large and vital organizations turn to using PAM with the aim of covering such risks, and from now on they must be much more careful in choosing the product and its contractor, deployment, and operation of the systems. It is worth mentioning that software product providers, especially with a purely commercial approach, are undoubtedly familiar with the product in more detail, but there is a fear that they may refrain from mentioning them due to commercial issues.

# This project is under development and the responsibility for the operation and use of this project lies with the user, and the developer accepts no responsibility.
