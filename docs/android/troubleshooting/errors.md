---
title: Матрица Xamarin.Android ошибок
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 7EBE4C01-8EFC-4B7E-97BA-D879994F59AB
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/13/2018
ms.openlocfilehash: e9916d8e264c202a914e6fd70e664beea276e93d
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="xamarinandroid-errors-matrix"></a>Матрица Xamarin.Android ошибок

## <a name="errors-reference"></a>Справочник ошибок

Этот документ содержит некоторые сведения о различных кодах ошибок из Xamarin.

|Категория|Описание|
|--- |--- |
|XA0xxx|mandroid ошибки|
|XA1xxx|Копирование файла или символических ссылок (проект связанные) ошибок|
|XA2xxx|Ошибки компоновщика|
|XA3xxx|Ошибки AOT|
|XA4xxx|Ошибки создания кода|
|XA5xxx|GCC и инструментов ошибки|
|XA6xxx|ошибки mandroid внутренние средства|
|XA7xxx|Зарезервированное|
|XA8xxx|Зарезервированное|
|XA9xxx|Ошибок лицензирования|


## <a name="error-codes"></a>Коды ошибок

### <a name="xa0xxx-errors"></a>Ошибки XA0xxx

|Код ошибки|Описание|
|--- |--- |
|XA0000|Непредвиденная ошибка - заполните [отчет ошибок](http://bugzilla.xamarin.com).|
|XA0001|"-devname предоставлен без вмешательства конкретного устройства.|
|XA0002|Не удалось выполнить синтаксический анализ переменной среды «{0}».|
|XA0003|Имя приложения «{0} .exe» конфликтует с именем сборки (DLL) пакета SDK или продукта.|
|XA0004|Новая логика refcounting требует sgen слишком включения.|
|XA0005|Выходной каталог «{0}» не существует.|
|XA0006|Ни одна платформа devel на «{0}», использовать--платформы = PLAT, чтобы указать пакет SDK|
|XA0007|Корневой сборки «{0}» не существует.|
|XA0008|Можно указать только один корневой сборки.|
|XA0009|Произошла ошибка при загрузке сборки: {0}.|
|XA0010|Не удалось выполнить синтаксический анализ аргументов командной строки: {0}.|
|XA0011|{0} была создана на основе последней среды выполнения ({1}) не поддерживает MonoTouch.|
|XA0012|Неполные данные предоставляются для завершения «{0}».|
|XA0013|Для профилирования поддержки требуется sgen слишком включения.|
|XA0014|операций ввода-вывода {0} не поддерживает создание приложений, предназначенных для ARMv6.|
|XA0020|Не удалось определить путь mandroid.|
|XA0100|EmbeddedNativeLibrary «{0}» является недопустимым в проект приложения Android. Вместо этого используйте AndroidNativeLibrary.|

### <a name="xa1xxx-errors"></a>XA1xxx Errors

|Код ошибки|Описание|
|--- |--- |
|XA1001|Не удалось найти приложение в указанном каталоге.|
|XA1002|Не удалось создать символьных ссылок, скопированные файлы.|
|XA1003|Не удалось завершить приложения «{0}». Может потребоваться вручную завершить приложение.|
|XA1004|Не удалось получить список установленных приложений.|
|XA1005|Не удалось завершить приложение «{0}» на устройстве «{1}»: {2}. Может потребоваться вручную завершить приложение.|
|XA1006|Не удалось установить приложение «{0}» на устройстве «{1}»: {2}.|
|XA1007|Не удается запустить приложение «{0}» на устройстве «{1}»: {2}. Приложение по-прежнему можно запустить вручную, нажав на нем.|
|XA1008|Не удается запустить имитатор: {0}.|
|XA1009|Не удалось скопировать сборку «{0}» к «{1}»: {2}.|
|XA1010|Не удалось загрузить сборку «{0}»: {1}.|
|XA1011|Не удалось добавить отсутствующий файл ресурсов: «{0}».|
|XA1101|Не удалось запустить приложение.|
|XA1102|Не удалось присоединить к приложению (kill его): {0}.|
|XA1103|Не удалось отсоединить.|
|XA1104|Сбой при отправке пакета: {0}.|
|XA1105|Тип неожиданный ответ.|
|XA1106|Не удалось получить список приложений на устройстве: Истекло время ожидания запроса.|
|XA1107|Не удается запустить приложение.|
|XA1201|Не удалось загрузить имитатор: {0}.|
|XA1301|Собственная библиотека ({1}) «{0}» был пропущен, так как он не соответствует текущей сборки architecture(s) ({2}).|

### <a name="xa2xxx-errors"></a>XA2xxx Errors

|Код ошибки|Описание|
|--- |--- |
|XA2001|Не удалось связать сборки.|
|XA2002|Не удается разрешить ссылку: {0}.|
|XA2003|Параметр «{0}» будет игнорироваться, так как компоновка отключена.|
|XA2004|Не удалось найти файл определения дополнительных компоновщика «{0}».|
|XA2005|Не удалось выполнить синтаксический анализ определения из «{0}».|
|XA2006|Не удалось разрешить ссылку на элемент метаданных (определенное в «{1}») «{0}» из «{2}».|

### <a name="xa3xxx-errors"></a>XA3xxx Errors

Это AOT ошибок.

|Код ошибки|Описание|
|--- |--- |
|XA3001|Удалось AOT сборки «{0}».|
|XA3002|Ограничение AOT: метод «{0}» должен быть статическим, так как он объявлен с [MonoPInvokeCallback].|
|XA3003|Конфликтующие--параметры отладки и--llvm. Отладка программной отключена.|


### <a name="xa4xxx-errors"></a>XA4xxx Errors

Это ошибки создания кода.

|Код ошибки|Описание|
|--- |--- |
|XA4001|Основной шаблон не может быть expansed для «{0}».|
|XA4101|Регистратор не удалось создать подпись для типа «{0}».|
|XA4102|Регистратор найден недопустимый тип «{0}» в сигнатуре метода «{2}». Вместо этого используйте «{1}».|
|XA4103|Регистратор найден недопустимый тип «{0}» в сигнатуре метода «{2}»: тип реализует INativeObject, но не имеет конструктора, который принимает два (IntPtr bool) аргументов.|
|XA4104|Регистратор не может маршалировать возвращаемое значение для типа «{0}» в сигнатуре метода «{1}».|
|XA4105|Регистратор не может маршалировать параметр типа «{0}» в сигнатуре метода «{1}».|
|XA4106|Регистратор не может маршалировать возвращаемое значение для структуры «{0}» в сигнатуре метода «{1}».|
|XA4107|Регистратор не может маршалировать параметр типа «{0}» в сигнатуре метода «{1}».|
|XA4108|Регистратор не удается получить тип ObjectiveC для управляемого типа «{0}».|
|XA4109|Не удалось скомпилировать код созданный регистратора. Отправьте [отчет ошибок](http://bugzilla.xamarin.com).|
|XA4110|Регистратор не может маршалировать выходной параметр типа «{0}» в сигнатуре метода «{1}».|
|XA4111|Регистратор не удалось создать подпись для типа «{0}» в методе «{1}».|
|XA4200|ACW можно создавать только для типов «claas».|
|XA4201|Не удалось определить имя JNI для типа {0}.|
|XA4203|Указанное имя типа должно быть полным.|
|XA4204|Не удалось разрешить тип интерфейса «{0}». Отсутствует ссылка на сборку?|
|XA4205|[ExportField] можно использовать только в методах с 0 параметров.|
|XA4206|[Экспорта] не может использоваться для универсального типа.|
|XA4207|[ExportField] не может использоваться для универсального типа.|
|XA4208|[Java.Interop.ExportFieldAttribute] не может использоваться на метод, возвращающий значение void.|
|XA4209|Не удалось создать JavaTypeInfo для класса: {0} из-за {1}.|
|XA4210|Необходимо добавить ссылку на Mono.Android.Export.dll при использовании ExportAttribute или ExportFieldAttribute.|
|XA4211|AndroidManifest.xml //uses-sdk/@android:targetSdkVersion «{0}» меньше, чем $(TargetFrameworkVersion) «{1}». С помощью API-\ {1\\} для ACW компиляции.|


### <a name="xa5xxx-errors"></a>Ошибки XA5xxx

|Код ошибки|Описание|
|--- |--- |
|XA5101|Отсутствует «{0}» компилятора. Выполните установку Android NDK.|
|XA5102|Не удалось выполнить преобразование из сборки в машинный код. Отправьте [отчет ошибок](http://bugzilla.xamarin.com).|
|XA5103|Не удалось скомпилировать файл «{0}». Отправьте [отчет ошибок](http://bugzilla.xamarin.com).|
|XA5201|Не удалось выполнить связывание собственный. Проверьте предоставленный gcc флаги пользователя: {0}|
|XA5202|Не удалось выполнить связывание собственный. Просмотрите журнал сборки.|
|XA5303|Машинный код связывания предупреждение: {0}.|
|XA5300|Пакет SDK для Android не найдена, или установлена не полностью.|
|XA5301|Отсутствует средство «удалить». Установите компонент «Средства командной строки» Xcode.|
|XA5302|Отсутствует средство «dsymutil». Установите компонент «Средства командной строки» Xcode.|
|XA5203|Не удалось создать символы отладки (dSYM directory). Просмотрите журнал сборки.|
|XA5204|Не удалось удалить конечный двоичный файл. Просмотрите журнал сборки.|
|XA5205|Отсутствует средство «aapt». Установите пакет средств построения пакета SDK для Android.|
|XA5206|{0}. Android ресурсов {1} каталог не существует.|
|XA5207|{0}. {1} файл библиотеки Java не существует.|
|XA5208|Не удалось загрузить. Загрузить {0} и поместить его в каталог {1}.|
|XA5209|Сбой распаковки. {0} Загрузите и извлеките файлы в каталоге {1}.|
|XA5210|{0}. Собственная библиотека {1} файл не существует.|

### <a name="xa6xxx-errors"></a>Ошибки XA6xxx

|Код ошибки|Описание|
|--- |--- |
|XA6001|Запущенный Cecil не поддерживает чередование сборки.|
|XA6002|Не удалось убрать сборки «{0}».|
|XA6003|UnauthorizedAccessException сообщение.|

### <a name="xa9xxx-errors"></a>Ошибки XA9xxx

Эти коды ошибок, ошибки лицензирования и активации.


#### <a name="xa9000"></a>XA9000

 **Причина:** истек срок действия лицензии

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|


#### <a name="xa9001"></a>XA9001

 **Причина:** истек срок действия пробной версии

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|ПРЕДУПРЕЖДЕНИЕ|



#### <a name="xa9002"></a>XA9002

 **Cause:** AndroidJavaSource

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОК|ОК|ОК|ОК|

 **Причина:** AndroidJavaLibrary

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОК|ОК|ОК|ОК|

 **Если сборка привязки .jar внедренных, это перехватывается во время упаковки не время построения.**

 **Причина:** AndroidNativeLibrary

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОК|ОК|ОК|ОК|


#### <a name="xa9003"></a>XA9003

 **Причина:** System.Runtime.Serialization

 **При выполнении проверка:** пакета

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|

 **Причина:** System.ServiceModel.Web

 **При выполнении проверка:** пакета

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|

 **Причина:** Mono.Data.Tds

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|

 **Это упоминается в System.Data.dll, что разрешено**

 **Причина:** Mono.Android.Export

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОК|ОК|ОК|ОК|



#### <a name="xa9004"></a>XA9004

 **Причина:** --профилирования

 **При выполнении проверка:** пакета

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|



#### <a name="xa9005"></a>XA9005

 **Причина:** ограничение размера (32 КБ).

 **При выполнении проверка:** пакета

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОК|-|-|-|



#### <a name="xa9006"></a>XA9006

 **Причина:** имен System.Data.SqlClient.

 **При выполнении проверка:** пакета

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|


#### <a name="xa9008"></a>XA9008

 **Причина:** построение из командной строки.

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОК|ОК|ОК|


#### <a name="xa9009"></a>XA9009

 **Причина:** отсутствует серийный номер.

 **При выполнении проверка:** не поддающегося

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|


#### <a name="xa9010"></a>XA9010

 **Причина:** недопустимый ProductId.

 **При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|

Эквивалентно XA9018.



#### <a name="xa9011"></a>XA9011

 **Причина:** не удалось обновить файл лицензии (в новый формат файлов).

 **При выполнении проверка:** активации

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|

#### <a name="xa9012"></a>XA9012

 **Причина:** Интернет отсутствует

 **При выполнении проверка:** активации

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|


#### <a name="xa9013"></a>XA9013

 **Причина:** Неизвестная ошибка

 **При выполнении проверка:** активации

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|


#### <a name="xa9014"></a>XA9014

 **Причина:** недопустимый Activation кода

 **При выполнении проверка:** активации

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|


#### <a name="xa9017"></a>XA9017

 **Причина:** сервер активации не возвращает действительной лицензии.

 **При выполнении проверка:** активации

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|ОШИБКА|


#### <a name="xa9018"></a>XA9018

**Причина:** недействительную лицензию

**При выполнении проверка:** построения

|Начального уровня|Indie|Business(Trial)|Business|Предприятие|
|--- |--- |--- |--- |--- |
|-|-|ОШИБКА|-|-|

