---
title: "Проверка подлинности веб-службы RESTful"
description: "Протокол HTTP поддерживает использование нескольких механизмов проверки подлинности для управления доступом к ресурсам. Обычная проверка подлинности предоставляет доступ к ресурсам только клиенты, которые имеют правильные учетные данные. В этой статье показано, как использовать обычную проверку подлинности для защиты доступа к ресурсам RESTful веб-службы."
ms.topic: article
ms.prod: xamarin
ms.assetid: 7B5FFDC4-F2AA-4B12-A30A-1DACC7FECBF1
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/22/2017
ms.openlocfilehash: 7aea74f95e8738cc415eaac3a5ac4f86b069d0f7
ms.sourcegitcommit: 61f5ecc5a2b5dcfbefdef91664d7460c0ee2f357
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/28/2018
---
# <a name="authenticating-a-restful-web-service"></a>Проверка подлинности веб-службы RESTful

_Протокол HTTP поддерживает использование нескольких механизмов проверки подлинности для управления доступом к ресурсам. Обычная проверка подлинности предоставляет доступ к ресурсам только клиенты, которые имеют правильные учетные данные. В этой статье показано, как использовать обычную проверку подлинности для защиты доступа к ресурсам RESTful веб-службы._

Сопутствующий образец приложения Xamarin.Forms использует размещенное Xamarin REST служба, предоставляющая доступ только для чтения к веб-службе. Таким образом операции, которые создание, обновление и удаление данных не изменится данным в приложении. Однако доступна в размещаемом версия службы REST *TodoRESTService* папку в пример приложения, а также инструкции по настройке службы можно найти существует. Этот ведущий версия службы REST предоставляет создания full, обновление, чтение и удаление доступа к данным.

> [!NOTE]
> В iOS 9 и более поздней версии безопасность транспорта приложения (ATS) обеспечивает безопасное соединение между Интернет-ресурсов (например, приложение серверных) и приложения, чтобы предотвратить случайное раскрытие конфиденциальных сведений. Поскольку ATS включена по умолчанию в приложениях, разработанных для iOS 9, все соединения будут применяться ATS требования безопасности. Если соединения не удовлетворяют этим требованиям, произойдет сбой с исключением.
> Если это не позволяет использовать ATS могут быть присоединены из `HTTPS` протокола и безопасную передачу Интернет-ресурсов. Это можно сделать путем обновления приложения **Info.plist** файла. Дополнительные сведения см. [безопасность транспорта приложения](~/ios/app-fundamentals/ats.md).

## <a name="authenticating-users-over-http"></a>Проверка подлинности пользователей по протоколу HTTP

Обычная проверка подлинности самый простой способ проверки подлинности, поддерживаемых HTTP и включает в себя клиент, отправляющий имя пользователя и пароль как текст незашифрованные в кодировке base64. Он работает следующим образом:

- Если веб-служба получает запрос на защищенный ресурс, он отклоняет запрос с кодом состояния HTTP 401 (доступ запрещен) и задает заголовок WWW-Authenticate ответа, как показано на следующей схеме:

![](rest-images/basic-authentication-fail.png "Сбой обычной проверки подлинности")

- Если веб-служба получает запрос на защищенный ресурс с `Authorization` правильно задать заголовок, web службы отвечает с кодом состояния HTTP 200, которые показывают, что запрос выполнен успешно, и что запрашиваемые данные находятся в ответе. Этот сценарий показан на следующей схеме:

![](rest-images/basic-authentication-success.png "Обычная проверка подлинности успешно")

> [!NOTE]
> Обычная проверка подлинности следует использовать только через HTTPS-соединение. При использовании подключения по протоколу HTTP, <code>Authorization</code> заголовок легко декодировать, если HTTP-трафика захвачен злоумышленником.

## <a name="specifying-basic-authentication-in-a-web-request"></a>Указание обычной проверки подлинности в веб-запроса

Использование обычной проверки подлинности указывается следующим образом:

