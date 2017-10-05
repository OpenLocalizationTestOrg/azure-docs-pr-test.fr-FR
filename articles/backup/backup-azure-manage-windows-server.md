---
title: "Gérer les serveurs et les coffres Azure Recovery Services | Microsoft Docs"
description: "Ce didacticiel vous apprend à gérer les serveurs et les coffres Azure Recovery Services."
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
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="8318e-103">Surveiller et gérer les serveurs et les coffres Azure Recovery services pour les ordinateurs Windows</span><span class="sxs-lookup"><span data-stu-id="8318e-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8318e-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="8318e-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="8318e-105">Classique</span><span class="sxs-lookup"><span data-stu-id="8318e-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="8318e-106">Cet article offre une vue d’ensemble des tâches de surveillance et de gestion des sauvegardes disponibles via le portail Azure et l’agent Sauvegarde Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="8318e-107">Cet article part du principe que vous disposez déjà d’un abonnement Azure et que vous avez créé au moins un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="8318e-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="8318e-108">Ouvrez un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="8318e-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="8318e-109">Le tableau de bord du coffre Recovery Services vous montre les détails ou les attributs d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="8318e-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="8318e-110">Connectez-vous au [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="8318e-111">Dans le menu Hub, cliquez sur **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="8318e-111">On the Hub menu, click **More Services**.</span></span>

    ![Ouvrir une liste de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="8318e-113">Vous voulez ouvrir un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="8318e-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="8318e-114">Dans la boîte de dialogue, commencez à taper **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="8318e-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="8318e-115">Au fur et à mesure des caractères saisis, la liste est filtrée.</span><span class="sxs-lookup"><span data-stu-id="8318e-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="8318e-116">Cliquez sur **Coffres Recovery Services** pour afficher la liste des coffres Recovery Services de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8318e-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="8318e-118">La liste des coffres Recovery Services s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8318e-118">The list of Recovery Services vaults opens.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="8318e-120">Dans la liste des coffres, sélectionnez le coffre Recovery Services que vous souhaitez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="8318e-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="8318e-121">Le panneau du tableau de bord du coffre Recovery Services s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="8318e-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![coffre recovery services tableau de bord](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="8318e-123">Une fois le coffre Recovery Services ouvert, essayez l’une des tâches d’analyse ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="8318e-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="8318e-124">Surveiller les travaux et les alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="8318e-125">Vous pouvez surveiller les travaux et les alertes à partir du tableau de bord du coffre Recovery Services dans lequel s’affichent :</span><span class="sxs-lookup"><span data-stu-id="8318e-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="8318e-126">Les détails des alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-126">Backup alerts details</span></span>
* <span data-ttu-id="8318e-127">Les fichiers et dossiers, ainsi que les machines virtuelles Azure protégées dans le cloud</span><span class="sxs-lookup"><span data-stu-id="8318e-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="8318e-128">Le stockage total consommé dans Azure</span><span class="sxs-lookup"><span data-stu-id="8318e-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="8318e-129">L’état du travail de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-129">Backup job status</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="8318e-131">Cliquez sur les informations contenues dans chacune de ces mosaïques pour ouvrir le panneau correspondant où vous pourrez gérer les tâches associées.</span><span class="sxs-lookup"><span data-stu-id="8318e-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="8318e-132">De haut en bas dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="8318e-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="8318e-133">Panneau Paramètres : vous donne accès aux tâches de sauvegarde disponibles.</span><span class="sxs-lookup"><span data-stu-id="8318e-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="8318e-134">Panneau Sauvegarde : vous permet de sauvegarder de nouveaux fichiers et dossiers (ou machines virtuelles Azure) dans le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="8318e-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="8318e-135">Panneau Supprimer : si un coffre Recovery Services n’est plus utilisé, vous pouvez le supprimer pour libérer de l’espace de stockage.</span><span class="sxs-lookup"><span data-stu-id="8318e-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="8318e-136">L’option Supprimer est disponible uniquement une fois que tous les serveurs protégés ont été supprimés du coffre.</span><span class="sxs-lookup"><span data-stu-id="8318e-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="8318e-138">Alertes relatives aux sauvegardes à l’aide de l’agent de sauvegarde Azure :</span><span class="sxs-lookup"><span data-stu-id="8318e-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="8318e-139">Niveau d’alerte</span><span class="sxs-lookup"><span data-stu-id="8318e-139">Alert Level</span></span> | <span data-ttu-id="8318e-140">Alertes envoyées</span><span class="sxs-lookup"><span data-stu-id="8318e-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="8318e-141">Critique</span><span class="sxs-lookup"><span data-stu-id="8318e-141">Critical</span></span> |<span data-ttu-id="8318e-142">Échec de sauvegarde, échec de récupération</span><span class="sxs-lookup"><span data-stu-id="8318e-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="8318e-143">Avertissement</span><span class="sxs-lookup"><span data-stu-id="8318e-143">Warning</span></span> |<span data-ttu-id="8318e-144">Sauvegarde terminée avec des avertissements (lorsque moins de cent fichiers n’ont pas été sauvegardés du fait de problèmes d’altération et que plus d’un million de fichiers ont été correctement sauvegardés)</span><span class="sxs-lookup"><span data-stu-id="8318e-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="8318e-145">Informations</span><span class="sxs-lookup"><span data-stu-id="8318e-145">Informational</span></span> |<span data-ttu-id="8318e-146">Aucun</span><span class="sxs-lookup"><span data-stu-id="8318e-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="8318e-147">Gérer les alertes de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-147">Manage Backup alerts</span></span>
<span data-ttu-id="8318e-148">Cliquez sur la mosaïque **Alertes de sauvegarde** pour ouvrir le panneau **Alertes de sauvegarde** et gérer les alertes.</span><span class="sxs-lookup"><span data-stu-id="8318e-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Alertes de sauvegarde](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="8318e-150">La mosaïque Alertes de sauvegarde indique :</span><span class="sxs-lookup"><span data-stu-id="8318e-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="8318e-151">le nombre d’alertes critiques non résolues dans les 24 dernières heures</span><span class="sxs-lookup"><span data-stu-id="8318e-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="8318e-152">le nombre d’alertes d’avertissement non résolues dans les 24 dernières heures</span><span class="sxs-lookup"><span data-stu-id="8318e-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="8318e-153">Cliquez sur chacun de ces liens pour accéder au panneau **Alertes de sauvegarde** affichant une vue filtrée sur ces alertes (critiques ou d’avertissement).</span><span class="sxs-lookup"><span data-stu-id="8318e-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="8318e-154">Dans le panneau Alertes de sauvegarde, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="8318e-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="8318e-155">Choisir les informations appropriées à inclure dans vos alertes</span><span class="sxs-lookup"><span data-stu-id="8318e-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Choisir les colonnes](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="8318e-157">Filtrer les alertes selon leur gravité, leur état et les heures de début/fin</span><span class="sxs-lookup"><span data-stu-id="8318e-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="8318e-159">Configurer les paramètres de gravité, de fréquence et de destination des notifications, mais aussi activer ou désactiver les alertes</span><span class="sxs-lookup"><span data-stu-id="8318e-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="8318e-161">Si la fréquence de **notification** est définie sur **Par alerte**, le système ne procède à aucun regroupement ou réduction des e-mails.</span><span class="sxs-lookup"><span data-stu-id="8318e-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="8318e-162">Chaque alerte génère une notification.</span><span class="sxs-lookup"><span data-stu-id="8318e-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="8318e-163">Il s’agit du paramètre par défaut. Un e-mail de résolution accompagne chaque notification.</span><span class="sxs-lookup"><span data-stu-id="8318e-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="8318e-164">Si la fréquence de **notification** est définie sur **Synthèse horaire**, un e-mail est envoyé à l’utilisateur pour lui indiquer que de nouvelles alertes non résolues ont été générées au cours de la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="8318e-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="8318e-165">Un e-mail de résolution est envoyé à la fin de l’heure.</span><span class="sxs-lookup"><span data-stu-id="8318e-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="8318e-166">Des alertes peuvent être envoyées pour les niveaux de gravité suivants :</span><span class="sxs-lookup"><span data-stu-id="8318e-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="8318e-167">Critique</span><span class="sxs-lookup"><span data-stu-id="8318e-167">critical</span></span>
* <span data-ttu-id="8318e-168">Avertissement</span><span class="sxs-lookup"><span data-stu-id="8318e-168">warning</span></span>
* <span data-ttu-id="8318e-169">information</span><span class="sxs-lookup"><span data-stu-id="8318e-169">information</span></span>

<span data-ttu-id="8318e-170">Pour désactiver l’alerte, cliquez sur le bouton **Inactivate** (Désactiver) dans le panneau contenant les détails du travail.</span><span class="sxs-lookup"><span data-stu-id="8318e-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="8318e-171">Lorsque vous cliquez sur Inactivate (Désactiver), vous pouvez ajouter des commentaires pour la résolution de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="8318e-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="8318e-172">Pour choisir les colonnes que vous souhaitez voir apparaître dans l’alerte, cliquez sur le bouton **Choisir les colonnes** .</span><span class="sxs-lookup"><span data-stu-id="8318e-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="8318e-173">Dans le panneau **Paramètres**, vous pouvez gérer les alertes de sauvegarde en sélectionnant **Monitoring and Reports (Surveillance et rapports) > Alertes et événements > Alertes de sauvegarde**, puis en cliquant sur **Filtrer** ou **Configurer les notifications**.</span><span class="sxs-lookup"><span data-stu-id="8318e-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="8318e-174">Gérer les éléments de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-174">Manage Backup items</span></span>
<span data-ttu-id="8318e-175">Vous pouvez désormais gérer les sauvegardes locales depuis le portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="8318e-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="8318e-176">Dans la section Sauvegarde du tableau de bord, la mosaïque **Éléments de sauvegarde** affiche le nombre d’éléments de sauvegarde protégés dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="8318e-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="8318e-177">Dans la mosaïque Éléments de sauvegarde, cliquez sur **File-Folders** (Dossiers de fichiers).</span><span class="sxs-lookup"><span data-stu-id="8318e-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="8318e-179">Le panneau Éléments de sauvegarde s’ouvre avec le filtre défini sur File-Folders (Dossiers de fichiers) et affiche chaque élément de sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="8318e-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="8318e-181">Sélectionnez un élément de sauvegarde spécifique dans la liste pour en afficher les principaux détails.</span><span class="sxs-lookup"><span data-stu-id="8318e-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="8318e-182">Dans le panneau **Paramètres**, vous pouvez gérer les fichiers et dossiers en sélectionnant **Éléments protégés > Éléments de sauvegarde**, puis en sélectionnant **File-Folders** (Dossiers de fichiers) dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="8318e-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="8318e-184">Gérer les travaux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-184">Manage Backup jobs</span></span>
<span data-ttu-id="8318e-185">Les travaux de sauvegarde réalisés en local (lorsque le serveur local sauvegarde vers Azure) et dans Azure s’affichent dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="8318e-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="8318e-186">Dans la section Sauvegarde du tableau de bord, la mosaïque Travail de sauvegarde indique le nombre de travaux :</span><span class="sxs-lookup"><span data-stu-id="8318e-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="8318e-187">en cours</span><span class="sxs-lookup"><span data-stu-id="8318e-187">in progress</span></span>
* <span data-ttu-id="8318e-188">ayant échoué au cours des 24 dernières heures</span><span class="sxs-lookup"><span data-stu-id="8318e-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="8318e-189">Pour gérer vos travaux de sauvegarde, cliquez sur la mosaïque **Travaux de sauvegarde** pour ouvrir le panneau Travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="8318e-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="8318e-191">Cliquez sur le bouton **Choisir les colonnes** en haut de la page pour modifier les informations disponibles dans le panneau Travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="8318e-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="8318e-192">Utilisez le bouton **Filtrer** pour sélectionner les fichiers ou les dossiers, ainsi que la sauvegarde de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="8318e-193">Si vous ne voyez pas vos fichiers et dossiers sauvegardés, cliquez sur le bouton **Filtrer** en haut de la page et sélectionnez **Fichiers et dossiers** dans le menu Item Type (Type d’élément).</span><span class="sxs-lookup"><span data-stu-id="8318e-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="8318e-194">Dans le panneau **Paramètres**, vous pouvez gérer les travaux de sauvegarde en sélectionnant **Monitoring and Reports (Surveillance et rapports) > Travaux > Travaux de sauvegarde**, puis en sélectionnant **File-Folders** (Dossiers de fichiers) dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="8318e-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="8318e-195">Surveiller l’utilisation de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-195">Monitor Backup usage</span></span>
<span data-ttu-id="8318e-196">Dans la section Sauvegarde du tableau de bord, la mosaïque Backup Usage (Utilisation de la sauvegarde) indique le stockage consommé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="8318e-197">Les données d’utilisation du stockage incluent :</span><span class="sxs-lookup"><span data-stu-id="8318e-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="8318e-198">L’utilisation du stockage cloud LRS associée au coffre</span><span class="sxs-lookup"><span data-stu-id="8318e-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="8318e-199">L’utilisation du stockage cloud GRS associée au coffre</span><span class="sxs-lookup"><span data-stu-id="8318e-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="8318e-200">Gérer vos serveurs de production</span><span class="sxs-lookup"><span data-stu-id="8318e-200">Manage your production servers</span></span>
<span data-ttu-id="8318e-201">Pour gérer vos serveurs de production, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8318e-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="8318e-202">Sous Gérer, cliquez sur **Infrastructure de sauvegarde > Serveurs de Production**.</span><span class="sxs-lookup"><span data-stu-id="8318e-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="8318e-203">Le panneau Serveurs de Production affiche une liste de tous vos serveurs de production disponibles.</span><span class="sxs-lookup"><span data-stu-id="8318e-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="8318e-204">Cliquez sur un serveur dans la liste pour afficher les détails correspondants.</span><span class="sxs-lookup"><span data-stu-id="8318e-204">Click on a server in the list to open the server details.</span></span>

![Éléments protégés](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="8318e-206">Ouvrir l’agent Azure Backup</span><span class="sxs-lookup"><span data-stu-id="8318e-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="8318e-207">Ouvrez **l’agent Microsoft Azure Backup** (vous pouvez le trouver en recherchant *Microsoft Azure Backup*sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="8318e-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="8318e-209">Dans les **Actions** disponibles à droite de la console de l’agent de sauvegarde, vous pouvez effectuer les tâches de gestion suivantes :</span><span class="sxs-lookup"><span data-stu-id="8318e-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="8318e-210">Inscription du serveur</span><span class="sxs-lookup"><span data-stu-id="8318e-210">Register Server</span></span>
* <span data-ttu-id="8318e-211">Planification d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-211">Schedule Backup</span></span>
* <span data-ttu-id="8318e-212">Sauvegarder maintenant</span><span class="sxs-lookup"><span data-stu-id="8318e-212">Back Up now</span></span>
* <span data-ttu-id="8318e-213">Modifier les propriétés</span><span class="sxs-lookup"><span data-stu-id="8318e-213">Change Properties</span></span>

![Actions de la console de l’agent Microsoft Azure Backup.](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="8318e-215">Pour **Récupérer des données**, consultez [Restauration de fichiers sur un serveur Windows ou un ordinateur client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8318e-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="8318e-216">Modifier la planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="8318e-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="8318e-217">Dans l’agent Microsoft Azure Backup, cliquez sur **Planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="8318e-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="8318e-219">Dans **l’Assistant Planification de sauvegarde**, conservez l’option **Modifier les éléments ou les dates/heures de sauvegarde** sélectionnée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8318e-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="8318e-221">Si vous souhaitez ajouter ou modifier des éléments, cliquez sur **Ajouter des éléments** dans l’écran **Sélectionner les éléments à sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="8318e-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="8318e-222">Vous pouvez également définir les **Paramètres d’exclusion** sur cette page de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="8318e-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="8318e-223">Si vous souhaitez exclure des fichiers ou des types de fichiers, lisez la procédure permettant d’ajouter des [paramètres d’exclusion](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="8318e-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="8318e-224">Sélectionnez les fichiers et les dossiers que vous souhaitez sauvegarder, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8318e-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="8318e-226">Spécifiez la **planification de sauvegarde**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8318e-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="8318e-227">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="8318e-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="8318e-229">La définition de la planification de sauvegarde est décrite en détail dans cet [article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="8318e-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="8318e-230">Sélectionnez la **Stratégie de rétention** pour la copie de sauvegarde et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8318e-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="8318e-232">Dans l’écran **Confirmation**, passez en revue les informations, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="8318e-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="8318e-233">Dès que l’Assistant a terminé la création de la **planification de sauvegarde**, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="8318e-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="8318e-234">Après la modification de la protection, vous pouvez confirmer le déclenchement correct des sauvegardes en accédant à l’onglet **Travaux** et en vérifiant que les modifications sont répercutées dans les tâches de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="8318e-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="8318e-235">Activation de la limitation du réseau</span><span class="sxs-lookup"><span data-stu-id="8318e-235">Enable Network Throttling</span></span>

<span data-ttu-id="8318e-236">L’agent Azure Backup contient un onglet Limitation qui vous permet de contrôler l’utilisation de la bande passante réseau pendant le transfert de données.</span><span class="sxs-lookup"><span data-stu-id="8318e-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="8318e-237">Cela peut s’avérer utile si vous avez besoin de sauvegarder des données pendant les heures de travail, mais ne souhaitez pas que le processus de sauvegarde interfère avec le reste du trafic internet.</span><span class="sxs-lookup"><span data-stu-id="8318e-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="8318e-238">La limitation du transfert de données s’applique aux activités de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="8318e-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="8318e-239">Pour activer la limitation :</span><span class="sxs-lookup"><span data-stu-id="8318e-239">To enable throttling:</span></span>

1. <span data-ttu-id="8318e-240">Dans **l’agent de Sauvegarde**, cliquez sur **Modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8318e-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="8318e-241">Sous l’onglet **Limitation, sélectionnez la case **Activer la limitation de la bande passante sur Internet pour les opérations de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="8318e-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitation du réseau](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="8318e-243">Une fois que vous avez activé la limitation, spécifiez la bande passante autorisée pour le transfert des données de sauvegarde durant les **Heures de travail** et les **Heures chômées**.</span><span class="sxs-lookup"><span data-stu-id="8318e-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="8318e-244">Les valeurs de bande passante, qui démarrent à 512 kilo-octets par seconde, peuvent aller jusqu’à 1 023 mégaoctets par seconde.</span><span class="sxs-lookup"><span data-stu-id="8318e-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="8318e-245">Vous pouvez également définir le début et la fin des **Heures de travail**et identifier les jours de la semaine considérés comme des jours de travail.</span><span class="sxs-lookup"><span data-stu-id="8318e-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="8318e-246">Les intervalles de temps situés en dehors des heures de travail sont considérés comme des périodes (heures) chômées.</span><span class="sxs-lookup"><span data-stu-id="8318e-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="8318e-247">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8318e-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="8318e-248">Gérer les paramètres d’exclusion</span><span class="sxs-lookup"><span data-stu-id="8318e-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="8318e-249">Ouvrez **l’agent Microsoft Azure Backup** (vous pouvez le trouver en recherchant *Microsoft Azure Backup*sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="8318e-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="8318e-251">Dans l’agent Microsoft Azure Backup, cliquez sur **Planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="8318e-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="8318e-253">Dans l’Assistant Planification de sauvegarde, conservez l’option **Modifier les éléments ou les dates/heures de sauvegarde** sélectionnée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8318e-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="8318e-255">Cliquez sur **Paramètres d’exclusion**.</span><span class="sxs-lookup"><span data-stu-id="8318e-255">Click **Exclusions Settings**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="8318e-257">Cliquez sur **Ajouter une exclusion**.</span><span class="sxs-lookup"><span data-stu-id="8318e-257">Click **Add Exclusion**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="8318e-259">Sélectionnez l’emplacement, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8318e-259">Select the location and then, click **OK**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="8318e-261">Ajoutez l’extension de fichier dans le champ **Type de fichier** .</span><span class="sxs-lookup"><span data-stu-id="8318e-261">Add the file extension in the **File Type** field.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="8318e-263">Ajout d’une extension .mp3</span><span class="sxs-lookup"><span data-stu-id="8318e-263">Adding an .mp3 extension</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="8318e-265">Pour ajouter une autre extension, cliquez sur **Ajouter une exclusion** et entrez une autre extension de type de fichier (ajout d’une extension .jpeg).</span><span class="sxs-lookup"><span data-stu-id="8318e-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="8318e-267">Lorsque vous avez ajouté toutes les extensions, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8318e-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="8318e-268">Suivez les instructions de l’Assistant Planification de sauvegarde en cliquant sur **Suivant** jusqu’à la **page de Confirmation**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="8318e-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="8318e-270">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="8318e-270">Frequently asked questions</span></span>
<span data-ttu-id="8318e-271">**Q1. Le travail de sauvegarde est indiqué comme terminé dans l’agent de sauvegarde Azure, pourquoi cela ne s’affiche pas immédiatement dans le portail ?**</span><span class="sxs-lookup"><span data-stu-id="8318e-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="8318e-272">R1.</span><span class="sxs-lookup"><span data-stu-id="8318e-272">A1.</span></span> <span data-ttu-id="8318e-273">Un délai maximal de 15 minutes est nécessaire pour que l’état du travail de sauvegarde dans l’agent de sauvegarde Azure soit répercuté dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="8318e-274">**Q2. En cas d’échec d’un travail de sauvegarde, combien de temps faut-il pour déclencher une alerte ?**</span><span class="sxs-lookup"><span data-stu-id="8318e-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="8318e-275">R2. Une alerte est générée dans les 20 minutes suivant l’échec de la sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="8318e-276">**Q3. Est-il possible qu’aucun e-mail ne soit envoyé alors que les notifications sont activées ?**</span><span class="sxs-lookup"><span data-stu-id="8318e-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="8318e-277">R3</span><span class="sxs-lookup"><span data-stu-id="8318e-277">A3.</span></span> <span data-ttu-id="8318e-278">Voici les cas pour lesquels la notification ne sera pas envoyée afin de réduire le bruit des alertes :</span><span class="sxs-lookup"><span data-stu-id="8318e-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="8318e-279">Si les notifications sont configurées sur une base horaire et qu’une alerte est déclenchée et résolue dans l’heure.</span><span class="sxs-lookup"><span data-stu-id="8318e-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="8318e-280">Si le travail est annulé.</span><span class="sxs-lookup"><span data-stu-id="8318e-280">Job is canceled.</span></span>
* <span data-ttu-id="8318e-281">Si le travail de sauvegarde secondaire a échoué, car un travail de sauvegarde d’origine est en cours.</span><span class="sxs-lookup"><span data-stu-id="8318e-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="8318e-282">Résolution des problèmes de surveillance</span><span class="sxs-lookup"><span data-stu-id="8318e-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="8318e-283">**Problème :** les travaux et/ou les alertes de l’agent de sauvegarde Azure n’apparaissent pas sur le portail.</span><span class="sxs-lookup"><span data-stu-id="8318e-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="8318e-284">**Étapes de dépannage :** le processus ```OBRecoveryServicesManagementAgent``` envoie les données relatives à l’alerte et au travail au service de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="8318e-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="8318e-285">Il peut arriver que ce processus se bloque ou s’arrête.</span><span class="sxs-lookup"><span data-stu-id="8318e-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="8318e-286">Pour vérifier que le processus n’est pas en cours d’exécution, ouvrez **Gestionnaire des tâches** et vérifiez si le processus ```OBRecoveryServicesManagementAgent``` est en cours.</span><span class="sxs-lookup"><span data-stu-id="8318e-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="8318e-287">En supposant que le processus ne fonctionne pas, ouvrez le **Panneau de configuration** et parcourez la liste des services.</span><span class="sxs-lookup"><span data-stu-id="8318e-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="8318e-288">Démarrez ou redémarrez l’**Agent de gestion Microsoft Azure Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="8318e-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="8318e-289">Pour plus d’informations, consultez les journaux à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="8318e-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="8318e-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8318e-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="8318e-291">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8318e-291">Next steps</span></span>
* [<span data-ttu-id="8318e-292">Restaurer un serveur Windows Server ou un client Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="8318e-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="8318e-293">Pour en savoir plus sur Azure Backup, consultez la [vue d’ensemble d’Azure Backup](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="8318e-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="8318e-294">Consultez le [forum Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="8318e-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
