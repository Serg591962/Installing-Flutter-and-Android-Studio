За исходные прими следующее установки
- ОС: Windows 10 Pro
- Python: D:\Python\Python3_13_4
- Каталог установки всего ПО: D:\progi\src
- Git установлен 
- Open JDK  не установлен
- Flutter SDK не установлен
- Исходные директории по твоей системе:
	- D:\progi\src — каталог установки всего ПО
	- D:\progi\src\android_avd — каталог, где будут храниться эмуляторы AVD
	- D:\progi\src\Android — будущая установка Android SDK
	- D:\progi\src\OpenJDK — будет путь к OpenJDK
	- D:\progi\src\flutter — путь к Flutter SDK
	- D:\progi\src\VSCode — путь к VSCode
	- D:\Python\Python3_13_4 — уже установлен
	- D:\wirt\project\flutter_projects - будут создаваться все проекты 
##### **Этап 1. Подготовительный этап**
###### 1.1. **Проверка и настройка системных переменных среды для удобства работы (например, JAVA_HOME, ANDROID_HOME, ANDROID_AVD_HOME)**
- ANDROID_AVD_HOME - D:\progi\src\android_avd -> проверка echo %ANDROID_AVD_HOME% => %ANDROID_AVD_HOME%
- JAVA_HOME - D:\progi\src\OpenJDK -> проверка echo %JAVA_HOME% => echo %JAVA_HOME%
- ANDROID_HOME - D:\progi\src\Android\Sdk -> проверка echo %ANDROID_HOME% => 
- в переменную Path:
	- %ANDROID_HOME%\platform-tools
	- %ANDROID_HOME%\cmdline-tools\latest\bin
	- %JAVA_HOME%\bin
	- D:\progi\src\flutter\bin
- проверка в cmd (после установки всего ПО):
	- ==adb --version==
	- ==flutter --version==
	- java -version
	- ==avdmanager list avd==
###### **1.2. Убедиться, что Git корректно установлен и доступен из командной строки**
PowerShell -> git --version => git version 2.50.0.windows.1
Настроить глобальные параметры Git:
- git config --global user.name "Serg"
- git config --global user.email "swik591962@gmail.com"
##### **Этап 2. Установка Java OpenJDK**
###### **2.1. Скачивание и установка OpenJDK (версия, совместимая с Android Studio)**
OpenJDK 17 (LTS) - полностью поддерживается Android Studio, Gradle и Flutter на 2025 год.
- скачать с https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.10%2B7/OpenJDK17U-jdk_x64_windows_hotspot_17.0.10_7.zip -> OpenJDK17U-jdk_x64_windows_hotspot_17.0.10_7.zip
- установить  D:\progi\src\OpenJDK\bin\
###### **2.2. Настройка переменной среды JAVA_HOME, указывающей на установленный JDK**
- Открыть "Переменные среды"
	- Имя: JAVA_HOME - значение: D:\progi\src\OpenJDK
	- Path: - значение "%JAVA_HOME%\bin
- Проверка:
	- Git Bash → java -version -> openjdk version "17.0.15" 2025-04-15 LTS
	- Git Bash → javac -version -> javac 17.0.15
	- Git Bash → echo $JAVA_HOME -> D:\progi\src\OpenJDK
##### **Этап 3. Установка Android Studio**
###### **3.1. Скачивание инсталлятора Android Studio с официального сайта**
Перейти на сайт: https://developer.android.com/studio    
Нажать Download Android Studio и скачать установщик - android-studio-2024.3.2.15-windows.
###### **3.2. Установка в каталог D:\progi\src\android-studio**
Запуск установки от имени администратора.=> окно Welcome to Android Studio Setup -> Next 
Окно "Choose Components" -> оставь галочки на Android SDK, Virtual Device -> Next  
Окно "Configuration Setting" -> установить вручную путь: D:\progi\src\android-studio -> Next
Окно "Choose Start Menu Folder" -> install  
Окно "Installation Complete" -> Next
Окно "Complete Android Studio Setup"-> убрать v окна Start Android Studi -> Finish (не запуская)
###### **3.3. При первом запуске: установка Android SDK, SDK Platform Tools, SDK Build Tools, SDK Manager, настройка локалей (набор параметров, определяющих язык)**
**3.3.1: Запуск Android Studio, выбор типа установки. указание пути SDK: D:\progi\src\Android\Sdk при установке,  установка SDK с компонентами.**
Запусти Android Studio-> окно Welcome Android Studio -> Next 
Окно Instal Type -> Custom -> Next
Окно "Components Setup" -> 
- Установка Android SDK Location: D:\progi\src\Android\Sdk
- Убедится, что выбрано:
    - ✅ Android SDK
    - ✅ Android SDK Platform-Tools (Android 15.0 - это API 35)
    - ✅ Performance (Android Emulator, hypervisor driver)
    - ✅ Android Virtual Device (AVD)
