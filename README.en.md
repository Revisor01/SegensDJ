<h1 align="center">SegensDJ</h1>

<p align="center">
  Mixing words of blessing like a DJ —<br>
  a Raspberry Pi with a DJ controller for the exhibition "Interreligiöse Segensräume" (interreligious spaces of blessing).
</p>

<p align="center">
  <a href="README.md">Deutsch</a> · <b>English</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Raspberry%20Pi%204-red" alt="Platform">
  <img src="https://img.shields.io/github/license/Revisor01/SegensDJ" alt="License">
</p>

## What it is about

In many religions a blessing is a word spoken to someone. SegensDJ lets
visitors of an exhibition play with it: a DJ controller holds spoken words of
blessing, sounds and noises from different traditions, which can be layered,
faded out and mixed anew.

The repository contains a ready-made image for the Raspberry Pi running the DJ
software Mixxx, set up for the controller, plus the sound files. The spoken
blessings are mostly in German.

## Features

- **Ready-made image** — write it to the SD card, boot, start mixing
- **36 sound files** — words of blessing, tones and noises in `Samples/`
- **Controller prepared** — Mixxx 2.3.3 with a mapping for the
  Pioneer DDJ-SB3
- **Remote access** — SSH, VNC and file sharing (SMB) for maintenance

## Installation

**Hardware.**
- Raspberry Pi 4 with 8 GB RAM
- Pioneer DDJ-SB3
- Speakers or an amplifier, via the 3.5 mm jack on the Pi or via the
  controller's sound card

<p float="left">
<img src="docs/pi4.png" width="32%" height="32%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="docs/sb3.svg" width="40%" height="40%">
</p>

**Write the image.** If you know how to flash SD cards, use your usual way.
Otherwise:

1. Install [balenaEtcher](https://etcher.balena.io).
2. Download [`SegensDJ-Pi.zip`](SegensDJ-Pi.zip) (stored in Git LFS).
3. Connect the SD card, open Etcher, choose "Flash from file" and select the
   file.
4. Select the SD card, confirm that nothing important is on it, and click
   "Flash".

**Set up Wi-Fi.** After writing, the partition `boot` appears (otherwise
remove and reinsert the card once). Create the file `wpa_supplicant.conf`
there:

```
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
       ssid="YOUR WIFI SSID"
       psk="YOUR PASSWORD"
       key_mgmt=WPA-PSK
}
```

Then put the card into the Pi and boot it; it connects to the Wi-Fi.

**Access.** Both ways need the IP address of the Pi.

- **SSH:** `ssh pi@<IP>`, user `pi`, password `mixxx`.
- **VNC:** if needed, start it via SSH with
  `sudo systemctl start vncserver@1.service`, then connect your VNC client to
  `<IP>:5901` with the password `mixxxpi`. Suitable clients include
  [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/),
  [TightVNC](https://www.tightvnc.com/download.php) or
  [UltraVNC](https://uvnc.com/).

**Please change both passwords after setup** (`passwd` and `vncpasswd`). They
are the image defaults and therefore public.

## Known quirks

- In `/home/pi/.mixxx/controllers/Pioneer-DDJ-SB3-scripts.js`, line 981 is
  commented out because Mixxx otherwise reports an error at startup. If the
  deck does not work properly, that is the first place to look.
- If the VNC server starts automatically, Mixxx does not detect the deck.
  That is why it is only started by hand when needed.

## Versions

The image is tagged as [release 0.1.0-beta](https://github.com/Revisor01/SegensDJ/releases).
Compared with the base image it contains the system updates of 8 November
2022, Mixxx 2.3.3 (because of the controller), a VNC server, an SMB share and a
time server.

## Structure

```
SegensDJ
├── SegensDJ-Pi.zip   — ready-made image for the SD card (Git LFS)
├── Samples/          — sound files (WAV)
└── docs/             — images for this page
```

## Contributing

Bug reports and suggestions are welcome as an
[issue](https://github.com/Revisor01/SegensDJ/issues). Please report security
issues privately as described in [SECURITY.md](SECURITY.md); see
[CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). The image is based on
[fayaaz/mixxx-pi-gen](https://github.com/fayaaz/mixxx-pi-gen).

## Contact

Pastor Simon Luthe · [mail@simonluthe.de](mailto:mail@simonluthe.de) ·
[simonluthe.de](https://simonluthe.de)
