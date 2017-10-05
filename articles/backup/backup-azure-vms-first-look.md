---
title: "Découverte : Sauvegarder des machines virtuelles Azure avec un coffre de sauvegarde | Microsoft Docs"
description: "Utilisez le portail classique pour sauvegarder des machines virtuelles Azure dans un coffre de sauvegarde. Ce didacticiel décrit toutes les phases, y compris la création du coffre de sauvegarde, l’inscription des machines virtuelles, l’élaboration de la stratégie de sauvegarde et l’exécution du travail de sauvegarde initiale."
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
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="52c1e-104">Découverte : sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="52c1e-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52c1e-105">Protéger les machines virtuelles avec un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="52c1e-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="52c1e-106">Protéger les machines virtuelles Azure avec un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="52c1e-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="52c1e-107">Ce didacticiel vous accompagne tout au long de la procédure de sauvegarde d’une machine virtuelle Azure vers un archivage de sauvegarde dans Azure.</span><span class="sxs-lookup"><span data-stu-id="52c1e-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="52c1e-108">Cet article décrit le modèle classique ou le modèle de déploiement Service Manager, pour la sauvegarde des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="52c1e-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="52c1e-109">Les étapes suivantes s’appliquent uniquement aux coffres de sauvegarde créés dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="52c1e-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="52c1e-110">Pour les nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52c1e-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="52c1e-111">Si vous souhaitez sauvegarder une machine virtuelle dans un coffre Recovery Services qui appartient à un groupe de ressources, consultez l’article [Découverte : Protéger les machines virtuelles avec un coffre Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="52c1e-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="52c1e-112">Pour pouvoir suivre ce didacticiel, les conditions préalables ci-après doivent être réunies :</span><span class="sxs-lookup"><span data-stu-id="52c1e-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="52c1e-113">Vous avez créé une machine virtuelle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="52c1e-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="52c1e-114">La machine virtuelle dispose d’une connectivité à des adresses IP publiques Azure.</span><span class="sxs-lookup"><span data-stu-id="52c1e-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="52c1e-115">Pour plus d’informations, consultez la rubrique [Connectivité réseau](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="52c1e-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="52c1e-116">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="52c1e-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="52c1e-117">Ce didacticiel est destiné aux machines virtuelles créées dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="52c1e-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="52c1e-118">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="52c1e-118">Create a backup vault</span></span>
<span data-ttu-id="52c1e-119">Un coffre de sauvegarde est une entité qui stocke les sauvegardes et les points de récupération créés au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="52c1e-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="52c1e-120">Le coffre de sauvegarde contient également les stratégies de sauvegarde qui sont appliquées aux machines virtuelles en cours de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c1e-121">Depuis mars 2017, vous ne pouvez plus utiliser le portail Classic pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="52c1e-122">Vous pouvez mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="52c1e-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="52c1e-123">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="52c1e-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="52c1e-124">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="52c1e-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="52c1e-125">À compter du 15 octobre 2017, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="52c1e-126">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="52c1e-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="52c1e-127">tous les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="52c1e-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="52c1e-128">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="52c1e-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="52c1e-129">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="52c1e-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="52c1e-130">Découverte et inscription des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="52c1e-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="52c1e-131">Avant d’enregistrer la machine virtuelle dans un coffre, lancez le processus de découverte pour identifier les nouvelles machines virtuelles éventuelles.</span><span class="sxs-lookup"><span data-stu-id="52c1e-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="52c1e-132">Ce dernier renvoie la liste des machines virtuelles de l’abonnement et des informations supplémentaires, comme le nom du service cloud et la région.</span><span class="sxs-lookup"><span data-stu-id="52c1e-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="52c1e-133">Connectez-vous au [portail Azure Classic](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="52c1e-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="52c1e-134">Dans le portail Azure Classic, cliquez sur **Recovery Services** pour ouvrir la liste des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="52c1e-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="52c1e-135">![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="52c1e-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="52c1e-136">Dans la liste des coffres, sélectionnez le coffre de sauvegarde d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="52c1e-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="52c1e-137">Votre coffre sélectionné s’ouvre à la page **Démarrage rapide** .</span><span class="sxs-lookup"><span data-stu-id="52c1e-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="52c1e-138">Dans le menu du coffre, cliquez sur **Éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-138">From the vault menu, click **Registered Items**.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="52c1e-140">Dans le menu **Type**, sélectionnez **Machine virtuelle Azure**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Sélectionner la charge de travail](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="52c1e-142">Cliquez sur **DÉCOUVRIR** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="52c1e-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="52c1e-143">![Bouton Découvrir](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="52c1e-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="52c1e-144">Le processus de découverte peut durer quelques minutes, le temps que les machines virtuelles soient affichées sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="52c1e-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="52c1e-145">Une notification affichée en bas de l’écran vous informe que le processus est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="52c1e-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Détection des machines virtuelles](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="52c1e-147">La notification change lorsque le processus est terminé.</span><span class="sxs-lookup"><span data-stu-id="52c1e-147">The notification changes when the process is complete.</span></span>

    ![Détection exécutée](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="52c1e-149">Cliquez sur **INSCRIRE** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="52c1e-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="52c1e-150">![Bouton Inscription](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="52c1e-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="52c1e-151">Dans le menu contextuel **Inscrire les éléments** , choisissez les machines virtuelles que vous souhaitez inscrire.</span><span class="sxs-lookup"><span data-stu-id="52c1e-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="52c1e-152">Plusieurs machines virtuelles peuvent être inscrites en même temps.</span><span class="sxs-lookup"><span data-stu-id="52c1e-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="52c1e-153">Un travail est créé pour chaque machine virtuelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="52c1e-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="52c1e-154">Cliquez sur **Afficher le travail** dans la notification pour accéder à la page **Travaux**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Inscrire du travail](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="52c1e-156">La machine virtuelle est également affichée dans la liste des éléments inscrits avec l’état de l’opération d’inscription.</span><span class="sxs-lookup"><span data-stu-id="52c1e-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![État de l’inscription 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="52c1e-158">Une fois l’opération terminée, l’état change pour refléter l’état *inscrit* .</span><span class="sxs-lookup"><span data-stu-id="52c1e-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![État de l’inscription 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="52c1e-160">Installer l’agent de machine virtuelle sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="52c1e-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="52c1e-161">L’agent de machine virtuelle Azure doit être installé sur la machine virtuelle Azure pour permettre la prise en charge de l’extension Backup.</span><span class="sxs-lookup"><span data-stu-id="52c1e-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="52c1e-162">Si votre machine virtuelle a été créée à partir de la galerie Azure, l’agent de machine virtuelle est déjà installé sur la machine virtuelle. Vous pouvez directement passer à l’étape de [protection de vos machines virtuelles](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="52c1e-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="52c1e-163">Si votre machine virtuelle a migré à partir d'un centre de données local, il est probable que l’agent de machine virtuelle n’y soit pas installé.</span><span class="sxs-lookup"><span data-stu-id="52c1e-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="52c1e-164">Vous devez installer l'agent sur la machine virtuelle avant de passer à l’étape de protection de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="52c1e-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="52c1e-165">Pour obtenir des instructions détaillées sur l’installation de l’agent de machine virtuelle, consultez la [section Agent VM de l’article sur la sauvegarde des machines virtuelles](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="52c1e-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="52c1e-166">Création de la stratégie de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="52c1e-166">Create the backup policy</span></span>
<span data-ttu-id="52c1e-167">Avant de déclencher le travail de sauvegarde initiale, définissez la planification des instantanés de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="52c1e-168">La planification des instantanés de sauvegarde et la durée de rétention de ces instantanés constituent la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="52c1e-169">Les informations de rétention sont basées sur le schéma de rotation des sauvegardes grand-père-père-fils.</span><span class="sxs-lookup"><span data-stu-id="52c1e-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="52c1e-170">Accédez au coffre de sauvegarde qui se trouve sous **Recovery Services** dans le portail Azure Classic, puis cliquez sur **Éléments inscrits**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="52c1e-171">Sélectionnez **Machine virtuelle Azure** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="52c1e-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Sélectionner la charge de travail dans le portail](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="52c1e-173">En bas de la page, cliquez sur **PROTÉGER** .</span><span class="sxs-lookup"><span data-stu-id="52c1e-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="52c1e-174">![Cliquer sur Protéger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="52c1e-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="52c1e-175">**L’Assistant Protection des éléments** s’affiche et répertorie *uniquement* les machines virtuelles inscrites qui ne sont pas protégées.</span><span class="sxs-lookup"><span data-stu-id="52c1e-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurer les paramètres de protection pendant la mise à jour](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="52c1e-177">Sélectionnez les machines virtuelles que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="52c1e-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="52c1e-178">Si au moins deux machines virtuelles portent le même nom, utilisez le service cloud pour les distinguer.</span><span class="sxs-lookup"><span data-stu-id="52c1e-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="52c1e-179">Dans le menu **Configurer la protection** , sélectionnez une stratégie existante ou créez-en une pour protéger les machines virtuelles que vous avez identifiées.</span><span class="sxs-lookup"><span data-stu-id="52c1e-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="52c1e-180">Les nouveaux coffres de sauvegarde ont une stratégie par défaut associée au coffre.</span><span class="sxs-lookup"><span data-stu-id="52c1e-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="52c1e-181">Cette stratégie prend un instantané chaque soir ; celui-ci est conservé pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="52c1e-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="52c1e-182">Vous pouvez associer plusieurs machines virtuelles à chaque stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="52c1e-183">Toutefois, vous ne pouvez associer votre machine virtuelle qu’à une seule stratégie à la fois.</span><span class="sxs-lookup"><span data-stu-id="52c1e-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Protéger grâce à la nouvelle stratégie](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="52c1e-185">Une stratégie de sauvegarde inclut le schéma de rétention des sauvegardes planifiées.</span><span class="sxs-lookup"><span data-stu-id="52c1e-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="52c1e-186">Si vous sélectionnez une stratégie de sauvegarde existante, vous ne pourrez pas modifier les options de rétention à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="52c1e-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="52c1e-187">Dans le champ **Durée de rétention** , définissez l’intervalle des points de sauvegarde spécifiques (quotidien, hebdomadaire, mensuel ou annuel).</span><span class="sxs-lookup"><span data-stu-id="52c1e-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="52c1e-189">La stratégie de rétention spécifie la durée de stockage d’une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="52c1e-190">Vous pouvez spécifier des stratégies de rétention différentes en fonction de la date à laquelle la sauvegarde est effectuée.</span><span class="sxs-lookup"><span data-stu-id="52c1e-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="52c1e-191">Cliquez sur **Travaux** pour afficher la liste des travaux **Configurer la protection**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Configurer le travail de protection](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="52c1e-193">Maintenant que vous avez créé la stratégie, passez à l'étape suivante et lancez la sauvegarde initiale.</span><span class="sxs-lookup"><span data-stu-id="52c1e-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="52c1e-194">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="52c1e-194">Initial backup</span></span>
<span data-ttu-id="52c1e-195">Une fois la machine virtuelle protégée par une stratégie, vous pouvez afficher cette relation dans l’onglet **Éléments protégés** . Avant l’exécution de la sauvegarde initiale, la valeur **Protégé (en attente de sauvegarde initiale)** s’affiche sous **État de la protection**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="52c1e-196">Par défaut, la première sauvegarde planifiée est la *sauvegarde initiale*.</span><span class="sxs-lookup"><span data-stu-id="52c1e-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Sauvegarde en attente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="52c1e-198">Pour lancer la sauvegarde initiale :</span><span class="sxs-lookup"><span data-stu-id="52c1e-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="52c1e-199">Cliquez sur le bouton **Sauvegarder maintenant** en bas de la page **Éléments protégés**.</span><span class="sxs-lookup"><span data-stu-id="52c1e-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="52c1e-200">![Icône Sauvegarder maintenant](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="52c1e-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="52c1e-201">Le service Azure Backup crée un travail de sauvegarde pour l’opération de sauvegarde initiale.</span><span class="sxs-lookup"><span data-stu-id="52c1e-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="52c1e-202">Cliquez sur l’onglet **Travaux** pour afficher la liste des travaux.</span><span class="sxs-lookup"><span data-stu-id="52c1e-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Sauvegarde en cours](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="52c1e-204">Une fois la sauvegarde initiale terminée, l’état de la machine virtuelle indiquée dans l’onglet **Éléments protégés** est défini sur la valeur *Protégé*.</span><span class="sxs-lookup"><span data-stu-id="52c1e-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![La machine virtuelle est sauvegardée avec un point de récupération](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="52c1e-206">La sauvegarde des machines virtuelles est un processus local.</span><span class="sxs-lookup"><span data-stu-id="52c1e-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="52c1e-207">Vous ne pouvez pas sauvegarder les machines virtuelles d’une région donnée vers un archivage de sauvegarde d’une autre région.</span><span class="sxs-lookup"><span data-stu-id="52c1e-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="52c1e-208">Par conséquent, il faut créer au moins un archivage pour chaque région Azure équipée de machines virtuelles nécessitant une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="52c1e-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="52c1e-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52c1e-209">Next steps</span></span>
<span data-ttu-id="52c1e-210">Maintenant que vous êtes parvenu à sauvegarder une machine virtuelle, d’autres étapes peuvent vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="52c1e-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="52c1e-211">L’étape la plus logique consiste à vous familiariser avec la restauration des données sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="52c1e-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="52c1e-212">Toutefois, certaines tâches de gestion vous aideront à comprendre comment protéger vos données et réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="52c1e-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="52c1e-213">Gestion et surveillance de vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="52c1e-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="52c1e-214">Restauration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="52c1e-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="52c1e-215">Instructions pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="52c1e-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="52c1e-216">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="52c1e-216">Questions?</span></span>
<span data-ttu-id="52c1e-217">Si vous avez des questions ou si vous souhaitez que certaines fonctionnalités soient incluses, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="52c1e-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
