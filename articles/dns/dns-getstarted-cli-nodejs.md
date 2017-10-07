---
title: "aaaGet main DNS Azure à l’aide d’Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate DNS zone et cet enregistrement dans le système DNS Azure. Ceci est un toocreate guide pas à pas et que vous gérez votre première zone DNS et un enregistrement à l’aide de hello Azure CLI 1.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="d9297-104">Prise en main d’Azure DNS à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9297-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9297-105">portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9297-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="d9297-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9297-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="d9297-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9297-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="d9297-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9297-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="d9297-109">Cet article vous guide tout hello étapes toocreate votre première zone DNS et à l’aide de l’enregistrement hello à multiplateforme Azure CLI 1.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="d9297-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d9297-110">Vous pouvez également effectuer ces étapes à l’aide de hello portail Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9297-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="d9297-111">Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier.</span><span class="sxs-lookup"><span data-stu-id="d9297-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="d9297-112">toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="d9297-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="d9297-113">Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="d9297-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="d9297-114">Enfin, toopublish votre serveur DNS de la zone toohello Internet, vous avez besoin de serveurs de noms tooconfigure hello pour le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="d9297-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="d9297-115">Chacune de ces étapes est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d9297-115">Each of these steps is described below.</span></span>

<span data-ttu-id="d9297-116">Ces instructions supposent que vous avez déjà installé et connecté tooAzure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="d9297-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="d9297-117">Pour plus d’aide, consultez [fonctionnement des zones toomanage DNS à l’aide d’Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="d9297-118">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="d9297-118">Create hello resource group</span></span>

<span data-ttu-id="d9297-119">Avant de créer la zone DNS de hello, un groupe de ressources est créé de Zone DNS de hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="d9297-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="d9297-120">Hello Voici commande hello.</span><span class="sxs-lookup"><span data-stu-id="d9297-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="d9297-121">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="d9297-121">Create a DNS zone</span></span>

<span data-ttu-id="d9297-122">Une zone DNS est créée à l’aide de hello `azure network dns zone create` commande.</span><span class="sxs-lookup"><span data-stu-id="d9297-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="d9297-123">aide toosee de cette commande, tapez `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="d9297-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="d9297-124">Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d9297-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="d9297-125">Utilisez hello exemple toocreate une zone DNS, en spécifiant les valeurs hello pour votre propre.</span><span class="sxs-lookup"><span data-stu-id="d9297-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="d9297-126">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="d9297-126">Create a DNS record</span></span>

<span data-ttu-id="d9297-127">toocreate un enregistrement DNS, utilisez hello `azure network dns record-set add-record` commande.</span><span class="sxs-lookup"><span data-stu-id="d9297-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="d9297-128">Pour obtenir de l’aide, consultez l’article `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="d9297-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="d9297-129">Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ».</span><span class="sxs-lookup"><span data-stu-id="d9297-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="d9297-130">nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="d9297-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="d9297-131">type d’enregistrement Hello est « A », avec l’adresse IP « 1.2.3.4 », et une durée de vie de 3 600 secondes (1 heure) de la valeur par défaut est utilisée.</span><span class="sxs-lookup"><span data-stu-id="d9297-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="d9297-132">Pour les autres types d’enregistrements, pour des jeux d’enregistrements avec plusieurs enregistrements, pour les autres valeurs de durée de vie et toomodify les enregistrements existants, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="d9297-133">Affichage des enregistrements</span><span class="sxs-lookup"><span data-stu-id="d9297-133">View records</span></span>

<span data-ttu-id="d9297-134">les enregistrements DNS toolist hello dans votre fuseau, utilisez :</span><span class="sxs-lookup"><span data-stu-id="d9297-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="d9297-135">Mettre à jour les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="d9297-135">Update name servers</span></span>

<span data-ttu-id="d9297-136">Une fois que vous êtes satisfait que votre zone DNS et les enregistrements ont été configurées correctement, vous devez tooconfigure votre nom de domaine toouse serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d9297-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="d9297-137">Cela permet à d’autres utilisateurs sur hello Internet toofind vos enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="d9297-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="d9297-138">serveurs de noms Hello pour votre zone sont fournies par hello `azure network dns zone show` commande :</span><span class="sxs-lookup"><span data-stu-id="d9297-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="d9297-139">Ces serveurs de noms doivent être configurés avec le Registre des noms de domaine hello (où vous avez acheté nom de domaine hello).</span><span class="sxs-lookup"><span data-stu-id="d9297-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="d9297-140">Tooset d’option hello des serveurs de noms hello pour le domaine de hello propose de votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="d9297-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="d9297-141">Pour plus d’informations, consultez [déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="d9297-142">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="d9297-142">Delete all resources</span></span>
 
<span data-ttu-id="d9297-143">toodelete toutes les ressources créées dans cet article, hello take suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="d9297-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d9297-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9297-144">Next steps</span></span>

<span data-ttu-id="d9297-145">toolearn en savoir plus sur Azure DNS, consultez [vue d’ensemble de DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="d9297-146">toolearn savoir plus sur la gestion des zones DNS dans le système DNS Azure, consultez [zones DNS de gestion dans DNS Azure à l’aide d’Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="d9297-147">toolearn savoir plus sur la gestion des enregistrements DNS dans le système DNS Azure, consultez [des enregistrements DNS de gérer et enregistrement définit dans le système DNS d’Azure à l’aide d’Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d9297-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

