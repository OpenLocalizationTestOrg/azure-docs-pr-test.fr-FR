---
title: "aaaReset hello mot de passe ou la configuration du Bureau à distance sur un ordinateur virtuel Windows Azure | Documents Microsoft"
description: "Découvrez comment tooreset un mot de passe ou les services Bureau à distance sur une machine virtuelle Windows créée à l’aide du modèle de déploiement classique hello avec hello portail Azure ou Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="3dc45-103">Comment le service Bureau à distance de hello tooreset ou son mot de passe de connexion dans une machine virtuelle Windows créé à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="3dc45-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3dc45-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3dc45-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3dc45-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3dc45-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3dc45-107">Vous pouvez également [effectuer ces étapes pour les machines virtuelles créées avec le modèle de déploiement du Gestionnaire de ressources hello](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="3dc45-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="3dc45-108">Si vous ne pouvez pas vous connecter tooa Windows virtual machine (VM), vous pouvez réinitialiser le mot de passe administrateur local hello ou réinitialiser la configuration du service Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="3dc45-109">Vous pouvez utiliser l’extension d’accès de la machine virtuelle Azure portal ou hello hello dans mot de passe Azure PowerShell tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="3dc45-110">Configuration de tooreset de méthodes ou les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="3dc45-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="3dc45-111">Vous pouvez réinitialiser les services Bureau à distance et les informations d’identification de différentes manières, selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="3dc45-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="3dc45-112">Réinitialiser à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3dc45-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="3dc45-113">Réinitialisation à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dc45-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="3dc45-114">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3dc45-114">Azure portal</span></span>
<span data-ttu-id="3dc45-115">Vous pouvez utiliser hello [portail Azure](https://portal.azure.com) tooreset hello service Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="3dc45-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="3dc45-116">tooexpand hello menus, barres hello trois dans le coin supérieur gauche de hello, puis cliquez sur **machines virtuelles (classiques)**:</span><span class="sxs-lookup"><span data-stu-id="3dc45-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Accédez à votre machine virtuelle Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="3dc45-118">Sélectionnez votre machine virtuelle de Windows, puis cliquez **réinitialiser à distance...** . configuration de bureau à distance tooreset hello apparaît hello boîte de dialogue suivante :</span><span class="sxs-lookup"><span data-stu-id="3dc45-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Page Réinitialiser la configuration RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="3dc45-120">Vous pouvez également réinitialiser le nom d’utilisateur hello et le mot de passe du compte d’administrateur local hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="3dc45-121">À partir de votre machine virtuelle, cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3dc45-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="3dc45-122">Panneau de réinitialisation de mot de passe Hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="3dc45-122">hello password reset blade is displayed:</span></span>

![Page Réinitialiser le mot de passe](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="3dc45-124">Après avoir entré le nouveau nom d’utilisateur hello et le mot de passe, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3dc45-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="3dc45-125">Extension VMAccess et PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dc45-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="3dc45-126">Vérifiez que hello que l’Agent VM est installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="3dc45-127">Hello extension VMAccess n’a pas besoin de toobe installé avant de pouvoir l’utiliser, tant que hello Agent de machine virtuelle est disponible.</span><span class="sxs-lookup"><span data-stu-id="3dc45-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="3dc45-128">Vérifiez que hello Qu'agent de machine virtuelle est déjà installée en utilisant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3dc45-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="3dc45-129">(Remplacez « myCloudService » et « myVM » par les noms hello de votre service cloud et votre machine virtuelle, respectivement.</span><span class="sxs-lookup"><span data-stu-id="3dc45-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="3dc45-130">Pour obtenir ces noms, exécutez `Get-AzureVM` sans paramètre.)</span><span class="sxs-lookup"><span data-stu-id="3dc45-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="3dc45-131">Si hello **écriture-host** commande affiche **True**, hello l’Agent VM est installé.</span><span class="sxs-lookup"><span data-stu-id="3dc45-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="3dc45-132">S’il affiche **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour [Agent de machine virtuelle et Extensions - partie 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) billet de blog Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc45-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="3dc45-133">Si vous avez créé l’ordinateur virtuel de hello à l’aide du portail de hello, vérifiez si `$vm.GetInstance().ProvisionGuestAgent` retourne **True**.</span><span class="sxs-lookup"><span data-stu-id="3dc45-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="3dc45-134">Si ce n’est pas le cas, définissez cette valeur à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="3dc45-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="3dc45-135">Cette commande empêche hello l’erreur suivante lorsque vous exécutez hello **Set-AzureVMExtension** dans les étapes suivantes hello : « Disposition invité Agent doit être activé sur l’objet de machine virtuelle hello avant de définir l’Extension d’accès IaaS VM. »</span><span class="sxs-lookup"><span data-stu-id="3dc45-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="3dc45-136">**Réinitialiser le mot de passe administrateur local hello**</span><span class="sxs-lookup"><span data-stu-id="3dc45-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="3dc45-137">Créer une information d’identification de connexion avec le nom du compte administrateur local en cours hello et un nouveau mot de passe, puis exécutez hello `Set-AzureVMAccessExtension` comme suit.</span><span class="sxs-lookup"><span data-stu-id="3dc45-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="3dc45-138">Si vous tapez un nom différent de compte en cours de hello, hello extension VMAccess renomme le compte d’administrateur local hello affecte le compte de toothat de mot de passe hello et émet une déconnexion de bureau à distance. Si le compte d’administrateur local hello est désactivé, hello extension VMAccess active.</span><span class="sxs-lookup"><span data-stu-id="3dc45-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="3dc45-139">Ces commandes de réinitialisent de la configuration du service Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="3dc45-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="3dc45-140">**Réinitialiser la configuration du service Bureau à distance hello**</span><span class="sxs-lookup"><span data-stu-id="3dc45-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="3dc45-141">tooreset hello Bureau à distance configuration du service, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dc45-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="3dc45-142">Hello extension VMAccess exécute deux commandes sur l’ordinateur virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="3dc45-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="3dc45-143">Cette commande active hello intégré groupe du pare-feu Windows qui autorise le trafic entrant Bureau à distance, qui utilise le port TCP 3389.</span><span class="sxs-lookup"><span data-stu-id="3dc45-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="3dc45-144">Cette commande définit too0 de valeur de Registre fDenyTSConnections hello, l’activation des connexions de bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="3dc45-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dc45-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dc45-145">Next steps</span></span>
<span data-ttu-id="3dc45-146">Si hello extension d’accès Azure VM ne répond pas et que vous êtes un mot de passe ne peut pas tooreset hello, vous pouvez [réinitialisation hello Windows mot de passe local en mode hors connexion](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3dc45-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3dc45-147">Cette méthode est un processus plus avancé et requiert que vous tooconnect hello du disque dur virtuel hello problématique VM tooanother machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3dc45-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="3dc45-148">Suivez les étapes de hello documentés en premier dans cet article et tente uniquement la méthode de réinitialisation hello mot de passe en mode hors connexion en dernier recours.</span><span class="sxs-lookup"><span data-stu-id="3dc45-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="3dc45-149">Extensions et fonctionnalités des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="3dc45-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="3dc45-150">Se connecter tooan machine virtuelle Azure avec RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="3dc45-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="3dc45-151">Résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="3dc45-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

