---
title: "Prise en main d’Azure DNS à l’aide d’Azure CLI 2.0 | Microsoft Docs"
description: "Découvrez comment créer une zone et un enregistrement DNS dans Azure DNS. Il s’agit d’un guide pas à pas pour la création et la gestion de votre première zone et de votre premier enregistrement DNS à l’aide d’Azure CLI 2.0."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 6958d61b29961f59cb22f62bec55f2d467e7e7cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="38e1f-104">Prise en main d’Azure DNS à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38e1f-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38e1f-105">portail Azure</span><span class="sxs-lookup"><span data-stu-id="38e1f-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="38e1f-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38e1f-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="38e1f-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="38e1f-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="38e1f-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38e1f-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="38e1f-109">Cet article vous guide tout au long de la procédure de création de votre première zone et de votre premier enregistrement DNS à l’aide de l’interface de ligne de commande Azure 2.0 multiplateforme, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="38e1f-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="38e1f-110">Vous pouvez également effectuer ces étapes à l’aide du portail Azure ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38e1f-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="38e1f-111">Une zone DNS permet d’héberger les enregistrements DNS d’un domaine particulier.</span><span class="sxs-lookup"><span data-stu-id="38e1f-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="38e1f-112">Pour commencer à héberger votre domaine dans le DNS Azure, vous devez créer une zone DNS pour ce nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="38e1f-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="38e1f-113">Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="38e1f-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="38e1f-114">Enfin, pour publier votre zone DNS sur Internet, vous devez configurer les serveurs de noms du domaine.</span><span class="sxs-lookup"><span data-stu-id="38e1f-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="38e1f-115">Chacune de ces étapes est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="38e1f-115">Each of these steps is described below.</span></span>

<span data-ttu-id="38e1f-116">Ces instructions partent du principe que vous avez déjà installé Azure CLI 2.0 et que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="38e1f-116">These instructions assume you have already installed and signed in to Azure CLI 2.0.</span></span> <span data-ttu-id="38e1f-117">Pour obtenir de l’aide, consultez [Gérer des zones DNS dans Azure DNS à l’aide d’Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="38e1f-118">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="38e1f-118">Create the resource group</span></span>

<span data-ttu-id="38e1f-119">Avant de créer la zone DNS, un groupe de ressources est créé pour contenir la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="38e1f-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="38e1f-120">Voici la commande.</span><span class="sxs-lookup"><span data-stu-id="38e1f-120">The following shows the command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="38e1f-121">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="38e1f-121">Create a DNS zone</span></span>

<span data-ttu-id="38e1f-122">Une zone DNS est créée à l'aide de la commande `az network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="38e1f-122">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="38e1f-123">Pour consulter l’aide de cette commande, tapez `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="38e1f-123">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="38e1f-124">L’exemple ci-dessous crée une zone DNS appelée *contoso.com* dans le groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="38e1f-124">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="38e1f-125">Utilisez l’exemple pour créer une zone DNS, en remplaçant les valeurs indiquées par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="38e1f-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="38e1f-126">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="38e1f-126">Create a DNS record</span></span>

<span data-ttu-id="38e1f-127">Pour créer un enregistrement DNS, utilisez la commande `az network dns record-set [record type] add-record`.</span><span class="sxs-lookup"><span data-stu-id="38e1f-127">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="38e1f-128">Pour obtenir de l’aide, concernant les enregistrements A par exemple, consultez `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="38e1f-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="38e1f-129">L’exemple suivant crée un enregistrement avec le nom relatif « www » dans la zone DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ».</span><span class="sxs-lookup"><span data-stu-id="38e1f-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="38e1f-130">Le nom complet du jeu d’enregistrements est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="38e1f-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="38e1f-131">Le type d’enregistrement est « A », avec l’adresse IP « 1.2.3.4 », et une durée de vie par défaut de 3 600 secondes (1 heure) est utilisée.</span><span class="sxs-lookup"><span data-stu-id="38e1f-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="38e1f-132">Pour découvrir d’autres types d’enregistrements, des jeux d’enregistrements comportant plus d’un enregistrement et d’autres valeurs de durée de vie et pour modifier les enregistrements existants, consultez [Gérer les enregistrements DNS et les jeux d’enregistrement dans Azure DNS à l’aide d’Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="38e1f-133">Affichage des enregistrements</span><span class="sxs-lookup"><span data-stu-id="38e1f-133">View records</span></span>

<span data-ttu-id="38e1f-134">Pour répertorier les enregistrements DNS dans votre zone, utilisez :</span><span class="sxs-lookup"><span data-stu-id="38e1f-134">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="38e1f-135">Mettre à jour les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="38e1f-135">Update name servers</span></span>

<span data-ttu-id="38e1f-136">Une fois que vous jugez que votre zone et vos enregistrements DNS ont été configurés correctement, vous devez configurer votre nom de domaine pour utiliser les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="38e1f-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="38e1f-137">Cela permet à d’autres utilisateurs sur Internet de rechercher vos enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="38e1f-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="38e1f-138">Les serveurs de noms de votre zone sont indiqués par la commande `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="38e1f-138">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="38e1f-139">Pour afficher les noms de serveurs de noms, utilisez la sortie JSON, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="38e1f-139">To see the name server names, use JSON output, as shown in the following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="38e1f-140">Ces serveurs de noms doivent être configurés avec le bureau d’enregistrement de noms de domaine (dans lequel vous avez acheté le nom de domaine).</span><span class="sxs-lookup"><span data-stu-id="38e1f-140">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="38e1f-141">Votre bureau d’enregistrement offre la possibilité de configurer les serveurs de noms pour le domaine.</span><span class="sxs-lookup"><span data-stu-id="38e1f-141">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="38e1f-142">Pour plus d’informations, consultez [Délégation de domaine à Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-142">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="38e1f-143">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="38e1f-143">Delete all resources</span></span>
 
<span data-ttu-id="38e1f-144">Pour supprimer toutes les ressources créées dans cet article, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="38e1f-144">To delete all resources created in this article, take the following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="38e1f-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38e1f-145">Next steps</span></span>

<span data-ttu-id="38e1f-146">Pour en savoir plus sur Azure DNS, consultez [Vue d’ensemble d’Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-146">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="38e1f-147">Pour en savoir plus sur la gestion des zones DNS dans Azure DNS, consultez [Gérer des zones DNS dans Azure DNS à l’aide d’Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-147">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="38e1f-148">Pour en savoir plus sur la gestion des enregistrements DNS dans Azure DNS, consultez [Gérer les enregistrements DNS et les jeux d’enregistrement dans Azure DNS à l’aide d’Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="38e1f-148">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
