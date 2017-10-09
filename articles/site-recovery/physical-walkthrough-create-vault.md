---
title: "aaaSet d’un coffre pour tooAzure de réplication de serveur physique à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello tooset d’un tooAzure de serveurs physiques tooreplicate coffre à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="c225d-103">Étape 6 : Configurer un coffre pour tooAzure de réplication de serveur physique</span><span class="sxs-lookup"><span data-stu-id="c225d-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="c225d-104">Cet article décrit comment tooset d’un coffre.</span><span class="sxs-lookup"><span data-stu-id="c225d-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="c225d-105">Vous créez le coffre hello et spécifier ce que vous souhaitez tooreplicate à partir de votre tooAzure emplacement local, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c225d-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="c225d-106">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c225d-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="c225d-107">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="c225d-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="c225d-108">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="c225d-108">Select a protection goal</span></span>

<span data-ttu-id="c225d-109">Sélectionnez les éléments tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="c225d-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="c225d-110">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="c225d-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="c225d-111">Bonjour ressource Menu, cliquez sur **Site Recovery** > **préparer l’Infrastructure** > **objectif de Protection**.</span><span class="sxs-lookup"><span data-stu-id="c225d-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="c225d-112">Dans **objectif de Protection**, sélectionnez **tooAzure** > **non virtualisé,**.</span><span class="sxs-lookup"><span data-stu-id="c225d-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c225d-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c225d-113">Next steps</span></span>

<span data-ttu-id="c225d-114">Accédez trop[étape 7 : configurer la source et cible](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="c225d-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
