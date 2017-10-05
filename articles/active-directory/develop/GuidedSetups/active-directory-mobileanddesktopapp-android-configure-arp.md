---
title: "Prise en main d’Azure AD v2 avec les applications Android - Configuration | Documents Microsoft"
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler l’API Microsoft Graph ou des API qui nécessitent des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
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
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="f81c4-103">Ajouter les informations d’inscription de l’application à votre application</span><span class="sxs-lookup"><span data-stu-id="f81c4-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="f81c4-104">Dans cette étape, vous devez ajouter l’ID client à votre projet.</span><span class="sxs-lookup"><span data-stu-id="f81c4-104">In this step, you need to add the Client ID to your project.</span></span>

1.  <span data-ttu-id="f81c4-105">Ouvrez `MainActivity` (sous `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="f81c4-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="f81c4-106">Remplacez la ligne commençant par `final static String CLIENT_ID` par :</span><span class="sxs-lookup"><span data-stu-id="f81c4-106">Replace the line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. <span data-ttu-id="f81c4-107">Ouvrez `app` > `manifests` > `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="f81c4-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="f81c4-108">Ajoutez l’activité suivante au nœud `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="f81c4-108">Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="f81c4-109">Cette opération inscrit une activité `BrowserTabActivity` pour autoriser le système d’exploitation à reprendre l’exécution de votre application une fois l’authentification effectuée :</span><span class="sxs-lookup"><span data-stu-id="f81c4-109">This register a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="f81c4-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f81c4-110">What is Next</span></span>

[<span data-ttu-id="f81c4-111">Test et validation</span><span class="sxs-lookup"><span data-stu-id="f81c4-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
