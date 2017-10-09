---
title: "les serveurs aaaRemove et désactivez la protection | Documents Microsoft"
description: "Cet article décrit comment toounregister les serveurs à partir d’une récupération de Site de coffre et la protection de toodisable pour les serveurs physiques et virtuels."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="b3d6d-103">Supprimer des serveurs et désactiver la protection</span><span class="sxs-lookup"><span data-stu-id="b3d6d-103">Remove servers and disable protection</span></span>

<span data-ttu-id="b3d6d-104">Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="b3d6d-105">service de Hello orchestre la réplication, le basculement et récupération des ordinateurs virtuels et des serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="b3d6d-106">Machines peuvent être répliquée tooAzure ou centre de données secondaire locale tooa.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="b3d6d-107">Pour avoir un rapide aperçu, consultez la section [Qu’est-ce qu’Azure Site Recovery ?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b3d6d-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="b3d6d-108">Cet article décrit comment toounregister les serveurs à partir des Services de récupération de coffre Bonjour portail Azure, et comment toodisable la protection des machines protégées par la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="b3d6d-109">Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b3d6d-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="b3d6d-110">Annuler l’inscription d’un serveur de configuration connecté</span><span class="sxs-lookup"><span data-stu-id="b3d6d-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="b3d6d-111">Si vous répliquez des ordinateurs virtuels VMware ou tooAzure des serveurs physiques Windows/Linux, vous pouvez annuler l’inscription un serveur de configuration connecté à partir d’un archivage comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b3d6d-112">Désactivez la protection des ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-112">Disable machine protection.</span></span> <span data-ttu-id="b3d6d-113">Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b3d6d-114">Dissociez les stratégies.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-114">Disassociate any policies.</span></span> <span data-ttu-id="b3d6d-115">Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **stratégies de réplication**, double-cliquez sur hello stratégie associée.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b3d6d-116">Serveur de configuration avec le bouton hello > **dissocier**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="b3d6d-117">Supprimez les processus locaux supplémentaires ou les serveurs cibles maîtres.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b3d6d-118">Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **serveurs de Configuration**, serveur de hello avec le bouton droit > **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="b3d6d-119">Supprimer le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="b3d6d-120">Désinstaller manuellement le service de mobilité hello en cours d’exécution sur le serveur cible maître de hello (il s’agit soit distinct serveur, ou en cours d’exécution sur le serveur de configuration hello).</span><span class="sxs-lookup"><span data-stu-id="b3d6d-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="b3d6d-121">Désinstallez les serveurs de traitement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="b3d6d-122">Désinstallez le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="b3d6d-123">Sur le serveur de configuration hello, désinstallez instance hello de MySQL qui a été installée par la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="b3d6d-124">Dans le Registre hello hello du serveur de configuration SUPPR hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="b3d6d-125">Annuler l’inscription d’un serveur de configuration non connecté</span><span class="sxs-lookup"><span data-stu-id="b3d6d-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="b3d6d-126">Si vous répliquez des ordinateurs virtuels VMware ou tooAzure des serveurs physiques Windows/Linux, vous pouvez annuler l’inscription un serveur de configuration non connecté à partir d’un archivage comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b3d6d-127">Désactivez la protection des ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-127">Disable machine protection.</span></span> <span data-ttu-id="b3d6d-128">Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="b3d6d-129">Sélectionnez **arrêter la gestion hello machine**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="b3d6d-130">Supprimez les processus locaux supplémentaires ou les serveurs cibles maîtres.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b3d6d-131">Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **serveurs de Configuration**, serveur de hello avec le bouton droit > **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="b3d6d-132">Supprimer le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="b3d6d-133">Désinstaller manuellement le service de mobilité hello en cours d’exécution sur le serveur cible maître de hello (il s’agit soit distinct serveur, ou en cours d’exécution sur le serveur de configuration hello).</span><span class="sxs-lookup"><span data-stu-id="b3d6d-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="b3d6d-134">Désinstallez les serveurs de traitement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="b3d6d-135">Désinstallez le serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="b3d6d-136">Sur le serveur de configuration hello, désinstallez instance hello de MySQL qui a été installée par la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="b3d6d-137">Dans le Registre hello hello du serveur de configuration SUPPR hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="b3d6d-138">Annuler l’inscription d’un serveur VMM connecté</span><span class="sxs-lookup"><span data-stu-id="b3d6d-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="b3d6d-139">En tant que meilleure pratique, nous vous recommandons d’annuler l’inscription serveur VMM de hello lorsqu’il est connecté tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="b3d6d-140">Cela garantit que les paramètres sur les serveurs VMM hello (et sur d’autres serveurs VMM avec les clouds associés) sont correctement nettoyées.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="b3d6d-141">En cas de problème de connectivité permanent, ne supprimez qu’un serveur non connecté.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="b3d6d-142">Si le serveur VMM de hello n’est pas connecté, vous devez toomanually exécuter un tooclean de script des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="b3d6d-143">Arrêter la réplication des machines virtuelles dans des clouds sur le serveur VMM tooremove de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="b3d6d-144">Supprimer tous les mappages réseau utilisés par les clouds sur le serveur VMM toodelete de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="b3d6d-145">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **le mappage réseau**, cliquez sur le mappage réseau hello >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b3d6d-146">Dissocier des stratégies de réplication à partir de clouds sur le serveur VMM tooremove de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="b3d6d-147">Dans **Infrastructure Site Recovery** > **pour System Center VMM** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b3d6d-148">Cliquez sur le cloud de hello > **dissocier**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="b3d6d-149">Supprimer le serveur VMM de hello ou nœud actif de VMM.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="b3d6d-150">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **serveurs VMM**, serveur de hello avec le bouton droit >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="b3d6d-151">Désinstallez hello fournisseur manuellement sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="b3d6d-152">Si vous avez un cluster, supprimez-le de tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="b3d6d-153">Si vous effectuez une réplication tooAzure, supprimez manuellement hello Microsoft Recovery Services agent hôtes Hyper-V dans des clouds hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="b3d6d-154">Annuler l’inscription d’un serveur VMM non connecté</span><span class="sxs-lookup"><span data-stu-id="b3d6d-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="b3d6d-155">Arrêter la réplication des machines virtuelles dans des clouds sur le serveur VMM tooremove de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="b3d6d-156">Supprimer tous les mappages réseau utilisés par les clouds sur le serveur VMM hello que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="b3d6d-157">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **le mappage réseau**, cliquez sur le mappage réseau hello >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b3d6d-158">Notez l’ID de hello du serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="b3d6d-159">Dissocier des stratégies de réplication à partir de clouds sur le serveur VMM tooremove de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="b3d6d-160">Dans **Infrastructure Site Recovery** > **pour System Center VMM** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b3d6d-161">Cliquez sur le cloud de hello > **dissocier**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="b3d6d-162">Supprimer le serveur VMM de hello ou le nœud actif.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="b3d6d-163">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **serveurs VMM**, serveur de hello avec le bouton droit >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="b3d6d-164">Téléchargez et exécutez hello [script de nettoyage](http://aka.ms/asr-cleanup-script-vmm) sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="b3d6d-165">Ouvrez PowerShell avec hello **exécuter en tant qu’administrateur** option, la stratégie d’exécution toochange hello pour l’étendue de la valeur par défaut (LocalMachine) hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="b3d6d-166">Dans le script de hello, spécifiez ID hello Hello serveur VMM que vous souhaitez tooremove.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="b3d6d-167">script de Hello supprime l’inscription et le cloud appariement des informations à partir du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="b3d6d-168">Exécutez le script de nettoyage de hello sur tous les serveurs VMM qui contiennent des clouds qui sont associés à des clouds sur le serveur VMM tooremove de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="b3d6d-169">Exécutez le script de nettoyage hello sur n’importe quel autres passifs nœuds de cluster VMM qui ont hello que fournisseur installé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="b3d6d-170">Désinstallez hello fournisseur manuellement sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="b3d6d-171">Si vous avez un cluster, supprimez-le de tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="b3d6d-172">Si vous tooAzure de réplication, vous pouvez supprimer hello Microsoft Recovery Services agent à partir des hôtes Hyper-V dans des clouds hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="b3d6d-173">Annuler l’inscription d’un hôte Hyper-V dans un site Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b3d6d-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="b3d6d-174">Les hôtes Hyper-V non gérés par VMM sont rassemblés dans un site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="b3d6d-175">Pour supprimer un hôte d’un site Hyper-V, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="b3d6d-176">Désactivez la réplication pour les machines virtuelles Hyper-V situé sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="b3d6d-177">Dissocier des stratégies pour le site de Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="b3d6d-178">Dans **Infrastructure Site Recovery** > **pour les Sites Hyper-V** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b3d6d-179">Site de hello avec le bouton droit > **dissocier**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="b3d6d-180">Supprimez les hôtes Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="b3d6d-181">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **hôtes Hyper-V**, serveur de hello avec le bouton droit >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="b3d6d-182">Supprimer le site de hello Hyper-V après la suppression de tous les ordinateurs hôtes à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="b3d6d-183">Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **Sites Hyper-V**, site de hello avec le bouton droit >  **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="b3d6d-184">Exécutez hello script suivant sur chaque hôte Hyper-V que vous avez supprimé.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="b3d6d-185">Hello script nettoie les paramètres sur le serveur de hello et annule l’inscription du coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="b3d6d-186">Désactiver la protection d’une machine virtuelle VMware ou d’un serveur physique</span><span class="sxs-lookup"><span data-stu-id="b3d6d-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="b3d6d-187">Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b3d6d-188">Dans **Supprimer la machine**, sélectionnez une de ces options :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="b3d6d-189">**Désactivez la protection de machine hello (recommandé)**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b3d6d-190">Utilisez cette toostop option réplication machine de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b3d6d-191">Les paramètres de Site Recovery seront nettoyés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="b3d6d-192">Vous voyez uniquement cette option Bonjour suivant circonstances :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="b3d6d-193">**Vous avez redimensionné le volume de machine virtuelle hello**: quand vous redimensionnez un Bonjour volume virtuel ordinateur passe dans un état critique.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="b3d6d-194">Sélectionnez cette option toodisables la protection tout en conservant les points de récupération dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="b3d6d-195">Lorsque vous réactivez la protection pour l’ordinateur de hello, données hello pour le volume de hello redimensionné seront transférée tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="b3d6d-196">**Vous avez exécuté récemment un basculement**— après avoir exécuté un basculement tootest votre environnement, sélectionnez ce toostart option protéger à nouveau les machines locales.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="b3d6d-197">Il désactive chaque machine virtuelle, et puis vous devez tooenable protection leur à nouveau.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="b3d6d-198">La désactivation de la machine hello avec ce paramètre n’affecte pas hello ordinateur virtuel dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="b3d6d-199">Ne désinstallez pas service de mobilité hello à partir de l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="b3d6d-200">**Arrêter la gestion hello machine**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="b3d6d-201">Si vous sélectionnez cette option, hello ordinateur sera uniquement être supprimé le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b3d6d-202">Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b3d6d-203">paramètres tooremove hello machine et ordinateur hello tooremove hello abonnement Azure, vous avez besoin de tooclean hello paramètres en désinstallant le service de mobilité hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="b3d6d-204">Désactiver la protection d’une machine virtuelle Hyper-V dans un cloud VMM</span><span class="sxs-lookup"><span data-stu-id="b3d6d-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="b3d6d-205">Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b3d6d-206">Dans **Supprimer la machine**, sélectionnez une de ces options :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="b3d6d-207">**Désactivez la protection de machine hello (recommandé)**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b3d6d-208">Utilisez cette toostop option réplication machine de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b3d6d-209">Les paramètres de Site Recovery seront nettoyés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="b3d6d-210">**Arrêter la gestion hello machine**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="b3d6d-211">Si vous sélectionnez cette option, hello ordinateur sera uniquement être supprimé le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b3d6d-212">Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b3d6d-213">paramètres tooremove hello machine et ordinateur hello tooremove hello abonnement Azure, vous avez besoin de tooclean hello paramètres des manuellement, à l’aide d’instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="b3d6d-214">Notez que si vous sélectionnez l’ordinateur virtuel de hello toodelete et ses disques durs, ils allez supprimés à partir de l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="b3d6d-215">Nettoyer les paramètres de protection - site VMM secondaire de réplication tooa</span><span class="sxs-lookup"><span data-stu-id="b3d6d-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="b3d6d-216">Si vous avez sélectionné **arrêter la gestion hello machine** et vous réplication tooa du site secondaire, exécutez ce script sur tooclean du serveur principal hello des paramètres de hello pour l’ordinateur virtuel principal hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="b3d6d-217">Dans la console VMM hello, cliquez sur console de VMM PowerShell hello PowerShell bouton tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="b3d6d-218">Remplacez SQLVM1 par nom hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b3d6d-219">Sur le serveur VMM secondaire de hello exécuter cette tooclean script des paramètres hello pour l’ordinateur virtuel secondaire de hello :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="b3d6d-220">Sur le serveur secondaire VMM hello, actualiser les machines virtuelles de hello sur le serveur hôte de Hyper-V hello, afin que hello machine virtuelle secondaire obtient détectée à nouveau dans la console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="b3d6d-221">Hello étapes ci-dessus, désactivez les paramètres de réplication de hello sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="b3d6d-222">Si vous souhaitez que la réplication pour l’ordinateur virtuel de hello, exécuter le script suivant oh de hello toostop hello des ordinateurs virtuels principales et secondaires.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="b3d6d-223">Remplacez SQLVM1 par nom hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="b3d6d-224">Nettoyer les paramètres de protection : tooAzure de réplication</span><span class="sxs-lookup"><span data-stu-id="b3d6d-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="b3d6d-225">Si vous avez sélectionné **arrêter la gestion hello machine** et vous répliquez tooAzure, exécutez ce script sur le serveur VMM source hello, à l’aide de PowerShell à partir de la console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b3d6d-226">Hello étapes ci-dessus, désactivez les paramètres de réplication hello sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="b3d6d-227">réplication de toostop pour l’ordinateur virtuel de hello en cours d’exécution sur le serveur hôte de Hyper-V hello, exécutez ce script.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="b3d6d-228">Remplacez SQLVM1 par nom hello de votre machine virtuelle et host01.contoso.com avec nom hello du serveur hôte de Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="b3d6d-229">Désactiver la protection d’une machine virtuelle Hyper-V dans un site Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b3d6d-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="b3d6d-230">Utilisez cette procédure si vous effectuez une réplication tooAzure d’ordinateurs virtuels Hyper-V sans serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="b3d6d-231">Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b3d6d-232">Dans **supprimer la Machine**, vous pouvez sélectionner hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3d6d-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="b3d6d-233">**Désactivez la protection de machine hello (recommandé)**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b3d6d-234">Utilisez cette toostop option réplication machine de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b3d6d-235">Les paramètres de Site Recovery seront nettoyés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="b3d6d-236">**Arrêter la gestion hello machine**.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="b3d6d-237">Si vous sélectionnez cette option machine de hello n’est supprimée du coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b3d6d-238">Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b3d6d-239">paramètres tooremove sur la machine de hello et ordinateur virtuel tooremove hello hello abonnement Azure, vous devez appliquer tooclean hello paramètres configuration manuellement.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="b3d6d-240">Si vous sélectionnez l’ordinateur virtuel de hello toodelete et ses disques durs, ils sont supprimés à partir de l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="b3d6d-241">Si vous avez sélectionné **arrêter la gestion hello machine**, exécutez ce script sur le serveur hôte de Hyper-V source hello, la réplication tooremove pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="b3d6d-242">Remplacez SQLVM1 par nom hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b3d6d-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
