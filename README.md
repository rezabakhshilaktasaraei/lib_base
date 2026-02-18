<div align="center">

# lib_base — Accessibility

<p>Screen reader detection for Telegram Desktop</p>

<p>
  <a href="#english"><strong>English</strong></a> |
  <a href="#فارسی"><strong>فارسی</strong></a>
</p>

<p>
  <em>Fork of <a href="https://github.com/desktop-app/lib_base">desktop-app/lib_base</a></em>
</p>

</div>

---

<details open>
<summary id="english"><h2>English</h2></summary>

### About

This fork contains the screen reader detection foundation for Telegram Desktop's accessibility system. It adds `ScreenReaderState`, a singleton that tracks whether a screen reader is active, enabling the rest of the UI to adapt (e.g. setting focus policies, enabling keyboard navigation).

### Contribution Merged Upstream — 1 PR

| PR | Description | Merged |
|----|-------------|--------|
| [#273](https://github.com/desktop-app/lib_base/pull/273) | **Screen reader detection** — `ScreenReaderState` singleton implementing `QAccessible::ActivationObserver` to receive `accessibilityActiveChanged(bool)` callbacks from Qt. Initializes with `QAccessible::isActive()` and exposes `activeValue()` returning `rpl::producer<bool>` for reactive UI adaptation. Thread-safe via `Instance()` | Oct 2025 |

### How It Works

`ScreenReaderState` registers itself as a `QAccessible::ActivationObserver` when the application starts. Qt calls `accessibilityActiveChanged(bool)` whenever a screen reader connects or disconnects. The state is exposed as a reactive stream:

```cpp
base::ScreenReaderState::Instance()->activeValue(
) | rpl::start_with_next([=](bool active) {
    widget->setFocusPolicy(active ? Qt::StrongFocus : Qt::NoFocus);
}, widget->lifetime());
```

This is used by [lib_ui](https://github.com/desktop-app/lib_ui) to automatically set `StrongFocus` on buttons, checkboxes, radio buttons, and sliders when a screen reader is active, so they become keyboard-navigable without affecting normal mouse-only usage.

### Key File

| File | Purpose |
|------|---------|
| `base/screen_reader_state.h/cpp` | `ScreenReaderState` — screen reader activation tracking |

### Related Repositories

- [lib_ui accessibility changes](https://github.com/rezabakhshilaktasaraei/lib_ui) — UI widget accessibility built on top of this detection
- [tdesktop accessibility changes](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) — Application-level accessibility using both libraries

</details>

---

<details>
<summary id="فارسی"><h2>فارسی</h2></summary>

<div dir="rtl" align="right">

### درباره پروژه

این فورک شامل پایه تشخیص صفحه‌خوان برای سیستم دسترس‌پذیری تلگرام دسکتاپ است. کلاس `ScreenReaderState` را اضافه می‌کند — یک سینگلتون که فعال بودن صفحه‌خوان را ردیابی می‌کند و به بقیه رابط کاربری اجازه می‌دهد خود را تطبیق دهد (مثلاً تنظیم سیاست فوکوس، فعال‌سازی پیمایش کیبورد).

### تغییر ادغام‌شده در مخزن رسمی — ۱ PR

</div>

| PR | توضیحات | تاریخ |
|----|---------|-------|
| [#273](https://github.com/desktop-app/lib_base/pull/273) | <div dir="rtl"><strong>تشخیص صفحه‌خوان</strong> — سینگلتون <code>ScreenReaderState</code> با پیاده‌سازی <code>QAccessible::ActivationObserver</code> برای دریافت callback از Qt. مقداردهی اولیه با <code>QAccessible::isActive()</code> و ارائه <code>activeValue()</code> به صورت <code>rpl::producer&lt;bool&gt;</code> برای تطبیق واکنشی رابط کاربری. ایمن از نظر نخ از طریق <code>Instance()</code></div> | اکتبر ۲۰۲۵ |

<div dir="rtl" align="right">

### نحوه عملکرد

`ScreenReaderState` خود را هنگام شروع برنامه به عنوان `QAccessible::ActivationObserver` ثبت می‌کند. Qt هر زمان که صفحه‌خوانی متصل یا قطع شود، `accessibilityActiveChanged(bool)` را فراخوانی می‌کند. وضعیت به صورت جریان واکنشی ارائه می‌شود:

</div>

```cpp
base::ScreenReaderState::Instance()->activeValue(
) | rpl::start_with_next([=](bool active) {
    widget->setFocusPolicy(active ? Qt::StrongFocus : Qt::NoFocus);
}, widget->lifetime());
```

<div dir="rtl" align="right">

این توسط [lib_ui](https://github.com/desktop-app/lib_ui) استفاده می‌شود تا هنگام فعال بودن صفحه‌خوان، به طور خودکار `StrongFocus` را روی دکمه‌ها، چک‌باکس‌ها، رادیوباتن‌ها و اسلایدرها تنظیم کند تا بدون تأثیر بر استفاده عادی با ماوس، با کیبورد قابل پیمایش شوند.

### فایل کلیدی

</div>

| فایل | کاربرد |
|------|--------|
| `base/screen_reader_state.h/cpp` | <div dir="rtl"><code>ScreenReaderState</code> — ردیابی فعال‌سازی صفحه‌خوان</div> |

<div dir="rtl" align="right">

### مخازن مرتبط

- [تغییرات دسترس‌پذیری lib_ui](https://github.com/rezabakhshilaktasaraei/lib_ui) — دسترس‌پذیری ویجت‌های رابط کاربری بر پایه این تشخیص
- [تغییرات دسترس‌پذیری tdesktop](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) — دسترس‌پذیری سطح برنامه با استفاده از هر دو کتابخانه

</div>

</details>
