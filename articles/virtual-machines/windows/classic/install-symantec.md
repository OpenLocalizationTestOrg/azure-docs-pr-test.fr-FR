---
title: aaaInstall Symantec Endpoint Protection sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment tooinstall et configurer l’extension de sécurité hello Symantec Endpoint Protection sur un nouveau ou machine virtuelle Azure existante créée avec le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Comment tooinstall et configurer Symantec Endpoint Protection sur une machine virtuelle Windows
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Cet article vous montre comment tooinstall et configurer le client de Symantec Endpoint Protection hello sur un ordinateur virtuel existant (VM) exécutant Windows Server. Le client complet inclut des services tels qu’une protection antivirus et anti-programmes espions, un pare-feu et une prévention contre les intrusions. client de Hello est installé comme une extension de sécurité à l’aide de hello Agent de machine virtuelle.

Si vous avez un abonnement auprès de Symantec pour une solution sur site, vous pouvez l’utiliser tooprotect vos machines virtuelles Azure. Si vous n’êtes pas encore client, vous pouvez vous inscrire pour une version d’évaluation. Pour plus d’informations sur cette solution, consultez la rubrique [Symantec Endpoint Protection sur la plateforme Azure de Microsoft][Symantec]. Cette page contient également des informations de toolicensing de liens et des instructions pour l’installation de client de hello si vous êtes déjà un client de Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Installation de Symantec Endpoint Protection sur une machine virtuelle existante
Avant de commencer, vous devez suivant de hello :

* module d’Azure PowerShell Hello, version 0.8.2 ou version ultérieure, sur votre ordinateur de travail. Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installés avec hello **azure de Get-Module | version de format-table** commande. Pour obtenir des instructions et une version plus récente de lien toohello, consultez [comment tooInstall et configurer Azure PowerShell][PS]. Ouvrez une session à l’aide d’abonnement Azure tooyour `Add-AzureAccount`.
* Hello Agent de machine virtuelle en cours d’exécution hello Machine virtuelle Azure.

Tout d’abord, vérifiez que hello Qu'agent de machine virtuelle est déjà installé sur l’ordinateur virtuel de hello. Renseignez nom du service cloud hello et nom de machine virtuelle et exécutez hello suivant de commandes à partir d’une invite de commandes de niveau administrateur Azure PowerShell. Remplacez tout le contenu du devis hello, y compris hello < et >.

> [!TIP]
> Si vous ne connaissez pas le service cloud hello et les noms des ordinateurs virtuels, exécutez **Get-AzureVM** noms de hello toolist pour tous les ordinateurs virtuels dans votre abonnement actuel.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Si hello **écriture-host** commande affiche **True**, hello l’Agent VM est installé. S’il affiche **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour billet de blog Azure [Agent de machine virtuelle et Extensions - partie 2][Agent].

Si hello Agent de machine virtuelle est installé, exécutez ces agent Symantec Endpoint Protection de commandes tooinstall hello.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify qui hello d’extension de sécurité Symantec a été installé et est à jour :

1. Ouvrez une session sur l’ordinateur virtuel de toohello. Pour obtenir des instructions, consultez [comment tooLog sur tooa Machine virtuelle exécutant Windows Server][Logon].
2. Pour Windows Server 2008 R2, cliquez sur **Démarrer > Symantec Endpoint Protection**. Pour Windows Server 2012 ou Windows Server 2012 R2, à partir de l’écran d’accueil hello, tapez **Symantec**, puis cliquez sur **Symantec Endpoint Protection**.
3. À partir de hello **état** onglet Hello **état-Symantec Endpoint Protection** fenêtre, appliquer des mises à jour ou redémarrer si nécessaire.

## <a name="additional-resources"></a>Ressources supplémentaires
[Comment tooLog sur tooa Machine virtuelle exécutant Windows Server][Logon]

[Fonctionnalités et extensions de machine virtuelle Azure][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
