---
title: "aaaReset hello mot de passe ou la configuration du Bureau à distance sur une machine virtuelle Windows | Documents Microsoft"
description: "Découvrez comment tooreset un mot de passe ou des services Bureau à distance sur une machine virtuelle Windows à l’aide de hello portail Azure ou Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="01d52-103">Comment tooreset hello service Bureau à distance ou son mot de passe de connexion dans une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="01d52-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="01d52-104">Si vous ne pouvez pas vous connecter tooa Windows virtual machine (VM), vous pouvez réinitialiser le mot de passe administrateur local hello ou réinitialiser la configuration du service Bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="01d52-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="01d52-105">Vous pouvez utiliser l’extension d’accès de la machine virtuelle Azure portal ou hello hello dans mot de passe Azure PowerShell tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="01d52-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="01d52-106">Si vous utilisez PowerShell, assurez-vous que vous avez hello [dernier module PowerShell installé et configuré](/powershell/azure/overview) et vous n’êtes pas connecté tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="01d52-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="01d52-107">Vous pouvez également [effectuer ces étapes pour les machines virtuelles créées avec le modèle de déploiement classique hello](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="01d52-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="01d52-108">Configuration de tooreset de méthodes ou les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="01d52-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="01d52-109">Vous pouvez réinitialiser les services Bureau à distance et les informations d’identification de différentes manières, selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="01d52-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="01d52-110">Réinitialiser à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="01d52-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="01d52-111">Réinitialisation à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01d52-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="01d52-112">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="01d52-112">Azure portal</span></span>
<span data-ttu-id="01d52-113">tooexpand hello menus, barres hello trois dans le coin supérieur gauche de hello, puis cliquez sur **virtuels**:</span><span class="sxs-lookup"><span data-stu-id="01d52-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Accédez à votre machine virtuelle Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="01d52-115">**Réinitialiser le mot de passe administrateur local hello**</span><span class="sxs-lookup"><span data-stu-id="01d52-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="01d52-116">Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="01d52-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="01d52-117">Panneau de réinitialisation de mot de passe Hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="01d52-117">hello password reset blade is displayed:</span></span>

![Page Réinitialiser le mot de passe](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="01d52-119">Entrez le nom d’utilisateur hello et un nouveau mot de passe, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="01d52-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="01d52-120">Réessayez de vous connecter tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="01d52-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="01d52-121">**Réinitialiser la configuration du service Bureau à distance hello**</span><span class="sxs-lookup"><span data-stu-id="01d52-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="01d52-122">Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="01d52-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="01d52-123">Panneau de réinitialisation de mot de passe Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01d52-123">hello password reset blade is displayed.</span></span> 

![Réinitialiser la configuration RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="01d52-125">Sélectionnez **uniquement à la configuration de réinitialisation** à partir du menu déroulant de hello, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="01d52-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="01d52-126">Réessayez de vous connecter tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="01d52-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="01d52-127">Extension VMAccess et PowerShell</span><span class="sxs-lookup"><span data-stu-id="01d52-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="01d52-128">Assurez-vous que vous avez hello [dernier module PowerShell installé et configuré](/powershell/azure/overview) et n’êtes pas connecté tooyour abonnement Azure avec hello `Login-AzureRmAccount` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="01d52-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="01d52-129">**Réinitialiser le mot de passe administrateur local hello**</span><span class="sxs-lookup"><span data-stu-id="01d52-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="01d52-130">Réinitialisation hello administrateur mot de passe nom d’utilisateur ou par hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01d52-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="01d52-131">Créez vos informations d’identification de compte comme suit :</span><span class="sxs-lookup"><span data-stu-id="01d52-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="01d52-132">Si vous tapez un nom différent de compte d’administrateur local hello en cours sur votre machine virtuelle, hello extension VMAccess renomme le compte d’administrateur local hello affecte votre compte toothat de mot de passe spécifié et génère un événement de fermeture de session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="01d52-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="01d52-133">Si le compte d’administrateur local hello sur votre machine virtuelle est désactivée, hello extension VMAccess active.</span><span class="sxs-lookup"><span data-stu-id="01d52-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="01d52-134">Hello après les mises à jour de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup` informations d’identification toohello spécifiées.</span><span class="sxs-lookup"><span data-stu-id="01d52-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="01d52-135">**Réinitialiser la configuration du service Bureau à distance hello**</span><span class="sxs-lookup"><span data-stu-id="01d52-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="01d52-136">Réinitialiser l’accès à distance tooyour machine virtuelle avec hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01d52-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="01d52-137">Hello exemple suivant réinitialise extension d’accès hello nommée `myVMAccess` sur hello ordinateur virtuel nommé `myVM` Bonjour `myResourceGroup` groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="01d52-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="01d52-138">En toutes circonstances, une machine virtuelle ne peut avoir qu’un seul agent d’accès de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="01d52-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="01d52-139">propriétés de l’agent tooset hello VM accès hello avec succès, `-ForceRerun` option peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="01d52-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="01d52-140">Lorsque vous utilisez `-ForceRerun`, assurez-vous que toouse hello le même nom pour l’agent d’accès de machine virtuelle hello qu’utilisé dans toutes les commandes précédentes.</span><span class="sxs-lookup"><span data-stu-id="01d52-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="01d52-141">Si vous toujours pas vous connecter à distance tooyour virtual machine, consultez plus tootry étapes au [résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure machine virtuelle](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01d52-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="01d52-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01d52-142">Next steps</span></span>
<span data-ttu-id="01d52-143">Si hello extension d’accès Azure VM ne répond pas et que vous êtes un mot de passe ne peut pas tooreset hello, vous pouvez [réinitialisation hello Windows mot de passe local en mode hors connexion](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01d52-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="01d52-144">Cette méthode est un processus plus avancé et requiert que vous tooconnect hello du disque dur virtuel hello problématique VM tooanother machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="01d52-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="01d52-145">Suivez les étapes de hello documentés en premier dans cet article et tente uniquement la méthode de réinitialisation hello mot de passe en mode hors connexion en dernier recours.</span><span class="sxs-lookup"><span data-stu-id="01d52-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="01d52-146">Extensions et fonctionnalités des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="01d52-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="01d52-147">Se connecter tooan machine virtuelle Azure avec RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="01d52-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="01d52-148">Résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="01d52-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

