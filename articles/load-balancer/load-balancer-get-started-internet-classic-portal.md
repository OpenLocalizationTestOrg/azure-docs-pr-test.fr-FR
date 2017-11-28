---
title: "Créer un équilibrage de charge accessible sur Internet à l’aide du Portail Azure Classic | Microsoft Docs"
description: "Découvrez comment créer un équilibreur de charge accessible sur Internet dans un modèle de déploiement classique à l’aide du portail Azure Classic."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="13529-103">Création d’un équilibreur de charge accessible sur Internet (classique) dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="13529-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="13529-104">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="13529-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="13529-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13529-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="13529-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="13529-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="13529-107">Services cloud Azure</span><span class="sxs-lookup"><span data-stu-id="13529-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="13529-108">Avant d’utiliser des ressources Azure, il est important de comprendre qu’Azure dispose actuellement de deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="13529-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="13529-109">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="13529-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="13529-110">Pour consulter la documentation relative aux différents outils, cliquez sur les onglets situés en haut de cet article.</span><span class="sxs-lookup"><span data-stu-id="13529-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="13529-111">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="13529-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="13529-112">Vous pouvez également [découvrir comment créer un équilibreur de charge accessible sur Internet à l’aide d’Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="13529-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="13529-113">Configurer un équilibrage de charge accessible sur Internet pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="13529-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="13529-114">Afin d'équilibrer le trafic réseau à partir d'Internet sur les machines virtuelles d'un service cloud, vous devez créer un jeu d'équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="13529-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="13529-115">Cette procédure suppose que vous avez déjà créé les machines virtuelles et qu’elles sont toutes dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="13529-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="13529-116">**Pour configurer un ensemble d'équilibrage de charge interne pour les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="13529-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="13529-117">Dans le portail Azure Classic, cliquez sur **Machines virtuelles**, puis sur le nom d’une machine virtuelle du jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="13529-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="13529-118">Cliquez sur **Points de terminaison**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13529-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="13529-119">Sur la page **Ajouter un point de terminaison à une machine virtuelle** , cliquez sur la flèche droite.</span><span class="sxs-lookup"><span data-stu-id="13529-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="13529-120">Dans la page **Spécifier les détails du point de terminaison** :</span><span class="sxs-lookup"><span data-stu-id="13529-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="13529-121">Dans **Nom**, saisissez le nom du point de terminaison ou sélectionnez-en un dans la liste des points de terminaison prédéfinis pour les protocoles communs.</span><span class="sxs-lookup"><span data-stu-id="13529-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="13529-122">Dans **Protocole**, sélectionnez le protocole requis, TCP ou UDP, pour ce type de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="13529-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="13529-123">Dans **Port public et Port privé**, entrez les numéros de port dont se servira la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13529-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="13529-124">Vous pouvez utiliser le port privé et des règles de pare-feu sur la machine virtuelle pour rediriger le trafic de façon pertinente pour votre application.</span><span class="sxs-lookup"><span data-stu-id="13529-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="13529-125">Le port privé et le port public peuvent être identiques.</span><span class="sxs-lookup"><span data-stu-id="13529-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="13529-126">Par exemple, pour un point de terminaison pour le trafic Web (HTTP), vous pouvez attribuer le port 80 comme port public ou privé.</span><span class="sxs-lookup"><span data-stu-id="13529-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="13529-127">Sélectionnez **Créer un jeu d'équilibrage de la charge**, puis cliquez sur la flèche vers la droite.</span><span class="sxs-lookup"><span data-stu-id="13529-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="13529-128">Sur la page **Configurer le jeu d'équilibrage de la charge** , indiquez le nom du jeu d'équilibrage de charge et attribuez les valeurs correspondant au comportement de sonde de l'équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="13529-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="13529-129">L'équilibrage de la charge utilise des sondes pour déterminer si les machines virtuelles du jeu d'équilibrage de la charge sont en mesure de recevoir le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="13529-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="13529-130">Cliquez sur la coche pour créer le point de terminaison à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="13529-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="13529-131">**Oui** s’affiche dans la colonne **Nom du jeu d’équilibrage de la charge** de la page **Points de terminaison** de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13529-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="13529-132">Dans le portail, cliquez sur **Machines virtuelles**, sur le nom d’une machine virtuelle supplémentaire du jeu d’équilibrage de la charge, sur **Points de terminaison**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13529-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="13529-133">Sur la page **Ajouter un point de terminaison à la machine virtuelle**, cliquez sur **Ajouter un point de terminaison à un jeu d’équilibrage de la charge existant**, sélectionnez le nom du jeu d’équilibrage de la charge, puis cliquez sur la flèche vers la droite.</span><span class="sxs-lookup"><span data-stu-id="13529-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="13529-134">Sur la page **Spécifier les détails du point de terminaison** , tapez le nom du point de terminaison, puis cliquez sur la coche.</span><span class="sxs-lookup"><span data-stu-id="13529-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="13529-135">Pour les machines virtuelles supplémentaires dans le jeu d’équilibrage de la charge, répétez les étapes 8 à 10.</span><span class="sxs-lookup"><span data-stu-id="13529-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13529-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13529-136">Next steps</span></span>

[<span data-ttu-id="13529-137">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="13529-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="13529-138">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="13529-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="13529-139">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="13529-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