1. «Основные» добавляется строка `Authorization` заголовок запроса.
1. Имя пользователя и пароль объединяются в строку в формате «имя», которое затем base64 закодированы и добавить `Authorization` заголовок запроса.

Таким образом «XamarinUser» имя пользователя и пароль «XamarinPassword», заголовок принимает следующий вид:

```csharp
Authorization: Basic WGFtYXJpblVzZXI6WGFtYXJpblBhc3N3b3Jk
```

`HttpClient` Класс может задавать `Authorization` значение заголовка на `HttpClient.DefaultRequestHeaders.Authorization` свойство. Поскольку `HttpClient` экземпляр существует в нескольких запросах `Authorization` заголовок нужно только задать один раз, а не при создания каждого запроса, как показано в следующем примере кода:

```csharp
public class RestService : IRestService
{
  HttpClient client;
  ...

  public RestService ()
  {
    var authData = string.Format ("{0}:{1}", Constants.Username, Constants.Password);
    var authHeaderValue = Convert.ToBase64String (Encoding.UTF8.GetBytes (authData));

    client = new HttpClient ();
    ...
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue ("Basic", authHeaderValue);
  }
  ...
}
```

Затем при запросе операции веб-службы запрос подписывается `Authorization` заголовка, указывающее, имеет ли пользователь разрешение для вызова операции.

> [!NOTE]
> Хотя образец службы REST учетные данные хранятся в виде константы, они не должны храниться незащищенный формат в опубликованном в приложении. [Xamarith.Auth](https://www.nuget.org/packages/Xamarin.Auth/) NuGet предоставляет функциональные возможности для безопасного хранения учетных данных. Дополнительные сведения см. [хранение и получение сведений о учетной записи на устройствах](~/xamarin-forms/data-cloud/authentication/oauth.md).


## <a name="processing-the-authorization-header-server-side"></a>Обработке на стороне сервера заголовок авторизации

Сопутствующий образца службы REST декорирует каждого действия с `[BasicAuthentication]` атрибута. Этот атрибут реализуется `BasicAuthenticationAttribute` класса в решении и используется для синтаксического анализа `Authorization` заголовок и определить допустимые учетные данные в кодировке base64, сравнивая их со значениями, сохраненными в *Web.config*. Хотя этот способ подходит для образца службы, требуется расширение общедоступный веб-службы.

В модуле обычной проверки подлинности, используемый службой IIS пользователи проходят проверку подлинности от учетных данных Windows. Таким образом пользователь должен иметь учетные записи для вашего домена. Тем не менее модель обычной проверки подлинности можно настроить таким образом, чтобы разрешить нестандартной проверки подлинности, где учетные записи проходят проверку подлинности от внешнего источника, например базы данных. Дополнительные сведения см. [обычной проверки подлинности в ASP.NET Web API](http://www.asp.net/web-api/overview/security/basic-authentication) на веб-сайте ASP.NET.

> [!NOTE]
> Обычная проверка подлинности не предназначен для управления ведением журнала. Таким образом для завершения сеанса является подход Стандартная обычной проверки подлинности для выхода.

## <a name="summary"></a>Сводка

В этой статье показано, как добавить обычную проверку подлинности на веб-запросы, выполненные с помощью приложения Xamarin.Forms `HttpClient` класса. Обычная проверка подлинности предоставляет доступ к ресурсам только клиенты, которые имеют правильные учетные данные. Дополнительные сведения об использовании [Xamarin.Auth](https://www.nuget.org/packages/Xamarin.Auth/) для управления процессом проверки подлинности в приложении Xamarin.Forms, чтобы пользователи использовали только Имея доступ к своим данным серверной части, в разделе [проверки подлинности пользователей с помощью поставщика удостоверений](~/xamarin-forms/data-cloud/authentication/oauth.md).


## <a name="related-links"></a>Связанные ссылки

- [TodoREST (пример)](https://developer.xamarin.com/samples/xamarin-forms/WebServices/TodoREST/)
- [Использование веб-службы RESTful](~/xamarin-forms/data-cloud/consuming/rest.md)
- [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)