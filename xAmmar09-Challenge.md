**السلام عليكم ورحمة الله وبركاته**

  _**Write up xAmmar09 challenge**_

التحدي عبارة عن OSINT + Crypto
الهدف الحصول على معلومات الـAttacker

الجزء الأول:
لقد رأى المحقق في بداية تحقيقه عن هذا الرمز المشفر : 
`0bfd63bf104e8eaeea30126f1d4e245c010889ea`
ومن هنا بدأ التحدي, وفي نهاية هذا الجزء سوف تكون النتيجة = IP attacker


**نبدأ بالحل**


**الخطوة الأولى:**
بالبداية لاحظنا ان الرمز عباره عن hash 
ننسخ الhash ونفك التشفير في موقع [crackstation](https://crackstation.net/)

![Desktop Screenshot ا- 11 42 03 38](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/ec0f709c-47b6-4305-8fc1-c10b9a0b07e2)

والان ظهر لنا اسم شخص (**aleksandrnichole**) 

**الخطوة الثانية:** 
نبدأ نسوي OSINT على اسم aleksandrnichole ...

نلاحظ انه يوجد حساب في Instagram بأسم aleksandrnichole

![Desktop Screenshot 2024 04 11 - 11 556 02 19](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/7d1afc04-0b3b-4a4e-887a-ddec18cf01ae)

ويوجد رسالة غريبه باللغة الروسية ورمز مشفر 


![Desktop Screenshot 2024 04 11 - 11 56 553 93](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/1a66bd39-4912-4189-b44f-7ba37cc0c0d4)

**ترجمة الرسالة:**
تهانينا، أنت على الطريق الصحيح.
استمروا في العمل الجيد مع هذا التحدي. لقد أرسلت الرمز إلى صديقي، وآمل ألا يتمكن أحد من فك شفرته.
 `87777777.88777888.77777877.87877888`


**الخطوة الثالثة:**
نبدأ بتحليل الرمز 
نلاحظ انه متكون من رقمين 7 و 8 
وبمجموع 32 رقم بين كل 8 ارقام نقطة ( . )
وهذا مشابه لتشفير binary + اربع نقاط مشابه لعنوان IP

الان نحول الأرقام الى 0 و 1 لفك التشفير ( 8 ⮂ 1 | 7 ⮂ 0 )
= `10000000.11000111.00000100.10100111`

الان ننسخ الرمز بعد تحويله الى binary وثم نذهب الى موقع [browserling](https://www.browserling.com/tools/bin-to-ip)
لفك تشفير Binary IP الى Regular IP Address

![Desktop Screenshot 2024 04 11 - 12 23 345 69](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/1bd9583d-ddd3-4632-9089-020cfb04ebed)

بعد فك التشفير ظهر لنا عنوان IP = 128.199.4.167


**الخطوة الرابعة:** 
نبحث عن العنوان ونلاحظ انه دخلنا على صفحة Apache2 Debian Default

![Desktop Screenshot 2024 04 11 - 12 30 553 06](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/306c228a-8cac-41e3-8f9a-17852cee8273)

بعدها ندخل ونبحث في page source

![Desktop Screenshot 2024 04 11 - 12 258 26 71](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/b2415790-ba6a-4b76-82ec-31298aa5ecde)

الان وجدنا مسار 
`_19228188281_security.txt `
ورمز تلميحه للجزء الأول 
`ZSITP7GOAWDJD7QKAO8JD7QKY9LGRZWFSMHUV8YZ`


**الخطوة الخامسة:** 
الان بعد ما وجدنا المسار نبحث عنه 
`http://128.199.4.167/_19228188281_security.txt `

![Desktop Screenshot 2024 04 11 - 12 356 40 09](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/a1a4b5ec-3c75-44a0-8cfa-4cd6c8a58426)

نرى يوجد رسالة مشفره Base64 
نذهب الى موقع [base64decode](https://www.base64decode.org/) ونفك التشفير 

![Desktop Screenshot 2024 04 11 - 12 40 007 72](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/7a3c9243-30eb-4b92-9a41-2fab291b73ed)

**ترجمة الرسالة:** 
إذا حصلت على الرمز الذي لصقته في تعليق، فاعلم أنني قمت بتشفيره باستخدام ROT18، ولكن إذا كسره شخص ما، فلا تقلق، فقد قمت بتشفيره بتشفير مختلف لأنني قلق من كشف معلوماتك الشخصية.

نلاحظ ان تم تشفير الرمز 
`ZSITP7GOAWDJD7QKAO8JD7QKY9LGRZWFSMHUV8YZ`
 بواسطة ROT18 وتشفير اخر 


**الخطوة السادسة:**
الان ننسخ الرمز 
`ZSITP7GOAWDJD7QKAO8JD7QKY9LGRZWFSMHUV8YZ`
ونفك التشفير هنا [dencode](https://dencode.com/cipher/rot18)

![‏‏لقطة الشاشة (1)](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/3d9ab824-4524-4be1-a1be-17e6d3f4afe8)

نلاحظ انه فك التشفير الى 
`MFVGC2TBNJQWQ2DXNB3WQ2DXL4YTEMJSFZUHI3LM`

والتشفير الاخر Base32 في موقع [CyberChef](https://gchq.github.io/CyberChef/)

![‏‏لقطة الشاشة (2)](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/8fd8131e-6851-4e15-aa6f-cb4e65264816)

الان كما نرى ظهر لنا مسار اخر
 `ajajajahhwhwhhw_1212.html` 


الخطوة الأخيرة:
الان نذهب الى **128.199.4.167** 
ونضع المسار  **ajajajahhwhwhhw_1212.html** 
`http://128.199.4.167/ajajajahhwhwhhw_1212.html`

![‏‏لقطة الشاشة (3)](https://github.com/TargaRayan/CTF-Write-up/assets/160002524/b92a6c6f-c29f-4971-956d-5595701b5ae7)


**وأخيرا نرى معلومات الـAttacker**  🎉
