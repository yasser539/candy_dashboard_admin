# دليل تحويل روابط الصور

## نظرة عامة
هذا الدليل يشرح كيفية تحويل روابط الصور من المسارات المحلية إلى الروابط المباشرة في قاعدة البيانات.

## المتطلبات

### 1. متغيرات البيئة
تأكد من وجود متغيرات البيئة التالية:
```bash
NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### 2. تثبيت التبعيات
```bash
npm install @supabase/supabase-js
```

## تشغيل السكريبت

### الطريقة الأولى: تشغيل مباشر
```bash
node migrate-image-urls.js
```

### الطريقة الثانية: تشغيل مع متغيرات البيئة
```bash
NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co \
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key \
node migrate-image-urls.js
```

### الطريقة الثالثة: استخدام ملف .env
1. أنشئ ملف `.env` في مجلد المشروع
2. أضف المتغيرات:
```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```
3. شغل السكريبت:
```bash
node migrate-image-urls.js
```

## ما يفعله السكريبت

### 1. تحويل الإعلانات
- يبحث عن جميع الإعلانات في جدول `ads`
- يتحقق من روابط الصور
- يحول المسارات المحلية إلى روابط مباشرة
- يحدث قاعدة البيانات

### 2. تحويل المنتجات
- يبحث عن جميع المنتجات في جدول `products`
- يتحقق من روابط الصور
- يحول المسارات المحلية إلى روابط مباشرة
- يحدث قاعدة البيانات

## مثال على التحويل

### قبل التحويل:
```sql
-- في قاعدة البيانات
image_url: "ads/1754343268635-screenshot.png"
```

### بعد التحويل:
```sql
-- في قاعدة البيانات
image_url: "https://your-project-ref.supabase.co/storage/v1/object/public/img/ads/1754343268635-screenshot.png"
```

## المخرجات المتوقعة

```
🔧 بدء تحويل روابط الصور...
📋 Project Ref: your-project-ref

📤 جلب جميع الإعلانات...
📊 تم العثور على 5 إعلان

🔄 تحديث الإعلان 1:
   من: ads/1754343268635-screenshot.png
   إلى: https://your-project-ref.supabase.co/storage/v1/object/public/img/ads/1754343268635-screenshot.png
✅ تم تحديث الإعلان 1

⏭️ تخطي الإعلان 2 (رابط مباشر موجود)

📈 ملخص التحويل:
✅ تم تحديث: 4 إعلان
⏭️ تم تخطي: 1 إعلان
📊 المجموع: 5 إعلان

📤 جلب جميع المنتجات...
📊 تم العثور على 10 منتج مع صور

🔄 تحديث المنتج 1:
   من: products/product-1.jpg
   إلى: https://your-project-ref.supabase.co/storage/v1/object/public/img/products/product-1.jpg
✅ تم تحديث المنتج 1

📈 ملخص تحويل المنتجات:
✅ تم تحديث: 8 منتج
⏭️ تم تخطي: 2 منتج
📊 المجموع: 10 منتج

🎉 تم الانتهاء من عملية التحويل!
💡 الآن جميع الصور تستخدم الروابط المباشرة
```

## الأمان

### قبل التشغيل
1. **احفظ نسخة احتياطية** من قاعدة البيانات
2. **اختبر السكريبت** على بيئة التطوير أولاً
3. **تحقق من الصلاحيات** - تأكد من أن المستخدم لديه صلاحيات الكتابة

### بعد التشغيل
1. **تحقق من النتائج** في قاعدة البيانات
2. **اختبر التطبيق** للتأكد من عمل الصور
3. **احفظ نسخة احتياطية** من البيانات المحدثة

## استكشاف الأخطاء

### خطأ: "Cannot find module '@supabase/supabase-js'"
```bash
npm install @supabase/supabase-js
```

### خطأ: "Environment variables not set"
تأكد من تعيين متغيرات البيئة:
```bash
export NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
export NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### خطأ: "Cannot extract project-ref"
تأكد من صحة URL في متغير البيئة:
```bash
# صحيح
NEXT_PUBLIC_SUPABASE_URL=https://abcd1234.supabase.co

# خطأ
NEXT_PUBLIC_SUPABASE_URL=https://supabase.co/project/abcd1234
```

### خطأ: "Permission denied"
تأكد من صلاحيات الكتابة في قاعدة البيانات:
```sql
-- تحقق من الصلاحيات
GRANT UPDATE ON ads TO authenticated;
GRANT UPDATE ON products TO authenticated;
```

## التراجع عن التغييرات

إذا احتجت للتراجع عن التغييرات:

### 1. استعادة النسخة الاحتياطية
```bash
# استعادة قاعدة البيانات من النسخة الاحتياطية
psql -d your_database -f backup.sql
```

### 2. تحويل الروابط المباشرة إلى مسارات محلية
```javascript
// سكريبت للتراجع (يمكن إنشاؤه عند الحاجة)
function revertToLocalPaths() {
  // تحويل الروابط المباشرة إلى مسارات محلية
  const localPath = publicUrl.replace(/https:\/\/[^\/]+\/storage\/v1\/object\/public\/img\//, '');
  return localPath;
}
```

## الدعم

إذا واجهت أي مشاكل:
1. تحقق من سجلات الأخطاء
2. تأكد من صحة متغيرات البيئة
3. اختبر الاتصال بقاعدة البيانات
4. راجع صلاحيات المستخدم 