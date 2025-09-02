# دليل الإعداد السريع لكباتن التوصيل

## 🚀 الإعداد السريع (5 دقائق)

### 1. قاعدة البيانات
```sql
-- انسخ محتوى ملف delivery_captains_setup.sql
-- نفذه في Supabase SQL Editor
```

### 2. Storage Bucket
```
1. اذهب إلى Supabase → Storage
2. أنشئ bucket باسم: captain-profiles
3. حدد: Public bucket ✅
4. File size limit: 5MB
5. Allowed MIME types: image/*
```

### 3. سياسات Storage
```sql
-- نفذ في SQL Editor
CREATE POLICY "Allow public read access to captain profiles" 
ON storage.objects FOR SELECT 
USING (bucket_id = 'captain-profiles');

CREATE POLICY "Allow authenticated users to upload captain profiles" 
ON storage.objects FOR INSERT 
WITH CHECK (bucket_id = 'captain-profiles' AND auth.role() = 'authenticated');

CREATE POLICY "Allow authenticated users to delete captain profiles" 
ON storage.objects FOR DELETE 
USING (bucket_id = 'captain-profiles' AND auth.role() = 'authenticated');
```

### 4. اختبر التطبيق
```
1. شغل التطبيق: npm run dev
2. اذهب إلى: /delivery-captains
3. ستجد 8 كباتن تجريبيين
```

## ✅ الملفات المحدثة

- ✅ `src/lib/supabase.ts` - أنواع البيانات الجديدة
- ✅ `src/lib/supabase-services.ts` - خدمات محدثة
- ✅ `src/app/delivery-captains/page.tsx` - صفحة جديدة
- ✅ `src/app/components/Sidebar.tsx` - رابط في القائمة

## 📊 الميزات المتاحة

- 👥 **8 كباتن تجريبيين** مع بيانات كاملة
- 📈 **إحصائيات الأداء** (التوصيلات، التقييم، الأرباح)
- 🚗 **معلومات المركبة** (النوع، الموديل، اللوحة)
- 📍 **معلومات الموقع** (المنطقة، المدينة)
- 🔄 **تحديث تلقائي** للأداء
- 📱 **واجهة متجاوبة** للجوال

## 🎯 النتيجة النهائية

بعد التنفيذ ستجد:
- صفحة كباتن التوصيل في القائمة الجانبية
- 8 كباتن تجريبيين مع بيانات كاملة
- إحصائيات شاملة للأداء
- إمكانية إضافة وتعديل وحذف الكباتن

## 🆘 استكشاف الأخطاء

### مشكلة: لا تظهر البيانات
```bash
# تحقق من تنفيذ SQL
# تأكد من وجود بيانات في جدول delivery_captains
```

### مشكلة: لا ترفع الصور
```bash
# تأكد من إنشاء bucket captain-profiles
# تحقق من سياسات Storage
```

### مشكلة: أخطاء في التطبيق
```bash
# أعد تشغيل التطبيق
npm run dev
```

## 📞 الدعم

إذا واجهت أي مشاكل:
1. تحقق من console المتصفح
2. تأكد من تنفيذ جميع الخطوات
3. تحقق من إعدادات Supabase
