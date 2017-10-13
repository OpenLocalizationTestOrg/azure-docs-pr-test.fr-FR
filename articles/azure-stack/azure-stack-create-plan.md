---
title: "Créer un plan dans Azure Stack | Microsoft Docs"
description: "En tant qu’administrateur cloud, créez un plan permettant aux abonnés d’approvisionner des machines virtuelles."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 30759dca746fd7fd02653556cb105f419f5bf854
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="a38e4-103">Créer un plan dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a38e4-103">Create a plan in Azure Stack</span></span>

<span data-ttu-id="a38e4-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="a38e4-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="a38e4-105">Les [plans](azure-stack-key-features.md) regroupent un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="a38e4-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="a38e4-106">En tant que fournisseur, vous pouvez créer des plans à proposer à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a38e4-106">As a provider, you can create plans to offer to your users.</span></span> <span data-ttu-id="a38e4-107">En retour, ceux-ci s’abonnent à vos offres pour utiliser les plans et les services qu’elles comprennent.</span><span class="sxs-lookup"><span data-stu-id="a38e4-107">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="a38e4-108">Cet exemple montre comment créer un plan comprenant les fournisseurs de ressources de stockage, réseau et de calcul.</span><span class="sxs-lookup"><span data-stu-id="a38e4-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="a38e4-109">Ce plan donne aux abonnés la possibilité d’approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a38e4-109">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="a38e4-110">Connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="a38e4-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="a38e4-111">Entrez les informations d’identification du compte que vous avez créé à l’étape 5 de la section [Exécuter le script PowerShell](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="a38e4-111">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="a38e4-112">Pour créer un plan et une offre auxquels les utilisateurs peuvent s’abonner, cliquez sur **Nouveau** > **Plans + offres clients** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="a38e4-112">To create a plan and offer that users can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="a38e4-113">Sur le panneau **Nouveau plan**, renseignez le **Nom d’affichage** et le **Nom de la ressource**.</span><span class="sxs-lookup"><span data-stu-id="a38e4-113">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="a38e4-114">Le nom d’affichage correspond au nom convivial du plan, que les locataires voient.</span><span class="sxs-lookup"><span data-stu-id="a38e4-114">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="a38e4-115">Seul l’administrateur peut voir le nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="a38e4-115">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="a38e4-116">Il s’agit du nom que les administrateurs utilisent pour gérer le plan en tant que ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a38e4-116">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="a38e4-117">Créez un **Groupe de ressources** ou sélectionnez-en un qui servira de conteneur pour le plan.</span><span class="sxs-lookup"><span data-stu-id="a38e4-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="a38e4-118">Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a38e4-118">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="a38e4-119">Cliquez sur **Quotas** et sur **Microsoft.Storage (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour personnaliser le quota.</span><span class="sxs-lookup"><span data-stu-id="a38e4-119">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="a38e4-120">Si vous créez un quota, entrez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="a38e4-120">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="a38e4-121">Cliquez sur **Microsoft.Network (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="a38e4-121">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="a38e4-122">Si vous créez un quota, tapez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="a38e4-122">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="a38e4-123">Cliquez sur **Microsoft.Compute (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="a38e4-123">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="a38e4-124">Si vous créez un quota, tapez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="a38e4-124">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="a38e4-125">Sur le panneau **Quotas**, cliquez sur **OK**, puis, sur le panneau **Nouveau plan**, cliquez sur **Créer** pour créer le plan.</span><span class="sxs-lookup"><span data-stu-id="a38e4-125">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="a38e4-126">Pour voir votre nouveau plan, cliquez sur **Toutes les ressources**, puis recherchez-le et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="a38e4-126">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="a38e4-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a38e4-127">Next steps</span></span>
[<span data-ttu-id="a38e4-128">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="a38e4-128">Create an offer</span></span>](azure-stack-create-offer.md)
