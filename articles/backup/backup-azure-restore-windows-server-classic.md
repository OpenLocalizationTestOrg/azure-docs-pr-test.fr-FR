---
title: "Restauration de données sur un serveur Windows ou un ordinateur client Windows à partir d’Azure à l’aide du modèle de déploiement classique | Microsoft Docs"
description: "Découvrez comment restaurer des fichiers à partir d’un serveur/client Windows."
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
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="14d58-103">Restauration de fichiers sur un serveur Windows ou un ordinateur client Windows à l’aide du modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="14d58-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14d58-104">Portail classique</span><span class="sxs-lookup"><span data-stu-id="14d58-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="14d58-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="14d58-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="14d58-106">Cet article explique comment récupérer des données à partir d’un coffre de sauvegarde et les restaurer sur un serveur ou un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="14d58-107">Depuis mars 2017, vous ne pouvez plus utiliser le portail Classic pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="14d58-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14d58-108">Vous pouvez désormais mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="14d58-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="14d58-109">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="14d58-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="14d58-110">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="14d58-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="14d58-111">À compter du **15 octobre 2017**, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="14d58-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="14d58-112">**À compter du 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="14d58-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="14d58-113">Les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="14d58-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="14d58-114">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="14d58-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="14d58-115">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="14d58-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="14d58-116">Pour restaurer des données, vous pouvez utiliser l’Assistant Récupérer des données dans l’agent Microsoft Azure Recovery Services (MARS).</span><span class="sxs-lookup"><span data-stu-id="14d58-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="14d58-117">Lorsque vous restaurez des données, il est possible de :</span><span class="sxs-lookup"><span data-stu-id="14d58-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="14d58-118">Restaurer des données sur l’ordinateur à partir duquel les sauvegardes ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="14d58-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="14d58-119">Restaurez les données sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="14d58-120">En janvier 2017, Microsoft a publié une mise à jour de la pré-version de l’agent MARS.</span><span class="sxs-lookup"><span data-stu-id="14d58-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="14d58-121">Outre des correctifs de bogues, cette mise à jour propose la fonction de restauration instantanée, ce qui vous permet de monter une capture instantanée de point de récupération inscriptible comme volume de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="14d58-122">Vous pouvez ensuite explorer le volume de récupération, copier les fichiers sur un ordinateur local et sélectionner les fichiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="14d58-123">La [Mise à jour de la Sauvegarde Azure de janvier 2017](https://support.microsoft.com/en-us/help/3216528?preview) est nécessaire si vous souhaitez utiliser la restauration instantanée pour restaurer des données.</span><span class="sxs-lookup"><span data-stu-id="14d58-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="14d58-124">De plus, les données de sauvegarde doivent être protégées dans des coffres pour les pays listés dans l’article relatif au support.</span><span class="sxs-lookup"><span data-stu-id="14d58-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="14d58-125">Consultez la [Mise à jour de la Sauvegarde Azure de janvier 2017](https://support.microsoft.com/en-us/help/3216528?preview) pour obtenir la liste la plus récente des pays qui prennent en charge la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="14d58-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="14d58-126">La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.</span><span class="sxs-lookup"><span data-stu-id="14d58-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="14d58-127">La restauration instantanée est disponible pour une utilisation dans des coffres Recovery Services dans le portail Azure et dans des coffres de sauvegarde dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="14d58-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="14d58-128">Si vous souhaitez utiliser la restauration instantanée, téléchargez la mise à jour MARS et suivez les procédures mentionnant cette opération.</span><span class="sxs-lookup"><span data-stu-id="14d58-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="14d58-129">Utiliser la restauration instantanée pour récupérer des données sur le même ordinateur</span><span class="sxs-lookup"><span data-stu-id="14d58-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="14d58-130">Si vous avez supprimé accidentellement un fichier et que vous voulez le restaurer sur le même ordinateur (à partir duquel la sauvegarde est effectuée), les étapes suivantes vous aident à récupérer les données.</span><span class="sxs-lookup"><span data-stu-id="14d58-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="14d58-131">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** .</span><span class="sxs-lookup"><span data-stu-id="14d58-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="14d58-132">Si vous ne savez pas où le composant logiciel enfichable a été installé, recherchez **Sauvegarde Microsoft Azure** sur l’ordinateur ou le serveur.</span><span class="sxs-lookup"><span data-stu-id="14d58-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="14d58-133">L’application de bureau devrait apparaître dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="14d58-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="14d58-134">Cliquez sur **Récupérer des données** pour lancer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="14d58-134">Click **Recover Data** to start the wizard.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="14d58-136">Sur le volet **Prise en main**, pour restaurer les données sur le même serveur ou ordinateur, sélectionnez **Ce serveur (`<server name>`)** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choisissez l’option Ce serveur pour restaurer les données sur le même ordinateur](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="14d58-138">Sur le volet **Sélectionnez le mode de récupération**, choisissez **Fichiers et dossiers individuels**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="14d58-140">Sur le volet **Sélectionner le volume et la date**, sélectionnez le volume qui contient les fichiers et/ou les dossiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="14d58-141">Dans le calendrier, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="14d58-142">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="14d58-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="14d58-143">Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="14d58-144">Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**.</span><span class="sxs-lookup"><span data-stu-id="14d58-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="14d58-146">Une fois que vous avez choisi le point de récupération à restaurer, cliquez sur **Monter**.</span><span class="sxs-lookup"><span data-stu-id="14d58-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="14d58-147">La Sauvegarde Azure monte le point de récupération local et l’utilise comme volume de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="14d58-148">Sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Parcourir** pour ouvrir l’Explorateur Windows et rechercher les fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="14d58-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="14d58-150">Dans l’Explorateur Windows, copiez les fichiers et/ou les dossiers que vous souhaitez restaurer et collez-les à l’emplacement local de votre choix sur l’ordinateur ou le serveur.</span><span class="sxs-lookup"><span data-stu-id="14d58-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="14d58-151">Vous pouvez ouvrir ou diffuser en continu les fichiers directement à partir du volume de récupération et vérifier que les versions récupérées sont les bonnes.</span><span class="sxs-lookup"><span data-stu-id="14d58-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiez et collez les fichiers et dossiers du volume monté vers l’emplacement local](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="14d58-153">Lorsque vous avez terminé la restauration des fichiers et/ou des dossiers, sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Démonter**.</span><span class="sxs-lookup"><span data-stu-id="14d58-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="14d58-154">Puis cliquez sur **Oui** pour confirmer que vous souhaitez démonter le volume.</span><span class="sxs-lookup"><span data-stu-id="14d58-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Démontez le volume et confirmez](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="14d58-156">Si vous ne cliquez pas sur Démonter, le Volume de récupération reste monté pendant six heures à compter du montage.</span><span class="sxs-lookup"><span data-stu-id="14d58-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="14d58-157">Aucune opération de sauvegarde ne s’exécute tant que le volume est monté.</span><span class="sxs-lookup"><span data-stu-id="14d58-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="14d58-158">Toute opération de sauvegarde planifiée pour s’exécuter au moment où le volume de récupération est monté s’exécutera une fois qu’il sera démonté.</span><span class="sxs-lookup"><span data-stu-id="14d58-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="14d58-159">Récupération des données sur le même ordinateur</span><span class="sxs-lookup"><span data-stu-id="14d58-159">Recover data to the same machine</span></span>
<span data-ttu-id="14d58-160">Si vous avez supprimé accidentellement un fichier et que vous voulez le restaurer sur le même ordinateur (à partir duquel la sauvegarde est effectuée), les étapes suivantes vous aident à récupérer les données.</span><span class="sxs-lookup"><span data-stu-id="14d58-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="14d58-161">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** .</span><span class="sxs-lookup"><span data-stu-id="14d58-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="14d58-162">Cliquez sur **Récupérer des données** pour lancer le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="14d58-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="14d58-164">Sélectionnez l’option **Ce serveur (*nomdevotremachine*)** pour restaurer le fichier sauvegardé sur le même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![Même ordinateur](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="14d58-166">Vous pouvez choisir **Naviguer jusqu’aux fichiers** ou **Rechercher des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="14d58-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="14d58-167">Conservez l’option par défaut si vous envisagez de restaurer un ou plusieurs fichiers dont le chemin est connu.</span><span class="sxs-lookup"><span data-stu-id="14d58-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="14d58-168">Si vous n’êtes pas certain de la structure de dossiers, mais que vous voulez rechercher un fichier, choisissez l’option **Rechercher des fichiers** .</span><span class="sxs-lookup"><span data-stu-id="14d58-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="14d58-169">Dans cette section, nous choisissons l’option par défaut.</span><span class="sxs-lookup"><span data-stu-id="14d58-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="14d58-171">Sélectionnez le volume à partir duquel vous voulez restaurer le fichier.</span><span class="sxs-lookup"><span data-stu-id="14d58-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="14d58-172">Vous pouvez restaurer le fichier à partir de n’importe quel point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="14d58-172">You can restore from any point in time.</span></span> <span data-ttu-id="14d58-173">Les dates qui s’affichent en **gras** dans le contrôle Calendrier indiquent la disponibilité d’un point de restauration.</span><span class="sxs-lookup"><span data-stu-id="14d58-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="14d58-174">Une fois qu’une date est sélectionnée, en fonction de votre planification de sauvegarde (et de la réussite d’une opération de sauvegarde), vous pouvez sélectionner un point dans le temps dans la liste déroulante **Heure** .</span><span class="sxs-lookup"><span data-stu-id="14d58-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="14d58-176">Sélectionnez les éléments à restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-176">Select the items to recover.</span></span> <span data-ttu-id="14d58-177">Vous pouvez sélectionner plusieurs fichiers/dossiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-177">You can multi-select folders/files you wish to restore.</span></span>

    ![Sélectionner des fichiers](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="14d58-179">Spécifiez les paramètres de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-179">Specify the recovery parameters.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="14d58-181">Vous avez la possibilité d’effectuer la restauration à l’emplacement d’origine (dans lequel le fichier/dossier sera remplacé) ou dans un autre emplacement sur le même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="14d58-182">Si le fichier/dossier que vous voulez restaurer existe dans l’emplacement cible, vous avez la possibilité de créer des copies (deux versions du même fichier), de remplacer les fichiers dans l’emplacement cible ou d’ignorer la récupération des fichiers qui existent dans la cible.</span><span class="sxs-lookup"><span data-stu-id="14d58-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="14d58-183">Il est vivement recommandé de conserver l’option par défaut qui consiste à restaurer les ACL sur les fichiers récupérés.</span><span class="sxs-lookup"><span data-stu-id="14d58-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="14d58-184">Une fois ces entrées fournies, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="14d58-185">Le flux de travail de récupération, qui consiste à restaurer les fichiers sur cet ordinateur, commence.</span><span class="sxs-lookup"><span data-stu-id="14d58-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="14d58-186">Récupération sur un autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="14d58-186">Recover to an alternate machine</span></span>
<span data-ttu-id="14d58-187">Si votre serveur entier est perdu, vous pouvez toujours récupérer les données d’Azure Backup sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="14d58-188">Les étapes suivantes illustrent le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="14d58-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="14d58-189">Les termes ci-après sont utilisés pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="14d58-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="14d58-190">*Ordinateur source* : ordinateur d’origine à partir duquel la sauvegarde a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="14d58-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="14d58-191">*Ordinateur cible* : ordinateur sur lequel les données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="14d58-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="14d58-192">*Exemple d’archivage* : archivage de sauvegarde dans lequel *l’ordinateur source* et *l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="14d58-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="14d58-193">Les sauvegardes effectuées à partir d’un ordinateur ne peuvent pas être restaurées sur un ordinateur qui exécute une version antérieure du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="14d58-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="14d58-194">Par exemple, si les sauvegardes sont effectuées à partir d’un ordinateur Windows 7, elles peuvent être restaurées sur un ordinateur Windows 8 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="14d58-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="14d58-195">Toutefois l’inverse n’est pas vrai.</span><span class="sxs-lookup"><span data-stu-id="14d58-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="14d58-196">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** sur l’ *ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="14d58-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="14d58-197">Vérifiez que *l’ordinateur cible* et *l’ordinateur source* sont inscrits auprès du même archivage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="14d58-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="14d58-198">Cliquez sur **Récupérer des données** pour lancer le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="14d58-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="14d58-200">Sélectionnez **Un autre serveur**</span><span class="sxs-lookup"><span data-stu-id="14d58-200">Select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="14d58-202">Fournissez le fichier d’informations d’identification de coffre qui correspond à l’ *exemple d’archivage*.</span><span class="sxs-lookup"><span data-stu-id="14d58-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="14d58-203">Si le fichier d’informations d’identification de coffre n’est pas valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de l’ *exemple d’archivage* dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="14d58-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="14d58-204">Une fois que le fichier d’informations d’identification de coffre est fourni, l’archivage de sauvegarde correspondant au fichier d’informations d’identification de coffre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="14d58-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="14d58-205">Sélectionnez l’ *ordinateur source* dans la liste des ordinateurs affichés.</span><span class="sxs-lookup"><span data-stu-id="14d58-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="14d58-207">Sélectionnez l’option **Rechercher des fichiers** ou **Naviguer jusqu’aux fichiers**.</span><span class="sxs-lookup"><span data-stu-id="14d58-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="14d58-208">Dans cette section, nous utilisons l’option **Rechercher des fichiers** .</span><span class="sxs-lookup"><span data-stu-id="14d58-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![action](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="14d58-210">Dans l’écran suivant, sélectionnez le volume et la date.</span><span class="sxs-lookup"><span data-stu-id="14d58-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="14d58-211">Recherchez le nom du fichier/dossier que vous souhaitez restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-211">Search for the folder/file name you want to restore.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="14d58-213">Sélectionnez l’emplacement vers lequel les fichiers doivent être restaurés.</span><span class="sxs-lookup"><span data-stu-id="14d58-213">Select the location where the files need to be restored.</span></span>

    ![Emplacement de restauration](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="14d58-215">Fournissez la phrase secrète de chiffrement qui a été fournie pendant l’inscription de *l’ordinateur source* dans *l’exemple d’archivage*.</span><span class="sxs-lookup"><span data-stu-id="14d58-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="14d58-217">Une fois l’entrée fournie, cliquez sur **Récupérer**pour déclencher la restauration des fichiers de sauvegarde dans la destination fournie.</span><span class="sxs-lookup"><span data-stu-id="14d58-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="14d58-218">Utiliser la restauration instantanée pour restaurer des données sur un autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="14d58-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="14d58-219">Si votre serveur entier est perdu, vous pouvez toujours récupérer les données d’Azure Backup sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14d58-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="14d58-220">Les étapes suivantes illustrent le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="14d58-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="14d58-221">Les termes ci-après sont utilisés pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="14d58-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="14d58-222">*Ordinateur source* : ordinateur d’origine à partir duquel la sauvegarde a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="14d58-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="14d58-223">*Ordinateur cible* : ordinateur sur lequel les données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="14d58-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="14d58-224">*Exemple d’archivage* – coffre Recovery Services dans lequel *l’ordinateur source* et *l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="14d58-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="14d58-225">Il est impossible de restaurer les sauvegardes sur un ordinateur cible qui fonctionne avec une version antérieure du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="14d58-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="14d58-226">Par exemple, une sauvegarde effectuée à partir d’un ordinateur Windows 7 ne peut pas être restaurée sur un ordinateur sous Windows 8 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="14d58-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="14d58-227">Il n’est pas possible de restaurer sur un ordinateur Windows 7 une sauvegarde effectuée à partir d’un ordinateur Windows 8.</span><span class="sxs-lookup"><span data-stu-id="14d58-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="14d58-228">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** sur l’ *ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="14d58-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="14d58-229">Vérifiez que *l’Ordinateur cible* et *l’Ordinateur source* sont inscrits auprès du même coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="14d58-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="14d58-230">Cliquez sur **Récupérer des données** pour ouvrir **l’Assistant Récupération de données**.</span><span class="sxs-lookup"><span data-stu-id="14d58-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="14d58-232">Sur le volet **Prise en main**, sélectionnez **Autre serveur**.</span><span class="sxs-lookup"><span data-stu-id="14d58-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="14d58-234">Fournissez le fichier d’informations d’identification correspondant à *l’Exemple de coffre*, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="14d58-235">Si le fichier d’informations d’identification du coffre n’est pas valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de *l’Exemple de coffre* dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="14d58-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="14d58-236">Une fois que vous avez fourni des informations d’identification de coffre valides, le nom du Coffre de sauvegarde correspondant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="14d58-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="14d58-237">Sur le volet **Sélectionner un serveur de sauvegarde**, sélectionnez *l’Ordinateur source* dans la liste des ordinateurs affichés et fournissez la phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="14d58-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="14d58-238">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-238">Then click **Next**.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="14d58-240">Sur le volet **Sélectionner un mode de récupération**, sélectionnez **Fichiers et dossiers individuels** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="14d58-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="14d58-242">Sur le volet **Sélectionner le volume et la date**, sélectionnez le volume qui contient les fichiers et/ou les dossiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="14d58-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="14d58-243">Dans le calendrier, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="14d58-244">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="14d58-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="14d58-245">Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="14d58-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="14d58-246">Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**.</span><span class="sxs-lookup"><span data-stu-id="14d58-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="14d58-248">Cliquez sur **Monter** pour monter localement le point de récupération comme volume de récupération sur votre *Ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="14d58-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="14d58-249">Sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Parcourir** pour ouvrir l’Explorateur Windows et rechercher les fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="14d58-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="14d58-251">Dans l’Explorateur Windows, copiez les fichiers et/ou les dossiers du volume de récupération et collez-les à l’emplacement de votre *Ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="14d58-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="14d58-252">Vous pouvez ouvrir ou diffuser en continu les fichiers directement à partir du volume de récupération et vérifier que les versions récupérées sont les bonnes.</span><span class="sxs-lookup"><span data-stu-id="14d58-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="14d58-254">Lorsque vous avez terminé la restauration des fichiers et/ou des dossiers, sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Démonter**.</span><span class="sxs-lookup"><span data-stu-id="14d58-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="14d58-255">Puis cliquez sur **Oui** pour confirmer que vous souhaitez démonter le volume.</span><span class="sxs-lookup"><span data-stu-id="14d58-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="14d58-257">Si vous ne cliquez pas sur Démonter, le Volume de récupération reste monté pendant six heures à compter du montage.</span><span class="sxs-lookup"><span data-stu-id="14d58-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="14d58-258">Aucune opération de sauvegarde ne s’exécute tant que le volume est monté.</span><span class="sxs-lookup"><span data-stu-id="14d58-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="14d58-259">Toute opération de sauvegarde planifiée pour s’exécuter au moment où le volume de récupération est monté s’exécutera une fois qu’il sera démonté.</span><span class="sxs-lookup"><span data-stu-id="14d58-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="14d58-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14d58-260">Next steps</span></span>
* [<span data-ttu-id="14d58-261">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="14d58-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="14d58-262">Consultez le [forum Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="14d58-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="14d58-263">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="14d58-263">Learn more</span></span>
* [<span data-ttu-id="14d58-264">Vue d’ensemble d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="14d58-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="14d58-265">Sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="14d58-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="14d58-266">Sauvegarde des charges de travail Microsoft</span><span class="sxs-lookup"><span data-stu-id="14d58-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
