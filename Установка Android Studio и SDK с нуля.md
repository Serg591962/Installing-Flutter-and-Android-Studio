За исходные прими следующее установки
- ОС: Windows 10 Pro
- Python: D:\Python\Python3_13_4
- Каталог установки всего ПО: D:\progi\src
- Git установлен 
- Open JDK  не установлен
- Flutter SDK не установлен
- Домашний каталог всех эмуляторов AVD должен быть - D:\wirt\project\flutter_projects\android_avd
##### **Этап 1. Установка Android Studio**
###### **1.1. Скачивание и установка Android Studio**
Перейди на сайт: https://developer.android.com/studio    
Нажми Download Android Studio и скачай установщик.
Запуск установки => окно Welcome to Android Studio Setup -> оставь галочки на Android SDK, Virtual Device -> Next  -> окно Android Studio Setup -> установить путь: D:\progi\src\android-studio -> Next -> Next -> install  -> Next -> Finish
Запуск Android Studio => окно Welcome Android Studio -> Next -> окно Instal Type
Custom -> 
- Установить путь: D:\progi\src\Android\Sdk
- Убедись, что выбрано:
    - ✅ Android SDK    
    - ✅ Android Virtual Device   
    - ✅ Performance (если будет)
Next -> Next -> Acept -> Finish
###### **1.2. Первичная настройка SDK**
Запуск Android Studio => окно Welcome Android Studio -> More Actions → SDK Manager
На вкладке **SDK Platforms**: -> Поставь галочку на: Android 14.0 (API 34), Android 13.0 (API 33)
Нажми: Show Package Details -> Для каждого API выбери: Android SDK Platform,  Sources for Android, Google APIs Intel x86_64 Atom System Image
Перейди на вкладку SDK Tools: ->Убедись, что выбрано: Android SDK Build-Tools, Android Emulator, Android SDK Command-line Tools (latest), Android SDK Platform-Tools -> Включи "Hide Obsolete Packages" -> Neht
Нажми Apply → OK → прими все лицензии → дождись установки.
###### **1.3. Настройка папки AVD**
Создай папку под AVD: - D:\wirt\project\flutter_projects\android_avd
Назначить папку как домашнюю директорию для AVD:
	- ANDROID_AVD_HOME
	- D:\wirt\project\flutter_projects\android_avd
Проверить настройку CMD -> echo %ANDROID_AVD_HOME% -> D:\wirt\project\flutter_projects\android_avd
###### **1.4. Установка OpenJDK**
- Установлена penJDK 17
	- скачать с https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.10%2B7/OpenJDK17U-jdk_x64_windows_hotspot_17.0.10_7.zip -> OpenJDK17U-jdk_x64_windows_hotspot_17.0.10_7.zip
	- установи D:\progi\src\OpenJDK\jdk-17
	- Открыть "Переменные среды"
		- Имя: JAVA_HOME - значение: "D:\progi\src\OpenJDK\jdk-17"
		- `Path`: - значение "%JAVA_HOME%\bin
	- Проверка:
		- CMD java -version -> openjdk version "17.0.10" 2024-01-16
		- CMD echo %JAVA_HOME% -> D:\progi\src\OpenJDK\jdk-17
###### **1.5. Установка вручную нужного образа эмулятора Android 14 API 34 (x86_64).**
cmd -> cd /d D:\progi\src\Android\Sdk\cmdline-tools\latest\bin
sdkmanager.bat "system-images;android-34;google_apis;x86_64"
**Удаление лишних:** 
- sdkmanager.bat --uninstall "sources;android-33" 
- sdkmanager.bat --uninstall "platforms;android-33"
- sdkmanager.bat --uninstall "system-images;android-33;..."
- если удалить не получилось удалить вручную папку D:\progi\src\Android\Sdk\platforms\android-33
**Проверить, что нужный образ установлен успешно:**
1. **способ**
	- cmd -> cd /d D:\progi\src\Android\Sdk\cmdline-tools\latest\bin -> sdkmanager.bat --list
	- в разделе Installed packages найти system-images;android-34;google_apis;x86_64 -> если он там -> образ установлен правильно.
2. **способ**
	- открыть D:\progi\src\Android\Sdk\system-images\android-34\google_apis\x86_64
	- В этой папке должны быть: system.img, package.xml, build.prop
