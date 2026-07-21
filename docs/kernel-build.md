# Custom Kernel and WSL2 Integration

## Kernel Version

The Catapult environment uses a custom WSL2 Linux kernel:

```text
Linux 6.18.35.2-silentium-usb3+
```

## Why a Custom Kernel Was Needed

The stock environment did not expose all of the USB, wireless, Bluetooth, and networking capabilities required for the project.

The custom kernel work focused on supporting:

- WSL2 USB passthrough
- USB/IP
- Marvell wireless hardware
- Wi-Fi access-point operation
- Bluetooth HCI
- Linux routing
- Firewall and NAT functionality
- systemd-managed services

## USB Attachment Flow

```text
Marvell USB module
        ↓
Windows USB stack
        ↓
usbipd-win
        ↓
WSL2 virtual machine
        ↓
Custom Linux kernel
        ↓
Marvell Wi-Fi and Bluetooth interfaces
```

## Typical Recovery Flow

After a Windows restart, WSL shutdown, or USB reset:

1. Start the Kali WSL2 distribution.
2. Open an Administrator PowerShell.
3. Confirm the Marvell device with `usbipd list`.
4. Attach the device to WSL.
5. Confirm the USB device inside Kali.
6. Confirm that `mlan0` and the Bluetooth controller are present.
7. Restart the Catapult services.

Example Windows command:

```powershell
usbipd attach --wsl --busid 2-1 --auto-attach
```

The BUSID can change and should always be confirmed with:

```powershell
usbipd list
```

Example Linux checks:

```bash
lsusb
ip -br link
bluetoothctl list
```

## Operational Lesson

The dashboard service intentionally checks for the Marvell interface before starting.

If `mlan0` is missing, the service remains inactive instead of starting with incomplete hardware support.

This makes USB attachment and interface recovery a required first step after some system restarts.
