---
title: "Prise en main d’Azure DNS à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment créer une zone et un enregistrement DNS dans Azure DNS. Il s’agit d’un guide pas à pas pour la création et la gestion de votre première zone et de votre premier enregistrement DNS à l’aide d’Azure CLI 1.0."
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="5a6e9-104">Prise en main d’Azure DNS à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a6e9-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a6e9-105">portail Azure</span><span class="sxs-lookup"><span data-stu-id="5a6e9-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="5a6e9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a6e9-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="5a6e9-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a6e9-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="5a6e9-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5a6e9-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="5a6e9-109">Cet article vous guide tout au long de la procédure de création de votre première zone et de votre premier enregistrement DNS à l’aide de l’interface de ligne de commande Azure 1.0 multiplateforme, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="5a6e9-110">Vous pouvez également effectuer ces étapes à l’aide du portail Azure ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="5a6e9-111">Une zone DNS permet d’héberger les enregistrements DNS d’un domaine particulier.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="5a6e9-112">Pour commencer à héberger votre domaine dans le DNS Azure, vous devez créer une zone DNS pour ce nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="5a6e9-113">Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="5a6e9-114">Enfin, pour publier votre zone DNS sur Internet, vous devez configurer les serveurs de noms du domaine.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="5a6e9-115">Chacune de ces étapes est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-115">Each of these steps is described below.</span></span>

<span data-ttu-id="5a6e9-116">Ces instructions supposent que vous avez déjà installé Azure CLI 1.0 et que vous y êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="5a6e9-117">Pour obtenir de l’aide, consultez [Gestion des zones DNS dans Azure DNS à l’aide d’Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="5a6e9-118">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5a6e9-118">Create the resource group</span></span>

<span data-ttu-id="5a6e9-119">Avant de créer la zone DNS, un groupe de ressources est créé pour contenir la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="5a6e9-120">Voici la commande.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="5a6e9-121">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="5a6e9-121">Create a DNS zone</span></span>

<span data-ttu-id="5a6e9-122">Une zone DNS est créée à l'aide de la commande `azure network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="5a6e9-123">Pour consulter l’aide de cette commande, tapez `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="5a6e9-124">L’exemple ci-dessous crée une zone DNS appelée *contoso.com* dans le groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="5a6e9-125">Utilisez l’exemple pour créer une zone DNS, en remplaçant les valeurs indiquées par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="5a6e9-126">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="5a6e9-126">Create a DNS record</span></span>

<span data-ttu-id="5a6e9-127">Pour créer un enregistrement DNS, utilisez la commande `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="5a6e9-128">Pour obtenir de l’aide, consultez l’article `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="5a6e9-129">L’exemple suivant crée un enregistrement avec le nom relatif « www » dans la zone DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ».</span><span class="sxs-lookup"><span data-stu-id="5a6e9-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="5a6e9-130">Le nom complet du jeu d’enregistrements est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="5a6e9-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="5a6e9-131">Le type d’enregistrement est « A », avec l’adresse IP « 1.2.3.4 », et une durée de vie par défaut de 3 600 secondes (1 heure) est utilisée.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="5a6e9-132">Pour découvrir d’autres types d’enregistrements, des jeux d’enregistrements comportant plus d’un enregistrement et d’autres valeurs de durée de vie et pour modifier les enregistrements existants, consultez [Gérer les enregistrements DNS et les jeux d’enregistrement dans Azure DNS à l’aide d’Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="5a6e9-133">Affichage des enregistrements</span><span class="sxs-lookup"><span data-stu-id="5a6e9-133">View records</span></span>

<span data-ttu-id="5a6e9-134">Pour répertorier les enregistrements DNS dans votre zone, utilisez :</span><span class="sxs-lookup"><span data-stu-id="5a6e9-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="5a6e9-135">Mettre à jour les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="5a6e9-135">Update name servers</span></span>

<span data-ttu-id="5a6e9-136">Une fois que vous jugez que votre zone et vos enregistrements DNS ont été configurés correctement, vous devez configurer votre nom de domaine pour utiliser les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="5a6e9-137">Cela permet à d’autres utilisateurs sur Internet de rechercher vos enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="5a6e9-138">Les serveurs de noms de votre zone sont indiqués par la commande `azure network dns zone show` :</span><span class="sxs-lookup"><span data-stu-id="5a6e9-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
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

<span data-ttu-id="5a6e9-139">Ces serveurs de noms doivent être configurés avec le bureau d’enregistrement de noms de domaine (dans lequel vous avez acheté le nom de domaine).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="5a6e9-140">Votre bureau d’enregistrement offre la possibilité de configurer les serveurs de noms pour le domaine.</span><span class="sxs-lookup"><span data-stu-id="5a6e9-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="5a6e9-141">Pour plus d’informations, consultez [Délégation de domaine à Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="5a6e9-142">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="5a6e9-142">Delete all resources</span></span>
 
<span data-ttu-id="5a6e9-143">Pour supprimer toutes les ressources créées dans cet article, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a6e9-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5a6e9-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a6e9-144">Next steps</span></span>

<span data-ttu-id="5a6e9-145">Pour en savoir plus sur Azure DNS, consultez [Vue d’ensemble d’Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="5a6e9-146">Pour en savoir plus sur la gestion des zones DNS dans Azure DNS, consultez [Gestion des zones DNS dans Azure DNS à l’aide d’Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="5a6e9-147">Pour en savoir plus sur la gestion des enregistrements DNS dans Azure DNS, consultez [Gérer les enregistrements DNS et les jeux d’enregistrement dans Azure DNS à l’aide d’Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5a6e9-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

