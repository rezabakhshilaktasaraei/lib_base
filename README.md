# lib_base — Accessibility Tracker

This repository is a fork of [desktop-app/lib_base](https://github.com/desktop-app/lib_base) that tracks **accessibility improvements** to Telegram Desktop's base library. All changes listed here are merged into the official upstream repository.

> This is part of the broader [Telegram Desktop Accessibility](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) effort.

## Merged Pull Requests

| PR | Title | Author | First Telegram Desktop Release |
|---|---|---|---|
| [#273](https://github.com/desktop-app/lib_base/pull/273) | Add screen reader detection via QAccessible::ActivationObserver | [@rezabakhshilaktasaraei](https://github.com/rezabakhshilaktasaraei) | [v6.2.5](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible/releases/tag/v6.2.5) |

## What Was Added

- **Screen reader detection** — A `ScreenReaderState` singleton that tracks whether a screen reader is active using Qt's `QAccessible::ActivationObserver`. UI components can subscribe to state changes and adapt their behavior (e.g., enabling keyboard focus policies when a screen reader is detected).

```cpp
base::ScreenReaderState::Instance()->activeValue(
) | rpl::start_with_next([=](bool active) {
    widget->setFocusPolicy(active ? Qt::StrongFocus : Qt::NoFocus);
}, widget->lifetime());
```

## Related Repositories

- [tdesktop-accessible](https://github.com/rezabakhshilaktasaraei/tdesktop-accessible) — Main tracker with releases
- [lib_ui](https://github.com/rezabakhshilaktasaraei/lib_ui) — UI widget accessibility

## License

GNU General Public License v3.0 with OpenSSL exception, same as the official [lib_base](https://github.com/desktop-app/lib_base).
