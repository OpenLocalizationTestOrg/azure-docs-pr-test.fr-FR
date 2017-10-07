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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Comment le service Bureau à distance de hello tooreset ou son mot de passe de connexion dans une machine virtuelle Windows créé à l’aide du modèle de déploiement classique de hello
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Vous pouvez également [effectuer ces étapes pour les machines virtuelles créées avec le modèle de déploiement du Gestionnaire de ressources hello](../reset-rdp.md).

Si vous ne pouvez pas vous connecter tooa Windows virtual machine (VM), vous pouvez réinitialiser le mot de passe administrateur local hello ou réinitialiser la configuration du service Bureau à distance hello. Vous pouvez utiliser l’extension d’accès de la machine virtuelle Azure portal ou hello hello dans mot de passe Azure PowerShell tooreset hello.

## <a name="ways-tooreset-configuration-or-credentials"></a>Configuration de tooreset de méthodes ou les informations d’identification
Vous pouvez réinitialiser les services Bureau à distance et les informations d’identification de différentes manières, selon vos besoins :

- [Réinitialiser à l’aide de hello portail Azure](#azure-portal)
- [Réinitialisation à l’aide d’Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portail Azure
Vous pouvez utiliser hello [portail Azure](https://portal.azure.com) tooreset hello service Bureau à distance. tooexpand hello menus, barres hello trois dans le coin supérieur gauche de hello, puis cliquez sur **machines virtuelles (classiques)**:

![Accédez à votre machine virtuelle Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

Sélectionnez votre machine virtuelle de Windows, puis cliquez **réinitialiser à distance...** . configuration de bureau à distance tooreset hello apparaît hello boîte de dialogue suivante :

![Page Réinitialiser la configuration RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Vous pouvez également réinitialiser le nom d’utilisateur hello et le mot de passe du compte d’administrateur local hello. À partir de votre machine virtuelle, cliquez sur **Support + dépannage** > **Réinitialiser le mot de passe**. Panneau de réinitialisation de mot de passe Hello s’affiche :

![Page Réinitialiser le mot de passe](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Après avoir entré le nouveau nom d’utilisateur hello et le mot de passe, cliquez sur **enregistrer**.

## <a name="vmaccess-extension-and-powershell"></a>Extension VMAccess et PowerShell
Vérifiez que hello que l’Agent VM est installé sur l’ordinateur virtuel de hello. Hello extension VMAccess n’a pas besoin de toobe installé avant de pouvoir l’utiliser, tant que hello Agent de machine virtuelle est disponible. Vérifiez que hello Qu'agent de machine virtuelle est déjà installée en utilisant hello commande suivante. (Remplacez « myCloudService » et « myVM » par les noms hello de votre service cloud et votre machine virtuelle, respectivement. Pour obtenir ces noms, exécutez `Get-AzureVM` sans paramètre.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Si hello **écriture-host** commande affiche **True**, hello l’Agent VM est installé. S’il affiche **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour [Agent de machine virtuelle et Extensions - partie 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) billet de blog Azure.

Si vous avez créé l’ordinateur virtuel de hello à l’aide du portail de hello, vérifiez si `$vm.GetInstance().ProvisionGuestAgent` retourne **True**. Si ce n’est pas le cas, définissez cette valeur à l’aide de cette commande :

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Cette commande empêche hello l’erreur suivante lorsque vous exécutez hello **Set-AzureVMExtension** dans les étapes suivantes hello : « Disposition invité Agent doit être activé sur l’objet de machine virtuelle hello avant de définir l’Extension d’accès IaaS VM. »

### <a name="reset-hello-local-administrator-account-password"></a>**Réinitialiser le mot de passe administrateur local hello**
Créer une information d’identification de connexion avec le nom du compte administrateur local en cours hello et un nouveau mot de passe, puis exécutez hello `Set-AzureVMAccessExtension` comme suit.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Si vous tapez un nom différent de compte en cours de hello, hello extension VMAccess renomme le compte d’administrateur local hello affecte le compte de toothat de mot de passe hello et émet une déconnexion de bureau à distance. Si le compte d’administrateur local hello est désactivé, hello extension VMAccess active.

Ces commandes de réinitialisent de la configuration du service Bureau à distance hello.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Réinitialiser la configuration du service Bureau à distance hello**
tooreset hello Bureau à distance configuration du service, exécutez hello de commande suivante :

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hello extension VMAccess exécute deux commandes sur l’ordinateur virtuel de hello :

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Cette commande active hello intégré groupe du pare-feu Windows qui autorise le trafic entrant Bureau à distance, qui utilise le port TCP 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Cette commande définit too0 de valeur de Registre fDenyTSConnections hello, l’activation des connexions de bureau à distance.

## <a name="next-steps"></a>Étapes suivantes
Si hello extension d’accès Azure VM ne répond pas et que vous êtes un mot de passe ne peut pas tooreset hello, vous pouvez [réinitialisation hello Windows mot de passe local en mode hors connexion](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cette méthode est un processus plus avancé et requiert que vous tooconnect hello du disque dur virtuel hello problématique VM tooanother machine virtuelle. Suivez les étapes de hello documentés en premier dans cet article et tente uniquement la méthode de réinitialisation hello mot de passe en mode hors connexion en dernier recours.

[Extensions et fonctionnalités des machines virtuelles Azure](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Se connecter tooan machine virtuelle Azure avec RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Résoudre les problèmes de bureau à distance connexions tooa basé sur Windows Azure virtual machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

