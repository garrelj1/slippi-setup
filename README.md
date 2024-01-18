# DISCLAIMER
The kernel module is not really my code. I've just adapted it slightly. [See here](https://github.com/hannesmann/gcadapter-oc-kmod) for the original repo

# Usage
`slippi-up` downloads the latest slippi launcher `.AppImage` 

`slippi` runs the launcher

# Controller Adapter Info/Setup
I use an adapter with the label **GC Controller Adapter For PC USB**

`lsusb` gives: `1a34:f705 ACRUX USB GamePad`

The kernel module in this repo has the correct updated VID and PID to patch the bInterval (polling rate)

> I only ever saw an average of ~300hz using this kernel module and detecting the rate with `evhz`. [See here](https://git.sr.ht/~iank/evhz) for the `evhz` command

## Dolphin config
Drop the controller setup file `ctl-default.ini` in: `~/.config/SlippiOnline/Config/Profiles/GCPad`

---

# README adapted from gcadapter-oc-kmod repo
> [link to original repo here](https://github.com/hannesmann/gcadapter-oc-kmod)

> The text below is taken from the README of the same repo that the kernel module code was taken from

The default overclock is from 125 Hz to 1000 Hz. Official adapters should be able to handle this but if you experience stutter or dropped inputs you can try lowering the rate to 500 Hz.

## Building
Use `make` to build gcadapter_oc.ko and `sudo insmod gcadapter_oc.ko` to load the module into the running kernel.

If you get an error saying "building multiple external modules is not supported" it's because you have a space somewhere in the path to the gcadapter-oc-kmod directory.

GNU Make can't handle spaces in filenames so move the directory to a path without spaces (example: `/home/falco/My Games/gcadapter-oc-kmod` -> `/home/falco/gcadapter-oc-kmod`).

## Changing the polling rate

Polling rate is set according to the `bInterval` value in the USB endpoint descriptor. The value sets the polling rate in milliseconds, for example: an interval value of 4 equals 250 Hz.

You can change the rate by using the kernel parameter `gcadapter_oc.rate=n` (if installed), passing the rate to `insmod gcadapter_oc.ko rate=n` or going into `/sys/module/gcadapter_oc/parameters` and using `echo n > rate` to change the value ([video](https://asciinema.org/a/455373)).

## Other helpful links
- [UnclePunch mod pack](https://github.com/UnclePunch/Training-Mode/tree/master) for training tech
- [20XX Hack Pack](https://github.com/DRGN-DRC/20XX-HACK-PACK)
