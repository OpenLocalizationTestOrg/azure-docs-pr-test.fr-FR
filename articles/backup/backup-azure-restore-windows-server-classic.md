---
title: "aaaRestore données tooa Windows Server ou Client Windows à partir d’Azure à l’aide hello modèle de déploiement classique | Documents Microsoft"
description: "Découvrez comment toorestore à partir de Windows Server ou Windows Client."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="3906b-103">Restaurer des fichiers tooa Windows server ou la machine du client Windows à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="3906b-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3906b-104">Portail classique</span><span class="sxs-lookup"><span data-stu-id="3906b-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="3906b-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3906b-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="3906b-106">Cet article explique comment les données de toorecover à partir d’une sauvegarde de coffre et restaurer tooa serveur ou l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3906b-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="3906b-107">À partir de mars 2017, vous pouvez créer n’est plus des coffres de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3906b-108">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="3906b-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="3906b-109">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="3906b-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="3906b-110">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="3906b-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="3906b-111">**Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3906b-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="3906b-112">**À compter du 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="3906b-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="3906b-113">Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="3906b-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="3906b-114">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="3906b-115">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="3906b-116">toorestore des données, vous utilisez hello récupérer les données Assistant agent de Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="3906b-117">Lorsque vous restaurez des données, il est possible de :</span><span class="sxs-lookup"><span data-stu-id="3906b-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="3906b-118">Restauration de données toohello est identique à l’ordinateur à partir de laquelle les sauvegardes hello ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="3906b-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="3906b-119">Restaurer un ordinateur autre tooan de données.</span><span class="sxs-lookup"><span data-stu-id="3906b-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="3906b-120">En janvier 2017, Microsoft a publié un agent de MARS toohello aperçu mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3906b-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="3906b-121">Ainsi que des correctifs de bogues, cette mise à jour Active la restauration instantanée, ce qui vous permet de toomount un instantané de point de récupération accessible en écriture comme un volume de reprise.</span><span class="sxs-lookup"><span data-stu-id="3906b-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="3906b-122">Vous pouvez ensuite Explorer hello récupération volume et copie les fichiers tooa ordinateur local ainsi sélectivement restauration de fichiers.</span><span class="sxs-lookup"><span data-stu-id="3906b-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="3906b-123">Hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) est requis si vous voulez toouse restauration instantanée toorestore données.</span><span class="sxs-lookup"><span data-stu-id="3906b-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="3906b-124">Les données de sauvegarde hello doivent également être protégées dans des coffres dans les paramètres régionaux répertoriés dans l’article du support technique hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="3906b-125">Consultez hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) pour hello dernière liste des paramètres régionaux qui prennent en charge la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="3906b-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="3906b-126">La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.</span><span class="sxs-lookup"><span data-stu-id="3906b-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="3906b-127">Restauration instantanée est disponible pour utilisation dans les Services de récupération des coffres Bonjour portail Azure et les coffres de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="3906b-128">Si vous souhaitez toouse restauration instantanée, téléchargez la mise à jour de MARS hello et suivez les procédures de hello mentionnant restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="3906b-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="3906b-129">Utiliser la restauration instantanée toohello de données toorecover même ordinateur</span><span class="sxs-lookup"><span data-stu-id="3906b-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="3906b-130">Si vous avez supprimé accidentellement une toorestore de fichier et qui souhaitent il toohello étapes de la même machine (à partir de quels hello est la sauvegarde), hello suivant vous permettra de récupérer les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="3906b-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="3906b-131">Ouvrez hello **Microsoft Azure Backup** snap dans.</span><span class="sxs-lookup"><span data-stu-id="3906b-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="3906b-132">Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="3906b-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="3906b-133">application de bureau Hello doit apparaître dans les résultats de la recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="3906b-134">Cliquez sur **récupérer les données** Assistant de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="3906b-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="3906b-136">Sur hello **mise en route** volet, toorestore hello données toohello même serveur ou ordinateur, sélectionnez **ce serveur (`<server name>`)** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choisissez cette toohello de données de serveur option toorestore hello même ordinateur](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="3906b-138">Sur hello **sélectionner le Mode de récupération** volet, choisissez **fichiers et dossiers individuels** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="3906b-140">Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.</span><span class="sxs-lookup"><span data-stu-id="3906b-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="3906b-141">Dans le calendrier de hello, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="3906b-142">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="3906b-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="3906b-143">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="3906b-144">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="3906b-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="3906b-146">Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **monter**.</span><span class="sxs-lookup"><span data-stu-id="3906b-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="3906b-147">Sauvegarde Azure monte le point de récupération locaux hello et l’utilise comme un volume de reprise.</span><span class="sxs-lookup"><span data-stu-id="3906b-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="3906b-148">Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3906b-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="3906b-150">Dans l’Explorateur Windows, hello copier les fichiers et/ou dossiers souhaité toorestore et les coller tooany emplacement local toohello serveur ou l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3906b-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="3906b-151">Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="3906b-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copiez et collez les fichiers et dossiers à partir de l’emplacement du volume monté toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="3906b-153">Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**.</span><span class="sxs-lookup"><span data-stu-id="3906b-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="3906b-154">Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="3906b-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Démontez le volume de hello et confirmer](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="3906b-156">Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pour six heures après hello lorsqu’elle a été montée.</span><span class="sxs-lookup"><span data-stu-id="3906b-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="3906b-157">Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté.</span><span class="sxs-lookup"><span data-stu-id="3906b-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="3906b-158">N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.</span><span class="sxs-lookup"><span data-stu-id="3906b-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="3906b-159">Récupérer des données toohello même ordinateur</span><span class="sxs-lookup"><span data-stu-id="3906b-159">Recover data toohello same machine</span></span>
<span data-ttu-id="3906b-160">Si vous avez supprimé accidentellement une toorestore de fichier et qui souhaitent il toohello étapes de la même machine (à partir de quels hello est la sauvegarde), hello suivant vous permettra de récupérer les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="3906b-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="3906b-161">Ouvrez hello **Microsoft Azure Backup** snap dans.</span><span class="sxs-lookup"><span data-stu-id="3906b-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="3906b-162">Cliquez sur **récupérer les données** flux de travail tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="3906b-164">Sélectionnez hello  **ce serveur (*Nom_de_votre_ordinateur*) ** hello de toorestore option fichier sauvegardé sur hello même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3906b-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Même ordinateur](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="3906b-166">Choisissez trop**parcourir vos fichiers** ou **recherche des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="3906b-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="3906b-167">Laissez option par défaut de hello si vous envisagez de toorestore un ou plusieurs fichiers dont le chemin est connu.</span><span class="sxs-lookup"><span data-stu-id="3906b-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="3906b-168">Si vous n’êtes pas sûr à propos de la structure de dossiers hello mais que vous aimeriez toosearch pour un fichier, choisissez hello **recherche des fichiers** option.</span><span class="sxs-lookup"><span data-stu-id="3906b-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="3906b-169">Pour les besoins de hello de cette section, nous continuerons avec l’option par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="3906b-171">Sélectionnez un volume hello à partir de laquelle vous souhaitez fichier hello de toorestore.</span><span class="sxs-lookup"><span data-stu-id="3906b-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="3906b-172">Vous pouvez restaurer le fichier à partir de n’importe quel point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="3906b-172">You can restore from any point in time.</span></span> <span data-ttu-id="3906b-173">Les dates qui apparaissent dans **gras** dans le contrôle de calendrier hello indiquer la disponibilité de hello d’un point de restauration.</span><span class="sxs-lookup"><span data-stu-id="3906b-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="3906b-174">Une fois qu’une date est sélectionnée, en fonction de votre planification de sauvegarde (et réussite hello d’une opération de sauvegarde), vous pouvez sélectionner un point dans le temps de hello **temps** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="3906b-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="3906b-176">Sélectionnez hello éléments toorecover.</span><span class="sxs-lookup"><span data-stu-id="3906b-176">Select hello items toorecover.</span></span> <span data-ttu-id="3906b-177">Vous pouvez sélections plusieurs dossiers/fichiers toorestore.</span><span class="sxs-lookup"><span data-stu-id="3906b-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Sélectionner des fichiers](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="3906b-179">Spécifiez des paramètres de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-179">Specify hello recovery parameters.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="3906b-181">Vous avez la possibilité de restaurer l’emplacement d’origine de toohello (les Bonjour fichier/dossier serait remplacé) ou tooanother Bonjour même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3906b-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="3906b-182">Si hello fichier/dossier que vous souhaitez toorestore existe dans l’emplacement cible de hello, vous pouvez créer des copies (deux versions de hello même fichier), remplacer les fichiers hello dans l’emplacement cible de hello ou ignorer des fichiers hello qui existe dans la cible de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="3906b-183">Il est fortement recommandé que vous laissez l’option par défaut hello restauration des ACL hello sur les fichiers hello qui sont en cours de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="3906b-184">Une fois ces entrées fournies, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="3906b-185">workflow de récupération Hello, qui restaure l’ordinateur de toothis fichiers hello, commencera.</span><span class="sxs-lookup"><span data-stu-id="3906b-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="3906b-186">Récupérer tooan un autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="3906b-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="3906b-187">Si l’intégralité du serveur est perdu, vous pouvez toujours récupérer des données à partir d’ordinateurs différents du tooa Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="3906b-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="3906b-188">Hello suit illustre des flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="3906b-189">terminologie Hello utilisée dans cette procédure inclut :</span><span class="sxs-lookup"><span data-stu-id="3906b-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="3906b-190">*Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="3906b-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="3906b-191">*Ordinateur cible* – hello machine toowhich hello données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="3906b-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="3906b-192">*Archivage de l’exemple* – hello de toowhich de coffre de sauvegarde hello *machine Source* et *de l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="3906b-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="3906b-193">Les sauvegardes effectuées à partir d’un ordinateur ne peut pas être restaurées sur un ordinateur qui exécute une version antérieure du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="3906b-194">Par exemple, si les sauvegardes sont effectuées à partir d’un ordinateur Windows 7, elles peuvent être restaurées sur un ordinateur Windows 8 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="3906b-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="3906b-195">Toutefois, inversement hello n’est pas vraie.</span><span class="sxs-lookup"><span data-stu-id="3906b-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="3906b-196">Ouvrez hello **Microsoft Azure Backup** dans l’alignement sur hello *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="3906b-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="3906b-197">Vérifiez que hello *de l’ordinateur cible* et hello *machine Source* sont inscrit toohello même archivage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="3906b-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="3906b-198">Cliquez sur **récupérer les données** flux de travail tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="3906b-200">Sélectionnez **Un autre serveur**</span><span class="sxs-lookup"><span data-stu-id="3906b-200">Select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="3906b-202">Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*.</span><span class="sxs-lookup"><span data-stu-id="3906b-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="3906b-203">Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré) Télécharger un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="3906b-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="3906b-204">Une fois que le fichier d’informations d’identification de coffre hello est fourni, le coffre de sauvegarde hello sur le fichier d’informations d’identification de coffre hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3906b-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="3906b-205">Sélectionnez hello *machine Source* à partir de la liste hello des ordinateurs affichés.</span><span class="sxs-lookup"><span data-stu-id="3906b-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="3906b-207">Sélectionnez soit hello **recherche des fichiers** ou **parcourir vos fichiers** option.</span><span class="sxs-lookup"><span data-stu-id="3906b-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="3906b-208">Pour les besoins de hello de cette section, nous allons utiliser hello **recherche des fichiers** option.</span><span class="sxs-lookup"><span data-stu-id="3906b-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="3906b-210">Sélectionnez hello volume et la date dans l’écran suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="3906b-211">Recherche de nom de dossier ou fichier hello souhaité toorestore.</span><span class="sxs-lookup"><span data-stu-id="3906b-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="3906b-213">Sélectionnez emplacement hello où les fichiers de hello doivent toobe restaurée.</span><span class="sxs-lookup"><span data-stu-id="3906b-213">Select hello location where hello files need toobe restored.</span></span>

    ![Emplacement de restauration](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="3906b-215">Fournir hello phrase secrète de chiffrement qui a été fourni au cours de *l’ordinateur Source* inscription trop*coffre d’exemple*.</span><span class="sxs-lookup"><span data-stu-id="3906b-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="3906b-217">Une fois l’entrée hello est fournie, cliquez sur **récupérer**, les déclencheurs hello restauration Hello sauvegardé des fichiers toohello destination fournie.</span><span class="sxs-lookup"><span data-stu-id="3906b-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="3906b-218">Utiliser la restauration instantanée toorestore données tooan autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="3906b-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="3906b-219">Si l’intégralité du serveur est perdu, vous pouvez toujours récupérer des données à partir d’ordinateurs différents du tooa Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="3906b-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="3906b-220">Hello suit illustre des flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="3906b-221">terminologie Hello utilisée dans cette procédure inclut :</span><span class="sxs-lookup"><span data-stu-id="3906b-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="3906b-222">*Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="3906b-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="3906b-223">*Ordinateur cible* – hello machine toowhich hello données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="3906b-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="3906b-224">*Archivage de l’exemple* – Bonjour Recovery Services coffre toowhich Bonjour *machine Source* et *de l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="3906b-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="3906b-225">Les sauvegardes ne peut pas être restaurée tooa machine de cible exécute une version antérieure du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="3906b-226">Par exemple, une sauvegarde effectuée à partir d’un ordinateur Windows 7 ne peut pas être restaurée sur un ordinateur sous Windows 8 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3906b-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="3906b-227">Une sauvegarde effectuée à partir d’un ordinateur Windows 8 ne peut pas être restaurée tooa Windows 7 ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3906b-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="3906b-228">Ouvrez hello **Microsoft Azure Backup** dans l’alignement sur hello *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="3906b-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="3906b-229">Assurez-vous de hello *de l’ordinateur cible* et hello *machine Source* sont toohello des Services de récupération même coffre.</span><span class="sxs-lookup"><span data-stu-id="3906b-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="3906b-230">Cliquez sur **récupérer les données** tooopen hello **Assistant de récupération des données**.</span><span class="sxs-lookup"><span data-stu-id="3906b-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="3906b-232">Sur hello **mise en route** volet, sélectionnez **un autre serveur**</span><span class="sxs-lookup"><span data-stu-id="3906b-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="3906b-234">Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="3906b-235">Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3906b-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="3906b-236">Une fois que vous fournissez une information d’identification de coffre valide, le nom hello Hello correspondant du coffre de sauvegarde s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3906b-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="3906b-237">Sur hello **sélectionner le serveur de sauvegarde** volet, sélectionnez hello *machine Source* à partir de la liste hello d’ordinateurs affichés et fournir le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="3906b-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="3906b-238">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-238">Then click **Next**.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="3906b-240">Sur hello **sélectionner le Mode de récupération** volet, sélectionnez **fichiers et dossiers individuels** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="3906b-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="3906b-242">Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.</span><span class="sxs-lookup"><span data-stu-id="3906b-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="3906b-243">Dans le calendrier de hello, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="3906b-244">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="3906b-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="3906b-245">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="3906b-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="3906b-246">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="3906b-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="3906b-248">Cliquez sur **de montage** point de récupération toolocally montage hello comme un volume de récupération sur votre *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="3906b-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="3906b-249">Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3906b-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="3906b-251">Dans l’Explorateur Windows, copiez hello fichiers et/ou dossiers à partir du volume de reprise hello et collez-les tooyour *de l’ordinateur cible* emplacement.</span><span class="sxs-lookup"><span data-stu-id="3906b-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="3906b-252">Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="3906b-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="3906b-254">Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**.</span><span class="sxs-lookup"><span data-stu-id="3906b-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="3906b-255">Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="3906b-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="3906b-257">Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pour six heures après hello lorsqu’elle a été montée.</span><span class="sxs-lookup"><span data-stu-id="3906b-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="3906b-258">Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté.</span><span class="sxs-lookup"><span data-stu-id="3906b-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="3906b-259">N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.</span><span class="sxs-lookup"><span data-stu-id="3906b-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="3906b-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3906b-260">Next steps</span></span>
* [<span data-ttu-id="3906b-261">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="3906b-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="3906b-262">Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="3906b-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="3906b-263">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="3906b-263">Learn more</span></span>
* [<span data-ttu-id="3906b-264">Vue d’ensemble d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="3906b-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="3906b-265">Sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="3906b-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="3906b-266">Sauvegarde des charges de travail Microsoft</span><span class="sxs-lookup"><span data-stu-id="3906b-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
