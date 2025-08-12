
**ADB (Android Debug Bridge)** — это мощный инструмент командной строки, который позволяет взаимодействовать с Android-устройствами и эмуляторами из компьютера.
##### **Шаг 1. Проверка работоспособности эмулятора**
1. Проверка списка доступных AVD (виртуальных устройств): PS C:\Windows\system32> D:\progi\src\Android\Sdk\emulator\emulator.exe -list-avds => Pixel_6
##### **Шаг 2. Проверить, запущен ли эмулятор**
1. PowerShell -> adb devices => List of devices attached
2. Иначе закрыть эмулятор: PowerShell -> adb -s emulator-5554 emu kill
##### **Шаг 3. Удалить AVD Pixel_5**
1. D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager delete avd -n Pixel_5 -> AVD 'Pixel_5' deleted.
##### **Шаг 4. Создать новый AVD Pixel_5**
1. Посмотри доступные образы: D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat --list -> найти Available Packages:
2. Скачать системный образ: D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat "system-images;android-35;google_apis;x86_64"
3. Создать новый Pixel_5:  D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager.bat create avd -n Pixel_5 -k "system-images;android-35;google_apis;x86_64" -d pixel_5
##### **Шаг 5. Создать новый эмулятор Pixel_5**
###### **5.1. Первый запуск - чистка и подготовка состояния**
1. Открывается терминал в Visual Studio Code: D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_5 -no-snapshot-load -wipe-data
	- `-no-snapshot-load` — запрещает загрузку старого снапшота.
    - `-wipe-data` — сбрасывает данные AVD (полный сброс).
    - Результат: Android стартует с нуля, как новый телефон из коробки.
    - После запуска проверить: adb shell getprop sys.boot_completed => 1 - эмулятор полностью загрузился, готов к работ, 0 или пусто - эмулятор ещё грузится или завис.
    - Проверить статус подключения эмулятора к ADB: adb devices => List of devices attached emulator-5554	device -> emulator-5554 -> подключённый эмулятор
2. Закрывается эмулятор корректно через крестик (Close). Это важно, чтобы данные сохранились в userdata.img.
###### **5.2. Второй запуск - создание снапшота**
1. В терминале VS Code запускаем: D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_5
2. Создаём снапшот и включаем Quick Boot: Меню  → Snapshots  -> Take Snapshot (дать понятное имя, например CleanSetup). -> запуск
3. Правильное выключение эмулятора через adb (сохранение состояния снапшота). В другом терминале (PowerShell): adb -s emulator-5554 emu kill
##### **6. Загрузка из терминала эмулятора**
###### **6.1. Загрузка из терминала эмулятора с снапшотом**
1. Узнать список снапшотов -> D:\progi\src\android_avd\Pixel_5.avd\snapshots
2. Запуск эмулятора с использованием снапшота: D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_5 -snapshot default_boot
###### **6.2. Загрузка из терминала эмулятора без снапшота**
1. D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_5 -wipe-data -no-snapshot-load
	- Параметр `-wipe-data` очистит все данные эмулятора, как после полной перезагрузки.
	- Параметр `-no-snapshot-load` запретит загрузку из любых снапшотов — будет запуск с нуля, дольше, чем Quick Boot.








D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager delete avd -n Pixel_6 -> AVD 'Pixel_6' deleted.