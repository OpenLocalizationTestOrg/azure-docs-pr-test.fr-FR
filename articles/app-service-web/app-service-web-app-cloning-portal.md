---
title: "aaaWeb clonage d’application à l’aide du portail Azure"
description: "Découvrez comment tooclone votre toonew d’applications Web des applications Web à l’aide du portail Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="3ffbc-103">Clonage de l’application Azure App Service à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3ffbc-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="3ffbc-104">Hello fonctionnalité dans de clonage [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) vous permet de facilement cloner application web existante applications tooa qui vient d’être créé dans une autre région ou dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="3ffbc-105">Cela permet aux clients toodeploy un nombre d’applications sur différentes régions rapidement et facilement.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="3ffbc-106">Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="3ffbc-107">nouvelles utilisations de fonctionnalité Hello hello même limitations en tant que fonctionnalité de sauvegarde des applications Web, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3ffbc-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="3ffbc-108">Clonage d’une application existante</span><span class="sxs-lookup"><span data-stu-id="3ffbc-108">Cloning an existing App</span></span>
<span data-ttu-id="3ffbc-109">l’application Hello web doit s’exécuter dans hello **Premium** mode afin que vous toocreate un clone de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="3ffbc-110">Bonjour [Azure Portal](https://portal.azure.com/), ouvrez le panneau de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="3ffbc-111">Cliquez sur **Outils**.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-111">Click **Tools**.</span></span> <span data-ttu-id="3ffbc-112">Ensuite, dans hello **outils** panneau, cliquez sur **le clonage d’application**.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="3ffbc-113">Si l’application web hello n’est pas déjà hello **Premium** mode, vous recevrez un message indiquant les modes hello pris en charge pour le clonage de l’application.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="3ffbc-114">À ce stade, vous avez hello option tooselect **mise à niveau**.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="3ffbc-115">Bonjour **le clonage d’application** panneau fournir un nom d’application web hello, groupe de ressources et un Plan App Service.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="3ffbc-116">Également hello utilisateur sera en mesure de toochoose si tooclone un nombre de paramètres de l’application web source ou non.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="3ffbc-117">Après avoir cliqué sur **créer** plate-forme de hello va commencer à travailler sur la création d’un clone de l’application web de source hello.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="3ffbc-118">Le clonage d’un tooan d’application existant environnement App Service</span><span class="sxs-lookup"><span data-stu-id="3ffbc-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="3ffbc-119">Bonjour **le clonage d’application** panneau hello client dispose hello option toochoose un pool d’applications dans un environnement App Service existant.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="3ffbc-120">Restrictions actuelles</span><span class="sxs-lookup"><span data-stu-id="3ffbc-120">Current Restrictions</span></span>
<span data-ttu-id="3ffbc-121">Cette fonctionnalité est actuellement en version préliminaire, nous travaillons tooadd nouvelles fonctionnalités au fil du temps, hello suivant liste sont hello restrictions connues sur la prise en charge actuelle de hello au clonage de l’application dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="3ffbc-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="3ffbc-122">Les paramètres d’Azure Traffic Manager ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="3ffbc-123">Les paramètres de mise à l’échelle automatique ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="3ffbc-124">Les paramètres de planification de sauvegarde ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="3ffbc-125">Les paramètres de réseau virtuel ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="3ffbc-126">Application Insights ne sont pas automatiquement définies sur l’application web de destination hello</span><span class="sxs-lookup"><span data-stu-id="3ffbc-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="3ffbc-127">Les paramètres d’authentification simple ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="3ffbc-128">Les paramètres d’extension Kudu ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="3ffbc-129">Les règles TiP ne sont pas clonées.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="3ffbc-130">Les contenus de la base de données ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="3ffbc-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="3ffbc-131">Références</span><span class="sxs-lookup"><span data-stu-id="3ffbc-131">References</span></span>
* [<span data-ttu-id="3ffbc-132">Clonage d’application web à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ffbc-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="3ffbc-133">Sauvegarde d’une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3ffbc-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="3ffbc-134">Comment tooCreate un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="3ffbc-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="3ffbc-135">Créer une application web dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="3ffbc-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="3ffbc-136">Introduction tooApp environnement de Service</span><span class="sxs-lookup"><span data-stu-id="3ffbc-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
