---
title: "Clonage d’application web à l’aide de PowerShell"
description: "Découvrez comment cloner vos applications web vers de nouvelles applications web à l’aide de PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="679c9-103">Clonage de l’application Azure App Service à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="679c9-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="679c9-104">Avec la publication de Microsoft Azure PowerShell version 1.1.0, une nouvelle option a été ajoutée à l’applet de commande New-AzureRMWebApp, qui permet à l’utilisateur de cloner une application web existante à une application qui vient d’être créée dans une autre région ou dans la même région.</span><span class="sxs-lookup"><span data-stu-id="679c9-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="679c9-105">Les utilisateurs peuvent ainsi déployer de nombreuses applications dans différentes régions.</span><span class="sxs-lookup"><span data-stu-id="679c9-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="679c9-106">Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="679c9-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="679c9-107">Cette nouvelle fonctionnalité utilise les mêmes limitations que la fonctionnalité de sauvegarde des applications web. Pour plus d’informations, consultez l’article [Sauvegarder une application web dans Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="679c9-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="679c9-108">Pour savoir comment utiliser les applets de commande Azure PowerShell basées sur Azure Resource Manager pour gérer vos applications web, consultez [Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="679c9-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="679c9-109">Clonage d’une application existante</span><span class="sxs-lookup"><span data-stu-id="679c9-109">Cloning an existing App</span></span>
<span data-ttu-id="679c9-110">Scénario : un utilisateur souhaite cloner le contenu d’une application web du Sud du centre des États-Unis vers une nouvelle application web de la région Nord du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="679c9-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="679c9-111">Ce peut être effectué à l’aide de la version Azure Resource Manager de l’applet de commande PowerShell pour créer une application web avec l’option -SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="679c9-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="679c9-112">Si nous connaissons le nom du groupe de ressources qui contient l’application web source, nous pouvons utiliser la commande PowerShell suivante pour obtenir les informations de l’application web source (dans ce cas nommée source-webapp) :</span><span class="sxs-lookup"><span data-stu-id="679c9-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="679c9-113">Pour créer un plan App Service, nous pouvons utiliser la commande New-AzureRmAppServicePlan comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="679c9-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="679c9-114">À l’aide de la commande New-AzureRmWebApp, nous pouvons créer l’application web dans la région Nord du centre des États-Unis et la lier à un plan App Service existant de niveau Premium. Par ailleurs, nous pouvons utiliser le même groupe de ressources que l’application web source ou en définir un nouveau, comme le montre le code suivant :</span><span class="sxs-lookup"><span data-stu-id="679c9-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="679c9-115">Pour cloner une application web existante, y compris le déploiement de tous les emplacements, l’utilisateur doit utiliser le paramètre IncludeSourceWebAppSlots, la commande PowerShell suivante illustre l’utilisation de ce paramètre avec la commande New-AzureRmWebApp :</span><span class="sxs-lookup"><span data-stu-id="679c9-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="679c9-116">Pour cloner une application web existante dans la même région, l’utilisateur doit créer un groupe de ressources et un plan de service d’application dans la même région, puis utiliser la commande PowerShell suivante pour cloner l’application web :</span><span class="sxs-lookup"><span data-stu-id="679c9-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="679c9-117">Clonage d’une application existante vers un App Service Environment</span><span class="sxs-lookup"><span data-stu-id="679c9-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="679c9-118">Scénario : un utilisateur souhaite cloner le contenu d’une application web du Sud du centre des États-Unis vers une nouvelle application web d’un App Service Environment (ASE) existant.</span><span class="sxs-lookup"><span data-stu-id="679c9-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="679c9-119">Si nous connaissons le nom du groupe de ressources qui contient l’application web source, nous pouvons utiliser la commande PowerShell suivante pour obtenir les informations de l’application web source (dans ce cas nommée source-webapp) :</span><span class="sxs-lookup"><span data-stu-id="679c9-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="679c9-120">S’il connaît le nom de l’environnement ASE et le nom du groupe de ressources auquel l’ASE appartient, l’utilisateur peut exécuter la commande New-AzureRmWebApp pour créer l’application web dans l’environnement ASE, comme le montre le code suivant :</span><span class="sxs-lookup"><span data-stu-id="679c9-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="679c9-121">Le paramètre -Location est requis en raison de l’héritage, mais il est ignoré dans le cas de la création d’une application dans un environnement ASE.</span><span class="sxs-lookup"><span data-stu-id="679c9-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="679c9-122">Clonage d’un emplacement d’application existant</span><span class="sxs-lookup"><span data-stu-id="679c9-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="679c9-123">Scénario : un utilisateur souhaite cloner un emplacement d’application web existant vers une nouvelle application web ou un nouvel emplacement d’application web.</span><span class="sxs-lookup"><span data-stu-id="679c9-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="679c9-124">La nouvelle application web peut résider dans la même région que l’emplacement d’application web d’origine ou dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="679c9-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="679c9-125">Si nous connaissons le nom du groupe de ressources qui contient l’application web source, vous pouvons utiliser la commande PowerShell suivante pour obtenir les informations de l’emplacement d’application web source (dans ce cas nommé source-webappslot) lié à source-webapp de l’application web :</span><span class="sxs-lookup"><span data-stu-id="679c9-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="679c9-126">Le code suivant illustre la création d’un clone de l’application web source vers une nouvelle application web :</span><span class="sxs-lookup"><span data-stu-id="679c9-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="679c9-127">Configuration de Traffic Manager lors du clonage d’une application</span><span class="sxs-lookup"><span data-stu-id="679c9-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="679c9-128">La création d’applications web sur plusieurs régions et la configuration d’Azure Traffic Manager pour acheminer le trafic vers toutes les applications web constituent un scénario contribuant largement à garantir que les applications client sont hautement disponibles. Au moment de cloner une application web existante, vous avez la possibilité de connecter les deux applications web à un nouveau profil de gestionnaire de trafic ou à un profil existant. Notez que seule la version Azure Resource manager de Traffic Manager est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="679c9-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="679c9-129">Création d’un profil Traffic Manager lors du clonage d’une application</span><span class="sxs-lookup"><span data-stu-id="679c9-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="679c9-130">Scénario : un utilisateur souhaite cloner une application web vers une autre région tout en configurant un profil Traffic Manager Azure Resource Manager qui inclut les deux applications web.</span><span class="sxs-lookup"><span data-stu-id="679c9-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="679c9-131">Le code suivant illustre la création d’un clone de l’application web source vers une nouvelle application web tout en configurant un nouveau profil Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="679c9-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="679c9-132">Ajout d’une nouvelle application web clonée à un profil Traffic Manager existant</span><span class="sxs-lookup"><span data-stu-id="679c9-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="679c9-133">Scénario : un utilisateur dispose déjà d’un profil Traffic Manager Azure Resource Manager auquel il souhaite ajouter les deux applications web comme points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="679c9-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="679c9-134">Pour ce faire, nous devons tout d’abord assembler l’ID de profil Traffic Manager existant. Nous devons disposer de l’ID d’abonnement, du nom de groupe de ressources et du nom du profil Traffic Manager existant.</span><span class="sxs-lookup"><span data-stu-id="679c9-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="679c9-135">Le code suivant illustre la création d’un clone de l’application web source vers une nouvelle application web tout en les ajoutant à un profil Traffic Manager existant :</span><span class="sxs-lookup"><span data-stu-id="679c9-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="679c9-136">Restrictions actuelles</span><span class="sxs-lookup"><span data-stu-id="679c9-136">Current Restrictions</span></span>
<span data-ttu-id="679c9-137">Cette fonctionnalité en est actuellement à sa version préliminaire. Nous nous efforçons d’ajouter de nouvelles fonctionnalités au fil du temps. La liste suivante répertorie les restrictions connues de la version actuelle du clonage d’application :</span><span class="sxs-lookup"><span data-stu-id="679c9-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="679c9-138">Les paramètres de mise à l’échelle automatique ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="679c9-139">Les paramètres de planification de sauvegarde ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="679c9-140">Les paramètres de réseau virtuel ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="679c9-141">Application Insights n’est pas automatiquement configuré dans l’application web de destination</span><span class="sxs-lookup"><span data-stu-id="679c9-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="679c9-142">Les paramètres d’authentification simple ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="679c9-143">Les paramètres d’extension Kudu ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="679c9-144">Les règles TiP ne sont pas clonées.</span><span class="sxs-lookup"><span data-stu-id="679c9-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="679c9-145">Les contenus de la base de données ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="679c9-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="679c9-146">Références</span><span class="sxs-lookup"><span data-stu-id="679c9-146">References</span></span>
* [<span data-ttu-id="679c9-147">Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure</span><span class="sxs-lookup"><span data-stu-id="679c9-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="679c9-148">Clonage d’application web à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="679c9-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="679c9-149">Sauvegarde d’une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="679c9-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="679c9-150">Prise en charge d’Azure Resource Manager pour la version préliminaire d’Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="679c9-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="679c9-151">Présentation de l'environnement App Service</span><span class="sxs-lookup"><span data-stu-id="679c9-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="679c9-152">Utilisation d’Azure PowerShell avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="679c9-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

