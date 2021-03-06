---
title: Поддержка UrhoSharp Android
description: В этом документе описываются настройки конкретного Android и сведения, относящиеся к функции для UrhoSharp. В частности, в нем рассматриваются Поддерживаемые архитектуры, как создать проект, Настройка и запуск Urho и внедрение пользовательских Urho.
ms.prod: xamarin
ms.assetid: 8409BD81-B1A6-4F5D-AE11-6BBD3F7C6327
author: charlespetzold
ms.author: chape
ms.date: 03/29/2017
ms.openlocfilehash: 6e489f52712989b5f94fa52d5ec6f22a13ce6252
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34783786"
---
# <a name="urhosharp-android-support"></a>Поддержка UrhoSharp Android

_Android определенные настройки и компоненты_

Пока Urho переносимой библиотеке классов, и обеспечивает такой же API, используемые в нескольких различных платформ для логику игры по-прежнему необходимо инициализировать Urho в драйвере определенной платформы, а в некоторых случаях, необходимо воспользоваться преимуществами конкретных компонентов платформы .

В следующих страницах, предполагается, что `MyGame` является подклассом `Application` класса.

## <a name="architectures"></a>Архитектуры

**Поддерживаемые архитектуры**: x86 armeabi, armeabi v7a

## <a name="create-a-project"></a>Создание проекта

Создание проекта Android и добавьте пакет UrhoSharp NuGet.

Добавить данные, содержащие активов для **активы** каталог и убедитесь, что все файлы имеют **AndroidAsset** как **действие при построении**.

![Установка проектов](android-images/image-3.png "добавить данные с ресурсами, к каталогу активы")

## <a name="configure-and-launching-urho"></a>Настройка и запуск Urho

Добавление с помощью инструкций для `Urho` и `Urho.Android` пространства имен, а затем добавьте следующий код для инициализации Urho, а также для запуска приложения.

Самый простой способ запуска игры, как выполняется в классе MyGame является вызов

```csharp
UrhoSurface.RunInActivity<MyGame>();
```

Откроется действие во весь экран с игрой как содержимое.

## <a name="custom-embedding-of-urho"></a>Внедрение пользовательских Urho

Можно также, что Urho взять на себя экрана всего приложения и ее использование в качестве компонента приложения, можно создать `SurfaceView` через:

```csharp
var surface = UrhoSurface.CreateSurface<MyGame>(activity)
```

Также потребуется для передачи несколько событий от вас действий UrhoSharp, например:

```csharp
protected override void OnPause()
{
    UrhoSurface.OnPause();
    base.OnPause();
}
```

Необходимо сделать это: `OnResume`, `OnPause`, `OnLowMemory`, `OnDestroy`, `DispatchKeyEvent` и `OnWindowFocusChanged`.

Это показано типичные действия, которое запускает игры.

```csharp
[Activity(Label = "MyUrhoApp", MainLauncher = true,
    Icon = "@drawable/icon", Theme = "@android:style/Theme.NoTitleBar.Fullscreen",
    ConfigurationChanges = ConfigChanges.KeyboardHidden | ConfigChanges.Orientation,
    ScreenOrientation = ScreenOrientation.Portrait)]
public class MainActivity : Activity
{
    protected override void OnCreate(Bundle bundle)
    {
        base.OnCreate(bundle);
        var mLayout = new AbsoluteLayout(this);
        var surface = UrhoSurface.CreateSurface<MyUrhoApp>(this);
        mLayout.AddView(surface);
        SetContentView(mLayout);
    }

    protected override void OnResume()
    {
        UrhoSurface.OnResume();
        base.OnResume();
    }

    protected override void OnPause()
    {
        UrhoSurface.OnPause();
        base.OnPause();
    }

    public override void OnLowMemory()
    {
        UrhoSurface.OnLowMemory();
        base.OnLowMemory();
    }

    protected override void OnDestroy()
    {
        UrhoSurface.OnDestroy();
        base.OnDestroy();
    }

    public override bool DispatchKeyEvent(KeyEvent e)
    {
        if (!UrhoSurface.DispatchKeyEvent(e))
            return false;
        return base.DispatchKeyEvent(e);
    }

    public override void OnWindowFocusChanged(bool hasFocus)
    {
        UrhoSurface.OnWindowFocusChanged(hasFocus);
        base.OnWindowFocusChanged(hasFocus);
    }
}
```

