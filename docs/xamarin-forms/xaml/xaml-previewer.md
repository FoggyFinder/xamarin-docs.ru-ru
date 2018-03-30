---
title: Средство предварительного просмотра XAML для Xamarin.Forms
description: В разделе отображаются при вводе макеты Xamarin.Forms!
ms.topic: article
ms.prod: xamarin
ms.assetid: 84769ff1-72fd-4c44-8251-dd6d5bf8c7b2
ms.technology: xamarin-forms
author: charlespetzold
ms.author: chape
ms.date: 02/24/2017
ms.openlocfilehash: a7a9c4fed92cb4ed8c8c12e97129bc8379037acb
ms.sourcegitcommit: 17a9cf246a4d33cfa232016992b308df540c8e4f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2018
---
# <a name="xaml-previewer-for-xamarinforms"></a>Средство предварительного просмотра XAML для Xamarin.Forms

_В разделе отображаются при вводе макеты Xamarin.Forms!_

## <a name="requirements"></a>Требования

Проекты требуют последний пакет Xamarin.Forms NuGet для средство предварительного просмотра XAML для работы. Предварительный просмотр приложения Android требуется [JDK 1.8 x64](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Дополнительные сведения в [заметки о выпуске](https://developer.xamarin.com/releases/studio/xamarin.studio_6.2/xamarin.studio_6.2/#Xamarin_Forms_Previewer).

## <a name="getting-started"></a>Начало работы

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Используйте **представление > Другие окна > средство предварительного просмотра Xamarin.Forms** меню в Visual Studio, чтобы открыть окно предварительного просмотра. Используйте **окна > создать группу вертикальных вкладок** меню, чтобы разместить его рядом друг с другом.

[![Предварительная версия элемента управления ListView в Visual Studio](xaml-previewer-images/xamlp-list-vs-sml.png "средство предварительного просмотра форм в Visual Studio")](xaml-previewer-images/xamlp-list-vs.png#lightbox "средство предварительного просмотра форм в Visual Studio")

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

**Предварительного просмотра** кнопку можно отобразить в редакторе, щелкнув правой кнопкой мыши XAML-файл, а затем выбрав **открыть с помощью > средства просмотра XAML**. Затем в области предварительного просмотра можно отображать и скрывать, нажав клавишу **предварительного просмотра** кнопку в правом верхнем углу любого окна документа XAML:

[![Предварительная версия элемента управления ListView в Visual Studio для Mac](xaml-previewer-images/xamlp-list-sml.png "средство предварительного просмотра форм в Visual Studio для Mac")](xaml-previewer-images/xamlp-list.png#lightbox "средство предварительного просмотра форм в Visual Studio для Mac")

-----

## <a name="xaml-preview-options"></a>Параметры предварительного просмотра XAML

Доступны следующие параметры в верхней части области просмотра.

* **Телефон** — отображения на экране телефона размер
* **Планшет** — отображения на экране планшета размер (Обратите внимание, элементы управления масштабом в правом нижнем углу панели)
* **Android** — Android версии экрана
* **iOS** — версии iOS экрана
* (Значок) — Portait использует книжной ориентации для предварительного просмотра
* Альбомная (значок) — использует альбомной ориентации для предварительного просмотра

## <a name="adding-design-time-data"></a>Добавление данных во время разработки

Некоторые макеты, может быть трудно визуализировать без данных привязаны к элементам пользовательского интерфейса. Чтобы сделать на предварительную версию более полезными, назначьте некоторые статические данные элементы управления, жесткого задания контекст привязки (либо в кода или с помощью XAML).

Ссылаться на Джеймсом Монтеманьо [в блоге о добавлении данных во время разработки](http://motzcod.es/post/143702671962/xamarinforms-xaml-previewer-design-time-data) чтобы узнать, как выполнить привязку к статическим ViewModel в XAML.

## <a name="troubleshooting"></a>Устранение неполадок

Проверьте следующие проблемы и [Xamarin форумы](https://forums.xamarin.com/categories/xamarin-forms), если возникли проблемы.

### <a name="xaml-preview-isnt-showing"></a>Предварительный просмотр XAML не отображается.

Проверьте следующее:

* Проект должен быть создан (скомпилированный) перед попыткой Предварительный просмотр файлов XAML.
* Конструктор агент должен быть настройки при первом предварительном файл XAML - будет отображаться индикатор хода выполнения в предварительном просмотре, а также сообщения о ходе выполнения, пока это не будет готов.
* Попробуйте закрыть и повторно открыв файл XAML.

### <a name="invalid-xaml-the-android-project-needs-to-built-before-preview-can-be-created"></a>Недопустимый XAML: Проект Android необходимо построения, чтобы можно было создать предварительный просмотр

Средство предварительного просмотра XAML требуется построение проекта перед отображением страницы.
Если ниже ошибка появляется в верхней части области просмотра, повторное построение приложения и повторите попытку.

![Сообщение об ошибке: проекта должны быть построены в первую очередь](xaml-previewer-images/error-not-built-sml.png "сообщение об ошибке: повторное построение проекта")