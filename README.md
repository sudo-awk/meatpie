# meatpie

Bash helper to bring up a **MeatPi Dual CAN** adapter (`16d0:1261`) as SocketCAN interfaces on Linux.

## What it does

- Detects the MeatPi USB device and its `ttyACM` ports
- Configures each port (raw, 115200 baud) and starts `slcand`
- Brings up `canN` interfaces without overwriting existing ones
- Clean teardown of interfaces and `slcand` processes

## Requirements

- Linux with SocketCAN
- `can-utils` (`sudo apt install can-utils`)
- `slcand` available on `PATH`

## Install

```bash
git clone https://github.com/sudo-awk/meatpie.git
cd meatpie
chmod +x meatpie
sudo cp meatpie /usr/local/bin/
```

## Usage

```bash
meatpie up       # detect ports, configure ACM, bring up canN
meatpie down     # tear down interfaces and stop slcand
meatpie status   # show interface, slcand, and USB state
```

## Config

Edit the top of the script:

| Variable            | Default  | Notes                          |
|---------------------|----------|--------------------------------|
| `BAUD_RATE`         | `115200` | Serial baud to the adapter     |
| `SLCAND_SPEED_FLAG` | `s6`     | `s5`=250k, `s6`=500k, `s8`=1000k |
| `CAN_BITRATE`       | `500000` | Displayed CAN bitrate          |

## Notes

CAN index starts after any existing `can*` interfaces, so other devices (`can0`, `can1`, ...) are never overwritten.

---

If this saved you time, buy me a coffee: https://buymeacoffee.com/

