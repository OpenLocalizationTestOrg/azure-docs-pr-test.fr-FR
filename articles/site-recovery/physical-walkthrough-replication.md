---
title: "Configurer une stratégie de réplication pour la réplication de serveurs physiques vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes requises pour configurer une stratégie de réplication lors de la réplication de serveurs physiques locaux vers le stockage Azure à l’aide du service Azure Site Recovery"
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
ms.openlocfilehash: 9ce23382001b54e7b9b7a58b8dd9aa61b400826d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-to-azure"></a><span data-ttu-id="272a4-103">Étape 8 : Configurer une stratégie de réplication pour la réplication de serveurs physiques vers Azure</span><span class="sxs-lookup"><span data-stu-id="272a4-103">Step 8: Set up a replication policy for physical server replication to Azure</span></span>


<span data-ttu-id="272a4-104">Cet article explique comment configurer une stratégie de réplication pour la réplication de serveurs physiques Windows/Linux vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="272a4-104">This article describes how to set up a replication policy when you're replicating Windows/Linux physical servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="272a4-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="272a4-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="272a4-106">Configurer une stratégie</span><span class="sxs-lookup"><span data-stu-id="272a4-106">Configure a policy</span></span>

1. <span data-ttu-id="272a4-107">Cliquez sur **Infrastructure de Site Recovery** > **Stratégies de réplication** > **+Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="272a4-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="272a4-108">Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="272a4-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="272a4-109">Dans le champ **Seuil d’objectif de point de récupération**, spécifiez la limite de l’objectif de point de récupération.</span><span class="sxs-lookup"><span data-stu-id="272a4-109">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="272a4-110">Cette valeur indique la fréquence à laquelle les points de récupération des données sont créés.</span><span class="sxs-lookup"><span data-stu-id="272a4-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="272a4-111">Une alerte est générée lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="272a4-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="272a4-112">Dans **Rétention des points de récupération**, spécifiez la durée de la fenêtre de rétention pour chaque point de récupération (en heures).</span><span class="sxs-lookup"><span data-stu-id="272a4-112">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="272a4-113">Les machines virtuelles répliquées peuvent être récupérées à n’importe quel point dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="272a4-113">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="272a4-114">Les machines virtuelles répliquées vers Premium Storage peuvent prendre en charge jusqu’à 24 heures de rétention et 72 heures en cas de stockage standard.</span><span class="sxs-lookup"><span data-stu-id="272a4-114">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="272a4-115">Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes).</span><span class="sxs-lookup"><span data-stu-id="272a4-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="272a4-116">Cliquez sur **OK** pour créer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="272a4-116">Click **OK** to create the policy.</span></span>

    ![Stratégie de réplication](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="272a4-118">Lorsque vous créez une stratégie, cette dernière est automatiquement associée au serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="272a4-118">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="272a4-119">Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="272a4-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="272a4-120">Par exemple, si la stratégie de réplication est **rep-policy**, la stratégie de restauration automatique correspond alors à **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="272a4-120">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="272a4-121">Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="272a4-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="272a4-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="272a4-122">Next steps</span></span>

<span data-ttu-id="272a4-123">Aller à l’[Étape 9 : Installer le service Mobilité](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="272a4-123">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>
