---
title: "aaaBack des tooAzure d’état Windows système | Documents Microsoft"
description: "En savoir plus tooback état du système de Windows Server et/ou tooAzure des ordinateurs Windows hello."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "Comment toobackup ; Comment tooback ; sauvegarde des fichiers et dossiers"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="eaf76-104">Sauvegarder l’état du système Windows dans un déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eaf76-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="eaf76-105">Cet article explique comment l’état tooAzure tooback de votre système Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eaf76-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="eaf76-106">Il s’agit d’un didacticiel toowalk prévue vous guident dans les principes de base hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="eaf76-107">Si vous souhaitez tooknow plus d’informations sur Azure Backup, lire ce [vue d’ensemble](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="eaf76-108">Si vous ne disposez pas d’un abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) pour accéder à n’importe quel service Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="eaf76-109">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="eaf76-109">Create a recovery services vault</span></span>
<span data-ttu-id="eaf76-110">tooback des fichiers et des dossiers, vous devez toocreate un coffre de Services de récupération dans la région de hello où vous souhaitez toostore hello données.</span><span class="sxs-lookup"><span data-stu-id="eaf76-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="eaf76-111">Vous devez également toodetermine comment vous souhaitez que votre stockage répliqué.</span><span class="sxs-lookup"><span data-stu-id="eaf76-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="eaf76-112">toocreate un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="eaf76-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="eaf76-113">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="eaf76-114">Dans le menu du Hub hello, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Services de récupération** et cliquez sur **les coffres de Services de récupération**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="eaf76-116">S’il existe des coffres des services de récupération dans l’abonnement de hello, coffres de hello sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="eaf76-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="eaf76-117">Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="eaf76-119">Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Créer un coffre Recovery Services - Étape 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="eaf76-121">Pour **nom**, entrez un coffre de hello tooidentify nom convivial.</span><span class="sxs-lookup"><span data-stu-id="eaf76-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="eaf76-122">nom de Hello doit toobe unique pour hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="eaf76-123">Tapez un nom contenant entre 2 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="eaf76-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="eaf76-124">Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="eaf76-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="eaf76-125">Bonjour **abonnement** section, utilisez hello toochoose de menu déroulant hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="eaf76-126">Si vous N'utilisez qu’un seul abonnement, cet abonnement s’affiche et vous pouvez ignorer toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="eaf76-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="eaf76-127">Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement.</span><span class="sxs-lookup"><span data-stu-id="eaf76-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="eaf76-128">Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="eaf76-129">Bonjour **groupe de ressources** section :</span><span class="sxs-lookup"><span data-stu-id="eaf76-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="eaf76-130">Sélectionnez **nouvel** si vous voulez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="eaf76-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="eaf76-131">Ou</span><span class="sxs-lookup"><span data-stu-id="eaf76-131">Or</span></span>
    * <span data-ttu-id="eaf76-132">Sélectionnez **utiliser l’existante** sur hello menu déroulant toosee hello disponible liste des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="eaf76-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="eaf76-133">Pour plus d’informations sur les groupes de ressources, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="eaf76-134">Cliquez sur **emplacement** tooselect hello région pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="eaf76-135">Ce choix détermine la région géographique de hello où vos données de sauvegarde sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="eaf76-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="eaf76-136">Au bas de hello du Panneau de coffre Recovery Services hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="eaf76-137">Il peut prendre plusieurs minutes pour hello que toobe créé de coffre de Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="eaf76-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="eaf76-138">Surveiller les notifications d’état hello dans la zone de droite supérieure hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="eaf76-139">Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="eaf76-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="eaf76-140">Si vous ne voyez pas votre coffre après quelques minutes, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Bouton Actualiser](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="eaf76-142">Une fois que vous voyez votre coffre dans la liste hello des archivages de Recovery Services, vous êtes prêt tooset une redondance de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="eaf76-143">Définir une redondance de stockage pour l’archivage de hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="eaf76-144">Lorsque vous créez un coffre Recovery Services, assurez-vous de redondance du stockage est configuré hello librement.</span><span class="sxs-lookup"><span data-stu-id="eaf76-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="eaf76-145">À partir de hello **les coffres de Services de récupération** panneau, cliquez sur le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Sélectionnez le coffre hello dans liste hello du coffre Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="eaf76-147">Lorsque vous sélectionnez le coffre de hello, hello **de coffre Recovery Services** panneau restreint et panneau de paramètres hello (*qui a le nom hello du coffre de hello de haut hello*) et le panneau de détails du coffre hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="eaf76-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Afficher la configuration du stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="eaf76-149">Dans le panneau des paramètres du coffre hello nouvelle tooscroll de diapositive vertical hello toohello section gérer vers le bas, puis cliquez sur **Infrastructure de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="eaf76-150">panneau d’Infrastructure de sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="eaf76-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="eaf76-151">Dans le panneau d’Infrastructure de sauvegarde hello, cliquez sur **Configuration de la sauvegarde** tooopen hello **Configuration de la sauvegarde** panneau.</span><span class="sxs-lookup"><span data-stu-id="eaf76-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Définir la configuration de stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="eaf76-153">Choisissez l’option de réplication de stockage approprié de hello pour votre coffre.</span><span class="sxs-lookup"><span data-stu-id="eaf76-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Options de configuration du stockage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="eaf76-155">Par défaut, votre archivage utilise un stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="eaf76-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="eaf76-156">Si vous utilisez Azure comme un point de terminaison principal de stockage de sauvegarde, continuer toouse **géo-redondant**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="eaf76-157">Si vous n’utilisez pas Azure comme un point de terminaison principal de stockage de sauvegarde, puis choisissez **localement redondant**, ce qui réduit les coûts de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="eaf76-158">Pour en savoir plus sur les options de stockage [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage), consultez la [présentation de la redondance du stockage](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="eaf76-159">Une fois votre coffre créé, vous devez le configurer pour la sauvegarde de l’état du système Windows.</span><span class="sxs-lookup"><span data-stu-id="eaf76-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="eaf76-160">Configurer le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-160">Configure hello vault</span></span>
1. <span data-ttu-id="eaf76-161">On hello panneau du coffre Recovery Services (pour hello coffre vous venez de créer), dans la section prise en main de hello, cliquez sur **sauvegarde**, puis sur hello **mise en route de la sauvegarde** panneau, sélectionnez  **Objectif de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="eaf76-163">Hello **sauvegarde objectif** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="eaf76-163">hello **Backup Goal** blade opens.</span></span>

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="eaf76-165">À partir de hello **votre charge de travail exécutant ?** menu déroulant, sélectionnez **local**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="eaf76-166">En effet, vous devez choisir l’option **Local**, car votre ordinateur Windows Server ou Windows est une machine physique, qui ne se trouve donc pas dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf76-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="eaf76-167">À partir de hello **comment vous souhaitez toobackup ?** menu, sélectionnez **état du système**et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Configuration des fichiers et dossiers](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="eaf76-169">Après avoir cliqué sur OK, une coche apparaît en regard trop**objectif de sauvegarde**et hello **Prepare infrastructure** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="eaf76-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Objectif de sauvegarde configuré, début de préparation de l’infrastructure](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="eaf76-171">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger l’Agent pour Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="eaf76-173">Si vous utilisez Windows Server essentiels, puis choisissez toodownload hello agent essentielles de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eaf76-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="eaf76-174">Un menu contextuel vous invite toorun ou enregistrer MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="eaf76-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Boîte de dialogue MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="eaf76-176">Dans le menu contextuel du téléchargement hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="eaf76-177">Par défaut, hello **MARSagentinstaller.exe** fichier est enregistré le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="eaf76-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="eaf76-178">Lorsque le programme d’installation hello est terminée, vous verrez un message vous demandant si vous souhaitez que le programme d’installation de toorun hello ou ouvrez le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="eaf76-180">Vous n’avez pas encore l’agent de tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="eaf76-181">Vous pouvez installer l’agent de hello après avoir téléchargé les informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="eaf76-182">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Télécharger les informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="eaf76-184">informations d’identification de coffre Hello téléchargement le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="eaf76-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="eaf76-185">Une fois les informations d’identification de coffre hello terminer le téléchargement, vous voyez un message vous demandant si vous souhaitez tooopen ou enregistrez les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="eaf76-186">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-186">Click **Save**.</span></span> <span data-ttu-id="eaf76-187">Si vous cliquez accidentellement sur **ouvrir**, permettent de boîte de dialogue hello qui tente d’informations d’identification du coffre tooopen hello donc pas.</span><span class="sxs-lookup"><span data-stu-id="eaf76-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="eaf76-188">Impossible d’ouvrir des informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="eaf76-189">Passez maintenant toohello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-189">Proceed toohello next step.</span></span> <span data-ttu-id="eaf76-190">informations d’identification de coffre Hello se trouvent dans le dossier Téléchargements de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Fin du téléchargement des informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="eaf76-192">Installer et inscrire l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="eaf76-193">Activer la sauvegarde via hello portail Azure n’est pas encore disponible.</span><span class="sxs-lookup"><span data-stu-id="eaf76-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="eaf76-194">Utilisez hello Microsoft Azure Recovery Services Agent tooback état du système Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eaf76-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="eaf76-195">Recherchez et double-cliquez sur hello **MARSagentinstaller.exe** de téléchargements de hello dossier (ou tout autre emplacement enregistré).</span><span class="sxs-lookup"><span data-stu-id="eaf76-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="eaf76-196">programme d’installation Hello fournit une série de messages qu’il extrait, installe et enregistre hello Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="eaf76-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Informations d’identification de programme d’installation de l’agent Recovery Services exécuté](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="eaf76-198">Assistant Installation de Microsoft Azure Recovery Services Agent de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="eaf76-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="eaf76-199">Assistant de hello toocomplete, vous devez :</span><span class="sxs-lookup"><span data-stu-id="eaf76-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="eaf76-200">Choisissez un emplacement pour le dossier d’installation et de cache hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="eaf76-201">Fournir les informations du serveur de votre proxy si vous utilisez un toohello tooconnect du serveur proxy internet.</span><span class="sxs-lookup"><span data-stu-id="eaf76-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="eaf76-202">Fournir votre nom d’utilisateur et votre mot de passe si vous utilisez un proxy authentifié.</span><span class="sxs-lookup"><span data-stu-id="eaf76-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="eaf76-203">Fournir des informations d’identification de coffre hello téléchargé</span><span class="sxs-lookup"><span data-stu-id="eaf76-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="eaf76-204">Enregistrer la phrase secrète de chiffrement hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="eaf76-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eaf76-205">Si vous perdez ou oubliez le mot de passe hello, Microsoft ne peut pas aider à récupérer les données de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="eaf76-206">Enregistrez le fichier de hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="eaf76-206">Save hello file in a secure location.</span></span> <span data-ttu-id="eaf76-207">Il est requis toorestore une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="eaf76-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="eaf76-208">Hello agent est installé et que votre ordinateur est inscrit toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="eaf76-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="eaf76-209">Vous êtes prêt tooconfigure et planifiez votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="eaf76-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="eaf76-210">Sauvegarder l’état du système Windows Server (préversion)</span><span class="sxs-lookup"><span data-stu-id="eaf76-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="eaf76-211">la sauvegarde initiale Hello inclut trois tâches :</span><span class="sxs-lookup"><span data-stu-id="eaf76-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="eaf76-212">Activer la sauvegarde de l’état système à l’aide de l’agent de sauvegarde Azure hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="eaf76-213">Planifier la sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-213">Schedule hello backup</span></span>
* <span data-ttu-id="eaf76-214">Sauvegarder des fichiers et des dossiers pour hello première fois</span><span class="sxs-lookup"><span data-stu-id="eaf76-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="eaf76-215">sauvegarde initiale toocomplete hello, utilisez hello Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="eaf76-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="eaf76-216">sauvegarde de l’état du système de tooenable à l’aide de l’agent de sauvegarde Azure hello</span><span class="sxs-lookup"><span data-stu-id="eaf76-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="eaf76-217">Dans une session PowerShell, exécutez hello suivant du moteur de commande toostop hello Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="eaf76-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="eaf76-218">Ouvrez hello du Registre Windows.</span><span class="sxs-lookup"><span data-stu-id="eaf76-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="eaf76-219">Add hello clé de Registre avec hello suivante spécifiée de la valeur DWord.</span><span class="sxs-lookup"><span data-stu-id="eaf76-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="eaf76-220">Chemin d’accès au Registre</span><span class="sxs-lookup"><span data-stu-id="eaf76-220">Registry path</span></span> | <span data-ttu-id="eaf76-221">Clé de Registre</span><span class="sxs-lookup"><span data-stu-id="eaf76-221">Registry key</span></span> | <span data-ttu-id="eaf76-222">Valeur DWord</span><span class="sxs-lookup"><span data-stu-id="eaf76-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="eaf76-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="eaf76-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="eaf76-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="eaf76-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="eaf76-225">2</span><span class="sxs-lookup"><span data-stu-id="eaf76-225">2</span></span> |

4. <span data-ttu-id="eaf76-226">Redémarrez le moteur de sauvegarde hello en exécutant hello suivant de commande dans une invite de commandes avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="eaf76-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="eaf76-227">travail de sauvegarde hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="eaf76-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="eaf76-228">Ouvrez l’agent de Microsoft Azure Recovery Services hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="eaf76-229">Vous pouvez le trouver en recherchant **Sauvegarde Microsoft Azure**sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eaf76-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Lancer hello Azure Recovery Services agent](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="eaf76-231">Dans l’agent Recovery Services hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="eaf76-233">Sur hello mise en route de la page de hello Assistant Planification de sauvegarde, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="eaf76-234">Page de tooBackup hello sélectionner les éléments, cliquez sur **ajouter les éléments**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="eaf76-235">Sélectionnez **État du système**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="eaf76-236">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-236">Click **Next**.</span></span>

7. <span data-ttu-id="eaf76-237">Hello planification de rétention et de sauvegarde de l’état système est automatiquement définie tooback de tous les dimanches à 9 h 00, heure locale, et la valeur de période de rétention hello too60 jours.</span><span class="sxs-lookup"><span data-stu-id="eaf76-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eaf76-238">La stratégie de sauvegarde et de rétention de l’état du système est configurée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="eaf76-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="eaf76-239">Si vous sauvegardez les fichiers et dossiers en outre état toohello du système de serveur Windows, spécifiez la stratégie de sauvegarde et de rétention hello uniquement pour les sauvegardes de fichiers à partir de l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="eaf76-240">Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="eaf76-241">Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="eaf76-242">tooback état du système Windows Server pour hello première fois</span><span class="sxs-lookup"><span data-stu-id="eaf76-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="eaf76-243">Vérifiez qu’aucune mise à jour de Windows Server nécessitant un redémarrage n’est en attente.</span><span class="sxs-lookup"><span data-stu-id="eaf76-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="eaf76-244">Dans l’agent Recovery Services hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Sauvegarder Windows Server maintenant](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="eaf76-246">Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="eaf76-247">puis cliquez sur **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="eaf76-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="eaf76-248">Cliquez sur **fermer** Assistant de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="eaf76-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="eaf76-249">Si vous fermez l’Assistant de hello avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="eaf76-250">Si vous sauvegardez des fichiers et dossiers sur votre serveur, en outre toohello Windows Server System State, Assistant sauvegarder maintenant hello sera uniquement sauvegarder les fichiers.</span><span class="sxs-lookup"><span data-stu-id="eaf76-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="eaf76-251">tooperform un état du système ad hoc sauvegarder, utilisez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="eaf76-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="eaf76-252">Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![RI terminé](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="eaf76-254">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="eaf76-254">Frequently asked questions</span></span>

<span data-ttu-id="eaf76-255">Hello questions et réponses suivantes fournissent des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="eaf76-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="eaf76-256">Nouveautés hello Volume de mise en lots</span><span class="sxs-lookup"><span data-stu-id="eaf76-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="eaf76-257">Hello Volume de mise en lots représente un emplacement intermédiaire de hello où hello disponible en mode natif, sauvegarde de Windows Server prépare hello sauvegarde de l’état système.</span><span class="sxs-lookup"><span data-stu-id="eaf76-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="eaf76-258">Azure Backup agent puis compresse et chiffre cette sauvegarde intermédiaire et envoie que via toohello de protocole HTTPS sécurisée configuré coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="eaf76-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="eaf76-259">**Nous vous recommandons vivement de que vous établissez hello Volume de mise en lots dans un volume non--système d’exploitation Windows. Si vous notez des problèmes avec les sauvegardes d’état du système, la vérification d’emplacement hello de votre Volume de mise en lots est première étape de dépannage hello.**</span><span class="sxs-lookup"><span data-stu-id="eaf76-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="eaf76-260">Comment puis-je modifier hello chemin d’accès du Volume intermédiaire spécifié dans l’agent de sauvegarde Azure hello ?</span><span class="sxs-lookup"><span data-stu-id="eaf76-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="eaf76-261">Hello Volume de mise en attente se trouve dans le dossier de cache hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="eaf76-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="eaf76-262">toochange cet emplacement, hello utilisez commande (dans une invite de commandes avec élévation de privilèges) suivante :</span><span class="sxs-lookup"><span data-stu-id="eaf76-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="eaf76-263">Puis mettez à jour hello suivant des entrées de Registre avec hello chemin d’accès toohello nouveau Volume de mise en lots dossier.</span><span class="sxs-lookup"><span data-stu-id="eaf76-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="eaf76-264">Chemin d’accès au Registre</span><span class="sxs-lookup"><span data-stu-id="eaf76-264">Registry path</span></span>|<span data-ttu-id="eaf76-265">Clé de Registre</span><span class="sxs-lookup"><span data-stu-id="eaf76-265">Registry key</span></span>|<span data-ttu-id="eaf76-266">Valeur</span><span class="sxs-lookup"><span data-stu-id="eaf76-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="eaf76-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="eaf76-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="eaf76-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="eaf76-268">SSBStagingPath</span></span> | <span data-ttu-id="eaf76-269">nouvel emplacement du volume intermédiaire</span><span class="sxs-lookup"><span data-stu-id="eaf76-269">new staging volume location</span></span> |

<span data-ttu-id="eaf76-270">Hello chemin d’accès de mise en lots respecte la casse et doit être hello même casse que celui qui existe sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="eaf76-271">Une fois que vous modifiez le chemin d’accès du volume hello intermédiaire, redémarrez le moteur de sauvegarde hello :</span><span class="sxs-lookup"><span data-stu-id="eaf76-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="eaf76-272">toopick chemin d’accès hello modifié, l’agent de Microsoft Azure Recovery Services hello ouvert et déclencheur une sauvegarde ad hoc de l’état du système.</span><span class="sxs-lookup"><span data-stu-id="eaf76-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="eaf76-273">Pourquoi est-état du système hello rétention par défaut de définir les jours de too60 ?</span><span class="sxs-lookup"><span data-stu-id="eaf76-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="eaf76-274">Hello cycle de vie d’une sauvegarde de l’état système est hello identique au paramètre hello « tombstone lifetime » pour le rôle de Windows Server Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="eaf76-275">valeur par défaut de Hello pour l’entrée de durée de vie de temporisation hello est de 60 jours.</span><span class="sxs-lookup"><span data-stu-id="eaf76-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="eaf76-276">Cette valeur peut être définie sur l’objet de configuration du Service d’annuaire (NTDS) hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="eaf76-277">Comment modifier la valeur par défaut de hello sauvegarde et de la stratégie de rétention pour l’état du système ?</span><span class="sxs-lookup"><span data-stu-id="eaf76-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="eaf76-278">valeur par défaut hello toochange sauvegarde et stratégie de rétention pour l’état du système :</span><span class="sxs-lookup"><span data-stu-id="eaf76-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="eaf76-279">Arrêter le moteur de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-279">Stop hello Backup engine.</span></span> <span data-ttu-id="eaf76-280">Exécutez hello de commande suivante à partir d’une invite de commandes avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="eaf76-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="eaf76-281">Ajouter ou mettre à jour hello suivant des entrées de clé de Registre dans HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="eaf76-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="eaf76-282">Nom de Registre</span><span class="sxs-lookup"><span data-stu-id="eaf76-282">Registry Name</span></span>|<span data-ttu-id="eaf76-283">Description</span><span class="sxs-lookup"><span data-stu-id="eaf76-283">Description</span></span>|<span data-ttu-id="eaf76-284">Valeur</span><span class="sxs-lookup"><span data-stu-id="eaf76-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="eaf76-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="eaf76-285">SSBScheduleTime</span></span>|<span data-ttu-id="eaf76-286">Utilisation de hello tooconfigure de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="eaf76-287">La valeur par défaut est 21h00 heure locale.</span><span class="sxs-lookup"><span data-stu-id="eaf76-287">Default is 9PM local time.</span></span>|<span data-ttu-id="eaf76-288">DWord : format HHMM (décimal), par exemple 2130 pour 21h30 heure locale.</span><span class="sxs-lookup"><span data-stu-id="eaf76-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="eaf76-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="eaf76-289">SSBScheduleDays</span></span>|<span data-ttu-id="eaf76-290">Jours de hello tooconfigure utilisé lorsque sauvegarde de l’état système doit être effectué au hello spécifié de fois.</span><span class="sxs-lookup"><span data-stu-id="eaf76-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="eaf76-291">Des chiffres spécifient les jours de semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="eaf76-292">0 représente le dimanche, 1 le lundi, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="eaf76-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="eaf76-293">Le jour de sauvegarde par défaut est le dimanche.</span><span class="sxs-lookup"><span data-stu-id="eaf76-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="eaf76-294">DWord : les jours de sauvegarde de toorun hello semaine (décimal), par exemple 1230 planifie les sauvegardes sur lundi, mardi, mercredi et dimanche.</span><span class="sxs-lookup"><span data-stu-id="eaf76-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="eaf76-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="eaf76-295">SSBRetentionDays</span></span>|<span data-ttu-id="eaf76-296">Sauvegarde de tooretain tooconfigure utilisé hello jours.</span><span class="sxs-lookup"><span data-stu-id="eaf76-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="eaf76-297">La valeur par défaut est 60.</span><span class="sxs-lookup"><span data-stu-id="eaf76-297">Default value is 60.</span></span> <span data-ttu-id="eaf76-298">La valeur maximale autorisée est 180.</span><span class="sxs-lookup"><span data-stu-id="eaf76-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="eaf76-299">DWord : La sauvegarde de tooretain jours (décimale).</span><span class="sxs-lookup"><span data-stu-id="eaf76-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="eaf76-300">Utilisez hello suivant du moteur de sauvegarde commande toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="eaf76-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="eaf76-301">Ouvrez hello Microsoft Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="eaf76-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="eaf76-302">Cliquez sur **planifier la sauvegarde** puis cliquez sur **suivant** jusqu'à ce que vous voyiez modifications hello soient répercutées.</span><span class="sxs-lookup"><span data-stu-id="eaf76-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="eaf76-303">Cliquez sur **Terminer** modifications de hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="eaf76-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="eaf76-304">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="eaf76-304">Questions?</span></span>
<span data-ttu-id="eaf76-305">Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="eaf76-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf76-306">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eaf76-306">Next steps</span></span>
* <span data-ttu-id="eaf76-307">Approfondissez vos connaissances sur la [sauvegarde de machines Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="eaf76-308">Maintenant que vous avez sauvegardé vos fichiers et vos dossiers, vous pouvez [gérer vos archivages et vos serveurs](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="eaf76-309">Si vous devez toorestore une sauvegarde, utilisez cet article trop[restaurer la machine virtuelle Windows tooa fichiers](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="eaf76-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
