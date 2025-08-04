# تحديث جدول الإعلانات - Ads Table Update

## 📋 ملخص التحديثات

تم تحديث جدول `ads` في Supabase ليدعم إدارة Storage بشكل أفضل مع الحقول الجديدة.

## 🔄 التغييرات المطبقة

### 1. تحديث مخطط الجدول

**الحقول الجديدة:**
- `storage_bucket` (TEXT DEFAULT 'img') - اسم البكت في Storage
- `storage_path` (TEXT) - المسار الكامل للصورة داخل البكت

**الحقول الموجودة:**
- `id` (UUID) - رقم تعريفي فريد
- `image_url` (TEXT) - رابط الصورة العامة
- `created_at` (TIMESTAMP) - تاريخ الإنشاء

### 2. تحديث TypeScript Interfaces

```typescript
export interface Ad {
  id: string
  image_url: string
  storage_bucket: string
  storage_path?: string
  created_at: string
}
```

### 3. تحديث خدمات الإعلانات

**الخدمات الجديدة:**
- `uploadAdImage(file: File, fileName: string)` - رفع صورة إلى Storage
- `deleteAdImage(storagePath: string)` - حذف صورة من Storage

**الخدمات المحدثة:**
- `createAd()` - يدعم الآن `storage_path` و `storage_bucket`
- `updateAd()` - محدث للعمل مع الحقول الجديدة
- `deleteAd()` - يحذف الصورة من Storage أيضاً

### 4. تحديث واجهة المستخدم

**الميزات الجديدة:**
- رفع الصور مباشرة إلى Supabase Storage
- حذف الصور من Storage عند حذف الإعلان
- إدارة أفضل للملفات والمسارات

## 🚀 كيفية التطبيق

### 1. تحديث قاعدة البيانات

قم بتنفيذ ملف `updated_ads_table.sql` في Supabase SQL Editor:

```sql
-- تحديث الجدول الموجود
ALTER TABLE ads 
ADD COLUMN IF NOT EXISTS storage_bucket TEXT DEFAULT 'img',
ADD COLUMN IF NOT EXISTS storage_path TEXT;

-- إضافة الفهارس
CREATE INDEX IF NOT EXISTS idx_ads_storage_bucket ON ads(storage_bucket);
```

### 2. إعداد Storage Bucket

تأكد من وجود bucket باسم `img` في Supabase Storage:

1. اذهب إلى Supabase Dashboard
2. انتقل إلى Storage
3. أنشئ bucket باسم `img` إذا لم يكن موجوداً
4. اضبط السياسات المناسبة للوصول العام

### 3. اختبار الميزات

1. **رفع صورة جديدة:**
   - اذهب إلى صفحة "الإعلانات والإشعارات"
   - اضغط "إضافة إعلان جديد"
   - اختر صورة
   - ستتم رفع الصورة تلقائياً إلى Storage

2. **حذف إعلان:**
   - اضغط على أيقونة الحذف
   - ستتم إزالة الصورة من Storage تلقائياً

## 🔧 الملفات المحدثة

1. **`src/lib/supabase.ts`** - تحديث interface
2. **`src/lib/supabase-services.ts`** - إضافة خدمات Storage
3. **`src/app/notifications/page.tsx`** - تحديث واجهة المستخدم
4. **`updated_ads_table.sql`** - مخطط قاعدة البيانات المحدث

## 📊 الفوائد

### ✅ تحسينات الأداء
- تخزين منظم للصور
- إدارة أفضل للمساحة
- فهارس محسنة للبحث

### ✅ أمان محسن
- فصل البيانات عن الملفات
- تحكم أفضل في الوصول
- حذف آمن للملفات

### ✅ قابلية التوسع
- دعم أنواع ملفات متعددة
- إدارة بكتات متعددة
- تنظيم أفضل للمحتوى

## 🛠 استكشاف الأخطاء

### مشكلة: لا يمكن رفع الصور
**الحل:**
1. تحقق من وجود bucket `img`
2. تحقق من سياسات Storage
3. تأكد من صلاحيات المستخدم

### مشكلة: الصور لا تظهر
**الحل:**
1. تحقق من `image_url` في قاعدة البيانات
2. تأكد من أن الرابط صحيح
3. تحقق من إعدادات CORS

### مشكلة: حذف الإعلان لا يحذف الصورة
**الحل:**
1. تحقق من وجود `storage_path`
2. تأكد من صلاحيات حذف الملفات
3. تحقق من سجلات الأخطاء

## 📝 ملاحظات مهمة

1. **البيانات الموجودة:** الإعلانات الموجودة ستحتفظ بـ `image_url` فقط
2. **التوافق:** الكود متوافق مع الإعلانات القديمة والجديدة
3. **النسخ الاحتياطية:** احتفظ بنسخة احتياطية قبل التحديث
4. **الاختبار:** اختبر الميزات في بيئة التطوير أولاً

---

**تاريخ التحديث:** $(date)
**الإصدار:** 2.0.0 