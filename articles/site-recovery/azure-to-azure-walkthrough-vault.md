---
title: "aaaSet d’un coffre pour Azure VM repliction entre les régions avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello nécessaire tooset d’un coffre pour la réplication Azure entre les régions Azure à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="92fb3-103">Étape 4 : Configurer un coffre pour la réplication tooAzure Azure</span><span class="sxs-lookup"><span data-stu-id="92fb3-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="92fb3-104">Après avoir [planification de réseaux](azure-to-azure-walkthrough-network.md), utilisez cette tooset article d’un coffre, pour les machines virtuelles (VM) Azure réplication tooanother région Azure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="92fb3-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="92fb3-105">Lorsque vous avez terminé l’article de hello, vous devez disposer d’un coffre Recovery Services configuré.</span><span class="sxs-lookup"><span data-stu-id="92fb3-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="92fb3-106">Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="92fb3-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="92fb3-107">La réplication de machines virtuelles Azure est actuellement disponible en préversion.</span><span class="sxs-lookup"><span data-stu-id="92fb3-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="92fb3-108">création d'un coffre</span><span class="sxs-lookup"><span data-stu-id="92fb3-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="92fb3-109">Nous vous recommandons de créer le coffre Recovery Services hello dans hello emplacement où votre tooreplicate de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="92fb3-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="92fb3-110">Par exemple, si votre emplacement cible est hello central US, créer dans le coffre hello **du centre des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="92fb3-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="92fb3-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92fb3-111">Next steps</span></span>

<span data-ttu-id="92fb3-112">Accédez trop[étape 5 : activer la réplication](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="92fb3-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
