---
title: "aaaAzure outils de ligne de commande multiplateforme basée sur le Gestionnaire de ressources pour l’application Web de Azure | Documents Microsoft"
description: "Découvrez comment toouse hello nouveaux outils de ligne de commande multiplateforme basée sur Azure Resource Manager toomanage vos applications Web Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="4f7a5-103">Utilisation de l’interface de ligne de commande XPlat basée sur Azure Resource Manager pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f7a5-104">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4f7a5-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="4f7a5-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f7a5-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="4f7a5-106">Avec la version hello de version des outils de ligne de commande de Microsoft Azure inter-plateformes 0.10.5, les nouvelles commandes ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="4f7a5-107">Ces commandes permettent de hello utilisateur hello capacité toouse basée sur le Gestionnaire de ressources Azure de PowerShell commandes toomanage du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="4f7a5-108">toolearn sur la gestion des groupes de ressources, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="4f7a5-109">En outre, tester les [Azure CLI 2.0](https://github.com/Azure/azure-cli), une interface CLI de nouvelle génération écrit dans Python pour le modèle de déploiement de gestion de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="4f7a5-110">Gestion des plans App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="4f7a5-111">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-111">Create an App Service Plan</span></span>
<span data-ttu-id="4f7a5-112">toocreate un plan app service, utilisez hello **appserviceplan azure créer** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="4f7a5-113">Voici les descriptions des paramètres différents de hello :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="4f7a5-114">**: groupe de ressources**: groupe de ressources qui inclut le plan de service d’application hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="4f7a5-115">**--nom**: nom du plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="4f7a5-116">**--location** : emplacement du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="4f7a5-117">**--référence (SKU)**: hello souhaité tarification sku (hello options sont : F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="4f7a5-118">D1 (Partagé).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-118">D1 (Shared).</span></span> <span data-ttu-id="4f7a5-119">B1 (De base, petit), B2 (De base, moyen) et B3 (De base, grand).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="4f7a5-120">S1 (Standard, petit), S2 (Standard, moyen) et S3 (Standard, grand).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="4f7a5-121">P1 (Premium, petit), P2 (Premium, moyen) et P3 (Premium, grand).)</span><span class="sxs-lookup"><span data-stu-id="4f7a5-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="4f7a5-122">**--instances**: hello du nombre de threads de travail dans le plan de service d’application hello (valeur par défaut est 1).</span><span class="sxs-lookup"><span data-stu-id="4f7a5-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="4f7a5-123">Exemple toouse cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="4f7a5-124">Créer un plan App Service Linux</span><span class="sxs-lookup"><span data-stu-id="4f7a5-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="4f7a5-125">À l’aide de hello même **appserviceplan azure créer** commande par hello paramètre supplémentaire **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="4f7a5-126">Notez les restrictions hello et décrites dans les régions [Introduction tooApp Service sur Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4f7a5-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="4f7a5-127">Répertorier les plans App Service existants</span><span class="sxs-lookup"><span data-stu-id="4f7a5-127">List Existing App Service Plans</span></span>
<span data-ttu-id="4f7a5-128">toolist hello app service place, utilisez **appserviceplan azure liste** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="4f7a5-129">toolist tous les plans de service d’application sous un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4f7a5-130">tooget un plan de service d’application spécifique, utilisez **appserviceplan azure afficher** commande :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="4f7a5-131">Configurer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="4f7a5-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="4f7a5-132">toochange hello paramètres d’un plan app service existant, utilisez hello **appserviceplan azure config** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="4f7a5-133">Vous pouvez modifier hello référence (SKU) et le nombre de traitements hello</span><span class="sxs-lookup"><span data-stu-id="4f7a5-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="4f7a5-134">Mise à l’échelle d’un plan App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="4f7a5-135">tooscale une existante du Plan App Service, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="4f7a5-136">La modification hello référence (SKU) d’un Plan App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="4f7a5-137">toochange hello référence (SKU) d’un existant du Plan App Service, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="4f7a5-138">Supprimer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="4f7a5-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="4f7a5-139">toodelete un plan de service d’application existant, assigné applications besoin toobe déplacés ou supprimés en premier.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="4f7a5-140">Puis à l’aide de hello **webapp azure supprimer** commande, vous pouvez supprimer le plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="4f7a5-141">Gestion des plans App Service</span><span class="sxs-lookup"><span data-stu-id="4f7a5-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="4f7a5-142">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="4f7a5-142">Create a web app</span></span>
<span data-ttu-id="4f7a5-143">toocreate une application web, utilisez hello **webapp azure créer** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="4f7a5-144">Voici les descriptions des paramètres différents de hello :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="4f7a5-145">**--nom**: nom de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="4f7a5-146">**--plan**: nom de plan de service hello utilisé toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="4f7a5-147">**: groupe de ressources**: groupe de ressources qui héberge le plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="4f7a5-148">**--emplacement**: hello d’emplacement de l’application web.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="4f7a5-149">Exemple toouse cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="4f7a5-150">Supprimer une application existante</span><span class="sxs-lookup"><span data-stu-id="4f7a5-150">Delete an existing app</span></span>
<span data-ttu-id="4f7a5-151">toodelete une application existante, vous pouvez utiliser hello **webapp azure supprimer** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="4f7a5-152">Vous devez toospecify hello nom application hello et nom de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="4f7a5-153">Répertorier les applications existantes</span><span class="sxs-lookup"><span data-stu-id="4f7a5-153">List existing apps</span></span>
<span data-ttu-id="4f7a5-154">toolist hello les applications existantes, utilisez hello **webapp azure liste** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="4f7a5-155">toolist toutes les applications dans un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4f7a5-156">tooget une application spécifique, utilisez hello **webapp azure afficher** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="4f7a5-157">Configurer une application existante</span><span class="sxs-lookup"><span data-stu-id="4f7a5-157">Configure an existing app</span></span>
<span data-ttu-id="4f7a5-158">paramètres de hello toochange et configurations pour une application existante, utilisez hello **jeu de configuration azure webapp** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="4f7a5-159">Exemple (1) : modification de la version de php hello d’une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="4f7a5-160">Exemple (2) : ajouter ou modifier les paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="4f7a5-161">tooknow autres que leur configuration peut être modifiée, utilisez hello **-h du jeu de configuration de l’application Web azure** commande.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="4f7a5-162">Changement d’état d’une application existante hello</span><span class="sxs-lookup"><span data-stu-id="4f7a5-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="4f7a5-163">Redémarrer une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-163">Restart an app</span></span>
<span data-ttu-id="4f7a5-164">toorestart une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="4f7a5-165">Arrêter une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-165">Stop an app</span></span>
<span data-ttu-id="4f7a5-166">toostop une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="4f7a5-167">Démarrer une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-167">Start an app</span></span>
<span data-ttu-id="4f7a5-168">toostart une application, vous devez spécifier le groupe de hello nom et les ressources de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="4f7a5-169">Gérer les profils de publication d’une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="4f7a5-170">Chaque application possède un profil de publication qui peut être utilisé toopublish votre code.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="4f7a5-171">Obtenir le profil de publication</span><span class="sxs-lookup"><span data-stu-id="4f7a5-171">Get Publishing Profile</span></span>
<span data-ttu-id="4f7a5-172">hello tooget profil pour une application, l’utilisation de publication :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4f7a5-173">Cette commande renvoie hello de ligne de commande toohello nom d’utilisateur et mot de passe des profils de publication.</span><span class="sxs-lookup"><span data-stu-id="4f7a5-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="4f7a5-174">Gérer les noms d’hôte d’une application</span><span class="sxs-lookup"><span data-stu-id="4f7a5-174">Manage app hostnames</span></span>
<span data-ttu-id="4f7a5-175">liaisons de nom d’hôte toomanage pour votre application, utilisez hello **noms d’hôte de la configuration azure webapp** commande</span><span class="sxs-lookup"><span data-stu-id="4f7a5-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="4f7a5-176">Répertorier les liaisons de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="4f7a5-176">List hostname bindings</span></span>
<span data-ttu-id="4f7a5-177">liaisons actuelles nom d’hôte tooget hello pour une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="4f7a5-178">Ajouter des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="4f7a5-178">Add hostname bindings</span></span>
<span data-ttu-id="4f7a5-179">tooadd nom d’hôte liaisons tooan l’application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="4f7a5-180">Supprimer des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="4f7a5-180">Delete hostname bindings</span></span>
<span data-ttu-id="4f7a5-181">liaisons de nom d’hôte toodelete, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4f7a5-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="4f7a5-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f7a5-182">Next Steps</span></span>
* <span data-ttu-id="4f7a5-183">toolearn sur la prise en charge d’Azure Resource Manager CLI, consultez [utiliser hello CLI d’Azure toomanage Azure ressources et groupes de ressources.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="4f7a5-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="4f7a5-184">toolearn sur la gestion du Service d’applications à l’aide de PowerShell, consultez [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4f7a5-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="4f7a5-185">toolearn sur le Service d’applications Azure sur Linux, consultez [Introduction tooApp Service sur Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4f7a5-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
