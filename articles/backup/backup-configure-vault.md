---
title: aaaUse Azure Backup agent tooback les fichiers et dossiers | Documents Microsoft
description: "Utilisez hello Microsoft Azure Backup agent tooback des tooAzure de fichiers et dossiers de Windows. Créer un coffre Recovery Services, installez l’agent de sauvegarde hello, définir la stratégie de sauvegarde hello et exécuter la sauvegarde initiale de hello sur les dossiers et fichiers de hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: coffre de sauvegarde ; sauvegarder un serveur Windows ; sauvegarder windows ;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="378dc-105">Sauvegarder un tooAzure ou client Windows Server à l’aide du modèle de déploiement du Gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="378dc-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="378dc-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="378dc-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="378dc-107">Portail classique</span><span class="sxs-lookup"><span data-stu-id="378dc-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="378dc-108">Cet article explique comment tooAzure de fichiers et dossiers tooback de votre client Windows Server (ou Windows) à l’aide de la sauvegarde Azure hello modèle de déploiement de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="378dc-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Étapes du processus de sauvegarde](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="378dc-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="378dc-110">Before you start</span></span>
<span data-ttu-id="378dc-111">tooback un serveur ou un client tooAzure, vous devez un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="378dc-112">Si vous n’en possédez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="378dc-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="378dc-113">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="378dc-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="378dc-114">Un coffre Recovery Services est une entité qui stocke toutes les sauvegardes de hello et les points de récupération que vous créez au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="378dc-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="378dc-115">le coffre Recovery Services Hello contient également hello appliqué de stratégie de sauvegarde toohello protégé fichiers et dossiers.</span><span class="sxs-lookup"><span data-stu-id="378dc-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="378dc-116">Lorsque vous créez un coffre Recovery Services, vous devez également sélectionner option de redondance de stockage approprié hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="378dc-117">toocreate un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="378dc-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="378dc-118">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="378dc-119">Dans le menu du Hub hello, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Services de récupération** et cliquez sur **les coffres de Services de récupération**.</span><span class="sxs-lookup"><span data-stu-id="378dc-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="378dc-121">S’il existe des coffres des services de récupération dans l’abonnement de hello, coffres de hello sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="378dc-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="378dc-122">Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="378dc-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="378dc-124">Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="378dc-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Créer un coffre Recovery Services - Étape 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="378dc-126">Pour **nom**, entrez un coffre de hello tooidentify nom convivial.</span><span class="sxs-lookup"><span data-stu-id="378dc-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="378dc-127">nom de Hello doit toobe unique pour hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="378dc-128">Tapez un nom contenant entre 2 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="378dc-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="378dc-129">Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="378dc-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="378dc-130">Bonjour **abonnement** section, utilisez hello toochoose de menu déroulant hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="378dc-131">Si vous N'utilisez qu’un seul abonnement, cet abonnement s’affiche et vous pouvez ignorer toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="378dc-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="378dc-132">Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement.</span><span class="sxs-lookup"><span data-stu-id="378dc-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="378dc-133">Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="378dc-134">Bonjour **groupe de ressources** section :</span><span class="sxs-lookup"><span data-stu-id="378dc-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="378dc-135">Sélectionnez **nouvel** si vous voulez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="378dc-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="378dc-136">Ou</span><span class="sxs-lookup"><span data-stu-id="378dc-136">Or</span></span>
    * <span data-ttu-id="378dc-137">Sélectionnez **utiliser l’existante** sur hello menu déroulant toosee hello disponible liste des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="378dc-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="378dc-138">Pour plus d’informations sur les groupes de ressources, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="378dc-139">Cliquez sur **emplacement** tooselect hello région pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="378dc-140">Ce choix détermine la région géographique de hello où vos données de sauvegarde sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="378dc-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="378dc-141">Au bas de hello du Panneau de coffre Recovery Services hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="378dc-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="378dc-142">Il peut prendre plusieurs minutes pour hello que toobe créé de coffre de Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="378dc-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="378dc-143">Surveiller les notifications d’état hello dans la zone de droite supérieure hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="378dc-144">Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="378dc-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="378dc-145">Si vous ne voyez pas votre coffre après quelques minutes, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="378dc-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Bouton Actualiser](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="378dc-147">Une fois que vous voyez votre coffre dans la liste hello des archivages de Recovery Services, vous êtes prêt tooset une redondance de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="378dc-148">Définir la redondance du stockage</span><span class="sxs-lookup"><span data-stu-id="378dc-148">Set storage redundancy</span></span>
<span data-ttu-id="378dc-149">Lorsque vous créez un archivage de Recovery Services pour la première fois, vous devez spécifier le mode de réplication du stockage.</span><span class="sxs-lookup"><span data-stu-id="378dc-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="378dc-150">À partir de hello **les coffres de Services de récupération** panneau, cliquez sur le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Sélectionnez le coffre hello dans liste hello du coffre Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="378dc-152">Lorsque vous sélectionnez le coffre de hello, hello **de coffre Recovery Services** panneau restreint et panneau de paramètres hello (*qui a le nom hello du coffre de hello de haut hello*) et le panneau de détails du coffre hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="378dc-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Afficher la configuration du stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="378dc-154">Dans le panneau des paramètres du coffre hello nouvelle tooscroll de diapositive vertical hello toohello section gérer vers le bas, puis cliquez sur **Infrastructure de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="378dc-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="378dc-155">panneau d’Infrastructure de sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="378dc-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="378dc-156">Dans le panneau d’Infrastructure de sauvegarde hello, cliquez sur **Configuration de la sauvegarde** tooopen hello **Configuration de la sauvegarde** panneau.</span><span class="sxs-lookup"><span data-stu-id="378dc-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Définir la configuration de stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="378dc-158">Choisissez l’option de réplication de stockage approprié de hello pour votre coffre.</span><span class="sxs-lookup"><span data-stu-id="378dc-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![Options de configuration du stockage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="378dc-160">Par défaut, votre archivage utilise un stockage géo-redondant.</span><span class="sxs-lookup"><span data-stu-id="378dc-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="378dc-161">Si vous utilisez Azure comme un point de terminaison principal de stockage de sauvegarde, continuer toouse **géo-redondant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="378dc-162">Si vous n’utilisez pas Azure comme un point de terminaison principal de stockage de sauvegarde, puis choisissez **localement redondant**, ce qui réduit les coûts de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="378dc-163">Pour en savoir plus sur les options de stockage [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage), consultez la [présentation de la redondance du stockage](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="378dc-164">Maintenant que vous avez créé un coffre, préparez votre tooback infrastructure des fichiers et des dossiers en téléchargeant et installation hello Microsoft Azure Recovery Services agent, téléchargement des informations d’identification de coffre et ensuite à l’aide de ces informations d’identification tooregister hello agent coffre de Hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="378dc-165">Configurer le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="378dc-165">Configure hello vault</span></span>

1. <span data-ttu-id="378dc-166">On hello panneau du coffre Recovery Services (pour hello coffre vous venez de créer), dans la section prise en main de hello, cliquez sur **sauvegarde**, puis sur hello **mise en route de la sauvegarde** panneau, sélectionnez  **Objectif de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="378dc-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="378dc-168">Hello **sauvegarde objectif** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="378dc-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="378dc-169">Si hello de coffre Recovery Services a été configuré précédemment, puis hello **sauvegarde objectif** panneaux s’ouvre lorsque vous cliquez sur **sauvegarde** sur les Services de récupération hello coffre lame.</span><span class="sxs-lookup"><span data-stu-id="378dc-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="378dc-171">À partir de hello **votre charge de travail exécutant ?** menu déroulant, sélectionnez **local**.</span><span class="sxs-lookup"><span data-stu-id="378dc-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="378dc-172">En effet, vous devez choisir l’option **Local**, car votre ordinateur Windows Server ou Windows est une machine physique, qui ne se trouve donc pas dans Azure.</span><span class="sxs-lookup"><span data-stu-id="378dc-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="378dc-173">À partir de hello **comment vous souhaitez toobackup ?** menu, sélectionnez **fichiers et dossiers**et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="378dc-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Configuration des fichiers et dossiers](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="378dc-175">Après avoir cliqué sur OK, une coche apparaît en regard trop**objectif de sauvegarde**et hello **Prepare infrastructure** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="378dc-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Objectif de sauvegarde configuré, début de préparation de l’infrastructure](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="378dc-177">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger l’Agent pour Windows Server ou Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="378dc-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="378dc-179">Si vous utilisez Windows Server essentiels, puis choisissez toodownload hello agent essentielles de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="378dc-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="378dc-180">Un menu contextuel vous invite toorun ou enregistrer MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="378dc-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Boîte de dialogue MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="378dc-182">Dans le menu contextuel du téléchargement hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="378dc-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="378dc-183">Par défaut, hello **MARSagentinstaller.exe** fichier est enregistré le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="378dc-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="378dc-184">Lorsque le programme d’installation hello est terminée, vous verrez un message vous demandant si vous souhaitez que le programme d’installation de toorun hello ou ouvrez le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="378dc-186">Vous n’avez pas encore l’agent de tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="378dc-187">Vous pouvez installer l’agent de hello après avoir téléchargé les informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="378dc-188">Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="378dc-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Télécharger les informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="378dc-190">informations d’identification de coffre Hello téléchargement le dossier Téléchargements de tooyour.</span><span class="sxs-lookup"><span data-stu-id="378dc-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="378dc-191">Une fois les informations d’identification de coffre hello terminer le téléchargement, vous voyez un message vous demandant si vous souhaitez tooopen ou enregistrez les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="378dc-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="378dc-192">Click **Save**.</span></span> <span data-ttu-id="378dc-193">Si vous cliquez accidentellement sur **ouvrir**, permettent de boîte de dialogue hello qui tente d’informations d’identification du coffre tooopen hello donc pas.</span><span class="sxs-lookup"><span data-stu-id="378dc-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="378dc-194">Impossible d’ouvrir des informations d’identification de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="378dc-195">Passez maintenant toohello.</span><span class="sxs-lookup"><span data-stu-id="378dc-195">Proceed toohello next step.</span></span> <span data-ttu-id="378dc-196">informations d’identification de coffre Hello se trouvent dans le dossier Téléchargements de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![Fin du téléchargement des informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="378dc-198">Installer et inscrire l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="378dc-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="378dc-199">Activer la sauvegarde via hello portail Azure n’est pas encore disponible.</span><span class="sxs-lookup"><span data-stu-id="378dc-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="378dc-200">Utilisez tooback de Microsoft Azure Recovery Services Agent hello des fichiers et des dossiers.</span><span class="sxs-lookup"><span data-stu-id="378dc-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="378dc-201">Recherchez et double-cliquez sur hello **MARSagentinstaller.exe** de téléchargements de hello dossier (ou tout autre emplacement enregistré).</span><span class="sxs-lookup"><span data-stu-id="378dc-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="378dc-202">programme d’installation Hello fournit une série de messages qu’il extrait, installe et enregistre hello Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="378dc-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Informations d’identification de programme d’installation de l’agent Recovery Services exécuté](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="378dc-204">Assistant Installation de Microsoft Azure Recovery Services Agent de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="378dc-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="378dc-205">Assistant de hello toocomplete, vous devez :</span><span class="sxs-lookup"><span data-stu-id="378dc-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="378dc-206">Choisissez un emplacement pour le dossier d’installation et de cache hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="378dc-207">Fournir les informations du serveur de votre proxy si vous utilisez un toohello tooconnect du serveur proxy internet.</span><span class="sxs-lookup"><span data-stu-id="378dc-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="378dc-208">Fournir votre nom d’utilisateur et votre mot de passe si vous utilisez un proxy authentifié.</span><span class="sxs-lookup"><span data-stu-id="378dc-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="378dc-209">Fournir des informations d’identification de coffre hello téléchargé</span><span class="sxs-lookup"><span data-stu-id="378dc-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="378dc-210">Enregistrer la phrase secrète de chiffrement hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="378dc-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="378dc-211">Si vous perdez ou oubliez le mot de passe hello, Microsoft ne peut pas aider à récupérer les données de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="378dc-212">Enregistrez le fichier de hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="378dc-212">Save hello file in a secure location.</span></span> <span data-ttu-id="378dc-213">Il est requis toorestore une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="378dc-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="378dc-214">Hello agent est installé et que votre ordinateur est inscrit toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="378dc-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="378dc-215">Vous êtes prêt tooconfigure et planifiez votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="378dc-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="378dc-216">Conditions de connectivité et réseau</span><span class="sxs-lookup"><span data-stu-id="378dc-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="378dc-217">Si votre ordinateur/proxy est limitée à un accès à internet, assurez-vous que les paramètres du pare-feu sur hello/proxy de l’ordinateur sont hello tooallow configuré URL suivantes :</span><span class="sxs-lookup"><span data-stu-id="378dc-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="378dc-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="378dc-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="378dc-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="378dc-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="378dc-220">*.MicrosoftAzure.com</span><span class="sxs-lookup"><span data-stu-id="378dc-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="378dc-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="378dc-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="378dc-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="378dc-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="378dc-223">Créer une stratégie de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="378dc-223">Create hello backup policy</span></span>
<span data-ttu-id="378dc-224">stratégie de sauvegarde Hello est planification de hello lorsque des points de récupération sont effectuées et hello de durée de conservation des points de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="378dc-225">Utilisez hello Microsoft Azure Backup agent toocreate hello stratégie de sauvegarde des fichiers et dossiers.</span><span class="sxs-lookup"><span data-stu-id="378dc-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="378dc-226">toocreate une planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="378dc-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="378dc-227">Ouvrez hello Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="378dc-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="378dc-228">Vous pouvez le trouver en recherchant **Sauvegarde Microsoft Azure**sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="378dc-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Lancez l’agent de sauvegarde Azure hello](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="378dc-230">Dans l’agent de sauvegarde hello **Actions** volet, cliquez sur **planifier la sauvegarde** toolaunch hello Assistant Planification de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="378dc-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Planifier une sauvegarde de Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="378dc-232">Sur hello **mise en route** page Hello Assistant Planification de sauvegarde, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="378dc-233">Sur hello **tooBackup de sélectionner les éléments** , cliquez sur **ajouter les éléments**.</span><span class="sxs-lookup"><span data-stu-id="378dc-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="378dc-234">Ouvre la boîte de dialogue Sélectionner les éléments Hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="378dc-235">Sélectionnez les fichiers de hello et dossiers que vous souhaitez tooprotect, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="378dc-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="378dc-236">Bonjour **tooBackup de sélectionner les éléments** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="378dc-237">Sur hello **spécifier la planification de sauvegarde** , spécifiez la planification de sauvegarde hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="378dc-238">Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="378dc-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Éléments de sauvegarde de Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="378dc-240">Pour plus d’informations sur comment toospecify hello planification de sauvegarde, voir l’article hello [tooreplace utilisez Azure Backup votre infrastructure de bande](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="378dc-241">Sur hello **sélectionner la stratégie de rétention** page, choisissez hello de stratégies de rétention spécifique hello de copie de sauvegarde hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="378dc-242">stratégie de rétention Hello spécifie la durée hello quelle sauvegarde hello est stocké.</span><span class="sxs-lookup"><span data-stu-id="378dc-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="378dc-243">Plutôt que de simplement spécifier « stratégie plate » pour tous les points de sauvegarde, vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello se produit.</span><span class="sxs-lookup"><span data-stu-id="378dc-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="378dc-244">Vous pouvez modifier toomeet de stratégies de rétention quotidienne, hebdomadaire, mensuel et annuel hello à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="378dc-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="378dc-245">Sur la page Choisir un Type de sauvegarde initiale de hello, choisissez le type de sauvegarde initiale hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="378dc-246">Conservez l’option hello **automatiquement sur le réseau de hello** sélectionné, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="378dc-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="378dc-247">Vous pouvez sauvegarder automatiquement sur le réseau de hello, ou vous pouvez sauvegarder en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="378dc-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="378dc-248">reste Hello de cet article décrit le processus hello pour sauvegarder automatiquement.</span><span class="sxs-lookup"><span data-stu-id="378dc-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="378dc-249">Si vous préférez toodo une sauvegarde hors connexion, consultez l’article de hello [workflow de sauvegarde en mode hors connexion dans Azure Backup](backup-azure-backup-import-export.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="378dc-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="378dc-250">Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="378dc-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="378dc-251">Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="378dc-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="378dc-252">Activation de la limitation du réseau</span><span class="sxs-lookup"><span data-stu-id="378dc-252">Enable network throttling</span></span>
<span data-ttu-id="378dc-253">Hello Microsoft Azure Backup agent fournit la limitation du réseau.</span><span class="sxs-lookup"><span data-stu-id="378dc-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="378dc-254">La limitation contrôle l’utilisation de la bande passante réseau durant le transfert de données.</span><span class="sxs-lookup"><span data-stu-id="378dc-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="378dc-255">Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic Internet.</span><span class="sxs-lookup"><span data-stu-id="378dc-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="378dc-256">La limitation s’applique tooback des activités et de restauration.</span><span class="sxs-lookup"><span data-stu-id="378dc-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="378dc-257">La limitation du réseau n’est pas disponible sur Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ou Windows 7 (avec service packs).</span><span class="sxs-lookup"><span data-stu-id="378dc-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="378dc-258">fonctionnalité de limitation du réseau de sauvegarde Azure Hello engage une qualité de Service (QoS) sur le système d’exploitation local de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="378dc-259">Bien que Azure Backup peut protéger ces systèmes d’exploitation, version hello de qualité de service disponibles sur ces plateformes ne fonctionne pas avec la limitation réseau Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="378dc-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="378dc-260">La limitation du réseau peut être utilisée sur tous les autres [systèmes d’exploitation pris en charge](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="378dc-261">**la limitation réseau tooenable**</span><span class="sxs-lookup"><span data-stu-id="378dc-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="378dc-262">Dans l’agent Microsoft Azure Backup hello, cliquez sur **modifier les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="378dc-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Modifier les propriétés](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="378dc-264">Sur hello **limitation** onglet, sélectionnez hello **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="378dc-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Limitation du réseau](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="378dc-266">Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.</span><span class="sxs-lookup"><span data-stu-id="378dc-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="378dc-267">valeurs de la bande passante Hello commencent à 512 kilobits par seconde (Kbits/s) et peuvent atteindre la too1, 023 mégaoctets par seconde (Mbits/s).</span><span class="sxs-lookup"><span data-stu-id="378dc-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="378dc-268">Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont des jours de travail pris en compte.</span><span class="sxs-lookup"><span data-stu-id="378dc-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="378dc-269">Les heures non comprises dans les heures de travail définies sont considérées comme des heures chômées.</span><span class="sxs-lookup"><span data-stu-id="378dc-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="378dc-270">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="378dc-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="378dc-271">tooback des fichiers et des dossiers pour hello première fois</span><span class="sxs-lookup"><span data-stu-id="378dc-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="378dc-272">Dans l’agent de sauvegarde hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Sauvegarder Windows Server maintenant](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="378dc-274">Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="378dc-275">puis cliquez sur **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="378dc-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="378dc-276">Cliquez sur **fermer** Assistant de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="378dc-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="378dc-277">Si vous procédez ainsi avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="378dc-278">Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="378dc-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![RI terminé](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="378dc-280">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="378dc-280">Questions?</span></span>
<span data-ttu-id="378dc-281">Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="378dc-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="378dc-282">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="378dc-282">Next steps</span></span>
<span data-ttu-id="378dc-283">Pour plus d’informations sur la sauvegarde des machines virtuelles ou d’autres charges de travail, consultez les références suivantes :</span><span class="sxs-lookup"><span data-stu-id="378dc-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="378dc-284">Maintenant que vous avez sauvegardé vos fichiers et vos dossiers, vous pouvez [gérer vos archivages et vos serveurs](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="378dc-285">Si vous devez toorestore une sauvegarde, utilisez cet article trop[restaurer la machine virtuelle Windows tooa fichiers](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="378dc-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
