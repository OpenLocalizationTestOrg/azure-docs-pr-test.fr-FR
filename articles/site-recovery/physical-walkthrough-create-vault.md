---
title: "Configurer un coffre pour la réplication de serveurs physiques vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer un coffre dans le cadre de la réplication de serveurs physiques vers Azure à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="57f69-103">Étape 6 : Configurer un coffre pour la réplication de serveurs physiques vers Azure</span><span class="sxs-lookup"><span data-stu-id="57f69-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="57f69-104">Cet article décrit comment configurer un coffre.</span><span class="sxs-lookup"><span data-stu-id="57f69-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="57f69-105">Vous créez le coffre et spécifiez ce que vous souhaitez répliquer à partir de l’emplacement local, vers Azure, à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="57f69-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="57f69-106">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="57f69-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="57f69-107">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="57f69-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="57f69-108">Sélectionner un objectif de protection</span><span class="sxs-lookup"><span data-stu-id="57f69-108">Select a protection goal</span></span>

<span data-ttu-id="57f69-109">Sélectionnez les éléments à répliquer et l’emplacement de la réplication.</span><span class="sxs-lookup"><span data-stu-id="57f69-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="57f69-110">Cliquez sur **Coffres Recovery Services** > coffre.</span><span class="sxs-lookup"><span data-stu-id="57f69-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="57f69-111">Dans le menu Ressource, cliquez sur **Site Recovery** > **Préparer l’infrastructure** > **Objectif de protection**.</span><span class="sxs-lookup"><span data-stu-id="57f69-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="57f69-112">Dans la boîte de dialogue **Objectif de protection**, sélectionnez **Vers Azure** > **Non virtualisé / Autre**.</span><span class="sxs-lookup"><span data-stu-id="57f69-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="57f69-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57f69-113">Next steps</span></span>

<span data-ttu-id="57f69-114">Aller à l’[Étape 7 : Configurer la source et la cible](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="57f69-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
