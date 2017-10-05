---
title: Types de ressources et fournisseurs de ressources Azure | Microsoft Docs
description: "Décrit les fournisseurs de ressources qui prennent en charge Resource Manager, ainsi que les schémas et versions d’API disponibles et les régions pouvant héberger les ressources."
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="c29f2-103">Fournisseurs et types de ressources</span><span class="sxs-lookup"><span data-stu-id="c29f2-103">Resource providers and types</span></span>

<span data-ttu-id="c29f2-104">Lorsque vous déployez des ressources, vous devez fréquemment récupérer des informations sur les fournisseurs et les types de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="c29f2-105">Dans cet article, vous apprenez à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-105">In this article, you learn to:</span></span>

* <span data-ttu-id="c29f2-106">Afficher tous les fournisseurs de ressources dans Azure</span><span class="sxs-lookup"><span data-stu-id="c29f2-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="c29f2-107">Vérifier l’état de l’inscription d’un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="c29f2-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="c29f2-108">Inscrire un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="c29f2-108">Register a resource provider</span></span>
* <span data-ttu-id="c29f2-109">Afficher les types de ressources pour un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="c29f2-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="c29f2-110">Afficher les emplacements valides pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="c29f2-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="c29f2-111">Afficher les versions d’API valides pour un type de ressource</span><span class="sxs-lookup"><span data-stu-id="c29f2-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="c29f2-112">Vous pouvez effectuer ces étapes via le portail, PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="c29f2-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="c29f2-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c29f2-113">PowerShell</span></span>

<span data-ttu-id="c29f2-114">Pour afficher tous les fournisseurs de ressources dans Azure et l’état de l’inscription de votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="c29f2-115">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="c29f2-116">L’inscription d’un fournisseur de ressources configure votre abonnement pour travailler avec le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c29f2-117">L’étendue pour l’inscription est toujours l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c29f2-118">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c29f2-119">Toutefois, vous devrez peut-être inscrire manuellement certains fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c29f2-120">Pour inscrire un fournisseur de ressources, vous devez être autorisé à effectuer `/register/action`l’opération pour le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c29f2-121">Cette opération est incluse dans les rôles de contributeur et de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="c29f2-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="c29f2-122">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="c29f2-123">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c29f2-124">Pour afficher des informations pour un fournisseur de ressources particulier, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="c29f2-125">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="c29f2-126">Pour afficher les types de ressources pour un fournisseur de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="c29f2-127">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="c29f2-128">La version de l'API correspond à une version des opérations de l'API REST publiées par le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c29f2-129">Lorsqu'un fournisseur de ressources active de nouvelles fonctionnalités, une nouvelle version de l'API REST sera publiée.</span><span class="sxs-lookup"><span data-stu-id="c29f2-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="c29f2-130">Pour obtenir les versions d’API disponibles pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="c29f2-131">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="c29f2-132">Resource Manager est pris en charge dans toutes les régions, mais il est possible que certaines ressources que vous déployez ne soient pas prises en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="c29f2-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c29f2-133">Par ailleurs, il peut y avoir des limitations sur votre abonnement qui vous empêchent d’utiliser certaines régions prenant en charge la ressource.</span><span class="sxs-lookup"><span data-stu-id="c29f2-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="c29f2-134">Pour obtenir les emplacements pris en charge pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="c29f2-135">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="c29f2-136">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c29f2-136">Azure CLI</span></span>
<span data-ttu-id="c29f2-137">Pour afficher tous les fournisseurs de ressources dans Azure et l’état de l’inscription de votre abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="c29f2-138">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="c29f2-139">L’inscription d’un fournisseur de ressources configure votre abonnement pour travailler avec le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c29f2-140">L’étendue pour l’inscription est toujours l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c29f2-141">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c29f2-142">Toutefois, vous devrez peut-être inscrire manuellement certains fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c29f2-143">Pour inscrire un fournisseur de ressources, vous devez être autorisé à effectuer `/register/action`l’opération pour le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c29f2-144">Cette opération est incluse dans les rôles de contributeur et de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="c29f2-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="c29f2-145">Qui retourne un message indiquant que l’inscription est en cours.</span><span class="sxs-lookup"><span data-stu-id="c29f2-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="c29f2-146">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c29f2-147">Pour afficher des informations pour un fournisseur de ressources particulier, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="c29f2-148">Qui retourne des résultats semblables à :</span><span class="sxs-lookup"><span data-stu-id="c29f2-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="c29f2-149">Pour afficher les types de ressources pour un fournisseur de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="c29f2-150">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="c29f2-151">La version de l'API correspond à une version des opérations de l'API REST publiées par le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c29f2-152">Lorsqu'un fournisseur de ressources active de nouvelles fonctionnalités, une nouvelle version de l'API REST sera publiée.</span><span class="sxs-lookup"><span data-stu-id="c29f2-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="c29f2-153">Pour obtenir les versions d’API disponibles pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="c29f2-154">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="c29f2-155">Resource Manager est pris en charge dans toutes les régions, mais il est possible que certaines ressources que vous déployez ne soient pas prises en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="c29f2-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c29f2-156">Par ailleurs, il peut y avoir des limitations sur votre abonnement qui vous empêchent d’utiliser certaines régions prenant en charge la ressource.</span><span class="sxs-lookup"><span data-stu-id="c29f2-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="c29f2-157">Pour obtenir les emplacements pris en charge pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="c29f2-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="c29f2-158">Résultat :</span><span class="sxs-lookup"><span data-stu-id="c29f2-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="c29f2-159">Portail</span><span class="sxs-lookup"><span data-stu-id="c29f2-159">Portal</span></span>

