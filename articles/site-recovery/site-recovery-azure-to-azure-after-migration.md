---
title: "tooset de machines aaaPrepare la récupération d’urgence entre les régions Azure après tooAzure de migration à l’aide de récupération de Site | Documents Microsoft"
description: "Cet article décrit comment tooprepare machines tooset la récupération d’urgence entre les régions Azure après tooAzure de migration à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="5ac37-103">Répliquer des machines virtuelles Azure tooanother région après migration tooAzure à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5ac37-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="5ac37-104">La réplication Azure Site Recovery pour les machines virtuelles Azure est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="5ac37-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="5ac37-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5ac37-105">Overview</span></span>

<span data-ttu-id="5ac37-106">Cet article vous aide à préparer des machines virtuelles pour la réplication entre les deux régions Azure une fois que ces ordinateurs ont été migrés à partir d’un tooAzure d’environnement sur site à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5ac37-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="5ac37-107">Récupération d’urgence et conformité</span><span class="sxs-lookup"><span data-stu-id="5ac37-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="5ac37-108">Aujourd'hui, plus des entreprises adoptent leur tooAzure les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="5ac37-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="5ac37-109">Avec déplacement de production de site critiques des entreprises tooAzure les charges de travail, configuration de la récupération d’urgence pour ces charges de travail est obligatoire pour la conformité et toosafeguard contre toute interruption dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="5ac37-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="5ac37-110">Étapes de préparation de machines migrées pour la réplication</span><span class="sxs-lookup"><span data-stu-id="5ac37-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="5ac37-111">tooprepare migré des ordinateurs pour configurer la réplication tooanother région Azure :</span><span class="sxs-lookup"><span data-stu-id="5ac37-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="5ac37-112">Achevez la migration.</span><span class="sxs-lookup"><span data-stu-id="5ac37-112">Complete migration.</span></span>
2. <span data-ttu-id="5ac37-113">Installez hello Azure agent si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5ac37-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="5ac37-114">Supprimer le service de mobilité hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="5ac37-115">Redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ac37-115">Restart hello VM.</span></span>