###### **1.6. Установка Flutter SDK**
**Скачивание Flutter SDK**
1. Перейти на: `[https://docs.flutter.dev/get-started/install/windows]` 
2. Скачать `.zip` архив (например `flutter_windows_3.x.x-stable.zip`)
3. Распаковать в D:/progi/src/flutter
4. Добавить в системную переменную в PATH  →  D:\progi\src\flutter\bin
	- в окно поиск ввести команду systempropertiesadvanced → "Запуск от имени администратора"
	- "Переменные среды..." -> В секции «Системные переменные» найди `Path` → «Изменить»
	- Нажми «Создать» → добавь: D:\progi\src\flutter -> «ОК» → «ОК»
**Проверка установки Flutter****
5. Проверка переменной PATH
Git Bash → echo $PATH → в выводе должен быть путь: /d/progi/src/flutter/bin
6. Проверка Flutter в Git Bash
Git Bash → flutter --version → Flutter 3.32.4 • channel stable • ...
7. Проверка окружения разработчика Flutter: установлены ли все необходимые инструменты (SDK, IDE, эмуляторы и т.п.).Flutter в CMD**
Git Bash → flutter doctor  → √ Flutter (Channel stable
Расшифровка символов
✓ - Всё отлично, компонент установлен, настроен и работает
 ! -  Компонент установлен частично или необязателен, но рекомендуется
✗ - Компонент отсутствует или сломан, Flutter не сможет работать без него
###### **1.7. Принять лицензии Android SDK**
Git Bach -> flutter doctor --android-licenses => запрашивает согласие -> Y
Git Bach -> flutter doctor => [√] Android toolchain - develop for Android devices (Android SDK version 36.0.0)
###### **1.8. Проверка готовности к созданию AVD и запуску Flutter-проекта**
Git Bach -> flutter doctor => [√] все позиции
##### **Этап 2. Создание AVD и запуск Flutter-проекта**
###### **2.1. Первая инициализация IDE**
Запуск Android Studio -> окно Missing SDK с записью No Android SDK Found -> Neht
Откроется окно SDK Components Setup -> Поле Android SDK Location -> D:\progi\src\Android\Sdk, все галочки отключить -> Next → Finish → Finish
###### **2.2. Создание AVD (эмулятора)**
Запуск Android Studio -> окно Welkome to  Android Studio -> More Actions → Virtual Device Manager => открывается экран Device Manager -> ➕ -> Create virtual device
Install Android Emulator Hypervisor Driver -> Next → Finish
**Проверить включена ли виртуализация в BIOS:**
Пуск → Параметры → Обновление и безопасность → Восстановление -> В разделе Особые варианты загрузки -> Перезагрузить сейчас
После синего экрана: Диагностика → Дополнительные параметры → Параметры встроенного ПО UEFI → Перезагрузить
После входа в BIOS -> Перейди в Security → Virtualization
- Intel (R) VT-x → Enabled
- Также включи: VT-d (если есть)
Сохрани: F10 → Yes
**Включить компоненты Windows:**
PowerShell от администратора -> dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /all => Операция успешно завершена.
Запуск Android Studio -> окно Welkome to  Android Studio -> More Actions → Virtual Device Manager => открывается экран Device Manager -> ➕ -> Create virtual device
Pixel 6 Pro -> Next
Окно Configure virtual device -> выбрать name -> first, api 34 а в окне Services, Google Apls то в окне System Image,  Google APIs Intel x86_64 Atom System Image в  окне System Image -> Finish => загрузка => окно Device manager с эмулятором (виртуальным устройством first)
###### **2.3. Установка плагинов Flutter и Dart в Android Studio**
Запуск Android Studio -> окно Welkome to  Android Studio -> Plugins -> Marketplace
В поле поиска вверху ввести **flutter** => Найти плагин Flutter -> instal => активируется кнопка Restart IDE
В поле поиска вверху ввести **dart** => Найти плагин Dart -> instal -> Найти плагин Flutter -> Restart IDE=> Android Studio перезагрузится
Plugins -> Marketplace -> проверить что Flatter и Dart установлены
Git Bach -> flutter doctor => [√] Flutter (Channel stable, 3.32.7, on Microsoft Windows [Version
    10.0.19045.6093], locale ru-RU)
**Указать путь к Flutter SDK.** 
Этот путь Android Studio сохраняет **внутри себя**, и его надо _один раз_ правильно указать.
Settings → Languages & Frameworks есть раздел Flutter — значит, путь к SDK сохранён.
Если нет:
- Welcome Screen → **New Flutter Project**
- Выбрать flatter -> В поле **Flutter SDK Path** укажи: D:\progi\src\flutter→ Next 
- Введи **project name**: flutter_first → Next
- В появившемся окне:
	- Project type: **Flutter Application**
    - Flutter SDK path: D:\progi\src\flutter
    - `Project name`: flutter_first
    - `Project location`: D:\wirt\flutter_projects\flutter_first
    - `Description`: по желанию
    - `Organization`: com.example
    - `Android language`: **Kotlin**
    - `Platforms`: включи все галочки
    - `Create project offline`: ❌ НЕ включать
- Create
- Проверить снова:  Android Studio → File → Settings -> Languages & Frameworks → Flutter
Убедится, что Dart SDK найден: Android Studio → File → Settings -> Languages & Frameworks → Dart 
Удалить временный проект (если хочешь)
- Удалить папку flutter_test_temp -> D:\wirt\flutter_projects\flutter_test_temp
- C:\Users\PC\AppData\Roaming\Google\AndroidStudio2025.1.1\options
- Удалить строку `<entry key="...flutter_test_temp"`... из recentProjects.xml, если хочешь убрать из списка.
- **Нельзя просто нажать Cancel.** Путь к Flutter SDK сохраняется только при создании проекта, если он проходит проверку. Кнопка Cancel обнуляет всё.Создание и запуск первого Flutter-проекта**
###### **2.4. Запуск AVD (эмулятора)**
Запуск Android Studio -> окно Welkome to  Android Studio -> открыть проект flutter_first -> верхнее меню → **Tools → Device Manager**
Найти AVD  (например, Pixel 6 Pro API 34) -> Нажать кнопку ▶ рядом с нужным устройством
=> эмулятор загрузится (появится рабочий стол Android)
###### **2.5. Запуск проекта Flutter на эмуляторе**
выбрать устройство эмулятора: справа Pixel_6_Pro_API_34 -> слева выбери Pixel 6 Pro mobile -> ▶ Run main.dart => на экране эмулятора появится стандартное Flutter-приложение:
- С заголовком: Flutter Demo Home Page
- С текстом: You have pushed the button this many times:
- Кнопкой + внизу справа
##### **Этап 3. Настройка VC code  для разработки в flutter приложении**
###### **3.1. Запуск VS Code**
Через ярлык в меню пуск
###### **3.2. Установить плагины  Flutter, Dart, Material Icon Theme.**
В левом меню нажать иконку квадратика с четырьмя гранями (Extensions) -> в строке поиска (Material Icon Theme) -> Install => После установки появится кнопка "Set File Icon Theme" (“Установить тему иконок”) -> нажать -> в поле выше выбрать Material Icon Theme
###### **3.3. Установка нового проекта**
Ctrl + Shift + P → Flutter: New Project -> Выбрать Flutter Application -> Указать путь: D:\wirt\project\flutter_projects -> ввести имя нового проекта - hello_flutter -> Enter =>
рабочее окно с файлом `main.dart`, кнопками устройств внизу и возможностью запускать проект.
**Запуск проекта.**
Menu -> Run -> Start Debugging (F5) => должно появится окно выбора эмулятора -> выбираем Pixel_6_Pro (android-x64 emulator) 











Проверка наличия эмулятора AVD (ANDROID_AVD_HOME = D:\android_avd)**
Git Bach -> flutter emulators -> Pixel_6_Pro • Pixel 6 Pro • Google • android
###### **3.2. Запуск эмулятора из PowerShell в VS Code**
**Запуск VS Code**
**Открыть папку с Flutter-проектом**
- File (Файл) → перейти к проекту D:\wirt\project\flutter_projects\flutter_first -> Open Folder



Ctrl + Shift + P → Flutter: New Project

Выбери Application

Укажи путь, например:

makefile
Копировать
Редактировать
D:\wirt\project\flutter_projects\first_app
Дождись создания проекта

▶️ ШАГ 6. ЗАПУСК НА ЭМУЛЯТОРЕ
Выбери устройство снизу слева (например, Pixel_6_API_34)

Нажми F5 или Run → Start Debugging

Приложение запустится на Android эмуляторе

✅ РЕЗУЛЬТАТ
Компонент	Состояние
AVD создан и виден	✅
Flutter SDK настроен	✅
VS Code настроен	✅
Запуск приложения	✅ через F5

Готов выдать команду на создание первого проекта с конкретным путём и примером, если нужно — подтвердите.

**Проверка текущих AVD**
D:\progi\src\Android\Sdk\cmdline-tools\latest\bin\avdmanager.bat list avd

 **Удаление всех AVD**
 