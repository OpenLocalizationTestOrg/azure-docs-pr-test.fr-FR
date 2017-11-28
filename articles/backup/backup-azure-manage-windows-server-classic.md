---
title: "les coffres de sauvegarde Azure aaaManage et serveurs Azure en utilisant le modèle de déploiement classique hello | Documents Microsoft"
description: Utilisez ce didacticiel toolearn comment les coffres toomanage Azure Backup et les serveurs.
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
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="39720-103">Gérer les coffres de sauvegarde Azure et les serveurs à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="39720-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39720-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="39720-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="39720-105">Classique</span><span class="sxs-lookup"><span data-stu-id="39720-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="39720-106">Dans cet article, vous trouverez une vue d’ensemble des tâches de gestion de sauvegarde hello disponibles via le portail Azure classic de hello et l’agent Microsoft Azure Backup de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39720-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="39720-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39720-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="39720-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="39720-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="39720-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39720-110">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="39720-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="39720-111">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="39720-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="39720-112">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39720-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="39720-113">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39720-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="39720-114">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="39720-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="39720-115">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="39720-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="39720-116">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="39720-117">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="39720-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="39720-118">Tâches du portail de gestion</span><span class="sxs-lookup"><span data-stu-id="39720-118">Management portal tasks</span></span>
1. <span data-ttu-id="39720-119">Connectez-vous à toohello [portail de gestion](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="39720-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="39720-120">Cliquez sur **Services de récupération**, puis cliquez sur nom hello de page de démarrage rapide de coffre de sauvegarde tooview hello.</span><span class="sxs-lookup"><span data-stu-id="39720-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Recovery Services](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="39720-122">En sélectionnant les options de hello en hello haut hello démarrage rapide, vous pouvez voir les tâches de gestion disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="39720-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Gérer les onglets](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="39720-124">tableau de bord</span><span class="sxs-lookup"><span data-stu-id="39720-124">Dashboard</span></span>
<span data-ttu-id="39720-125">Sélectionnez **tableau de bord** présentation de l’utilisation de hello toosee pour le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="39720-126">Hello **présentation de l’utilisation** inclut :</span><span class="sxs-lookup"><span data-stu-id="39720-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="39720-127">nombre de Hello des serveurs Windows inscrits toocloud</span><span class="sxs-lookup"><span data-stu-id="39720-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="39720-128">nombre de Hello de machines virtuelles protégées dans le cloud</span><span class="sxs-lookup"><span data-stu-id="39720-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="39720-129">stockage total de Hello consommé dans Azure</span><span class="sxs-lookup"><span data-stu-id="39720-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="39720-130">état Hello des tâches récentes</span><span class="sxs-lookup"><span data-stu-id="39720-130">hello status of recent jobs</span></span>

<span data-ttu-id="39720-131">En bas de hello Hello du tableau de bord, vous pouvez effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="39720-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="39720-132">**Gérer le certificat** - si un certificat était utilisé tooregister hello serveur, puis utiliser ce certificat de hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="39720-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="39720-133">Si vous utilisez des informations d'identification de coffre, n'utilisiez pas **Manage certificate**.</span><span class="sxs-lookup"><span data-stu-id="39720-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="39720-134">**Supprimer** -coffre de sauvegarde en cours de suppressions hello.</span><span class="sxs-lookup"><span data-stu-id="39720-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="39720-135">Si un coffre de sauvegarde est n’est plus utilisé, vous pouvez le supprimer toofree l’espace de stockage.</span><span class="sxs-lookup"><span data-stu-id="39720-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="39720-136">**Supprimer** est activé uniquement après la suppression de tous les serveurs inscrits dans le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="39720-138">Éléments inscrits</span><span class="sxs-lookup"><span data-stu-id="39720-138">Registered items</span></span>
<span data-ttu-id="39720-139">Sélectionnez **éléments inscrits** tooview les noms de hello des serveurs hello sont inscrits toothis coffre.</span><span class="sxs-lookup"><span data-stu-id="39720-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="39720-141">Hello **Type** filtre par défaut est tooAzure Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39720-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="39720-142">les noms de hello tooview des serveurs hello toothis inscrits coffre, **Windows server** de hello menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="39720-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="39720-143">À ce stade, vous pouvez effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="39720-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="39720-144">**Autoriser la réinscription** - lorsque cette option est sélectionnée pour un serveur, vous pouvez utiliser hello **Assistant Inscription** dans hello Microsoft Azure Backup agent tooregister hello serveur local avec le coffre de sauvegarde hello une deuxième fois. .</span><span class="sxs-lookup"><span data-stu-id="39720-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="39720-145">Vous devrez peut-être toore dans le Registre en raison de l’erreur tooan dans le certificat de hello ou si un serveur a rencontré toobe reconstruit.</span><span class="sxs-lookup"><span data-stu-id="39720-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="39720-146">**Supprimer** -supprime un serveur d’archivage de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="39720-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="39720-147">Toutes les données stockée hello associées avec le serveur de hello est supprimé immédiatement.</span><span class="sxs-lookup"><span data-stu-id="39720-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Tâches d’éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="39720-149">Éléments protégés</span><span class="sxs-lookup"><span data-stu-id="39720-149">Protected items</span></span>
<span data-ttu-id="39720-150">Sélectionnez **éléments protégés** éléments hello tooview qui ont été sauvegardées à partir de serveurs de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Éléments protégés](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="39720-152">Configuration</span><span class="sxs-lookup"><span data-stu-id="39720-152">Configure</span></span>
<span data-ttu-id="39720-153">À partir de hello **configurer** onglet, vous pouvez sélectionner option de redondance de stockage approprié hello.</span><span class="sxs-lookup"><span data-stu-id="39720-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="39720-154">Hello meilleur temps tooselect hello option redondance du stockage est juste après la création d’un coffre et avant tous les ordinateurs sont inscrit tooit.</span><span class="sxs-lookup"><span data-stu-id="39720-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="39720-155">Une fois qu’un élément a été inscrit toohello coffre, option de redondance du stockage hello est verrouillée et ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="39720-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configuration](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="39720-157">Consultez cet article pour plus d’informations sur la [redondance du stockage](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="39720-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="39720-158">Tâches de l’agent Microsoft Azure Backup</span><span class="sxs-lookup"><span data-stu-id="39720-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="39720-159">Console</span><span class="sxs-lookup"><span data-stu-id="39720-159">Console</span></span>
<span data-ttu-id="39720-160">Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="39720-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="39720-162">À partir de hello **Actions** disponible à l’adresse hello à droite de la console de l’agent de sauvegarde hello effectuer hello les tâches de gestion suivantes :</span><span class="sxs-lookup"><span data-stu-id="39720-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="39720-163">Inscription du serveur</span><span class="sxs-lookup"><span data-stu-id="39720-163">Register Server</span></span>
* <span data-ttu-id="39720-164">Planification d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="39720-164">Schedule Backup</span></span>
* <span data-ttu-id="39720-165">Sauvegarder maintenant</span><span class="sxs-lookup"><span data-stu-id="39720-165">Back Up now</span></span>
* <span data-ttu-id="39720-166">Modifier les propriétés</span><span class="sxs-lookup"><span data-stu-id="39720-166">Change Properties</span></span>

![Actions de la console de l’agent](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="39720-168">trop**récupérer les données**, consultez [restaurer des fichiers tooa Windows server ou la machine du client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="39720-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="39720-169">Modifier une sauvegarde existante</span><span class="sxs-lookup"><span data-stu-id="39720-169">Modify an existing backup</span></span>
1. <span data-ttu-id="39720-170">Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="39720-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="39720-172">Bonjour **Assistant Planification de sauvegarde** laisser hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39720-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modifier une sauvegarde planifiée](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="39720-174">Si vous souhaitez tooadd ou de modifier les éléments sur hello **tooBackup de sélectionner les éléments** écran, cliquez sur **ajouter les éléments**.</span><span class="sxs-lookup"><span data-stu-id="39720-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="39720-175">Vous pouvez également définir **paramètres d’Exclusion** à partir de cette page dans l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="39720-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="39720-176">Si vous souhaitez que les fichiers tooexclude ou procédure hello pour l’ajout de lecture de types de fichiers [paramètres d’exclusion](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="39720-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="39720-177">Sélectionnez les fichiers de hello et les dossiers que vous souhaitez tooback haut et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="39720-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Sélectionner les éléments à sauvegarder](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="39720-179">Spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39720-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="39720-180">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="39720-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Spécifier votre planification de sauvegarde](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="39720-182">Spécifier la planification de sauvegarde hello est expliquée en détail dans ce [article](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="39720-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="39720-183">Sélectionnez hello **stratégie de rétention** pour la copie de sauvegarde hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39720-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Sélectionner votre stratégie de rétention](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="39720-185">Sur hello **Confirmation** hello consulter les informations de l’écran, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="39720-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="39720-186">Une fois l’Assistant de hello termine la création de hello **planification de sauvegarde**, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="39720-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="39720-187">Après la modification de protection, vous pouvez vérifier le déclenchement de sauvegardes par toohello de va **travaux** onglet et en s’assurant que les modifications sont répercutées dans hello des travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39720-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="39720-188">Activation de la limitation du réseau</span><span class="sxs-lookup"><span data-stu-id="39720-188">Enable Network Throttling</span></span>
<span data-ttu-id="39720-189">agent de sauvegarde Azure Hello comprend un onglet de limitation qui vous permet de toocontrol utilisation de la bande passante réseau lors du transfert de données.</span><span class="sxs-lookup"><span data-stu-id="39720-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="39720-190">Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic internet.</span><span class="sxs-lookup"><span data-stu-id="39720-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="39720-191">La limitation des données de transfert s’applique tooback des activités et de restauration.</span><span class="sxs-lookup"><span data-stu-id="39720-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="39720-192">tooenable de limitation :</span><span class="sxs-lookup"><span data-stu-id="39720-192">tooenable throttling:</span></span>

1. <span data-ttu-id="39720-193">Bonjour **agent de sauvegarde**, cliquez sur **modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="39720-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="39720-194">Sélectionnez hello **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="39720-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitation du réseau](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="39720-196">Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.</span><span class="sxs-lookup"><span data-stu-id="39720-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="39720-197">valeurs de la bande passante Hello commencent à 512 kilo-octets par seconde (Kbits/s) et peuvent atteindre la too1023 les mégaoctets par seconde (Mbits/s).</span><span class="sxs-lookup"><span data-stu-id="39720-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="39720-198">Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont considérés comme travail jours.</span><span class="sxs-lookup"><span data-stu-id="39720-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="39720-199">temps de Hello en dehors de hello désigné des heures de travail est toobe pris en compte les heures chômées.</span><span class="sxs-lookup"><span data-stu-id="39720-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="39720-200">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="39720-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="39720-201">Paramètres d’exclusion</span><span class="sxs-lookup"><span data-stu-id="39720-201">Exclusion settings</span></span>
1. <span data-ttu-id="39720-202">Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="39720-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Ouvrir l’agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="39720-204">Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="39720-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="39720-206">Bonjour Assistant Planification de sauvegarde, laissez hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39720-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modifier une planification](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="39720-208">Cliquez sur **Paramètres d’exclusion**.</span><span class="sxs-lookup"><span data-stu-id="39720-208">Click **Exclusions Settings**.</span></span>

    ![Sélectionner des éléments tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="39720-210">Cliquez sur **Ajouter une exclusion**.</span><span class="sxs-lookup"><span data-stu-id="39720-210">Click **Add Exclusion**.</span></span>

    ![Ajouter des exclusions](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="39720-212">Sélectionnez l’emplacement de hello et cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="39720-212">Select hello location and then, click **OK**.</span></span>

    ![Sélectionnez un emplacement pour l’exclusion](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="39720-214">Extension de fichier hello Bonjour **Type de fichier** champ.</span><span class="sxs-lookup"><span data-stu-id="39720-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Exclure par type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="39720-216">Ajout d’une extension .mp3</span><span class="sxs-lookup"><span data-stu-id="39720-216">Adding an .mp3 extension</span></span>

    ![Exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="39720-218">tooadd une autre extension, cliquez sur **ajouter une Exclusion** et entrez une autre extension de fichier (l’ajout d’une extension .jpeg).</span><span class="sxs-lookup"><span data-stu-id="39720-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Autre exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="39720-220">Lorsque vous avez ajouté toutes les extensions de hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="39720-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="39720-221">Poursuivez hello Assistant Planification de sauvegarde en cliquant sur **suivant** jusqu'à hello **page de Confirmation**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="39720-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Confirmation de l’exclusion](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="39720-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39720-223">Next steps</span></span>
* [<span data-ttu-id="39720-224">Restaurer un serveur Windows Server ou un client Windows à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="39720-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="39720-225">toolearn en savoir plus sur Azure Backup, consultez [vue d’ensemble de la sauvegarde Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="39720-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="39720-226">Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="39720-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
