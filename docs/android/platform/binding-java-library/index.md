---
title: Привязка библиотеки Java
description: Android сообщество имеет много библиотек Java, которые можно использовать в приложении; в этом руководстве объясняется, как внедрить Java библиотеки в приложении Xamarin.Android путем создания библиотеки привязок.
ms.prod: xamarin
ms.assetid: B39FF1D5-69C3-8A76-D268-C227A23C9485
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 05/01/2017
ms.openlocfilehash: 3c2ed92da07519516db94697bbeaac9f328baa22
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="binding-a-java-library"></a>Привязка библиотеки Java

_Android сообщество имеет много библиотек Java, которые можно использовать в приложении; в этом руководстве объясняется, как внедрить Java библиотеки в приложении Xamarin.Android путем создания библиотеки привязок._

## <a name="overview"></a>Обзор

Экосистема стороннюю библиотеку для Android больших объемов. По этой причине часто имеет смысл использовать существующую библиотеку Android чем создание нового. Xamarin.Android предлагает два способа использования этих библиотек.

-   Создание *привязки библиотеки* , автоматически создает оболочку для библиотеки с помощью C# оболочек, могут вызывать код Java с помощью C# вызывает.

-   Используйте *Java Native Interface* (*JNI*) для вызова в коде библиотеки Java непосредственно. JNI — структура программирования, которая включает код Java для вызова и вызываться собственных приложений или библиотек.

В этом руководстве объясняется первый вариант: создание *привязки библиотеки* , создает оболочку для существующих библиотек Java в сборку, в которой можно перейти в приложении. Дополнительные сведения об использовании JNI см. в разделе [работа с JNI](~/android/platform/java-integration/working-with-jni.md).

Xamarin.Android реализует привязок с помощью *управляемых с помощью вызываемых оболочек* (*MCW*). MCW представляет собой мост JNI, который используется, когда управляемый код должен вызывать код Java. Управляемые вызываемой оболочки также обеспечивают поддержку для создания подклассов типов Java и переопределения виртуальных методов для типов Java. Аналогичным образом каждый раз, когда код Android среды выполнения (ГРАФИКА), которые будут вызывать управляемый код, это происходит через другой мост JNI, известные как Android вызываемой оболочки (ACW). Это [архитектура](~/android/internals/architecture.md) проиллюстрирован на следующей схеме:

