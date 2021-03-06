---
title: Функции marshmallow
description: Эта статья поможет вам приступить к использованию в с помощью Xamarin.Android для разработки приложений для Android 6.0 Marshmallow.
ms.prod: xamarin
ms.assetid: E4D6F183-98D2-460A-9D65-937639A899E0
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/01/2018
ms.openlocfilehash: d2150e18a377d61a2e79fabfc845f57cfab8a5c7
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="marshmallow-features"></a>Функции marshmallow

_Эта статья поможет вам приступить к использованию в с помощью Xamarin.Android для разработки приложений для Android 6.0 Marshmallow._

В этой статье приведен обзор новых возможностей в Android 6.0 Marshmallow, содержит сведения о подготовке Xamarin.Android для разработки приложений Android Marshmallow и содержит ссылки на примеры приложений, которые показывают, как использовать новый Android Marshmallow функции в Xamarin.Android приложений. 


## <a name="overview"></a>Обзор

[Android 6.0 Marshmallow](http://developer.android.com/about/versions/marshmallow/index.html), является Далее основных Android выпуске после Android без описания операций.
Xamarin.Android поддерживает Android Marshmallow и включает в себя:

-   **API 23/Android 6.0 привязок** &ndash; Android 6.0 добавляет многие новые API для включения новых возможностей, описанных ниже; эти API доступны для приложений Xamarin.Android, при ориентировании API уровня 23. Дополнительные сведения об интерфейсах API Android 6.0 см. в разделе [Android 6.0 API-интерфейсы](http://developer.android.com/preview/api-overview.html). 

[![Планшеты и телефоны под управлением Marshmallow героя изображения](marshmallow-images/android-m-hero-sml.png)](marshmallow-images/android-m-hero.png#lightbox)

Несмотря на то, что выпуск Marshmallow основном ориентирован на «польский и качества», также предоставляет множество новых функций, представляющие интерес для разработчиков Xamarin.Android. Эти функции включают перечисленные ниже. 

-   **Среда выполнения разрешения** &ndash; это улучшение позволяет пользователям утверждение разрешения безопасности на основе конкретном случае во время выполнения. 

-   **Улучшения проверки подлинности** &ndash; начиная с Android Marshmallow приложений теперь можно использовать датчики отпечатков пальцев для проверки подлинности пользователей, а новые *подтверждения учетных данных* компонентов минимизирует необходимость ввода пароли. 

-   **Связывание приложения** &ndash; эта возможность помогает избежать потребность **выбора приложения** всплывающее путем автоматического сопоставления приложений с веб-доменах. 

-   **Прямой общий ресурс** &ndash; можно определить *прямой конечные объекты папки* , чтобы сделать совместное использование быстрого и интуитивно понятный для пользователей, эта функция позволяет uers использовать содержимое совместно с другими приложениями. 

-   **Голосовая связь взаимодействий** &ndash; этот новый интерфейс API позволяет строить сетевого голосовых функций в веб-приложения. 

-   **Режим отображения 4 K** &ndash; в Android Marshmallow приложение может запросить разрешение экрана 4 КБ на оборудовании, которое ее поддерживает. 

-   **Новые возможности аудио** &ndash; начиная с Marshmallow Android теперь поддерживает протокол MIDI. Он также предоставляет новые классы для создания цифровой записи звука и объекты воспроизведения и предлагает новый API обработчики для связывания аудио-и ввода. 

-   **Новые возможности видео** &ndash; Marshmallow предоставляет новый класс, который позволяет приложениям обрабатывать потоки аудио и видео синхронизации; этот класс также поддерживает частоту динамического воспроизведения. 

-   **Android для работы** &ndash; Marshmallow включает расширенные элементы управления для устройств, принадлежащих организации, одного пользователя. Он поддерживает автоматическую установку и удаление приложений по владельцу устройства, принятие автоматического обновления системы, улучшенная сертификат управления, данных отслеживания использования, управление разрешениями и уведомления о состоянии рабочих. 

-   **Библиотека поддержки материала разработки** &ndash; новый *библиотека поддержки конструктора* предоставляет компоненты, разработки и шаблоны, которые упрощает построение внешний вид и поведение конструктора материал в веб-приложения. 

Кроме того большого количества обновлений библиотеки Android ядра были выпущены с Android M, и эти обновления предоставляет пользователям новые возможности для Android M и более ранних версиях Android.

Кроме того большого количества обновлений библиотеки Android ядра были выпущены с Android Marshmallow, и эти обновления предоставляет пользователям новые возможности для Android Marshmallow и более ранних версиях Android. В этой статье объясняется, как приступить к созданию приложений с Android Marshmallow и в нем представлены общие сведения о новой функции выделения в Android 6.0. 

## <a name="requirements"></a>Требования

Для использования новых возможностей Android Marshmallow приложения на основе Xamarin требуется следующее. 

-   **Xamarin.Android** &ndash; Xamarin.Android 5.1.7.12 или более поздней версии необходимо установить и настроить с помощью Visual Studio или Xamarin Studio.

-   **Visual Studio для Mac** или **Visual Studio** &ndash; Если вы используете Visual Studio для Mac версии 5.9.7.22 или более поздней версии. Если вы используете Visual Studio версии 3.11.1537 или более поздней версии средства Xamarin для Visual Studio не требуется. 

-   **Пакет SDK для Android** &ndash; Android 6.0 SDK (API 23) должен быть установлен через диспетчер Android SDK.

-   **Java Developer Kit** &ndash; требует Xamarin.Android [JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) или более поздней версии, если вы разрабатываете API уровня 24 или выше (JDK 1.8 также поддерживает API уровня до 24, включая Marshmallow). 64-разрядной версии JDK 1.8 является обязательным, если вы используете пользовательские элементы управления или средство предварительного просмотра формы.

Можно продолжать использовать [JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) при разработке специально для API уровня 23 или более ранней версии. 


## <a name="getting-started"></a>Начало работы

Чтобы начать работу с Android Marshmallow с Xamarin.Android, необходимо загрузить и установить новейшие средства и пакеты SDK, прежде чем создавать проект Android Marshmallow: 

1.  Установите последние обновления из Xamarin **стабильный** канала. 

2.  Установка средств и пакетов Android 6.0 Marshmallow SDK.

3.  Создайте новый проект Xamarin.Android, предназначенное Android 6.0 Marshmallow (API уровня 23). 

4.  Настройка для Android Marshmallow эмуляторе или устройстве.

Каждое из этих действий описан в следующих разделах:


### <a name="install-xamarin-updates"></a>Установка обновлений для Xamarin

Чтобы обновить Xamarin таким образом, чтобы она включает поддержку Android 6.0 Marshmallow, измените канал обновления для **стабильный** и установить все обновления. Дополнительные сведения об установке обновлений в канале обновлений см. в разделе [смены каналов обновления](https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/). 


### <a name="install-the-android-60-sdk"></a>Установка пакета SDK для Android версии 6.0

Создание проекта Xamarin.Android для Android Marshmallow, сначала необходимо использовать диспетчер Android SDK Manager для установки пакета SDK для Android 6.0:

-   Запустите диспетчер Android SDK (в Visual Studio для Mac с помощью **Сервис > Диспетчер пакетов SDK**; в Visual Studio, используйте **средства > Android > Диспетчер Android SDK Manager**) и установите последний пакет инструментов SDK Android:

    [![При выборе средства пакета SDK для Android в диспетчер Android SDK](marshmallow-images/mnc-preview-tools.png)](marshmallow-images/mnc-preview-tools.png#lightbox)

-   Кроме того, установите последнюю версию **Android 6.0** пакетами SDK:

    [![При выборе пакета SDK для Android 6.0 пакетов в диспетчере Android SDK](marshmallow-images/mnc-preview-packages.png)](marshmallow-images/mnc-preview-packages.png#lightbox)

Необходимо установить пакет инструментов SDK Android версии 24.3.4 или более поздней версии.
Дополнительные сведения об использовании диспетчер Android SDK Manager для установки пакета SDK для Android 6.0 см. в разделе [диспетчер пакетов SDK](http://developer.android.com/tools/help/sdk-manager.html).



### <a name="start-a-xamarinandroid-project"></a>Запуск проекта Xamarin.Android

Создание нового проекта Xamarin.Android. Если вы не знакомы с разработки приложений Android с помощью Xamarin, см. раздел [Привет, Android](~/android/get-started/hello-android/index.md) Дополнительные сведения о создании проектов Android. 

При создании проекта Android, необходимо настроить параметры версии целевой объект Android 6.0 MarshMallow. Чтобы выбрать проект для Marshmallow, необходимо настроить проект для **API уровня 23 (версии 6.0 Xamarin.Android поддержки)**. Дополнительные сведения о настройке Android API уровня уровней см. в разделе [основные сведения об уровнях Android API](~/android/app-fundamentals/android-api-levels.md).



### <a name="configure-an-emulator-or-device"></a>Настройка эмулятора или устройства

Если вы используете эмулятор, запустите диспетчер AVD Android и создать новое устройство, используя следующие параметры:

-   Устройство: Nexus, 5, 6 или 9.
-   Целевая платформа: Android 6.0 - API уровня 23
-   ABI: x86

Например это виртуальное устройство настраивается для эмуляции 5 хранилища:

[![Настройка с помощью Nexus 5 устройств, целевой объект Android 6.0 и Intel Atom (x86) AVD](marshmallow-images/android-m-avd.png)](marshmallow-images/android-m-avd.png#lightbox)

Если вы используете физического устройства, например, 5 хранилища, 6 или 9, можно установить изображение Android Marshmallow. Дополнительные сведения об обновлении устройства для Android Marshmallow см. в разделе [образы оборудования системы](http://developer.android.com/preview/download.html#images).



## <a name="new-features"></a>Новые функции

Многие изменения, появившиеся в Android Marshmallow уделено повышения удобства работы пользователя для Android, что повышает производительность и исправлении ошибок. Однако Marshmallow также представлены некоторые существенные изменения в основы платформы Android. В следующих разделах, выделите эти усовершенствования и предоставляют ссылки, которые помогут вам приступить к работе с помощью новых функций Android Marshmallow в вашем приложении. 



### <a name="runtime-permissions"></a>Разрешения среды выполнения

Система Android разрешений значительно оптимизирован и упрощенный с момента Android без описания операций. В Android Marshmallow пользователям предоставлять разрешения на основе конкретном случае во время выполнения, а не во время установки. Для поддержки этой возможности на Android Marshmallow и более поздних версий, разработать приложение будет запрашивать у пользователя разрешения во время выполнения (в контексте, для которых необходимы разрешения). Это изменение облегчает пользователям запускать приложения с помощью немедленно, поскольку он упрощает процесс установки и обновления приложения. 

В разделе [запрос разрешений среды выполнения в Android Marshmallow](https://blog.xamarin.com/requesting-runtime-permissions-in-android-marshmallow/) Дополнительные сведения (в том числе примеры кода) о реализации в приложениях Xamarin.Android разрешения среды выполнения.
Xamarin предоставляет также пример приложения, демонстрирующий принцип работы разрешений на время выполнения в Android Marshmallow (и более поздние версии): [RuntimePermissions](https://developer.xamarin.com/samples/monodroid/android-m/RuntimePermissions).

Этот образец приложения демонстрирует следующее:

-   Как проверить и запросить разрешения во время выполнения.
-   Как объявить разрешения для устройств Android M.

Чтобы использовать этот пример приложения:

1.  Коснитесь **камеры** или **контактов** кнопки, отображаемые для разрешений на доступ запроса диалогового окна.
2.  Предоставьте разрешение на просмотр камеры или контактов фрагментов.

Дополнительные сведения о новых возможностях разрешения среды выполнения в Android Marshmallow см. в разделе [работа с разрешениями системы](https://developer.android.com/preview/features/runtime-permissions.html).



### <a name="authentication-enhancements"></a>Улучшения проверки подлинности

Android Marshmallow включает два улучшениями процесса проверки подлинности, которые помогают устранить потребность в паролей:

-   **Отпечаток пальца проверки подлинности** &ndash; использует сканирования отпечатков пальцев для проверки подлинности пользователей.

-   **Подтвердить учетные данные** &ndash; выполняет проверку подлинности пользователей, в зависимости от того, как долго устройства разблокирован.

Ссылки и примеров приложений, описанным ниже могут помочь становятся привычную эти новые возможности.


#### <a name="fingerprint-authentication"></a>Проверка подлинности отпечатков пальцев

На устройствах, поддерживающих отпечатков пальцев проверку оборудования, можно использовать новый `FingerPrintManager` класс для проверки подлинности пользователя.
Дополнительные сведения о функции проверки подлинности отпечатков пальцев в Android Marshmallow см. в разделе [проверки подлинности отпечатков пальцев](https://developer.android.com/preview/api-overview.html#fingerprint-authentication).

Xamarin предоставляет образец приложения, демонстрирующий способ использования зарегистрированных отпечатки для проверки подлинности пользователя в приложении: [FingerprintDialog](https://developer.xamarin.com/samples/monodroid/android-m/FingerprintDialog).

Чтобы использовать этот пример приложения:

1.  Touch **покупки** кнопку, чтобы открыть диалоговое окно проверки подлинности отпечатков пальцев.
2.  Сканировать отпечатка пальца зарегистрированного пользователя для проверки подлинности.

Обратите внимание, что приложение из этого примера требуется устройством чтения отпечатков пальцев.
Это приложение не сохраняет отпечатками пальцев (или пароль).



#### <a name="voice-interactions"></a>Взаимодействие голоса

Новая возможность взаимодействия голоса в Android Marshmallow пользователи приложения для использования голоса для подтверждения действия и выберите из списка параметров. Дополнительные сведения о голосовых взаимодействий см. в разделе [Обзор интерфейса API взаимодействия голосовых](https://developers.google.com/voice-actions/interaction/). 

В разделе [добавьте диалога приложение Android с взаимодействиями голосовых](https://blog.xamarin.com/add-a-conversation-to-your-android-app-with-voice-interactions/) Дополнительные сведения (в том числе примеры кода) о реализации взаимодействия голоса в приложениях Xamarin.Android.
Пример приложения доступен, показано, как использовать API взаимодействия голоса в приложении Xamarin.Android: [голоса взаимодействия](https://github.com/jamesmontemagno/MarshmallowSamples/tree/master/VoiceInteractions).



#### <a name="confirm-credential"></a>Подтверждение учетных данных

С помощью нового *подтверждения учетных данных* компонентов из Android Marshmallow, можно освободить пользователей от необходимости запоминать и введите пароли для отдельных приложений путем проверки подлинности их в зависимости от того, как долго устройства разблокирован.
Чтобы сделать это, можно использовать новый `SetUserAuthenticationValidityDurationSeconds` метод `KeyGenerator`. Используйте `KeyGuardManager` `CreateConfirmDeviceCredentialIntent` метод повторно пройти проверку подлинности пользователя в приложении. Дополнительные сведения об этой новой функции в Android Marshmallow см. в разделе [подтверждения учетных данных](https://developer.android.com/preview/api-overview.html#confirm-credential).

Xamarin предоставляет образец приложения, демонстрирующий использование учетных данных устройства (например, ПИН-код, шаблон или пароль) в приложении: [ConfirmCredential](https://developer.xamarin.com/samples/monodroid/android-m/ConfirmCredential/)

Чтобы использовать этот пример приложения:

1.  Настройка экрана блокировки безопасности на устройстве (**Secure > Безопасность > Screenlock**).
2.  Коснитесь **покупки** кнопку и подтвердите экран блокировки безопасности учетных данных.



### <a name="chrome-custom-tabs"></a>Пользовательские вкладки Chrome

Разработчикам приложений приходится выбор, когда пользователь касается URL-адрес: приложение можно запустить браузер или с помощью браузера в приложении на основе `WebView`. Оба варианта связана с проблемами &ndash; запуском обозревателя является переключение контекста большого объема, не настраиваемые при `WebView`s поддерживают состояние с помощью браузера. Кроме того, использование `WebView`s можно добавить дополнительные затраты. 

*Хром пользовательских вкладок* дает возможность простого и эффективного отображения веб-сайтов с помощью Chrome без необходимости оставьте приложение пользователям. Эта функция дает приложения больший контроль над веб-интерфейс пользователя; берет на себя переходы между машинный код и веб-содержимого более прозрачную без приходится прибегать к `WebView`. Приложения могут также влиять на Chrome отображения и работы, настроив следующие: 

-   Цвет панели инструментов

-   Открыть или закрыть анимацию

-   Пользовательские действия в меню панели инструментов и переполнения Chrome

-   Перед запуском Chrome и содержимое упреждающую выборку (для загрузки быстрее)

Чтобы воспользоваться преимуществами этой функции в вашем приложении Xamarin.Android, загрузите и установите [Android поддержки пользовательских вкладок библиотеки](https://www.nuget.org/packages/Xamarin.Android.Support.CustomTabs/).
Дополнительные сведения об этой функции см. в разделе [Chrome пользовательских вкладок](https://developer.chrome.com/multidevice/android/customtabs).



### <a name="material-design-support-library"></a>Библиотека поддержки материала разработки

Android без описания операций появились [разработки материал](http://www.google.com/design/spec/material-design/introduction.html) как новый язык разработки для обновления взаимодействие с Android (см. [темы материал](~/android/user-interface/material-theme.md) сведения об использовании конструктора материалов в приложениях Xamarin.Android). С Android Marshmallow появился Google *библиотеку поддержки Android разработки* для упрощения приложения разработчики могут применять материал разработать внешний вид и поведение. Эта библиотека включает следующие компоненты:

-   **CoordinatorLayout** &ndash; новый `CoordinatorLayout` мини-приложение, аналогично, но эффективнее, чем `FrameLayout`. Можно использовать `CoordinatorLayout` как контейнер для дочерних представлений или как макета верхнего уровня, который предоставляет `layout_anchor` атрибут, который может использоваться для представления привязки относительно других представлений.

-   **Свертывание панели инструментов** &ndash; новый `CollapsingToolbarLayout` является свертывания панель приложения, который является оболочкой для `Toolbar`. (Обратите внимание, что *панель приложения* является то, что ранее назывался *панель действий*.)

-   **Кнопка с плавающей** &ndash; round кнопки, которая обозначает главное действие на интерфейсе приложения.

-   **С плавающей запятой метки для редактирования текста** &ndash; использует новый `TextInputLayout` мини-приложения (который является оболочкой для `EditText`) Показать метку с плавающей запятой, если указание будет скрыт, если пользователь вводит текст.

-   **Представления навигации** &ndash; новый `NavigationView` мини-приложение дает возможность использовать лоток навигации в виде, проще для перехода.

-   **Snackbar** &ndash; новый `SnackBar` мини-приложения — это упрощенный отзыв механизм (аналогично всплывающее уведомление), отображаются краткие сообщения в нижней части экрана появляется над всеми другими элементами на экране.

-   **Существенные вкладки** &ndash; новый `TabLayout` мини-приложения предоставляет горизонтальное расположение для отображение вкладок как способ реализации навигации верхнего уровня в приложении.

Чтобы воспользоваться преимуществами [библиотека поддержки конструктора](http://developer.android.com/tools/support-library/features.html#design) в своем приложении Xamarin.Android, загрузите и установите Xamarin [разработке библиотеки поддержки Xamarin](https://www.nuget.org/packages/Xamarin.Android.Support.Design/) пакет NuGet.

В разделе [привлекательных материал разработки с Android библиотека конструктора поддержки](https://blog.xamarin.com/add-beautiful-material-design-with-the-android-support-design-library/) Дополнительные сведения (в том числе примеры кода) с помощью библиотеки поддержки конструктора материал в Xamarin.Android приложениях.
Xamarin предоставляет пример приложения, который демонстрирует новую библиотеку Android разработки на Xamarin.Android &ndash; [Cheesesquare](https://developer.xamarin.com/samples/monodroid/android5.0/Cheesesquare).
Этот образец демонстрирует следующие функции библиотеки конструктора:


-   Свертывание панели инструментов
-   С плавающей запятой Управляющая кнопка
-   Закрепление представления
-   NavigationView
-   Snackbar

Дополнительные сведения о библиотеке разработки см. в разделе [библиотеку поддержки Android разработки](http://android-developers.blogspot.co.at/2015/05/android-design-support-library.html) в блоге разработчика Android.


### <a name="additional-library-updates"></a>Дополнительные библиотеки обновлений

В дополнение к Android Marshmallow Google объявила связанных обновлений на несколько основных библиотек Android. Xamarin предоставляет Xamarin.Android поддержку для этих обновлений через несколько пакетов NuGet предварительной версии: 

-   [Службы Google Play](https://www.nuget.org/packages?q=Xamarin+Google+Play+Services) &ndash; последнюю версию службы Google Play включает новый *приглашает приложения* функции, которая позволяет пользователям совместно использовать свои приложения с друзьями. Дополнительные сведения об этой функции см. в разделе [Reach разверните приложения с Google App приглашает](http://blog.xamarin.com/expand-your-apps-reach-with-googles-app-invites/). 

-   [Android библиотеки поддержки](https://www.nuget.org/packages?q=xamarin+support+library) &ndash; эти NuGets предоставляют возможности, доступные только для библиотеки API-интерфейсы, обеспечивая обратную совместимость версий API-интерфейсы платформы Android. 

-   [Библиотека Android переносном](https://www.nuget.org/packages/Xamarin.Android.Wear) &ndash; это NuGet включает привязок службы Google Play. Последнюю версию библиотеки переносном добавляет новые функции, (включая упрощения навигации для пользовательских приложений) на платформу с Android. 


## <a name="summary"></a>Сводка

В этой статье представлена Android Marshmallow и описано, как установить и настроить новейшие средства и пакеты для разработки Xamarin.Android на Marshmallow. Оно также предоставляет обзор наиболее важных новых функций, Android Marshmallow Xamarin.Android разработки.


## <a name="related-links"></a>Связанные ссылки

- [Android 6.0 Marshmallow](http://developer.android.com/about/versions/marshmallow/index.html)
- [Получение пакета SDK для Android](https://developer.android.com/sdk/index.html#Other)
- [Обзор возможностей](https://developer.android.com/preview/api-overview.html)
- [Заметки о выпуске](https://developer.xamarin.com/releases/android/xamarin.android_5/xamarin.android_5.1.99/)
- [RuntimePermissions (пример)](https://developer.xamarin.com/samples/monodroid/android-m/RuntimePermissions)
- [ConfirmCredential (пример)](https://developer.xamarin.com/samples/monodroid/android-m/ConfirmCredential)
- [FingerprintDialog (пример)](https://developer.xamarin.com/samples/monodroid/android-m/FingerprintDialog)
