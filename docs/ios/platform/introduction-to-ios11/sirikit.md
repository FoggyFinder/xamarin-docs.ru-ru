---
title: SiriKit обновлений в iOS 11
description: В этом документе описывается работа с SiriKit в iOS 11. В частности он проверяет, как работать с задачами и примечания и как обеспечить альтернативные имена для приложения.
ms.prod: xamarin
ms.assetid: 8F75300B-B591-42ED-9D17-001992A5C381
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 09/07/2017
ms.openlocfilehash: 28160b40c97b8cc62fae95d3643801f1c4cc5e93
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34787589"
---
# <a name="sirikit-updates-in-ios-11"></a>SiriKit обновлений в iOS 11

SiriKit впервые появился в iOS 10, с количеством доменов службы (включая тренировки игнорировать резервирования и вызова). Ссылаться на [SiriKit раздел](~/ios/platform/sirikit/index.md) SiriKit основные понятия и как реализовать SiriKit в вашем приложении.

![Демонстрация списка задач Siri](sirikit-images/sirikit.png)

SiriKit в iOS 11 добавляет эти новые и обновленные намерения домены:

- [**Содержит список и заметки о** ](#listsnotes) — новые! Предоставляет API для приложений для обработки задач и заметок.
- **Коды Visual** — новые! Siri можно отобразить QR-коды должны совместно использовать контактные сведения или участвовать в платежных транзакций.
- **Платежи** — добавлен способы поиска и передачи для оплаты взаимодействий.
- **Воспользуйтесь преимуществами резервирования** — добавлены Отмена намерения расстояния и обратную связь.

Другие новые функции:

- [**Имена приложений альтернативных** ](#alternativenames) — предоставляет псевдонимы, которые помогают клиентам сообщить Siri целевые приложения, предлагая альтернативные имена и произношения.
- **Запуск тренировки** — предоставляет возможность запускать тренировки в фоновом режиме.

Некоторые из этих компонентов описываются ниже. Дополнительные сведения о других посвящены [SiriKit документации компании Apple](https://developer.apple.com/documentation/sirikit).

<a name="listsnotes" />

## <a name="lists-and-notes"></a>Списки и примечания

Новый домен, списки и примечания предоставляет API-Интерфейс для приложений для обработки задач и заметок через запросы Siri голоса.

**Задачи**

- Имеет заголовок и состояние завершения.
- При необходимости укажите крайний срок и расположение.

**Примечания**

- Имеет заголовок и содержимого поля.

Задачи и заметки можно организовать в группы. В оставшейся части этого раздела описывается, как реализовать этот новый домен с SiriKit, с помощью [TasksNotes SiriKit пример](https://developer.xamarin.com/samples/monotouch/ios11/SiriKitSample/).

### <a name="how-to-process-a-sirikit-request"></a>Обработка запроса SiriKit

Обработайте запрос SiriKit, выполнив следующие действия:

1. **Разрешить** — проверки параметров и запрашивать дополнительные сведения от пользователя (при необходимости).
2. **Подтвердите** – окончательная проверка и проверки, обработки запроса.
3. **Обрабатывать** — выполнить операцию (обновление данных или выполнение сетевых операций).

Первые два действия являются необязательными, (несмотря на то, что рекомендуется), и последний шаг является обязательным.
Более подробные инструкции в [SiriKit раздел](~/ios/platform/sirikit/index.md).

### <a name="resolve-and-confirm-methods"></a>Решения и подтвердите методы

Эти необязательные методы позволяют код выполнять проверки, выберите значения по умолчанию или запрос дополнительных сведений от пользователя.

Например для `IINCreateTaskListIntent` интерфейс, необходимый метод — `HandleCreateTaskList`. Существует четыре необязательные методы, которые обеспечивают больший контроль над Siri взаимодействия:

- `ResolveTitle` — Проверяет заголовок и задает заголовок по умолчанию (если применимо) сообщает, что данные не требуется.
- `ResolveTaskTitles` — Проверяет список задач произносятся пользователем.
- `ResolveGroupName` — Проверяет имя группы, выбирает группу по умолчанию или сообщает, что данные не требуется.
- `ConfirmCreateTaskList` — Проверяет, что ваш код может выполнить запрошенную операцию, но не выполняет (только `Handle*` методы следует изменять данные).

### <a name="handle-the-intent"></a>Назначение обработки

Существует шесть целей в домене списки и примечания, три для задач и три заметки о.
Ниже приведены методы, которые необходимо реализовать для обработки этих целей.

- Для задачи:
  - `HandleAddTasks`
  - `HandleCreateTaskList`
  - `HandleSetTaskAttribute`
- Для примечания.
  - `HandleCreateNote`
  - `HandleAppendToNote`
  - `HandleSearchForNotebookItems`

У каждого метода есть намерения Тип переданного ему, который содержит все сведения, Siri проанализированный из запроса пользователя (и возможно обновление в `Resolve*` и `Confirm*` методов).
Ваше приложение должно синтаксического анализа данных, а затем выполнить некоторые действия для хранения или иной обработки данных и возвращают результат, Siri говорит и показывает пользователю.

### <a name="response-codes"></a>Коды ответов

Необходимая `Handle*` и необязательные `Confirm*` методы указать код ответа, задав значение для объекта, передаваемого обработчику их завершения. Ответы берутся из `INCreateTaskListIntentResponseCode` перечисления:

- `Ready` — Возвращает на этапе подтверждения (т. е. из `Confirm*` метода, но не из `Handle*` метода).
- `InProgress` — Используется для длительных задач (например, операции сети или сервера).
- `Success` — Ответ подробные сведения о Успешная операция (только из `Handle*` метода).
- `Failure` — Означает, что произошла ошибка, и не удалось выполнить операцию.
- `RequiringAppLaunch` — Не удалось обработать назначение, но операция возможна в приложении.
- `Unspecified` -Не использовать: сообщение об ошибке будет отображаться для пользователя.

Дополнительные сведения об этих методов и ответы в компании Apple [SiriKit перечислены и заметки о документации](https://developer.apple.com/documentation/sirikit/lists_and_notes).

### <a name="implementing-lists-and-notes"></a>Реализация списков и примечания

[TasksNotes SiriKit пример](https://developer.xamarin.com/samples/monotouch/ios11/SiriKitSample/) был создан с помощью следующих действий для добавления поддержки SiriKit пустого приложения iOS.

Во-первых Чтобы добавить поддержку SiriKit, выполните следующие действия для приложения iOS.

1. Деления **SiriKit** в **Entitlements.plist**.
2. Добавить **конфиденциальности — Описание использования Siri** ключа для **Info.plist**, вместе с сообщением для ваших клиентов.
3. Вызовите `INPreferences.RequestSiriAuthorization` метода в приложении, чтобы предложить пользователю разрешить Siri взаимодействия.
4. Добавьте SiriKit для идентификатора приложения на портале разработчиков и повторно создать профили подготовки для включения новых права.

Затем добавьте новый проект расширения приложения для обработки запросов Siri:

1. Щелкните правой кнопкой мыши решение и выберите **Добавить > Добавить новый проект...** .
2. Выберите **iOS > расширения > целей расширения** шаблона.
3. Будут добавлены два новых проектов: назначение и IntentUI. Настройки пользовательского интерфейса не является обязательным, поэтому Образец включает только код в **намерение** проекта.

Проект расширения — где все SiriKit запросы будут обрабатываться. Как отдельное расширение он не имеет автоматически каким-либо образом, для взаимодействия с основного приложения — это обычно конфликт устраняется реализацией общедоступным хранилищем файлов с помощью групп приложений.

#### <a name="configure-the-intenthandler"></a>Настройка IntentHandler

`IntentHandler` Класс является точкой входа для Siri запрашивает — каждые намерение передается `GetHandler` метод, который возвращает объект, который может обработать запрос.

В следующем примере кода показана простая реализация:

```csharp
[Register("IntentHandler")]
public partial class IntentHandler : INExtension, IINNotebookDomainHandling
{
  protected IntentHandler(IntPtr handle) : base(handle)
  {}
  public override NSObject GetHandler(INIntent intent)
  {
    // This is the default implementation.  If you want different objects to handle different intents,
    // you can override this and return the handler you want for that particular intent.
    return this;
  }
  // add intent handlers here!
}
```

Класс должен наследоваться от `INExtension`, так как в примере происходит обработка списков и заметки целей, также реализует `IINNotebookDomainHandling`.

> [!NOTE]
> - В .NET для интерфейсов с заглавной буквы префиксом имеется соглашение `I`, которой соответствует Xamarin при привязке протоколы из пакета SDK.
> - Xamarin также сохраняет имена типов из iOS и Apple использует первые два символа в именах типов с учетом платформы, к которой принадлежит тип.
> - Для `Intents` framework, типы с префиксом `IN*` (например) `INExtension`), но это _не_ интерфейсов.
> - Также следует, что протоколы (которые становятся интерфейсов в C#) в конечном итоге два `I`s, такие как `IINAddTasksIntentHandling`.

#### <a name="handling-intents"></a>Способы обработки

Каждая цель (Добавить задачу, задайте атрибут задачи, и т. д) реализуется в одном методе аналогично показанному ниже. Метод должен выполнить три основные функции:

1. **Обрабатывает назначение** — синтаксический анализ по Siri данные становятся доступными в `intent` объекта, зависящие от типа цели. Приложение может пройти проверку с помощью необязательно `Resolve*` методы.
2. **Проверка и обновление хранилища данных** — сохранение данных в файловую систему (с помощью групп приложений iOS основного приложения можно также доступа к нему) или через сетевой запрос.
3. **Укажите ответа** — использование `completion` обработчик отправить ответ Siri для чтения и отображения для пользователя:

```csharp
public void HandleCreateTaskList(INCreateTaskListIntent intent, Action<INCreateTaskListIntentResponse> completion)
{
  var list = TaskList.FromIntent(intent);
  // TODO: have to create the list and tasks... in your app data store
  var response = new INCreateTaskListIntentResponse(INCreateTaskListIntentResponseCode.Success, null)
  {
    CreatedTaskList = list
  };
  completion(response);
}
```

Обратите внимание, что `null` передается как второй параметр в ответ — это параметр действия пользователя, а если он не задан, будет использоваться значение по умолчанию.
Можно задать тип пользовательского действия, при условии, что ваше приложение iOS поддерживает его через `NSUserActivityTypes` ключа в **Info.plist**. Затем можно этот случай при открытии приложения и выполнения определенных операций (например, открытие контроллер соответствующего представления и загрузка данных из операции Siri).

Пример также кодируется `Success` результат, но в реальных сценариях должны быть добавлены соответствующие сообщения об ошибках.

### <a name="test-phrases"></a>Тестирование фраз

В примере приложения должны работать следующих фраз теста:

- «Обеспечить список покупок с яблоки "Бананы" и Груши в TasksNotes»
- «Добавить задачи WWDC в TasksNotes»
- «Добавить задачу WWDC список обучения в TasksNotes»
- «Пометить посетить WWDC как завершенный в TasksNotes»
- «В TasksNotes напомнить купить iphone при получении Главная»
- «Пометить покупке iPhone как завершенный в TasksNotes»
- «Напомнить оставьте Домашняя страница в 8: 00 в TasksNotes»

![Создать новый список пример](sirikit-images/createtasklist-sml.png) ![Набор задач, как полный пример](sirikit-images/settaskattribute-sml.png)

> [!NOTE]
> Поддерживает симулятор iOS 11 тестирование с помощью Siri (в отличие от более ранних версий).
>
> Если тестирование на реальном устройстве, не забудьте настроить ваш код приложения и профили для поддержки SiriKit подготовки.

<a name="alternativenames" />

## <a name="alternative-names"></a>Альтернативные имена

Эта новая функция iOS 11 означает, что можно назначить альтернативные имена для вашего приложения, чтобы помочь пользователям запускать правильно с Siri. Добавьте следующие разделы для **Info.plist** файл проекта приложения iOS:

![Info.plist отображение приложения альтернативное имя ключей и значений](sirikit-images/alternative-names.png)

В наборе имена альтернативные приложения следующих фраз также будет работать для примера приложения (которая называется фактически **TasksNotes**):

- «Для создания списка яблоки "Бананы" и Груши в продуктовом _MonkeyNotes_»
- «Добавить задачу WWDC в _MonkeyTodo_»


## <a name="troubleshooting"></a>Устранение неполадок

Некоторые ошибки, которые могут возникнуть во время выполнения образца или добавлении SiriKit в собственных приложениях:

### <a name="nsinternalinconsistencyexception"></a>NSInternalInconsistencyException

_Objective-C исключение.  Имя: NSInternalInconsistencyException причина: использование класса < INPreferences: 0x60400082ff00 > из приложения требуется com.apple.developer.siri права. Включена возможность Siri в своем проекте Xcode?_

- SiriKit установлен в **Entitlements.plist**.
- **Entitlements.plist** настраивается в **параметры проекта > сборки > подписывание пакета iOS**.

  [![Параметры проекта, в том, что правильно установить права](sirikit-images/set-entitlements-sml.png)](sirikit-images/set-entitlements.png#lightbox)

- (для развертывания устройства) Включить SiriKit имеет идентификатор приложения и подготовительного профиля загружены.


## <a name="related-links"></a>Связанные ссылки

- [SiriKit (Apple)](https://developer.apple.com/documentation/sirikit)
- [Образец SiriKit TasksNotes](https://developer.xamarin.com/samples/monotouch/ios11/SiriKitSample/)
- [Что такое New в SiriKit (WWDC) (видео)](https://developer.apple.com/videos/play/wwdc2017/214/)
