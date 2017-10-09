---
title: aaaInstall Trend Micro Deep Security sur une machine virtuelle | Documents Microsoft
description: "Cet article décrit comment tooinstall et configurer Trend Micro security sur un ordinateur virtuel créé avec le modèle de déploiement classique hello dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur une machine virtuelle Windows
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Cet article vous montre comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur un nouveau ou existant ordinateur virtuel (VM) exécutant Windows Server. Deep Security inclut une protection anti-programmes malveillants, un pare-feu, un système de prévention contre les intrusions et une surveillance de l’intégrité.

client de Hello est installé comme une extension de sécurité via hello Agent de machine virtuelle. Sur une machine virtuelle, vous installez hello Deep Security Agent, en tant que hello Qu'agent de machine virtuelle est automatiquement créé par hello portail Azure.

Une machine virtuelle existante, créée à l’aide du portail classique de hello, hello CLI d’Azure ou PowerShell n’est peut-être pas un agent de machine virtuelle. Pour un ordinateur virtuel existant qui n’a pas hello Agent de machine virtuelle, vous devez toodownload et installez en premier. Cet article aborde ces deux situations.

Si vous avez un abonnement en cours à partir de Trend Micro pour une solution sur site, vous pouvez l’utiliser toohelp protéger vos machines virtuelles Azure. Si vous n’êtes pas encore client, vous pouvez vous inscrire pour une version d’évaluation. Pour plus d’informations sur cette solution, consultez hello Trend Micro blog [Microsoft Azure VM Extension pour approfondie sécurité de l’Agent](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Installer hello Deep Security Agent sur un nouvel ordinateur virtuel

Hello [portail Azure](http://portal.azure.com) vous permet d’installer l’extension de sécurité Trend Micro hello lorsque vous utilisez une image à partir de hello **Marketplace** toocreate hello virtual machine. Si vous créez une machine virtuelle unique, à l’aide du portail de hello est une protection de tooadd facilement à partir de Trend Micro.

À l’aide d’une entrée à partir de hello **Marketplace** ouvre un Assistant qui vous permet de configurer la machine virtuelle de hello. Vous utilisez hello **paramètres** panneau, panneau de configuration troisième hello d’Assistant hello, tooinstall hello extension de sécurité Trend Micro.  Pour plus d’informations, consultez [créer une machine virtuelle exécutant Windows Bonjour Azure portal](tutorial.md).

Si vous obtenez les toohello **paramètres** Panneau de l’Assistant de hello, procédez comme hello comme suit :

1. Cliquez sur **Extensions**, puis cliquez sur **ajouter une extension** dans le volet suivant de hello.

   ![Démarrer l’ajout de l’extension de hello][1]

2. Sélectionnez **Deep Security Agent** Bonjour **nouvelle ressource** volet. Dans le volet de Deep Security Agent hello, cliquez sur **créer**.

   ![Identifier le Deep Security Agent][2]

3. Entrez hello **identificateur du locataire** et **mot de passe d’Activation client** pour l’extension de hello. Vous pouvez également entrer un **identificateur de stratégie de sécurité**. Ensuite, cliquez sur **OK** client de hello tooadd.

   ![Fournir les détails de l’extension][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Installer hello Deep Security Agent sur un ordinateur virtuel existant
tooinstall hello l’agent sur un ordinateur virtuel existant, vous devez hello éléments suivants :

* module d’Azure PowerShell Hello, version 0.8.2 ou plus récente, installée sur votre ordinateur local. Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installés à l’aide de hello **azure de Get-Module | version de format-table** commande. Pour obtenir des instructions et une version plus récente de lien toohello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Ouvrez une session à l’aide d’abonnement Azure tooyour `Add-AzureAccount`.
* Hello Agent de machine virtuelle installé sur la machine virtuelle cible hello.

Tout d’abord, vérifiez que hello Qu'agent de machine virtuelle est déjà installé. Renseignez nom du service cloud hello et nom de machine virtuelle et exécutez hello suivant de commandes à partir d’une invite de commandes de niveau administrateur Azure PowerShell. Remplacez tout le contenu du devis hello, y compris hello < et >.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Si vous ne connaissez pas le service cloud hello et nom d’ordinateur virtuel, exécutez **Get-AzureVM** toodisplay que les informations pour tous les hello des machines virtuelles dans votre abonnement actuel.

Si hello **écriture-host** commande **True**, hello l’Agent VM est installé. Si elle retourne **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour billet de blog Azure [Agent de machine virtuelle et Extensions - partie 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Si hello Agent de machine virtuelle est installé, exécutez ces commandes.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Étapes suivantes
Il prend quelques minutes pour hello toostart de l’agent en cours d’exécution lorsqu’il est installé. Après cela, vous devez tooactivate Deep Security sur l’ordinateur virtuel de hello afin qu’il puisse être gérée par un gestionnaire de sécurité approfondie. Hello suivant des articles pour en savoir plus, consultez :

* L’article de Trend sur cette solution, [Sécurité cloud instantanée pour Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [exemple de script Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine
* [Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) pour l’exemple hello

## <a name="additional-resources"></a>Ressources supplémentaires
[Comment toolog sur l’ordinateur virtuel de tooa exécutant Windows Server]

[Fonctionnalités et extensions de machine virtuelle Azure]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Comment toolog sur l’ordinateur virtuel de tooa exécutant Windows Server]:connect-logon.md
[Fonctionnalités et extensions de machine virtuelle Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
