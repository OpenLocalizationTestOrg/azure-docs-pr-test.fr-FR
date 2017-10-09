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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="82d53-103">Créer une application (Express)</span><span class="sxs-lookup"><span data-stu-id="82d53-103">Create an application (Express)</span></span>
<span data-ttu-id="82d53-104">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="82d53-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="82d53-105">Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="82d53-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="82d53-106">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="82d53-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="82d53-107">Assurez-vous que l’option hello pour le programme d’installation interactive est activée</span><span class="sxs-lookup"><span data-stu-id="82d53-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="82d53-108">Suivez les instructions de hello tooadd une application de tooyour URL de redirection</span><span class="sxs-lookup"><span data-stu-id="82d53-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="82d53-109">Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)</span><span class="sxs-lookup"><span data-stu-id="82d53-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="82d53-110">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="82d53-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="82d53-111">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application</span><span class="sxs-lookup"><span data-stu-id="82d53-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="82d53-112">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="82d53-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="82d53-113">Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée</span><span class="sxs-lookup"><span data-stu-id="82d53-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="82d53-114">Cliquez sur `Add Platform`, puis sélectionnez `Web`.</span><span class="sxs-lookup"><span data-stu-id="82d53-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="82d53-115">Revenir en arrière tooVisual Studio et, dans l’Explorateur de solutions, sélectionnez le projet de hello et examinez les fenêtre de propriétés de hello (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4)</span><span class="sxs-lookup"><span data-stu-id="82d53-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="82d53-116">Changent avec SSL activé`True`</span><span class="sxs-lookup"><span data-stu-id="82d53-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="82d53-117">Copiez hello URL SSL et ajouter cette liste de toohello URL de l’URL de redirection dans la liste du portail hello d’inscription d’URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="82d53-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="82d53-119">Ajoutez hello qui suit dans `web.config` situé dans le dossier racine de hello section hello `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="82d53-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="82d53-120">Remplacez `ClientId` par hello Id d’Application vous venez d’enregistrer</span><span class="sxs-lookup"><span data-stu-id="82d53-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="82d53-121">Remplacez `redirectUri` par hello URL SSL de votre projet</span><span class="sxs-lookup"><span data-stu-id="82d53-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
