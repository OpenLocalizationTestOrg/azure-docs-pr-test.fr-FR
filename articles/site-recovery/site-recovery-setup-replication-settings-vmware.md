---
title: "aaaSet des paramètres de réplication pour Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication tooorchestrate toodeploy Site Recovery, le basculement et récupération des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="5147d-103">Gérer la stratégie de réplication pour VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="5147d-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="5147d-104">Créer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="5147d-104">Create a replication policy</span></span>

1. <span data-ttu-id="5147d-105">Sélectionnez **Gérer** > **Infrastructure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="5147d-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="5147d-106">Sélectionnez **Stratégies de réplication** sous **Pour les machines VMware et physiques**.</span><span class="sxs-lookup"><span data-stu-id="5147d-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="5147d-107">Sélectionnez **+Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="5147d-107">Select **+Replication policy**.</span></span>

    ![Créer une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="5147d-109">Entrez le nom de la stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="5147d-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="5147d-110">Dans **seuil RPO**, spécifiez la limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="5147d-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="5147d-111">Des alertes sont générées lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="5147d-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="5147d-112">Dans **rétention du point de récupération**, spécifier (en heures) hello de durée de conservation hello pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="5147d-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="5147d-113">Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre de rétention.</span><span class="sxs-lookup"><span data-stu-id="5147d-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5147d-114">Les heures too24 de rétention sont pris en charge pour les machines répliquées toopremium stockage.</span><span class="sxs-lookup"><span data-stu-id="5147d-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="5147d-115">Les heures too72 de rétention sont pris en charge pour les machines répliquées toostandard stockage.</span><span class="sxs-lookup"><span data-stu-id="5147d-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5147d-116">Une stratégie de réplication pour la restauration automatique est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="5147d-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="5147d-117">Dans **Fréquence des captures instantanées cohérentes au niveau de l’application**, spécifiez la fréquence de création des points de récupération qui contiennent des captures instantanées cohérentes au niveau de l’application (en minutes).</span><span class="sxs-lookup"><span data-stu-id="5147d-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="5147d-118">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5147d-118">Click **OK**.</span></span> <span data-ttu-id="5147d-119">stratégie de Hello doit être créée dans les 30 secondes too60.</span><span class="sxs-lookup"><span data-stu-id="5147d-119">hello policy should be created in 30 too60 seconds.</span></span>

![Génération d’une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="5147d-121">Associer un serveur de configuration à une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="5147d-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="5147d-122">Choisissez toowhich de stratégie de réplication hello tooassociate hello configuration serveur.</span><span class="sxs-lookup"><span data-stu-id="5147d-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="5147d-123">Cliquez sur **Associer**.</span><span class="sxs-lookup"><span data-stu-id="5147d-123">Click **Associate**.</span></span>
<span data-ttu-id="5147d-124">![Associer un serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="5147d-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="5147d-125">Sélectionnez le serveur de configuration hello de liste hello des serveurs.</span><span class="sxs-lookup"><span data-stu-id="5147d-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="5147d-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5147d-126">Click **OK**.</span></span> <span data-ttu-id="5147d-127">serveur de configuration Hello doit être associé dans un seul tootwo minutes.</span><span class="sxs-lookup"><span data-stu-id="5147d-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Association du serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="5147d-129">Modifier une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="5147d-129">Edit a replication policy</span></span>
1. <span data-ttu-id="5147d-130">Choisissez la stratégie de réplication hello pour lequel vous souhaitez tooedit les paramètres de réplication.</span><span class="sxs-lookup"><span data-stu-id="5147d-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="5147d-131">![Modifier la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="5147d-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="5147d-132">Cliquez sur **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="5147d-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="5147d-133">![Modifier les paramètres de la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="5147d-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="5147d-134">Modifier les paramètres de hello selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5147d-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="5147d-135">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5147d-135">Click **Save**.</span></span> <span data-ttu-id="5147d-136">stratégie de Hello doit être enregistré dans les deux minutes toofive, selon le nombre de machines virtuelles sont à l’aide de la stratégie de réplication.</span><span class="sxs-lookup"><span data-stu-id="5147d-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Enregistrer la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="5147d-138">Dissocier un serveur de configuration d’une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="5147d-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="5147d-139">Choisissez toowhich de stratégie de réplication hello tooassociate hello configuration serveur.</span><span class="sxs-lookup"><span data-stu-id="5147d-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="5147d-140">Cliquez sur **Dissocier**.</span><span class="sxs-lookup"><span data-stu-id="5147d-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="5147d-141">Sélectionnez le serveur de configuration hello de liste hello des serveurs.</span><span class="sxs-lookup"><span data-stu-id="5147d-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="5147d-142">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5147d-142">Click **OK**.</span></span> <span data-ttu-id="5147d-143">serveur de configuration Hello doit être dissocié en un seul tootwo minutes.</span><span class="sxs-lookup"><span data-stu-id="5147d-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5147d-144">Vous ne pouvez pas dissocier un serveur de configuration s’il existe au moins un élément répliqué à l’aide de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5147d-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="5147d-145">Assurez-vous qu’aucun élément répliquées à l’aide de la stratégie de hello avant de vous dissocier le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="5147d-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="5147d-146">Supprimer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="5147d-146">Delete a replication policy</span></span>

1. <span data-ttu-id="5147d-147">Choisissez la stratégie de réplication hello que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="5147d-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="5147d-148">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="5147d-148">Click **Delete**.</span></span> <span data-ttu-id="5147d-149">stratégie de Hello doit être supprimée en 30 secondes too60.</span><span class="sxs-lookup"><span data-stu-id="5147d-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5147d-150">Vous ne pouvez pas supprimer une stratégie de réplication s’il a tooit de serveur associé au moins une configuration.</span><span class="sxs-lookup"><span data-stu-id="5147d-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="5147d-151">Assurez-vous qu’aucun élément répliquées à l’aide de la stratégie de hello et supprimez que tous les hello associées des serveurs de configuration avant de supprimer la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5147d-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
