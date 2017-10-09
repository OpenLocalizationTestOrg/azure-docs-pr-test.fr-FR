---
title: "aaaCreate un équilibreur de charge interne - portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge dans le Gestionnaire de ressources à l’aide de hello portail Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="0e840-103">Créer un équilibreur de charge interne Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e840-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e840-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e840-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="0e840-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e840-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="0e840-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="0e840-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="0e840-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="0e840-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0e840-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0e840-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0e840-109">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0e840-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="0e840-110">Prise en main de la création d’un équilibreur de charge interne avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e840-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="0e840-111">Utilisez hello suivant les étapes toocreate un équilibreur de charge interne dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0e840-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="0e840-112">Ouvrez un navigateur, accédez toohello [portail Azure](http://portal.azure.com)et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="0e840-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="0e840-113">Hello du côté supérieur gauche de l’écran hello, cliquez sur **nouveau** > **réseau** > **équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="0e840-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="0e840-114">Bonjour **équilibrage de charge créer** panneau, entrez un **nom** pour votre équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="0e840-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="0e840-115">Sous **Schéma**, cliquez sur **Interne**.</span><span class="sxs-lookup"><span data-stu-id="0e840-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="0e840-116">Cliquez sur **réseau virtuel**, et puis sélectionnez hello réseau virtuel où vous souhaitez l’équilibrage de charge toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0e840-117">Si vous ne voyez pas le réseau virtuel de hello à toouse, vérifiez hello **emplacement** vous utilisez pour l’équilibrage de charge hello et modifiez-le en conséquence.</span><span class="sxs-lookup"><span data-stu-id="0e840-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="0e840-118">Cliquez sur **sous-réseau**, puis sélectionnez le sous-réseau hello où vous souhaitez l’équilibrage de charge toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="0e840-119">Sous **l’attribution d’adresses IP**, cliquez sur **dynamique** ou **statique**, selon que vous souhaitez adresse hello pour hello charge équilibrage toobe fixe (statique) ou non.</span><span class="sxs-lookup"><span data-stu-id="0e840-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0e840-120">Si vous sélectionnez toouse une adresse IP statique, vous devez tooprovide une adresse pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="0e840-121">Sous **groupe de ressources** spécifier nom hello d’un nouveau groupe de ressources pour l’équilibrage de charge hello, ou cliquez sur **sélectionnez existante** et sélectionnez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="0e840-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="0e840-122">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0e840-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="0e840-123">Configuration des règles d’équilibrage de la charge</span><span class="sxs-lookup"><span data-stu-id="0e840-123">Configure load balancing rules</span></span>

<span data-ttu-id="0e840-124">Après hello création de l’équilibrage de charge, accédez tooconfigure de ressource de programme d’équilibrage de charge toohello il.</span><span class="sxs-lookup"><span data-stu-id="0e840-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="0e840-125">Vous devez tooconfigure tout d’abord un pool d’adresses de serveur principal et d’une sonde avant de configurer une règle d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="0e840-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="0e840-126">Étape 1 : Configurer un pool principal</span><span class="sxs-lookup"><span data-stu-id="0e840-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="0e840-127">Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0e840-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="0e840-128">Bonjour **paramètres** panneau, cliquez sur **pools principaux**.</span><span class="sxs-lookup"><span data-stu-id="0e840-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="0e840-129">Bonjour **pools d’adresses principaux** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0e840-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="0e840-130">Bonjour **ajouter le pool principal** panneau, entrez un **nom** de pool hello du serveur principal, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e840-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="0e840-131">Étape 2 : Configurer une sonde</span><span class="sxs-lookup"><span data-stu-id="0e840-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="0e840-132">Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0e840-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="0e840-133">Bonjour **paramètres** panneau, cliquez sur **sondes**.</span><span class="sxs-lookup"><span data-stu-id="0e840-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="0e840-134">Bonjour **sondes** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0e840-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="0e840-135">Bonjour **ajouter sonde** panneau, entrez un **nom** pour la sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="0e840-136">Sous **Protocole**, sélectionnez **HTTP** (pour les sites web) ou **TCP** (pour les autres applications basées sur TCP).</span><span class="sxs-lookup"><span data-stu-id="0e840-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="0e840-137">Sous **Port**, spécifiez hello port toouse lors de l’accès de sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="0e840-138">Sous **chemin d’accès** (pour HTTP sondes uniquement), spécifiez toouse de chemin d’accès hello comme une sonde.</span><span class="sxs-lookup"><span data-stu-id="0e840-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="0e840-139">Sous **intervalle** spécifier la fréquence à laquelle tooprobe hello application.</span><span class="sxs-lookup"><span data-stu-id="0e840-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="0e840-140">Sous **seuil défaillance**, spécifiez le nombre de tentatives doivent échouer avant que la machine virtuelle de serveur principal hello est marqué comme étant défectueux.</span><span class="sxs-lookup"><span data-stu-id="0e840-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="0e840-141">Cliquez sur **OK** toocreate sonde.</span><span class="sxs-lookup"><span data-stu-id="0e840-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="0e840-142">Étape 3 : Configurer les règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="0e840-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="0e840-143">Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0e840-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="0e840-144">Bonjour **paramètres** panneau, cliquez sur **règles d’équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="0e840-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="0e840-145">Bonjour **règles d’équilibrage de charge** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0e840-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="0e840-146">Bonjour **règle d’équilibrage ajouter** panneau, entrez un **nom** pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="0e840-147">Sous **Protocole**, sélectionnez **HTTP** (pour les sites web) ou **TCP** (pour les autres applications basées sur TCP).</span><span class="sxs-lookup"><span data-stu-id="0e840-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="0e840-148">Sous **Port**, spécifiez les clients du port hello connectent à équilibrage de charge tooin hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="0e840-149">Sous **port principal**, spécifiez hello port toobe est utilisé dans le pool principal hello (en règle générale, port d’équilibrage de charge hello et port du serveur principal hello sont hello même).</span><span class="sxs-lookup"><span data-stu-id="0e840-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="0e840-150">Sous **pool principal**, sélectionnez hello principal pool que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0e840-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="0e840-151">Sous **persistance de Session**, sélectionnez la façon dont vous souhaitez que les sessions toopersist.</span><span class="sxs-lookup"><span data-stu-id="0e840-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="0e840-152">Sous **délai d’inactivité (minutes)**, spécifiez le délai d’inactivité de hello.</span><span class="sxs-lookup"><span data-stu-id="0e840-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="0e840-153">Sous **Adresse IP flottante (retour serveur direct)**, cliquez sur **Désactivé** ou **Activé**.</span><span class="sxs-lookup"><span data-stu-id="0e840-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="0e840-154">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e840-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e840-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e840-155">Next steps</span></span>

[<span data-ttu-id="0e840-156">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="0e840-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0e840-157">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="0e840-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

