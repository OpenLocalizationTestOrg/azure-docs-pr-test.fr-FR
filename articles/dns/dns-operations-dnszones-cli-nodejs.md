---
title: zones DNS de Azure - Azure CLI 1.0 aaaManage DNS | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure CLI 1.0. Cet article explique comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="77ef9-104">Comment toomanage les Zones DNS à l’aide d’Azure DNS hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="77ef9-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77ef9-105">Portail</span><span class="sxs-lookup"><span data-stu-id="77ef9-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="77ef9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77ef9-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="77ef9-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="77ef9-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="77ef9-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="77ef9-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="77ef9-109">Ce guide montre comment toomanage votre DNS zones à l’aide de hello inter-plateformes CLI Azure 1.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="77ef9-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="77ef9-110">Vous pouvez également gérer vos zones DNS à l’aide de [Azure PowerShell](dns-operations-dnszones.md) ou de bienvenue du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77ef9-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="77ef9-111">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="77ef9-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="77ef9-112">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="77ef9-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="77ef9-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.</span><span class="sxs-lookup"><span data-stu-id="77ef9-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="77ef9-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="77ef9-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="77ef9-115">Introduction</span><span class="sxs-lookup"><span data-stu-id="77ef9-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="77ef9-116">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="77ef9-116">Getting help</span></span>

<span data-ttu-id="77ef9-117">Toutes les commandes CLI 1.0 relatives tooAzure DNS commence par `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="77ef9-118">Aide est disponible pour chaque commande à l’aide de hello `--help` option (forme abrégée : `-h`).</span><span class="sxs-lookup"><span data-stu-id="77ef9-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="77ef9-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="77ef9-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="77ef9-120">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="77ef9-120">Create a DNS zone</span></span>

<span data-ttu-id="77ef9-121">Une zone DNS est créée à l’aide de hello `azure network dns zone create` commande.</span><span class="sxs-lookup"><span data-stu-id="77ef9-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="77ef9-122">Pour obtenir de l’aide, consultez l’article `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="77ef9-123">Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="77ef9-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="77ef9-124">toocreate une zone DNS avec balises</span><span class="sxs-lookup"><span data-stu-id="77ef9-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="77ef9-125">Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*, à l’aide de hello `--tags` paramètre (forme abrégée : `-t`) :</span><span class="sxs-lookup"><span data-stu-id="77ef9-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="77ef9-126">Obtention d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="77ef9-126">Get a DNS zone</span></span>

<span data-ttu-id="77ef9-127">tooretrieve une zone DNS, utilisez `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="77ef9-128">Pour obtenir de l’aide, consultez l’article `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="77ef9-129">exemple Hello retourne zone DNS de hello *contoso.com* et ses données associées du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="77ef9-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="77ef9-130">Hello, l’exemple suivant est la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="77ef9-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="77ef9-131">Notez que les enregistrements DNS ne sont pas retournés par `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="77ef9-132">utiliser des enregistrements DNS de toolist, `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="77ef9-133">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="77ef9-133">List DNS zones</span></span>

<span data-ttu-id="77ef9-134">utiliser des zones DNS tooenumerate `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="77ef9-135">Pour obtenir de l’aide, consultez l’article `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="77ef9-136">Groupe de ressources en spécifiant hello répertorie uniquement les zones dans le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="77ef9-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="77ef9-137">L’omission de groupe de ressources hello répertorie toutes les zones d’abonnement de hello :</span><span class="sxs-lookup"><span data-stu-id="77ef9-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="77ef9-138">Mise à jour d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="77ef9-138">Update a DNS zone</span></span>

<span data-ttu-id="77ef9-139">Tooa modifications ressource de zone DNS peut être établie en utilisant `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="77ef9-140">Pour obtenir de l’aide, consultez l’article `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="77ef9-141">Cette commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="77ef9-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="77ef9-142">Il est tooupdate utilisé uniquement les propriétés de ressource de zone hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="77ef9-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="77ef9-143">Ces propriétés sont actuellement limitée toohello [Azure Resource Manager « balises »](dns-zones-records.md#tags) pour les ressources de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="77ef9-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="77ef9-144">Hello suivant montre comment les balises tooupdate hello sur une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="77ef9-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="77ef9-145">les balises existantes Hello sont remplacés par la valeur hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="77ef9-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="77ef9-146">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="77ef9-146">Delete a DNS Zone</span></span>

<span data-ttu-id="77ef9-147">Les zones DNS peuvent être supprimées en utilisant `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="77ef9-148">Pour obtenir de l’aide, consultez l’article `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="77ef9-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="77ef9-149">Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="77ef9-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="77ef9-150">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="77ef9-150">This operation cannot be undone.</span></span> <span data-ttu-id="77ef9-151">Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="77ef9-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="77ef9-152">tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="77ef9-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="77ef9-153">Cette commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="77ef9-153">This command prompts for confirmation.</span></span> <span data-ttu-id="77ef9-154">Hello facultatif `--quiet` basculer (forme abrégée : `-q`) supprime cette invite.</span><span class="sxs-lookup"><span data-stu-id="77ef9-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="77ef9-155">Hello suivant montre comment toodelete hello zone *contoso.com* du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="77ef9-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="77ef9-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77ef9-156">Next steps</span></span>

<span data-ttu-id="77ef9-157">Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-getstarted-create-recordset-cli-nodejs.md) dans votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="77ef9-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="77ef9-158">Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="77ef9-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