Next -> 
Окно "Werify Setting" -> Next
Окно "License Agreement" -> Accept -> Finish => Android Studio скачает SDK и установит всё в D:\progi\src\Android\Sdk -> Finish
**3.3.2. Проверка установки SDK, Platform Tools, Emulator через SDK Manager**
После завершения загрузки компонентов (может занять 2–5 мин), откроется окно Welcome to Android Studio -> More Actions → SDK Manager
Окно "Languages&Frameworcs > Android SDC" -> Вкладка SDK Platforms:
- Android SDK Location: D:\progi\src\Android\Sdk
- Android 15
Окно "Languages&Frameworcs > Android SDC" -> Вкладка SDK Tools:
- ✅ Android SDK Build-Tools
- ✅ Android Emulator
- ✅ Android Command-line Tools
- ✅ Google USB Driver (если требуется)
Apply -> OK
Окно " SDK Components Instaler" -> Finish
Окно "Languages&Frameworcs > Android SDC" -> Вкладка SDK Platforms: -> OK
###### **3.4. Настройка среды AVD через переменную ANDROID_AVD_HOME**
Завершить все процессы Android Studio перед изменением переменной.
Создай каталог для AVD - D:\progi\src\android_avd
Создать переменную среды ANDROID_AVD_HOME - D:\progi\src\android_avd
Проверка PowerShell -> echo $env:ANDROID_AVD_HOME => D:\progi\src\android_avd
Создать AVD: Открыть Android Studio -> 
Окно "Welcome to Android Studio" → More Actions → Device Manager 
Окно "Device Manager" -> + (Create Device) 
Окно "Add Device" -> выбрать Pixel 5 -> Next 
Окно "Configure Virtual Device"-> выбрать API 35 - Android 15.0 -> Finish => AVD должен быть создан в: D:\progi\src\android_avd\.android\avd 
Окно " SDK Components Instaler" -> Finish
Окно "Device Manager" -> появился AVD Pixel 5
D:\progi\src\android_avd\.android\avd -> должны быть файл .ini и каталог Pixel_5.avd
##### **Этап 4. Настройка Android SDK**
###### **4.1. Установка SDK платформ (Android 12 / 13)**
Запустить Android Studio -> откроется окно Welcome Android Studio -> More Actions → SDK Manager
Окно "Languages&Frameworcs > Android SDC" -> Вкладка SDK Platforms:
- ✅ Android 13.0 (Tiramisu) — API Level 33
- ✅ Android 12.0 (Snow Cone) — API Level 31
Apply -> OK => Android Studio скачает и установит необходимые SDK платформы
Окно " SDK Components Instaler" -> Finish -> OK
###### **4.2 Установка Build Tools и Platform Tools**
Запустить Android Studio -> откроется окно Welcome to Android Studio → More Actions → SDK Manager
Окно "Languages&Frameworcs > Android SDC" -> Вкладка SDK Tools:
✅ Android SDK Build-Tools -> Show Package Details -> выбрать 32.0.0
✅ Android SDK Platform-Tools
✅ Android Emulator
✅ Intel x86 Emulator Accelerator (HAXM installer)
Apply → OK
Окно " SDK Components Instaler" -> Finish -> OK
###### **4.3. Проверка наличия и корректности установки SDK**
Проверь каталог SDK: D:\progi\src\Android\Sdk\ -> Должны быть следующие подпапки:
build-tools, platforms, platform-tools, emulator, system-images
###### **4.4. Проверка и настройка AVD**
Запустить Android Studio -> откроется окно Welcome to Android Studio -> More Actions → Device Manager -> выбрать созданный AVD -> ▶️ **Run**, чтобы убедиться, что эмулятор запускается
Закрыть эмулятор -> PowerShell -> adb emu kill
##### **Этап 5. Установка Visual Studio Code**
###### **5.1. Скачивание и установка VS Code в D:\progi\src\VSCode**
https://code.visualstudio.com/ -> Download for Windows → VSCodeUserSetup-x64-1.102.3
Запустить установку -> Далее -> выбор папки установки: D:\progi\src\VSCode-> Далее -> Далее ->  ✅: Add to PATH, Register code as an editor for supported file types, Add "Open with Code" action to Windows Explorer -> далее -> установить -> завершить
###### **5.2. Проверка переменной среды**
cmd -> code --version -> 1.102.3
###### **5.3. Установка расширений Flutter и Dart**
запустить VS Code -> Extensions (`Ctrl+Shift+X`) -> ввести: Flutter -> Dart подтянется автоматически -> install
##### **Этап 6. Установка Flutter SDK**
###### **6.1. Скачать Flutter SDK (Windows, без установки через Android Studio)**
https://docs.flutter.dev/get-started/install/windows/mobile -> Download and install (ручная установка) => flutter_windows_3.22.1-stable.zip => распаковать в D:\progi\src\flutter
в системную переменную среды Path -> D:\progi\src\flutter\bin
Открыть VS Code → Terminal → New Terminal ->
flutter doctor --android-licenses => принять лицензии
**6.2.1. Проверка системных переменных среды**
echo $env:PATH => D:\progi\src\flutter\bin
**6.2.2. Запуск и анализ flutter doctor**
dart --version => Dart SDK version: 3.8.1
flutter doctor
	[√] Flutter (Channel stable) - путь Flutter установлен
	[√] Android toolchain - SDK найден, лицензии приняты
	[√] Android Studio (version 2024.3.2) - Обнаружен и указан путь
	[√] Connected device (3 available) - эмуляторы и физические устройства Flutter видит и распознаёт корректно (аналог: [√] VS Code, [√] AVD/эмулятор)
	[X] Visual Studio - develop Windows apps - пока не ставим так как не планируем делать Windows Desktop-приложения
