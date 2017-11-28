---
title: aaaManage Azure recovery services coffres et serveurs | Documents Microsoft
description: "Utilisez ce didacticiel toolearn comment les services de récupération Azure toomanage coffres et les serveurs."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="e5757-103">Surveiller et gérer les serveurs et les coffres Azure Recovery services pour les ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="e5757-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5757-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e5757-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="e5757-105">Classique</span><span class="sxs-lookup"><span data-stu-id="e5757-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="e5757-106">Dans cet article vous trouverez une vue d’ensemble de hello analyse et gestion des tâches de sauvegarde disponibles via hello agent Microsoft Azure Backup Azure portal et hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="e5757-107">Cet article part du principe que vous disposez déjà d’un abonnement Azure et que vous avez créé au moins un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e5757-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="e5757-108">Ouvrez un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="e5757-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="e5757-109">tableau de bord coffre de Services de récupération Hello vous montre les détails de hello ou les attributs d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e5757-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="e5757-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e5757-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="e5757-111">Dans le menu du Hub hello, cliquez sur **plus Services**.</span><span class="sxs-lookup"><span data-stu-id="e5757-111">On hello Hub menu, click **More Services**.</span></span>

    ![Ouvrir une liste de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="e5757-113">Vous voulez tooopen un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e5757-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="e5757-114">Dans la boîte de dialogue hello, commencez à taper **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="e5757-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="e5757-115">Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée.</span><span class="sxs-lookup"><span data-stu-id="e5757-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="e5757-116">Cliquez sur **les coffres de Services de récupération** les coffres de liste de hello toodisplay des Services de récupération dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e5757-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="e5757-118">liste Hello des archivages de Recovery Services s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e5757-118">hello list of Recovery Services vaults opens.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="e5757-120">À partir de la liste de hello des coffres, sélectionnez le nom de hello Hello coffre Recovery Services tooopen.</span><span class="sxs-lookup"><span data-stu-id="e5757-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="e5757-121">Panneau de tableau de bord coffre Hello Recovery Services s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e5757-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![coffre recovery services tableau de bord](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="e5757-123">Maintenant que vous avez ouvert le coffre Recovery Services hello, essayez une des tâches de surveillance ni gestion hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="e5757-124">Surveiller les travaux et les alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="e5757-125">Vous surveillez les travaux et alertes à partir de hello Services de récupération de coffre de tableau de bord, où vous voyez :</span><span class="sxs-lookup"><span data-stu-id="e5757-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="e5757-126">Les détails des alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-126">Backup alerts details</span></span>
* <span data-ttu-id="e5757-127">Fichiers et dossiers, ainsi que les machines virtuelles protégées dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="e5757-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="e5757-128">Le stockage total consommé dans Azure</span><span class="sxs-lookup"><span data-stu-id="e5757-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="e5757-129">L’état du travail de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-129">Backup job status</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="e5757-131">En cliquant sur les informations de hello dans chacun de ces vignettes ouvrir Panneau associé de hello où vous gérer les tâches associées.</span><span class="sxs-lookup"><span data-stu-id="e5757-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="e5757-132">De haut hello Hello du tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="e5757-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="e5757-133">Panneau Paramètres : vous donne accès aux tâches de sauvegarde disponibles.</span><span class="sxs-lookup"><span data-stu-id="e5757-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="e5757-134">Coffre de sauvegarde - permet de sauvegarder des fichiers et dossiers (ou machines virtuelles Azure) toohello Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e5757-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="e5757-135">DELETE - si des services de récupération d’un coffre est n’est plus utilisé, vous pouvez le supprimer toofree l’espace de stockage.</span><span class="sxs-lookup"><span data-stu-id="e5757-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="e5757-136">DELETE est activée uniquement après la suppression de tous les serveurs protégés à partir du coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="e5757-138">Alertes relatives aux sauvegardes à l’aide de l’agent de sauvegarde Azure :</span><span class="sxs-lookup"><span data-stu-id="e5757-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="e5757-139">Niveau d’alerte</span><span class="sxs-lookup"><span data-stu-id="e5757-139">Alert Level</span></span> | <span data-ttu-id="e5757-140">Alertes envoyées</span><span class="sxs-lookup"><span data-stu-id="e5757-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="e5757-141">Critique</span><span class="sxs-lookup"><span data-stu-id="e5757-141">Critical</span></span> |<span data-ttu-id="e5757-142">Échec de sauvegarde, échec de récupération</span><span class="sxs-lookup"><span data-stu-id="e5757-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="e5757-143">Avertissement</span><span class="sxs-lookup"><span data-stu-id="e5757-143">Warning</span></span> |<span data-ttu-id="e5757-144">Sauvegarde s’est terminée avec avertissements (si les fichiers de moins de cent ne sont pas sauvegardés en raison de problèmes de toocorruption, et plusieurs millions fichiers sont correctement sauvegardés)</span><span class="sxs-lookup"><span data-stu-id="e5757-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="e5757-145">Informations</span><span class="sxs-lookup"><span data-stu-id="e5757-145">Informational</span></span> |<span data-ttu-id="e5757-146">Aucun</span><span class="sxs-lookup"><span data-stu-id="e5757-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="e5757-147">Gérer les alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-147">Manage Backup alerts</span></span>
<span data-ttu-id="e5757-148">Cliquez sur hello **les alertes de sauvegarde** vignette tooopen hello **les alertes de sauvegarde** panneau et gérer les alertes.</span><span class="sxs-lookup"><span data-stu-id="e5757-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Alertes de sauvegarde](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="e5757-150">Alertes de sauvegarde Hello vignette vous montre hello nombre de :</span><span class="sxs-lookup"><span data-stu-id="e5757-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="e5757-151">le nombre d’alertes critiques non résolues dans les 24 dernières heures</span><span class="sxs-lookup"><span data-stu-id="e5757-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="e5757-152">le nombre d’alertes d’avertissement non résolues dans les 24 dernières heures</span><span class="sxs-lookup"><span data-stu-id="e5757-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="e5757-153">En cliquant sur chacun de ces liens vous conduit toohello **les alertes de sauvegarde** panneau avec une vue filtrée de ces alertes (critiques ou avertissements).</span><span class="sxs-lookup"><span data-stu-id="e5757-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="e5757-154">À partir du panneau d’alertes de sauvegarde hello, vous :</span><span class="sxs-lookup"><span data-stu-id="e5757-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="e5757-155">Choisissez tooinclude des informations appropriées hello avec vos alertes.</span><span class="sxs-lookup"><span data-stu-id="e5757-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Choisir les colonnes](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="e5757-157">Filtrer les alertes selon leur gravité, leur état et les heures de début/fin</span><span class="sxs-lookup"><span data-stu-id="e5757-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="e5757-159">Configurer les paramètres de gravité, de fréquence et de destination des notifications, mais aussi activer ou désactiver les alertes</span><span class="sxs-lookup"><span data-stu-id="e5757-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="e5757-161">Si **par alerte** est sélectionné comme hello **notifier** fréquence aucun regroupement ou une réduction des courriers électroniques se produit.</span><span class="sxs-lookup"><span data-stu-id="e5757-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="e5757-162">Chaque alerte génère une notification.</span><span class="sxs-lookup"><span data-stu-id="e5757-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="e5757-163">C’est le paramètre par défaut de hello et courrier électronique de résolution hello est envoyé également immédiatement.</span><span class="sxs-lookup"><span data-stu-id="e5757-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="e5757-164">Si **horaire Digest** est sélectionné comme hello **notifier** fréquence un e-mail est envoyée à utilisateur toohello indiquant qu’il n’y pas résolu nouvelles alertes générés Bonjour dernière heure.</span><span class="sxs-lookup"><span data-stu-id="e5757-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="e5757-165">Un message électronique de résolution est envoyé à fin hello d’heure de hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="e5757-166">Les alertes peuvent être envoyées pour hello suivant des niveaux de gravité :</span><span class="sxs-lookup"><span data-stu-id="e5757-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="e5757-167">Critique</span><span class="sxs-lookup"><span data-stu-id="e5757-167">critical</span></span>
* <span data-ttu-id="e5757-168">Avertissement</span><span class="sxs-lookup"><span data-stu-id="e5757-168">warning</span></span>
* <span data-ttu-id="e5757-169">information</span><span class="sxs-lookup"><span data-stu-id="e5757-169">information</span></span>

<span data-ttu-id="e5757-170">Vous désactivez l’alerte hello avec hello **désactiver** bouton dans le panneau de détails de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="e5757-171">Lorsque vous cliquez sur Inactivate (Désactiver), vous pouvez ajouter des commentaires pour la résolution de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="e5757-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="e5757-172">Vous choisissez les colonnes hello souhaité dans le cadre de l’alerte hello avec hello tooappear **choisir les colonnes** bouton.</span><span class="sxs-lookup"><span data-stu-id="e5757-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="e5757-173">À partir de hello **paramètres** panneau, vous gérez les alertes de sauvegarde en sélectionnant **analyse et rapports > alertes et événements > alertes de sauvegarde** , puis en cliquant sur **filtre** ou  **Configurer des Notifications**.</span><span class="sxs-lookup"><span data-stu-id="e5757-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="e5757-174">Gérer les éléments de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-174">Manage Backup items</span></span>
<span data-ttu-id="e5757-175">La gestion des sauvegardes en local est maintenant disponible dans le portail de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="e5757-176">Dans la section de sauvegarde hello du tableau de bord hello, hello **des éléments de sauvegarde** vignette affiche le nombre de hello des éléments de sauvegarde protégés toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="e5757-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="e5757-177">Cliquez sur **fichiers-dossiers** Bonjour vignette d’éléments de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e5757-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="e5757-179">les éléments de sauvegarde Hello panneau s’ouvre avec hello filtrer ensemble tooFile-dossier dans lequel vous consultez chaque élément répertorié de sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="e5757-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="e5757-181">Si vous sélectionnez un élément de sauvegarde spécifique à partir de la liste de hello, vous consultez des informations essentielles hello pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="e5757-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="e5757-182">À partir de hello **paramètres** panneau, vous gérez des fichiers et dossiers en sélectionnant **éléments protégés > des éléments de sauvegarde** , puis en sélectionnant **dossiers de fichiers** de hello menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="e5757-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="e5757-184">Gérer les travaux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-184">Manage Backup jobs</span></span>
<span data-ttu-id="e5757-185">Tâches de sauvegarde pour à la fois localement (lorsque le serveur local de hello sauvegarde tooAzure) et les sauvegardes Azure sont visibles dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="e5757-186">Dans la section de sauvegarde du tableau de bord hello de hello, vignette de travail de sauvegarde hello affiche hello nombre tâches :</span><span class="sxs-lookup"><span data-stu-id="e5757-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="e5757-187">en cours</span><span class="sxs-lookup"><span data-stu-id="e5757-187">in progress</span></span>
* <span data-ttu-id="e5757-188">Échec de hello des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="e5757-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="e5757-189">toomanage vos travaux de sauvegarde, cliquez sur hello **les travaux de sauvegarde** vignette, qui ouvre le panneau des travaux de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="e5757-191">Vous modifiez les informations hello disponibles dans le panneau des travaux de sauvegarde hello avec hello **choisir les colonnes** bouton en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="e5757-192">Hello d’utilisation **filtre** tooselect bouton entre fichiers et de dossiers et de sauvegarde de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e5757-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="e5757-193">Si vous ne voyez pas votre sauvegarde des fichiers et des dossiers, cliquez sur **filtre** bouton en haut de hello de page de hello et sélectionnez **fichiers et dossiers** à partir du menu de Type d’élément hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="e5757-194">À partir de hello **paramètres** panneau, gérer des travaux de sauvegarde en sélectionnant **analyse et rapports > travaux > travaux de sauvegarde** , puis en sélectionnant **dossiers de fichiers** de dépôt de hello vers le bas du menu.</span><span class="sxs-lookup"><span data-stu-id="e5757-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="e5757-195">Surveiller l’utilisation de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-195">Monitor Backup usage</span></span>
<span data-ttu-id="e5757-196">Dans la section de sauvegarde du tableau de bord hello de hello, vignette d’utilisation de la sauvegarde de hello montre stockage hello consommé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e5757-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="e5757-197">Les données d’utilisation du stockage incluent :</span><span class="sxs-lookup"><span data-stu-id="e5757-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="e5757-198">Utilisation du stockage LRS cloud associée hello coffre</span><span class="sxs-lookup"><span data-stu-id="e5757-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="e5757-199">Utilisation du stockage GRS cloud associée hello coffre</span><span class="sxs-lookup"><span data-stu-id="e5757-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="e5757-200">Gérer vos serveurs de production</span><span class="sxs-lookup"><span data-stu-id="e5757-200">Manage your production servers</span></span>
<span data-ttu-id="e5757-201">Cliquez sur les serveurs de production, toomanage **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="e5757-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="e5757-202">Sous Gérer, cliquez sur **Infrastructure de sauvegarde > Serveurs de Production**.</span><span class="sxs-lookup"><span data-stu-id="e5757-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="e5757-203">listes de panneau Hello les serveurs de Production de tous vos serveurs de production disponible.</span><span class="sxs-lookup"><span data-stu-id="e5757-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="e5757-204">Cliquez sur un serveur dans les détails du serveur hello liste tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-204">Click on a server in hello list tooopen hello server details.</span></span>

![Éléments protégés](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="e5757-206">Agent de sauvegarde Azure hello ouvert</span><span class="sxs-lookup"><span data-stu-id="e5757-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="e5757-207">Ouvrez hello **Microsoft Azure Backup agent** (vous le rechercher votre ordinateur pour *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="e5757-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="e5757-209">À partir de hello **Actions** disponible à l’adresse hello à droite de la console de l’agent de sauvegarde hello vous effectuez hello les tâches de gestion suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5757-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="e5757-210">Inscription du serveur</span><span class="sxs-lookup"><span data-stu-id="e5757-210">Register Server</span></span>
* <span data-ttu-id="e5757-211">Planification d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e5757-211">Schedule Backup</span></span>
* <span data-ttu-id="e5757-212">Sauvegarder maintenant</span><span class="sxs-lookup"><span data-stu-id="e5757-212">Back Up now</span></span>
* <span data-ttu-id="e5757-213">Modifier les propriétés</span><span class="sxs-lookup"><span data-stu-id="e5757-213">Change Properties</span></span>

![Actions de la console de l’agent Microsoft Azure Backup.](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="e5757-215">trop**récupérer les données**, consultez [restaurer des fichiers tooa Windows server ou la machine du client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="e5757-216">Modifier la planification de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="e5757-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="e5757-217">Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5757-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="e5757-219">Bonjour **Assistant Planification de sauvegarde** laisser hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5757-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="e5757-221">Si vous souhaitez tooadd ou de modifier les éléments sur hello **tooBackup de sélectionner les éléments** écran, cliquez sur **ajouter les éléments**.</span><span class="sxs-lookup"><span data-stu-id="e5757-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="e5757-222">Vous pouvez également définir **paramètres d’Exclusion** à partir de cette page dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="e5757-223">Si vous souhaitez que les fichiers tooexclude ou procédure hello pour l’ajout de lecture de types de fichiers [paramètres d’exclusion](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="e5757-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="e5757-224">Sélectionnez les fichiers de hello et les dossiers que vous souhaitez tooback haut et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5757-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="e5757-226">Spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5757-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="e5757-227">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="e5757-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="e5757-229">Spécifier la planification de sauvegarde hello est expliquée en détail dans ce [article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="e5757-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="e5757-230">Sélectionnez hello **stratégie de rétention** pour la copie de sauvegarde hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5757-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="e5757-232">Sur hello **Confirmation** hello consulter les informations de l’écran, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e5757-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="e5757-233">Une fois l’Assistant de hello termine la création de hello **planification de sauvegarde**, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="e5757-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="e5757-234">Après la modification de protection, vous pouvez vérifier le déclenchement de sauvegardes par toohello de va **travaux** onglet et en s’assurant que les modifications sont répercutées dans hello des travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e5757-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="e5757-235">Activation de la limitation du réseau</span><span class="sxs-lookup"><span data-stu-id="e5757-235">Enable Network Throttling</span></span>

<span data-ttu-id="e5757-236">agent de sauvegarde Azure Hello comprend un onglet de limitation qui vous permet de toocontrol utilisation de la bande passante réseau lors du transfert de données.</span><span class="sxs-lookup"><span data-stu-id="e5757-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="e5757-237">Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic internet.</span><span class="sxs-lookup"><span data-stu-id="e5757-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="e5757-238">La limitation des données de transfert s’applique tooback des activités et de restauration.</span><span class="sxs-lookup"><span data-stu-id="e5757-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="e5757-239">tooenable de limitation :</span><span class="sxs-lookup"><span data-stu-id="e5757-239">tooenable throttling:</span></span>

1. <span data-ttu-id="e5757-240">Bonjour **agent de sauvegarde**, cliquez sur **modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="e5757-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="e5757-241">Sur hello ** limitation onglet, sélectionnez **activer l’utilisation de la bande passante internet de limitation pour les opérations de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5757-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitation du réseau](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="e5757-243">Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.</span><span class="sxs-lookup"><span data-stu-id="e5757-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="e5757-244">valeurs de la bande passante Hello commencent à 512 kilo-octets par seconde (Kbits/s) et peuvent atteindre la too1023 les mégaoctets par seconde (Mbits/s).</span><span class="sxs-lookup"><span data-stu-id="e5757-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="e5757-245">Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont considérés comme travail jours.</span><span class="sxs-lookup"><span data-stu-id="e5757-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="e5757-246">temps de Hello en dehors de hello désigné des heures de travail est toobe pris en compte les heures chômées.</span><span class="sxs-lookup"><span data-stu-id="e5757-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="e5757-247">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5757-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="e5757-248">Gérer les paramètres d’exclusion</span><span class="sxs-lookup"><span data-stu-id="e5757-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="e5757-249">Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="e5757-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="e5757-251">Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e5757-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="e5757-253">Bonjour Assistant Planification de sauvegarde, laissez hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5757-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="e5757-255">Cliquez sur **Paramètres d’exclusion**.</span><span class="sxs-lookup"><span data-stu-id="e5757-255">Click **Exclusions Settings**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="e5757-257">Cliquez sur **Ajouter une exclusion**.</span><span class="sxs-lookup"><span data-stu-id="e5757-257">Click **Add Exclusion**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="e5757-259">Sélectionnez l’emplacement de hello et cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5757-259">Select hello location and then, click **OK**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="e5757-261">Extension de fichier hello Bonjour **Type de fichier** champ.</span><span class="sxs-lookup"><span data-stu-id="e5757-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="e5757-263">Ajout d’une extension .mp3</span><span class="sxs-lookup"><span data-stu-id="e5757-263">Adding an .mp3 extension</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="e5757-265">tooadd une autre extension, cliquez sur **ajouter une Exclusion** et entrez une autre extension de fichier (l’ajout d’une extension .jpeg).</span><span class="sxs-lookup"><span data-stu-id="e5757-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="e5757-267">Lorsque vous avez ajouté toutes les extensions de hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5757-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="e5757-268">Poursuivez hello Assistant Planification de sauvegarde en cliquant sur **suivant** jusqu'à hello **page de Confirmation**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e5757-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="e5757-270">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="e5757-270">Frequently asked questions</span></span>
<span data-ttu-id="e5757-271">**Q1. état du travail de sauvegarde Hello affiche comme étant terminée en hello agent de sauvegarde Azure, pourquoi n’il obtenir répercutée immédiatement dans le portail ?**</span><span class="sxs-lookup"><span data-stu-id="e5757-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="e5757-272">R1.</span><span class="sxs-lookup"><span data-stu-id="e5757-272">A1.</span></span> <span data-ttu-id="e5757-273">Il est au délai maximal de 15 minutes entre l’état du travail de sauvegarde hello répercutée dans hello agent de sauvegarde Azure et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e5757-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="e5757-274">**Q.2 en cas d’échec d’une opération de sauvegarde, combien de temps faut-il tooraise une alerte ?**</span><span class="sxs-lookup"><span data-stu-id="e5757-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="e5757-275">A.2 une alerte est générée au sein de 20 minutes de hello Échec de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="e5757-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="e5757-276">**Q3. Est-il possible qu’aucun e-mail ne soit envoyé alors que les notifications sont activées ?**</span><span class="sxs-lookup"><span data-stu-id="e5757-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="e5757-277">R3</span><span class="sxs-lookup"><span data-stu-id="e5757-277">A3.</span></span> <span data-ttu-id="e5757-278">Voici les cas de hello lorsque hello notification ne sera pas être envoyée dans un bruit de commande tooreduce hello alerte :</span><span class="sxs-lookup"><span data-stu-id="e5757-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="e5757-279">Si les notifications sont configurées par heure et une alerte est déclenchée et résolue au sein de l’heure de hello</span><span class="sxs-lookup"><span data-stu-id="e5757-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="e5757-280">Si le travail est annulé.</span><span class="sxs-lookup"><span data-stu-id="e5757-280">Job is canceled.</span></span>
* <span data-ttu-id="e5757-281">Si le travail de sauvegarde secondaire a échoué, car un travail de sauvegarde d’origine est en cours.</span><span class="sxs-lookup"><span data-stu-id="e5757-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="e5757-282">Résolution des problèmes de surveillance</span><span class="sxs-lookup"><span data-stu-id="e5757-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="e5757-283">**Problème :** travaux et/ou les alertes à partir de l’agent de sauvegarde Azure hello n’apparaissent pas dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="e5757-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="e5757-284">**Étapes de dépannage :** hello processus, ```OBRecoveryServicesManagementAgent```, envoie hello toohello de données de travail et d’alerte service Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e5757-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="e5757-285">Il peut arriver que ce processus se bloque ou s’arrête.</span><span class="sxs-lookup"><span data-stu-id="e5757-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="e5757-286">processus de hello tooverify n’est pas en cours d’exécution, ouvrez **le Gestionnaire des tâches** et vérifiez si hello ```OBRecoveryServicesManagementAgent``` est en cours.</span><span class="sxs-lookup"><span data-stu-id="e5757-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="e5757-287">En supposant que le processus de hello ne fonctionne pas, ouvrez **le panneau de configuration** et parcourir la liste hello des services.</span><span class="sxs-lookup"><span data-stu-id="e5757-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="e5757-288">Démarrez ou redémarrez l’**Agent de gestion Microsoft Azure Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="e5757-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="e5757-289">Pour plus d’informations, consultez journaux hello à :</span><span class="sxs-lookup"><span data-stu-id="e5757-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="e5757-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e5757-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="e5757-291">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5757-291">Next steps</span></span>
* [<span data-ttu-id="e5757-292">Restaurer un serveur Windows Server ou un client Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="e5757-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="e5757-293">toolearn en savoir plus sur Azure Backup, consultez [vue d’ensemble de la sauvegarde Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="e5757-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="e5757-294">Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="e5757-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
