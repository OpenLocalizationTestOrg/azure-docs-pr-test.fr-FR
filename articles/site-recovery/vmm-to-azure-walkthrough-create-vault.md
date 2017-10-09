---
title: "aaaSet d’un coffre pour tooAzure de réplication (avec System Center VMM) d’Hyper-V à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset d’un coffre pour tooAzure de réplication (avec VMM) d’Hyper-V à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="e30fc-103">Étape 7 : configurer un coffre pour la réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e30fc-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="e30fc-104">Cet article décrit comment configurer un coffre tooset et spécifier ce que vous souhaitez tooreplicate à partir de votre emplacement local, tooAzure à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e30fc-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="e30fc-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e30fc-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e30fc-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="e30fc-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="e30fc-107">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="e30fc-107">Select a protection goal</span></span>

<span data-ttu-id="e30fc-108">Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="e30fc-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="e30fc-109">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="e30fc-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="e30fc-110">Bonjour ressource Menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **objectif de Protection**.</span><span class="sxs-lookup"><span data-stu-id="e30fc-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="e30fc-111">Dans **objectif de Protection**, sélectionnez **tooAzure** > **Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="e30fc-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="e30fc-112">Sélectionnez **Oui** tooconfirm vous n VMM.</span><span class="sxs-lookup"><span data-stu-id="e30fc-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![Sélectionner des objectifs](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="e30fc-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e30fc-114">Next steps</span></span>

<span data-ttu-id="e30fc-115">Accédez trop[étape 8 : configurer la source et cible](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="e30fc-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
