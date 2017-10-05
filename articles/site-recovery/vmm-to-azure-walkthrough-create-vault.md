---
title: "Configurer un coffre pour la réplication Hyper-V (avec System Center VMM) vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes requises pour configurer un coffre pour la réplication Hyper-V (avec VMM) vers Azure à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: af453ec27ba15ad8c59cf9f544584ad18dc0f74a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="3b073-103">Étape 7 : configurer un coffre pour la réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="3b073-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="3b073-104">Cet article explique comment configurer un coffre, et spécifier ce que vous souhaitez répliquer à partir de l’emplacement local, sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3b073-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="3b073-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3b073-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3b073-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="3b073-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="3b073-107">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="3b073-107">Select a protection goal</span></span>

<span data-ttu-id="3b073-108">Sélectionnez les éléments à répliquer et l’emplacement de la réplication.</span><span class="sxs-lookup"><span data-stu-id="3b073-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="3b073-109">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="3b073-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="3b073-110">Dans le menu Ressource, cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="3b073-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="3b073-111">Dans **Objectif de protection**, sélectionnez **To Azure (Vers Azure)** > **, puis Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="3b073-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="3b073-112">Sélectionnez **Oui** pour confirmer que vous utilisez VMM.</span><span class="sxs-lookup"><span data-stu-id="3b073-112">Select **Yes** to confirm you're nusing VMM.</span></span> 

     ![Sélectionner des objectifs](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="3b073-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b073-114">Next steps</span></span>

<span data-ttu-id="3b073-115">Aller à l’[Étape 8 : configurer la source et la cible](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="3b073-115">Go to [Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
