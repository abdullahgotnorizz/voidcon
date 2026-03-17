# Void40 ZMK Firmware — Pi Pico (RP2040)

## What's in this folder

```
void40-zmk/
├── build.yaml                        ← Tells ZMK what board/shield to build
├── .github/workflows/build.yml       ← GitHub Actions auto-builder
├── config/
│   ├── west.yml                      ← ZMK dependency manifest
│   ├── void40.keymap                 ← Your key layout (4 layers)
│   └── void40.conf                   ← Keyboard settings
└── README.md                         ← This file
```

---

## Layer Map

| Layer | Activate by | What it does |
|-------|-------------|--------------|
| 0 Base | Default | Normal QWERTY |
| 1 Lower | Hold key left of spacebar | Numbers, F-keys, symbols |
| 2 Raise | Hold key right of spacebar | Shifted symbols, media keys |
| 3 Adjust | Hold both FN keys | Bluetooth slots, mute, reset |

---

## How to build & flash (easiest way — GitHub Actions)

This is the recommended method. No toolchain needed on your machine.

### 1. Create a GitHub account (if you don't have one)
Go to https://github.com and sign up.

### 2. Create a new repository
- Go to https://github.com/new
- Name it `void40-zmk-config`
- Set it to **Public**
- Click **Create repository**

### 3. Upload these files
Upload the entire contents of this zip to your new repo. You can drag and drop files on the GitHub website.

Make sure the structure looks like:
```
your-repo/
├── build.yaml
├── .github/workflows/build.yml
└── config/
    ├── west.yml
    ├── void40.keymap
    └── void40.conf
```

### 4. Wait for the build
- Click the **Actions** tab in your repo
- You'll see a build running — wait ~5 minutes
- When it's green ✅, click it → scroll down to **Artifacts**
- Download `firmware.zip` → inside is `rpi_pico-void40.uf2`

### 5. Flash to your Pi Pico
1. Hold the **BOOTSEL** button on the Pi Pico
2. While holding, plug it into your PC via USB
3. It mounts as a USB drive called `RPI-RP2`
4. Drag and drop `rpi_pico-void40.uf2` onto that drive
5. It will automatically reboot as your keyboard ✅

---

## How to remap keys

Edit `config/void40.keymap` — change any `&kp KEYNAME` to a different key.

Common keys:
- `&kp TAB`, `&kp ESC`, `&kp BSPC`, `&kp RET`
- `&kp LCTRL`, `&kp LSHFT`, `&kp LALT`, `&kp LGUI`
- `&kp A` through `&kp Z`, `&kp N0` through `&kp N9`
- `&trans` = transparent (passes through to layer below)
- `&bootloader` = puts Pi Pico into flash mode

Full ZMK key list: https://zmk.dev/docs/codes

After editing, push to GitHub and a new firmware will build automatically.

---

## Wiring the Void40 to Pi Pico

The Void40 PCB expects a Pro Micro pinout. Use this mapping:

| Pro Micro Pin | Pi Pico GPIO |
|---------------|-------------|
| D1 (row 0)    | GP1         |
| D0 (row 1)    | GP0         |
| D4 (row 2)    | GP4         |
| D5 (row 3)    | GP5         |
| F4 (col 0)    | GP6         |
| F5 (col 1)    | GP7         |
| F6 (col 2)    | GP8         |
| F7 (col 3)    | GP9         |
| B1 (col 4)    | GP10        |
| B3 (col 5)    | GP11        |
| B2 (col 6)    | GP12        |
| B6 (col 7)    | GP13        |
| B5 (col 8)    | GP14        |
| B4 (col 9)    | GP15        |
| D7 (col 10)   | GP16        |
| C6 (col 11)   | GP17        |

> **Note:** If you're using a Pro Micro to Pi Pico adapter board, check if it maps pins directly — you may not need to rewire anything.
