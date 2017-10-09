---
title: "aaaWeb application clonage à l’aide de PowerShell"
description: "Découvrez comment tooclone vos applications Web de toonew les applications Web à l’aide de PowerShell."
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
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="dfa50-103">Clonage de l’application Azure App Service à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfa50-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="dfa50-104">Avec la version de hello de Microsoft Azure PowerShell version 1.1.0 une nouvelle option a été ajouté AzureRMWebApp tooNew qui donnerait hello utilisateur hello capacité tooclone une application existante tooa nouvellement créé d’application Web dans une autre région ou dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="dfa50-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="dfa50-105">Cela permet aux clients toodeploy un nombre d’applications sur différentes régions rapidement et facilement.</span><span class="sxs-lookup"><span data-stu-id="dfa50-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="dfa50-106">Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium.</span><span class="sxs-lookup"><span data-stu-id="dfa50-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="dfa50-107">nouvelles utilisations de fonctionnalité Hello hello même limitations en tant que fonctionnalité de sauvegarde des applications Web, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="dfa50-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="dfa50-108">toolearn sur l’utilisation du Gestionnaire de ressources Azure en fonction toomanage des applets de commande Azure PowerShell vérification de vos applications Web [Azure Resource Manager en fonction des commandes PowerShell pour l’application Web Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="dfa50-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="dfa50-109">Clonage d’une application existante</span><span class="sxs-lookup"><span data-stu-id="dfa50-109">Cloning an existing App</span></span>
<span data-ttu-id="dfa50-110">Scénario : Une application web existante dans la région Amérique du Sud, hello l’utilisateur souhaiterait tooclone hello contenu tooa nouvelle application web dans la région Amérique du Nord.</span><span class="sxs-lookup"><span data-stu-id="dfa50-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="dfa50-111">Cela peut être accompli à l’aide de la version du Gestionnaire de ressources Azure hello de toocreate d’applet de commande PowerShell hello une application web avec l’option - SourceWebApp de hello.</span><span class="sxs-lookup"><span data-stu-id="dfa50-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="dfa50-112">Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello informations PowerShell commande tooget hello source application web (dans ce cas nommées webapp-source) suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfa50-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="dfa50-113">toocreate un nouveau Plan App Service, nous pouvons utiliser la commande New-AzureRmAppServicePlan comme dans l’exemple suivant de hello</span><span class="sxs-lookup"><span data-stu-id="dfa50-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="dfa50-114">À l’aide de la commande hello AzureRmWebApp de nouveau, nous pouvons créer une application web hello dans la région de hello Amérique du Nord et comment lier il tooan couche premium existante du Plan App Service, en outre, nous pouvons utiliser hello même ressource de groupe en tant qu’application web de hello source, ou définir un nouveau groupe de ressources , suivant de hello montre que :</span><span class="sxs-lookup"><span data-stu-id="dfa50-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="dfa50-115">tooclone une application web existante, y compris tous les emplacements de déploiement associé, hello devra toouse hello IncludeSourceWebAppSlots paramètre, hello PowerShell commande suivante illustre l’utilisation de hello de ce paramètre avec hello New-AzureRmWebApp commande :</span><span class="sxs-lookup"><span data-stu-id="dfa50-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="dfa50-116">tooclone une application web existante dans hello même région, hello devra toocreate un groupe de ressources et d’un nouveau service d’application plan Bonjour même région, puis en utilisant hello suivants PowerShell commande tooclone hello web app</span><span class="sxs-lookup"><span data-stu-id="dfa50-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="dfa50-117">Le clonage d’un tooan d’application existant environnement App Service</span><span class="sxs-lookup"><span data-stu-id="dfa50-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="dfa50-118">Scénario : Une application web existante dans la région Amérique du Sud, hello l’utilisateur souhaiterait tooclone hello contenu tooa nouveau web application tooan existant d’environnement de Service d’application (ASE).</span><span class="sxs-lookup"><span data-stu-id="dfa50-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="dfa50-119">Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello informations PowerShell commande tooget hello source application web (dans ce cas nommées webapp-source) suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfa50-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="dfa50-120">Connaître le nom de hello ASE et nom de groupe de ressources hello hello ASE appartient à, utilisateur de hello pouvez utiliser la commande hello New-AzureRmWebApp toocreate hello application web dans ASE existant hello, hello suivant montre que :</span><span class="sxs-lookup"><span data-stu-id="dfa50-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="dfa50-121">paramètre d’emplacement Hello est nécessaire en raison de la raison de toolegacy, mais dans les cas de hello de création d’une application dans un environnement app service seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="dfa50-122">Clonage d’un emplacement d’application existant</span><span class="sxs-lookup"><span data-stu-id="dfa50-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="dfa50-123">Scénario : hello aimerait tooclone une tooeither l’emplacement d’application Web existante une application Web ou un nouvel emplacement de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="dfa50-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="dfa50-124">Hello nouvelle application Web peut être Bonjour même région comme emplacement de l’application Web hello d’origine ou dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="dfa50-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="dfa50-125">Le fait de connaître les ressources hello nom du groupe qui contient la source de l’application web de hello, nous pouvons utiliser hello commande PowerShell informations tooget hello source web application de l’emplacement (dans ce cas nommées source-webappslot) lié tooWeb application source-application Web suivante :</span><span class="sxs-lookup"><span data-stu-id="dfa50-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="dfa50-126">suivant de Hello illustre la création d’un clone de hello source web application tooa nouvelle application web :</span><span class="sxs-lookup"><span data-stu-id="dfa50-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="dfa50-127">Configuration de Traffic Manager lors du clonage d’une application</span><span class="sxs-lookup"><span data-stu-id="dfa50-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="dfa50-128">Créer des applications web de plusieurs régions et configurer Azure Traffic Manager tooroute trafic tooall ces applications web, est un tooinsure n scénarios importants qui les applications clients sont hautement disponibles, durant le clonage d’une application web existante, vous avez hello option tooconnect web applications tooeither un profil traffic manager nouveau ou existant - Notez que seul Azure Resource Manager la version de Traffic Manager est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dfa50-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="dfa50-129">Création d’un profil Traffic Manager lors du clonage d’une application</span><span class="sxs-lookup"><span data-stu-id="dfa50-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="dfa50-130">Scénario : hello l’utilisateur souhaiterait tooclone une région de tooanother web app, lors de la configuration d’un profil de gestionnaire de ressources Azure traffic manager qui incluent les deux applications web.</span><span class="sxs-lookup"><span data-stu-id="dfa50-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="dfa50-131">suivant de Hello illustre la création d’un clone de hello source web application tooa nouvelle application web lors de la configuration d’un nouveau profil Traffic Manager :</span><span class="sxs-lookup"><span data-stu-id="dfa50-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="dfa50-132">Ajout de nouveaux cloné Web App tooan profil Traffic Manager existant</span><span class="sxs-lookup"><span data-stu-id="dfa50-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="dfa50-133">Scénario : utilisateur de hello dispose déjà d’un profil traffic manager de Azure Resource Manager qu’il souhaite tooadd à la fois les applications en tant que points de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="dfa50-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="dfa50-134">toodo par conséquent, nous devons tooassemble hello existant id de profil traffic manager, nous devons id d’abonnement hello, nom de groupe de ressources et nom du profil hello existant traffic manager.</span><span class="sxs-lookup"><span data-stu-id="dfa50-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="dfa50-135">Une fois que l’id de gestionnaire de trafic hello, suivant de hello illustre la création d’un clone de hello source web application tooa nouvelle application web lors de l’ajout de leur profil de Traffic Manager existant tooan :</span><span class="sxs-lookup"><span data-stu-id="dfa50-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="dfa50-136">Restrictions actuelles</span><span class="sxs-lookup"><span data-stu-id="dfa50-136">Current Restrictions</span></span>
<span data-ttu-id="dfa50-137">Cette fonctionnalité est actuellement en version préliminaire, nous travaillons tooadd nouvelles fonctionnalités au fil du temps, hello suivant liste sont hello restrictions connues sur la version actuelle de hello au clonage de l’application :</span><span class="sxs-lookup"><span data-stu-id="dfa50-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="dfa50-138">Les paramètres de mise à l’échelle automatique ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="dfa50-139">Les paramètres de planification de sauvegarde ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="dfa50-140">Les paramètres de réseau virtuel ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="dfa50-141">Application Insights ne sont pas automatiquement définies sur l’application web de destination hello</span><span class="sxs-lookup"><span data-stu-id="dfa50-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="dfa50-142">Les paramètres d’authentification simple ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="dfa50-143">Les paramètres d’extension Kudu ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="dfa50-144">Les règles TiP ne sont pas clonées.</span><span class="sxs-lookup"><span data-stu-id="dfa50-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="dfa50-145">Les contenus de la base de données ne sont pas clonés.</span><span class="sxs-lookup"><span data-stu-id="dfa50-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="dfa50-146">Références</span><span class="sxs-lookup"><span data-stu-id="dfa50-146">References</span></span>
* [<span data-ttu-id="dfa50-147">Commandes PowerShell basées sur Azure Resource Manager pour Application web Azure</span><span class="sxs-lookup"><span data-stu-id="dfa50-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="dfa50-148">Clonage d’application web à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="dfa50-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="dfa50-149">Sauvegarde d’une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dfa50-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="dfa50-150">Prise en charge d’Azure Resource Manager pour la version préliminaire d’Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dfa50-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="dfa50-151">Introduction tooApp environnement de Service</span><span class="sxs-lookup"><span data-stu-id="dfa50-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="dfa50-152">Utilisation d'Azure PowerShell avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dfa50-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

