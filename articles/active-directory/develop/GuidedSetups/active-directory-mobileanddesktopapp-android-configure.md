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
## <a name="create-an-application-express"></a><span data-ttu-id="21cd1-103">Créer une application (Express)</span><span class="sxs-lookup"><span data-stu-id="21cd1-103">Create an application (Express)</span></span>
<span data-ttu-id="21cd1-104">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="21cd1-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="21cd1-105">Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="21cd1-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="21cd1-106">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="21cd1-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="21cd1-107">Assurez-vous que l’option hello pour le programme d’installation interactive est activée</span><span class="sxs-lookup"><span data-stu-id="21cd1-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="21cd1-108">Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code</span><span class="sxs-lookup"><span data-stu-id="21cd1-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="21cd1-109">Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)</span><span class="sxs-lookup"><span data-stu-id="21cd1-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="21cd1-110">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="21cd1-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="21cd1-111">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application</span><span class="sxs-lookup"><span data-stu-id="21cd1-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="21cd1-112">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="21cd1-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="21cd1-113">Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée</span><span class="sxs-lookup"><span data-stu-id="21cd1-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="21cd1-114">Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et appuyez sur Save (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="21cd1-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="21cd1-115">Ouvrez `MainActivity` (sous `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="21cd1-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="21cd1-116">Remplacez hello *[entrer une application hello Id ici]* dans la ligne hello commençant par `final static String CLIENT_ID` avec l’ID d’application hello enregistré :</span><span class="sxs-lookup"><span data-stu-id="21cd1-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="21cd1-117">Ouvrez `AndroidManifest.xml` (sous `app`  >  `manifests`) hello ajouter suivant activité trop`manifest\application` nœud.</span><span class="sxs-lookup"><span data-stu-id="21cd1-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="21cd1-118">Cela permet d’enregistrer un `BrowserTabActivity` tooallow hello tooresume du système d’exploitation de votre application après l’achèvement de l’authentification de hello :</span><span class="sxs-lookup"><span data-stu-id="21cd1-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="21cd1-119">Bonjour `BrowserTabActivity`, remplacez `[Enter hello application Id here]` avec l’ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="21cd1-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
