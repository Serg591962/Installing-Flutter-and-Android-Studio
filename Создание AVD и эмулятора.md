##### Шаг 1. Создание AVD (Android Virtual Device)
1. **Откройте Android Studio.**
2. **Перейдите в AVD Manager:** More Actions → Virtual Device Manager.
3. **Создание нового виртуального устройства:** + (Нажмите кнопку **Create Virtual Device**)    
4. **Выбор устройства:** Pixel 5 -> Next.    
5. **Выбор образа системы (System Image):** Выберите версию Android, которую хотите эмулировать (Android 13, API 33). Скачать образ -> Finish
6.  **Создайте AVD:**  Finish
##### **Шаг 2. Проверка нового AVD, если при первом запуске создания эмулятора появляется system isn't responding**
###### **2.1. Проверка системного образа**
- Android Studio → Tools → SDK Manager -> вкладка SDK Platforms.
- Найдите API, на котором создан AVD (например, Android 13 API 33) -> Нажмите "Show Package Details" -> Удалите образ Google APIs x86_64 System Image (или тот, который вы используете) ->  Снова скачайте этот же образ.
- Это исключит вариант с повреждённым system.img.
##### **Шаг 2. Запуск эмулятора**
1. После создания AVD в AVD Manager появится список виртуальных устройств.
2. Нажмите на зелёный треугольник (кнопку **Play**) рядом с нужным AVD.
3. Запустится эмулятор, который загрузит выбранный образ Android и создаст виртуальное устройство на вашем компьютере.
4. После завершения процесса загрузки появляется образ телефона (UI Android) 
##### **Шаг 5. Проверка работоспособности эмулятора**
1. Проверка списка доступных AVD (виртуальных устройств): PS C:\Windows\system32> D:\progi\src\Android\Sdk\emulator\emulator.exe -list-avds => Pixel_6
2. Запуск нужного эмулятора: D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_6 => После завершения процесса загрузки появляется образ телефона (UI Android)  

##### **Шаг 1. Закрыть эмулятор**
1. PowerShell -> adb -s emulator-5554 emu kill
##### **Шаг 2. Удалить AVD Pixel_5**
1. D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager delete avd -n Pixel_5 -> AVD 'Pixel_5' deleted.
##### **Шаг 3. Создать новый AVD Pixel_5**
1. Посмотри доступные образы: D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat --list -> найти Available Packages:
2. Скачать системный образ: D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\sdkmanager.bat "system-images;android-35;google_apis;x86_64"
3. Создать новый Pixel_5:  D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager.bat create avd -n Pixel_5 -k "system-images;android-35;google_apis;x86_64" -d pixel_5
##### **Шаг 4. Создать новый эмулятор Pixel_5**
1. Запустить Pixel_5 с очисткой данных и без снапшота: D:\progi\src\Android\Sdk\emulator\emulator.exe -avd Pixel_5 -no-snapshot-load -wipe-data
2. После запуска эмулятора и завершения процесса загрузки, появления образа телефона (UI Android), проверить статус подключения эмулятора к ADB: adb devices => List of devices attached emulator-5554	device -> emulator-5554 -> подключённый эмулятор
##### **Шаг 5. Закрыть эмулятор**
1. PowerShell -> adb -s emulator-5554 emu kill
##### **Шаг 6. Проверить, что ADB работает в терминале Visual Studio Code**
1. Откройте Visual Studio Code.
2. Откройте встроенный терминал: adb devices



