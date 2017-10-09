---
title: aaaAzure AD v2 Windows Desktop mise en route - Config | Documents Microsoft
description: "Cet article explique comment une application de bureau Windows .NET (XAML) peut obtenir un jeton d’accès et appeler une API protégée par un point de terminaison Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="a025b-104">Créer une application (Express)</span><span class="sxs-lookup"><span data-stu-id="a025b-104">Create an application (Express)</span></span>
<span data-ttu-id="a025b-105">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="a025b-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="a025b-106">Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="a025b-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="a025b-107">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="a025b-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="a025b-108">Assurez-vous que l’option hello pour le programme d’installation interactive est activée</span><span class="sxs-lookup"><span data-stu-id="a025b-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="a025b-109">Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code</span><span class="sxs-lookup"><span data-stu-id="a025b-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="a025b-110">Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)</span><span class="sxs-lookup"><span data-stu-id="a025b-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="a025b-111">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="a025b-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="a025b-112">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application</span><span class="sxs-lookup"><span data-stu-id="a025b-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="a025b-113">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="a025b-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="a025b-114">Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée</span><span class="sxs-lookup"><span data-stu-id="a025b-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="a025b-115">Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et appuyez sur Save (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="a025b-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="a025b-116">Copiez hello GUID dans l’ID de l’Application, revenez en arrière tooVisual Studio, ouvrez `App.xaml.cs` et remplacez `your_client_id_here` par hello ID d’Application vous venez d’enregistrer :</span><span class="sxs-lookup"><span data-stu-id="a025b-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
