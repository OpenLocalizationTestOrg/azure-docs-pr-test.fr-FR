---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - Config | Documents Microsoft
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="5c8ea-103">Configurer votre application de Web ASP.NET avec les informations d’inscription de l’application hello</span><span class="sxs-lookup"><span data-stu-id="5c8ea-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="5c8ea-104">Dans cette étape, vous configurerez votre toouse projet SSL et ensuite utiliser hello URL SSL tooconfigure des informations d’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="5c8ea-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="5c8ea-105">Après cela, ajoutez l’application hello' solution tooyour des informations d’inscription via *web.config*.</span><span class="sxs-lookup"><span data-stu-id="5c8ea-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="5c8ea-106">Dans l’Explorateur de solutions, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4)</span><span class="sxs-lookup"><span data-stu-id="5c8ea-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="5c8ea-107">Modification `SSL Enabled` trop`True`</span><span class="sxs-lookup"><span data-stu-id="5c8ea-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="5c8ea-108">Copier la valeur hello à partir de `SSL URL` ci-dessus et collez-le dans hello `Redirect URL` champ haut hello de cette page, puis cliquez sur *mise à jour*:</span><span class="sxs-lookup"><span data-stu-id="5c8ea-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="5c8ea-109">![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="5c8ea-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="5c8ea-110">Ajoutez hello qui suit dans `web.config` fichier situé dans le dossier racine, sous la section `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="5c8ea-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
