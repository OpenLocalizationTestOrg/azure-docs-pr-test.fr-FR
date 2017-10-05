---
title: "Configurer un coffre pour la réplication Hyper-V (sans System Center VMM) vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes requises pour configurer un coffre pour la réplication Hyper-V sur Azure à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="b2af2-103">Étape 7 : configurer un coffre pour la réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b2af2-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="b2af2-104">Cet article explique comment configurer un coffre, et spécifier ce que vous souhaitez répliquer à partir de l’emplacement local, sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b2af2-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="b2af2-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b2af2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b2af2-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b2af2-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="b2af2-107">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="b2af2-107">Select a protection goal</span></span>

<span data-ttu-id="b2af2-108">Sélectionnez les éléments à répliquer et l’emplacement de la réplication.</span><span class="sxs-lookup"><span data-stu-id="b2af2-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="b2af2-109">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="b2af2-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="b2af2-110">Dans le menu Ressource, cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="b2af2-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="b2af2-111">Dans **Objectif de protection**, sélectionnez **To Azure (Vers Azure)** > **, puis Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b2af2-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="b2af2-112">Sélectionnez **Non** pour confirmer que vous n’utilisez pas VMM.</span><span class="sxs-lookup"><span data-stu-id="b2af2-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![Sélectionner des objectifs](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="b2af2-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2af2-114">Next steps</span></span>

<span data-ttu-id="b2af2-115">Aller à l’[Étape 8 : configurer la source et la cible](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="b2af2-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
