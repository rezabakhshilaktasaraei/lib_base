<div align="center">

**[فارسی](README.fa.md)** | **English**

</div>

# lib_base — Accessibility

Screen reader detection for Telegram Desktop

> Fork of [desktop-app/lib_base](https://github.com/desktop-app/lib_base)

## About

This fork adds the screen reader detection foundation for Telegram Desktop's accessibility system. It introduces the `ScreenReaderState` class — a singleton that tracks whether a screen reader is active and allows the rest of the UI to adapt accordingly (e.g., setting focus policies, enabling keyboard navigation).

## Contribution Merged Upstream — 1 PR

| PR | Description | Date |
|----|-------------|------|
| [#273](https://github.com/desktop-app/lib_base/pull/273) | **Screen reader detection** — `ScreenReaderState` singleton using `QAccessible::ActivationObserver`, reactive `activeValue()` producer for UI components to adapt when a screen reader is active | Oct 2025 |

## How It Works

Components subscribe to the screen reader state and adapt their behavior when a screen reader becomes active:

```cpp
base::ScreenReaderState::Instance()->activeValue(
) | rpl::start_with_next([=](bool active) {
    widget->setFocusPolicy(active ? Qt::StrongFocus : Qt::NoFocus);
}, widget->lifetime());
```

When a screen reader starts, `activeValue()` emits `true`, and widgets can enable strong focus, add keyboard handlers, or expose additional accessibility information. When the screen reader stops, the UI reverts to its default behavior.

## Key File

| File | Purpose |
|------|---------|
| `base/platform/win/base_screen_reader_win.h/cpp` | `ScreenReaderState` singleton, `QAccessible::ActivationObserver` integration, reactive `activeValue()` producer |

## Related Repositories

- [lib_ui accessibility changes](https://github.com/rezabakhshilaktasaraei/lib_ui) — Widget-level accessibility built on top of this detection
- [tdesktop accessibility changes](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) — Application-level accessibility using both libraries

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE), with an OpenSSL exception.
