---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication de serveur physique avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication locale stockage tooAzure de serveurs physiques à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="d1c2b-103">Étape 8 : Définir une stratégie de réplication pour le serveur physique réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1c2b-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="d1c2b-104">Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure de serveurs physiques Windows/Linux à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="d1c2b-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d1c2b-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="d1c2b-106">Configurer une stratégie</span><span class="sxs-lookup"><span data-stu-id="d1c2b-106">Configure a policy</span></span>

1. <span data-ttu-id="d1c2b-107">Cliquez sur **Infrastructure de Site Recovery** > **Stratégies de réplication** > **+Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="d1c2b-108">Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="d1c2b-109">Dans **seuil RPO**, spécifiez la limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="d1c2b-110">Cette valeur indique la fréquence à laquelle les points de récupération des données sont créés.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="d1c2b-111">Une alerte est générée lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="d1c2b-112">Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="d1c2b-113">Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="d1c2b-114">Des too24 rétention d’heures est pris en charge pour les machines répliquées toopremium stockage et 72 heures pour le stockage standard.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="d1c2b-115">Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes).</span><span class="sxs-lookup"><span data-stu-id="d1c2b-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="d1c2b-116">Cliquez sur **OK** stratégie de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-116">Click **OK** toocreate hello policy.</span></span>

    ![Stratégie de réplication](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="d1c2b-118">Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="d1c2b-119">Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="d1c2b-120">Par exemple, si hello stratégie de réplication est **rep-policy** stratégie de restauration automatique hello sera **rep-stratégie de la restauration automatique**.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="d1c2b-121">Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c2b-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1c2b-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1c2b-122">Next steps</span></span>

<span data-ttu-id="d1c2b-123">Accédez trop[étape 9 : installer le service de mobilité hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="d1c2b-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
