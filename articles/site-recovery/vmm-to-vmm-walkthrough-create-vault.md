---
title: "Création d’un coffre pour la réplication Hyper-V sur un site secondaire avec Azure Site Recovery | Microsoft Docs"
description: "Décrit comment créer un coffre lors de la réplication de machines virtuelles Hyper-V sur un site secondaire System Center VMM avec Azure Site Recovery."
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
ms.openlocfilehash: 28cfcf12b2e369f96664c163c0b6f2aa8a6ddcb9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="2d686-103">Étape 5 : Créer un coffre pour la réplication Hyper-V sur un site secondaire</span><span class="sxs-lookup"><span data-stu-id="2d686-103">Step 5: Create a vault for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="2d686-104">Après avoir préparé [les serveurs System Center Virtual Machine Manager (VMM) et les hôtes/clusters Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) locaux pour la réplication Hyper-V sur un site secondaire à l’aide [d’Azure Site Recovery](site-recovery-overview.md), vous pouvez créer un coffre Recovery Services et sélectionner le scénario de réplication.</span><span class="sxs-lookup"><span data-stu-id="2d686-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication to a secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select the replication scenario.</span></span>

<span data-ttu-id="2d686-105">Après avoir lu cet article, publiez des commentaires au bas de ce dernier ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2d686-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2d686-106">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="2d686-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="2d686-107">Choisir un objectif en matière de protection</span><span class="sxs-lookup"><span data-stu-id="2d686-107">Choose a protection goal</span></span>

<span data-ttu-id="2d686-108">Sélectionnez les éléments à répliquer et l’emplacement de la réplication.</span><span class="sxs-lookup"><span data-stu-id="2d686-108">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="2d686-109">Cliquez sur **Site Recovery** > **Étape 1 : Préparez l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="2d686-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="2d686-110">Sélectionnez **Vers le site de récupération**, puis **Oui, avec Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="2d686-110">Select **To recovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="2d686-111">Sélectionnez **Oui** pour indiquer que vous utilisez VMM pour gérer les hôtes Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2d686-111">Select **Yes** to indicate you're using VMM to manage the Hyper-V hosts.</span></span>
4. <span data-ttu-id="2d686-112">Sélectionnez **Oui** si vous avez un serveur VMM secondaire.</span><span class="sxs-lookup"><span data-stu-id="2d686-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="2d686-113">Si vous déployez la réplication entre des clouds sur un seul serveur VMM, cliquez sur **Non**.</span><span class="sxs-lookup"><span data-stu-id="2d686-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="2d686-114">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d686-114">Then click **OK**.</span></span>

    ![Sélectionner des objectifs](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="2d686-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d686-116">Next steps</span></span>

<span data-ttu-id="2d686-117">Aller à [Étape 6 : Configurer la source et la cible de réplication](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="2d686-117">Go to [Step 6: Set up the replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>