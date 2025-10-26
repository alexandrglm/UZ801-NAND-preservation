# UZ801 v3.2 board STOCK sysdefault. 20251026 Backups
---

⚠️ **There are several versions of BOARDS, please make sure you use the correct board/rev.** ⚠️
I am not responsible for incorrect use. I assume you know what you are doing, and that you keep your backups to fix further issues.

---
## Files in Release
[Here](https://github.com/alexandrglm/UZ801-NAND-preservation/releases/tag/main)

---

## REquirements:

* [Bkerler's EDL tool](https://github.com/bkerler/edl)

* ADBCONTROL: [Original](https://marian.schedenig.name/2014/07/03/remote-control-your-android-phone-through-adb/), [FORK](https://github.com/Radon8472/adbcontrol)

* ADBCONTROL Usage:
1. Set `config.properties` as needed:
```
adbCommand = /usr/bin/adb       # Or...your PATH for adb (which adb)
screenshotDelay = 100
localImageFilePath = ~/UZ801/adbcontrol_screenshot.png
phoneImageFilePath = /mnt/sdcard/adbcontrol_screenshot.png
serial = 0123456789ABCDEF       # Or ... the device's serial (adb devices)
```

2. Start ADB:
```bash
java -jar ./adbcontrol.jar
```
3. If blank screen is shown:
```bash
adb shell settings put system screen_off_timeout 2147483647
adb shell input keyevent 26
```

---

## OS LANGUAGE

- Set to ENGLISH

---

## WIFI Tether

user: 4G-UFI-9F4
pass: 1234567890 (wpa2)

---

## Web App Login

- user: admin
- pass: admin

---

## BKERLER USAGE:
Assuming you got a fully working EDL environment:

---

## Backup Procedures

### Read a Single Partition

```bash
edl r <partitionname> <filename> [--memory=memtype] [--sectorsize==bytes] [--lun=lun] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Example:**

```bash
edl r modem modem.bin --memory=eMMC --serial
```

### Read All Partitions to a Directory

```bash
edl rl <directory> [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--skip=partnames] [--genxml] [--skipresponse] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Example:**

```bash
edl rl backup/ --memory=eMMC --serial --genxml
```

* This generates a backup of all partitions and optionally produces a rawprogram XML.

### Read the Entire Flash

```bash
edl rf <filename> [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Example:**

```bash
edl rf full_flash.bin --memory=eMMC --serial
```

### Read Specific Sectors

```bash
edl rs <start_sector> <sectors> <filename> [--lun=lun] [--sectorsize==bytes] [--memory=memtype] [--loader=filename] [--debugmode] [--skipresponse] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

---

## Restore / Write Procedures

### Write a Single Partition

```bash
edl w <partitionname> <filename> [--partitionfilename=filename] [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--skipwrite] [--skipresponse] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Example:**

```bash
edl w modem modem.bin --memory=eMMC --serial
```

### Write All Partitions from a Directory

```bash
edl wl <directory> [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--skip=partnames] [--skipresponse] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Example:**

```bash
edl wl backup/ --memory=eMMC --serial
```

### Write Entire Flash from File

```bash
edl wf <filename> [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--loader=filename] [--skipresponse] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

### Write Specific Sectors

```bash
edl ws <start_sector> <filename> [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--skipwrite] [--skipresponse] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

### Using Rawprogram XML for Restore

```bash
edl qfil <rawprogram.xml> <patch.xml> <imagedir> [--memory=memtype] [--loader=filename] [--debugmode] [--skipresponse] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **rawprogram.xml**: Configuration file describing partitions.
* **patch.xml**: Optional patch file.
* **imagedir**: Directory containing partition images.

---

## Additional Commands

* **Reset device:**

```bash
edl reset [--resetmode=mode] [--loader=filename] [--debugmode] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

* **Print GPT table:**

```bash
edl printgpt [--memory=memtype] [--lun=lun] [--sectorsize==bytes] [--loader=filename] [--debugmode] [--skipresponse] [--vid=vid] [--pid=pid] [--portname=portname] [--serial]
```

---

