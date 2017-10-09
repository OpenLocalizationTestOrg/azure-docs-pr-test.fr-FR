---
title: "mise en route d’aaaAzure AD v2 iOS - configurer | Documents Microsoft"
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="5c56c-103">Créer une application (Express)</span><span class="sxs-lookup"><span data-stu-id="5c56c-103">Create an application (Express)</span></span>
<span data-ttu-id="5c56c-104">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="5c56c-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="5c56c-105">Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="5c56c-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="5c56c-106">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="5c56c-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="5c56c-107">Assurez-vous que l’option hello pour le programme d’installation interactive est activée</span><span class="sxs-lookup"><span data-stu-id="5c56c-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="5c56c-108">Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code</span><span class="sxs-lookup"><span data-stu-id="5c56c-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="5c56c-109">Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)</span><span class="sxs-lookup"><span data-stu-id="5c56c-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="5c56c-110">Accédez trop[portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="5c56c-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="5c56c-111">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="5c56c-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="5c56c-112">Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée</span><span class="sxs-lookup"><span data-stu-id="5c56c-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="5c56c-113">Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et cliquez sur `Save`.</span><span class="sxs-lookup"><span data-stu-id="5c56c-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="5c56c-114">Revenir en arrière tooXcode.</span><span class="sxs-lookup"><span data-stu-id="5c56c-114">Go back tooXcode.</span></span> <span data-ttu-id="5c56c-115">Dans `ViewController.swift`, remplacez la ligne hello commençant par '`let kClientID`' avec l’ID d’application hello enregistré :</span><span class="sxs-lookup"><span data-stu-id="5c56c-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="5c56c-116">Touche CTRL enfoncée et cliquez sur <code>Info.plist</code> toobring haut du menu contextuel de hello, puis cliquez sur : <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="5c56c-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="5c56c-117">Sous hello <code>dict</code> nœud racine, ajoutez hello :</span><span class="sxs-lookup"><span data-stu-id="5c56c-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="5c56c-118">Remplacez <i> <code>[Your_Application_Id_Here]</code> </i> avec hello Id d’Application vous venez d’enregistrer</span><span class="sxs-lookup"><span data-stu-id="5c56c-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
