# Quantum Mechanical Keyboard Firmware

[![Current Version](https://img.shields.io/github/tag/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/tags)
[![Discord](https://img.shields.io/discord/440868230475677696.svg)](https://discord.gg/Uq7gcHh)
[![Docs Status](https://img.shields.io/badge/docs-ready-orange.svg)](https://docs.qmk.fm)
[![GitHub contributors](https://img.shields.io/github/contributors/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/pulse/monthly)
[![GitHub forks](https://img.shields.io/github/forks/qmk/qmk_firmware.svg?style=social&label=Fork)](https://github.com/qmk/qmk_firmware/)

This is a keyboard firmware based on the [tmk\_keyboard firmware](https://github.com/tmk/tmk_keyboard) with some useful features for Atmel AVR and ARM controllers, and more specifically, the [OLKB product line](https://olkb.com), the [ErgoDox EZ](https://ergodox-ez.com) keyboard, and the Clueboard product line.

## Documentation

* [See the official documentation on docs.qmk.fm](https://docs.qmk.fm)

Setup required for this to work:
Dont know, check the official QMK page.


## Flash firmware onto device:
Flash onto device via: 

```
qmk flash -kb sofle -km via -e CONVERT_TO=helios 
```

- This flashes the "via" keymap. The exact layout can then later be chanbed.
- Note the `helios`. This is the specific rp2040 board used. 

Then. go to via in browser. 

You might need to change some settings to get the USB port to work. Check the chrome log with `chrome://device-log` and see if there are any access denied prompts. To fix this, you need to set the permission for the USB device via a udef rule. Like this: 

```
vim /etc/udev/rules.d/99-via.rules 
```

And add:

```
KERNEL=="hidraw*", SUBSYSTEM=="hidraw", MODE="0666", TAG+="uaccess", TAG+="udev-acl"
```

Note: To reload your udef rule without needing to re-logg, execute the following:

```
sudo udevadm control --reload-rules && sudo udevadm trigger
```

# Layout setup:
Since via is a pain to use with different languages other than english (ANSI), we simply join them by setting the layout to english....
But now, how do you type characters like `ö` `ë` `ä`? By using macros in via. Example:

To type a `ö`, use: 

```
{KC_RALT,KC_RSFT,KC_QUOT}o
```

It types a `"` followed by a `o`, which then gets converted. Note: You need to setup the `compose key`, which is also kinda quirky... Read through [here](https://askubuntu.com/questions/70784/how-can-i-enable-compose-key), especially the "In Ubuntu 22.04 and later" section.

