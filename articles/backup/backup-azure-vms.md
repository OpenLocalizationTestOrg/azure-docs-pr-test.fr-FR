---
title: "aaaBack de coffre de sauvegarde de machines virtuelles déployées classique tooa | Documents Microsoft"
description: "Découvrez, inscrivez et sauvegardez vos machines virtuelles avec ces procédures pour la sauvegarde de la machine virtuelle Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde de machine virtuelle ; sauvegarder la machine virtuelle ; sauvegarde et récupération d’urgence ; sauvegarde de machine virtuelle"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="9f45f-104">Sauvegarde des machines virtuelles Azure (portail classique)</span><span class="sxs-lookup"><span data-stu-id="9f45f-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f45f-105">Sauvegarder le coffre de Services tooRecovery de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9f45f-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="9f45f-106">Sauvegarder des machines virtuelles tooBackup coffre</span><span class="sxs-lookup"><span data-stu-id="9f45f-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="9f45f-107">Cet article fournit des procédures hello pour la sauvegarde d’un coffre de sauvegarde tooa déployés classique Azure virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="9f45f-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="9f45f-108">Il existe quelques tâches que vous devez tootake charge avant que vous puissiez sauvegarder une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="9f45f-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="9f45f-109">Si vous n’avez pas déjà fait hello donc, complète [conditions préalables](backup-azure-vms-prepare.md) tooprepare votre environnement pour sauvegarder vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9f45f-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="9f45f-110">Pour plus d’informations, reportez-vous aux articles de hello [planification de votre infrastructure de sauvegarde de machine virtuelle dans Azure](backup-azure-vms-introduction.md) et [machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="9f45f-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="9f45f-111">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9f45f-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9f45f-112">Un coffre de sauvegarde peut uniquement protéger les machines virtuelles déployées à l’aide du modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="9f45f-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="9f45f-113">Vous ne pouvez pas utiliser un coffre de sauvegarde pour protéger les machines virtuelles déployées par le biais de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9f45f-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="9f45f-114">Consultez [sauvegarder les machines virtuelles tooRecovery Services coffre](backup-azure-arm-vms.md) pour plus d’informations sur l’utilisation des Services de récupération des coffres-forts.</span><span class="sxs-lookup"><span data-stu-id="9f45f-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="9f45f-115">Les trois principales étapes de la sauvegarde des machines virtuelles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="9f45f-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Tooback trois étapes d’une machine virtuelle IaaS de Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="9f45f-117">La sauvegarde des machines virtuelles est un processus local.</span><span class="sxs-lookup"><span data-stu-id="9f45f-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="9f45f-118">Vous ne pouvez pas sauvegarder les machines virtuelles dans un coffre de sauvegarde de tooa région dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="9f45f-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="9f45f-119">Par conséquent, vous devez créer un archivage de sauvegarde dans chaque région Azure dans laquelle des machines virtuelles seront sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="9f45f-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="9f45f-120">À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.</span><span class="sxs-lookup"><span data-stu-id="9f45f-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="9f45f-121">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="9f45f-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="9f45f-122">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="9f45f-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="9f45f-123">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9f45f-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="9f45f-124">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f45f-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="9f45f-125">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="9f45f-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="9f45f-126">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="9f45f-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="9f45f-127">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="9f45f-128">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="9f45f-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="9f45f-129">Étape 1 - Découverte des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="9f45f-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="9f45f-130">tooensure n’importe quel abonnement toohello ajouté de nouvelles machines virtuelles (VM) sont identifiés avant d’inscrire, exécuter le processus de découverte hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="9f45f-131">Hello traiter les requêtes Azure pour la liste des ordinateurs virtuels dans l’abonnement hello, ainsi que les informations hello comme nom du service cloud hello et région de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="9f45f-132">Connectez-vous à toohello [portal de classique](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="9f45f-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="9f45f-133">Dans la liste de hello des services Azure, cliquez sur **Services de récupération** liste de hello tooopen de coffres de sauvegarde et de récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="9f45f-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="9f45f-134">![Ouvrir la liste d’archivage](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="9f45f-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="9f45f-135">Dans la liste hello de coffres de sauvegarde, sélectionnez tooback de coffre hello d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9f45f-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="9f45f-136">S’il s’agit d’un nouveau portail de hello coffre ouvre toohello **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="9f45f-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Ouvrir le menu Éléments inscrits](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="9f45f-138">Si le coffre hello a été configuré précédemment, le portail de hello ouvre toohello utilisé le plus récemment menu.</span><span class="sxs-lookup"><span data-stu-id="9f45f-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="9f45f-139">À partir du menu de coffre hello (en hello haut hello), cliquez sur **éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="9f45f-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Ouvrir le menu Éléments inscrits](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="9f45f-141">À partir de hello **Type** menu, sélectionnez **Machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="9f45f-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="9f45f-143">Cliquez sur **DISCOVER** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="9f45f-144">![Bouton découverte](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="9f45f-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="9f45f-145">processus de découverte Hello peut prendre quelques minutes hello virtuels sont en cours sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="9f45f-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="9f45f-146">Il existe une notification bas hello écran hello qui vous permet de savoir que hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="9f45f-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Détection des machines virtuelles](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="9f45f-148">modifications de la notification Hello lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="9f45f-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="9f45f-149">Si le processus de découverte hello n’a pas trouvé les ordinateurs virtuels de hello, vérifiez d’abord que Hello VMs existent.</span><span class="sxs-lookup"><span data-stu-id="9f45f-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="9f45f-150">Si les ordinateurs virtuels de hello existent, vérifiez hello machines virtuelles sont dans hello même région que le coffre de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="9f45f-151">Si les machines virtuelles de hello existent et sont hello la même région, vérifiez que Hello VM n’est pas déjà inscrit tooa coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9f45f-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="9f45f-152">Si une machine virtuelle est le coffre de sauvegarde attribué tooa il n’est pas coffres de sauvegarde tooother toobe disponible attribué.</span><span class="sxs-lookup"><span data-stu-id="9f45f-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Détection exécutée](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="9f45f-154">Une fois que vous avez découvert de nouveaux éléments de hello, accédez tooStep 2 et enregistrer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9f45f-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="9f45f-155">Étape 2 - Inscription des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="9f45f-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="9f45f-156">Vous inscrivez une tooassociate de machine virtuelle Azure avec hello service Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="9f45f-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="9f45f-157">L’inscription est généralement une activité unique.</span><span class="sxs-lookup"><span data-stu-id="9f45f-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="9f45f-158">Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure, puis cliquez sur **éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="9f45f-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="9f45f-159">Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="9f45f-161">Cliquez sur **inscrire** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="9f45f-162">![Bouton Inscription](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="9f45f-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="9f45f-163">Bonjour **enregistrer les éléments** menu contextuel, sélectionnez hello ordinateurs virtuels que vous souhaitez tooregister.</span><span class="sxs-lookup"><span data-stu-id="9f45f-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="9f45f-164">S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello cloud service toodistinguish entre eux.</span><span class="sxs-lookup"><span data-stu-id="9f45f-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="9f45f-165">Plusieurs machines virtuelles peuvent être inscrites en même temps.</span><span class="sxs-lookup"><span data-stu-id="9f45f-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="9f45f-166">Un travail est créé pour chaque machine virtuelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9f45f-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="9f45f-167">Cliquez sur **afficher le travail** dans hello notification toogo toohello **travaux** page.</span><span class="sxs-lookup"><span data-stu-id="9f45f-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Inscrire du travail](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="9f45f-169">machine virtuelle de Hello apparaît également dans la liste hello des éléments inscrits, ainsi que de l’état hello de l’opération d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![État de l’inscription 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="9f45f-171">Lors de la fin de l’opération de hello, hello devient tooreflect hello *inscrit* état.</span><span class="sxs-lookup"><span data-stu-id="9f45f-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![État de l’inscription 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="9f45f-173">Étape 3 - Protection des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="9f45f-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="9f45f-174">Vous pouvez désormais configurer une stratégie de sauvegarde et de rétention pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="9f45f-175">Plusieurs machines virtuelles peuvent être protégées par la même action de protection.</span><span class="sxs-lookup"><span data-stu-id="9f45f-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="9f45f-176">Les coffres de sauvegarde Azure créés après mai 2015 fournis avec une stratégie par défaut intégrées dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="9f45f-177">Cette stratégie par défaut est fournie avec une durée de conservation par défaut de 30 jours et une fréquence de sauvegarde quotidienne d’une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="9f45f-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="9f45f-178">Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure, puis cliquez sur **éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="9f45f-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="9f45f-179">Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Sélectionner la charge de travail dans le portail](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="9f45f-181">Cliquez sur **protéger** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="9f45f-182">Hello **Assistant protéger** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9f45f-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="9f45f-183">Assistant de Hello répertorie uniquement les ordinateurs virtuels qui sont enregistrés et non protégés.</span><span class="sxs-lookup"><span data-stu-id="9f45f-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="9f45f-184">Sélectionnez hello ordinateurs virtuels que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="9f45f-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="9f45f-185">S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello cloud service toodistinguish entre les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="9f45f-186">Vous pouvez protéger plusieurs machines virtuelles en même temps.</span><span class="sxs-lookup"><span data-stu-id="9f45f-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configurer les paramètres de protection pendant la mise à jour](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="9f45f-188">Choisissez un **planification de sauvegarde** tooback les machines virtuelles hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9f45f-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="9f45f-189">Vous pouvez sélectionner un ensemble de stratégies existant ou en définir un nouveau.</span><span class="sxs-lookup"><span data-stu-id="9f45f-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="9f45f-190">Vous pouvez associer plusieurs machines virtuelles à chaque stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9f45f-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="9f45f-191">Toutefois, hello virtual machine peut uniquement être associé avec une stratégie à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="9f45f-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Protéger grâce à la nouvelle stratégie](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="9f45f-193">Une stratégie de sauvegarde inclut un jeu de rétention pour les sauvegardes planifiée de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="9f45f-194">Si vous sélectionnez une stratégie de sauvegarde existante, vous ne pouvez pas modifier les options de rétention hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="9f45f-195">Choisissez un **de rétention** tooassociate avec des sauvegardes hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Protéger avec la rétention flexible](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="9f45f-197">Stratégie de rétention spécifie la durée hello pour stocker une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9f45f-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="9f45f-198">Vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="9f45f-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="9f45f-199">Par exemple, un point de sauvegarde effectué quotidiennement (qui sert de point de récupération opérationnel) peut être conservé pendant 90 jours.</span><span class="sxs-lookup"><span data-stu-id="9f45f-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="9f45f-200">En comparaison, un point de sauvegarde effectuée à la fin de hello de chaque trimestre (à des fins d’audit) peut-être toobe conservée pendant des mois ou années.</span><span class="sxs-lookup"><span data-stu-id="9f45f-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="9f45f-202">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="9f45f-202">In this example image:</span></span>

   * <span data-ttu-id="9f45f-203">**Stratégie de rétention quotidienne**: les sauvegardes effectuées quotidiennement sont stockées pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="9f45f-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="9f45f-204">**Stratégie de rétention hebdomadaire**: les sauvegardes effectuées tous les dimanches sont conservées pendant 104 semaines.</span><span class="sxs-lookup"><span data-stu-id="9f45f-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="9f45f-205">**Stratégie de rétention mensuelle**: les sauvegardes effectuées sur hello dernier dimanche de chaque mois sont conservées pendant 120 mois.</span><span class="sxs-lookup"><span data-stu-id="9f45f-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="9f45f-206">**Stratégie de rétention annuelle**: les sauvegardes effectuées sur hello premier dimanche de chaque mois de janvier sont conservés pour de 99 ans.</span><span class="sxs-lookup"><span data-stu-id="9f45f-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="9f45f-207">Un travail est créé de stratégie de protection tooconfigure hello et associer hello machines virtuelles toothat stratégie pour chaque ordinateur virtuel que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9f45f-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="9f45f-208">liste de hello tooview de **configurer la Protection** travaux, à partir du menu de coffres hello, cliquez sur **travaux** et sélectionnez **configurer la Protection** de hello **opération**  filtre.</span><span class="sxs-lookup"><span data-stu-id="9f45f-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Configurer le travail de protection](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="9f45f-210">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="9f45f-210">Initial backup</span></span>
<span data-ttu-id="9f45f-211">Une fois que l’ordinateur virtuel de hello est protégé par une stratégie, elle s’affiche sous hello **éléments protégés** onglet dont l’état hello *Protected - (en attente de sauvegarde initiale)*.</span><span class="sxs-lookup"><span data-stu-id="9f45f-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="9f45f-212">Par défaut, première sauvegarde planifiée du hello est hello *sauvegarde initiale*.</span><span class="sxs-lookup"><span data-stu-id="9f45f-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="9f45f-213">sauvegarde initiale du hello tootrigger immédiatement après la configuration de la protection :</span><span class="sxs-lookup"><span data-stu-id="9f45f-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="9f45f-214">En bas de hello Hello **éléments protégés** , cliquez sur **sauvegarde maintenant**.</span><span class="sxs-lookup"><span data-stu-id="9f45f-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="9f45f-215">Hello service Azure Backup crée une tâche de sauvegarde pour l’opération de sauvegarde initiale hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="9f45f-216">Cliquez sur hello **travaux** liste de hello onglet tooview des tâches.</span><span class="sxs-lookup"><span data-stu-id="9f45f-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Sauvegarde en cours](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="9f45f-218">Au cours de l’opération de sauvegarde hello, hello Azure Backup service émet une extension de sauvegarde commande toohello dans chaque tooflush de machine virtuelle, tous les travaux d’écriture et prenant un instantané cohérent.</span><span class="sxs-lookup"><span data-stu-id="9f45f-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="9f45f-219">Lorsque les sauvegarde initiale hello se termine, état hello de machine virtuelle de hello Bonjour **éléments protégés** onglet est *protégé*.</span><span class="sxs-lookup"><span data-stu-id="9f45f-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="9f45f-221">Affichage des détails et de l’état de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9f45f-221">Viewing backup status and details</span></span>
<span data-ttu-id="9f45f-222">Une fois que protégé, nombre d’ordinateurs virtuels hello augmente également Bonjour **tableau de bord** page Résumé.</span><span class="sxs-lookup"><span data-stu-id="9f45f-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="9f45f-223">Hello **tableau de bord** page affiche également le nombre de hello de travaux à partir de hello des dernières 24 heures qui ont été *réussie*, ont *échec*et sont *en cours d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="9f45f-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="9f45f-224">Sur hello **travaux** page, utilisez hello **état**, **opération**, ou **de** et **à** toofilter de menus travaux de Hello.</span><span class="sxs-lookup"><span data-stu-id="9f45f-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![État de la sauvegarde sur la page Tableau de bord](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="9f45f-226">Les valeurs dans le tableau de bord hello sont actualisés toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="9f45f-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="9f45f-227">Résolution des erreurs</span><span class="sxs-lookup"><span data-stu-id="9f45f-227">Troubleshooting errors</span></span>
<span data-ttu-id="9f45f-228">Si vous rencontrez des problèmes pendant la sauvegarde de votre machine virtuelle, consultez hello [article de résolution des problèmes de machine virtuelle](backup-azure-vms-troubleshoot.md) de l’aide.</span><span class="sxs-lookup"><span data-stu-id="9f45f-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f45f-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f45f-229">Next steps</span></span>
* [<span data-ttu-id="9f45f-230">Gestion et surveillance de vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9f45f-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="9f45f-231">Restauration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9f45f-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
