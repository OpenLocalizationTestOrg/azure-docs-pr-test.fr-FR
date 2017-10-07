---
title: "prise en charge du Gestionnaire de ressources pour l’équilibrage de charge d’aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="36139-104">Utilisation de la prise en charge d’Azure Resource Manager pour l’équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="36139-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="36139-105">Le Gestionnaire de ressources Azure est un framework de gestion préférés hello pour les services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="36139-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="36139-106">Azure Load Balancer peut être géré à l’aide des outils et des API basés sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36139-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="36139-107">Concepts</span><span class="sxs-lookup"><span data-stu-id="36139-107">Concepts</span></span>

<span data-ttu-id="36139-108">Avec le Gestionnaire de ressources, équilibrage de charge Azure contient hello suivant des ressources enfants :</span><span class="sxs-lookup"><span data-stu-id="36139-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="36139-109">Configuration d’une adresse IP frontale : un équilibreur de charge peut inclure une ou plusieurs adresses IP frontales, également appelées « adresses IP virtuelles ».</span><span class="sxs-lookup"><span data-stu-id="36139-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="36139-110">Ces adresses IP servent d’entrée pour le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="36139-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="36139-111">Pool d’adresses principal, il s’agit des adresses IP associées machine virtuelle de hello Interface de carte réseau (NIC) toowhich charge sera distribué.</span><span class="sxs-lookup"><span data-stu-id="36139-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="36139-112">Règles d’équilibrage de charge – une propriété de règle mappe une adresse IP donnée frontal et le port jeu tooa de combinaison d’adresses IP de serveur principal et combinaison de port.</span><span class="sxs-lookup"><span data-stu-id="36139-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="36139-113">Un même équilibreur de charge peut avoir plusieurs règles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="36139-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="36139-114">Chaque règle est une combinaison d’une adresse IP et d’un port frontaux et d’une adresse IP et d’un port principaux associés aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="36139-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="36139-115">Sondes – sondes activer vous tookeep suivi d’intégrité hello des instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="36139-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="36139-116">Si une sonde d’intégrité échoue, instance de machine virtuelle hello est automatiquement mis hors rotation.</span><span class="sxs-lookup"><span data-stu-id="36139-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="36139-117">Des règles NAT de trafic entrant – définissant les règles NAT hello entrant qui traversent hello frontal IP et adresse IP de fin toohello distribuée précédent.</span><span class="sxs-lookup"><span data-stu-id="36139-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="36139-118">Modèles de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="36139-118">Quickstart templates</span></span>

<span data-ttu-id="36139-119">Le Gestionnaire de ressources Azure vous permet de tooprovision vos applications à l’aide d’un modèle déclaratif.</span><span class="sxs-lookup"><span data-stu-id="36139-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="36139-120">Dans un modèle unique, vous pouvez déployer plusieurs services ainsi que leurs dépendances.</span><span class="sxs-lookup"><span data-stu-id="36139-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="36139-121">Vous utilisez hello même modèle toorepeatedly déployer votre application au cours de chaque étape du cycle de vie application hello.</span><span class="sxs-lookup"><span data-stu-id="36139-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="36139-122">Les modèles peuvent inclure des définitions de machines virtuelles, de réseaux virtuels, de groupes à haute disponibilité, d’interfaces réseau (NIC), de comptes de stockage, d’équilibreurs de charge, de groupes de sécurité réseau et d’adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="36139-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="36139-123">Avec des modèles, vous pouvez créer tout ce dont vous avez besoin pour une application complexe.</span><span class="sxs-lookup"><span data-stu-id="36139-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="36139-124">fichier de modèle Hello peut être vérifiée dans le système de gestion de contenu pour le contrôle de version et de collaboration.</span><span class="sxs-lookup"><span data-stu-id="36139-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="36139-125">En savoir plus sur les modèles</span><span class="sxs-lookup"><span data-stu-id="36139-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="36139-126">En savoir plus sur les ressources de réseau</span><span class="sxs-lookup"><span data-stu-id="36139-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="36139-127">Des modèles de démarrage rapide utilisant Azure Load Balancer se trouvent dans un [référentiel GitHub](https://github.com/Azure/azure-quickstart-templates) qui héberge un ensemble de modèles générés par la communauté.</span><span class="sxs-lookup"><span data-stu-id="36139-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="36139-128">Exemples de modèles :</span><span class="sxs-lookup"><span data-stu-id="36139-128">Examples of templates:</span></span>

* [<span data-ttu-id="36139-129">2 machines virtuelles dans un équilibrage de charge et les règles d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="36139-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="36139-130">2 machines virtuelles dans un réseau virtuel avec un équilibrage de charge interne et les règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="36139-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="36139-131">2 machines virtuelles dans un équilibreur de charge et configurer des règles NAT sur hello équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="36139-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="36139-132">Configuration de l'équilibrage de charge Azure avec PowerShell ou la CLI</span><span class="sxs-lookup"><span data-stu-id="36139-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="36139-133">Prise en main des applets de commande, des outils de ligne de commande et des API REST Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36139-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="36139-134">[Applets de commande de mise en réseau Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) peut être utilisé toocreate un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="36139-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="36139-135">Comment toocreate un équilibreur de charge à l’aide du Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="36139-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="36139-136">À l’aide de hello CLI d’Azure avec la gestion des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="36139-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="36139-137">API REST de l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="36139-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="36139-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36139-138">Next steps</span></span>

<span data-ttu-id="36139-139">Vous pouvez également [commencer par créer un équilibrage de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="36139-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="36139-140">Découvrez comment toomanage [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="36139-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="36139-141">Ceci est important lorsque votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="36139-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
