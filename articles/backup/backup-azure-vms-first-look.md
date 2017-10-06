---
title: "Découverte : Sauvegarder des machines virtuelles Azure avec un coffre de sauvegarde | Microsoft Docs"
description: "Utilisez tooback portail classique de hello de coffre de sauvegarde tooa de machines virtuelles Azure. Ce didacticiel explique toutes les phases, y compris la création du coffre de sauvegarde hello, l’inscription d’ordinateurs virtuels de hello, création de stratégie de sauvegarde et en cours d’exécution du travail de sauvegarde initiale hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="91806-104">Découverte : sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="91806-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91806-105">Protéger les machines virtuelles avec un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="91806-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="91806-106">Protéger les machines virtuelles Azure avec un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="91806-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="91806-107">Ce didacticiel vous guide tout au long des étapes de hello pour la sauvegarde d’un machine virtuelle Azure (VM) tooa coffre de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="91806-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="91806-108">Cet article décrit le modèle classique de hello ou modèle de déploiement de Service Manager, pour la sauvegarde des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="91806-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="91806-109">Hello étapes suivantes s’appliquent uniquement les coffres tooBackup créés dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="91806-110">Microsoft recommande d’utiliser le modèle de gestionnaire de ressources hello pour les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="91806-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="91806-111">Si vous êtes intéressé par sauvegarde un coffre de Services de récupération tooa machine virtuelle qui appartient tooa groupe de ressources, consultez [tout d’abord rechercher : protéger les machines virtuelles avec un coffre recovery services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="91806-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="91806-112">toosuccessfully effectuer des opérations suivantes de hello didacticiel, ces conditions doivent être réunies :</span><span class="sxs-lookup"><span data-stu-id="91806-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="91806-113">Vous avez créé une machine virtuelle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="91806-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="91806-114">Hello machine virtuelle a des adresses IP publiques de connectivité tooAzure.</span><span class="sxs-lookup"><span data-stu-id="91806-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="91806-115">Pour plus d’informations, consultez la rubrique [Connectivité réseau](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="91806-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="91806-116">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="91806-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="91806-117">Ce didacticiel est pour une utilisation avec les ordinateurs virtuels créés dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="91806-118">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="91806-118">Create a backup vault</span></span>
<span data-ttu-id="91806-119">Un coffre de sauvegarde est une entité qui stocke toutes les sauvegardes de hello et les points de récupération qui ont été créées au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="91806-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="91806-120">coffre de sauvegarde Hello contient également des stratégies de sauvegarde hello sont appliqués toohello des ordinateurs virtuels en cours de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="91806-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91806-121">À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.</span><span class="sxs-lookup"><span data-stu-id="91806-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="91806-122">Vous pouvez mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="91806-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="91806-123">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="91806-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="91806-124">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="91806-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="91806-125">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91806-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="91806-126">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="91806-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="91806-127">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="91806-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="91806-128">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="91806-129">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="91806-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="91806-130">Découverte et inscription des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="91806-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="91806-131">Avant d’inscrire hello machine virtuelle dans un coffre, exécutez tooidentify de processus de découverte hello de nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="91806-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="91806-132">Cela retourne une liste d’ordinateurs virtuels dans l’abonnement hello, ainsi que des informations supplémentaires telles que le nom du service cloud hello et la région de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="91806-133">Connectez-vous à toohello [portail Azure Classic](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="91806-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="91806-134">Bonjour portail Azure classic, cliquez sur **Services de récupération** liste de hello tooopen des archivages de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="91806-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="91806-135">![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="91806-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="91806-136">À partir de la liste de hello des coffres, sélectionnez tooback de coffre hello d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="91806-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="91806-137">Lorsque vous sélectionnez votre archivage, il s’ouvre dans hello **Quick Start** page</span><span class="sxs-lookup"><span data-stu-id="91806-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="91806-138">Dans le menu de coffre hello, cliquez sur **éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="91806-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="91806-140">À partir de hello **Type** menu, sélectionnez **Machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="91806-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="91806-142">Cliquez sur **DISCOVER** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="91806-143">![Bouton découverte](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="91806-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="91806-144">processus de découverte Hello peut prendre quelques minutes hello virtuels sont en cours sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="91806-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="91806-145">Il existe une notification bas hello écran hello qui vous permet de savoir que hello est en cours.</span><span class="sxs-lookup"><span data-stu-id="91806-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Détection des machines virtuelles](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="91806-147">modifications de la notification Hello lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="91806-147">hello notification changes when hello process is complete.</span></span>

    ![Détection exécutée](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="91806-149">Cliquez sur **inscrire** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="91806-150">![Bouton Inscription](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="91806-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="91806-151">Bonjour **enregistrer les éléments** menu contextuel, sélectionnez hello ordinateurs virtuels que vous souhaitez tooregister.</span><span class="sxs-lookup"><span data-stu-id="91806-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="91806-152">Plusieurs machines virtuelles peuvent être inscrites en même temps.</span><span class="sxs-lookup"><span data-stu-id="91806-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="91806-153">Un travail est créé pour chaque machine virtuelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="91806-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="91806-154">Cliquez sur **afficher le travail** dans hello notification toogo toohello **travaux** page.</span><span class="sxs-lookup"><span data-stu-id="91806-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Inscrire du travail](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="91806-156">machine virtuelle de Hello apparaît également dans la liste hello des éléments inscrits, ainsi que de l’état hello de l’opération d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![État de l’inscription 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="91806-158">Lors de la fin de l’opération de hello, hello devient tooreflect hello *inscrit* état.</span><span class="sxs-lookup"><span data-stu-id="91806-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![État de l’inscription 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="91806-160">Installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="91806-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="91806-161">Hello Agent de machine virtuelle Azure doit être installé sur la machine virtuelle Azure à hello sauvegarde extension toowork de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="91806-162">Si votre machine virtuelle a été créé à partir de la galerie Azure de hello, hello Agent de machine virtuelle est déjà présent sur hello machine virtuelle ; Vous pouvez ignorer trop[protéger vos machines virtuelles](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="91806-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="91806-163">Si votre machine virtuelle migré à partir d’un centre de données local, hello VM probablement n’a pas hello installé d’Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="91806-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="91806-164">Vous devez installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello avant hello de tooprotect continuer machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="91806-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="91806-165">Pour obtenir des instructions détaillées sur l’installation de hello Agent de machine virtuelle, consultez hello [section Agent de machine virtuelle de l’article de machines virtuelles de sauvegarde hello](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="91806-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="91806-166">Créer une stratégie de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="91806-166">Create hello backup policy</span></span>
<span data-ttu-id="91806-167">Avant de déclencher de travail de sauvegarde initiale hello, planifier hello quand les instantanés de sauvegarde sont créés.</span><span class="sxs-lookup"><span data-stu-id="91806-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="91806-168">Hello planifier des instantanés de sauvegarde sont effectuées et hello durée ces instantanés sont conservés, est la stratégie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="91806-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="91806-169">informations de rétention Hello sont basées sur le jeu de sauvegarde rotation grand-père-father-son.</span><span class="sxs-lookup"><span data-stu-id="91806-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="91806-170">Accédez de coffre de sauvegarde toohello sous **Services de récupération** dans hello portail Azure Classic, puis cliquez sur **éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="91806-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="91806-171">Sélectionnez **Machine virtuelle Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Sélectionner la charge de travail dans le portail](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="91806-173">Cliquez sur **protéger** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="91806-174">![Cliquer sur Protéger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="91806-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="91806-175">Hello **Assistant protéger** apparaît et répertorie *uniquement* les ordinateurs virtuels qui sont enregistrés et non protégés.</span><span class="sxs-lookup"><span data-stu-id="91806-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurer les paramètres de protection pendant la mise à jour](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="91806-177">Sélectionnez hello ordinateurs virtuels que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="91806-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="91806-178">S’il existe deux ou plusieurs machines virtuelles avec hello même nom, utilisez hello toodistinguish Service Cloud entre des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="91806-179">Sur hello **configurer la protection** menu, sélectionnez une stratégie existante ou créer une nouvelle tooprotect de stratégie hello virtuels que vous avez identifié.</span><span class="sxs-lookup"><span data-stu-id="91806-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="91806-180">Des coffres de sauvegarde ont une stratégie par défaut associée au coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="91806-181">Cette stratégie est un plan quotidien chaque soir d’instantané et instantané quotidien de hello est conservé pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="91806-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="91806-182">Vous pouvez associer plusieurs machines virtuelles à chaque stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="91806-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="91806-183">Toutefois, hello virtual machine ne peut être associé à une stratégie à une heure.</span><span class="sxs-lookup"><span data-stu-id="91806-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Protéger grâce à la nouvelle stratégie](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="91806-185">Une stratégie de sauvegarde inclut un jeu de rétention pour les sauvegardes planifiée de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="91806-186">Si vous sélectionnez une stratégie de sauvegarde existante, vous serez options de rétention hello toomodify impossible à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="91806-187">Sur **de rétention** définir hello quotidienne, hebdomadaire, mensuelle et annuelle étendue pour les points de sauvegarde spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="91806-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="91806-189">Stratégie de rétention spécifie la durée hello pour stocker une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="91806-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="91806-190">Vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="91806-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="91806-191">Cliquez sur **travaux** liste de hello tooview de **configurer la Protection** travaux.</span><span class="sxs-lookup"><span data-stu-id="91806-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Configurer le travail de protection](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="91806-193">Maintenant que vous avez créé la stratégie de hello, passez l’étape suivante de toohello et exécuter la sauvegarde initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="91806-194">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="91806-194">Initial backup</span></span>
<span data-ttu-id="91806-195">Une fois qu’un ordinateur virtuel a été protégé par une stratégie, vous pouvez afficher cette relation à hello **éléments protégés** onglet. Jusqu'à ce que la sauvegarde initiale de hello se produit, hello **état de la Protection** affiche sous la forme **Protected - (en attente de sauvegarde initiale)**.</span><span class="sxs-lookup"><span data-stu-id="91806-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="91806-196">Par défaut, première sauvegarde planifiée du hello est hello *sauvegarde initiale*.</span><span class="sxs-lookup"><span data-stu-id="91806-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Sauvegarde en attente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="91806-198">toostart hello sauvegarde initiale maintenant :</span><span class="sxs-lookup"><span data-stu-id="91806-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="91806-199">Sur hello **éléments protégés** , cliquez sur **sauvegarde maintenant** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="91806-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="91806-200">![Icône Sauvegarder maintenant](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="91806-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="91806-201">Hello service Azure Backup crée une tâche de sauvegarde pour l’opération de sauvegarde initiale hello.</span><span class="sxs-lookup"><span data-stu-id="91806-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="91806-202">Cliquez sur hello **travaux** liste de hello onglet tooview des tâches.</span><span class="sxs-lookup"><span data-stu-id="91806-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Sauvegarde en cours](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="91806-204">Lorsque la sauvegarde initiale est terminée, le statut de hello de machine virtuelle de hello Bonjour **éléments protégés** onglet est *protégé*.</span><span class="sxs-lookup"><span data-stu-id="91806-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="91806-206">La sauvegarde des machines virtuelles est un processus local.</span><span class="sxs-lookup"><span data-stu-id="91806-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="91806-207">Vous ne pouvez pas sauvegarder des ordinateurs virtuels à partir d’un coffre de sauvegarde de tooa région dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="91806-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="91806-208">Par conséquent, pour chaque région Azure qui a des machines virtuelles qui doivent toobe sauvegardé, au moins un coffre de sauvegarde doit être créé dans cette région.</span><span class="sxs-lookup"><span data-stu-id="91806-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="91806-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91806-209">Next steps</span></span>
<span data-ttu-id="91806-210">Maintenant que vous êtes parvenu à sauvegarder une machine virtuelle, d’autres étapes peuvent vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="91806-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="91806-211">Hello plus logique consiste toofamiliarize vous-même avec la restauration de données tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="91806-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="91806-212">Toutefois, il existe des tâches de gestion qui vous aideront à comprendre comment tookeep sécurité de vos données et réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="91806-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="91806-213">Gestion et surveillance de vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="91806-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="91806-214">Restauration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="91806-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="91806-215">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="91806-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="91806-216">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="91806-216">Questions?</span></span>
<span data-ttu-id="91806-217">Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="91806-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