[![Android архитектура JNI моста](images/architecture.png)](images/architecture.png#lightbox)

Библиотека привязок представляет сборку, содержащую управляемый вызываемых оболочек для типов Java. Например, здесь является типом Java, `MyClass`, который необходимо заключать в библиотеке привязки:

```java
package com.xamarin.mycode;

public class MyClass
{
    public String myMethod (int i) { ... }
}
```

После мы создаем библиотеку привязок для **.jar** , содержащий `MyClass`, можно создать его экземпляр и вызова методов из C#:

```csharp
var instance = new MyClass ();

string result = instance.MyMethod (42);
```

Для создания этой библиотеки привязок, используется Xamarin.Android *библиотеки привязок Java* шаблона. Итоговый проект привязки создает сборку .NET с классами MCW **.jar** файлы и ресурсы для проектов Android библиотек, внедренный в него. Также можно создать привязки библиотеки для Android архива (. AAR) файлы и проекты библиотеки Android Eclipse. С помощью ссылки на сборку привязки библиотеки DLL, можно повторно использовать существующую библиотеку Java в проекте Xamarin.Android.

При ссылке на типы в библиотеке привязки, необходимо использовать пространство имен привязки библиотеки. Как правило, вы добавляете `using` директивы в верхней части вашего исходного кода C# файлы, имя пакета Java версии пространства имен .NET. Например, если в имени пакета Java в список связанных **.jar** находится в следующем расположении:

```csharp
com.company.package
```

Затем нужно будет только разместить следующие `using` инструкции в верхней части C# исходные файлы для доступа к типы в значение границы **.jar** файла:

```csharp
using Com.Company.Package;
```


При привязке существующей библиотеки Android, это необходимо учитывать следующие моменты:

* **Существуют ли все внешние зависимости для библиотеки?** &ndash; Все зависимости Java, необходимые для библиотеки Android должны быть включены в проект Xamarin.Android, как **ReferenceJar** или как **EmbeddedReferenceJar**. Все собственные сборки необходимо добавить в проект привязки, как **EmbeddedNativeLibrary**.  

* **Какая версия Android API имеет ли целевой библиотеки Android?** &ndash; Невозможно «перейти» уровень Android API; Убедитесь, что такой же API предназначен для привязки проекта Xamarin.Android уровень (или выше) как библиотеку Android.

* **Какая версия JDK был использован для компиляции библиотеки?** &ndash; Ошибок привязки может возникнуть, если библиотека Android был создан с помощью другой версии JDK, чем используется с Xamarin.Android. Если это возможно необходимо перекомпилируйте библиотеку Android, используя ту же версию JDK, используемая для установки Xamarin.Android.


## <a name="build-actions"></a>Действия при сборке

При создании библиотеки привязки задаются *построения действий* на **.jar** или. AAR-файлы, которые включить в проект библиотеки привязок &ndash; определяет каждое действие сборки как **.jar** или. Файл AAR будут внедрены в (или ссылается) библиотеки привязок. В следующем списке перечислены эти построения действий:

* `EmbeddedJar` &ndash; Внедряет **.jar** в результирующей привязки библиотеки DLL в качестве внедренного ресурса. Это самый простой и действия большинства часто используемых сборки. Используйте этот параметр, если нужно **.jar** автоматически компилируются в байтовый код и упакованы в библиотеке привязок.

* `InputJar` &ndash; Нельзя внедрить **.jar** в полученная библиотека привязок. БИБЛИОТЕКИ DLL. Библиотеки привязок. Библиотеки DLL, имеют зависимость в данном **.jar** во время выполнения. Используйте этот параметр, если не хотите включать **.jar** в библиотеке привязок (например, для лицензирования причинам). Если используется этот параметр, необходимо убедиться, что входные данные **.jar** на устройства, которое запускает приложение.

* `LibraryProjectZip` &ndash; Внедряет. Файл AAR в полученная библиотека привязок. БИБЛИОТЕКИ DLL. Это похоже на EmbeddedJar, за исключением того, доступа к ресурсам (а также код) значение границы. AAR-файл. Используйте этот параметр, если требуется внедрить. AAR в библиотеку привязок.

* `ReferenceJar` &ndash; Указывает ссылку **.jar**: ссылка **.jar** — **.jar** такой список связанных **.jar** или. Зависит от AAR-файлы. Эта ссылка **.jar** применяется только для удовлетворения зависимости времени компиляции. При использовании действие построения C# привязки не создаются для ссылки на **.jar** и не внедрен в полученная библиотека привязок. БИБЛИОТЕКИ DLL. Этот параметр используется при внесении библиотеку привязок для ссылки на **.jar** , но еще не сделано еще. Действие построения полезен для упаковки несколько **.jar**s (и (или). AARs) в несколько независимых библиотек привязок.

* `EmbeddedReferenceJar` &ndash; Внедряет ссылку **.jar** в полученная библиотека привязок. БИБЛИОТЕКИ DLL. Это действие построения используется для создания привязок C# для обоих входных данных **.jar** (или. AAR) и все его ссылки **.jar**(s) в библиотеке привязок.

* `EmbeddedNativeLibrary` &ndash; Внедряет собственный **.so** в привязку. Это действие построения используется для **.so** файлы, которые требуются **.jar** файла выполняется привязка. Может потребоваться вручную загрузить **.so** библиотеки перед выполнением кода в библиотеке Java. Это описано ниже.

Эти действия описаны более подробно в следующих руководствах построения.

Кроме того следующие действия сборки используются для импорта документации по Java API и преобразовывать их в C# XML-документации:

* `JavaDocJar` используется для указания архив Javadoc JAR-файл для библиотеки Java, который соответствует стиля пакета Maven (обычно `FOOBAR-javadoc**.jar**`).
* `JavaDocIndex` используется для указания `index.html` файла в справочной документации API HTML.
* `JavaSourceJar` используется в дополнение к `JavaDocJar`, чтобы сначала создать JavaDoc из источников и затем обрабатывать результаты как `JavaDocIndex`, для библиотеки Java, который соответствует Maven пакета стиля (обычно `FOOBAR-sources**.jar**`).

Документацию по API должны быть doclet по умолчанию из Java8, Java7 или Java6 SDK (это разные формат), или DroidDoc стиля.

## <a name="including-a-native-library-in-a-binding"></a>Включая собственной библиотеки в привязке

Может потребоваться включить **.so** библиотеку в проекте привязки Xamarin.Android, как часть привязки библиотеки Java. При выполнении упакованного кода Java для осуществления вызовов JNI и сообщение об ошибке завершится Xamarin.Android _java.lang.UnsatisfiedLinkError: собственный метод, не найден:_ будет отображаться в logcat ожидания для приложения.

Для этого исправления ситуации нужно вручную загрузить **.so** библиотеки с помощью вызова `Java.Lang.JavaSystem.LoadLibrary`. Например при условии, что проект Xamarin.Android общие библиотеки **libpocketsphinx_jni.so** включен в проект привязки с помощью действия построения **EmbeddedNativeLibrary**, следующие фрагмент кода (выполняется перед началом использования общей библиотеки) будет загружать **.so** библиотеки:

```csharp
Java.Lang.JavaSystem.LoadLibrary("pocketsphinx_jni");
```

## <a name="adapting-java-apis-to-ceparsl"></a>Адаптация Java API-интерфейсы для C&eparsl;

Генератор привязки Xamarin.Android изменит некоторые Java стили и шаблоны в соответствии с шаблонами в .NET. В следующем списке описываются как Java будет сопоставляться с C# / .NET:

-   _Методы Setter или Getter_ на языке Java, _свойства_ в .NET.

-   _Поля_ на языке Java, _свойства_ в .NET.

-   _Прослушиватели/Listener интерфейсы_ на языке Java, _событий_ в .NET. Параметры методов в интерфейсе обратного вызова, будет представлен `EventArgs` подкласс.

-   Объект _вложенные статический класс_ в Java — _вложенных классов_ в .NET.

-   _Внутренний класс_ в Java — _вложенных классов_ с конструктор экземпляра, а в C#.



## <a name="binding-scenarios"></a>Сценарии привязки

Следующие руководства по сценариям привязки, чтобы привязать библиотеки Java (или библиотек) для внесения в приложении:

-   [Привязка. JAR](~/android/platform/binding-java-library/binding-a-jar.md) приведен пример привязки библиотек для **.jar** файлов.

-   [Привязка. AAR](~/android/platform/binding-java-library/binding-an-aar.md) приведен пример привязки библиотек для. AAR-файлы. Чтение в этом пошаговом руководстве, чтобы узнать, как выполнить привязку библиотеки Android Studio.

-   [Привязка проекта библиотеки служб Eclipse](~/android/platform/binding-java-library/binding-a-library-project.md) приведен пример создания привязки библиотеки из проектов библиотеки Android. Чтение в этом пошаговом руководстве, чтобы узнать, как привязать проекты библиотеки Android Eclipse.

-   [Настройка привязок](~/android/platform/binding-java-library/customizing-bindings/index.md) объясняет, как вручную изменить привязки, чтобы устранить ошибки построения и формирование получающийся API, чтобы оно было больше «C#-как».

-   [Устранение неполадок привязки](~/android/platform/binding-java-library/troubleshooting-bindings.md) перечислены распространенные ошибки привязки, объясняется, возможные причины ее возникновения и предложения по разрешению этих проблем.


## <a name="related-links"></a>Связанные ссылки

- [Работа с JNI](~/android/platform/java-integration/working-with-jni.md)
- [GAPI Metadata](http://www.mono-project.com/docs/gui/gtksharp/gapi/#metadata)
- [Использование собственных библиотек](~/android/platform/native-libraries.md)