##### **Этап 7. Проверка работы эмулятора AVD**
**7.1. Убедиться, что AVD создаётся в D:\progi\src\android_avd, а не в C:\Users\User\.android.**
PowerShell -> echo $Env:ANDROID_AVD_HOME => D:\progi\src\android_avd
**7.2. Создание AVD через Android Studio**
Запустить Android Studio -> откроется окно Welcome Android Studio -> More Actions → Device Manager -> + (Create Device) => окно Add Device -> выбрать Pixel 5 -> Next -> выбрать API 35 - Android 15.0 -> Finish => AVD должен быть создан в: :\progi\src\android_avd\.android\avd -> Finish
**7.3. Запуск и проверка**
- ✅ Вариант 1: GUI -> в Device Manager ▶️ — AVD запустится
- ✅ Вариант 2: CLI -> 
	- PowerShell -> cd "D:\progi\src\Android\Sdk\emulator"
	- PowerShell -> .\emulator.exe -list-avds => Medium_Phone_API_36.0, Pixel_5, Pixel_6 -> вернет имена эмуляторов
	- PowerShell -> .\emulator.exe -avd Pixel_6 -> запустит эмулятор Pixel_6
**7.4. Проверка во Flutter**
Git Bash → flutter devices => sdk gphone64 x86 64 (mobile) • emulator-5554 • android-x64 • Android 15 (API 35) (emulator) -> эмулятор создан, запущен, распознан Flutter как устройство, API 35 (Android 15) поддерживается и активен
##### 8. **Создание Flutter проекта в VS Code**
###### **8.1. Проверка flutter и VS Code**
Открыть VS Code -> Меню → Terminal → New Terminal -> flutter --version => не должно быть ошибок
###### **8.2. Инициализировать новый проект**
Перейти  в папку для проектов -> cd D:\wirt\project\flutter_projects
Создать проект test_app -> flutter create test_app
###### **8.3. Открыть проект в VS Code**
File → Open Folder → D:\wirt\project\flutter_projects\test_app
**Проверка Flutter Doctor** -> открыть терминал внутри проекта -> flutter doctor-> все пункты отмечены ✅
###### **8.4. Запуск проекта на эмуляторе**
- PowerShell -> cd "D:\progi\src\Android\Sdk\emulator"
- PowerShell -> .\emulator.exe -avd Pixel_6
###### **8.5. Запуск проекта на эмуляторе**
Git Bash → cd /d/wirt/project/flutter_projects/test_app
Git Bash → flutter run
на эмуляторе появится классическое синее приложение Flutter с кнопкой "+".
###### **8.6. Проверка успешной сборки**
**В терминале должно быть:**
Running Gradle task 'assembleDebug'...
Built build\app\outputs\flutter-apk\app-debug.apk.
Syncing files to device Android SDK built for x86...
**А на эмуляторе — работающее приложение**
