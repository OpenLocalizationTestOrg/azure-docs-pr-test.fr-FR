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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Comment tooreset hello service Bureau à distance ou son mot de passe de connexion dans une machine virtuelle Windows
Si vous ne pouvez pas vous connecter tooa Windows virtual machine (VM), vous pouvez réinitialiser le mot de passe administrateur local hello ou réinitialiser la configuration du service Bureau à distance hello. Vous pouvez utiliser l’extension d’accès de la machine virtuelle Azure portal ou hello hello dans mot de passe Azure PowerShell tooreset hello. Si vous utilisez PowerShell, assurez-vous que vous avez hello [dernier module PowerShell installé et configuré](/powershell/azure/overview) et vous n’êtes pas connecté tooyour abonnement Azure. Vous pouvez également [effectuer ces étapes pour les machines virtuelles créées avec le modèle de déploiement classique hello](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuration de tooreset de méthodes ou les informations d’identification
Vous pouvez réinitialiser les services Bureau à distance et les informations d’identification de différentes manières, selon vos besoins :

- [Réinitialiser à l’aide de hello portail Azure](#azure-portal)
- [Réinitialisation à l’aide d’Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portail Azure
tooexpand hello menus, barres hello trois dans le coin supérieur gauche de hello, puis cliquez sur **virtuels**:

![Accédez à votre machine virtuelle Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Réinitialiser le mot de passe administrateur local hello**

Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**. Panneau de réinitialisation de mot de passe Hello s’affiche :

![Page Réinitialiser le mot de passe](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Entrez le nom d’utilisateur hello et un nouveau mot de passe, puis cliquez sur **mise à jour**. Réessayez de vous connecter tooyour machine virtuelle.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Réinitialiser la configuration du service Bureau à distance hello**

Sélectionnez votre machine virtuelle Windows, puis cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**. Panneau de réinitialisation de mot de passe Hello s’affiche. 

![Réinitialiser la configuration RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Sélectionnez **uniquement à la configuration de réinitialisation** à partir du menu déroulant de hello, puis cliquez sur **mise à jour**. Réessayez de vous connecter tooyour machine virtuelle.


## <a name="vmaccess-extension-and-powershell"></a>Extension VMAccess et PowerShell
Assurez-vous que vous avez hello [dernier module PowerShell installé et configuré](/powershell/azure/overview) et n’êtes pas connecté tooyour abonnement Azure avec hello `Login-AzureRmAccount` applet de commande.

### <a name="reset-hello-local-administrator-account-password"></a>**Réinitialiser le mot de passe administrateur local hello**
Réinitialisation hello administrateur mot de passe nom d’utilisateur ou par hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) applet de commande PowerShell. Créez vos informations d’identification de compte comme suit :

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Si vous tapez un nom différent de compte d’administrateur local hello en cours sur votre machine virtuelle, hello extension VMAccess renomme le compte d’administrateur local hello affecte votre compte toothat de mot de passe spécifié et génère un événement de fermeture de session Bureau à distance. Si le compte d’administrateur local hello sur votre machine virtuelle est désactivée, hello extension VMAccess active.

Hello après les mises à jour de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup` informations d’identification toohello spécifiées.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Réinitialiser la configuration du service Bureau à distance hello**
Réinitialiser l’accès à distance tooyour machine virtuelle avec hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) applet de commande PowerShell. Hello exemple suivant réinitialise extension d’accès hello nommée `myVMAccess` sur hello ordinateur virtuel nommé `myVM` Bonjour `myResourceGroup` groupe de ressources :

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> En toutes circonstances, une machine virtuelle ne peut avoir qu’un seul agent d’accès de machine virtuelle. propriétés de l’agent tooset hello VM accès hello avec succès, `-ForceRerun` option peut être utilisée. Lorsque vous utilisez `-ForceRerun`, assurez-vous que toouse hello le même nom pour l’agent d’accès de machine virtuelle hello qu’utilisé dans toutes les commandes précédentes.

Si vous toujours pas vous connecter à distance tooyour virtual machine, consultez plus tootry étapes au [résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure machine virtuelle](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Étapes suivantes
Si hello extension d’accès Azure VM ne répond pas et que vous êtes un mot de passe ne peut pas tooreset hello, vous pouvez [réinitialisation hello Windows mot de passe local en mode hors connexion](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cette méthode est un processus plus avancé et requiert que vous tooconnect hello du disque dur virtuel hello problématique VM tooanother machine virtuelle. Suivez les étapes de hello documentés en premier dans cet article et tente uniquement la méthode de réinitialisation hello mot de passe en mode hors connexion en dernier recours.

[Extensions et fonctionnalités des machines virtuelles Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Se connecter tooan machine virtuelle Azure avec RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