<span data-ttu-id="5ac37-116">Ces étapes sont décrites en détail dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="5ac37-117">Étape 1 : Migrer les charges de travail en cours d’exécution sur les ordinateurs virtuels Hyper-V, les ordinateurs virtuels VMware et toorun des serveurs physiques sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="5ac37-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="5ac37-118">tooset la réplication et de migrer votre Hyper-V, VMware et tooAzure de charges de travail physiques, suivez hello étapes locale Bonjour [virtuels IaaS de Azure migrer entre les régions Azure avec Azure Site Recovery](site-recovery-migrate-to-azure.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="5ac37-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="5ac37-119">Après la migration, vous ne devez toocommit ou supprimer un basculement.</span><span class="sxs-lookup"><span data-stu-id="5ac37-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="5ac37-120">Au lieu de cela, sélectionnez hello **effectuer la Migration** option pour chaque ordinateur, vous souhaitez toomigrate :</span><span class="sxs-lookup"><span data-stu-id="5ac37-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="5ac37-121">Dans **répliquées des éléments**, avec le bouton droit hello machine virtuelle, puis cliquez sur **effectuer la Migration**.</span><span class="sxs-lookup"><span data-stu-id="5ac37-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="5ac37-122">Cliquez sur **OK** étape de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5ac37-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="5ac37-123">Vous pouvez suivre la progression dans les propriétés de machine virtuelle hello en surveillant le travail de Migration complète hello dans **les tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="5ac37-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="5ac37-124">Hello **effectuer la Migration** action se termine le processus de migration hello, supprime la réplication pour l’ordinateur de hello et arrête la facturation de récupération de Site pour l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="5ac37-126">Étape 2 : Installer l’agent de machine virtuelle Azure hello sur l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="5ac37-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="5ac37-127">Bonjour Azure [agent de machine virtuelle](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) doit être installé sur l’ordinateur virtuel de hello pour hello Site Recovery extension toowork et toohelp protègent hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5ac37-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5ac37-128">Depuis la version 9.7.0.0, sur les machines virtuelles Windows, programme d’installation de service de mobilité hello installe également hello dernière machine virtuelle Azure agent disponible.</span><span class="sxs-lookup"><span data-stu-id="5ac37-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="5ac37-129">Sur la migration hello virtual machine répond à l’installation des agents requise pour l’utilisation de toute extension de machine virtuelle, notamment l’extension de Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="5ac37-130">Bonjour Azure VM agent besoins toobe manuellement uniquement installée si hello service mobilité installé sur hello migrés machine est 9,6 ou version antérieure.</span><span class="sxs-lookup"><span data-stu-id="5ac37-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="5ac37-131">Hello tableau suivant fournit des informations supplémentaires sur l’installation d’agent de machine virtuelle hello et de validation qu’il a été installé :</span><span class="sxs-lookup"><span data-stu-id="5ac37-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="5ac37-132">**opération**</span><span class="sxs-lookup"><span data-stu-id="5ac37-132">**Operation**</span></span> | <span data-ttu-id="5ac37-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="5ac37-133">**Windows**</span></span> | <span data-ttu-id="5ac37-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="5ac37-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ac37-135">L’installation d’agent de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="5ac37-135">Installing hello VM agent</span></span> |<span data-ttu-id="5ac37-136">Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="5ac37-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="5ac37-137">Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="5ac37-138">Installer hello dernières [agent Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5ac37-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="5ac37-139">Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="5ac37-140">Nous vous recommandons d’installer l’agent de hello à partir de votre référentiel de distribution.</span><span class="sxs-lookup"><span data-stu-id="5ac37-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="5ac37-141">Nous *ne recommandons pas* l’installation de l’agent Linux VM de hello directement à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ac37-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="5ac37-142">Valider l’installation de l’agent de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="5ac37-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="5ac37-143">1. Parcourir le dossier de C:\WindowsAzure\Packages toohello Bonjour Azure VM.</span><span class="sxs-lookup"><span data-stu-id="5ac37-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="5ac37-144">Vous devez voir fichier WaAppAgent.exe de hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="5ac37-145">2. Clic droit sur hello fichier, accédez trop**propriétés**, puis sélectionnez hello **détails** hello d’onglet **Version du produit** champ doit être 2.6.1198.718 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5ac37-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="5ac37-146">N/A</span><span class="sxs-lookup"><span data-stu-id="5ac37-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="5ac37-147">Étape 3 : Suppression hello service mobilité de hello migrés machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ac37-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="5ac37-148">Si vous avez migré votre machines de VMware locales ou les serveurs physiques sur Windows/Linux, vous devez toomanually suppression et la désinstallation du service hello mobilité à partir de l’ordinateur virtuel migré de hello.</span><span class="sxs-lookup"><span data-stu-id="5ac37-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5ac37-149">Cette étape n’est pas nécessaire pour tooAzure migré des ordinateurs virtuels Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="5ac37-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="5ac37-150">Désinstaller le service de mobilité hello sur un ordinateur Windows Server</span><span class="sxs-lookup"><span data-stu-id="5ac37-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="5ac37-151">Utilisez une des hello suivant du service de mobilité de méthodes toouninstall hello sur un ordinateur Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5ac37-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="5ac37-152">Désinstaller à l’aide de l’interface utilisateur Windows de hello</span><span class="sxs-lookup"><span data-stu-id="5ac37-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="5ac37-153">Dans le panneau de configuration de hello, sélectionnez **programmes**.</span><span class="sxs-lookup"><span data-stu-id="5ac37-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="5ac37-154">Sélectionnez **Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery**, puis sélectionnez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="5ac37-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="5ac37-155">Désinstallation avec une invite de commandes</span><span class="sxs-lookup"><span data-stu-id="5ac37-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="5ac37-156">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5ac37-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5ac37-157">service de mobilité hello toouninstall, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ac37-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="5ac37-158">Désinstaller le service de mobilité hello sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="5ac37-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="5ac37-159">Sur votre serveur Linux, connectez-vous en tant qu’utilisateur **root**.</span><span class="sxs-lookup"><span data-stu-id="5ac37-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="5ac37-160">Dans un terminal, accédez trop/utilisateur/local/récupération automatique du système.</span><span class="sxs-lookup"><span data-stu-id="5ac37-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="5ac37-161">service de mobilité hello toouninstall, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ac37-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="5ac37-162">Étape 4 : Redémarrer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ac37-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="5ac37-163">Après avoir désinstallé le service de mobilité hello, hello redémarrage machine virtuelle avant de configurer de réplication tooanother région Azure.</span><span class="sxs-lookup"><span data-stu-id="5ac37-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ac37-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ac37-164">Next steps</span></span>
- <span data-ttu-id="5ac37-165">Commencer à protéger vos charges de travail en [répliquant des machines virtuelles Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5ac37-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="5ac37-166">Découvrir l’[Aide à la mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="5ac37-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
