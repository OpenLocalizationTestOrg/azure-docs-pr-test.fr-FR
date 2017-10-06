---
title: aaaBack des tooAzure Windows les fichiers et dossiers (Gestionnaire de ressources) | Documents Microsoft
description: "En savoir plus tooback des tooAzure de fichiers et dossiers de Windows dans un déploiement du Gestionnaire de ressources."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Comment toobackup ; Comment tooback ; sauvegarde des fichiers et dossiers"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="5518c-104">Premier aperçu : sauvegarder des fichiers et des dossiers dans un déploiement de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5518c-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="5518c-105">Cet article explique comment tooAzure tooback votre Windows Server (ou un ordinateur Windows) les fichiers et dossiers à l’aide d’un déploiement du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="5518c-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="5518c-106">Il s’agit d’un didacticiel toowalk prévue vous guident dans les principes de base hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="5518c-107">Si vous souhaitez tooget démarré à l’aide de la sauvegarde Azure, vous êtes au bon endroit de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="5518c-108">Si vous souhaitez tooknow plus d’informations sur Azure Backup, lire ce [vue d’ensemble](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="5518c-109">Si vous ne disposez pas d’un abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) pour accéder à n’importe quel service Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5518c-110">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5518c-110">Create a recovery services vault</span></span>
<span data-ttu-id="5518c-111">tooback des fichiers et des dossiers, vous devez toocreate un coffre de Services de récupération dans la région de hello où vous souhaitez toostore hello données.</span><span class="sxs-lookup"><span data-stu-id="5518c-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="5518c-112">Vous devez également toodetermine comment vous souhaitez que votre stockage répliqué.</span><span class="sxs-lookup"><span data-stu-id="5518c-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="5518c-113">toocreate un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5518c-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="5518c-114">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="5518c-115">Dans le menu du Hub hello, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Services de récupération** et cliquez sur **les coffres de Services de récupération**.</span><span class="sxs-lookup"><span data-stu-id="5518c-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="5518c-117">S’il existe des coffres des services de récupération dans l’abonnement de hello, coffres de hello sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="5518c-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="5518c-118">Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5518c-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="5518c-120">Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="5518c-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Créer un coffre Recovery Services - Étape 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="5518c-122">Pour **nom**, entrez un coffre de hello tooidentify nom convivial.</span><span class="sxs-lookup"><span data-stu-id="5518c-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="5518c-123">nom de Hello doit toobe unique pour hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="5518c-124">Tapez un nom contenant entre 2 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="5518c-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="5518c-125">Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="5518c-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="5518c-126">Bonjour **abonnement** section, utilisez hello toochoose de menu déroulant hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="5518c-127">Si vous N'utilisez qu’un seul abonnement, cet abonnement s’affiche et vous pouvez ignorer toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="5518c-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="5518c-128">Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement.</span><span class="sxs-lookup"><span data-stu-id="5518c-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="5518c-129">Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="5518c-130">Bonjour **groupe de ressources** section :</span><span class="sxs-lookup"><span data-stu-id="5518c-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="5518c-131">Sélectionnez **nouvel** si vous voulez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5518c-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="5518c-132">Ou</span><span class="sxs-lookup"><span data-stu-id="5518c-132">Or</span></span>
    * <span data-ttu-id="5518c-133">Sélectionnez **utiliser l’existante** sur hello menu déroulant toosee hello disponible liste des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="5518c-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="5518c-134">Pour plus d’informations sur les groupes de ressources, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="5518c-135">Cliquez sur **emplacement** tooselect hello région pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="5518c-136">Ce choix détermine la région géographique de hello où vos données de sauvegarde sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="5518c-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="5518c-137">Au bas de hello du Panneau de coffre Recovery Services hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="5518c-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="5518c-138">Il peut prendre plusieurs minutes pour hello que toobe créé de coffre de Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="5518c-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="5518c-139">Surveiller les notifications d’état hello dans la zone de droite supérieure hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="5518c-140">Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="5518c-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="5518c-141">Si vous ne voyez pas votre coffre après quelques minutes, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="5518c-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Bouton Actualiser](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="5518c-143">Une fois que vous voyez votre coffre dans la liste hello des archivages de Recovery Services, vous êtes prêt tooset une redondance de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="5518c-144">Définir une redondance de stockage pour l’archivage de hello</span><span class="sxs-lookup"><span data-stu-id="5518c-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="5518c-145">Lorsque vous créez un coffre Recovery Services, assurez-vous de redondance du stockage est configuré hello librement.</span><span class="sxs-lookup"><span data-stu-id="5518c-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="5518c-146">À partir de hello **les coffres de Services de récupération** panneau, cliquez sur le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Sélectionnez le coffre hello dans liste hello du coffre Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="5518c-148">Lorsque vous sélectionnez le coffre de hello, hello **de coffre Recovery Services** panneau restreint et panneau de paramètres hello (*qui a le nom hello du coffre de hello de haut hello*) et le panneau de détails du coffre hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="5518c-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Afficher la configuration du stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="5518c-150">Dans le panneau des paramètres du coffre hello nouvelle tooscroll de diapositive vertical hello toohello section gérer vers le bas, puis cliquez sur **Infrastructure de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5518c-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="5518c-151">panneau d’Infrastructure de sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5518c-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="5518c-152">Dans le panneau d’Infrastructure de sauvegarde hello, cliquez sur **Configuration de la sauvegarde** tooopen hello **Configuration de la sauvegarde** panneau.</span><span class="sxs-lookup"><span data-stu-id="5518c-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Définir la configuration de stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="5518c-154">Choisissez l’option de réplication de stockage approprié de hello pour votre coffre.</span><span class="sxs-lookup"><span data-stu-id="5518c-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Options de configuration du stockage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="5518c-156">Par défaut, votre archivage utilise un stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="5518c-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="5518c-157">Si vous utilisez Azure comme un point de terminaison principal de stockage de sauvegarde, continuer toouse **géo-redondant**.</span><span class="sxs-lookup"><span data-stu-id="5518c-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="5518c-158">Si vous n’utilisez pas Azure comme un point de terminaison principal de stockage de sauvegarde, puis choisissez **localement redondant**, ce qui réduit les coûts de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="5518c-159">Pour en savoir plus sur les options de stockage [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage), consultez la [présentation de la redondance du stockage](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="5518c-160">Une fois votre coffre créé, vous devez le configurer pour la sauvegarde des fichiers et dossiers.</span><span class="sxs-lookup"><span data-stu-id="5518c-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="5518c-161">Configurer le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="5518c-161">Configure hello vault</span></span>
1. <span data-ttu-id="5518c-162">On hello panneau du coffre Recovery Services (pour hello coffre vous venez de créer), dans la section prise en main de hello, cliquez sur **sauvegarde**, puis sur hello **mise en route de la sauvegarde** panneau, sélectionnez  **Objectif de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5518c-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="5518c-164">Hello **sauvegarde objectif** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5518c-164">hello **Backup Goal** blade opens.</span></span>

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="5518c-166">À partir de hello **votre charge de travail exécutant ?** menu déroulant, sélectionnez **local**.</span><span class="sxs-lookup"><span data-stu-id="5518c-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="5518c-167">En effet, vous devez choisir l’option **Local**, car votre ordinateur Windows Server ou Windows est une machine physique, qui ne se trouve donc pas dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5518c-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="5518c-168">À partir de hello **comment vous souhaitez toobackup ?** menu, sélectionnez **fichiers et dossiers**et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5518c-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Configuration des fichiers et dossiers](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="5518c-170">Après avoir cliqué sur OK, une coche apparaît en regard trop**objectif de sauvegarde**et hello **Prepare infrastructure** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5518c-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Objectif de sauvegarde configuré, début de préparation de l’infrastructure](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="5518c-172">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger l’Agent pour Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="5518c-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="5518c-174">Si vous utilisez Windows Server essentiels, puis choisissez toodownload hello agent essentielles de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5518c-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="5518c-175">Un menu contextuel vous invite toorun ou enregistrer MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="5518c-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Boîte de dialogue MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="5518c-177">Dans le menu contextuel du téléchargement hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5518c-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="5518c-178">Par défaut, hello **MARSagentinstaller.exe** fichier est enregistré le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="5518c-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="5518c-179">Lorsque le programme d’installation hello est terminée, vous verrez un message vous demandant si vous souhaitez que le programme d’installation de toorun hello ou ouvrez le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="5518c-181">Vous n’avez pas encore l’agent de tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="5518c-182">Vous pouvez installer l’agent de hello après avoir téléchargé les informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="5518c-183">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="5518c-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Télécharger les informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="5518c-185">informations d’identification de coffre Hello téléchargement le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="5518c-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="5518c-186">Une fois les informations d’identification de coffre hello terminer le téléchargement, vous voyez un message vous demandant si vous souhaitez tooopen ou enregistrez les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="5518c-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5518c-187">Click **Save**.</span></span> <span data-ttu-id="5518c-188">Si vous cliquez accidentellement sur **ouvrir**, permettent de boîte de dialogue hello qui tente d’informations d’identification du coffre tooopen hello donc pas.</span><span class="sxs-lookup"><span data-stu-id="5518c-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="5518c-189">Impossible d’ouvrir des informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="5518c-190">Passez maintenant toohello.</span><span class="sxs-lookup"><span data-stu-id="5518c-190">Proceed toohello next step.</span></span> <span data-ttu-id="5518c-191">informations d’identification de coffre Hello se trouvent dans le dossier Téléchargements de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Fin du téléchargement des informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="5518c-193">Installer et inscrire l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="5518c-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="5518c-194">Activer la sauvegarde via hello portail Azure n’est pas encore disponible.</span><span class="sxs-lookup"><span data-stu-id="5518c-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="5518c-195">Utilisez tooback de Microsoft Azure Recovery Services Agent hello des fichiers et des dossiers.</span><span class="sxs-lookup"><span data-stu-id="5518c-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="5518c-196">Recherchez et double-cliquez sur hello **MARSagentinstaller.exe** de téléchargements de hello dossier (ou tout autre emplacement enregistré).</span><span class="sxs-lookup"><span data-stu-id="5518c-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="5518c-197">programme d’installation Hello fournit une série de messages qu’il extrait, installe et enregistre hello Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="5518c-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Informations d’identification de programme d’installation de l’agent Recovery Services exécuté](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="5518c-199">Assistant Installation de Microsoft Azure Recovery Services Agent de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="5518c-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="5518c-200">Assistant de hello toocomplete, vous devez :</span><span class="sxs-lookup"><span data-stu-id="5518c-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="5518c-201">Choisissez un emplacement pour le dossier d’installation et de cache hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="5518c-202">Fournir les informations du serveur de votre proxy si vous utilisez un toohello tooconnect du serveur proxy internet.</span><span class="sxs-lookup"><span data-stu-id="5518c-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="5518c-203">Fournir votre nom d’utilisateur et votre mot de passe si vous utilisez un proxy authentifié.</span><span class="sxs-lookup"><span data-stu-id="5518c-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="5518c-204">Fournir des informations d’identification de coffre hello téléchargé</span><span class="sxs-lookup"><span data-stu-id="5518c-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="5518c-205">Enregistrer la phrase secrète de chiffrement hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="5518c-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5518c-206">Si vous perdez ou oubliez le mot de passe hello, Microsoft ne peut pas aider à récupérer les données de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="5518c-207">Enregistrez le fichier de hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="5518c-207">Save hello file in a secure location.</span></span> <span data-ttu-id="5518c-208">Il est requis toorestore une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="5518c-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="5518c-209">Hello agent est installé et que votre ordinateur est inscrit toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="5518c-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="5518c-210">Vous êtes prêt tooconfigure et planifiez votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="5518c-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="5518c-211">Conditions de connectivité et réseau</span><span class="sxs-lookup"><span data-stu-id="5518c-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="5518c-212">Si votre ordinateur/proxy est limitée à un accès à internet, assurez-vous que les paramètres du pare-feu sur hello mcahine/proxy sont hello tooallow configuré URL suivantes :</span><span class="sxs-lookup"><span data-stu-id="5518c-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="5518c-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="5518c-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="5518c-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="5518c-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="5518c-215">*.MicrosoftAzure.com</span><span class="sxs-lookup"><span data-stu-id="5518c-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="5518c-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="5518c-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="5518c-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="5518c-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="5518c-218">Sauvegarder vos fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="5518c-218">Back up your files and folders</span></span>
<span data-ttu-id="5518c-219">la sauvegarde initiale Hello inclut deux tâches principales :</span><span class="sxs-lookup"><span data-stu-id="5518c-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="5518c-220">Planifier la sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="5518c-220">Schedule hello backup</span></span>
* <span data-ttu-id="5518c-221">Sauvegarder des fichiers et des dossiers pour hello première fois</span><span class="sxs-lookup"><span data-stu-id="5518c-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="5518c-222">sauvegarde initiale toocomplete hello, utilisez hello Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="5518c-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="5518c-223">travail de sauvegarde hello tooschedule</span><span class="sxs-lookup"><span data-stu-id="5518c-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="5518c-224">Ouvrez l’agent de Microsoft Azure Recovery Services hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="5518c-225">Vous pouvez le trouver en recherchant **Sauvegarde Microsoft Azure**sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5518c-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Lancer hello Azure Recovery Services agent](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="5518c-227">Dans l’agent Recovery Services hello, cliquez sur **planifier la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5518c-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="5518c-229">Sur hello mise en route de la page de hello Assistant Planification de sauvegarde, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="5518c-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="5518c-230">Page de tooBackup hello sélectionner les éléments, cliquez sur **ajouter les éléments**.</span><span class="sxs-lookup"><span data-stu-id="5518c-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="5518c-231">Sélectionnez les fichiers de hello et dossiers que vous souhaitez tooback haut, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5518c-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="5518c-232">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5518c-232">Click **Next**.</span></span>
7. <span data-ttu-id="5518c-233">Sur hello **spécifier la planification de sauvegarde** , spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="5518c-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="5518c-234">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="5518c-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="5518c-236">Pour plus d’informations sur comment toospecify hello planification de sauvegarde, voir l’article hello [tooreplace utilisez Azure Backup votre infrastructure de bande](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="5518c-237">Sur hello **sélectionner la stratégie de rétention** page, sélectionnez hello **stratégie de rétention** de copie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="5518c-238">stratégie de rétention Hello spécifie la durée de stockage des données de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="5518c-239">Plutôt que de spécifier une stratégie « plate » pour tous les points de sauvegarde, vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello se produit.</span><span class="sxs-lookup"><span data-stu-id="5518c-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="5518c-240">Vous pouvez modifier toomeet de stratégies de rétention quotidienne, hebdomadaire, mensuel et annuel hello à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5518c-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="5518c-241">Sur la page Choisir un Type de sauvegarde initiale de hello, choisissez le type de sauvegarde initiale hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="5518c-242">Conservez l’option hello **automatiquement sur le réseau de hello** sélectionné, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="5518c-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="5518c-243">Vous pouvez sauvegarder automatiquement sur le réseau de hello, ou vous pouvez sauvegarder en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="5518c-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="5518c-244">reste Hello de cet article décrit le processus hello pour sauvegarder automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5518c-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="5518c-245">Si vous préférez toodo une sauvegarde hors connexion, consultez l’article de hello [workflow de sauvegarde en mode hors connexion dans Azure Backup](backup-azure-backup-import-export.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5518c-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="5518c-246">Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="5518c-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="5518c-247">Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="5518c-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="5518c-248">tooback des fichiers et des dossiers pour hello première fois</span><span class="sxs-lookup"><span data-stu-id="5518c-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="5518c-249">Dans l’agent Recovery Services hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Sauvegarder Windows Server maintenant](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="5518c-251">Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="5518c-252">puis cliquez sur **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="5518c-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="5518c-253">Cliquez sur **fermer** Assistant de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="5518c-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="5518c-254">Si vous fermez l’Assistant de hello avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="5518c-255">Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5518c-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![RI terminé](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="5518c-257">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="5518c-257">Questions?</span></span>
<span data-ttu-id="5518c-258">Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="5518c-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5518c-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5518c-259">Next steps</span></span>
* <span data-ttu-id="5518c-260">Approfondissez vos connaissances sur la [sauvegarde de machines Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="5518c-261">Maintenant que vous avez sauvegardé vos fichiers et vos dossiers, vous pouvez [gérer vos archivages et vos serveurs](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="5518c-262">Si vous devez toorestore une sauvegarde, utilisez cet article trop[restaurer la machine virtuelle Windows tooa fichiers](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="5518c-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
