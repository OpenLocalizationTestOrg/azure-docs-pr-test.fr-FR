---
title: "Support d’Azure Resource Manager pour l’équilibrage de charge | Microsoft Docs"
description: "Utilisation de Powershell pour l’équilibrage de charge avec Azure Resource Manager. Utilisation de modèles pour l'équilibrage de charge"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="c0a2a-104">Utilisation de la prise en charge d’Azure Resource Manager pour l’équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c0a2a-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="c0a2a-105">Azure Resource Manager est l’infrastructure de gestion des services par défaut dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="c0a2a-106">Azure Load Balancer peut être géré à l’aide des outils et des API basés sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="c0a2a-107">Concepts</span><span class="sxs-lookup"><span data-stu-id="c0a2a-107">Concepts</span></span>

<span data-ttu-id="c0a2a-108">Avec Azure Resource Manager, Azure Load Balancer contient les ressources enfants suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0a2a-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="c0a2a-109">Configuration d’une adresse IP frontale : un équilibreur de charge peut inclure une ou plusieurs adresses IP frontales, également appelées « adresses IP virtuelles ».</span><span class="sxs-lookup"><span data-stu-id="c0a2a-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="c0a2a-110">Ces adresses IP servent d'entrée pour le trafic.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="c0a2a-111">Pool d’adresses principal : il s’agit des adresses IP associées à la carte d’interface réseau (NIC) des machines virtuelles vers lesquelles la charge sera distribuée.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="c0a2a-112">Règles d'équilibrage de charge : une propriété de règle mappe une combinaison donnée d'adresse IP et de port frontaux vers un ensemble de combinaisons d'adresses IP et de port principaux.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="c0a2a-113">Un même équilibreur de charge peut avoir plusieurs règles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="c0a2a-114">Chaque règle est une combinaison d’une adresse IP et d’un port frontaux et d’une adresse IP et d’un port principaux associés aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="c0a2a-115">Sondes : les sondes vous permettent d'effectuer le suivi de l'intégrité des instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="c0a2a-116">En cas d'échec d'une sonde d'intégrité, l'instance de machine virtuelle est automatiquement mise hors service.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="c0a2a-117">Règles NAT de trafic entrant : règles NAT définissant le trafic entrant qui transite via l'adresse IP frontale et est distribué à l'adresse IP principale.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="c0a2a-118">Modèles de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="c0a2a-118">Quickstart templates</span></span>

<span data-ttu-id="c0a2a-119">Azure Resource Manager vous permet d’approvisionner vos applications à l'aide d'un modèle déclaratif.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="c0a2a-120">Dans un modèle unique, vous pouvez déployer plusieurs services ainsi que leurs dépendances.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="c0a2a-121">Le même modèle vous permet de déployer plusieurs fois votre application à chaque phase du cycle de vie de l’application.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="c0a2a-122">Les modèles peuvent inclure des définitions de machines virtuelles, de réseaux virtuels, de groupes à haute disponibilité, d’interfaces réseau (NIC), de comptes de stockage, d’équilibreurs de charge, de groupes de sécurité réseau et d’adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="c0a2a-123">Avec des modèles, vous pouvez créer tout ce dont vous avez besoin pour une application complexe.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="c0a2a-124">Le contrôle de version et la collaboration du fichier de modèle peuvent être vérifiés dans le système de gestion de contenu.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="c0a2a-125">En savoir plus sur les modèles</span><span class="sxs-lookup"><span data-stu-id="c0a2a-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="c0a2a-126">En savoir plus sur les ressources de réseau</span><span class="sxs-lookup"><span data-stu-id="c0a2a-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="c0a2a-127">Des modèles de démarrage rapide utilisant Azure Load Balancer se trouvent dans un [référentiel GitHub](https://github.com/Azure/azure-quickstart-templates) qui héberge un ensemble de modèles générés par la communauté.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="c0a2a-128">Exemples de modèles :</span><span class="sxs-lookup"><span data-stu-id="c0a2a-128">Examples of templates:</span></span>

* [<span data-ttu-id="c0a2a-129">2 machines virtuelles dans un équilibrage de charge et les règles d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c0a2a-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="c0a2a-130">2 machines virtuelles dans un réseau virtuel avec un équilibrage de charge interne et les règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c0a2a-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="c0a2a-131">2 machines virtuelles dans un équilibrage de charge et la configuration des règles NAT sur l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c0a2a-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="c0a2a-132">Configuration de l'équilibrage de charge Azure avec PowerShell ou la CLI</span><span class="sxs-lookup"><span data-stu-id="c0a2a-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="c0a2a-133">Prise en main des applets de commande, des outils de ligne de commande et des API REST Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0a2a-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="c0a2a-134">[cmdlets de mise en réseau Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) peuvent être utilisées pour créer un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="c0a2a-135">Création d’un équilibrage de charge à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0a2a-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="c0a2a-136">Utilisation de la CLI Azure avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0a2a-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="c0a2a-137">API REST de l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c0a2a-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="c0a2a-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0a2a-138">Next steps</span></span>

<span data-ttu-id="c0a2a-139">Vous pouvez également [commencer par créer un équilibrage de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="c0a2a-140">Découvrez comment gérer les [paramètres de délai d’expiration TCP inactif pour un équilibreur de charge](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="c0a2a-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="c0a2a-141">C’est important lorsque votre application a besoin de conserver des connexions actives pour les serveurs situés derrière un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="c0a2a-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
