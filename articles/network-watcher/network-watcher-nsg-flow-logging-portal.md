---
title: "journaux de flux aaaManage réseau sécurité groupe avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux toomanage flux du groupe de sécurité réseau dans l’Observateur réseau de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="0d5c1-103">Gérer les journaux de flux de groupe de sécurité réseau Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0d5c1-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0d5c1-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0d5c1-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="0d5c1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d5c1-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="0d5c1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0d5c1-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="0d5c1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d5c1-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="0d5c1-108">API REST</span><span class="sxs-lookup"><span data-stu-id="0d5c1-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="0d5c1-109">Journaux de flux de groupe de sécurité réseau sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="0d5c1-110">Ces journaux de flux, écrits au format JSON, fournissent des informations importantes, notamment :</span><span class="sxs-lookup"><span data-stu-id="0d5c1-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="0d5c1-111">les flux entrants et sortants, règle par règle ;</span><span class="sxs-lookup"><span data-stu-id="0d5c1-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="0d5c1-112">Hello NIC hello flux s’applique à.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="0d5c1-113">5-tuple plus d’informations sur le flux hello (source/destination IP, port source ou de destination, protocole).</span><span class="sxs-lookup"><span data-stu-id="0d5c1-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="0d5c1-114">des informations indiquant si le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0d5c1-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0d5c1-115">Before you begin</span></span>

<span data-ttu-id="0d5c1-116">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer une instance de l’Observateur réseau](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="0d5c1-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="0d5c1-117">scénario de Hello suppose également que vous disposez d’un groupe de ressources avec un ordinateur virtuel valide.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="0d5c1-118">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="0d5c1-118">Register Insights provider</span></span>

<span data-ttu-id="0d5c1-119">Pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="0d5c1-120">fournisseur de hello tooregister, hello prennent comme suit :</span><span class="sxs-lookup"><span data-stu-id="0d5c1-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="0d5c1-121">Accédez trop**abonnements**, puis sélectionnez abonnement hello pour lequel vous souhaitez tooenable flux journaux.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="0d5c1-122">Sur hello **abonnement** panneau, sélectionnez **fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="0d5c1-123">Examinez la liste hello des fournisseurs et vérifiez que hello **microsoft.insights** fournisseur est inscrit.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="0d5c1-124">Sinon, sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-124">If not, then select **Register**.</span></span>

![Afficher les fournisseurs][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="0d5c1-126">Activer les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="0d5c1-126">Enable flow logs</span></span>

<span data-ttu-id="0d5c1-127">Ces étapes vous guident tout au long des processus de hello d’activation des journaux de flux sur un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="0d5c1-128">Étape 1</span><span class="sxs-lookup"><span data-stu-id="0d5c1-128">Step 1</span></span>

<span data-ttu-id="0d5c1-129">Passez l’instance de l’Observateur réseau tooa, puis sélectionnez **de flux de groupe de sécurité réseau consigne**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Vue d’ensemble des journaux de flux][1]

### <a name="step-2"></a><span data-ttu-id="0d5c1-131">Étape 2</span><span class="sxs-lookup"><span data-stu-id="0d5c1-131">Step 2</span></span>

<span data-ttu-id="0d5c1-132">Sélectionnez un groupe de sécurité réseau à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-132">Select a network security group from hello list.</span></span>

![Vue d’ensemble des journaux de flux][2]

### <a name="step-3"></a><span data-ttu-id="0d5c1-134">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="0d5c1-134">Step 3</span></span> 

<span data-ttu-id="0d5c1-135">Sur hello **paramètres des journaux de flux** panneau, définir le statut de hello trop**sur**, puis configurez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="0d5c1-136">Quand vous avez terminé, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-136">When you're done, select **OK**.</span></span> <span data-ttu-id="0d5c1-137">Ensuite, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-137">Then select **Save**.</span></span>

![Vue d’ensemble des journaux de flux][3]

## <a name="download-flow-logs"></a><span data-ttu-id="0d5c1-139">Télécharger des journaux de flux</span><span class="sxs-lookup"><span data-stu-id="0d5c1-139">Download flow logs</span></span>

<span data-ttu-id="0d5c1-140">Les journaux des flux sont enregistrés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="0d5c1-141">Télécharger votre tooview de journaux flux les.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="0d5c1-142">Étape 1</span><span class="sxs-lookup"><span data-stu-id="0d5c1-142">Step 1</span></span>

<span data-ttu-id="0d5c1-143">journaux de flux toodownload, sélectionnez **vous pouvez télécharger les journaux de flux à partir de comptes de stockage configuré**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="0d5c1-144">Cette étape vous amène la vue de compte de stockage tooa où vous pouvez choisir quels toodownload journaux.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Paramètres des journaux de flux][4]

### <a name="step-2"></a><span data-ttu-id="0d5c1-146">Étape 2</span><span class="sxs-lookup"><span data-stu-id="0d5c1-146">Step 2</span></span>

<span data-ttu-id="0d5c1-147">Atteindre le compte de stockage correct toohello.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-147">Go toohello correct storage account.</span></span> <span data-ttu-id="0d5c1-148">Ensuite, sélectionnez **Conteneurs** > **insights-journal-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Paramètres des journaux de flux][5]

### <a name="step-3"></a><span data-ttu-id="0d5c1-150">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="0d5c1-150">Step 3</span></span>

<span data-ttu-id="0d5c1-151">Atteindre l’emplacement de toohello du journal de flux de hello, sélectionnez-le, puis sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0d5c1-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Paramètres des journaux de flux][6]

<span data-ttu-id="0d5c1-153">Pour plus d’informations sur la structure hello du journal de hello, visitez [vue d’ensemble du journal de flux groupe réseau sécurité](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d5c1-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d5c1-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d5c1-154">Next steps</span></span>

<span data-ttu-id="0d5c1-155">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0d5c1-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
