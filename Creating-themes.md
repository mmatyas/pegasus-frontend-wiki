Note: The following documentation is not yet complete!

---

In short, every theme needs a `theme.ini` metadata file and a `theme.qml`, the main QML file. These files should be under `~/.config/pegasus-frontend/themes/<theme name>/`.

The `theme.ini` is a list of `key = value` pairs, you'll need at least a `name` (other values aren't used at the moment). The format may also change in the future, eg. I'll likely start using `:` instead of `=`.

The `theme.qml` is the QML component that'll fill the screen, which at the moment must be a `FocusScope` with active focus:

```
import QtQuick 2.7

FocusScope {
    focus: true

    // your code here
}
```

Other than that, you're free to use whatever QML elements you want (EXCEPT the Qt Quick Controls 1/2 items, as they aren't really for this kind of application and are not available in the automatic builds).

To access the game data, you can use the similarly undocumented `pegasus` object:

- `pegasus.platforms` is a list (= you can use as a `model`) of platforms
- `pegasus.currentPlatform` is the currently selected platform
- `pegasus.currentPlatformIndex` is the index of the currently selected platform (most parts are read-only, but this is a field is writable)

Every `platform` has a `shortName` (eg. `nes`) and `longName` (which is currently empty as ES2 files only have one `<name>`) field, and `games`, `currentGame` and `currentGameIndex` fields, which work similarly as listed above.

Finally, every `game` has the following single-value fields: `boxFront`, `boxBack`, `boxSpine`, `boxFull`, `box` (same as `boxFull`), `cartridge`, `logo`, `marquee`, `bezel`, `gridicon`, `flyer`, `music`, and the following lists: `fanarts`, `screenshots`, `videos`.

Note that values may be empty (eg. no games for a platform, or no particular asset for a game). The field names may also change (we're still in alpha). Also in case you see `.qmlc` files, those are caches, no need eg. commit them to Git or such.
