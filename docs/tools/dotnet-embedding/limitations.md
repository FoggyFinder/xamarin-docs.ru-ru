---
title: Ограничения внедрения .NET
description: В этом документе описываются ограничения внедрения .NET, средство, которое позволяет использовать код .NET в других языках программирования.
ms.prod: xamarin
ms.assetid: EBBBB886-1CEF-4DF4-AFDD-CA96049F878E
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: fdd3ac4cd57ac7f79f9071d62e758625b30f05dd
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34794128"
---
# <a name="net-embedding-limitations"></a>Ограничения внедрения .NET

В этом документе описываются ограничения внедрения .NET и когда это возможно, предлагаются обходные пути для них.

## <a name="general"></a>Общие

### <a name="use-more-than-one-embedded-library-in-a-project"></a>Использование более одного внедренные библиотеки в проект

Не могут существовать две Mono среды выполнения, совместно существующих внутри одного приложения. Это означает, что нельзя использовать две разные внедрения .NET созданные библиотеки внутри одного приложения.

**Обходной путь:** генератор можно использовать для создания единого библиотеку, которая включает несколько сборок (из разных проектов).

### <a name="subclassing"></a>Создание подклассов

Внедрение .NET упрощает интеграцию Mono среды выполнения в приложениях, предоставляя ряд готовых к использованию API для целевого языка и платформы.

Но это не является двусторонней интеграции, например нельзя подкласс управляемого типа и ожидать, что управляемый код обратного вызова в машинном коде, так как это совместное существование неизвестно, управляемый код.

В зависимости от потребностей возможно на инструкции по решению части этого ограничения, например

* управляемый код может p/invoke в машинном коде. Это требует настройки управляемого кода для поддержки настройки из машинного кода;

* Использование продуктов как Xamarin.iOS и предоставления управляемую библиотеку, которое позволит Objective-C (в данном случае) создать подкласс некоторых управляемых NSObject подклассов.

## <a name="objective-c-generated-code"></a>Созданный код Objective-c.

### <a name="nullability"></a>Допустимость значений NULL

Нет без метаданных в .NET, сообщите нам, если пустая ссылка является допустимым или не для API. Большинство API-интерфейсы вызывают `ArgumentNullException` , если они не может справиться с `null` аргумент. Это создает проблему, как-Objective-C обработку исключений, то лучше избегать.

Потому что невозможно создать заметки точные допустимость значений NULL в файлах заголовков и хотите свести к минимуму управляемые исключения мы по умолчанию для аргументов, отличных от null (`NS_ASSUME_NONNULL_BEGIN`) и добавить некоторые только, если возможна точности, заметки допустимость значений NULL.

### <a name="bitcode-ios"></a>Bitcode (iOS)

В настоящее время внедрения .NET не поддерживает bitcode на iOS, которая включена для некоторые шаблоны проекта Xcode. Это будет необходимо отключить, чтобы успешно ссылки, созданной платформ.

![Параметр Bitcode](images/ios-bitcode-option.png)
