---
title: "Prise en main d’Azure AD v2 avec les applications de serveur web ASP.NET - Configuration | Microsoft Docs"
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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="b6e87-103">Configurer votre application Web ASP.NET avec les informations d’inscription de l’application</span><span class="sxs-lookup"><span data-stu-id="b6e87-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="b6e87-104">Dans cette étape, vous allez configurer votre projet pour utiliser SSL, puis vous servir de l’URL SSL pour configurer les informations d’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="b6e87-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="b6e87-105">Ensuite, ajoutez les informations d’inscription de l’application à votre solution via *web.config*.</span><span class="sxs-lookup"><span data-stu-id="b6e87-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="b6e87-106">Dans l’Explorateur de solutions, sélectionnez le projet et examinez la fenêtre `Properties` (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4).</span><span class="sxs-lookup"><span data-stu-id="b6e87-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="b6e87-107">Remplacez `SSL Enabled` par `True` :</span><span class="sxs-lookup"><span data-stu-id="b6e87-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="b6e87-108">Copiez la valeur de `SSL URL` ci-dessus et collez-la dans le champ `Redirect URL` en haut de cette page, puis cliquez sur *Mettre à jour* :</span><span class="sxs-lookup"><span data-stu-id="b6e87-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="b6e87-109">![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="b6e87-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="b6e87-110">Ajoutez le code suivant dans le fichier `web.config` situé dans le dossier racine, sous la section `configuration\appSettings` :</span><span class="sxs-lookup"><span data-stu-id="b6e87-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
