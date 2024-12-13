---

---
---

# The Story

![Task banner for day DAY 1](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/5fc2847e1bbebc03aa89fbf2-1730193392309.svg)

_McSkidy tapped keys with a confident grin,_

_A suspicious website, now where to begin?_

_She'd seen sites like this, full of code and of grime,_

_Shady domains, and breadcrumbs easy to find._

---

كل عام وانتم بخير نهايه 2024 قربت وبدأ Advent of Cyber 2024 زي كل سنه.
في اليوم الاول هنتعلم ازاي نحقق في ملفات الروابط الضارة (Malicious Link Files) .. وكمان هنفهم إيه هو OPSEC وأهميته؟
وهنتعلم تتبع الهويات الرقمية وربطها بأشخاص حقيقيين ... خلينا نفهم السيناريو الاول عن ايه وايه مطلوب مننا نعمله

الموقع اللي بنحقق فيه اسمه **"The Glitch's All-in-One Converter"** هو أداة لتحويل فيديوهات YouTube إلى ملفات MP3، وبيتم تداوله بين منظمي SOC-mas الموقع شكله في البداية شرعي وجذاب وفي صفحة "About" بتقول إن الموقع معمول بواسطة "The Glitch"
هنلاقي في الموقع برضو بيقول إن خدماته "آمنة" و"محمية"، لكن من خبرتنا دي غالبًا مجرد كلام تسويقي ومش صحيح 🤔
**طيب ليه بنقول انه مش آمن او ايه هي التهديدات المحتمله من الموقع دا؟**

>[!bug] Malvertising (الإعلانات الضارة):
> كتير من المواقع دي بتعرض إعلانات خبيثة الإعلانات دي ممكن تستغل ثغرات في أجهزة المستخدم، وتوصل برمجيات خبيثة.
>- مثال: ظهور نوافذ منبثقة (Pop-ups) مزعجة تطلب تحميل تحديثات مزيفة.

>[!bug] Phishing Scams (احتيال التصيد الإلكتروني)
>ممكن يطلب منك الموقع ملء استبيانات أو تقديم بيانات شخصية بحجة تقديم الخدمة والبيانات دي ممكن تُستخدم في هجمات احتيال لاحقة.

>[!bug] Bundled Malware (البرمجيات الضارة المرفقة)
>أحيانًا الملفات المحملة من الموقع بيكون فيها برمجيات خبيثة بالتالي المستخدم ممكن يثبت برامج ضارة على جهازه بدون ما ياخد باله، زي أدوات Keyloggers أو Trojans ودا اللي هيحصل معانا انهارده

---
طبعا Tryhackme وضح بالفعل ازاى نبدأ نحقق في الموقع والادوت اللي هنستخدمها والخطوات الاول اللي على اساسها هنبدأ نحل باقي الاسئله فأنا هاختصر واعمل نبذه توضيحيه عن الخطوات والادوات اللي تم توضيحها في الروم وكمان اوضح النتائج اللي وصلنا لها والخطورة بتاعتها

### Investigation Steps 

>[!quote] خطوات التحقيق 
>في البدايه هنشغل الماشين عشان نفتح الموقع زي ماهو موضح في الروم ونخلي بالنا اننا منعملش Download او نفتح حاجه على نظامنا الاساسي
>بعد كدا من الخطوات اللي موجودة في الروم هي اننا نجرب نحول فيديو ونعمله download اللي بينزل كملف zip ثم نعمله **Extract** 
>هيظهرلنا ملف اسمه song.mp3 وملف تاني اسمه somg.mp3 ومن تحليلنا للملف الاول طلع ان مفيش حاجه suspicious
>لكن الملف التاني هو اللي ضار ﻷن بدل ما يكون الملف MP3، طلع "MS Windows shortcut" أو المعروف بملف `**.lnk**`

#### إيه هو ملف .lnk؟

>ملفات `.lnk` هي اختصارات في نظام تشغيل ويندوز. بتُستخدم لربط ملف، مجلد، أو برنامج معين على سطح المكتب مثلًا، الاختصارات اللي بتفتح البرامج زي المتصفح أو الألعاب هي ملفات .lnk
>**طيب واضح انه برنامج عادي ليه قلنا انه ضار؟**
>ﻷن الـ Attackers ممكن يستغلوا النوع ده من الملفات لتشغيل Commands مباشرة على جهازك بدل ما الملف يربطك بأغنية MP3، ممكن يشغل سكريبت خبيث أو يشغل برمجية ضارة في الخلفية زي الـ Powershell script اللي وصلنا له مع tryhackme

---
طيب تمام كدا احنا عرفنا ان الملف خطير وعرفنا السبب بعدا ما استخدمنا 2 tools مع THM وممكن نستخدم ادوات تانيه برضو زي Virustotal:

بنعمل upload للملف او بناخد الهاش باستخدام الكوماند دا:


![[md5.png]]

