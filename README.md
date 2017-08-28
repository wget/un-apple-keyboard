# un-apple-keyboard

Make Apple keyboards like all your other keyboards


This solutions combines custom udevs rules, changes to parameters of the apple_hid linux kernel driver, and keyfuzz, a tool written by Lennart Poettering, manipulating scancode/keycode translation tables of keyboard drivers supporting the Linux input layer API.

From the [keyfuzz help page](http://0pointer.de/lennart/projects/keyfuzz/):

> keyfuzz is not a daemon like Gnome acme which reacts on special hotkeys but a tool to make non-standard keyboards compatible with such daemons. keyfuzz should be run once at boot time, the modifications it makes stay active after the tool quits until reboot. keyfuzz does not interact directly with XFree86. However, newer releases of the latter (4.1 and above) rely on the Linux input API, so they take advantage of the fixed translation tables.

## Features

* The keyboard is considered as an ISO keyboard (e.g. `<` and `>` located at the right of the `Left Shift` key are working like expected).
* The function keys are disabled by default. You need to press the `Fn` key in combination to trigger them. The default behavior is keys from `F1` to `F12`.
* The `Alt` and `Cmd` keys are swapped.
* `F13` is mapped to `SYSRQ`, `F14` to `Scroll Lock` and `F15` to `Pause`.

The first 3 aforementioned features are brought to you using the default linux kernel module `apple_hid`.

The last one is provided by providing a mapping to  ̀keyfuzz`.

## Known bugs / to be developped

* Enable numkey automatically
* KDE can recognize F16 to F18, but for some reason F19 is not catched by Kwin. showkey is recognizing it though.
* The keyfuzz rules are generated like this

```
# map F13 to SYSRQ
458856 99

where 458856 = 0x00070068 in Hex format and 68 represents the USB HID usage ID for F13 in Hex
where 99 represents the SYSRQ key as listed in /usr/include/linux/input.h
```
[src.](https://arstechnica.com/civis/viewtopic.php?p=21847635&sid=bd7e02f609a79d05414d95105c34e6e8#p21847635)

* When using KDE, the features 1, 2, 3 can be simuled using keyboard options. However, these will only be applied in the GUI, TTY is not concerned. See [here](http://fsymbols.com/keyboard/linux/choosers/) to define key chooser using KDE (`Compose` key and explanatin with key levels).

## Name

[The `un-` prefix is used in English to express the contrary, the opposite, the sense "not"](https://en.wiktionary.org/wiki/un-#English). This is what this package does: with it, your keyboard is not an Apple keyboard anymore.

## License

This solution was initially written by [Tavian Barnes](https://github.com/tavianator), but I took maintainership of his [AUR package](https://aur.archlinux.org/packages/un-apple-keyboard/) as he is not using an Apple keyboard anymore. This project has been initially discussed on [a thread on the Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=136439).

[DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE](LICENSE)

