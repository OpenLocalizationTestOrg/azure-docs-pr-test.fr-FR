---
title: "Restaurer des données dans Azure sur un serveur Windows ou un ordinateur Windows | Microsoft Docs"
description: "Découvrez comment restaurer des données stockées dans Azure sur un serveur Windows ou un ordinateur Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="6a39d-103">Restauration de fichiers sur un serveur Windows ou un ordinateur client Windows à l’aide du modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6a39d-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a39d-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6a39d-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="6a39d-105">Portail classique</span><span class="sxs-lookup"><span data-stu-id="6a39d-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="6a39d-106">Cet article explique comment restaurer des données depuis un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6a39d-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="6a39d-107">Pour restaurer des données, vous pouvez utiliser l’Assistant Récupérer des données dans l’agent Microsoft Azure Recovery Services (MARS).</span><span class="sxs-lookup"><span data-stu-id="6a39d-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="6a39d-108">Lorsque vous restaurez des données, il est possible de :</span><span class="sxs-lookup"><span data-stu-id="6a39d-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="6a39d-109">Restaurer des données sur l’ordinateur à partir duquel les sauvegardes ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="6a39d-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="6a39d-110">Restaurez les données sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6a39d-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="6a39d-111">En janvier 2017, Microsoft a publié une mise à jour de la pré-version de l’agent MARS.</span><span class="sxs-lookup"><span data-stu-id="6a39d-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="6a39d-112">Outre des correctifs de bogues, cette mise à jour propose la fonction de restauration instantanée, ce qui vous permet de monter une capture instantanée de point de récupération inscriptible comme volume de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="6a39d-113">Vous pouvez ensuite explorer le volume de récupération, copier les fichiers sur un ordinateur local et sélectionner les fichiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="6a39d-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="6a39d-114">La [Mise à jour de la Sauvegarde Azure de janvier 2017](https://support.microsoft.com/en-us/help/3216528?preview) est nécessaire si vous souhaitez utiliser la restauration instantanée pour restaurer des données.</span><span class="sxs-lookup"><span data-stu-id="6a39d-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="6a39d-115">De plus, les données de sauvegarde doivent être protégées dans des coffres pour les pays listés dans l’article relatif au support.</span><span class="sxs-lookup"><span data-stu-id="6a39d-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="6a39d-116">Consultez la [Mise à jour de la Sauvegarde Azure de janvier 2017](https://support.microsoft.com/en-us/help/3216528?preview) pour obtenir la liste la plus récente des pays qui prennent en charge la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="6a39d-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="6a39d-117">La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.</span><span class="sxs-lookup"><span data-stu-id="6a39d-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="6a39d-118">La restauration instantanée est disponible pour une utilisation dans des coffres Recovery Services dans le portail Azure et dans des coffres de sauvegarde dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="6a39d-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="6a39d-119">Si vous souhaitez utiliser la restauration instantanée, téléchargez la mise à jour MARS et suivez les procédures mentionnant cette opération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="6a39d-120">Utiliser la restauration instantanée pour récupérer des données sur le même ordinateur</span><span class="sxs-lookup"><span data-stu-id="6a39d-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="6a39d-121">Si vous avez supprimé accidentellement un fichier et que vous voulez le restaurer sur le même ordinateur (à partir duquel la sauvegarde est effectuée), les étapes suivantes vous aident à récupérer les données.</span><span class="sxs-lookup"><span data-stu-id="6a39d-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="6a39d-122">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** .</span><span class="sxs-lookup"><span data-stu-id="6a39d-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="6a39d-123">Si vous ne savez pas où le composant logiciel enfichable a été installé, recherchez **Sauvegarde Microsoft Azure** sur l’ordinateur ou le serveur.</span><span class="sxs-lookup"><span data-stu-id="6a39d-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="6a39d-124">L’application de bureau devrait apparaître dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="6a39d-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="6a39d-125">Cliquez sur **Récupérer des données** pour lancer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="6a39d-125">Click **Recover Data** to start the wizard.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="6a39d-127">Sur le volet **Prise en main**, pour restaurer les données sur le même serveur ou ordinateur, sélectionnez **Ce serveur (`<server name>`)** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choisissez l’option Ce serveur pour restaurer les données sur le même ordinateur](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="6a39d-129">Sur le volet **Sélectionnez le mode de récupération**, choisissez **Fichiers et dossiers individuels**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="6a39d-131">Sur le volet **Sélectionner le volume et la date**, sélectionnez le volume qui contient les fichiers et/ou les dossiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="6a39d-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="6a39d-132">Dans le calendrier, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="6a39d-133">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6a39d-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="6a39d-134">Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="6a39d-135">Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="6a39d-137">Une fois que vous avez choisi le point de récupération à restaurer, cliquez sur **Monter**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="6a39d-138">La Sauvegarde Azure monte le point de récupération local et l’utilise comme volume de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="6a39d-139">Sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Parcourir** pour ouvrir l’Explorateur Windows et rechercher les fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6a39d-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="6a39d-141">Dans l’Explorateur Windows, copiez les fichiers et/ou les dossiers que vous souhaitez restaurer et collez-les à l’emplacement local de votre choix sur l’ordinateur ou le serveur.</span><span class="sxs-lookup"><span data-stu-id="6a39d-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="6a39d-142">Vous pouvez ouvrir ou diffuser en continu les fichiers directement à partir du volume de récupération et vérifier que les versions récupérées sont les bonnes.</span><span class="sxs-lookup"><span data-stu-id="6a39d-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Copiez et collez les fichiers et dossiers du volume monté vers l’emplacement local](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="6a39d-144">Lorsque vous avez terminé la restauration des fichiers et/ou des dossiers, sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Démonter**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="6a39d-145">Puis cliquez sur **Oui** pour confirmer que vous souhaitez démonter le volume.</span><span class="sxs-lookup"><span data-stu-id="6a39d-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Démontez le volume et confirmez](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="6a39d-147">Si vous ne cliquez pas sur Démonter, le volume de récupération reste monté pendant 6 heures à compter du montage.</span><span class="sxs-lookup"><span data-stu-id="6a39d-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="6a39d-148">Toutefois, la durée du montage est étendue jusqu’à un maximum de 24 heures en cas de copie de fichier en cours.</span><span class="sxs-lookup"><span data-stu-id="6a39d-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="6a39d-149">Aucune opération de sauvegarde ne s’exécute tant que le volume est monté.</span><span class="sxs-lookup"><span data-stu-id="6a39d-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="6a39d-150">Toute opération de sauvegarde planifiée pour s’exécuter au moment où le volume de récupération est monté s’exécutera une fois qu’il sera démonté.</span><span class="sxs-lookup"><span data-stu-id="6a39d-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="6a39d-151">Utiliser la restauration instantanée pour restaurer des données sur un autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="6a39d-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="6a39d-152">Si votre serveur entier est perdu, vous pouvez toujours récupérer les données d’Azure Backup sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6a39d-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="6a39d-153">Les étapes suivantes illustrent le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="6a39d-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="6a39d-154">Les termes ci-après sont utilisés pour cette procédure :</span><span class="sxs-lookup"><span data-stu-id="6a39d-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="6a39d-155">*Ordinateur source* : ordinateur d’origine à partir duquel la sauvegarde a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="6a39d-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="6a39d-156">*Ordinateur cible* : ordinateur sur lequel les données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="6a39d-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="6a39d-157">*Exemple d’archivage* – coffre Recovery Services dans lequel *l’ordinateur source* et *l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="6a39d-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="6a39d-158">Il est impossible de restaurer les sauvegardes sur un ordinateur cible qui fonctionne avec une version antérieure du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="6a39d-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="6a39d-159">Par exemple, une sauvegarde effectuée à partir d’un ordinateur Windows 7 ne peut pas être restaurée sur un ordinateur sous Windows 8 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6a39d-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="6a39d-160">Il n’est pas possible de restaurer sur un ordinateur Windows 7 une sauvegarde effectuée à partir d’un ordinateur Windows 8.</span><span class="sxs-lookup"><span data-stu-id="6a39d-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="6a39d-161">Ouvrez le composant logiciel enfichable **Microsoft Azure Backup** sur l’ *ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="6a39d-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="6a39d-162">Vérifiez que *l’Ordinateur cible* et *l’Ordinateur source* sont inscrits auprès du même coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6a39d-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="6a39d-163">Cliquez sur **Récupérer des données** pour ouvrir **l’Assistant Récupération de données**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="6a39d-165">Sur le volet **Prise en main**, sélectionnez **Autre serveur**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="6a39d-167">Fournissez le fichier d’informations d’identification correspondant à *l’Exemple de coffre*, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="6a39d-168">Si le fichier d’informations d’identification du coffre n’est pas valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de *l’Exemple de coffre* dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6a39d-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="6a39d-169">Une fois que vous avez fourni des informations d’identification de coffre valides, le nom du Coffre de sauvegarde correspondant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6a39d-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="6a39d-170">Sur le volet **Sélectionner un serveur de sauvegarde**, sélectionnez *l’Ordinateur source* dans la liste des ordinateurs affichés et fournissez la phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="6a39d-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="6a39d-171">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-171">Then click **Next**.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="6a39d-173">Sur le volet **Sélectionner un mode de récupération**, sélectionnez **Fichiers et dossiers individuels** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="6a39d-175">Sur le volet **Sélectionner le volume et la date**, sélectionnez le volume qui contient les fichiers et/ou les dossiers à restaurer.</span><span class="sxs-lookup"><span data-stu-id="6a39d-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="6a39d-176">Dans le calendrier, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="6a39d-177">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6a39d-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="6a39d-178">Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a39d-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="6a39d-179">Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="6a39d-181">Cliquez sur **Monter** pour monter localement le point de récupération comme volume de récupération sur votre *Ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="6a39d-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="6a39d-182">Sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Parcourir** pour ouvrir l’Explorateur Windows et rechercher les fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6a39d-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="6a39d-184">Dans l’Explorateur Windows, copiez les fichiers et/ou les dossiers du volume de récupération et collez-les à l’emplacement de votre *Ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="6a39d-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="6a39d-185">Vous pouvez ouvrir ou diffuser en continu les fichiers directement à partir du volume de récupération et vérifier que les versions récupérées sont les bonnes.</span><span class="sxs-lookup"><span data-stu-id="6a39d-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="6a39d-187">Lorsque vous avez terminé la restauration des fichiers et/ou des dossiers, sur le volet **Rechercher et récupérer des fichiers**, cliquez sur **Démonter**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="6a39d-188">Puis cliquez sur **Oui** pour confirmer que vous souhaitez démonter le volume.</span><span class="sxs-lookup"><span data-stu-id="6a39d-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="6a39d-190">Si vous ne cliquez pas sur Démonter, le volume de récupération reste monté pendant 6 heures à compter du montage.</span><span class="sxs-lookup"><span data-stu-id="6a39d-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="6a39d-191">Toutefois, la durée du montage est étendue jusqu’à un maximum de 24 heures en cas de copie de fichier en cours.</span><span class="sxs-lookup"><span data-stu-id="6a39d-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="6a39d-192">Aucune opération de sauvegarde ne s’exécute tant que le volume est monté.</span><span class="sxs-lookup"><span data-stu-id="6a39d-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="6a39d-193">Toute opération de sauvegarde planifiée pour s’exécuter au moment où le volume de récupération est monté s’exécutera une fois qu’il sera démonté.</span><span class="sxs-lookup"><span data-stu-id="6a39d-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="6a39d-194">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="6a39d-194">Troubleshooting</span></span>
<span data-ttu-id="6a39d-195">Si Azure Backup ne monte pas efficacement le volume de montage, même lorsque vous cliquez plusieurs fois sur **Monter**, ou ne parvient pas à le monter et génère une ou plusieurs erreurs, suivez la procédure ci-dessous pour entamer une récupération normale.</span><span class="sxs-lookup"><span data-stu-id="6a39d-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="6a39d-196">Si le processus de montage s’exécute depuis plusieurs minutes, annulez-le.</span><span class="sxs-lookup"><span data-stu-id="6a39d-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="6a39d-197">Vérifiez que vous disposez de la dernière version de l’agent de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="6a39d-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="6a39d-198">Pour en savoir plus sur la version de l’agent de sauvegarde Azure, cliquez sur la zone **À propos de l’agent Microsoft Azure Recovery Services** du volet **Actions** de la console de sauvegarde Microsoft Azure, et assurez-vous que le numéro de **version** est égal ou supérieur à celui qu’indique [cet article](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="6a39d-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="6a39d-199">Vous pouvez télécharger la dernière version [ici](https://go.microsoft.com/fwLink/?LinkID=288905).</span><span class="sxs-lookup"><span data-stu-id="6a39d-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="6a39d-200">Cliquez sur **Gestionnaire de périphériques** -> **Contrôleurs de stockage** et vérifiez que vous pouvez localiser **l’initiateur Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="6a39d-201">Si la réponse est oui, accédez directement à l’étape 7 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6a39d-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="6a39d-202">Si vous ne pouvez pas localiser le service Initiateur iSCSI de Microsoft indiqué à l’étape 3, vérifiez si, sous **Gestionnaire de périphériques** -> **Contrôleurs de stockage**, l’entrée **Appareil inconnu** s’affiche, associée à l’ID matériel **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="6a39d-203">Cliquez avec le bouton droit sur l’entrée **Appareil inconnu** et sélectionnez **Mettre à jour le pilote**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="6a39d-204">Mettez à jour le pilote, en sélectionnant l’option **Rechercher automatiquement un pilote logiciel mis à jour**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="6a39d-205">Suite à la mise à jour, l’entrée **Appareil inconnu** est remplacée par **Initiateur Microsoft iSCSI**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6a39d-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Chiffrement](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="6a39d-207">Cliquez sur **Gestionnaire des tâches** -> **Services (local)** -> **Service Initiateur iSCSI de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Chiffrement](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="6a39d-209">Redémarrez le service Initiateur iSCSI de Microsoft en cliquant avec le bouton droit sur ce dernier, en cliquant sur **Arrêter**, puis en cliquant à nouveau sur le bouton droit et en sélectionnant **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="6a39d-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="6a39d-210">Recommencez la récupération à l’aide de la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="6a39d-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="6a39d-211">Si elle échoue encore, redémarrez votre serveur/client.</span><span class="sxs-lookup"><span data-stu-id="6a39d-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="6a39d-212">Si un redémarrage n’est pas souhaitable, ou si la récupération échoue même après le redémarrage du serveur, essayez de l’exécuter au moyen d’un autre ordinateur et contactez le Support Azure en accédant au [portail Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), puis en soumettant une demande de support.</span><span class="sxs-lookup"><span data-stu-id="6a39d-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a39d-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a39d-213">Next steps</span></span>
* <span data-ttu-id="6a39d-214">Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="6a39d-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
