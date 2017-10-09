---
title: "Sauvegarde Azure : Tooa de restaurer l’état système Windows Server | Documents Microsoft"
description: "Explication étape par étape pour la restauration de l’état du système de Windows Server à partir d’une sauvegarde dans Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="a6121-103">Restaurer l’état système tooWindows Server</span><span class="sxs-lookup"><span data-stu-id="a6121-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="a6121-104">Cet article explique comment les sauvegardes d’état du système Windows Server toorestore à partir d’un Azure Recovery Services coffre.</span><span class="sxs-lookup"><span data-stu-id="a6121-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="a6121-105">toorestore état du système, doit avoir une sauvegarde de l’état du système (créé à l’aide d’instructions hello dans [sauvegarder l’état du système](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) et vérifiez que vous avez installé hello [version la plus récente de Microsoft Azure Recovery de hello L’agent de services (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="a6121-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="a6121-106">La récupération des données d’état du système Windows Server à partir d’un coffre Azure Recovery Services est un processus en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="a6121-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="a6121-107">Restaurer l’état du système sous forme de fichiers à partir de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="a6121-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="a6121-108">Lors de la restauration de l’état du système sous forme de fichiers à partir de Sauvegarde Azure, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="a6121-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="a6121-109">Restaurer l’état système toohello même serveur sur lequel les sauvegardes hello ont été effectuées, ou</span><span class="sxs-lookup"><span data-stu-id="a6121-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="a6121-110">Restaurer l’état système fichier tooan autre serveur.</span><span class="sxs-lookup"><span data-stu-id="a6121-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="a6121-111">Appliquer tooa de fichiers hello restauré l’état du système Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a6121-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="a6121-112">Récupération de l’état système de fichiers toohello même serveur</span><span class="sxs-lookup"><span data-stu-id="a6121-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="a6121-113">Hello suit explique comment tooroll sauvegarder votre état précédent de tooa de configuration de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a6121-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="a6121-114">Restauration de votre serveur tooa arrière de configuration connu, l’état stable, peut être extrêmement utile.</span><span class="sxs-lookup"><span data-stu-id="a6121-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="a6121-115">Hello suivant l’état du système du serveur hello étapes restauration à partir d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="a6121-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="a6121-116">Ouvrez hello **Microsoft Azure Backup** enfichable.</span><span class="sxs-lookup"><span data-stu-id="a6121-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="a6121-117">Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="a6121-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="a6121-118">application de bureau Hello doit apparaître dans les résultats de la recherche hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="a6121-119">Cliquez sur **récupérer les données** Assistant de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="a6121-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="a6121-121">Sur hello **mise en route** volet, toorestore hello données toohello même serveur ou ordinateur, sélectionnez **ce serveur (`<server name>`)** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Choisissez cette toohello de données de serveur option toorestore hello même ordinateur](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="a6121-123">Sur hello **sélectionner le Mode de récupération** volet, choisissez **état du système** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Parcourir les fichiers](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="a6121-125">Calendrier hello dans **sélectionner le Volume et la Date** point du volet, sélectionnez une récupération.</span><span class="sxs-lookup"><span data-stu-id="a6121-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="a6121-126">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="a6121-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a6121-127">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="a6121-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="a6121-128">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="a6121-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume et date](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="a6121-130">Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="a6121-131">Sauvegarde Azure monte le point de récupération locaux hello et l’utilise comme un volume de reprise.</span><span class="sxs-lookup"><span data-stu-id="a6121-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="a6121-132">Dans le volet suivant de hello, spécifiez la destination hello pour hello récupérées des fichiers d’état du système, puis cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="a6121-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="a6121-133">Hello option, **créer des copies pour avoir les deux versions**, crée des copies des fichiers individuels dans une archive de fichier de l’état du système existante au lieu de créer la copie de hello de hello totalité l’état du système de l’archive.</span><span class="sxs-lookup"><span data-stu-id="a6121-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Options de récupération](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="a6121-135">Vérifiez les détails de la récupération sur hello hello **Confirmation** volet et cliquez sur **récupérer**.</span><span class="sxs-lookup"><span data-stu-id="a6121-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Cliquez sur récupérer tooacknowledge hello recover action](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="a6121-137">Hello de copie *WindowsImageBackup* répertoire hello volume non critiques tooa destination récupération du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="a6121-138">Hello volume du système d’exploitation Windows est généralement un volume critique de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="a6121-139">Une fois la récupération de hello a réussi, suivez les étapes de hello dans la section de hello, [appliquer restauré toohello de fichiers d’état du système Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello les processus de récupération de l’état du système.</span><span class="sxs-lookup"><span data-stu-id="a6121-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="a6121-140">Récupération de l’état système de fichiers sur un autre serveur tooan</span><span class="sxs-lookup"><span data-stu-id="a6121-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="a6121-141">Si votre serveur Windows est endommagé ou est inaccessible, et vous souhaitez toorestore il état stable de tooa en récupérant hello état du système Windows Server, vous pouvez restaurer l’état du système du serveur hello endommagé à partir d’un autre serveur.</span><span class="sxs-lookup"><span data-stu-id="a6121-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="a6121-142">Utilisez hello suivant les étapes permettant de restaurer toohello état du système sur un serveur distinct.</span><span class="sxs-lookup"><span data-stu-id="a6121-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="a6121-143">terminologie Hello utilisée dans cette procédure inclut :</span><span class="sxs-lookup"><span data-stu-id="a6121-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="a6121-144">*Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.</span><span class="sxs-lookup"><span data-stu-id="a6121-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="a6121-145">*Ordinateur cible* – hello machine toowhich hello données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="a6121-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="a6121-146">*Archivage de l’exemple* – Bonjour Recovery Services coffre toowhich Bonjour *machine Source* et *de l’ordinateur cible* sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="a6121-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="a6121-147">Les sauvegardes effectuées à partir d’un ordinateur ne peut pas être ordinateur restauré tooa exécutant une version antérieure du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="a6121-148">Par exemple, les sauvegardes effectuées à partir d’un ordinateur Windows Server 2016 ordinateur ne peut pas être restaurée tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a6121-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="a6121-149">Toutefois, l’inverse de hello est possible.</span><span class="sxs-lookup"><span data-stu-id="a6121-149">However, hello inverse is possible.</span></span> <span data-ttu-id="a6121-150">Vous pouvez utiliser les sauvegardes à partir de Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a6121-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="a6121-151">Ouvrez hello **Microsoft Azure Backup** enfichable sur hello *de l’ordinateur cible*.</span><span class="sxs-lookup"><span data-stu-id="a6121-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="a6121-152">Vérifiez que hello *de l’ordinateur cible* et hello *machine Source* sont toohello des Services de récupération même coffre.</span><span class="sxs-lookup"><span data-stu-id="a6121-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="a6121-153">Cliquez sur **récupérer les données** flux de travail tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="a6121-155">Sélectionnez **Un autre serveur**</span><span class="sxs-lookup"><span data-stu-id="a6121-155">Select **Another server**</span></span>

    ![Un autre serveur](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="a6121-157">Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*.</span><span class="sxs-lookup"><span data-stu-id="a6121-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="a6121-158">Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a6121-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="a6121-159">Une fois que le fichier d’informations d’identification de coffre hello est fourni, le coffre Recovery Services hello associé au fichier d’informations d’identification de coffre hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a6121-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="a6121-160">Dans le volet de sélectionner un serveur de sauvegarde hello, sélectionnez hello *machine Source* à partir de la liste hello des ordinateurs affichés.</span><span class="sxs-lookup"><span data-stu-id="a6121-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="a6121-162">Dans le volet Sélectionner un Mode de récupération de hello, choisissez **état du système** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="a6121-164">Sur hello calendrier Bonjour **sélectionner le Volume et la Date** point du volet, sélectionnez une récupération.</span><span class="sxs-lookup"><span data-stu-id="a6121-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="a6121-165">Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps.</span><span class="sxs-lookup"><span data-stu-id="a6121-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a6121-166">Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="a6121-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="a6121-167">Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="a6121-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Éléments de recherche](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="a6121-169">Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="a6121-170">Sur hello **sélectionner le Mode de récupération système état** volet, hello destination de l’état du système de fichiers toobe récupérée, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Chiffrement](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="a6121-172">Hello option, **créer des copies pour avoir les deux versions**, crée des copies des fichiers individuels dans une archive de fichier de l’état du système existante au lieu de créer la copie de hello de hello totalité l’état du système de l’archive.</span><span class="sxs-lookup"><span data-stu-id="a6121-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="a6121-173">Vérifiez les détails de la récupération sur le volet de Confirmation hello hello, puis cliquez sur **récupérer**.</span><span class="sxs-lookup"><span data-stu-id="a6121-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Cliquez sur le processus de récupération du bouton tooconfirm hello hello récupérer](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="a6121-175">Hello de copie *WindowsImageBackup* répertoire tooa non critiques volume sur hello serveur (par exemple D:\).</span><span class="sxs-lookup"><span data-stu-id="a6121-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="a6121-176">Hello volume du système d’exploitation Windows est généralement un volume critique de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="a6121-177">processus de récupération toocomplete hello, suivant de hello utilisez section trop[appliquer hello restauré les fichiers de l’état du système sur un serveur Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="a6121-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="a6121-178">Appliquer l’état du système restauré sur un serveur Windows</span><span class="sxs-lookup"><span data-stu-id="a6121-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="a6121-179">Une fois que vous avez récupéré l’état du système sous forme de fichiers à l’aide d’Azure Recovery Services Agent, utilisez hello sauvegarde Windows Server utilitaire tooapply hello récupéré tooWindows d’état du système serveur.</span><span class="sxs-lookup"><span data-stu-id="a6121-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="a6121-180">Hello utilitaire sauvegarde Windows Server est déjà disponible sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="a6121-181">Hello suit explique comment tooapply hello récupérées à l’état du système.</span><span class="sxs-lookup"><span data-stu-id="a6121-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="a6121-182">Les commandes suivantes de hello utilisation tooreboot votre serveur dans *Mode réparation Services d’annuaire*.</span><span class="sxs-lookup"><span data-stu-id="a6121-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="a6121-183">À partir d’une invite de commandes avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="a6121-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="a6121-184">Après le redémarrage de hello, ouvrez le composant logiciel enfichable Sauvegarde Windows Server des hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="a6121-185">Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **sauvegarde Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="a6121-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="a6121-186">application de bureau Hello s’affiche dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="a6121-187">Dans le composant logiciel enfichable hello, sélectionnez **sauvegarde locale**.</span><span class="sxs-lookup"><span data-stu-id="a6121-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Sélectionnez la sauvegarde locale toorestore à partir de là](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="a6121-189">Dans la console de sauvegarde locale hello, Bonjour **volet Actions**, cliquez sur **récupérer** tooopen hello Assistant récupération.</span><span class="sxs-lookup"><span data-stu-id="a6121-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="a6121-190">Sélectionnez l’option de hello, **une sauvegarde stockée dans un autre emplacement**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Choisissez toorecover tooa autre serveur](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="a6121-192">Lorsque vous spécifiez le type d’emplacement hello, sélectionnez **dossier partagé distant** si votre sauvegarde de l’état du système a été récupérée tooanother server.</span><span class="sxs-lookup"><span data-stu-id="a6121-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="a6121-193">Si l’état du système a été récupéré localement, sélectionnez **Lecteurs locaux**.</span><span class="sxs-lookup"><span data-stu-id="a6121-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Sélectionnez si toorecovery de serveur local ou un autre](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="a6121-195">Entrez hello chemin d’accès toohello *WindowsImageBackup* active, ou cliquez sur le disque local hello contenant ce répertoire (par exemple, D:\WindowsImageBackup), récupéré en tant que partie de la récupération de fichiers hello état du système à l’aide de la récupération d’Azure L’Agent et cliquez sur services **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![chemin d’accès fichier partagé toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="a6121-197">Version de l’état du système hello SELECT que vous souhaitez toorestore, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="a6121-198">Dans le volet de sélectionner le Type de récupération hello, sélectionnez **état du système** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="a6121-199">Pour l’emplacement de hello Hello récupérer l’état du système, sélectionnez **emplacement d’origine**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a6121-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="a6121-200">Passez en revue les détails de confirmation hello, vérifiez les paramètres de redémarrage hello, puis cliquez sur **récupérer** tooapplly hello restauration des fichiers de l’état du système.</span><span class="sxs-lookup"><span data-stu-id="a6121-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![lancement hello restaurer les fichiers de l’état du système](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="a6121-202">Considérations spéciales pour la récupération de l’état du système sur le serveur Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6121-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="a6121-203">La sauvegarde de l’état du système inclut les données Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6121-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="a6121-204">Utilisez hello suivant les étapes toorestore Service de domaine Active Directory (AD DS) dans son état précédent du tooa état actuel.</span><span class="sxs-lookup"><span data-stu-id="a6121-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="a6121-205">Redémarrez le contrôleur de domaine hello dans le Mode restauration des Services d’annuaire (DSRM).</span><span class="sxs-lookup"><span data-stu-id="a6121-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="a6121-206">Suivez les étapes de hello [ici](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover applets de commande de sauvegarde de Windows Server toouse les services AD DS.</span><span class="sxs-lookup"><span data-stu-id="a6121-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="a6121-207">Résoudre les problèmes d’échec de restauration de l’état du système</span><span class="sxs-lookup"><span data-stu-id="a6121-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="a6121-208">Si le processus précédent de hello de l’application de l’état du système ne se termine pas correctement, vous pouvez utiliser hello environnement de récupération Windows (Windows RE) toorecover votre serveur Windows.</span><span class="sxs-lookup"><span data-stu-id="a6121-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="a6121-209">Hello étapes suivantes expliquent comment toorecover à l’aide de remporter de RE.</span><span class="sxs-lookup"><span data-stu-id="a6121-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="a6121-210">Utilisez cette option uniquement si Windows Server ne démarre pas normalement après une restauration de l’état du système.</span><span class="sxs-lookup"><span data-stu-id="a6121-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="a6121-211">Hello suivant processus efface les données non système, soyez prudent.</span><span class="sxs-lookup"><span data-stu-id="a6121-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="a6121-212">Démarre votre serveur Windows hello environnement de récupération Windows (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="a6121-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="a6121-213">Sélectionnez le dépannage de hello trois options.</span><span class="sxs-lookup"><span data-stu-id="a6121-213">Select Troubleshoot from hello three available options.</span></span>

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="a6121-215">À partir de hello **Options avancées** écran, sélectionnez **invite de commandes** et fournir le nom d’utilisateur administrateur hello serveur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a6121-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![ouverture du menu](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="a6121-217">Fournir le mot de passe et le nom d’utilisateur administrateur hello serveur.</span><span class="sxs-lookup"><span data-stu-id="a6121-217">Provide hello server administrator username and password.</span></span>

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="a6121-219">Lorsque vous ouvrez l’invite de commandes hello en mode administrateur, exécutez après les versions de sauvegarde de l’état du système de commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="a6121-221">Exécutez hello suivant commande tooget tous les volumes disponibles dans la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="a6121-223">Hello commande suivante récupère tous les volumes qui font partie de la sauvegarde de l’état système de hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="a6121-224">Notez que cette étape récupère uniquement hello volumes critiques qui font partie de l’état du système hello.</span><span class="sxs-lookup"><span data-stu-id="a6121-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="a6121-225">Toutes les données autres que les données système sont effacées.</span><span class="sxs-lookup"><span data-stu-id="a6121-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="a6121-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6121-227">Next steps</span></span>
* <span data-ttu-id="a6121-228">Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="a6121-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
