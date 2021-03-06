---
title: Автоматическая подготовка
description: После успешной установки Xamarin.iOS следующим шагом в разработке приложений для iOS является подготовка устройства iOS. В этом руководстве описано, как использовать функцию автоматического подписывания для запроса сертификатов и профилей разработки.
ms.prod: xamarin
ms.assetid: 81FCB2ED-687C-40BC-ABF1-FB4303034D01
ms.technology: xamarin-ios
author: asb3993
ms.author: amburns
ms.date: 05/22/2018
ms.openlocfilehash: d324e469ba392b14c635990d607bf04c949ad5db
ms.sourcegitcommit: 9f8e7393019791bbd6af4fefaa24a1602adabb4e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2018
ms.locfileid: "34458584"
---
# <a name="automatic-provisioning"></a>Автоматическая подготовка

_Установив Xamarin.iOS для разработки приложений для iOS можно приступать к подготовке устройства iOS. В этом руководстве описано, как использовать функцию автоматического подписывания для запроса сертификатов и профилей разработки._

## <a name="requirements"></a>Требования

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

- Visual Studio для Mac 7.3 или более поздней версии
- Xcode 9 или более поздней версии

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

- Visual Studio 2017 версии 15.7 (или более поздней)

Вам потребуется подключение к узлу сборки Mac со следующими компонентами:

- Xcode 9 или более поздней версии

-----

## <a name="enabling-automatic-signing"></a>Включение автоматического подписывания

Прежде чем начинать процесс автоматического подписывания, следует убедиться, что в Visual Studio добавлен идентификатор Apple, как описано в руководстве [Управление учетными записями Apple](~/cross-platform/macios/apple-account-management.md). После добавления идентификатора Apple вы можете использовать любую связанную _команду_. Это позволяет создавать сертификаты, профили и другие идентификаторы для этой группы. На основе идентификатора команды также создается префикс для идентификатора приложения, который будет включен в профиль подготовки. Это позволяет компании Apple подтверждать вашу личность.

> [!IMPORTANT]
> Перед началом работы обязательно посетите сайт [iTunes Connect](https://itunesconnect.apple.com/) или [appleid.apple.com](https://appleid.apple.com), чтобы проверить, принята ли последняя версия политик учетных записей Apple. Если поступит соответствующий запрос, примите новые условия соглашений об использовании учетных записей от Apple. Если не приняты условия соглашения о конфиденциальности, вышедшего в мае 2018 г., при попытке подготовки устройства поступит следующее оповещение:
> ```
> Unexpected authentication failure. Reason: {
> "authType" : "sa"
>}
>```

Чтобы автоматически подписать приложение для развертывания на устройстве iOS, выполните указанные ниже действия:

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

1. Откройте проект iOS в Visual Studio для Mac.

2. Откройте файл **Info.plist**.

3. В разделе **Signing** (Подписывание) выберите **Automatic Provisioning** (Автоматическая подготовка):

    ![Раскрывающийся список для выбора команды](automatic-provisioning-images/image2.png)

4. Выберите свою команду в раскрывающемся списке **Team** (Команда).

6. Через несколько секунд будут созданы сертификат для подписи и профиль подготовки:

    ![успешное создание сертификата и профиля](automatic-provisioning-images/image5.png)

    Если автоматическое подписывание выполнить не удалось, на **панели автоматического подписывания** будет указана причина ошибки.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

1. Свяжите Visual Studio 2017 с компьютером Mac, как описано в руководстве [Связывание с компьютером Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md).

2. Откройте параметры подготовки, выбрав **Проект > Параметры подготовки к работе...**

3. Выберите схему **Автоматическая подготовка**:

    ![Выбор схемы автоматической подготовки](automatic-provisioning-images/prov4.png)

4. Выберите команду из поля со списком **Команда**, чтобы запустить процесс автоматического подписывания.

    ![Выбор команды](automatic-provisioning-images/prov3.png)

4. Будет запущен процесс автоматического подписывания. Затем Visual Studio попытается создать идентификатор приложения, профиль подготовки и удостоверение подписи для использования этих артефактов при подписывании. Процесс создания отображается в выходных данных сборки:

    ![Выходные данные сборки с создаваемыми артефактами](automatic-provisioning-images/prov5.png)

-----

## <a name="triggering-automatic-provisioning"></a>Активация автоматической подготовки

При включении автоматического подписывания Visual Studio для Mac при необходимости обновляет соответствующие артефакты при наступлении любого из следующих событий:

* Устройство iOS подключается к компьютеру Mac
    - При этом автоматически проверяется регистрация устройства на портале разработчика Apple. Если устройство не зарегистрировано, оно добавляется, и создается содержащий его профиль подготовки.
* Изменяется идентификатор пакета приложения.
    - При этом обновляется идентификатор приложения. Создается профиль подготовки, содержащий этот идентификатор приложения.
* В файле Entitlements.plist включается поддерживаемая возможность.
    - Эта возможность будет добавлена в идентификатор приложения, и будет создан профиль подготовки с обновленным идентификатором приложения.
    - В настоящее время поддерживаются не все возможности. Дополнительные сведения о поддерживаемых возможностях см. в руководстве [Работа с возможностями](~/ios/deploy-test/provisioning/capabilities/index.md).


## <a name="related-links"></a>Связанные ссылки

- [Бесплатная подготовка](~/ios/get-started/installation/device-provisioning/free-provisioning.md)
- [Распространение приложений](~/ios/deploy-test/app-distribution/index.md)
- [Устранение неполадок](~/ios/deploy-test/troubleshooting.md)
- [Руководство Apple. Распространение приложений](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html)
