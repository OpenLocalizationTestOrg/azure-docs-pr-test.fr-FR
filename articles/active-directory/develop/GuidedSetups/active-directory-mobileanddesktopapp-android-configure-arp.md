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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="688b5-103">Ajouter une application de l’application hello d’enregistrement d’informations tooyour</span><span class="sxs-lookup"><span data-stu-id="688b5-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="688b5-104">Dans cette étape, vous avez besoin d’un projet de tooyour tooadd hello ID Client.</span><span class="sxs-lookup"><span data-stu-id="688b5-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="688b5-105">Ouvrez `MainActivity` (sous `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="688b5-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="688b5-106">Remplacez la ligne hello commençant par `final static String CLIENT_ID` avec :</span><span class="sxs-lookup"><span data-stu-id="688b5-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="688b5-107">Ouvrez `app` > `manifests` > `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="688b5-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="688b5-108">Ajouter hello suivant activité trop`manifest\application` nœud.</span><span class="sxs-lookup"><span data-stu-id="688b5-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="688b5-109">Ce Registre une `BrowserTabActivity` tooallow hello tooresume du système d’exploitation de votre application après l’achèvement de l’authentification de hello :</span><span class="sxs-lookup"><span data-stu-id="688b5-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

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

### <a name="what-is-next"></a><span data-ttu-id="688b5-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="688b5-110">What is Next</span></span>

[<span data-ttu-id="688b5-111">Test et validation</span><span class="sxs-lookup"><span data-stu-id="688b5-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
