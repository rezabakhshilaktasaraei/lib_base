<div align="center">

**[English](README.md)** | **فارسی**

</div>

<div dir="rtl" align="right">

# lib_base — دسترس‌پذیری

تشخیص صفحه‌خوان برای تلگرام دسکتاپ

> فورک از [desktop-app/lib_base](https://github.com/desktop-app/lib_base)

## درباره پروژه

این فورک شامل پایه تشخیص صفحه‌خوان برای سیستم دسترس‌پذیری تلگرام دسکتاپ است. کلاس ScreenReaderState را اضافه می‌کند — یک سینگلتون که فعال بودن صفحه‌خوان را ردیابی می‌کند و به بقیه رابط کاربری اجازه می‌دهد خود را تطبیق دهد (مثلاً تنظیم سیاست فوکوس، فعال‌سازی پیمایش کیبورد).

## تغییرات ادغام‌شده در مخازن رسمی — ۱ پول‌ریکوئست

</div>

| PR | توضیحات | تاریخ |
|----|---------|-------|
| [#273](https://github.com/desktop-app/lib_base/pull/273) | **تشخیص صفحه‌خوان** — سینگلتون `ScreenReaderState` با استفاده از `QAccessible::ActivationObserver`، تولیدکننده واکنشی `activeValue()` برای تطبیق اجزای رابط کاربری | اکتبر ۲۰۲۵ |

<div dir="rtl" align="right">

## نحوه عملکرد

اجزای رابط کاربری به وضعیت صفحه‌خوان مشترک می‌شوند و هنگام فعال شدن صفحه‌خوان رفتار خود را تطبیق می‌دهند:

</div>

```cpp
base::ScreenReaderState::Instance()->activeValue(
) | rpl::start_with_next([=](bool active) {
    widget->setFocusPolicy(active ? Qt::StrongFocus : Qt::NoFocus);
}, widget->lifetime());
```

<div dir="rtl" align="right">

هنگامی که صفحه‌خوان شروع به کار می‌کند، `activeValue()` مقدار `true` را ارسال می‌کند و ویجت‌ها می‌توانند فوکوس قوی را فعال کنند، مدیریت‌کننده‌های کیبورد اضافه کنند، یا اطلاعات دسترس‌پذیری بیشتری را نمایان سازند. هنگامی که صفحه‌خوان متوقف می‌شود، رابط کاربری به رفتار پیش‌فرض خود باز می‌گردد.

## فایل کلیدی

</div>

| فایل | کاربرد |
|------|--------|
| `base/platform/win/base_screen_reader_win.h/cpp` | سینگلتون `ScreenReaderState`، یکپارچه‌سازی با `QAccessible::ActivationObserver`، تولیدکننده واکنشی `activeValue()` |

<div dir="rtl" align="right">

## مخازن مرتبط

- [تغییرات دسترس‌پذیری lib_ui](https://github.com/rezabakhshilaktasaraei/lib_ui) — دسترس‌پذیری ویجت‌های رابط کاربری بر پایه این تشخیص
- [تغییرات دسترس‌پذیری tdesktop](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) — دسترس‌پذیری سطح برنامه با استفاده از هر دو کتابخانه

## مجوز

این پروژه تحت مجوز [GNU General Public License v3.0](LICENSE) با استثنای OpenSSL منتشر شده است.

</div>
