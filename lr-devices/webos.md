## LG WebOS

### Soft reset

Settings > General > About This TV > User Agreements > Untick everything > Reload

### Prerequisites

1. Install WebOS CLI

```bash
npm install -g @webos-tools/cli
```

### Debugger

1. LG Content Store > Search > Developer Mode > Install > Open

2. Create LG developer account (TBC) > Plug in wired keyboard > Sign in

3. Dev Mode Status On > Reload the app > Open Developer Mode > Key Server On

4. Add device on your laptop:

```bash
ares-setup-device

Select add
Enter Device Name: webos372
Enter Device IP address: 192.168.1.109  # WebOS IP address
Enter Device Port: 9922                 # Device port by default
Enter ssh user: prisoner                # Default ssh user
Enter description: WebOS 3.7.2
Set default ? No
Save ? Yes

name                deviceinfo                   connection  profile
------------------  ---------------------------  ----------  -------
webos372            prisoner@192.168.1.109:9922  ssh         tv
emulator (default)  developer@127.0.0.1:6622     ssh         tv
```

5. Get the key from the device

```bash
ares-novacom --device webos372 --getkey

SSH Private Key: /Users/beraliv/.ssh/webos372_webos
input passphrase: # Enter passphrase from Developer Mode app
```

> [!WARNING]  
> Make sure you turn of proxies when requesting keys from the devices.
> Otherwise, you will get "_Failed to get ssh private key_"

6. Build your application in `*.ipk` file, e.g. `~/Downloads/app.ipk`

7. Install application on your device

```bash
ares-install ~/Downloads/app.ipk -d webos372

[Info] Set target device : webos372
Installing package /Users/alexey.berezin/Downloads/app.ipk
Success
```

8. Inspect your application

```bash
ares-inspect APP_ID -d webos372

[Info] Set target device : webos372
Application Debugging - http://localhost:50693/devtools/devtools.html?experiments=true&ws=localhost:50693/devtools/page/F5619BBB-FC20-9EA0-D6A6-CC2EE5D4D083
```

> [!NOTE]  
> `APP_ID` is supplied in your `*-appinfo.json` under `id`

9. Open Application Debugging ✅