وبعدين نفحصه باستخدام Virustotal

![[Cyber Advent/assets/Selection_060.png]]

![[Cyber Advent/assets/Selection_061.png]]

خلينا نوضح الادوات والاوامر اللي استخدمناها في التحقيق:****

|**Tool/Command**|**Purpose**|**How to Use**|**Output**|
|---|---|---|---|
|**Command `file`**|- Identify the file type.|`file <filename>`|- Displays the file type, e.g., "MS Windows shortcut", "PNG image".|
|**Tool `exiftool`**|- Extract metadata from files.|`exiftool <filename>`|- Shows details like author name, creation date, and file properties.|
|**VirusTotal**|- Analyze files or URLs for malware or suspicious activity.|- Upload the file on VirusTotal website or use the API for scanning.|- Provides a detailed report: malicious or safe, hash info, and file behavior.|

---
### PowerShell script

**احنا لما استخدمنا exiftool ظهر لنا powershell command وتفاصيلة كانت:**

![[exif 1.png]]

#### 1. الـ Flags `-ep Bypass` و `-nop`:

الأعلام دي (Flags) بتتضاف لأوامر PowerShell عشان تلغي القيود العادية اللي بتمنع تشغيل سكريبتات غير موثوقة
الـ`-ep Bypass`: بتلغي الـ "Execution Policy" اللي بتحدد نوع السكريبتات المسموح بتشغيلها
الـ`-nop`: بتشغل PowerShell من غير ما تحمّل إعدادات الـ User Profile (الإعدادات الشخصية للمستخدم) بمعنى بسيط، بتفتح الباب لتشغيل السكريبتات بحرية من غير أي عقبات أمنية.

#### 2. استخدام `DownloadFile`:

الكود بيستخدم Method (طريقة) اسمها `DownloadFile` عشان يحمل ملف (في الحالة دي اسمه IS.ps1) من سيرفر بعيد وعنوان الملف: `https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1`  وبعد التنزيل بيتحط في فولدر: **`C:\ProgramData\`**

#### 3. تشغيل السكريبت باستخدام `iex`:

بعد ما الملف يتحمل على الجهاز، بيتنفذ باستخدام أمر `iex` اللي هو اختصار لـ **Invoke-Expression**.
الأمر ده بيشغّل السكريبت اللي تم تحميله (`IS.ps1`) باستخدام PowerShell والنتيجة هي ان الكود الضار الموجود في السكريبت يبدأ يشتغل على الجهاز

---
## Introduction to OPSEC

#### يعني إيه OPSEC؟

- الـ **OPSEC** هو اختصار لـ **Operational Security**، وده مفهوم أصله عسكري معناه حماية المعلومات الحساسة والعمليات من الوقوع في إيدين الخصوم
- الهدف منه إنك تكتشف وتلغي أي ثغرات ممكن المهاجم يستغلها عشان يعرف هويتك أو خططك

---

#### **إيه اللي بيحصل لو فيه فشل في OPSEC؟**

في عالم الأمن السيبراني، لما المهاجمين ما يتبعوش ممارسات OPSEC بشكل صحيح، ممكن يسيبوا آثار رقمية وراهم والآثار دي لو تم جمعها بذكاء، ممكن تكشف عن هويتهم 😬

---

#### **أخطاء شائعة في OPSEC:**

1. **إعادة استخدام أسماء الحسابات أو الإيميلات**:
    
    - لو المهاجم استخدم نفس الاسم أو البريد الإلكتروني على أكتر من منصة، ده بيسهّل تتبعه.
    - أحيانًا بيكون السبب غرور أو نسيان، لكن النتيجة واحدة: كشف الهوية.
2. **استخدام Metadata يمكن تعقبه**:
    
    - زي بيانات مخفية في الصور أو الكود (Metadata) اللي تكشف:
        - اسم الجهاز.
        - إحداثيات GPS.
        - الوقت والتاريخ.
3. **نشر معلومات بشكل علني**:
    - الكتابة في منتديات أو رفع أكواد على GitHub مع تفاصيل ممكن تتربط بهويتهم أو مكانهم
4. **عدم استخدام VPN أو Proxy أثناء النشاطات الخبيثة**:
    
    - ده يسمح للجهات الأمنية بتتبع عنوان الـ IP الحقيقي للشخص.

>**عندنا امثبه حقيقية عن OPSEC mistakes تم ذكرها في الروم**

---
## Questions:

##### 1. Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author?

![[Screenshot_2024-12-13_09-44-04.png]]

##### 2. The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server?

>هنلاقي الاجابه هنا https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1

##### 3. Who is M.M? Maybe his Github profile page would provide clues?
هنفتح اكونت github بتاعه وهنلاقي الاسم

![[Cyber Advent/assets/Selection_009.png]]

##### 4. What is the number of commits on the GitHub repo where the issue was raised?

![[Screenshot_2024-12-13_09-44-04 1.png]]