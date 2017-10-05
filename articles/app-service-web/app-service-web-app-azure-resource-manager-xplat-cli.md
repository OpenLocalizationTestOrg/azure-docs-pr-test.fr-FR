---
title: "Outils en ligne de commande multiplateformes basés sur Azure Resource Manager pour Azure Web App | Microsoft Docs"
description: "Découvrez comment utiliser les nouveaux outils en ligne de commande multiplateformes basés sur Azure Resource Manager pour gérer vos applications Azure Web Apps."
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="09953-103">Utilisation de l’interface de ligne de commande XPlat basée sur Azure Resource Manager pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="09953-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09953-104">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="09953-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="09953-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09953-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="09953-106">La version 0.10.5 des outils en ligne de commande multiplateformes Microsoft Azure comporte de nouvelles commandes.</span><span class="sxs-lookup"><span data-stu-id="09953-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="09953-107">Ces commandes permettent à l’utilisateur de gérer App Service à l’aide de commandes PowerShell basées sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="09953-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="09953-108">Pour en savoir plus sur la gestion des groupes de ressources, voir [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md) (Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure).</span><span class="sxs-lookup"><span data-stu-id="09953-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="09953-109">Essayez également [Azure CLI 2.0](https://github.com/Azure/azure-cli), une interface de ligne de commande nouvelle génération écrite en Python pour le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="09953-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="09953-110">Gestion des plans App Service</span><span class="sxs-lookup"><span data-stu-id="09953-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="09953-111">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="09953-111">Create an App Service Plan</span></span>
<span data-ttu-id="09953-112">Pour créer un plan App Service, utilisez la commande **azure appserviceplan create**.</span><span class="sxs-lookup"><span data-stu-id="09953-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="09953-113">Voici une description des différents paramètres :</span><span class="sxs-lookup"><span data-stu-id="09953-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="09953-114">**--resource-group** : groupe de ressources contenant le nouveau plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09953-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="09953-115">**--name** : nom du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09953-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="09953-116">**--location** : emplacement du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09953-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="09953-117">**--sku** : SKU de tarification souhaité (Les options sont les suivantes : F1 (Gratuit).</span><span class="sxs-lookup"><span data-stu-id="09953-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="09953-118">D1 (Partagé).</span><span class="sxs-lookup"><span data-stu-id="09953-118">D1 (Shared).</span></span> <span data-ttu-id="09953-119">B1 (De base, petit), B2 (De base, moyen) et B3 (De base, grand).</span><span class="sxs-lookup"><span data-stu-id="09953-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="09953-120">S1 (Standard, petit), S2 (Standard, moyen) et S3 (Standard, grand).</span><span class="sxs-lookup"><span data-stu-id="09953-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="09953-121">P1 (Premium, petit), P2 (Premium, moyen) et P3 (Premium, grand).)</span><span class="sxs-lookup"><span data-stu-id="09953-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="09953-122">**--instances** : nombre de threads de travail dans le plan App Service (Valeur par défaut : 1).</span><span class="sxs-lookup"><span data-stu-id="09953-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="09953-123">Exemple d’utilisation de cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="09953-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="09953-124">Créer un plan App Service Linux</span><span class="sxs-lookup"><span data-stu-id="09953-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="09953-125">En utilisant la même commande **azure appserviceplan create** avec le paramètre supplémentaire **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="09953-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="09953-126">Consultez les restrictions et les régions décrites dans [Présentation d’App Service sur Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="09953-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="09953-127">Répertorier les plans App Service existants</span><span class="sxs-lookup"><span data-stu-id="09953-127">List Existing App Service Plans</span></span>
<span data-ttu-id="09953-128">Pour répertorier les plans App Service existants, utilisez la commande **azure appserviceplan list**.</span><span class="sxs-lookup"><span data-stu-id="09953-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="09953-129">Pour répertorier tous les plans App Service associés à un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="09953-130">Pour accéder à un plan App Service spécifique, utilisez la commande **azure appserviceplan show**.</span><span class="sxs-lookup"><span data-stu-id="09953-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="09953-131">Configurer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="09953-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="09953-132">Pour modifier les paramètres d’un plan App Service existant, utilisez la commande **azure appserviceplan config**.</span><span class="sxs-lookup"><span data-stu-id="09953-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="09953-133">Vous pouvez modifier le SKU et le nombre de threads de travail.</span><span class="sxs-lookup"><span data-stu-id="09953-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="09953-134">Mise à l’échelle d’un plan App Service</span><span class="sxs-lookup"><span data-stu-id="09953-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="09953-135">Pour mettre à l’échelle un plan App Service existant, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="09953-136">Modification du SKU d’un plan App Service</span><span class="sxs-lookup"><span data-stu-id="09953-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="09953-137">Pour modifier le SKU d’un plan App Service existant, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="09953-138">Supprimer un plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="09953-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="09953-139">Pour supprimer un plan App Service existant, toutes les applications affectées doivent d’abord être déplacées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="09953-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="09953-140">Ensuite, à l’aide de la commande **azure webapp delete**, vous pouvez supprimer le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09953-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="09953-141">Gestion des plans App Service</span><span class="sxs-lookup"><span data-stu-id="09953-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="09953-142">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="09953-142">Create a web app</span></span>
<span data-ttu-id="09953-143">Pour créer une application web, utilisez la commande **azure webapp create**.</span><span class="sxs-lookup"><span data-stu-id="09953-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="09953-144">Voici une description des différents paramètres :</span><span class="sxs-lookup"><span data-stu-id="09953-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="09953-145">**--name** : nom de l’application web.</span><span class="sxs-lookup"><span data-stu-id="09953-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="09953-146">**--plan** : nom du plan de service utilisé pour héberger l’application web.</span><span class="sxs-lookup"><span data-stu-id="09953-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="09953-147">**--resource-group** : groupe de ressources qui héberge le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09953-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="09953-148">**--location** : emplacement de l’application web.</span><span class="sxs-lookup"><span data-stu-id="09953-148">**--location**: the web app location.</span></span>

<span data-ttu-id="09953-149">Exemple d’utilisation de cette applet de commande :</span><span class="sxs-lookup"><span data-stu-id="09953-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="09953-150">Supprimer une application existante</span><span class="sxs-lookup"><span data-stu-id="09953-150">Delete an existing app</span></span>
<span data-ttu-id="09953-151">Pour supprimer une application existante, vous pouvez utiliser la commande **azure webapp delete**.</span><span class="sxs-lookup"><span data-stu-id="09953-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="09953-152">Vous devez spécifier le nom de l’application et le nom du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="09953-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="09953-153">Répertorier les applications existantes</span><span class="sxs-lookup"><span data-stu-id="09953-153">List existing apps</span></span>
<span data-ttu-id="09953-154">Pour répertorier les applications existantes, utilisez la commande **azure webapp list**.</span><span class="sxs-lookup"><span data-stu-id="09953-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="09953-155">Pour répertorier toutes les applications dans un groupe de ressources spécifique, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="09953-156">Pour accéder à une application spécifique, utilisez la commande **azure webapp show**.</span><span class="sxs-lookup"><span data-stu-id="09953-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="09953-157">Configurer une application existante</span><span class="sxs-lookup"><span data-stu-id="09953-157">Configure an existing app</span></span>
<span data-ttu-id="09953-158">Pour modifier les paramètres et configurations d’une application existante, utilisez la commande **azure webapp config set**.</span><span class="sxs-lookup"><span data-stu-id="09953-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="09953-159">Exemple (1) : modifier la version php d’une application</span><span class="sxs-lookup"><span data-stu-id="09953-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="09953-160">Exemple (2) : ajouter ou modifier les paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="09953-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="09953-161">Pour savoir quelle autre configuration peut être modifiée, utilisez la commande **azure webapp config set -h**.</span><span class="sxs-lookup"><span data-stu-id="09953-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="09953-162">Modifier l’état d’une application existante</span><span class="sxs-lookup"><span data-stu-id="09953-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="09953-163">Redémarrer une application</span><span class="sxs-lookup"><span data-stu-id="09953-163">Restart an app</span></span>
<span data-ttu-id="09953-164">Pour redémarrer une application, vous devez spécifier le nom et le groupe de ressources de cette application.</span><span class="sxs-lookup"><span data-stu-id="09953-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="09953-165">Arrêter une application</span><span class="sxs-lookup"><span data-stu-id="09953-165">Stop an app</span></span>
<span data-ttu-id="09953-166">Pour arrêter une application, vous devez spécifier le nom et le groupe de ressources de cette application.</span><span class="sxs-lookup"><span data-stu-id="09953-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="09953-167">Démarrer une application</span><span class="sxs-lookup"><span data-stu-id="09953-167">Start an app</span></span>
<span data-ttu-id="09953-168">Pour démarrer une application, vous devez spécifier le nom et le groupe de ressources de cette application.</span><span class="sxs-lookup"><span data-stu-id="09953-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="09953-169">Gérer les profils de publication d’une application</span><span class="sxs-lookup"><span data-stu-id="09953-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="09953-170">Chaque application dispose d’un profil de publication qui peut être utilisé pour publier votre code.</span><span class="sxs-lookup"><span data-stu-id="09953-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="09953-171">Obtenir le profil de publication</span><span class="sxs-lookup"><span data-stu-id="09953-171">Get Publishing Profile</span></span>
<span data-ttu-id="09953-172">Pour obtenir le profil de publication d’une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="09953-173">Cette commande renvoie le nom d’utilisateur et le mot de passe du profil de publication à la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="09953-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="09953-174">Gérer les noms d’hôte d’une application</span><span class="sxs-lookup"><span data-stu-id="09953-174">Manage app hostnames</span></span>
<span data-ttu-id="09953-175">Pour gérer les liaisons de nom d’hôte de votre application, utilisez la commande **azure webapp config hostnames**.</span><span class="sxs-lookup"><span data-stu-id="09953-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="09953-176">Répertorier les liaisons de nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="09953-176">List hostname bindings</span></span>
<span data-ttu-id="09953-177">Pour obtenir les liaisons de nom d’hôte actuelles pour une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="09953-178">Ajouter des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="09953-178">Add hostname bindings</span></span>
<span data-ttu-id="09953-179">Pour ajouter des liaisons de noms d’hôte à une application, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="09953-180">Supprimer des liaisons de noms d’hôte</span><span class="sxs-lookup"><span data-stu-id="09953-180">Delete hostname bindings</span></span>
<span data-ttu-id="09953-181">Pour supprimer des liaisons de noms d’hôte, utilisez :</span><span class="sxs-lookup"><span data-stu-id="09953-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="09953-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09953-182">Next Steps</span></span>
* <span data-ttu-id="09953-183">Pour en savoir plus sur la prise en charge de l’interface de ligne de commande Azure Resource Manager, voir [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md) (Utiliser l’interface de ligne de commande Azure pour gérer les ressources et les groupes de ressources Azure).</span><span class="sxs-lookup"><span data-stu-id="09953-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="09953-184">Pour en savoir plus sur la gestion d’App Service à l’aide de PowerShell, voir [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps](app-service-web-app-azure-resource-manager-powershell.md) (Utilisation de PowerShell basé sur Azure Resource Manager pour gérer Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="09953-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="09953-185">Pour en savoir plus sur Azure App Service sur Linux, voir [Présentation d’App Service sur Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="09953-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
