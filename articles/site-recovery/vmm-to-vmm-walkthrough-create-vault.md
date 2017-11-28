---
title: "aaaCreate un coffre pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment toocreate un coffre lors de la réplication des ordinateurs virtuels Hyper-V tooa System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="f78a0-103">Étape 5 : Créer un coffre pour le site secondaire de tooa de réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f78a0-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="f78a0-104">Après avoir préparé local [les serveurs System Center Virtual Machine Manager (VMM) et les hôtes/clusters Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) pour Hyper-V réplication tooa site secondaire à l’aide [Azure Site Recovery](site-recovery-overview.md), vous pouvez créer un Scénario de réplication Sélectionnez hello et coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f78a0-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="f78a0-105">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f78a0-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f78a0-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="f78a0-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="f78a0-107">Choisir un objectif en matière de protection</span><span class="sxs-lookup"><span data-stu-id="f78a0-107">Choose a protection goal</span></span>

<span data-ttu-id="f78a0-108">Sélectionnez ce que vous souhaitez tooreplicate, et où tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="f78a0-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="f78a0-109">Cliquez sur **Site Recovery** > **Étape 1 : Préparez l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="f78a0-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="f78a0-110">Sélectionnez **toorecovery site**, puis sélectionnez **Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="f78a0-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="f78a0-111">Sélectionnez **Oui** tooindicate que vous utilisez des hôtes VMM toomanage hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f78a0-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="f78a0-112">Sélectionnez **Oui** si vous avez un serveur VMM secondaire.</span><span class="sxs-lookup"><span data-stu-id="f78a0-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="f78a0-113">Si vous déployez la réplication entre des clouds sur un seul serveur VMM, cliquez sur **Non**.</span><span class="sxs-lookup"><span data-stu-id="f78a0-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="f78a0-114">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f78a0-114">Then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="f78a0-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f78a0-116">Next steps</span></span>

<span data-ttu-id="f78a0-117">Accédez trop[étape 6 : configurer la source de réplication hello et cible](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="f78a0-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
