---
title: "équilibrage de charge aaaCreate une côté Internet - portail Azure classic | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide de modèle de déploiement classique hello portail Azure classic"
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
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="d90f7-103">Commencer à créer un Internet faisant face à l’équilibrage de charge (classiques) Bonjour portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="d90f7-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d90f7-104">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="d90f7-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="d90f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d90f7-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="d90f7-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d90f7-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="d90f7-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="d90f7-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="d90f7-108">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="d90f7-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="d90f7-109">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="d90f7-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="d90f7-110">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="d90f7-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="d90f7-111">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="d90f7-112">Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d90f7-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="d90f7-113">Configurer un équilibrage de charge accessible sur Internet pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="d90f7-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="d90f7-114">Dans l’ordre tooload équilibrer le trafic réseau à partir de hello Internet entre les machines virtuelles de hello d’un service cloud, vous devez créer un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="d90f7-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="d90f7-115">Cette procédure suppose que vous avez déjà créé des machines virtuelles de hello et qu’ils sont tous dans hello même service cloud.</span><span class="sxs-lookup"><span data-stu-id="d90f7-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="d90f7-116">**tooconfigure un jeu d’équilibrage de la charge pour les machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="d90f7-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="d90f7-117">Bonjour portail Azure classic, cliquez sur **virtuels**, puis cliquez sur nom hello d’un ordinateur virtuel dans le jeu d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="d90f7-118">Cliquez sur **Points de terminaison**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d90f7-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="d90f7-119">Sur hello **ajouter un ordinateur virtuel de tooa point de terminaison** , cliquez sur la flèche vers la droite hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="d90f7-120">Sur hello **spécifier les détails de hello du point de terminaison hello** page :</span><span class="sxs-lookup"><span data-stu-id="d90f7-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="d90f7-121">Dans **nom**, tapez un nom pour le point de terminaison hello ou sélectionnez nom de hello dans la liste hello des points de terminaison prédéfinis pour les protocoles communs.</span><span class="sxs-lookup"><span data-stu-id="d90f7-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="d90f7-122">Dans **protocole**, sélectionnez le protocole hello requis par type hello du point de terminaison, TCP ou UDP, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="d90f7-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="d90f7-123">Dans **les ports Public et privé**, tapez les numéros de port hello souhaité hello toouse de machine virtuelle, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="d90f7-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="d90f7-124">Vous pouvez utiliser un port privé hello et les règles de pare-feu sur le trafic tooredirect de machine virtuelle hello d’une manière qui convient à votre application.</span><span class="sxs-lookup"><span data-stu-id="d90f7-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="d90f7-125">un port privé Hello peut être hello identique au port public de hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="d90f7-126">Par exemple, pour un point de terminaison pour le trafic web (HTTP), vous pouvez affecter 80 tooboth hello publiques et privées voies.</span><span class="sxs-lookup"><span data-stu-id="d90f7-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="d90f7-127">Sélectionnez **créer un jeu d’équilibrage de la charge**, puis cliquez sur la flèche vers la droite hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="d90f7-128">Sur hello **configurer le jeu d’équilibrage de charge hello** page, tapez un nom pour le jeu d’équilibrage de charge hello, puis assigner des valeurs hello pour le comportement de sonde de hello équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="d90f7-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="d90f7-129">Hello équilibreur de charge utilise des sondes toodetermine si virtuels hello dans le jeu d’équilibrage de charge hello sont tooreceive disponibles du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d90f7-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="d90f7-130">Cliquez sur hello coche toocreate hello équilibrée point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d90f7-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="d90f7-131">Vous verrez **Oui** Bonjour **nom de jeu d’équilibrage de charge** colonne Hello **points de terminaison** page pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="d90f7-132">Dans le portail de hello, cliquez sur **virtuels**, cliquez sur le nom hello d’un ordinateur virtuel supplémentaire dans le jeu d’équilibrage de charge hello **points de terminaison**, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d90f7-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="d90f7-133">Sur hello **ajouter un ordinateur virtuel de tooa point de terminaison** , cliquez sur **ajouter le jeu d’équilibrage de charge existant point de terminaison tooan**, sélectionnez nom hello du jeu d’équilibrage de charge hello, puis cliquez sur la flèche vers la droite hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="d90f7-134">Sur hello **spécifier les détails de hello du point de terminaison hello** page, tapez un nom pour le point de terminaison hello, puis cliquez sur la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="d90f7-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="d90f7-135">Pour hello autres machines virtuelles dans le jeu d’équilibrage de charge hello, répétez les étapes 8 à 10.</span><span class="sxs-lookup"><span data-stu-id="d90f7-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d90f7-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d90f7-136">Next steps</span></span>

[<span data-ttu-id="d90f7-137">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="d90f7-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d90f7-138">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d90f7-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d90f7-139">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d90f7-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
