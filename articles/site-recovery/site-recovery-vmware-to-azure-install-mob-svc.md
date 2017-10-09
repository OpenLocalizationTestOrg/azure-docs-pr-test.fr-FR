---
title: "aaaInstall Service mobilité (VMware ou tooAzure physique) | Documents Microsoft"
description: "Découvrez comment tooinstall hello tooprotect de l’agent Mobility Service vos ordinateurs locaux."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="c6582-103">Installer le Service mobilité (VMware ou tooAzure physique)</span><span class="sxs-lookup"><span data-stu-id="c6582-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="c6582-104">Le Service Azure Site Recovery mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello.</span><span class="sxs-lookup"><span data-stu-id="c6582-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="c6582-105">Déployer Service mobilité tooevery ordinateur (VMware VM ou serveur physique) que vous souhaitez tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c6582-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="c6582-106">Vous pouvez déployer le Service mobilité toohello serveurs que tooprotect à l’aide des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c6582-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="c6582-107">Installation du service Mobilité à l’aide d’outils de déploiement de logiciels tels que System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="c6582-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="c6582-108">Installation du Service Mobilité à l’aide d’Azure Automation et de la Configuration de l’état souhaité (Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="c6582-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="c6582-109">Installer le Service mobilité manuellement en utilisant l’interface utilisateur graphique de hello (GUI)</span><span class="sxs-lookup"><span data-stu-id="c6582-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="c6582-110">Installation manuelle du service Mobilité à l’aide d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="c6582-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="c6582-111">Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c6582-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="c6582-112">Depuis la version 9.7.0.0, sur les machines virtuelles (VM), Windows installer du Service mobilité hello installe également hello dernière version disponible [agent Azure VM](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="c6582-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="c6582-113">Lorsqu’un ordinateur bascule tooAzure, ordinateur de hello satisfait hello agent requis pour l’installation à l’aide de n’importe quelle extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6582-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6582-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c6582-114">Prerequisites</span></span>
<span data-ttu-id="c6582-115">Effectuez ces étapes préalables avant d’installer manuellement le service Mobilité sur votre serveur :</span><span class="sxs-lookup"><span data-stu-id="c6582-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="c6582-116">Connectez-vous au serveur de configuration tooyour, puis ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c6582-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c6582-117">Modifier le dossier bin de hello répertoire toohello, puis créer un fichier de mot de passe :</span><span class="sxs-lookup"><span data-stu-id="c6582-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="c6582-118">Stockez le fichier de mot de passe de hello dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c6582-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="c6582-119">Vous utilisez des fichiers de hello pendant hello installation du Service mobilité.</span><span class="sxs-lookup"><span data-stu-id="c6582-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="c6582-120">Programmes d’installation du Service mobilité pour tous les systèmes d’exploitation pris en charge se trouvent dans le dossier de %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.</span><span class="sxs-lookup"><span data-stu-id="c6582-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="c6582-121">Correspondance entre le programme d’installation du service Mobilité et le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="c6582-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="c6582-122">Nom du modèle de fichier de programme d’installation</span><span class="sxs-lookup"><span data-stu-id="c6582-122">Installer file template name</span></span>| <span data-ttu-id="c6582-123">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="c6582-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="c6582-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="c6582-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="c6582-125">Windows Server 2008 R2 SP1 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c6582-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="c6582-126">Windows Server 2012 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c6582-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="c6582-127">Windows Server 2012 R2 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="c6582-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="c6582-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="c6582-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="c6582-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="c6582-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="c6582-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="c6582-133">CentOS 7.0, 7.1, 7.2 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="c6582-134">CentOs 7.3 (migration uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="c6582-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="c6582-136">SUSE Linux Enterprise Server 11 SP3 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="c6582-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="c6582-138">SUSE Linux Enterprise Server 11 SP4 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="c6582-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="c6582-140">Oracle Enterprise Linux 6.4, 6.5 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="c6582-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="c6582-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="c6582-142">Ubuntu Linux 14.04 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="c6582-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="c6582-143">Installer le Service mobilité manuellement à l’aide de l’interface graphique utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="c6582-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="c6582-144">Si vous utilisez un **serveur de Configuration** tooreplicate **machines virtuelles Azure IaaS** à partir d’un tooanother abonnement Azure ou la région puis **utiliser hello d’installation en fonction de ligne de commande**  (méthode)</span><span class="sxs-lookup"><span data-stu-id="c6582-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="c6582-145">Installation manuelle du service Mobilité à l’aide d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="c6582-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="c6582-146">Installation avec une ligne de commande sur un ordinateur Windows</span><span class="sxs-lookup"><span data-stu-id="c6582-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="c6582-147">Installation avec une ligne de commande sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="c6582-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="c6582-148">Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c6582-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="c6582-149">toodo une installation push du Service mobilité à l’aide de récupération de Site, tous les ordinateurs cibles doivent respecter hello suivant des conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="c6582-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="c6582-150">Après l’installation du Service mobilité, Bonjour portail Azure, sélectionnez hello **répliquer** toostart bouton protéger ces ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c6582-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="c6582-151">Désinstallation d’un service Mobilité sur un ordinateur Windows Server</span><span class="sxs-lookup"><span data-stu-id="c6582-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="c6582-152">Utilisez une des hello suivant les méthodes toouninstall Service mobilité sur un ordinateur Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c6582-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="c6582-153">Désinstaller à l’aide de l’interface graphique utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="c6582-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="c6582-154">Dans le panneau de configuration, sélectionnez **Programmes**.</span><span class="sxs-lookup"><span data-stu-id="c6582-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="c6582-155">Sélectionnez **Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery**, puis sélectionnez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="c6582-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="c6582-156">Désinstallation avec une invite de commandes</span><span class="sxs-lookup"><span data-stu-id="c6582-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="c6582-157">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c6582-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c6582-158">toouninstall Service mobilité, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6582-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="c6582-159">Désinstaller le service Mobilité sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="c6582-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="c6582-160">Sur votre serveur Linux, connectez-vous en tant qu’utilisateur **root**.</span><span class="sxs-lookup"><span data-stu-id="c6582-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="c6582-161">Dans un terminal, accédez trop/utilisateur/local/récupération automatique du système.</span><span class="sxs-lookup"><span data-stu-id="c6582-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="c6582-162">toouninstall Service mobilité, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6582-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
