---
title: "Se connecter à Azure Data Lake Store à partir de réseaux virtuels | Microsoft Docs"
description: "Se connecter à Azure Data Lake Store à partir de réseaux virtuels Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ff7d28d7b53e872b804788647b1e672fafcf6995
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="acd16-103">Accéder à Azure Data Lake Store à partir de machines virtuelles au sein d’un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="acd16-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="acd16-104">Azure Data Lake Store est un service PaaS qui s’exécute sur des adresses IP Internet publiques.</span><span class="sxs-lookup"><span data-stu-id="acd16-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="acd16-105">En général, tout serveur qui peut se connecter à l’Internet public peut également se connecter aux points de terminaison Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="acd16-106">Par défaut, toutes les machines virtuelles qui se trouvent dans des réseaux virtuels Azure peuvent accéder à Internet et, ainsi, accéder à Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="acd16-107">Toutefois, il est possible de configurer des machines virtuelles dans un réseau virtuel afin qu’elles n’aient pas accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="acd16-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span></span> <span data-ttu-id="acd16-108">Pour ces machines virtuelles, l’accès à Azure Data Lake Store est également restreint.</span><span class="sxs-lookup"><span data-stu-id="acd16-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="acd16-109">Bloquer l’accès à l’Internet public pour des machines virtuelles dans des réseaux virtuels Azure peut être effectué à l’aide d’une des approches suivantes.</span><span class="sxs-lookup"><span data-stu-id="acd16-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span></span>

* <span data-ttu-id="acd16-110">En configurant des groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="acd16-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="acd16-111">En configurant des itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="acd16-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="acd16-112">En échangeant des itinéraires par le biais de BGP (protocole de routage dynamique standard du secteur) quand ExpressRoute bloque l’accès à Internet</span><span class="sxs-lookup"><span data-stu-id="acd16-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span></span>

<span data-ttu-id="acd16-113">Dans cet article, vous allez apprendre à activer l’accès à Azure Data Lake Store à partir de machines virtuelles Azure soumises à des restrictions d’accès aux ressources, à l’aide d’une des trois méthodes mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="acd16-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span></span>

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="acd16-114">Activation de la connectivité à Azure Data Lake Store à partir de machines virtuelles bénéficiant d’une connectivité limitée</span><span class="sxs-lookup"><span data-stu-id="acd16-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="acd16-115">Pour accéder à Azure Data Lake Store à partir de ces machines virtuelles, vous devez les configurer de manière à ce qu’elles puissent accéder à l’adresse IP associée au compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span></span> <span data-ttu-id="acd16-116">Vous pouvez identifier les adresses IP de vos comptes Data Lake Store en résolvant les noms DNS de vos comptes (`<account>.azuredatalakestore.net`).</span><span class="sxs-lookup"><span data-stu-id="acd16-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="acd16-117">Pour ce faire, vous pouvez utiliser des outils tels que **nslookup**.</span><span class="sxs-lookup"><span data-stu-id="acd16-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="acd16-118">Ouvrez une invite de commandes sur votre ordinateur et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="acd16-118">Open a command prompt on your computer and run the following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="acd16-119">La sortie se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="acd16-119">The output resembles the following.</span></span> <span data-ttu-id="acd16-120">La valeur en regard de la propriété **Address** est l’adresse IP associée à votre compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="acd16-121">Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="acd16-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="acd16-122">Quand une règle de groupe de sécurité réseau est utilisée pour bloquer l’accès à Internet, vous pouvez créer un autre groupe de sécurité réseau qui autorise l’accès à l’adresse IP de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span></span> <span data-ttu-id="acd16-123">Pour plus d’informations sur les règles de groupe de sécurité réseau, consultez [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md) (Qu’est-ce qu’un groupe de sécurité réseau ?).</span><span class="sxs-lookup"><span data-stu-id="acd16-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="acd16-124">Pour savoir comment créer des groupes de sécurité réseau, consultez [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) (Guide pratique pour gérer les groupes de sécurité réseau à l’aide du portail Azure).</span><span class="sxs-lookup"><span data-stu-id="acd16-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="acd16-125">Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’un itinéraire défini par l’utilisateur ou d’ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acd16-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="acd16-126">Quand des itinéraires, définis par l’utilisateur ou échangés par le biais de BGP, sont utilisés pour bloquer l’accès à Internet, un itinéraire spécial doit être configuré afin que les machines virtuelles dans ces sous-réseaux puissent accéder aux points de terminaison Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="acd16-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="acd16-127">Pour plus d’informations, consultez [Présentation des itinéraires définis par l’utilisateur](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="acd16-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="acd16-128">Pour obtenir des instructions sur la création d’itinéraires définis par l’utilisateur, consultez [Création d’itinéraires définis par l’utilisateur (UDR) dans Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="acd16-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="acd16-129">Activation de la connectivité à partir de machines virtuelles restreintes à l’aide d’ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="acd16-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="acd16-130">Quand un circuit ExpressRoute est configuré, les serveurs locaux peuvent accéder à Data Lake Store par le biais de l’appairage public.</span><span class="sxs-lookup"><span data-stu-id="acd16-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="acd16-131">Pour plus d’informations sur la configuration d’ExpressRoute pour l’appairage public, consultez [Forum Aux Questions ExpressRoute](../expressroute/expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="acd16-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="acd16-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="acd16-132">See also</span></span>
* [<span data-ttu-id="acd16-133">Présentation d'Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="acd16-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="acd16-134">Sécurisation des données stockées dans Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="acd16-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)
