---
title: "Configurer les paramètres de réplication pour Azure Site Recovery | Microsoft Docs"
description: "Explique comment déployer Site Recovery pour orchestrer la réplication, le basculement et la récupération de machines virtuelles Hyper-V dans des clouds VMM vers Azure."
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
ms.openlocfilehash: 73a1f19177f23441f5f7165cf2bc92ba85e62aa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-replication-policy-for-vmware-to-azure"></a><span data-ttu-id="b64d5-103">Gérer la stratégie de réplication pour VMware dans Azure</span><span class="sxs-lookup"><span data-stu-id="b64d5-103">Manage replication policy for VMware to Azure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="b64d5-104">Créer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b64d5-104">Create a replication policy</span></span>

1. <span data-ttu-id="b64d5-105">Sélectionnez **Gérer** > **Infrastructure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="b64d5-106">Sélectionnez **Stratégies de réplication** sous **Pour les machines VMware et physiques**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="b64d5-107">Sélectionnez **+Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-107">Select **+Replication policy**.</span></span>

    ![Créer une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="b64d5-109">Entrez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="b64d5-109">Enter the policy name.</span></span>

5. <span data-ttu-id="b64d5-110">Dans le champ **Seuil d’objectif de point de récupération**, spécifiez la limite de l’objectif de point de récupération.</span><span class="sxs-lookup"><span data-stu-id="b64d5-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="b64d5-111">Des alertes sont générées lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="b64d5-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="b64d5-112">Dans **Rétention des points de récupération**, spécifiez la durée (en heures) de la fenêtre de rétention pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="b64d5-112">In **Recovery point retention**, specify (in hours) the duration of the retention window for each recovery point.</span></span> <span data-ttu-id="b64d5-113">Les machines protégées peuvent être récupérées à tout moment pendant cette fenêtre de rétention.</span><span class="sxs-lookup"><span data-stu-id="b64d5-113">Protected machines can be recovered to any point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64d5-114">Les machines virtuelles répliquées vers le Stockage Premium peuvent prendre en charge jusqu’à 24 heures de rétention.</span><span class="sxs-lookup"><span data-stu-id="b64d5-114">Up to 24 hours of retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="b64d5-115">Les machines virtuelles répliquées vers le Stockage Standard peuvent prendre en charge jusqu’à 72 heures de rétention.</span><span class="sxs-lookup"><span data-stu-id="b64d5-115">Up to 72 hours of retention is supported for machines replicated to standard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64d5-116">Une stratégie de réplication pour la restauration automatique est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="b64d5-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="b64d5-117">Dans **Fréquence des captures instantanées cohérentes au niveau de l’application**, spécifiez la fréquence de création des points de récupération qui contiennent des captures instantanées cohérentes au niveau de l’application (en minutes).</span><span class="sxs-lookup"><span data-stu-id="b64d5-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="b64d5-118">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-118">Click **OK**.</span></span> <span data-ttu-id="b64d5-119">La création de la stratégie devrait prendre entre 30 et 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="b64d5-119">The policy should be created in 30 to 60 seconds.</span></span>

![Génération d’une stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="b64d5-121">Associer un serveur de configuration à une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b64d5-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="b64d5-122">Choisissez la stratégie de réplication à laquelle vous souhaitez associer le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="b64d5-122">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="b64d5-123">Cliquez sur **Associer**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-123">Click **Associate**.</span></span>
<span data-ttu-id="b64d5-124">![Associer un serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="b64d5-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="b64d5-125">Sélectionnez le serveur de configuration dans la liste des serveurs.</span><span class="sxs-lookup"><span data-stu-id="b64d5-125">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="b64d5-126">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-126">Click **OK**.</span></span> <span data-ttu-id="b64d5-127">L’association du serveur de configuration devrait prendre entre une et deux minutes.</span><span class="sxs-lookup"><span data-stu-id="b64d5-127">The configuration server should be associated in one to two minutes.</span></span>

![Association du serveur de configuration](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="b64d5-129">Modifier une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b64d5-129">Edit a replication policy</span></span>
1. <span data-ttu-id="b64d5-130">Choisissez la stratégie de réplication pour laquelle vous souhaitez modifier les paramètres de réplication.</span><span class="sxs-lookup"><span data-stu-id="b64d5-130">Choose the replication policy for which you want to edit replication settings.</span></span>
<span data-ttu-id="b64d5-131">![Modifier la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="b64d5-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="b64d5-132">Cliquez sur **Edit Settings**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="b64d5-133">![Modifier les paramètres de la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="b64d5-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="b64d5-134">Modifiez les paramètres selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="b64d5-134">Change the settings based on your need.</span></span>
4. <span data-ttu-id="b64d5-135">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-135">Click **Save**.</span></span> <span data-ttu-id="b64d5-136">L’enregistrement de la stratégie devrait prendre entre deux et cinq minutes en fonction du nombre de machines virtuelles utilisant la stratégie de réplication.</span><span class="sxs-lookup"><span data-stu-id="b64d5-136">The policy should be saved in two to five minutes, depending on how many VMs are using that replication policy.</span></span>

![Enregistrer la stratégie de réplication](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="b64d5-138">Dissocier un serveur de configuration d’une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b64d5-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="b64d5-139">Choisissez la stratégie de réplication à laquelle vous souhaitez associer le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="b64d5-139">Choose the replication policy to which you want to associate the configuration server.</span></span>
2. <span data-ttu-id="b64d5-140">Cliquez sur **Dissocier**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="b64d5-141">Sélectionnez le serveur de configuration dans la liste des serveurs.</span><span class="sxs-lookup"><span data-stu-id="b64d5-141">Select the configuration server from the list of servers.</span></span>
4. <span data-ttu-id="b64d5-142">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-142">Click **OK**.</span></span> <span data-ttu-id="b64d5-143">La dissociation du serveur de configuration devrait prendre entre une et deux minutes.</span><span class="sxs-lookup"><span data-stu-id="b64d5-143">The configuration server should be dissociated in one to two minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64d5-144">Vous ne pouvez pas dissocier un serveur de configuration si un élément répliqué utilise cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="b64d5-144">You cannot dissociate a configuration server if there is at least one replicated item using the policy.</span></span> <span data-ttu-id="b64d5-145">Vérifiez qu’aucun élément répliqué n’utilise la stratégie avant de dissocier le serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="b64d5-145">Make sure there are no replicated items using the policy before you dissociate the configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="b64d5-146">Supprimer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b64d5-146">Delete a replication policy</span></span>

1. <span data-ttu-id="b64d5-147">Choisissez la stratégie de réplication que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="b64d5-147">Choose the replication policy that you want to delete.</span></span>
2. <span data-ttu-id="b64d5-148">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b64d5-148">Click **Delete**.</span></span> <span data-ttu-id="b64d5-149">La suppression de la stratégie devrait prendre entre 30 et 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="b64d5-149">The policy should be deleted in 30 to 60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b64d5-150">Vous ne pouvez pas supprimer une stratégie de réplication si un serveur de configuration lui est associé.</span><span class="sxs-lookup"><span data-stu-id="b64d5-150">You cannot delete a replication policy if it has at least one configuration server associated to it.</span></span> <span data-ttu-id="b64d5-151">Assurez-vous qu’aucun élément répliqué n’utilise la stratégie, et supprimez tous les serveurs de configuration avant de supprimer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="b64d5-151">Make sure there are no replicated items using the policy and delete all the associated configuration servers before you delete the policy.</span></span>
