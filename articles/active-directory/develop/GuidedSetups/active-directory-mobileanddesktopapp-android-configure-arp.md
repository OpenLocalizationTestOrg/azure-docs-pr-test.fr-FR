---
title: "aaaAzure AD v2 Android mise en route : configuration | Documents Microsoft"
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Ajouter une application de l’application hello d’enregistrement d’informations tooyour

Dans cette étape, vous avez besoin d’un projet de tooyour tooadd hello ID Client.

1.  Ouvrez `MainActivity` (sous `app` > `java` > *`{host}.{namespace}`*).
2.  Remplacez la ligne hello commençant par `final static String CLIENT_ID` avec :
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Ouvrez `app` > `manifests` > `AndroidManifest.xml`.
4. Ajouter hello suivant activité trop`manifest\application` nœud. Ce Registre une `BrowserTabActivity` tooallow hello tooresume du système d’exploitation de votre application après l’achèvement de l’authentification de hello :

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a>Étapes suivantes

[Test et validation](active-directory-mobileanddesktopapp-android-test.md)
