---
title: "données aaaRestore dans Azure tooa Windows Server ou ordinateur Windows | Documents Microsoft"
description: "Découvrez comment les données de toorestore stockées dans Azure tooa Windows Server ou de l’ordinateur Windows."
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
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="62b03-103">Restaurer des fichiers tooa Windows server ou la machine du client Windows à l’aide du modèle de déploiement de gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="62b03-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62b03-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="62b03-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="62b03-105">Portail classique</span><span class="sxs-lookup"><span data-stu-id="62b03-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="62b03-106">Cet article explique comment toorestore des données à partir d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="62b03-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="62b03-107">toorestore des données, vous utilisez hello récupérer les données Assistant agent de Microsoft Azure Recovery Services (MARS) hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="62b03-108">Lorsque vous restaurez des données, il est possible de :</span><span class="sxs-lookup"><span data-stu-id="62b03-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="62b03-109">Restauration de données toohello est identique à l’ordinateur à partir de laquelle les sauvegardes hello ont été effectuées.</span><span class="sxs-lookup"><span data-stu-id="62b03-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="62b03-110">Restaurer un ordinateur autre tooan de données.</span><span class="sxs-lookup"><span data-stu-id="62b03-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="62b03-111">En janvier 2017, Microsoft a publié un agent de MARS toohello aperçu mise à jour.</span><span class="sxs-lookup"><span data-stu-id="62b03-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="62b03-112">Ainsi que des correctifs de bogues, cette mise à jour Active la restauration instantanée, ce qui vous permet de toomount un instantané de point de récupération accessible en écriture comme un volume de reprise.</span><span class="sxs-lookup"><span data-stu-id="62b03-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="62b03-113">Vous pouvez ensuite Explorer hello récupération volume et copie les fichiers tooa ordinateur local ainsi sélectivement restauration de fichiers.</span><span class="sxs-lookup"><span data-stu-id="62b03-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="62b03-114">Hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) est requis si vous voulez toouse restauration instantanée toorestore données.</span><span class="sxs-lookup"><span data-stu-id="62b03-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="62b03-115">Les données de sauvegarde hello doivent également être protégées dans des coffres dans les paramètres régionaux répertoriés dans l’article du support technique hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="62b03-116">Consultez hello [janvier 2017 mise à jour d’Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) pour hello dernière liste des paramètres régionaux qui prennent en charge la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="62b03-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="62b03-117">La restauration instantanée n’est actuellement **pas** disponible dans tous les pays.</span><span class="sxs-lookup"><span data-stu-id="62b03-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="62b03-118">Restauration instantanée est disponible pour utilisation dans les Services de récupération des coffres Bonjour portail Azure et les coffres de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="62b03-119">Si vous souhaitez toouse restauration instantanée, téléchargez la mise à jour de MARS hello et suivez les procédures de hello mentionnant restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="62b03-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="62b03-120">Utiliser la restauration instantanée toohello de données toorecover même ordinateur</span><span class="sxs-lookup"><span data-stu-id="62b03-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="62b03-121">Si vous avez supprimé accidentellement une toorestore de fichier et qui souhaitent il toohello étapes de la même machine (à partir de quels hello est la sauvegarde), hello suivant vous permettra de récupérer les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="62b03-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="62b03-122">Ouvrez hello **Microsoft Azure Backup** snap dans.</span><span class="sxs-lookup"><span data-stu-id="62b03-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="62b03-123">Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="62b03-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="62b03-124">application de bureau Hello doit apparaître dans les résultats de la recherche hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="62b03-125">Cliquez sur **récupérer les données** Assistant de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="62b03-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="62b03-127">Sur hello **mise en route** volet, toorestore hello données toohello même serveur ou ordinateur, sélectionnez **ce serveur (`<server name>`)** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62b03-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choisissez cette toohello de données de serveur option toorestore hello même ordinateur](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="62b03-129">Sur hello **sélectionner le Mode de récupération** volet, choisissez **fichiers et dossiers individuels** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62b03-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="62b03-131">Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.</span><span class="sxs-lookup"><span data-stu-id="62b03-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="62b03-132">Dans le calendrier de hello, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="62b03-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="62b03-133">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="62b03-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="62b03-134">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="62b03-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="62b03-135">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="62b03-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume et date](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="62b03-137">Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **monter**.</span><span class="sxs-lookup"><span data-stu-id="62b03-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="62b03-138">Sauvegarde Azure monte le point de récupération locaux hello et l’utilise comme un volume de reprise.</span><span class="sxs-lookup"><span data-stu-id="62b03-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="62b03-139">Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="62b03-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Options de récupération](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="62b03-141">Dans l’Explorateur Windows, hello copier les fichiers et/ou dossiers souhaité toorestore et les coller tooany emplacement local toohello serveur ou l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="62b03-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="62b03-142">Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="62b03-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Copiez et collez les fichiers et dossiers à partir de l’emplacement du volume monté toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="62b03-144">Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**.</span><span class="sxs-lookup"><span data-stu-id="62b03-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="62b03-145">Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="62b03-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Démontez le volume de hello et confirmer](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="62b03-147">Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pendant 6 heures à partir de l’heure hello lorsqu’elle a été montée.</span><span class="sxs-lookup"><span data-stu-id="62b03-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="62b03-148">Toutefois, le temps de montage hello est étendue jusqu'à un maximum de 24 heures en cas d’une copie de fichier en cours.</span><span class="sxs-lookup"><span data-stu-id="62b03-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="62b03-149">Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté.</span><span class="sxs-lookup"><span data-stu-id="62b03-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="62b03-150">N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.</span><span class="sxs-lookup"><span data-stu-id="62b03-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="62b03-151">Utiliser la restauration instantanée toorestore données tooan autre ordinateur</span><span class="sxs-lookup"><span data-stu-id="62b03-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="62b03-152">Si l’intégralité du serveur est perdu, vous pouvez toujours récupérer des données à partir d’ordinateurs différents du tooa Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="62b03-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="62b03-153">Hello suit illustre des flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="62b03-154">terminologie Hello utilisée dans cette procédure inclut :</span><span class="sxs-lookup"><span data-stu-id="62b03-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="62b03-155">*Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="62b03-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="62b03-156">*Ordinateur cible* – hello machine toowhich hello données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="62b03-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="62b03-157">*Archivage de l’exemple* – Bonjour Recovery Services coffre toowhich Bonjour *machine Source* et *de l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="62b03-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="62b03-158">Les sauvegardes ne peut pas être restaurée tooa machine de cible exécute une version antérieure du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="62b03-159">Par exemple, une sauvegarde effectuée à partir d’un ordinateur Windows 7 ne peut pas être restaurée sur un ordinateur sous Windows 8 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="62b03-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="62b03-160">Une sauvegarde effectuée à partir d’un ordinateur Windows 8 ne peut pas être restaurée tooa Windows 7 ordinateur.</span><span class="sxs-lookup"><span data-stu-id="62b03-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="62b03-161">Ouvrez hello **Microsoft Azure Backup** dans l’alignement sur hello *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="62b03-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="62b03-162">Assurez-vous de hello *de l’ordinateur cible* et hello *machine Source* sont toohello des Services de récupération même coffre.</span><span class="sxs-lookup"><span data-stu-id="62b03-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="62b03-163">Cliquez sur **récupérer les données** tooopen hello **Assistant de récupération des données**.</span><span class="sxs-lookup"><span data-stu-id="62b03-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="62b03-165">Sur hello **mise en route** volet, sélectionnez **un autre serveur**</span><span class="sxs-lookup"><span data-stu-id="62b03-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="62b03-167">Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62b03-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="62b03-168">Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="62b03-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="62b03-169">Une fois que vous fournissez une information d’identification de coffre valide, le nom hello Hello correspondant du coffre de sauvegarde s’affiche.</span><span class="sxs-lookup"><span data-stu-id="62b03-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="62b03-170">Sur hello **sélectionner le serveur de sauvegarde** volet, sélectionnez hello *machine Source* à partir de la liste hello d’ordinateurs affichés et fournir le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="62b03-171">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="62b03-171">Then click **Next**.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="62b03-173">Sur hello **sélectionner le Mode de récupération** volet, sélectionnez **fichiers et dossiers individuels** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62b03-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="62b03-175">Sur hello **sélectionner le Volume et la Date** volet, volume hello select qui contient les fichiers hello et/ou les dossiers que vous souhaitez toorestore.</span><span class="sxs-lookup"><span data-stu-id="62b03-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="62b03-176">Dans le calendrier de hello, sélectionnez un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="62b03-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="62b03-177">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="62b03-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="62b03-178">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="62b03-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="62b03-179">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="62b03-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Éléments de recherche](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="62b03-181">Cliquez sur **de montage** point de récupération toolocally montage hello comme un volume de récupération sur votre *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="62b03-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="62b03-182">Sur hello **Parcourir et restaurer des fichiers** volet, cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="62b03-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="62b03-184">Dans l’Explorateur Windows, copiez hello fichiers et/ou dossiers à partir du volume de reprise hello et collez-les tooyour *de l’ordinateur cible* emplacement.</span><span class="sxs-lookup"><span data-stu-id="62b03-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="62b03-185">Vous pouvez ouvrir ou diffuser des fichiers hello directement à partir de volume de récupération hello et vérifiez hello correct versions sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="62b03-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="62b03-187">Quand vous avez terminé de restauration des fichiers de hello et/ou des dossiers, sur hello **Parcourir et les fichiers de récupération** volet, cliquez sur **démontage**.</span><span class="sxs-lookup"><span data-stu-id="62b03-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="62b03-188">Puis cliquez sur **Oui** tooconfirm que vous souhaitez le volume de hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="62b03-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Chiffrement](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="62b03-190">Si vous ne cliquez pas sur les démonter, hello récupération Volume restera monté pendant 6 heures à partir de l’heure hello lorsqu’elle a été montée.</span><span class="sxs-lookup"><span data-stu-id="62b03-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="62b03-191">Toutefois, le temps de montage hello est étendue jusqu'à un maximum de 24 heures en cas d’une copie de fichier en cours.</span><span class="sxs-lookup"><span data-stu-id="62b03-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="62b03-192">Aucune opération de sauvegarde ne s’exécuteront pendant que hello volume est monté.</span><span class="sxs-lookup"><span data-stu-id="62b03-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="62b03-193">N’importe quel toorun de l’opération de sauvegarde planifiée pendant les temps de hello lorsque le volume de hello est monté, s’exécute une fois que le volume de récupération hello est déchargé.</span><span class="sxs-lookup"><span data-stu-id="62b03-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="62b03-194">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="62b03-194">Troubleshooting</span></span>
<span data-ttu-id="62b03-195">Si Azure Backup n’est pas monté correctement reconstitution hello même après plusieurs minutes, d’un clic sur **de montage** ou le volume de reprise toomount hello échoue avec une ou plusieurs erreurs, suivez les étapes de hello ci-dessous toobegin récupération normalement.</span><span class="sxs-lookup"><span data-stu-id="62b03-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="62b03-196">Annuler le processus de montage en cours de hello au cas où il a été exécuté pendant plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="62b03-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="62b03-197">Vérifiez que vous êtes sur la version la plus récente de l’agent de sauvegarde Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="62b03-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="62b03-198">toofind des informations de version hello d’Azure Backup agent, cliquez sur **sur Microsoft Azure Recovery Services Agent** sur hello **Actions** volet de Microsoft Azure Backup de la console et vérifiez que hello  **Version** nombre est égal tooor ultérieure à la version de hello mentionnée dans [cet article](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="62b03-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="62b03-199">Vous pouvez télécharger la version la plus récente à partir de hello [ici](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="62b03-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="62b03-200">Accédez trop**le Gestionnaire de périphériques** -> **contrôleurs de stockage** et assurez-vous que vous pouvez localiser **initiateur Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="62b03-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="62b03-201">Si vous pouvez le localiser, accéder directement toostep 7 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="62b03-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="62b03-202">Si vous ne trouvez pas le service Microsoft iSCSI Initiator comme indiqué à l’étape 3, vérifiez toosee si vous pouvez trouver une entrée sous **le Gestionnaire de périphériques** -> **contrôleurs de stockage** appelée  **APPAREIL inconnu** avec l’ID de matériel **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="62b03-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="62b03-203">Cliquez avec le bouton droit sur l’entrée **Appareil inconnu** et sélectionnez **Mettre à jour le pilote**.</span><span class="sxs-lookup"><span data-stu-id="62b03-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="62b03-204">Pilote hello de mise à jour par l’option hello trop **rechercher automatiquement un pilote mis à jour**.</span><span class="sxs-lookup"><span data-stu-id="62b03-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="62b03-205">Fin de la mise à jour hello doit modifier **périphérique inconnu** trop**initiateur Microsoft iSCSI** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="62b03-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Chiffrement](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="62b03-207">Accédez trop**le Gestionnaire des tâches** -> **Services (Local)** -> **Service initiateur Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="62b03-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Chiffrement](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="62b03-209">Redémarrez le service de Microsoft iSCSI Initiator hello en cliquant sur service hello, en cliquant sur **arrêter** et à nouveau le bouton droit et en cliquant sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="62b03-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="62b03-210">Recommencez la récupération à l’aide de la restauration instantanée.</span><span class="sxs-lookup"><span data-stu-id="62b03-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="62b03-211">Si la récupération de hello échoue encore, redémarrez votre serveur/client.</span><span class="sxs-lookup"><span data-stu-id="62b03-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="62b03-212">Si un redémarrage n’est pas souhaitable ou récupération de hello persiste même après le redémarrage du serveur de hello, essayez de récupérer à partir d’un autre ordinateur et contactez le Support de Azure en accédant trop[portail Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) et soumettre une demande de support.</span><span class="sxs-lookup"><span data-stu-id="62b03-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62b03-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62b03-213">Next steps</span></span>
* <span data-ttu-id="62b03-214">Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="62b03-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
