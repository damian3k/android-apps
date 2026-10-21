<p align="center"><img src="icon256.png" width="128" height="128" alt="Android Apps icon"></p>

# Android Apps 0.1

**[English](#english) · [Polski](#polski)**

**Download / Pobierz:** [Releases](https://github.com/damian3k/android-apps/releases/latest)

| Platform | File | Guide / Instrukcja |
|---|---|---|
| Windows 10/11 x64 | `AndroidApps_0.1-windows-x64.zip` (adb included / adb w zestawie) | this file / ten plik |
| macOS 12+ Apple Silicon | `AndroidApps-0.1-macos-arm64.zip` | [README-multiplatform.md](README-multiplatform.md) |
| macOS 12+ Intel | `AndroidApps-0.1-macos-x64.zip` | [README-multiplatform.md](README-multiplatform.md) |
| Linux x64 | `AndroidApps-0.1-linux-x64.tar.gz` | [README-multiplatform.md](README-multiplatform.md) |
| Linux ARM64 | `AndroidApps-0.1-linux-arm64.tar.gz` | [README-multiplatform.md](README-multiplatform.md) |

Each package includes its own guide. / Każda paczka zawiera własną instrukcję.

**Early test release / Wczesna wersja testowa:** 0.1 has been tested on a Samsung Galaxy S20 FE 5G and a Meta Quest 3. / Wersja 0.1 była testowana na Samsungu Galaxy S20 FE 5G i Meta Quest 3.

Based on / Na bazie: [Quest Apps](https://github.com/damian3k/quest-apps).

**Build from source / Budowanie ze źródeł:** .NET 9 SDK, then `dotnet run -c Release`. Packages for all platforms: `python tools/build-release.py`. The repository does not include adb; on Windows put Google's Platform-Tools files into `adb\` first, see [NOTICE.md](NOTICE.md). / Repozytorium nie zawiera adb; na Windows najpierw skopiuj pliki Platform-Tools od Google do `adb\`, patrz [NOTICE.md](NOTICE.md).

License / Licencja: [MIT](LICENSE). Not affiliated with Google, Samsung or Meta. / Projekt niezależny, niezwiązany z firmami Google, Samsung ani Meta.

---

<a id="english"></a>
## English

Android Apps is a Windows tool for Android devices: phones, tablets, Android TV and Meta Quest headsets. It talks to the device over ADB (by USB cable or Wi-Fi) and lets you:

- see every installed app with its size, version and icon, and how full the storage is,
- uninstall apps and delete large leftover files,
- install APKs (with OBB game data) by drag & drop,
- launch and stop apps from the PC,
- **lock** an app (kiosk mode) so it cannot be left,
- control **many devices at once**: install APKs, and launch, lock and unlock the same app on all of them.

This is an early test release (0.1). So far it has been tested on a Samsung Galaxy S20 FE 5G and a Meta Quest 3. Other Android devices should work too, but details may differ between brands. Android Apps is based on [Quest Apps](https://github.com/damian3k/quest-apps).

### 1. Requirements

- **Windows 10/11 x64.** Nothing else to install: `adb` ships in the `adb\` folder next to `AndroidApps.exe`. Keep the two together.
- An Android device with **USB debugging** turned on (in Developer options), or a Quest headset with **Developer Mode** turned on. Section 2 shows how.
- A USB cable that carries data (not a charge-only cable), needed once per device.
- For Wi-Fi: the computer and the device on the **same network**. Guest networks and networks that isolate devices from each other block it.
- Some brands need the manufacturer's USB driver on Windows (for example Samsung USB Driver) if the device is not seen at all.

### 2. First-time setup of a new device (pairing)

Every new device must be connected **by cable once**. That is when the device learns to trust your PC. Wi-Fi cannot be set up for a device that has never been connected by cable.

1. **Turn on USB debugging.**
   - **Phone or tablet:** open Settings → About phone and tap **Build number** 7 times (on Samsung: Settings → About phone → Software information → Build number). Enter your PIN if asked. A new **Developer options** menu appears in Settings (often under System). Open it and turn on **USB debugging**.
   - **Xiaomi (MIUI / HyperOS):** in Developer options also turn on **Install via USB** and **USB debugging (Security settings)**. Without them, installing APKs fails.
   - **Android TV:** the Build entry is usually under Settings → Device Preferences → About. The rest is the same.
   - **Meta Quest:** open the Meta Horizon app on your phone → Devices → pick the headset → Headset settings → Developer Mode → on. Restart the headset. The exact menu names can differ between app versions. Meta may also ask you to create or join a developer organization on its website first.
2. **Close other tools that bring their own adb**, such as Android Studio, SideQuest, Meta Quest Developer Hub, or phone-manager suites like Samsung Smart Switch. Two adb versions running at the same time keep disconnecting each other.
3. Start `AndroidApps.exe` and **connect the device by a USB data cable**.
4. **Unlock the screen** (on a Quest: put the headset on). A prompt says *"Allow USB debugging?"*. Tick **"Always allow from this computer"** and press **Allow**.
   - Until you do this, the device list shows it as *unauthorized*. **This is the most common problem.** The prompt only appears on an unlocked screen.
   - If no prompt appears, unplug and plug the cable back in with the screen unlocked.
   - With "Always allow" ticked, this prompt never comes back for this PC.
5. Press **Refresh**. The device shows up with an icon for its type, for example *"📱 samsung SM G781B •0402 — USB"* or *"🥽 Quest 3 •0402 — USB"*, and its apps load. Icons: 📱 phone, 📲 tablet, 📺 TV, ⌚ watch, 🥽 Quest.
6. **Turn on Wi-Fi.** Press **Enable Wi-Fi** in the toolbar. After a few seconds the list shows *"USB + Wi-Fi"* and the status says you can unplug the cable.
7. *(Recommended)* Tick **Keep awake**. A device that goes to sleep can drop the Wi-Fi connection. What Keep awake does depends on the device:
   - **Quest:** the headset ignores the proximity sensor and stays on when taken off the head. It uses more battery.
   - **Phone or tablet:** it turns on the developer option **Stay awake**, so the screen stays on while charging (also over USB). On battery the device sleeps as usual.
8. **Unplug the cable.** The app switches to Wi-Fi by itself (*"Cable unplugged — continuing over Wi-Fi"*). Everything works the same, including installing.

The device is now remembered: its name, model and Wi-Fi address are saved on the PC.

Android 11 and newer also has **Wireless debugging** in Developer options, with its own pairing code. Android Apps does not use it. It uses the classic way (`adb tcpip 5555`) through the **Enable Wi-Fi** button, which works on any Android version after one cable connection.

### 3. Every day, and after a device restart

- **Device was not restarted:** just start Android Apps. It finds the remembered device on Wi-Fi and connects by itself, with no cable.
- **Device was restarted or powered off:** the device turns Wi-Fi ADB off on every restart. Plug in the cable, press **Enable Wi-Fi**, and unplug. You do **not** have to confirm "Allow USB debugging" again.
- **Device got a new IP address** (for example after a router restart): press **Find on Wi-Fi**. It scans the local network for devices that have Wi-Fi ADB on.

### 4. Main window

The window title is *"Android Apps 0.1 — what's on my device"*.

**Toolbar**

| Control | What it does |
|---|---|
| **Refresh** | Reloads apps, storage and large files from the selected device. |
| **Device list** | Devices connected now, plus ones seen before. Each one has an icon by type (📱 📲 📺 ⌚ 🥽) and its manufacturer and model. Labels: *USB*, *Wi-Fi*, *USB + Wi-Fi*, *nearby* (answers on Wi-Fi, connects when picked), *not found*. |
| **Find on Wi-Fi** | Searches the local network for devices with Wi-Fi ADB on. |
| **Multi-device…** | Opens the window for controlling many devices at once (see section 6). |
| **Enable Wi-Fi / Disconnect Wi-Fi** | Turns Wi-Fi ADB on for a device connected by cable, or drops the Wi-Fi connection. |
| **MTP** | Switches USB to MTP (Media Transfer Protocol), so file explorers on your computer can browse the device over the cable. Turning it off returns USB to ADB only. ADB keeps working in both modes. |
| **Keep awake** | Quest: the headset stays on when it is taken off; a restart turns this off again. Phone or tablet: turns on *Stay awake*, so the screen stays on while charging; on battery it sleeps as usual. |
| **Sort** | **Sort: size** or **Sort: name**. |

**Storage bar.** Shows how full the device is: store apps are blue, sideloaded apps orange, app data and the system grey. Point at an app in the list to highlight it on the bar.

**Tabs**

- **Store — official / Sideloaded — unknown sources.** Every app with its icon, version, size and source. Apps installed from Google Play, Galaxy Store, Huawei AppGallery, Xiaomi GetApps, OPPO App Market, Amazon Appstore, F-Droid or the Meta Store count as *Store — official*. Everything else is *Sideloaded*. The search box above the list filters it by app name or package name. Each row has buttons:
  - **Launch** starts the app on the device. While the app runs, the row shows *● running*, and the buttons change to **Stop** and **Lock**.
  - **Lock** turns on kiosk mode (see section 5). **Unlock** ends it.
  - **Uninstall** removes the app and its data, after asking first.
- **Large files (app data).** Files of 50 MB or more in shared storage: downloads, videos, game data. **Delete** removes a file after asking first. A game may download deleted data again.
- **Install apps.**
  1. Drag `.apk` files or whole game folders into the window, or use **Choose APK…** / **Choose folder…**. You can also drag an APK onto `AndroidApps.exe`.
  2. OBB game data is found automatically: a folder named after the package, or `main.*.<package>.obb` files next to the APK. It is copied to `/sdcard/Android/obb/<package>/`.
  3. Each entry shows whether it is a **new app** or an **update** of an installed version.
  4. Press **Install**. Progress and speed are shown for each app. **Cancel** stops the queue. **Clear finished** removes finished entries from the list, and **Remove** takes out a single entry.
     When an app is installed, its row gets **Launch** (it turns into **Stop** while the app runs, to close it) and **Install again**, which installs the same APK (and OBB) once more, for example after an uninstall.
  5. **Grant all permissions** gives the app every permission it asks for, so the device does not ask later.
  6. Two cases ask before going ahead:
     - the APK is signed with a different key than the installed version → *Uninstall & install* (the app's saved data is lost);
     - the APK is an older version than the installed one → *Downgrade*.
  7. Split-APK bundles (`.xapk`, `.apks`, `.apkm`) are not supported.

### 5. Lock (kiosk mode)

**Lock** pins a running app. On phones and tablets this uses Android's screen pinning; on a Quest the headset's own pinning.

- other apps cannot be opened,
- if someone goes to the home screen, the recent apps or a system menu, the app is brought back on top within about a second. On a Quest this also covers the Meta menu (Meta button or hand gesture),
- if someone quits the app, it is started and locked again within a few seconds,
- if the pin is lifted on the device, it is put back.

Limitations:

- System menus **cannot be fully blocked** this way. They can flash for a moment. Full blocking needs a device managed by a company (MDM): on Android, for example Android Enterprise with the app as device owner; on a Quest, Meta Horizon Managed Services, ManageXR or ArborXR, with the headset enrolled in an organization.
- Guarding needs **Android Apps running on the PC and connected** to the device. Use Wi-Fi and Keep awake (a phone or tablet should stay on its charger). With the PC app closed, the device stays pinned, but an app that was quit or left is not brought back.
- When you close Android Apps while devices are locked, it asks: **Unlock & close** or **Keep locked**.

### 6. Multi-device window

**What it is for:** classrooms, kiosks and shops, demo stations, test phones, VR arcades. In general, any time several devices should run the same app and stay locked in it, controlled from one PC.

**Setup:** pair **every** device once as described in section 2 (cable → Allow USB debugging → Enable Wi-Fi). Then they can all run on Wi-Fi at the same time.

**Use it:**

1. In the main window, press **Multi-device…**. The window *"Android Apps — multi-device"* opens. Remembered devices that answer on Wi-Fi are connected automatically.
2. **Name the devices:** click the name field (for example *"Quest 3 •0402"*) and type something like *"Station 1"*. The name is saved and also shown in the main window.
3. **Tick** the devices to control, or use **Select all** / **Select none**. Each row shows the connection, battery (⚡ while charging), the app on top (*Now*), the kiosk state and the result of the last action.
4. **Pick an app** on the right. **Filter apps…** narrows the list. The list shows apps on the selected devices; *on all 4* in green, or *on 3 of 4* in yellow. Below the list it says which selected devices do not have the app.
5. Press an action. It runs **on all selected devices at the same time**:

| Action | What happens |
|---|---|
| **Launch** | Starts the app. Devices without the app are skipped. |
| **Launch & Lock** | Starts the app and locks it (kiosk). A device locked to another app is unlocked first. |
| **Unlock** | Ends the kiosk. |
| **Stop** | Unlocks and closes the app. |
| **Keep awake On / Off** | Turns Keep awake on or off (see section 4): Quest headsets stay on when taken off, phones and tablets stay on while charging. |

**Installing on many devices:** press **Install APK…** or **Install folder…** (or drop APK files and game folders on the window). The app shows what it found and on which devices, and after you confirm it installs everything **on all selected devices in parallel**, including OBB game data. Progress is shown next to each device. All permissions the apps ask for are granted. A device that already has a newer version, or a copy signed with a different key, is skipped with a note; downgrade or replace that one from the main window. **Cancel install** stops all uploads.

The result for each device (with the time) appears next to it, and a summary appears at the top, for example *"done on 3 device(s), 1 skipped"*.

Locks are shared between both windows: a device locked here shows **Unlock** in the main window too, and the other way round.

### 7. Troubleshooting

| Problem | What to do |
|---|---|
| *unauthorized* | The most common problem. Unlock the device screen (on a Quest: put the headset on) and accept "Allow USB debugging" with *Always allow from this computer* ticked. If no prompt appears, unplug and plug the cable back in with the screen unlocked. |
| *No device* | Check that the cable carries data. Check that USB debugging is on. Wake and unlock the device. Try another USB port. Close Android Studio, SideQuest, MQDH and phone-manager suites (for example Samsung Smart Switch). If Windows does not see the device at all, install the manufacturer's USB driver (for example Samsung USB Driver). Press Refresh. |
| Install fails on Xiaomi | Turn on **Install via USB** and **USB debugging (Security settings)** in Developer options. |
| Wi-Fi: *Could not connect / not found* | The PC and device must be on the same network, not a guest network. Turn off any VPN and check the firewall. If the device was restarted, turn Wi-Fi ADB on again by cable. |
| Wi-Fi keeps dropping | Turn on **Keep awake**. A device can turn Wi-Fi off when it sleeps. A phone or tablet stays awake only while charging. |
| New IP address | **Find on Wi-Fi**. |
| Install error | The message explains it (*different key*, *newer version installed*, *not enough space*, *wrong CPU*…). |
| Kiosk app not coming back | Android Apps must be running and connected. Check the status line and the device row. |

### 8. Files and extras

- Settings and cache live in `%AppData%\AndroidApps\`:
  - `cache\` holds app names and icons,
  - `devices.json` holds remembered devices, their names and IP addresses,
  - `selected-device.txt` holds the device selected in the main window.
- Command-line helpers, mainly for testing:
  - `AndroidApps.exe <file.apk|folder>…` opens the app with these files already in the install queue.
  - `AndroidApps.exe --scan <paths>` shows what would be queued, without installing.
  - `AndroidApps.exe --label-file <file.apk>` reads the name and version from a local APK.

---

<a id="polski"></a>
## Polski

Android Apps to program na Windows do urządzeń z Androidem: telefonów, tabletów, Android TV i gogli Meta Quest. Łączy się z urządzeniem przez ADB, kablem USB albo przez Wi-Fi, i pozwala:

- zobaczyć wszystkie zainstalowane aplikacje z rozmiarem, wersją i ikoną, a także zajętość pamięci,
- odinstalowywać aplikacje i usuwać duże, zalegające pliki,
- instalować APK (razem z danymi gier OBB) przez przeciągnięcie,
- uruchamiać i zamykać aplikacje z komputera,
- **blokować** aplikację (tryb kiosku), tak żeby nie dało się z niej wyjść,
- sterować **wieloma urządzeniami naraz**: instalować APK oraz uruchamiać, blokować i odblokowywać tę samą aplikację na wszystkich.

To wczesna wersja testowa (0.1). Na razie była sprawdzana na Samsungu Galaxy S20 FE 5G i Meta Quest 3. Inne urządzenia z Androidem też powinny działać, ale szczegóły mogą się różnić w zależności od producenta. Android Apps powstał na bazie [Quest Apps](https://github.com/damian3k/quest-apps).

### 1. Wymagania

- **Windows 10/11 x64.** Niczego nie trzeba doinstalowywać: `adb` jest w folderze `adb\` obok `AndroidApps.exe`. Trzymaj je razem.
- Urządzenie z Androidem z włączonym **debugowaniem USB** (w opcjach programisty) albo gogle Quest z włączonym **trybem dewelopera**. Jak to zrobić, opisuje punkt 2.
- Kabel USB do przesyłania danych (nie sam ładujący), potrzebny raz na każde urządzenie.
- Do Wi-Fi: komputer i urządzenie w **tej samej sieci**. Sieci dla gości i sieci izolujące urządzenia od siebie to blokują.
- Niektóre marki wymagają na Windows sterownika USB od producenta (np. Samsung USB Driver), jeśli komputer w ogóle nie widzi urządzenia.

### 2. Pierwsze podłączenie nowego urządzenia (parowanie)

Każde nowe urządzenie trzeba **raz podłączyć kablem**. Wtedy urządzenie uczy się ufać Twojemu komputerowi. Nie da się włączyć Wi-Fi dla urządzenia, które nigdy nie było podłączone kablem.

1. **Włącz debugowanie USB.**
   - **Telefon lub tablet:** otwórz Ustawienia → Informacje o telefonie i stuknij 7 razy w **Numer wersji** (na Samsungu: Ustawienia → Informacje o telefonie → Informacje o oprogramowaniu → Numer wersji). Jeśli trzeba, podaj PIN. W Ustawieniach pojawi się nowe menu **Opcje programisty** (często w sekcji System). Otwórz je i włącz **Debugowanie USB**.
   - **Xiaomi (MIUI / HyperOS):** w opcjach programisty włącz też **Instaluj przez USB** i **Debugowanie USB (ustawienia zabezpieczeń)**. Bez tego instalacja APK się nie uda.
   - **Android TV:** numer wersji jest zwykle w Ustawienia → Ustawienia urządzenia → Informacje. Reszta wygląda tak samo.
   - **Meta Quest:** otwórz aplikację Meta Horizon w telefonie → Urządzenia → wybierz gogle → Ustawienia gogli → Tryb dewelopera → włącz. Zrestartuj gogle. Nazwy menu mogą się różnić w zależności od wersji aplikacji. Meta może też najpierw poprosić o założenie lub dołączenie do organizacji deweloperskiej na swojej stronie.
2. **Zamknij inne programy z własnym adb**, np. Android Studio, SideQuest, Meta Quest Developer Hub albo pakiety do zarządzania telefonem, takie jak Samsung Smart Switch. Dwie wersje adb działające jednocześnie wzajemnie się rozłączają.
3. Uruchom `AndroidApps.exe` i **podłącz urządzenie kablem USB do przesyłania danych**.
4. **Odblokuj ekran** (w Queście: załóż gogle). Pojawi się pytanie *„Zezwolić na debugowanie USB?”*. Zaznacz **„Zawsze zezwalaj z tego komputera”** i naciśnij **Zezwól**.
   - Dopóki tego nie zrobisz, lista urządzeń pokazuje je jako *unauthorized*. **To najczęstszy problem.** Pytanie pojawia się tylko na odblokowanym ekranie.
   - Jeśli pytanie się nie pojawia, odepnij i podepnij kabel przy odblokowanym ekranie.
   - Z zaznaczonym „Zawsze zezwalaj” to pytanie dla tego komputera już nigdy nie wróci.
5. Naciśnij **Refresh**. Urządzenie pojawi się z ikoną swojego typu, np. *„📱 samsung SM G781B •0402 — USB”* albo *„🥽 Quest 3 •0402 — USB”*, i wczytają się aplikacje. Ikony: 📱 telefon, 📲 tablet, 📺 telewizor, ⌚ zegarek, 🥽 Quest.
6. **Włącz Wi-Fi.** Naciśnij **Enable Wi-Fi** w górnym pasku. Po kilku sekundach lista pokaże *„USB + Wi-Fi”*, a status napisze, że można odpiąć kabel.
7. *(Zalecane)* Zaznacz **Keep awake**. Gdy urządzenie zasypia, połączenie Wi-Fi może się zerwać. Działanie Keep awake zależy od urządzenia:
   - **Quest:** gogle ignorują czujnik zbliżeniowy i nie wyłączają się po zdjęciu z głowy. Bateria zużywa się szybciej.
   - **Telefon lub tablet:** włącza opcję programisty **Pozostaw włączony ekran**, więc ekran nie gaśnie podczas ładowania (także przez USB). Na baterii urządzenie zasypia jak zwykle.
8. **Odepnij kabel.** Aplikacja sama przejdzie na Wi-Fi (*„Cable unplugged — continuing over Wi-Fi”*). Wszystko działa tak samo, łącznie z instalowaniem.

Urządzenie jest teraz zapamiętane: jego nazwa, model i adres Wi-Fi są zapisane na komputerze.

Android 11 i nowszy ma też w opcjach programisty **Debugowanie bezprzewodowe** z własnym kodem parowania. Android Apps z niego nie korzysta. Używa klasycznego sposobu (`adb tcpip 5555`) przez przycisk **Enable Wi-Fi**, który działa na każdej wersji Androida po jednym podłączeniu kablem.

### 3. Na co dzień i po restarcie urządzenia

- **Urządzenie nie było restartowane:** po prostu uruchom Android Apps. Program sam znajdzie zapamiętane urządzenie w Wi-Fi i połączy się z nim, bez kabla.
- **Urządzenie zostało zrestartowane albo wyłączone:** przy każdym restarcie urządzenie wyłącza Wi-Fi ADB. Podłącz kabel, naciśnij **Enable Wi-Fi** i odepnij. **Nie** trzeba ponownie zatwierdzać „Zezwól na debugowanie USB”.
- **Urządzenie dostało nowy adres IP** (np. po restarcie routera): naciśnij **Find on Wi-Fi**. Program przeszuka sieć lokalną w poszukiwaniu urządzeń z włączonym Wi-Fi ADB.

### 4. Główne okno

Tytuł okna to *„Android Apps 0.1 — what's on my device”*.

**Górny pasek**

| Element | Do czego służy |
|---|---|
| **Refresh** | Ponownie wczytuje aplikacje, pamięć i duże pliki z wybranego urządzenia. |
| **Lista urządzeń** | Urządzenia podłączone teraz oraz te widziane wcześniej. Każde ma ikonę typu (📱 📲 📺 ⌚ 🥽) oraz producenta i model. Opisy: *USB*, *Wi-Fi*, *USB + Wi-Fi*, *nearby* (w zasięgu Wi-Fi, połączy się po wybraniu), *not found*. |
| **Find on Wi-Fi** | Przeszukuje sieć lokalną w poszukiwaniu urządzeń z włączonym Wi-Fi ADB. |
| **Multi-device…** | Otwiera okno do sterowania wieloma urządzeniami naraz (punkt 6). |
| **Enable Wi-Fi / Disconnect Wi-Fi** | Włącza Wi-Fi ADB dla urządzenia podłączonego kablem albo rozłącza połączenie Wi-Fi. |
| **MTP** | Przełącza USB w tryb MTP (Media Transfer Protocol), dzięki czemu eksplorator plików na komputerze widzi pamięć urządzenia przez kabel. Wyłączenie przywraca USB do trybu „tylko ADB”. ADB działa w obu trybach. |
| **Keep awake** | Quest: gogle nie zasypiają po zdjęciu z głowy; restart wyłącza tę opcję. Telefon lub tablet: włącza *Pozostaw włączony ekran*, więc ekran nie gaśnie podczas ładowania; na baterii urządzenie zasypia jak zwykle. |
| **Sort** | **Sort: size** (według rozmiaru) albo **Sort: name** (według nazwy). |

**Pasek pamięci.** Pokazuje zajętość urządzenia: aplikacje ze sklepu na niebiesko, wgrane z zewnątrz (sideloaded) na pomarańczowo, dane aplikacji i system na szaro. Najechanie na aplikację na liście podświetla ją na pasku.

**Zakładki**

- **Store — official / Sideloaded — unknown sources.** Wszystkie aplikacje z ikoną, wersją, rozmiarem i źródłem. Aplikacje zainstalowane ze Sklepu Google Play, Galaxy Store, Huawei AppGallery, Xiaomi GetApps, OPPO App Market, Amazon Appstore, F-Droid albo Meta Store trafiają do *Store — official*. Wszystkie pozostałe to *Sideloaded*. Pole wyszukiwania nad listą filtruje ją po nazwie aplikacji albo pakietu. W każdym wierszu są przyciski:
  - **Launch** uruchamia aplikację na urządzeniu. Gdy aplikacja działa, wiersz pokazuje *● running*, a przyciski zmieniają się na **Stop** i **Lock**.
  - **Lock** włącza tryb kiosku (punkt 5). **Unlock** go wyłącza.
  - **Uninstall** usuwa aplikację razem z jej danymi, po potwierdzeniu.
- **Large files (app data).** Pliki od 50 MB wzwyż we wspólnej pamięci: pobrane pliki, filmy, dane gier. **Delete** usuwa plik po potwierdzeniu. Gra może ponownie pobrać usunięte dane.
- **Install apps.**
  1. Przeciągnij pliki `.apk` albo całe foldery z grami do okna lub użyj **Choose APK…** / **Choose folder…**. Można też przeciągnąć APK na `AndroidApps.exe`.
  2. Dane gier OBB są wykrywane automatycznie: folder o nazwie pakietu albo pliki `main.*.<pakiet>.obb` obok APK. Trafiają do `/sdcard/Android/obb/<pakiet>/`.
  3. Każda pozycja pokazuje, czy to **nowa aplikacja**, czy **aktualizacja** zainstalowanej wersji.
  4. Naciśnij **Install**. Przy każdej aplikacji widać postęp i prędkość. **Cancel** zatrzymuje kolejkę. **Clear finished** usuwa z listy zakończone pozycje, a **Remove** usuwa pojedynczą pozycję.
     Przy zainstalowanej aplikacji pojawiają się **Launch** (gdy aplikacja działa, zmienia się w **Stop**, żeby ją zamknąć) oraz **Install again**, które instaluje ten sam APK (i OBB) jeszcze raz, np. po odinstalowaniu.
  5. **Grant all permissions** nadaje aplikacji wszystkie uprawnienia, o które prosi, więc urządzenie nie pyta o nie później.
  6. W dwóch przypadkach program pyta przed kontynuacją:
     - APK jest podpisane innym kluczem niż zainstalowana wersja → *Uninstall & install* (zapisane dane aplikacji przepadną);
     - APK to starsza wersja niż zainstalowana → *Downgrade*.
  7. Paczki dzielone (`.xapk`, `.apks`, `.apkm`) nie są obsługiwane.

### 5. Lock (tryb kiosku)

**Lock** przypina uruchomioną aplikację. Na telefonach i tabletach korzysta z androidowego przypinania ekranu, w Queście z przypinania wbudowanego w gogle.

- nie da się otworzyć innych aplikacji,
- gdy ktoś przejdzie do ekranu głównego, ostatnich aplikacji albo menu systemowego, aplikacja wraca na wierzch w ciągu około sekundy. W Queście dotyczy to też menu Meta (przycisk Meta albo gest dłoni),
- gdy ktoś zamknie aplikację, uruchamia się ona ponownie i zostaje znowu zablokowana w ciągu kilku sekund,
- gdy ktoś zdejmie przypięcie na urządzeniu, zostaje ono założone z powrotem.

Ograniczenia:

- Tym sposobem **nie da się całkowicie zablokować** menu systemowych. Mogą na chwilę mignąć. Pełna blokada wymaga urządzenia zarządzanego przez firmę (MDM): na Androidzie np. Android Enterprise z aplikacją jako właścicielem urządzenia (device owner), w Queście Meta Horizon Managed Services, ManageXR albo ArborXR, z goglami zapisanymi w organizacji.
- Pilnowanie wymaga, żeby **Android Apps działał na komputerze i był połączony** z urządzeniem. Używaj Wi-Fi i Keep awake (telefon lub tablet niech stoi na ładowarce). Po zamknięciu programu urządzenie zostaje przypięte, ale zamknięta lub opuszczona aplikacja nie zostanie już przywrócona.
- Przy zamykaniu Android Apps z zablokowanymi urządzeniami program pyta: **Unlock & close** albo **Keep locked**.

### 6. Okno wielu urządzeń (Multi-device)

**Do czego służy:** klasy, kioski i sklepy, stanowiska demo, telefony testowe, salony VR. Ogólnie wszędzie tam, gdzie kilka urządzeń ma uruchomić tę samą aplikację i w niej zostać, sterowanych z jednego komputera.

**Przygotowanie:** sparuj **każde** urządzenie raz, tak jak w punkcie 2 (kabel → Zezwól na debugowanie USB → Enable Wi-Fi). Potem wszystkie mogą działać jednocześnie przez Wi-Fi.

**Jak używać:**

1. W głównym oknie naciśnij **Multi-device…**. Otworzy się okno *„Android Apps — multi-device”*. Zapamiętane urządzenia, które odpowiadają w Wi-Fi, połączą się automatycznie.
2. **Nazwij urządzenia:** kliknij pole z nazwą (np. *„Quest 3 •0402”*) i wpisz np. *„Stanowisko 1”*. Nazwa zapisuje się na stałe i jest widoczna także w głównym oknie.
3. **Zaznacz** urządzenia, którymi chcesz sterować, albo użyj **Select all** / **Select none**. Każdy wiersz pokazuje połączenie, baterię (⚡ podczas ładowania), aplikację na wierzchu (*Now*), stan kiosku i wynik ostatniej akcji.
4. **Wybierz aplikację** po prawej. Pole **Filter apps…** zawęża listę. Lista pokazuje aplikacje z zaznaczonych urządzeń: *on all 4* na zielono albo *on 3 of 4* na żółto. Pod listą widać, na których zaznaczonych urządzeniach danej aplikacji brakuje.
5. Naciśnij akcję. Wykonuje się **na wszystkich zaznaczonych urządzeniach jednocześnie**:

| Akcja | Co się dzieje |
|---|---|
| **Launch** | Uruchamia aplikację. Urządzenia bez tej aplikacji są pomijane. |
| **Launch & Lock** | Uruchamia aplikację i ją blokuje (kiosk). Urządzenie zablokowane na innej aplikacji jest najpierw odblokowywane. |
| **Unlock** | Wyłącza kiosk. |
| **Stop** | Odblokowuje i zamyka aplikację. |
| **Keep awake On / Off** | Włącza albo wyłącza Keep awake (punkt 4): gogle Quest nie zasypiają po zdjęciu z głowy, telefony i tablety nie gaszą ekranu podczas ładowania. |

**Instalacja na wielu urządzeniach:** naciśnij **Install APK…** albo **Install folder…** (albo przeciągnij pliki APK i foldery gier na okno). Program pokaże, co znalazł i na których urządzeniach zainstaluje, a po potwierdzeniu instaluje wszystko **na wszystkich zaznaczonych urządzeniach naraz**, razem z danymi OBB. Postęp widać przy każdym urządzeniu. Aplikacje dostają wszystkie uprawnienia, o które proszą. Urządzenie, które ma już nowszą wersję albo kopię podpisaną innym kluczem, jest pomijane z komentarzem; taką instalację zrób w głównym oknie. **Cancel install** przerywa wszystkie wysyłki.

Wynik dla każdego urządzenia (z godziną) pojawia się przy nim, a podsumowanie na górze, np. *„done on 3 device(s), 1 skipped”*.

Blokady są wspólne dla obu okien: urządzenie zablokowane tutaj ma przycisk **Unlock** także w głównym oknie, i odwrotnie.

### 7. Rozwiązywanie problemów

| Problem | Co zrobić |
|---|---|
| *unauthorized* | Najczęstszy problem. Odblokuj ekran urządzenia (w Queście: załóż gogle) i zatwierdź „Zezwól na debugowanie USB” z zaznaczonym *Zawsze zezwalaj z tego komputera*. Jeśli pytanie się nie pojawia, odepnij i podepnij kabel przy odblokowanym ekranie. |
| *No device* | Sprawdź, czy kabel przesyła dane i czy debugowanie USB jest włączone. Wybudź i odblokuj urządzenie. Spróbuj innego portu USB. Zamknij Android Studio, SideQuest, MQDH i pakiety do zarządzania telefonem (np. Samsung Smart Switch). Jeśli Windows w ogóle nie widzi urządzenia, zainstaluj sterownik USB producenta (np. Samsung USB Driver). Naciśnij Refresh. |
| Instalacja nie działa na Xiaomi | Włącz w opcjach programisty **Instaluj przez USB** i **Debugowanie USB (ustawienia zabezpieczeń)**. |
| Wi-Fi: *Could not connect / not found* | Komputer i urządzenie muszą być w tej samej sieci, nie w sieci dla gości. Wyłącz VPN i sprawdź zaporę. Jeśli urządzenie było restartowane, włącz Wi-Fi ADB ponownie przez kabel. |
| Wi-Fi ciągle się rozłącza | Włącz **Keep awake**. Uśpione urządzenie może wyłączyć Wi-Fi. Telefon lub tablet nie zasypia tylko podczas ładowania. |
| Nowy adres IP | **Find on Wi-Fi**. |
| Błąd instalacji | Komunikat wyjaśnia przyczynę (*inny klucz*, *zainstalowana nowsza wersja*, *brak miejsca*, *inny procesor*…). |
| Aplikacja w kiosku nie wraca | Android Apps musi działać i być połączony. Sprawdź linię statusu i wiersz urządzenia. |

### 8. Pliki i dodatki

- Ustawienia i pamięć podręczna są w `%AppData%\AndroidApps\`:
  - `cache\` przechowuje nazwy i ikony aplikacji,
  - `devices.json` przechowuje zapamiętane urządzenia, ich nazwy i adresy IP,
  - `selected-device.txt` przechowuje urządzenie wybrane w głównym oknie.
- Polecenia z linii poleceń, głównie do testów:
  - `AndroidApps.exe <plik.apk|folder>…` otwiera program z tymi plikami od razu w kolejce instalacji.
  - `AndroidApps.exe --scan <ścieżki>` pokazuje, co trafiłoby do kolejki, bez instalowania.
  - `AndroidApps.exe --label-file <plik.apk>` odczytuje nazwę i wersję z lokalnego APK.
