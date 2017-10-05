---
title: "Réinitialisation du mot de passe ou de la configuration Bureau à distance sur une machine virtuelle Windows | Microsoft Docs"
description: "Découvrez comment réinitialiser un mot de passe de compte ou des services Bureau à distance sur une machine virtuelle Windows à l’aide du Portail Azure ou d’Azure PowerShell."
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
ms.openlocfilehash: 2e002e3f336422b8fa1eceece889cd083e355a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="dfb03-103">Comment réinitialiser le service Bureau à distance ou son mot de passe de connexion dans une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="dfb03-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="dfb03-104">Si vous ne pouvez pas vous connecter à une machine virtuelle Windows, vous pouvez réinitialiser le mot de passe d’administrateur local ou la configuration du service Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="dfb03-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="dfb03-105">Vous pouvez utiliser le portail Azure ou l’extension d’accès aux machines virtuelles dans Azure PowerShell pour réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dfb03-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="dfb03-106">Si vous utilisez PowerShell, assurez-vous d’avoir le [dernier module PowerShell installé et configuré](/powershell/azure/overview)et d’être connecté à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb03-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="dfb03-107">Vous pouvez également [effectuer ces étapes pour les machines virtuelles créées à l’aide du modèle de déploiement classique](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="dfb03-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="dfb03-108">Comment réinitialiser la configuration ou les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="dfb03-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="dfb03-109">Vous pouvez réinitialiser les services Bureau à distance et les informations d’identification de différentes manières, selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="dfb03-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="dfb03-110">Réinitialisation à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="dfb03-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="dfb03-111">Réinitialisation à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfb03-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="dfb03-112">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dfb03-112">Azure portal</span></span>
<span data-ttu-id="dfb03-113">Pour développer le menu du portail, cliquez sur les trois barres dans l’angle supérieur gauche, puis sur **Machines virtuelles** :</span><span class="sxs-lookup"><span data-stu-id="dfb03-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Accédez à votre machine virtuelle Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="dfb03-115">**Réinitialiser le mot de passe de compte d’administrateur local**</span><span class="sxs-lookup"><span data-stu-id="dfb03-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="dfb03-116">Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dfb03-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="dfb03-117">Le panneau de réinitialisation du mot de passe s’affiche :</span><span class="sxs-lookup"><span data-stu-id="dfb03-117">The password reset blade is displayed:</span></span>

![Page Réinitialiser le mot de passe](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="dfb03-119">Entrez le nom d’utilisateur et un nouveau mot de passe, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="dfb03-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="dfb03-120">Essayez à nouveau de vous connecter à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfb03-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="dfb03-121">**Réinitialiser la configuration du service Bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="dfb03-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="dfb03-122">Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dfb03-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="dfb03-123">Le panneau de réinitialisation du mot de passe s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dfb03-123">The password reset blade is displayed.</span></span> 

![Réinitialiser la configuration RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="dfb03-125">Sélectionnez **Réinitialiser la configuration uniquement** dans le menu déroulant, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="dfb03-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="dfb03-126">Essayez à nouveau de vous connecter à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfb03-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="dfb03-127">Extension VMAccess et PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfb03-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="dfb03-128">Assurez-vous d’avoir le [dernier module PowerShell installé et configuré](/powershell/azure/overview)et d’être connecté à votre abonnement Azure à l’aide de l’applet de commande `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="dfb03-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="dfb03-129">**Réinitialiser le mot de passe de compte d’administrateur local**</span><span class="sxs-lookup"><span data-stu-id="dfb03-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="dfb03-130">Réinitialisez le mot de passe ou le nom d’utilisateur de l’administrateur à l’aide de l’applet de commande PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="dfb03-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="dfb03-131">Créez vos informations d’identification de compte comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfb03-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="dfb03-132">Si vous tapez un nom différent de celui du compte de l’administrateur local actuel sur votre machine virtuelle, l’extension VMAccess renomme le compte d’administrateur local, affecte le mot de passe à ce compte et envoie une commande de fermeture de la session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="dfb03-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="dfb03-133">Si le compte d’administrateur local sur votre machine virtuelle est désactivé, l’extension VMAccess l’active.</span><span class="sxs-lookup"><span data-stu-id="dfb03-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="dfb03-134">L’exemple suivant met à jour la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`, sur les informations d’identification spécifiées.</span><span class="sxs-lookup"><span data-stu-id="dfb03-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="dfb03-135">**Réinitialiser la configuration du service Bureau à distance**</span><span class="sxs-lookup"><span data-stu-id="dfb03-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="dfb03-136">Réinitialisez l’accès à distance à votre machine virtuelle avec l’applet de commande PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="dfb03-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="dfb03-137">L’exemple suivant réinitialise l’extension d’accès nommée `myVMAccess`, sur la machine virtuelle nommée `myVM`, dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="dfb03-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="dfb03-138">En toutes circonstances, une machine virtuelle ne peut avoir qu’un seul agent d’accès de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfb03-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="dfb03-139">Pour pouvoir définir les propriétés de l’agent d’accès à la machine virtuelle, l’option `-ForceRerun` peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="dfb03-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="dfb03-140">Si vous utilisez `-ForceRerun`, assurez-vous d’utiliser le même nom pour l’agent d’accès à la machine virtuelle que celui défini par les commandes précédentes.</span><span class="sxs-lookup"><span data-stu-id="dfb03-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="dfb03-141">Si vous ne pouvez toujours pas vous connecter à distance à votre machine virtuelle, consultez les étapes supplémentaires dans la rubrique [Résolution des problèmes de connexion Bureau à distance avec une machine virtuelle Azure exécutant Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfb03-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="dfb03-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dfb03-142">Next steps</span></span>
<span data-ttu-id="dfb03-143">Si l’extension d’accès aux machines virtuelles Azure ne répond pas et que vous ne pouvez pas réinitialiser le mot de passe, vous pouvez [réinitialiser le mot de passe Windows local en mode hors connexion](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfb03-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dfb03-144">Cette méthode est plus avancée et nécessite que vous connectiez le disque dur virtuel de la machine virtuelle problématique à une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfb03-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="dfb03-145">Suivez d’abord la procédure décrite dans cet article et n’utilisez la méthode de réinitialisation du mot de passe en mode hors connexion qu’en dernier recours.</span><span class="sxs-lookup"><span data-stu-id="dfb03-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="dfb03-146">Extensions et fonctionnalités des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dfb03-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="dfb03-147">Connexion à une machine virtuelle Microsoft Azure avec RDP ou SSH</span><span class="sxs-lookup"><span data-stu-id="dfb03-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="dfb03-148">Résolution des problèmes de connexion Bureau à distance avec une machine virtuelle Azure Windows</span><span class="sxs-lookup"><span data-stu-id="dfb03-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

