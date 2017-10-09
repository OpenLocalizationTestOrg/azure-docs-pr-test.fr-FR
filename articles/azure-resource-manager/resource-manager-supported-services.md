---
title: aaaAzure fournisseurs de ressources et les types de ressources | Documents Microsoft
description: "Décrit les fournisseurs de ressources hello qui prennent en charge le Gestionnaire de ressources, leurs schémas et les versions disponibles de l’API et les régions hello qui peuvent héberger des ressources de hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="92533-103">Fournisseurs et types de ressources</span><span class="sxs-lookup"><span data-stu-id="92533-103">Resource providers and types</span></span>

<span data-ttu-id="92533-104">Lorsque vous déployez des ressources, vous devez fréquemment tooretrieve d’informations sur les types et les fournisseurs de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="92533-105">Dans cet article, vous apprenez à :</span><span class="sxs-lookup"><span data-stu-id="92533-105">In this article, you learn to:</span></span>

* <span data-ttu-id="92533-106">Afficher tous les fournisseurs de ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="92533-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="92533-107">Vérifier l’état de l’inscription d’un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="92533-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="92533-108">Inscrire un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="92533-108">Register a resource provider</span></span>
* <span data-ttu-id="92533-109">Afficher les types de ressources pour un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="92533-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="92533-110">Afficher les emplacements valides pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="92533-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="92533-111">Afficher les versions d’API valides pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="92533-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="92533-112">Vous pouvez effectuer ces étapes via le portail de hello, PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="92533-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="92533-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92533-113">PowerShell</span></span>

<span data-ttu-id="92533-114">toosee tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, utilisent :</span><span class="sxs-lookup"><span data-stu-id="92533-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="92533-115">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="92533-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="92533-116">L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="92533-117">étendue Hello pour l’inscription est toujours hello abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="92533-118">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="92533-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="92533-119">Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="92533-120">tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="92533-121">Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="92533-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="92533-122">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="92533-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="92533-123">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="92533-124">informations de toosee pour un fournisseur de ressources particulier, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="92533-125">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="92533-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="92533-126">types de ressources toosee hello pour un fournisseur de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="92533-127">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="92533-128">version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="92533-129">Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="92533-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="92533-130">versions disponibles API tooget hello pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="92533-131">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="92533-132">Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="92533-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="92533-133">En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="92533-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="92533-134">tooget les emplacements de hello pris en charge pour un type de ressource, utilisez.</span><span class="sxs-lookup"><span data-stu-id="92533-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="92533-135">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="92533-136">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="92533-136">Azure CLI</span></span>
<span data-ttu-id="92533-137">toosee tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, utilisent :</span><span class="sxs-lookup"><span data-stu-id="92533-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="92533-138">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="92533-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="92533-139">L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="92533-140">étendue Hello pour l’inscription est toujours hello abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="92533-141">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="92533-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="92533-142">Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="92533-143">tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="92533-144">Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="92533-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="92533-145">Qui retourne un message indiquant que l’inscription est en cours.</span><span class="sxs-lookup"><span data-stu-id="92533-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="92533-146">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="92533-147">informations de toosee pour un fournisseur de ressources particulier, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="92533-148">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="92533-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="92533-149">types de ressources toosee hello pour un fournisseur de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="92533-150">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="92533-151">version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="92533-152">Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="92533-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="92533-153">versions disponibles API tooget hello pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="92533-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="92533-154">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="92533-155">Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="92533-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="92533-156">En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="92533-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="92533-157">tooget les emplacements de hello pris en charge pour un type de ressource, utilisez.</span><span class="sxs-lookup"><span data-stu-id="92533-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="92533-158">Résultat :</span><span class="sxs-lookup"><span data-stu-id="92533-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="92533-159">Portail</span><span class="sxs-lookup"><span data-stu-id="92533-159">Portal</span></span>

<span data-ttu-id="92533-160">sélectionner de tous les fournisseurs de ressources dans Azure et l’état de l’inscription de hello pour votre abonnement, toosee **abonnements**.</span><span class="sxs-lookup"><span data-stu-id="92533-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![sélectionner les abonnements](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="92533-162">Choisissez hello abonnement tooview.</span><span class="sxs-lookup"><span data-stu-id="92533-162">Choose hello subscription tooview.</span></span>

![spécifier l’abonnement](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="92533-164">Sélectionnez **fournisseurs de ressources** et afficher la liste des fournisseurs de ressources disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="92533-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![afficher les fournisseurs de ressources](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="92533-166">L’inscription d’un fournisseur de ressources de configure toowork de votre abonnement avec le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="92533-167">étendue Hello pour l’inscription est toujours hello abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="92533-168">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="92533-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="92533-169">Toutefois, vous devrez peut-être toomanually inscrire des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="92533-170">tooregister un fournisseur de ressources, vous devez avoir hello de tooperform autorisation `/register/action` opération hello pour fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="92533-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="92533-171">Cette opération est incluse dans hello collaborateurs et les rôles de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="92533-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="92533-172">tooregister un fournisseur de ressources, sélectionnez **inscrire**.</span><span class="sxs-lookup"><span data-stu-id="92533-172">tooregister a resource provider, select **Register**.</span></span>

![inscrire un fournisseur de ressources](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="92533-174">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="92533-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="92533-175">informations toosee pour un fournisseur de ressources particulier, sélectionnez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="92533-175">toosee information for a particular resource provider, select **More services**.</span></span>

![sélectionner d’autres services](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="92533-177">Recherchez **l’Explorateur de ressources** et sélectionnez-le dans les options disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="92533-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![sélectionner l’Explorateur de ressources](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="92533-179">Sélectionnez **Fournisseurs**.</span><span class="sxs-lookup"><span data-stu-id="92533-179">Select **Providers**.</span></span>

![sélectionner les fournisseurs](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="92533-181">Ressources et fournisseur de ressources hello sélectionnez le type que vous souhaitez tooview.</span><span class="sxs-lookup"><span data-stu-id="92533-181">Select hello resource provider and resource type that you want tooview.</span></span>

![sélectionner le type de ressource](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="92533-183">Le Gestionnaire de ressources est pris en charge dans toutes les régions, mais les ressources hello que vous déployez ne peuvent pas être pris en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="92533-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="92533-184">En outre, il peut être sur votre abonnement, les limitations qui vous empêchent d’utiliser certaines régions qui prennent en charge la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="92533-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="92533-185">l’Explorateur de ressources Hello affiche des emplacements valides pour le type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="92533-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![afficher les emplacements](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="92533-187">version de l’API Hello correspond version tooa d’opérations d’API REST publiées par le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92533-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="92533-188">Comme un fournisseur de ressources permet de nouvelles fonctionnalités, il libère une nouvelle version de hello API REST.</span><span class="sxs-lookup"><span data-stu-id="92533-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="92533-189">l’Explorateur de ressources Hello affiche les versions des API valides pour le type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="92533-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![afficher les versions d’API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="92533-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92533-191">Next steps</span></span>
* <span data-ttu-id="92533-192">toolearn sur la création de modèles du Gestionnaire de ressources, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="92533-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="92533-193">toolearn sur le déploiement de ressources, consultez [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="92533-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="92533-194">opérations de hello tooview pour un fournisseur de ressources, consultez [API REST Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="92533-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

