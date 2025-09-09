# Rapid Project Design – Backend for Lenora Platform

> **Ready‑to‑paste plan** (Arabic + English). Put this file in your repo as `README.md` or share with your developer.

---

## 📆 Overview (نظرة عامة)

Backend for **Lenora**: multi‑role e‑commerce + influencer collaboration for the Arab female market.  
الخلفية (Backend) لمنصة **لينورا** تدعم أدوار متعددة ومتجر متعدد + تعاون المؤثرات + دروبشوبنق، مهيأة بالكامل للغة العربية وواجهة RTL.

---

## 1) 🔧 Technology Stack (التقنيات)

| Layer | Technology |
|---|---|
| Programming Language | PHP 8.x |
| Framework | Laravel 10+ |
| API Type | RESTful API + Webhooks |
| Database | MySQL 8 (Hostinger) |
| File Storage | Local أو S3‑compatible |
| Background Jobs | Laravel Queue (DB أو Redis) |
| Caching | Laravel Cache + (Redis اختياري) |
| Authentication | Laravel Sanctum (Token) |
| Payment | Tap / Paymob / HyperPay |
| SMS | Unifonic / Twilio / Hala.io |
| Email | SMTP (Mailtrap / SendGrid) |
| Admin Panel | Nova أو لوحة مخصصة |
| API Docs | Swagger (L5‑Swagger) |
| Deployment | Hostinger (Backend & MySQL) |

---

## 2) 🔐 Auth & Roles (المصادقة والصلاحيات)

- أدوار: `super_admin, merchant, model, influencer, customer`  
- Tokens عبر **Sanctum**.  
- استعادة كلمة المرور + تحقق البريد/الجوال.

---

## 3) 📂 Database Models (نماذج قاعدة البيانات)

```
users, roles, permissions, profiles,
stores, products, categories,
orders, order_items, invoices,
wallets, transactions,
collaborations, ads_campaigns,
dropship_products,
messages, notifications, reviews,
promotions, settings
```

---

## 4) 🧠 Core Modules (الوحدات الأساسية)

### 🛒 Store Management
- إنشاء/تعديل المتجر، المنتجات + المتغيّرات
- المخزون، مناطق وأسعار الشحن، العروض

### 🧱 Influencer Collaboration
- دعوات بين التاجرات والمؤثرات
- تتبع النقرات والمبيعات
- مشاركة الأرباح والدفع

### 🛆 Dropshipping Engine
- مخزون مشترك للدروبشوبنق
- ربط منتجات الموردين
- مزامنة السعر/المخزون
- عمولة لكل عملية

### 💬 Messaging
- مراسلة شبه فورية (Polling أو Echo)
- مرفقات (صور/صوت)، إشراف إداري

### 💼 Orders
- حالات الطلب: pending/confirmed/shipped/delivered/returned
- بوابات الدفع + المرتجعات + إشعارات SMS/Email

### 📊 Analytics
- مبيعات، أداء المؤثرات، التحويلات، ROI

---

## 5) 🧾 Admin Panel (لوحة التحكم)
- لوحة مؤشرات، إدارة المستخدمين، المنتجات والمتاجر
- تقارير عمولات وعوائد
- إدارة البانرات والعروض
- محرر الأدوار والصلاحيات
- CMS لصفحات النظام (شروط/عن…)

---

## 6) 📡 API Design
- REST JSON، أسماء: `/api/v1/...`
- استجابة قياسية:
```json
{
  "status": true,
  "message": "Success",
  "data": {}
}
```

**نماذج مسارات:**
```
POST   /api/v1/auth/login
GET    /api/v1/products
POST   /api/v1/orders
GET    /api/v1/users/{id}/wallet
```

---

## 7) ♻️ Queues & Jobs
- إرسال البريد/SMS، حساب أرباح المؤثرات
- استقبال Webhooks الشحن/الدفع
- تقارير أسبوعية

---

## 8) 📦 Suggested Structure
```
/app
  /Http/Controllers/Api/V1
  /Models
  /Services
  /Jobs
  /Events
/routes
  api.php
/config
  payment.php
  dropshipping.php
```

---

## 9) 🚀 Deployment (Hostinger)
- النشر على Hostinger + تفعيل **cron** للـ Scheduler
- ملف **.htaccess** لتوجيه الطلبات إلى `public/index.php` (مرفق)
- يمكن نشر الواجهة على Vercel أو أي خدمة مناسبة

---

## 10) ⏱️ Timeline (Sprints)
| Sprint | Duration | Deliverables |
|---|---|---|
| 1 | 1 week | Auth + Roles + Basic Models |
| 2 | 1 week | Product, Store, Order APIs |
| 3 | 1 week | Wallet, Transactions, Campaigns |
| 4 | 1 week | Dropshipping, CMS, Notifications |
| 5 | 1 week | Admin Panel, Tests, Swagger |

---

## ✅ Notes
- دعم RTL والعربية بالكامل
- بنية نظيفة قابلة للتوسع إلى SaaS
- استخدام الكاش والطوابير اختياري حسب الاستضافة