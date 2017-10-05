---
title: "Gérer les serveurs et les coffres Azure Backup à l’aide du modèle de déploiement classique | Microsoft Docs"
description: "Ce didacticiel vous apprend à gérer les serveurs et les coffres Azure Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="e8ede-103">Gérer les serveurs et les coffres Azure Backup à l’aide du modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="e8ede-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8ede-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e8ede-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="e8ede-105">Classique</span><span class="sxs-lookup"><span data-stu-id="e8ede-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="e8ede-106">Cet article offre une vue d’ensemble des tâches de gestion des sauvegardes disponibles via le portail Azure Classic et l’agent Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e8ede-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8ede-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e8ede-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e8ede-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="e8ede-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e8ede-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e8ede-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8ede-110">Vous pouvez désormais mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e8ede-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="e8ede-111">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="e8ede-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="e8ede-112">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e8ede-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="e8ede-113">À compter du 15 octobre 2017, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e8ede-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="e8ede-114">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="e8ede-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="e8ede-115">tous les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e8ede-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="e8ede-116">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="e8ede-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="e8ede-117">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="e8ede-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="e8ede-118">Tâches du portail de gestion</span><span class="sxs-lookup"><span data-stu-id="e8ede-118">Management portal tasks</span></span>
1. <span data-ttu-id="e8ede-119">Connectez-vous au [portail de gestion](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e8ede-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e8ede-120">Cliquez sur **Recovery Services**, puis sur le nom du coffre de sauvegarde pour afficher la page de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="e8ede-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Recovery Services](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="e8ede-122">Sélectionnez les options situées en haut de la page de démarrage rapide pour afficher les tâches de gestion disponibles.</span><span class="sxs-lookup"><span data-stu-id="e8ede-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Gérer les onglets](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="e8ede-124">Tableau de bord</span><span class="sxs-lookup"><span data-stu-id="e8ede-124">Dashboard</span></span>
<span data-ttu-id="e8ede-125">Sélectionnez **Tableau de bord** pour afficher l’aperçu de l’utilisation du serveur.</span><span class="sxs-lookup"><span data-stu-id="e8ede-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="e8ede-126">La **vue d’ensemble de l’utilisation** inclut :</span><span class="sxs-lookup"><span data-stu-id="e8ede-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="e8ede-127">Le nombre de serveurs Windows inscrits auprès du cloud</span><span class="sxs-lookup"><span data-stu-id="e8ede-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="e8ede-128">Le nombre de machines virtuelles Azure protégées dans le cloud</span><span class="sxs-lookup"><span data-stu-id="e8ede-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="e8ede-129">Le stockage total consommé dans Azure</span><span class="sxs-lookup"><span data-stu-id="e8ede-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="e8ede-130">L’état des travaux récents</span><span class="sxs-lookup"><span data-stu-id="e8ede-130">The status of recent jobs</span></span>

<span data-ttu-id="e8ede-131">En bas du tableau de bord, vous pouvez réaliser les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8ede-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="e8ede-132">**Gérer un certificat** : si un certificat a été utilisé pour enregistrer le serveur, utilisez cette tâche pour mettre à jour le certificat.</span><span class="sxs-lookup"><span data-stu-id="e8ede-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="e8ede-133">Si vous utilisez des informations d'identification de coffre, n'utilisiez pas **Manage certificate**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="e8ede-134">**Supprimer** : permet de supprimer le coffre de sauvegarde actuel.</span><span class="sxs-lookup"><span data-stu-id="e8ede-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="e8ede-135">Si un coffre de sauvegarde n'est plus utilisé, vous pouvez le supprimer pour libérer de l'espace de stockage.</span><span class="sxs-lookup"><span data-stu-id="e8ede-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="e8ede-136">**Supprimer** est disponible uniquement une fois que tous les serveurs inscrits ont été supprimés du coffre.</span><span class="sxs-lookup"><span data-stu-id="e8ede-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="e8ede-138">Éléments inscrits</span><span class="sxs-lookup"><span data-stu-id="e8ede-138">Registered items</span></span>
<span data-ttu-id="e8ede-139">Sélectionnez **Éléments inscrits** pour afficher le nom des serveurs inscrits auprès de ce coffre.</span><span class="sxs-lookup"><span data-stu-id="e8ede-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="e8ede-141">Le filtre **Type** permet de filtrer les valeurs par défaut sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ede-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="e8ede-142">Sélectionnez **Windows Server** dans le menu déroulant pour afficher le nom des serveurs inscrits auprès de ce coffre.</span><span class="sxs-lookup"><span data-stu-id="e8ede-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="e8ede-143">Exécutez ensuite les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8ede-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="e8ede-144">**Autoriser la réinscription** : quand cette option est sélectionnée pour un serveur, vous pouvez utiliser **l’Assistant Inscription** dans l’agent de Sauvegarde Microsoft Azure local pour inscrire à nouveau le serveur auprès du coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e8ede-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="e8ede-145">Vous devrez peut-être effectuer cette nouvelle inscription en raison d'une erreur dans le certificat ou de la nécessité de régénérer un serveur.</span><span class="sxs-lookup"><span data-stu-id="e8ede-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="e8ede-146">**Supprimer** : permet de supprimer un serveur du coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e8ede-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="e8ede-147">Toutes les données stockées associées au serveur sont immédiatement supprimées.</span><span class="sxs-lookup"><span data-stu-id="e8ede-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Tâches d’éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="e8ede-149">Éléments protégés</span><span class="sxs-lookup"><span data-stu-id="e8ede-149">Protected items</span></span>
<span data-ttu-id="e8ede-150">Sélectionnez **Éléments protégés** pour afficher les éléments sauvegardés à partir des serveurs.</span><span class="sxs-lookup"><span data-stu-id="e8ede-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Éléments protégés](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="e8ede-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="e8ede-152">Configure</span></span>
<span data-ttu-id="e8ede-153">Dans l’onglet **Configurer** , vous pouvez sélectionner l’option de redondance de stockage appropriée.</span><span class="sxs-lookup"><span data-stu-id="e8ede-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="e8ede-154">Nous vous recommandons de sélectionner l’option de redondance de stockage juste après avoir créé un coffre et avant d’y inscrire des ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="e8ede-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="e8ede-155">Une fois qu’un élément a été inscrit dans l’archivage, l’option de redondance de stockage est verrouillée et ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="e8ede-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configuration](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="e8ede-157">Consultez cet article pour plus d’informations sur la [redondance du stockage](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="e8ede-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="e8ede-158">Tâches de l’agent Microsoft Azure Backup</span><span class="sxs-lookup"><span data-stu-id="e8ede-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="e8ede-159">Console</span><span class="sxs-lookup"><span data-stu-id="e8ede-159">Console</span></span>
<span data-ttu-id="e8ede-160">Ouvrez l’ **agent Microsoft Azure Backup** (vous pouvez le trouver en recherchant *Microsoft Azure Backup*sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="e8ede-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="e8ede-162">Dans les **Actions** disponibles à droite de la console de l’agent de sauvegarde, vous pouvez effectuer les tâches de gestion suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8ede-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="e8ede-163">Inscription du serveur</span><span class="sxs-lookup"><span data-stu-id="e8ede-163">Register Server</span></span>
* <span data-ttu-id="e8ede-164">Planification d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e8ede-164">Schedule Backup</span></span>
* <span data-ttu-id="e8ede-165">Sauvegarder maintenant</span><span class="sxs-lookup"><span data-stu-id="e8ede-165">Back Up now</span></span>
* <span data-ttu-id="e8ede-166">Modifier les propriétés</span><span class="sxs-lookup"><span data-stu-id="e8ede-166">Change Properties</span></span>

![Actions de la console de l’agent](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="e8ede-168">Pour **Récupérer des données**, consultez [Restauration de fichiers sur un serveur Windows ou un ordinateur client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="e8ede-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="e8ede-169">Modifier une sauvegarde existante</span><span class="sxs-lookup"><span data-stu-id="e8ede-169">Modify an existing backup</span></span>
1. <span data-ttu-id="e8ede-170">Dans l’agent Microsoft Azure Backup, cliquez sur **Planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="e8ede-172">Dans **l’Assistant Planification de sauvegarde**, conservez l’option **Modifier les éléments ou les dates/heures de sauvegarde** sélectionnée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modifier une sauvegarde planifiée](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="e8ede-174">Si vous souhaitez ajouter ou modifier des éléments, cliquez sur **Ajouter des éléments** dans l’écran **Sélectionner les éléments à sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="e8ede-175">Vous pouvez également définir les **Paramètres d’exclusion** sur cette page de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="e8ede-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="e8ede-176">Si vous souhaitez exclure des fichiers ou des types de fichiers, lisez la procédure permettant d’ajouter des [paramètres d’exclusion](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="e8ede-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="e8ede-177">Sélectionnez les fichiers et les dossiers que vous souhaitez sauvegarder, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Sélectionner les éléments à sauvegarder](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="e8ede-179">Spécifiez la **planification de sauvegarde**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="e8ede-180">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="e8ede-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Spécifier votre planification de sauvegarde](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="e8ede-182">La définition de la planification de sauvegarde est décrite en détail dans cet [article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="e8ede-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="e8ede-183">Sélectionnez la **Stratégie de rétention** pour la copie de sauvegarde et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Sélectionner votre stratégie de rétention](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="e8ede-185">Dans l’écran **Confirmation**, passez en revue les informations, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="e8ede-186">Dès que l’Assistant a terminé la création de la **planification de sauvegarde**, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="e8ede-187">Après la modification de la protection, vous pouvez confirmer le déclenchement correct des sauvegardes en accédant à l’onglet **Travaux** et en vérifiant que les modifications sont répercutées dans les tâches de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e8ede-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="e8ede-188">Activation de la limitation du réseau</span><span class="sxs-lookup"><span data-stu-id="e8ede-188">Enable Network Throttling</span></span>
<span data-ttu-id="e8ede-189">L’agent Azure Backup contient un onglet Limitation qui vous permet de contrôler l’utilisation de la bande passante réseau pendant le transfert de données.</span><span class="sxs-lookup"><span data-stu-id="e8ede-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="e8ede-190">Cela peut s’avérer utile si vous avez besoin de sauvegarder des données pendant les heures de travail, mais ne souhaitez pas que le processus de sauvegarde interfère avec le reste du trafic internet.</span><span class="sxs-lookup"><span data-stu-id="e8ede-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="e8ede-191">La limitation du transfert de données s’applique aux activités de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="e8ede-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="e8ede-192">Pour activer la limitation :</span><span class="sxs-lookup"><span data-stu-id="e8ede-192">To enable throttling:</span></span>

1. <span data-ttu-id="e8ede-193">Dans **l’agent de Sauvegarde**, cliquez sur **Modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="e8ede-194">Cochez la case **Activer la limitation de la bande passante sur Internet pour les opérations de sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="e8ede-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitation du réseau](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="e8ede-196">Une fois que vous avez activé la limitation, spécifiez la bande passante autorisée pour le transfert des données de sauvegarde durant les **Heures de travail** et les **Heures chômées**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="e8ede-197">Les valeurs de bande passante, qui démarrent à 512 kilo-octets par seconde, peuvent aller jusqu’à 1 023 mégaoctets par seconde.</span><span class="sxs-lookup"><span data-stu-id="e8ede-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="e8ede-198">Vous pouvez également définir le début et la fin des **Heures de travail**et identifier les jours de la semaine considérés comme des jours de travail.</span><span class="sxs-lookup"><span data-stu-id="e8ede-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="e8ede-199">Les intervalles de temps situés en dehors des heures de travail sont considérés comme des périodes (heures) chômées.</span><span class="sxs-lookup"><span data-stu-id="e8ede-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="e8ede-200">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="e8ede-201">Paramètres d’exclusion</span><span class="sxs-lookup"><span data-stu-id="e8ede-201">Exclusion settings</span></span>
1. <span data-ttu-id="e8ede-202">Ouvrez l’ **agent Microsoft Azure Backup** (vous pouvez le trouver en recherchant *Microsoft Azure Backup*sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="e8ede-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Ouvrir l’agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="e8ede-204">Dans l’agent Microsoft Azure Backup, cliquez sur **Planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="e8ede-206">Dans l’Assistant Planification de sauvegarde, conservez l’option **Modifier les éléments ou les dates/heures de sauvegarde** sélectionnée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modifier une planification](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="e8ede-208">Cliquez sur **Paramètres d’exclusion**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-208">Click **Exclusions Settings**.</span></span>

    ![Sélectionner des éléments à exclure](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="e8ede-210">Cliquez sur **Ajouter une exclusion**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-210">Click **Add Exclusion**.</span></span>

    ![Ajouter des exclusions](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="e8ede-212">Sélectionnez l’emplacement, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-212">Select the location and then, click **OK**.</span></span>

    ![Sélectionnez un emplacement pour l’exclusion](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="e8ede-214">Ajoutez l’extension de fichier dans le champ **Type de fichier** .</span><span class="sxs-lookup"><span data-stu-id="e8ede-214">Add the file extension in the **File Type** field.</span></span>

    ![Exclure par type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="e8ede-216">Ajout d’une extension .mp3</span><span class="sxs-lookup"><span data-stu-id="e8ede-216">Adding an .mp3 extension</span></span>

    ![Exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="e8ede-218">Pour ajouter une autre extension, cliquez sur **Ajouter une exclusion** et entrez une autre extension de type de fichier (ajout d’une extension .jpeg).</span><span class="sxs-lookup"><span data-stu-id="e8ede-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Autre exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="e8ede-220">Lorsque vous avez ajouté toutes les extensions, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="e8ede-221">Suivez les instructions de l’Assistant Planification de sauvegarde en cliquant sur **Suivant** jusqu’à la **page de Confirmation**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e8ede-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmation de l’exclusion](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="e8ede-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8ede-223">Next steps</span></span>
* [<span data-ttu-id="e8ede-224">Restaurer un serveur Windows Server ou un client Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="e8ede-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="e8ede-225">Pour en savoir plus sur Azure Backup, consultez la [vue d’ensemble d’Azure Backup](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="e8ede-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="e8ede-226">Consultez le [forum Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="e8ede-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
