---
title: UrhoSharp iOS и tvOS поддержки
description: В этом документе рассматриваются операций ввода-вывода и поддержку tvOS UrhoSharp. Он описывает, как создать проект, настроить и запустить Urho и выполнять пользовательский внедрения Urho.
ms.prod: xamarin
ms.assetid: 7B06567E-E789-4EA1-A2A9-F3B2212EDD23
author: charlespetzold
ms.author: chape
ms.date: 03/29/2017
ms.openlocfilehash: 7e8975b6885f6c902634e05aafca0b8ee60a981c
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34783979"
---
# <a name="urhosharp-ios-and-tvos-support"></a>UrhoSharp iOS и tvOS поддержки

Пока Urho переносимой библиотеке классов, и обеспечивает такой же API, используемые в нескольких различных платформ для логику игры по-прежнему необходимо инициализировать Urho в драйвере определенной платформы, а в некоторых случаях, необходимо воспользоваться преимуществами конкретных компонентов платформы .

В следующих страницах, предполагается, что `MyGame` является sublcass из `Application` класса.

## <a name="ios-and-tvos"></a>iOS и tvOS

**Поддерживаемые архитектуры:** armv7 arm64, i386

## <a name="creating-a-project"></a>Создание проекта

Создайте проект iOS, а затем добавить данные в каталог ресурсов и убедитесь, что все файлы имеют **BundleResource** как **действие при построении**.

![Установка проектов](ios-images/image-4.png "добавить данные в каталог ресурсов")

## <a name="configuring-and-launching-urho"></a>Настройка и запуск Urho

Добавление с помощью инструкций для `Urho` и `Urho.iOS` пространства имен, а затем добавьте следующий код для инициализации Urho, а также для запуска приложения:

```csharp
new MyGame().Run();
```

Обратите внимание, что поскольку ожидает iOS `FinishedLaunching` для выполнения, следует очередь вызов `Run()` для выполнения после завершения работы метода, это распространенных случаях:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
    LaunchGame();
    return true;
}

async void LaunchGame()
{
    await Task.Yield();
    new SamplyGame().Run();
}
```

Важно отключить оптимизацию PNG, так как оптимизатор PNG операций ввода-вывода по умолчанию будет создавать образы, которые не могут правильно в настоящее время использует Urho

## <a name="custom-embedding-of-urho"></a>Внедрение пользовательских Urho

Можно также, что Urho взять на себя экрана всего приложения и ее использование в качестве компонента приложения, можно создать `UrhoSurface` это `UIView` , который можно внедрить в существующем приложении.

Это то, что необходимо сделать:

```csharp
var view = new UrhoSurface () {
    Frame = new CGRect (100,100,200,200),
    BackgroundColor = UIColor.Red
}
window.AddSubview (view);
```

Это будет размещаться классе Urho, таким образом, а затем это можно сделать:

```csharp
new MyGame().Run ();
```

