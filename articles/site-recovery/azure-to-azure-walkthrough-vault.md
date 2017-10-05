---
title: "Configurer un coffre pour la réplication de machines virtuelles Azure entre des régions avec Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer un coffre pour la réplication Azure entre des régions Azure à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="aa94a-103">Étape 4 : Configurer un coffre pour la réplication entre régions Azure</span><span class="sxs-lookup"><span data-stu-id="aa94a-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="aa94a-104">Après avoir [planifié les réseaux](azure-to-azure-walkthrough-network.md), utilisez cet article afin de configurer un coffre pour la réplication de machines virtuelles vers une autre région Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aa94a-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="aa94a-105">Une fois l’article terminé, vous devez avoir un coffre Recovery Services configuré.</span><span class="sxs-lookup"><span data-stu-id="aa94a-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="aa94a-106">Publiez des commentaires au bas de cet article ou posez des questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="aa94a-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="aa94a-107">La réplication de machines virtuelles Azure est disponible en préversion.</span><span class="sxs-lookup"><span data-stu-id="aa94a-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="aa94a-108">création d'un coffre</span><span class="sxs-lookup"><span data-stu-id="aa94a-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="aa94a-109">Nous vous recommandons de créer le coffre Recovery Services à l’emplacement où vous souhaitez répliquer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="aa94a-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="aa94a-110">Par exemple, si votre emplacement cible est la région États-Unis du Centre, créez le coffre dans **États-Unis du Centre**.</span><span class="sxs-lookup"><span data-stu-id="aa94a-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aa94a-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa94a-111">Next steps</span></span>

<span data-ttu-id="aa94a-112">Aller à [Étape 5 : Activer la réplication](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="aa94a-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
