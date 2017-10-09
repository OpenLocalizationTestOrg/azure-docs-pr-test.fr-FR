---
title: aaaCreate des batteries de serveurs SharePoint dans Azure | Documents Microsoft
description: "Créez rapidement une nouvelle batterie de serveurs SharePoint 2013 ou SharePoint 2016 dans Azure à l’aide de hello Azure marketplace de portail."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="c3027-103">Créer des batteries de serveurs SharePoint à l’aide de hello Azure marketplace de portail</span><span class="sxs-lookup"><span data-stu-id="c3027-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="c3027-104">Batteries de serveurs SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="c3027-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="c3027-105">Marketplace de portail Microsoft Azure hello, vous pouvez créer rapidement des batteries de serveurs SharePoint Server 2013 préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="c3027-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="c3027-106">Cela peut vous faire gagner un temps précieux lorsque vous avez besoin d'une batterie de serveurs SharePoint de base ou à haute disponibilité pour un environnement de test/développement ou si vous envisagez l'adoption de SharePoint Server 2013 comme solution de collaboration pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="c3027-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="c3027-107">Hello **batterie de serveurs SharePoint** élément Bonjour Azure Marketplace de hello portail Azure a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="c3027-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="c3027-108">Elle a été remplacée par hello **batterie SharePoint 2013 non - HA** et **batterie de serveurs SharePoint 2013 à haute disponibilité** éléments.</span><span class="sxs-lookup"><span data-stu-id="c3027-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="c3027-109">batterie de serveurs SharePoint base Hello se compose de trois machines virtuelles dans cette configuration.</span><span class="sxs-lookup"><span data-stu-id="c3027-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="c3027-111">Vous pouvez utiliser cette configuration de batterie comme configuration simplifiée pour le développement d'applications SharePoint ou pour votre évaluation initiale de SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="c3027-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="c3027-112">toocreate hello base (trois serveurs) batterie de serveurs SharePoint :</span><span class="sxs-lookup"><span data-stu-id="c3027-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="c3027-113">Cliquez [ici](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="c3027-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="c3027-114">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="c3027-115">Sur hello **batterie SharePoint 2013 non - HA** volet, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="c3027-116">Spécifiez des paramètres sur les étapes de hello Hello **créer batterie SharePoint 2013 non - HA** volet, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="c3027-117">batterie de serveurs SharePoint de haute disponibilité Hello se compose de neuf machines virtuelles dans cette configuration.</span><span class="sxs-lookup"><span data-stu-id="c3027-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="c3027-119">Vous pouvez utiliser cette charges client plus élevées de batterie de serveurs configuration tootest, la haute disponibilité d’un site SharePoint externe hello et groupes de disponibilité AlwaysOn de SQL Server pour une batterie de serveurs SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c3027-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="c3027-120">Vous pouvez également l'utiliser pour le développement d'applications SharePoint dans un environnement à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c3027-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="c3027-121">toocreate hello haute disponibilité (serveur neuf) batterie de serveurs SharePoint :</span><span class="sxs-lookup"><span data-stu-id="c3027-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="c3027-122">Cliquez [ici](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="c3027-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="c3027-123">Cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="c3027-124">Sur hello **batterie de serveurs SharePoint 2013 à haute disponibilité** volet, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="c3027-125">Spécifiez des paramètres sur les étapes de hello sept Hello **créer 2013 à haute disponibilité batterie de serveurs SharePoint** volet, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c3027-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="c3027-126">Vous ne pouvez pas créer de hello **batterie SharePoint 2013 non - HA** ou **batterie de serveurs SharePoint 2013 à haute disponibilité** avec une version d’évaluation gratuite de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3027-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="c3027-127">Hello portail Azure crée deux de ces batteries de serveurs dans un réseau virtuel cloud uniquement avec une présence sur le web sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c3027-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="c3027-128">Aucun site-à-site VPN ou ExpressRoute connexion tooyour arrière organisation réseau est.</span><span class="sxs-lookup"><span data-stu-id="c3027-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="c3027-129">Lorsque vous créez hello base ou les batteries SharePoint haute disponibilité à l’aide de hello portail Azure, vous ne pouvez pas spécifier un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="c3027-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="c3027-130">toowork contourner cette limitation, créez ces batteries de serveurs avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3027-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="c3027-131">Pour plus d’informations, consultez la page [Créer des batteries de serveurs de développement/test SharePoint 2013 avec le portail Azure](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="c3027-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="c3027-132">Batteries de serveurs SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="c3027-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="c3027-133">Consultez [cet article](https://technet.microsoft.com/library/mt723354.aspx) pour hello de toobuild instructions hello suivant monoserveur SharePoint Server 2016 de batterie de serveurs.</span><span class="sxs-lookup"><span data-stu-id="c3027-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="c3027-135">La gestion des batteries de serveurs SharePoint hello</span><span class="sxs-lookup"><span data-stu-id="c3027-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="c3027-136">Vous pouvez administrer des serveurs de hello de ces batteries de serveurs via des connexions Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="c3027-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="c3027-137">Pour plus d’informations, consultez [ouvrir une session sur l’ordinateur virtuel de toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="c3027-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="c3027-138">À partir du site Central Administration SharePoint de hello, vous pouvez configurer mes sites, les applications SharePoint et autres fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="c3027-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="c3027-139">Pour plus d'informations, consultez la page sur la [configuration de SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3027-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3027-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3027-140">Next steps</span></span>
* <span data-ttu-id="c3027-141">Découvrez d’autres [configurations de SharePoint](https://technet.microsoft.com/library/dn635309.aspx) dans les services d’infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="c3027-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
