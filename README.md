# Candy Dashboard Admin

نظام إدارة متكامل لتطبيق توصيل الحلويات مع لوحة تحكم إدارية متقدمة.

## المميزات

### 🔐 نظام الصلاحيات المتقدم
- إدارة صلاحيات مفصلة لكل مستخدم
- 22 صلاحية مختلفة تغطي جميع جوانب النظام
- تحكم دقيق في الوصول للصفحات والوظائف

### 📊 لوحة تحكم شاملة
- **إدارة الطلبات**: تتبع حالة الطلبات وتحديثها
- **الخريطة الحية**: مراقبة التوصيل في الوقت الفعلي
- **إدارة المستخدمين**: العملاء والتجار والموظفين
- **إدارة المنتجات**: المخزون والمنتجات
- **التقارير**: تقارير مفصلة وإحصائيات
- **سجل العمليات**: تتبع جميع العمليات
- **نظام الإشعارات**: إشعارات ذكية للمستخدمين

### 🎨 واجهة مستخدم حديثة
- تصميم متجاوب يعمل على جميع الأجهزة
- ألوان جميلة ومتسقة
- تجربة مستخدم سلسة وسهلة

## التقنيات المستخدمة

- **Frontend**: Next.js 15, React 19, TypeScript
- **Styling**: Tailwind CSS
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **Icons**: Lucide React
- **Deployment**: Vercel (مقترح)

## الإعداد والتشغيل

### المتطلبات
- Node.js 18+
- npm أو yarn
- حساب Supabase

### خطوات الإعداد

1. **استنساخ المشروع**
```bash
git clone https://github.com/yasser539/candy-dashboard-admin.git
cd candy-dashboard-admin
```

2. **تثبيت التبعيات**
```bash
npm install
```

3. **إعداد Supabase**
   - اتبع دليل الإعداد في `SUPABASE_SETUP.md`
   - أنشئ مشروع Supabase جديد
   - نفذ ملف `database_schema.sql`
   - نفذ ملف `sample_data.sql` للبيانات الافتراضية

4. **إعداد متغيرات البيئة**
```bash
# أنشئ ملف .env.local
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

5. **تشغيل المشروع**
```bash
npm run dev
```

6. **فتح التطبيق**
   - اذهب إلى `http://localhost:3000`
   - سجل دخول باستخدام:
     - المدير: `admin@example.com` / `123456`
     - الموظف: `employee@example.com` / `123456`

## هيكل قاعدة البيانات

### الجداول الرئيسية
- **users**: المستخدمين (المديرين والموظفين)
- **permissions**: صلاحيات المستخدمين
- **customers**: العملاء
- **merchants**: التجار
- **employees**: الموظفين (كباتن التوصيل)
- **products**: المنتجات
- **inventory**: المخزون
- **orders**: الطلبات
- **notifications**: الإشعارات
- **audit_log**: سجل العمليات
- **support_tickets**: تذاكر الدعم
- **reports**: التقارير

### العلاقات
- كل مستخدم له صلاحيات في جدول `permissions`
- كل طلب مرتبط بعميل وتاجر وموظف (اختياري)
- كل منتج مرتبط بتاجر
- كل مخزون مرتبط بمنتج

## نظام الصلاحيات

### الصلاحيات المتاحة (22 صلاحية)

#### صلاحيات العرض الأساسية
- `canViewDashboard` - عرض لوحة التحكم
- `canViewOrders` - عرض الطلبات
- `canViewLiveMap` - عرض الخريطة الحية
- `canViewUsers` - عرض العملاء
- `canViewMerchants` - عرض التجار
- `canViewEmployees` - عرض الموظفين
- `canViewProducts` - عرض المنتجات
- `canViewInventory` - عرض المخزون
- `canViewReports` - عرض التقارير
- `canViewAuditLog` - عرض سجل العمليات
- `canViewSupport` - عرض الدعم
- `canViewPermissions` - عرض الصلاحيات

#### صلاحيات الإدارة
- `canModifyUsers` - تعديل وحذف مستخدمين
- `canAssignDeliverer` - تعيين موصل للطلب
- `canAddProducts` - إضافة منتج جديد
- `canModifyPrices` - تعديل الأسعار
- `canExportReports` - تصدير تقارير شاملة
- `canUpdateOrderStatus` - تحديث حالة الطلب
- `canSendNotifications` - إرسال إشعارات عامة
- `canProcessComplaints` - معالجة الشكاوى
- `canManageMerchants` - إدارة التجار
- `canManageEmployees` - إدارة الموظفين
- `canManageInventory` - إدارة المخزون

## الملفات المهمة

### إعداد Supabase
- `src/lib/supabase.ts` - تكوين Supabase
- `src/lib/supabase-services.ts` - خدمات قاعدة البيانات
- `database_schema.sql` - هيكل قاعدة البيانات
- `sample_data.sql` - البيانات الافتراضية
- `SUPABASE_SETUP.md` - دليل إعداد Supabase

### المكونات الرئيسية
- `src/app/components/Layout.tsx` - التخطيط الرئيسي
- `src/app/components/Sidebar.tsx` - الشريط الجانبي
- `src/app/components/ProtectedRoute.tsx` - حماية الصفحات
- `src/app/context/AuthContext.tsx` - إدارة المصادقة والصلاحيات

### الصفحات
- `src/app/page.tsx` - الصفحة الرئيسية
- `src/app/orders/page.tsx` - إدارة الطلبات
- `src/app/live-map/page.tsx` - الخريطة الحية
- `src/app/permissions/page.tsx` - إدارة الصلاحيات
- `src/app/users/page.tsx` - إدارة العملاء
- `src/app/merchants/page.tsx` - إدارة التجار
- `src/app/employees/page.tsx` - إدارة الموظفين
- `src/app/products/page.tsx` - إدارة المنتجات
- `src/app/inventory/page.tsx` - إدارة المخزون
- `src/app/reports/page.tsx` - التقارير
- `src/app/audit-log/page.tsx` - سجل العمليات
- `src/app/support/page.tsx` - الدعم
- `src/app/notifications/page.tsx` - الإشعارات

## النشر

### Vercel (مقترح)
```bash
npm install -g vercel
vercel
```

### متغيرات البيئة للإنتاج
```env
NEXT_PUBLIC_SUPABASE_URL=your_production_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_production_supabase_anon_key
```

## المساهمة

1. Fork المشروع
2. أنشئ branch جديد (`git checkout -b feature/amazing-feature`)
3. Commit التغييرات (`git commit -m 'Add amazing feature'`)
4. Push إلى Branch (`git push origin feature/amazing-feature`)
5. أنشئ Pull Request

## الترخيص

هذا المشروع مرخص تحت رخصة MIT - راجع ملف `LICENSE` للتفاصيل.

## الدعم

إذا واجهت أي مشاكل أو لديك أسئلة:

1. راجع ملف `SUPABASE_SETUP.md`
2. تحقق من Issues في GitHub
3. أنشئ Issue جديد مع تفاصيل المشكلة

## المطور

تم تطوير هذا المشروع بواسطة فريق تطوير متخصص في تطبيقات إدارة الأعمال.

---

**ملاحظة**: تأكد من إعداد Supabase بشكل صحيح قبل تشغيل المشروع. راجع `SUPABASE_SETUP.md` للحصول على تعليمات مفصلة.
