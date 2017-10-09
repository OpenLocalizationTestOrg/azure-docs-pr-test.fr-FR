---
title: "aaaSet d’un coffre pour tooAzure de réplication (sans System Center VMM) d’Hyper-V à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset d’un coffre pour tooAzure de réplication Hyper-V à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="b594a-103">Étape 7 : configurer un coffre pour la réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b594a-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="b594a-104">Cet article décrit comment configurer un coffre tooset et spécifier ce que vous souhaitez tooreplicate à partir de votre emplacement local, tooAzure à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b594a-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="b594a-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b594a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b594a-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b594a-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="b594a-107">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="b594a-107">Select a protection goal</span></span>

<span data-ttu-id="b594a-108">Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="b594a-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="b594a-109">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="b594a-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="b594a-110">Bonjour ressource Menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **objectif de Protection**.</span><span class="sxs-lookup"><span data-stu-id="b594a-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="b594a-111">Dans **objectif de Protection**, sélectionnez **tooAzure** > **Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b594a-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="b594a-112">Sélectionnez **non** tooconfirm vous n’utilisez pas de VMM.</span><span class="sxs-lookup"><span data-stu-id="b594a-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Sélectionner des objectifs](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="b594a-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b594a-114">Next steps</span></span>

<span data-ttu-id="b594a-115">Accédez trop[étape 8 : configurer la source et cible](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="b594a-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
