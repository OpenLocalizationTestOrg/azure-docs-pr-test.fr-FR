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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Créer une application (Express)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est activée
4.  Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application
2. Entrez un nom pour votre application, ainsi que votre adresse e-mail. 
3. Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée
4. Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et appuyez sur Save (Enregistrer).
5.  Ouvrez `MainActivity` (sous `app` > `java` > *`{host}.{namespace}`*).
6.  Remplacez hello *[entrer une application hello Id ici]* dans la ligne hello commençant par `final static String CLIENT_ID` avec l’ID d’application hello enregistré :

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Ouvrez `AndroidManifest.xml` (sous `app`  >  `manifests`) hello ajouter suivant activité trop`manifest\application` nœud. Cela permet d’enregistrer un `BrowserTabActivity` tooallow hello tooresume du système d’exploitation de votre application après l’achèvement de l’authentification de hello :
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
Bonjour `BrowserTabActivity`, remplacez `[Enter hello application Id here]` avec l’ID d’application hello.
</li>
</ol>
