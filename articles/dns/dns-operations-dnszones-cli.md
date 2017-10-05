---
title: "Gérer des zones DNS dans Azure DNS - Azure CLI 2.0 | Microsoft Docs"
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure CLI 2.0. Cet article explique comment mettre à jour, supprimer et créer des zones DNS sur Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="27643-104">Gérer des zones DNS dans Azure DNS à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="27643-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27643-105">Portail</span><span class="sxs-lookup"><span data-stu-id="27643-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="27643-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27643-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="27643-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="27643-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="27643-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="27643-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="27643-109">Ce guide montre comment gérer vos zones DNS à l’aide de l’interface de ligne de commande Azure interplateforme, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="27643-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="27643-110">Vous pouvez également gérer vos zones DNS à l’aide [d’Azure PowerShell](dns-operations-dnszones.md) ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="27643-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="27643-111">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="27643-111">CLI versions to complete the task</span></span>

<span data-ttu-id="27643-112">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="27643-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="27643-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27643-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="27643-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27643-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="27643-115">Introduction</span><span class="sxs-lookup"><span data-stu-id="27643-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="27643-116">Configuration d’Azure CLI 2.0 pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="27643-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="27643-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="27643-117">Before you begin</span></span>

<span data-ttu-id="27643-118">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="27643-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="27643-119">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="27643-119">An Azure subscription.</span></span> <span data-ttu-id="27643-120">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27643-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="27643-121">Installez la dernière version d’Azure CLI 2.0, disponible pour Windows, Linux ou MAC.</span><span class="sxs-lookup"><span data-stu-id="27643-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="27643-122">Pour plus d’informations, consultez la page [Installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="27643-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="27643-123">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="27643-123">Sign in to your Azure account</span></span>

<span data-ttu-id="27643-124">Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="27643-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="27643-125">Pour en savoir plus, consultez Connectez-vous à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="27643-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="27643-126">Sélection de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="27643-126">Select the subscription</span></span>

<span data-ttu-id="27643-127">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="27643-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="27643-128">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="27643-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="27643-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="27643-129">Create a resource group</span></span>

<span data-ttu-id="27643-130">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="27643-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="27643-131">Ce dernier est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="27643-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="27643-132">Toutefois, étant donné que toutes les ressources DNS sont globales et non régionales, le choix de l’emplacement du groupe de ressources n’a aucun impact sur Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="27643-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="27643-133">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="27643-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="27643-134">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="27643-134">Getting help</span></span>

<span data-ttu-id="27643-135">Toutes les commandes CLI 2.0 liées à Azure DNS commencent par `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="27643-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="27643-136">Une aide est disponible pour chaque commande avec l’option `--help` (forme abrégée : `-h`).</span><span class="sxs-lookup"><span data-stu-id="27643-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="27643-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="27643-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="27643-138">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="27643-138">Create a DNS zone</span></span>

<span data-ttu-id="27643-139">Une zone DNS est créée à l'aide de la commande `az network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="27643-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="27643-140">Pour obtenir de l’aide, consultez l’article `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="27643-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="27643-141">L’exemple ci-dessous crée une zone DNS appelée *contoso.com* dans le groupe de ressources *MyResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="27643-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="27643-142">Pour créer une zone DNS avec des étiquettes</span><span class="sxs-lookup"><span data-stu-id="27643-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="27643-143">L’exemple suivant montre comment créer une zone DNS avec deux [balises Azure Resource Manager](dns-zones-records.md#tags), *projet = demo* et *env = test*, à l’aide du paramètre `--tags` (forme abrégée : `-t`) :</span><span class="sxs-lookup"><span data-stu-id="27643-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="27643-144">Obtention d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="27643-144">Get a DNS zone</span></span>

<span data-ttu-id="27643-145">Pour récupérer une zone DNS, utilisez `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="27643-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="27643-146">Pour obtenir de l’aide, consultez l’article `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="27643-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="27643-147">L’exemple suivant retourne la zone DNS *contoso.com* et les données associées à partir du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="27643-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="27643-148">L’exemple suivant est la réponse.</span><span class="sxs-lookup"><span data-stu-id="27643-148">The following example is the response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="27643-149">Notez que les enregistrements DNS ne sont pas retournés par `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="27643-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="27643-150">Pour lister les enregistrements DNS, utilisez `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="27643-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="27643-151">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="27643-151">List DNS zones</span></span>

<span data-ttu-id="27643-152">Pour énumérer des zones DNS, utilisez `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="27643-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="27643-153">Pour obtenir de l’aide, consultez l’article `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="27643-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="27643-154">Spécifier le groupe de ressources permet de ne lister que les zones du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="27643-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="27643-155">Omettre le groupe de ressources permet de lister toutes les zones de l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="27643-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="27643-156">Mise à jour d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="27643-156">Update a DNS zone</span></span>

<span data-ttu-id="27643-157">Vous pouvez apporter des modifications à une ressource de zone DNS à l’aide de `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="27643-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="27643-158">Pour obtenir de l’aide, consultez l’article `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="27643-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="27643-159">Cette commande ne met pas à jour les jeux d’enregistrements DNS dans la zone (voir [Gestion des enregistrements DNS](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="27643-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="27643-160">Elle est utilisée uniquement pour mettre à jour les propriétés de la ressource de zone elle-même.</span><span class="sxs-lookup"><span data-stu-id="27643-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="27643-161">Ces propriétés sont actuellement limitées aux [« balises » Azure Resource Manager](dns-zones-records.md#tags) de la ressource de zone.</span><span class="sxs-lookup"><span data-stu-id="27643-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="27643-162">L’exemple suivant montre comment mettre à jour les balises sur une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="27643-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="27643-163">Les balises existantes sont remplacées par la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="27643-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="27643-164">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="27643-164">Delete a DNS zone</span></span>

<span data-ttu-id="27643-165">Les zones DNS peuvent être supprimées en utilisant `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="27643-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="27643-166">Pour obtenir de l’aide, consultez l’article `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="27643-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="27643-167">Supprimer une zone DNS supprime également tous les enregistrements DNS de la zone.</span><span class="sxs-lookup"><span data-stu-id="27643-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="27643-168">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="27643-168">This operation cannot be undone.</span></span> <span data-ttu-id="27643-169">Si la zone DNS est en cours d’utilisation, les services utilisant la zone échouent lors de la suppression de la zone.</span><span class="sxs-lookup"><span data-stu-id="27643-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="27643-170">Pour vous protéger contre la suppression accidentelle de zones, consultez la page [Comment protéger des zones et enregistrements DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="27643-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="27643-171">Cette commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="27643-171">This command prompts for confirmation.</span></span> <span data-ttu-id="27643-172">Le switch `--yes` facultatif supprime cette invite.</span><span class="sxs-lookup"><span data-stu-id="27643-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="27643-173">L’exemple suivant montre comment supprimer la zone *contoso.com* à partir du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="27643-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="27643-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27643-174">Next steps</span></span>

<span data-ttu-id="27643-175">Découvrez comment [gérer des jeux d’enregistrements et des enregistrements](dns-getstarted-create-recordset-cli.md) dans votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="27643-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="27643-176">Découvrez comment [déléguer votre domaine à Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="27643-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

