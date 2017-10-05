---
title: "Gérer les journaux de flux des groupes de sécurité réseau avec Azure Network Watcher | Microsoft Docs"
description: "Cette page explique comment gérer les journaux des flux de groupe de sécurité réseau dans Azure Network Watcher"
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="1bdb1-103">Gérer les journaux de flux des groupes de sécurité réseau sur le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1bdb1-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1bdb1-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1bdb1-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="1bdb1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bdb1-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="1bdb1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bdb1-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="1bdb1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bdb1-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="1bdb1-108">API REST</span><span class="sxs-lookup"><span data-stu-id="1bdb1-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="1bdb1-109">Les journaux de flux des groupes de sécurité réseau correspondent à une fonctionnalité de Network Watcher qui permet de visualiser des informations sur le trafic IP d’entrée et de sortie par le biais d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="1bdb1-110">Ces journaux de flux, écrits au format JSON, fournissent des informations importantes, notamment :</span><span class="sxs-lookup"><span data-stu-id="1bdb1-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="1bdb1-111">les flux entrants et sortants, règle par règle ;</span><span class="sxs-lookup"><span data-stu-id="1bdb1-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="1bdb1-112">la carte réseau à laquelle s’applique le flux ;</span><span class="sxs-lookup"><span data-stu-id="1bdb1-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="1bdb1-113">cinq informations sur le flux (adresse IP source ou de destination, port source ou de destination, protocole) ;</span><span class="sxs-lookup"><span data-stu-id="1bdb1-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="1bdb1-114">des informations indiquant si le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1bdb1-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1bdb1-115">Before you begin</span></span>

<span data-ttu-id="1bdb1-116">Ce scénario suppose que vous ayez déjà suivi la procédure décrite sur la page [Créer une instance de Network Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="1bdb1-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="1bdb1-117">Il part également du principe que vous disposez d’un groupe de ressources et d’une machine virtuelle valide.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="1bdb1-118">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="1bdb1-118">Register Insights provider</span></span>

<span data-ttu-id="1bdb1-119">Pour que la journalisation du flux fonctionne correctement, le fournisseur **Microsoft.Insights** doit être inscrit.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="1bdb1-120">Pour inscrire le fournisseur, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1bdb1-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="1bdb1-121">Accédez à **Abonnements**, puis sélectionnez l’abonnement pour lequel vous souhaitez activer les journaux de flux.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="1bdb1-122">Sur le panneau **Abonnement**, sélectionnez **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="1bdb1-123">Étudiez la liste des fournisseurs et vérifiez que le fournisseur **microsoft.insights** est inscrit.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="1bdb1-124">Sinon, sélectionnez **Inscrire**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-124">If not, then select **Register**.</span></span>

![Afficher les fournisseurs][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="1bdb1-126">Activer les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="1bdb1-126">Enable flow logs</span></span>

<span data-ttu-id="1bdb1-127">Ces étapes vous guident tout au long du processus d’activation des journaux de flux sur un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="1bdb1-128">Étape 1</span><span class="sxs-lookup"><span data-stu-id="1bdb1-128">Step 1</span></span>

<span data-ttu-id="1bdb1-129">Accédez à une instance de Network Watcher, puis sélectionnez **Journaux de flux des NSG**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Vue d’ensemble des journaux de flux][1]

### <a name="step-2"></a><span data-ttu-id="1bdb1-131">Étape 2</span><span class="sxs-lookup"><span data-stu-id="1bdb1-131">Step 2</span></span>

<span data-ttu-id="1bdb1-132">Sélectionnez un groupe de sécurité réseau dans la liste.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-132">Select a network security group from the list.</span></span>

![Vue d’ensemble des journaux de flux][2]

### <a name="step-3"></a><span data-ttu-id="1bdb1-134">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="1bdb1-134">Step 3</span></span> 

<span data-ttu-id="1bdb1-135">Dans le panneau **Paramètres des journaux de flux**, réglez l’état sur **Activé**, puis configurez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="1bdb1-136">Quand vous avez terminé, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-136">When you're done, select **OK**.</span></span> <span data-ttu-id="1bdb1-137">Ensuite, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-137">Then select **Save**.</span></span>

![Vue d’ensemble des journaux de flux][3]

## <a name="download-flow-logs"></a><span data-ttu-id="1bdb1-139">Télécharger des journaux de flux</span><span class="sxs-lookup"><span data-stu-id="1bdb1-139">Download flow logs</span></span>

<span data-ttu-id="1bdb1-140">Les journaux des flux sont enregistrés dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="1bdb1-141">Téléchargez vos journaux de flux pour les afficher.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="1bdb1-142">Étape 1</span><span class="sxs-lookup"><span data-stu-id="1bdb1-142">Step 1</span></span>

<span data-ttu-id="1bdb1-143">Pour télécharger des journaux de flux, sélectionnez **Vous pouvez télécharger les journaux de flux à partir de comptes de stockage configurés**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="1bdb1-144">Cette étape vous amène sur une vue du compte de stockage qui vous permet de choisir les journaux à télécharger.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Paramètres des journaux de flux][4]

### <a name="step-2"></a><span data-ttu-id="1bdb1-146">Étape 2</span><span class="sxs-lookup"><span data-stu-id="1bdb1-146">Step 2</span></span>

<span data-ttu-id="1bdb1-147">Accédez au compte de stockage approprié.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-147">Go to the correct storage account.</span></span> <span data-ttu-id="1bdb1-148">Ensuite, sélectionnez **Conteneurs** > **insights-journal-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Paramètres des journaux de flux][5]

### <a name="step-3"></a><span data-ttu-id="1bdb1-150">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="1bdb1-150">Step 3</span></span>

<span data-ttu-id="1bdb1-151">Accédez à l’emplacement du journal de flux, sélectionnez-le, puis sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="1bdb1-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Paramètres des journaux de flux][6]

<span data-ttu-id="1bdb1-153">Pour plus d’informations sur la structure du journal, consultez la page [Vue d’ensemble des journaux de flux des groupes de sécurité réseau](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1bdb1-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bdb1-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bdb1-154">Next steps</span></span>

<span data-ttu-id="1bdb1-155">Découvrez comment [visualiser vos journaux de flux des NSG avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="1bdb1-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
