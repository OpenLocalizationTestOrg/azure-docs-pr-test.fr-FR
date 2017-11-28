---
title: "commandes d’aaaAzure basée sur le Gestionnaire de ressources de PowerShell pour l’application Web de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello nouvelle toomanage de commandes PowerShell de basée sur le Gestionnaire de ressources Azure, vos applications Web Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="41bba-103">À l’aide de PowerShell de Azure Resource Manager-Based tooManage Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="41bba-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41bba-104">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="41bba-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="41bba-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41bba-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="41bba-106">Avec Microsoft Azure PowerShell version 1.0.0 nouvelles commandes ont été ajoutés, qui donnent hello utilisateur hello capacité toouse basée sur le Gestionnaire de ressources Azure de PowerShell commandes toomanage les applications Web.</span><span class="sxs-lookup"><span data-stu-id="41bba-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="41bba-107">toolearn sur la gestion des groupes de ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="41bba-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="41bba-108">toolearn sur la liste complète des paramètres et des options pour les applets de commande PowerShell de hello hello voir hello [complète la référence d’applet de commande de basée sur le Web application Azure Resource Manager des PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="41bba-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="41bba-109">Gestion des plans App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="41bba-110">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-110">Create an App Service Plan</span></span>
<span data-ttu-id="41bba-111">toocreate un plan app service, utilisez hello **New-AzureRmAppServicePlan** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="41bba-112">Voici les descriptions des paramètres différents de hello :</span><span class="sxs-lookup"><span data-stu-id="41bba-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="41bba-113">**Nom**: nom du plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="41bba-114">**Location**: emplacement du plan de service.</span><span class="sxs-lookup"><span data-stu-id="41bba-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="41bba-115">**ResourceGroupName**: groupe de ressources qui inclut le plan de service d’application hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="41bba-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="41bba-116">**Couche**: hello souhaité niveau tarifaire (valeur par défaut est libre, les autres options sont Shared, Basic, Standard et Premium.)</span><span class="sxs-lookup"><span data-stu-id="41bba-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="41bba-117">**WorkerSize**: hello taille des travailleurs (valeur par défaut est petit, si le paramètre de niveau hello a été spécifié comme base, Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="41bba-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="41bba-118">Les autres options sont Moyen et Grand.)</span><span class="sxs-lookup"><span data-stu-id="41bba-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="41bba-119">**La valeur NumberofWorkers**: hello du nombre de threads de travail dans le plan de service d’application hello (valeur par défaut est 1).</span><span class="sxs-lookup"><span data-stu-id="41bba-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="41bba-120">Exemple toouse cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="41bba-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="41bba-121">Création d’un plan App Service dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="41bba-122">planification d’un service d’application toocreate dans un environnement app service, utilisez hello même commande **New-AzureRmAppServicePlan** avec le nom de hello toospecify de paramètres supplémentaires de ASE et le nom de groupe de ressources de ASE.</span><span class="sxs-lookup"><span data-stu-id="41bba-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="41bba-123">Exemple toouse cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="41bba-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="41bba-124">toolearn plus en détail l’environnement app service, vérification [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="41bba-125">Répertorier les plans App Service existants</span><span class="sxs-lookup"><span data-stu-id="41bba-125">List Existing App Service Plans</span></span>
<span data-ttu-id="41bba-126">toolist hello app service place, utilisez **Get-AzureRmAppServicePlan** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="41bba-127">toolist tous les plans de service d’application sous votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="41bba-128">toolist tous les plans de service d’application sous un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="41bba-129">tooget un plan de service d’application spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="41bba-130">Configurer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="41bba-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="41bba-131">toochange hello paramètres d’un plan app service existant, utilisez hello **Set-AzureRmAppServicePlan** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="41bba-132">Vous pouvez modifier le niveau de hello, la taille du travail et le nombre de traitements hello</span><span class="sxs-lookup"><span data-stu-id="41bba-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="41bba-133">Mise à l’échelle d’un plan App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="41bba-134">tooscale une existante du Plan App Service, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="41bba-135">Modification de la taille du travail hello d’un Plan App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="41bba-136">taille de hello toochange des travailleurs dans une existante du Plan App Service, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="41bba-137">La modification hello niveau d’un Plan App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="41bba-138">couche de hello toochange d’une existante du Plan App Service, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="41bba-139">Supprimer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="41bba-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="41bba-140">toodelete un plan de service d’application existant, assigné web applications besoin toobe déplacés ou supprimés en premier.</span><span class="sxs-lookup"><span data-stu-id="41bba-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="41bba-141">Puis à l’aide de hello **Remove-AzureRmAppServicePlan** vous pouvez supprimer le plan de service d’application hello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="41bba-142">Gestion d’App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="41bba-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="41bba-143">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="41bba-143">Create a Web App</span></span>
<span data-ttu-id="41bba-144">toocreate une application web, utilisez hello **New-AzureRmWebApp** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="41bba-145">Voici les descriptions des paramètres différents de hello :</span><span class="sxs-lookup"><span data-stu-id="41bba-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="41bba-146">**Nom**: nom de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="41bba-147">**AppServicePlan**: nom de plan de service hello utilisé toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="41bba-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="41bba-148">**ResourceGroupName**: groupe de ressources qui héberge le plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="41bba-149">**Emplacement**: hello d’emplacement de l’application web.</span><span class="sxs-lookup"><span data-stu-id="41bba-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="41bba-150">Exemple toouse cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="41bba-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="41bba-151">Créer une application web dans un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="41bba-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="41bba-152">toocreate une application web dans un environnement de Service de l’application (ASE).</span><span class="sxs-lookup"><span data-stu-id="41bba-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="41bba-153">Utilisez hello même **New-AzureRmWebApp** avec le nom de paramètres supplémentaires toospecify hello ASE et nom de groupe de ressources hello hello ASE appartient à.</span><span class="sxs-lookup"><span data-stu-id="41bba-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="41bba-154">toolearn plus en détail l’environnement app service, vérification [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="41bba-155">Supprimer une application web existante</span><span class="sxs-lookup"><span data-stu-id="41bba-155">Delete an existing Web App</span></span>
<span data-ttu-id="41bba-156">toodelete une application web existante, vous pouvez utiliser hello **Remove-AzureRmWebApp** applet de commande, vous devez toospecify hello nom hello web app et nom de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="41bba-157">Répertorier les applications web existantes</span><span class="sxs-lookup"><span data-stu-id="41bba-157">List existing Web Apps</span></span>
<span data-ttu-id="41bba-158">toolist hello des applications web existantes, utilisez hello **Get-AzureRmWebApp** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="41bba-159">toolist toutes les applications web sous votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="41bba-160">toolist toutes les applications web sous un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="41bba-161">tooget une application web spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="41bba-162">Configurer une application web existante</span><span class="sxs-lookup"><span data-stu-id="41bba-162">Configure an existing Web App</span></span>
<span data-ttu-id="41bba-163">paramètres de hello toochange et configurations pour une application web existante, utilisez hello **Set-AzureRmWebApp** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41bba-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="41bba-164">Pour obtenir une liste complète des paramètres, consultez hello [lien de référence d’applet de commande](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="41bba-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="41bba-165">Exemple (1) : utilisez cette applet de commande toochange les chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="41bba-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="41bba-166">Exemple (2) : ajouter ou modifier les paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="41bba-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="41bba-167">Exemple (3) : set hello web application toorun en mode 64 bits</span><span class="sxs-lookup"><span data-stu-id="41bba-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="41bba-168">Changement d’état d’une application Web existante hello</span><span class="sxs-lookup"><span data-stu-id="41bba-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="41bba-169">Redémarrer une application web</span><span class="sxs-lookup"><span data-stu-id="41bba-169">Restart a web app</span></span>
<span data-ttu-id="41bba-170">toorestart une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="41bba-171">Arrêter une application web</span><span class="sxs-lookup"><span data-stu-id="41bba-171">Stop a web app</span></span>
<span data-ttu-id="41bba-172">toostop une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="41bba-173">Démarrer une application web</span><span class="sxs-lookup"><span data-stu-id="41bba-173">Start a web app</span></span>
<span data-ttu-id="41bba-174">toostart une application web, vous devez spécifier hello nom ressource groupe et de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="41bba-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="41bba-175">Gérer les profils de publication Web Apps</span><span class="sxs-lookup"><span data-stu-id="41bba-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="41bba-176">Chaque application web a un profil de publication qui peut être utilisé toopublish vos applications, plusieurs opérations peuvent être exécutées sur les profils de publication.</span><span class="sxs-lookup"><span data-stu-id="41bba-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="41bba-177">Obtenir le profil de publication</span><span class="sxs-lookup"><span data-stu-id="41bba-177">Get Publishing Profile</span></span>
<span data-ttu-id="41bba-178">hello tooget publication profil pour une application web, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="41bba-179">Cette commande renvoie hello publication de ligne de commande toohello profil ainsi hello publication profil tooa texte fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="41bba-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="41bba-180">Réinitialiser le profil de publication</span><span class="sxs-lookup"><span data-stu-id="41bba-180">Reset Publishing Profile</span></span>
<span data-ttu-id="41bba-181">tooreset à la fois hello mot de passe de publication pour FTP et web deploy pour une application web, utilisez :</span><span class="sxs-lookup"><span data-stu-id="41bba-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="41bba-182">Gérer les certificats d’application web</span><span class="sxs-lookup"><span data-stu-id="41bba-182">Manage Web App Certificates</span></span>
<span data-ttu-id="41bba-183">toolearn sur comment toomanage web des certificats de l’application, consultez [liaison de certificats SSL à l’aide de PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="41bba-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41bba-184">Next Steps</span></span>
* <span data-ttu-id="41bba-185">toolearn sur la prise en charge du Gestionnaire de ressources de Azure PowerShell, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="41bba-186">toolearn sur les environnements de Service d’application, consultez [Introduction tooApp environnement de Service.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="41bba-187">toolearn sur la gestion des certificats SSL de Service d’application à l’aide de PowerShell, consultez [liaison de certificats SSL à l’aide de PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="41bba-188">toolearn sur la liste complète des applets de commande PowerShell de basée sur Azure Resource Manager pour les applications Web Azure, hello consultez [référence d’applet de commande Azure de PowerShell Cmdlets de Web Apps Azure Resource Manager.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="41bba-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="41bba-189">toolearn sur la gestion du Service d’applications à l’aide de la CLI, consultez [Using Azure Resource Manager-Based XPlat CLI pour l’application Web Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="41bba-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

