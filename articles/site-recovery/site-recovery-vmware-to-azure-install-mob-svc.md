---
title: "Installation du service Mobilité (VMware ou serveur physique vers Azure) | Microsoft Docs"
description: "Découvrez comment installer l’agent du service Mobilité pour protéger vos machines locales."
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="2210e-103">Installation du service Mobilité (VMware ou serveur physique vers Azure)</span><span class="sxs-lookup"><span data-stu-id="2210e-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="2210e-104">Le service de mobilité Azure Site Recovery capture les écritures de données sur un ordinateur, puis les transfère au serveur de traitement.</span><span class="sxs-lookup"><span data-stu-id="2210e-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="2210e-105">Déployez le service Mobilité sur chaque ordinateur (machine virtuelle VMware ou serveur physique) que vous souhaitez répliquer vers Azure.</span><span class="sxs-lookup"><span data-stu-id="2210e-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="2210e-106">Vous pouvez déployer le service Mobilité pour les serveurs que vous souhaitez protéger à l’aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2210e-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="2210e-107">Installation du service Mobilité à l’aide d’outils de déploiement de logiciels tels que System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="2210e-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="2210e-108">Installation du Service Mobilité à l’aide d’Azure Automation et de la Configuration de l’état souhaité (Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="2210e-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="2210e-109">Installation du service Mobilité manuellement à l’aide de l’interface utilisateur graphique</span><span class="sxs-lookup"><span data-stu-id="2210e-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="2210e-110">Installation manuelle du service Mobilité à l’aide d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="2210e-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="2210e-111">Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2210e-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="2210e-112">À compter de la version 9.7.0.0, sur les machines virtuelles Windows, le programme d’installation du service Mobilité installe également [l’agent Azure VM](../virtual-machines/windows/extensions-features.md#azure-vm-agent) le plus récent disponible.</span><span class="sxs-lookup"><span data-stu-id="2210e-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="2210e-113">Lorsqu’un ordinateur bascule vers Azure, l’ordinateur répond aux conditions requises d’installation de l’agent pour l’utilisation de n’importe quelle extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2210e-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2210e-114">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="2210e-114">Prerequisites</span></span>
<span data-ttu-id="2210e-115">Effectuez ces étapes préalables avant d’installer manuellement le service Mobilité sur votre serveur :</span><span class="sxs-lookup"><span data-stu-id="2210e-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="2210e-116">Connectez-vous à votre serveur de configuration, puis ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2210e-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2210e-117">Indiquez le dossier bin, puis créez un fichier de phrase secrète :</span><span class="sxs-lookup"><span data-stu-id="2210e-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="2210e-118">Stockez le fichier de phrase secrète dans un emplacement sécurisé.</span><span class="sxs-lookup"><span data-stu-id="2210e-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="2210e-119">Vous utilisez le fichier pendant l’installation du service Mobilité.</span><span class="sxs-lookup"><span data-stu-id="2210e-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="2210e-120">Les programmes d’installation du service Mobilité pour tous les systèmes d’exploitation pris en charge se trouvent dans le dossier %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.</span><span class="sxs-lookup"><span data-stu-id="2210e-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="2210e-121">Correspondance entre le programme d’installation du service Mobilité et le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="2210e-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="2210e-122">Nom du modèle de fichier de programme d’installation</span><span class="sxs-lookup"><span data-stu-id="2210e-122">Installer file template name</span></span>| <span data-ttu-id="2210e-123">Système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="2210e-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="2210e-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="2210e-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="2210e-125">Windows Server 2008 R2 SP1 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="2210e-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="2210e-126">Windows Server 2012 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="2210e-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="2210e-127">Windows Server 2012 R2 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="2210e-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="2210e-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="2210e-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="2210e-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="2210e-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="2210e-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="2210e-133">CentOS 7.0, 7.1, 7.2 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="2210e-134">CentOs 7.3 (migration uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="2210e-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="2210e-136">SUSE Linux Enterprise Server 11 SP3 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="2210e-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="2210e-138">SUSE Linux Enterprise Server 11 SP4 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="2210e-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="2210e-140">Oracle Enterprise Linux 6.4, 6.5 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="2210e-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="2210e-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="2210e-142">Ubuntu Linux 14.04 (64 bits uniquement)</span><span class="sxs-lookup"><span data-stu-id="2210e-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="2210e-143">Installer le service Mobilité manuellement à l’aide de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="2210e-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2210e-144">Si vous utilisez un **Serveur de configuration** pour répliquer les **machines virtuelles Azure IaaS** d’un abonnement/d’une région Azure sur un(e) autre, il vous faudra **utiliser la méthode d’installation en ligne de commande**.</span><span class="sxs-lookup"><span data-stu-id="2210e-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="2210e-145">Installation manuelle du service Mobilité à l’aide d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="2210e-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="2210e-146">Installation avec une ligne de commande sur un ordinateur Windows</span><span class="sxs-lookup"><span data-stu-id="2210e-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="2210e-147">Installation avec une ligne de commande sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="2210e-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="2210e-148">Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2210e-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="2210e-149">Pour effectuer une installation Push du service Mobilité à l’aide de Site Recovery, tous les ordinateurs cibles doivent répondre aux conditions préalables suivantes.</span><span class="sxs-lookup"><span data-stu-id="2210e-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="2210e-150">Une fois le service Mobilité installé, dans le portail Azure, sélectionnez le bouton **Répliquer** pour commencer à protéger ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2210e-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="2210e-151">Désinstallation d’un service Mobilité sur un ordinateur Windows Server</span><span class="sxs-lookup"><span data-stu-id="2210e-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="2210e-152">Utilisez une des méthodes suivantes pour désinstaller le service Mobilité sur un ordinateur Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2210e-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="2210e-153">Désinstallation à l’aide de l’interface utilisateur graphique</span><span class="sxs-lookup"><span data-stu-id="2210e-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="2210e-154">Dans le panneau de configuration, sélectionnez **Programmes**.</span><span class="sxs-lookup"><span data-stu-id="2210e-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="2210e-155">Sélectionnez **Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery**, puis sélectionnez **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="2210e-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="2210e-156">Désinstallation avec une invite de commandes</span><span class="sxs-lookup"><span data-stu-id="2210e-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="2210e-157">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2210e-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2210e-158">Exécutez la commande suivante pour désinstaller le service Mobilité :</span><span class="sxs-lookup"><span data-stu-id="2210e-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="2210e-159">Désinstaller le service Mobilité sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="2210e-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="2210e-160">Sur votre serveur Linux, connectez-vous en tant qu’utilisateur **root**.</span><span class="sxs-lookup"><span data-stu-id="2210e-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="2210e-161">Dans un terminal, accédez à /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="2210e-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="2210e-162">Exécutez la commande suivante pour désinstaller le service Mobilité :</span><span class="sxs-lookup"><span data-stu-id="2210e-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
