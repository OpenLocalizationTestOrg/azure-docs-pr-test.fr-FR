---
title: "Clonage d’application web à l’aide du portail Azure"
description: "Découvrez comment cloner vos applications web vers de nouvelles applications web à l’aide du portail Azure."
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="360d1-103">Clonage de l’application Azure App Service à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="360d1-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="360d1-104">La fonctionnalité de clonage dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) vous permet de cloner facilement des applications web existantes vers une application nouvellement créée dans une autre région ou dans la même région.</span><span class="sxs-lookup"><span data-stu-id="360d1-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="360d1-105">Les utilisateurs peuvent ainsi déployer de nombreuses applications dans différentes régions.</span><span class="sxs-lookup"><span data-stu-id="360d1-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="360d1-106">Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="360d1-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="360d1-107">Cette nouvelle fonctionnalité utilise les mêmes limitations que la fonctionnalité de sauvegarde des applications web. Pour plus d’informations, consultez l’article [Sauvegarder une application web dans Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="360d1-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="360d1-108">Clonage d’une application existante</span><span class="sxs-lookup"><span data-stu-id="360d1-108">Cloning an existing App</span></span>
<span data-ttu-id="360d1-109">L’application web doit être exécutée en mode **Premium** pour vous permettre de créer un clone de l’application web.</span><span class="sxs-lookup"><span data-stu-id="360d1-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="360d1-110">Dans le [portail Azure](https://portal.azure.com/), ouvrez le panneau de votre application web.</span><span class="sxs-lookup"><span data-stu-id="360d1-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="360d1-111">Cliquez sur **Outils**.</span><span class="sxs-lookup"><span data-stu-id="360d1-111">Click **Tools**.</span></span> <span data-ttu-id="360d1-112">Ensuite, dans le panneau **Outils**, cliquez sur **Cloner l’application**.</span><span class="sxs-lookup"><span data-stu-id="360d1-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="360d1-113">Si l’application web n’est pas en mode **Premium** , vous recevez un message indiquant les modes pris en charge pour le clonage d’applications.</span><span class="sxs-lookup"><span data-stu-id="360d1-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="360d1-114">À ce stade, vous avez la possibilité de sélectionner **Mise à niveau**.</span><span class="sxs-lookup"><span data-stu-id="360d1-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="360d1-115">Dans le panneau **Cloner l’application** , entrez un nom pour la nouvelle application web, le groupe de ressources et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="360d1-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="360d1-116">L’utilisateur pourra également choisir de cloner plusieurs paramètres de l’application web source.</span><span class="sxs-lookup"><span data-stu-id="360d1-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="360d1-117">Après avoir cliqué sur **Créer** , la plateforme commence à travailler sur la création d’un clone de l’application web source.</span><span class="sxs-lookup"><span data-stu-id="360d1-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="360d1-118">Clonage d’une application existante vers un App Service Environment</span><span class="sxs-lookup"><span data-stu-id="360d1-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="360d1-119">Dans le panneau **Cloner l’application** , le client pourra choisir un pool d’applications dans un environnement App Service existant.</span><span class="sxs-lookup"><span data-stu-id="360d1-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="360d1-120">Restrictions actuelles</span><span class="sxs-lookup"><span data-stu-id="360d1-120">Current Restrictions</span></span>
<span data-ttu-id="360d1-121">Cette fonctionnalité en est actuellement à sa version préliminaire. Nous nous efforçons d’ajouter de nouvelles fonctionnalités au fil du temps. La liste suivante répertorie les restrictions connues de la prise en charge actuelle du clonage d’application dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="360d1-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="360d1-122">Les paramètres d’Azure Traffic Manager ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="360d1-123">Les paramètres de mise à l’échelle automatique ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="360d1-124">Les paramètres de planification de sauvegarde ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="360d1-125">Les paramètres de réseau virtuel ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="360d1-126">Application Insights n’est pas automatiquement configuré dans l’application web de destination</span><span class="sxs-lookup"><span data-stu-id="360d1-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="360d1-127">Les paramètres d’authentification simple ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="360d1-128">Les paramètres d’extension Kudu ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="360d1-129">Les règles TiP ne sont pas clonées.</span><span class="sxs-lookup"><span data-stu-id="360d1-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="360d1-130">Les contenus de la base de données ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="360d1-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="360d1-131">Références</span><span class="sxs-lookup"><span data-stu-id="360d1-131">References</span></span>
* [<span data-ttu-id="360d1-132">Clonage d’application web à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="360d1-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="360d1-133">Sauvegarde d’une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="360d1-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="360d1-134">Comment créer un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="360d1-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="360d1-135">Créer une application web dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="360d1-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="360d1-136">Présentation de l'environnement App Service</span><span class="sxs-lookup"><span data-stu-id="360d1-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