<span data-ttu-id="c29f2-160">Pour afficher tous les fournisseurs de ressources dans Azure et l’état de l’inscription de votre abonnement, sélectionnez **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="c29f2-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![sélectionner les abonnements](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="c29f2-162">Choisissez l’abonnement à afficher.</span><span class="sxs-lookup"><span data-stu-id="c29f2-162">Choose the subscription to view.</span></span>

![spécifier l’abonnement](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="c29f2-164">Sélectionnez **Fournisseurs de ressources** et affichez la liste des fournisseurs de ressources disponibles.</span><span class="sxs-lookup"><span data-stu-id="c29f2-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![afficher les fournisseurs de ressources](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="c29f2-166">L’inscription d’un fournisseur de ressources configure votre abonnement pour travailler avec le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c29f2-167">L’étendue pour l’inscription est toujours l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c29f2-168">Par défaut, de nombreux fournisseurs de ressources sont enregistrés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c29f2-169">Toutefois, vous devrez peut-être inscrire manuellement certains fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c29f2-170">Pour inscrire un fournisseur de ressources, vous devez être autorisé à effectuer `/register/action`l’opération pour le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c29f2-171">Cette opération est incluse dans les rôles de contributeur et de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="c29f2-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="c29f2-172">Pour inscrire un fournisseur de ressources, sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="c29f2-172">To register a resource provider, select **Register**.</span></span>

![inscrire un fournisseur de ressources](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="c29f2-174">Vous ne pouvez pas annuler l’inscription d’un fournisseur de ressources lorsque vous avez encore des types de ressources de ce fournisseur de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="c29f2-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c29f2-175">Pour afficher des informations pour un fournisseur de ressources particulier, sélectionnez **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="c29f2-175">To see information for a particular resource provider, select **More services**.</span></span>

![sélectionner d’autres services](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="c29f2-177">Recherchez **Explorateur de ressources** et sélectionnez-le dans les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="c29f2-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![sélectionner l’Explorateur de ressources](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="c29f2-179">Sélectionnez **Fournisseurs**.</span><span class="sxs-lookup"><span data-stu-id="c29f2-179">Select **Providers**.</span></span>

![sélectionner les fournisseurs](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="c29f2-181">Sélectionnez le fournisseur de ressources et le type de ressource que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="c29f2-181">Select the resource provider and resource type that you want to view.</span></span>

![sélectionner le type de ressource](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="c29f2-183">Resource Manager est pris en charge dans toutes les régions, mais il est possible que certaines ressources que vous déployez ne soient pas prises en charge dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="c29f2-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c29f2-184">Par ailleurs, il peut y avoir des limitations sur votre abonnement qui vous empêchent d’utiliser certaines régions prenant en charge la ressource.</span><span class="sxs-lookup"><span data-stu-id="c29f2-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="c29f2-185">L’Explorateur de ressources affiche les emplacements valides pour le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="c29f2-185">The resource explorer displays valid locations for the resource type.</span></span>

![afficher les emplacements](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="c29f2-187">La version de l'API correspond à une version des opérations de l'API REST publiées par le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="c29f2-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c29f2-188">Lorsqu'un fournisseur de ressources active de nouvelles fonctionnalités, une nouvelle version de l'API REST sera publiée.</span><span class="sxs-lookup"><span data-stu-id="c29f2-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="c29f2-189">L’Explorateur de ressources affiche les versions d’API valides pour le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="c29f2-189">The resource explorer displays valid API versions for the resource type.</span></span>

![afficher les versions d’API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="c29f2-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c29f2-191">Next steps</span></span>
* <span data-ttu-id="c29f2-192">Pour en savoir plus sur la création de modèles Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c29f2-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c29f2-193">Pour en savoir plus sur le déploiement de ressources, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c29f2-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="c29f2-194">Pour afficher les opérations pour un fournisseur de ressources, consultez [API REST Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="c29f2-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

