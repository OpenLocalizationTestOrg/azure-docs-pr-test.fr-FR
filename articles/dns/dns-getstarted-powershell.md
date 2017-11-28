---
title: "aaaGet main DNS Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate DNS zone et cet enregistrement dans le système DNS Azure. Ceci est un toocreate guide pas à pas et gérer votre première zone DNS et enregistrer à l’aide de PowerShell."
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
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="65fe3-104">Prise en main d’Azure DNS à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="65fe3-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="65fe3-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="65fe3-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="65fe3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65fe3-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="65fe3-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="65fe3-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="65fe3-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="65fe3-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="65fe3-109">Cet article vous assiste hello étapes toocreate votre première zone DNS et un enregistrement à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65fe3-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="65fe3-110">Vous pouvez également effectuer ces étapes à l’aide de hello portail Azure ou hello CLI d’Azure inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="65fe3-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="65fe3-111">Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier.</span><span class="sxs-lookup"><span data-stu-id="65fe3-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="65fe3-112">toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="65fe3-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="65fe3-113">Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS.</span><span class="sxs-lookup"><span data-stu-id="65fe3-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="65fe3-114">Enfin, toopublish votre serveur DNS de la zone toohello Internet, vous avez besoin de serveurs de noms tooconfigure hello pour le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="65fe3-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="65fe3-115">Chacune de ces étapes est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="65fe3-115">Each of these steps is described below.</span></span>

<span data-ttu-id="65fe3-116">Ces instructions supposent que vous avez déjà installé et connecté tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65fe3-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="65fe3-117">Pour plus d’aide, consultez [fonctionnement des zones toomanage DNS à l’aide de PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="65fe3-118">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="65fe3-118">Create hello resource group</span></span>

<span data-ttu-id="65fe3-119">Avant de créer la zone DNS de hello, un groupe de ressources est créé de Zone DNS de hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="65fe3-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="65fe3-120">Hello Voici commande hello.</span><span class="sxs-lookup"><span data-stu-id="65fe3-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="65fe3-121">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="65fe3-121">Create a DNS zone</span></span>

<span data-ttu-id="65fe3-122">Une zone DNS est créée à l’aide de hello `New-AzureRmDnsZone` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="65fe3-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="65fe3-123">Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="65fe3-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="65fe3-124">Utilisez hello exemple toocreate une zone DNS, en spécifiant les valeurs hello pour votre propre.</span><span class="sxs-lookup"><span data-stu-id="65fe3-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="65fe3-125">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="65fe3-125">Create a DNS record</span></span>

<span data-ttu-id="65fe3-126">Vous créez des jeux d’enregistrements à l’aide de hello `New-AzureRmDnsRecordSet` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="65fe3-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="65fe3-127">Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com », dans le groupe de ressources « MyResourceGroup ».</span><span class="sxs-lookup"><span data-stu-id="65fe3-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="65fe3-128">nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="65fe3-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="65fe3-129">type d’enregistrement Hello est « A », avec l’adresse IP « 1.2.3.4 » et hello durée de vie est 3 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="65fe3-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="65fe3-130">Pour les autres types d’enregistrements, pour des jeux d’enregistrements avec plusieurs enregistrements et les enregistrements existants toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide d’Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="65fe3-131">Affichage des enregistrements</span><span class="sxs-lookup"><span data-stu-id="65fe3-131">View records</span></span>

<span data-ttu-id="65fe3-132">les enregistrements DNS toolist hello dans votre fuseau, utilisez :</span><span class="sxs-lookup"><span data-stu-id="65fe3-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="65fe3-133">Mettre à jour les serveurs de noms</span><span class="sxs-lookup"><span data-stu-id="65fe3-133">Update name servers</span></span>

<span data-ttu-id="65fe3-134">Une fois que vous êtes satisfait que votre zone DNS et les enregistrements ont été configurées correctement, vous devez tooconfigure votre nom de domaine toouse serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65fe3-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="65fe3-135">Cela permet à d’autres utilisateurs sur hello Internet toofind vos enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="65fe3-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="65fe3-136">serveurs de noms Hello pour votre zone sont fournies par hello `Get-AzureRmDnsZone` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="65fe3-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="65fe3-137">Ces serveurs de noms doivent être configurés avec le Registre des noms de domaine hello (où vous avez acheté nom de domaine hello).</span><span class="sxs-lookup"><span data-stu-id="65fe3-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="65fe3-138">Tooset d’option hello des serveurs de noms hello pour le domaine de hello propose de votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="65fe3-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="65fe3-139">Pour plus d’informations, consultez [déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="65fe3-140">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="65fe3-140">Delete all resources</span></span>

<span data-ttu-id="65fe3-141">toodelete toutes les ressources créées dans cet article, hello take suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="65fe3-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="65fe3-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65fe3-142">Next steps</span></span>

<span data-ttu-id="65fe3-143">toolearn en savoir plus sur Azure DNS, consultez [vue d’ensemble de DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="65fe3-144">toolearn savoir plus sur la gestion des zones DNS dans le système DNS Azure, consultez [zones DNS de gestion dans DNS Azure à l’aide de PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="65fe3-145">toolearn savoir plus sur la gestion des enregistrements DNS dans le système DNS Azure, consultez [des enregistrements DNS de gérer et enregistrement définit dans le système DNS d’Azure à l’aide de PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="65fe3-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

