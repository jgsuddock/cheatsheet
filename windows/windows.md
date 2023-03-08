# Windows

## Keyboard Shortcuts

| Description | Keyboard Shortcut |
| --- | --- |
| Bluetooth Connect Panel | `Win + K` |
| Lock Screen | `Win + L` |
| Clipboard History | `Win + V` |
| Admin Quick Action Panel | `Win + X` |

## Cleanup

Run these commands in administrator mode:

```powershell
sfc /scannow

DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth
```
