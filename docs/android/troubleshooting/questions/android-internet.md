---
title: "Почему мой Android выпуска не удается подключиться к Интернету?"
ms.topic: article
ms.prod: xamarin
ms.assetid: A6FE770B-A19A-4BF8-95E9-2CF880D4AFC5
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.openlocfilehash: 60da469001f8a9641aff7e014add5f58bdb389cb
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="why-cant-my-android-release-build-connect-to-the-internet"></a>Почему мой Android выпуска не удается подключиться к Интернету?

## <a name="cause"></a>Причина

Наиболее распространенной причиной этой проблемы является, **INTERNET** разрешение автоматически включается в отладочном построении, но должен быть установлен вручную для сборки выпуска. Это так, как разрешение Интернет используется чтобы отладчик мог присоединиться к процессу, как описано для «Этому» [здесь](~/android/deploy-test/building-apps/build-process.md).


## <a name="fix"></a>Исправление

Чтобы устранить проблему, может потребоваться разрешение Интернета в Android манифеста. Это можно сделать через редактор манифестов или sourcecode манифеста:

-   Исправить в редактор: В проекте Android перейдите в **свойства -> AndroidManifest.xml -> требуемые разрешения** и проверьте **Интернета**

-   Исправьте в Sourcecode: Откройте в редакторе исходного AndroidManifest и добавьте тег разрешений внутри `<Manifest>` теги:

    ```xml
    <Manifest>
    ...
    <uses-permission android:name="android.permission.INTERNET" />
    </Manifest>
    ```