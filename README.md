# جفجير

## 1) إنشاء مشروع Firebase
1. ادخل https://console.firebase.google.com وأنشئ مشروعاً جديداً.
2. **Authentication > Sign-in method**: فعّل **Google** و **Anonymous** (الأخير للتعليق كزائر).
3. **Firestore Database**: أنشئ قاعدة بيانات (Production mode).
4. **Storage**: فعّله لرفع الصور والفيديو (قد يتطلب Firebase خطة Blaze، وهي مجانية ضمن الحد الأدنى للاستخدام).
5. **Project settings > Your apps > Web (</>)**: سجّل تطبيق ويب وانسخ الإعدادات.

## 2) ضبط الملفات
- `firebase-config.js`: الصق الإعدادات وضع بريد الأدمن في `ADMIN_EMAIL`.
- `firestore.rules` و `storage.rules`: استبدل `your@gmail.com` ببريد الأدمن نفسه (ثلاثة مواضع في الملفين).

## 3) النشر
```
npm i -g firebase-tools
firebase login
firebase use --add        # اختر مشروعك
firebase deploy
```
بعد النشر ستحصل على رابط مثل `https://YOUR_PROJECT.web.app`. ادخل بحساب جوجل الأدمن، وسيظهر زر «+ وصفة». أول عملية حفظ تنقل الوصفات الأساسية إلى قاعدة البيانات تلقائياً.

## 4) GitHub
```
git init
git add .
git commit -m "Jafjeer"
git branch -M main
git remote add origin https://github.com/USER/jafjeer.git
git push -u origin main
```
(إعدادات Firebase في الواجهة ليست سرّية، والحماية الفعلية في ملفات rules.)
إن نشرت من GitHub Pages فأضف نطاقه في **Authentication > Settings > Authorized domains**.

## 5) الإعلانات (AdSense)
- تحتاج غالباً دومين خاصاً بك وموافقة Google AdSense.
- أضف سكربت AdSense داخل `<head>` في `index.html`، ثم ضع وحدة الإعلان داخل `<div class="ad" id="adslot">` بدل النص.

## 6) تطبيق الجوال
- **سريعاً:** افتح الرابط في كروم أندرويد > «إضافة إلى الشاشة الرئيسية» (الملف manifest.json جاهز).
- **للمتاجر:** تحويل الصفحة إلى Flutter أو Capacitor في خطوة لاحقة.
