---
title: zones DNS de Azure - Azure CLI 2.0 aaaManage DNS | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure CLI 2.0. Cet article explique comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure."
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
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="29e22-104">Comment toomanage les Zones DNS à l’aide d’Azure DNS hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="29e22-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="29e22-105">Portail</span><span class="sxs-lookup"><span data-stu-id="29e22-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="29e22-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29e22-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="29e22-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="29e22-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="29e22-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="29e22-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="29e22-109">Ce guide montre comment toomanage votre DNS zones à l’aide de hello inter-plateformes CLI d’Azure, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="29e22-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="29e22-110">Vous pouvez également gérer vos zones DNS à l’aide de [Azure PowerShell](dns-operations-dnszones.md) ou de bienvenue du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29e22-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="29e22-111">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="29e22-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="29e22-112">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="29e22-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="29e22-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="29e22-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="29e22-115">Introduction</span><span class="sxs-lookup"><span data-stu-id="29e22-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="29e22-116">Configuration d’Azure CLI 2.0 pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="29e22-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="29e22-117">Before you begin</span></span>

<span data-ttu-id="29e22-118">Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-118">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="29e22-119">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="29e22-119">An Azure subscription.</span></span> <span data-ttu-id="29e22-120">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29e22-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="29e22-121">Installez hello dernière version de hello Azure CLI 2.0, disponible pour Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="29e22-121">Install hello latest version of hello Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="29e22-122">Plus d’informations est disponible à l’adresse [installation Bonjour Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="29e22-122">More information is available at [Install hello Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="29e22-123">Se connecter tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="29e22-123">Sign in tooyour Azure account</span></span>

<span data-ttu-id="29e22-124">Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="29e22-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="29e22-125">Pour plus d’informations, consultez le journal dans tooAzure de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="29e22-125">For more information, see Log in tooAzure from hello Azure CLI</span></span>

```
az login
```

### <a name="select-hello-subscription"></a><span data-ttu-id="29e22-126">Sélectionnez l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="29e22-126">Select hello subscription</span></span>

<span data-ttu-id="29e22-127">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-127">Check hello subscriptions for hello account.</span></span>

```
az account list
```

<span data-ttu-id="29e22-128">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="29e22-128">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="29e22-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="29e22-129">Create a resource group</span></span>

<span data-ttu-id="29e22-130">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="29e22-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="29e22-131">Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="29e22-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="29e22-132">Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="29e22-132">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="29e22-133">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="29e22-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="29e22-134">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="29e22-134">Getting help</span></span>

<span data-ttu-id="29e22-135">Toutes les commandes CLI 2.0 relatives tooAzure DNS commence par `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="29e22-135">All CLI 2.0 commands relating tooAzure DNS start with `az network dns`.</span></span> <span data-ttu-id="29e22-136">Aide est disponible pour chaque commande à l’aide de hello `--help` option (forme abrégée : `-h`).</span><span class="sxs-lookup"><span data-stu-id="29e22-136">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="29e22-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29e22-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="29e22-138">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-138">Create a DNS zone</span></span>

<span data-ttu-id="29e22-139">Une zone DNS est créée à l’aide de hello `az network dns zone create` commande.</span><span class="sxs-lookup"><span data-stu-id="29e22-139">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="29e22-140">Pour obtenir de l’aide, consultez l’article `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="29e22-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="29e22-141">Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="29e22-141">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="29e22-142">toocreate une zone DNS avec balises</span><span class="sxs-lookup"><span data-stu-id="29e22-142">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="29e22-143">Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*, à l’aide de hello `--tags` paramètre (forme abrégée : `-t`) :</span><span class="sxs-lookup"><span data-stu-id="29e22-143">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="29e22-144">Obtention d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-144">Get a DNS zone</span></span>

<span data-ttu-id="29e22-145">tooretrieve une zone DNS, utilisez `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="29e22-145">tooretrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="29e22-146">Pour obtenir de l’aide, consultez l’article `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="29e22-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="29e22-147">exemple Hello retourne zone DNS de hello *contoso.com* et ses données associées du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="29e22-147">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="29e22-148">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-148">hello following example is hello response.</span></span>

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

<span data-ttu-id="29e22-149">Notez que les enregistrements DNS ne sont pas retournés par `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="29e22-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="29e22-150">utiliser des enregistrements DNS de toolist, `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="29e22-150">toolist DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="29e22-151">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-151">List DNS zones</span></span>

<span data-ttu-id="29e22-152">utiliser des zones DNS tooenumerate `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="29e22-152">tooenumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="29e22-153">Pour obtenir de l’aide, consultez l’article `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="29e22-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="29e22-154">Groupe de ressources en spécifiant hello répertorie uniquement les zones dans le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="29e22-154">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="29e22-155">L’omission de groupe de ressources hello répertorie toutes les zones d’abonnement de hello :</span><span class="sxs-lookup"><span data-stu-id="29e22-155">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="29e22-156">Mise à jour d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-156">Update a DNS zone</span></span>

<span data-ttu-id="29e22-157">Tooa modifications ressource de zone DNS peut être établie en utilisant `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="29e22-157">Changes tooa DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="29e22-158">Pour obtenir de l’aide, consultez l’article `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="29e22-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="29e22-159">Cette commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="29e22-159">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="29e22-160">Il est tooupdate utilisé uniquement les propriétés de ressource de zone hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="29e22-160">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="29e22-161">Ces propriétés sont actuellement limitée toohello [Azure Resource Manager « balises »](dns-zones-records.md#tags) pour les ressources de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-161">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="29e22-162">Hello suivant montre comment les balises tooupdate hello sur une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="29e22-162">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="29e22-163">les balises existantes Hello sont remplacés par la valeur hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="29e22-163">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="29e22-164">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="29e22-164">Delete a DNS zone</span></span>

<span data-ttu-id="29e22-165">Les zones DNS peuvent être supprimées en utilisant `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="29e22-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="29e22-166">Pour obtenir de l’aide, consultez l’article `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="29e22-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="29e22-167">Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="29e22-167">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="29e22-168">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="29e22-168">This operation cannot be undone.</span></span> <span data-ttu-id="29e22-169">Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="29e22-169">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="29e22-170">tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="29e22-170">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="29e22-171">Cette commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="29e22-171">This command prompts for confirmation.</span></span> <span data-ttu-id="29e22-172">Hello facultatif `--yes` commutateur supprime cette invite.</span><span class="sxs-lookup"><span data-stu-id="29e22-172">hello optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="29e22-173">Hello suivant montre comment toodelete hello zone *contoso.com* du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="29e22-173">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="29e22-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29e22-174">Next steps</span></span>

<span data-ttu-id="29e22-175">Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-getstarted-create-recordset-cli.md) dans votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="29e22-175">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="29e22-176">Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="29e22-176">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

