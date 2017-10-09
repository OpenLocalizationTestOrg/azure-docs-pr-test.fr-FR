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
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Répliquer des machines virtuelles Azure tooanother région après migration tooAzure à l’aide d’Azure Site Recovery

>[!NOTE]
> La réplication Azure Site Recovery pour les machines virtuelles Azure est actuellement en préversion.

## <a name="overview"></a>Vue d'ensemble

Cet article vous aide à préparer des machines virtuelles pour la réplication entre les deux régions Azure une fois que ces ordinateurs ont été migrés à partir d’un tooAzure d’environnement sur site à l’aide d’Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Récupération d’urgence et conformité
Aujourd'hui, plus des entreprises adoptent leur tooAzure les charges de travail. Avec déplacement de production de site critiques des entreprises tooAzure les charges de travail, configuration de la récupération d’urgence pour ces charges de travail est obligatoire pour la conformité et toosafeguard contre toute interruption dans une région Azure.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Étapes de préparation de machines migrées pour la réplication
tooprepare migré des ordinateurs pour configurer la réplication tooanother région Azure :

1. Achevez la migration.
2. Installez hello Azure agent si nécessaire.
3. Supprimer le service de mobilité hello.  
4. Redémarrez hello machine virtuelle.

Ces étapes sont décrites en détail dans les sections suivantes de hello.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Étape 1 : Migrer les charges de travail en cours d’exécution sur les ordinateurs virtuels Hyper-V, les ordinateurs virtuels VMware et toorun des serveurs physiques sur des machines virtuelles Azure

tooset la réplication et de migrer votre Hyper-V, VMware et tooAzure de charges de travail physiques, suivez hello étapes locale Bonjour [virtuels IaaS de Azure migrer entre les régions Azure avec Azure Site Recovery](site-recovery-migrate-to-azure.md) l’article. 

Après la migration, vous ne devez toocommit ou supprimer un basculement. Au lieu de cela, sélectionnez hello **effectuer la Migration** option pour chaque ordinateur, vous souhaitez toomigrate :
1. Dans **répliquées des éléments**, avec le bouton droit hello machine virtuelle, puis cliquez sur **effectuer la Migration**. Cliquez sur **OK** étape de hello toocomplete. Vous pouvez suivre la progression dans les propriétés de machine virtuelle hello en surveillant le travail de Migration complète hello dans **les tâches de récupération de Site**.
2. Hello **effectuer la Migration** action se termine le processus de migration hello, supprime la réplication pour l’ordinateur de hello et arrête la facturation de récupération de Site pour l’ordinateur de hello.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Étape 2 : Installer l’agent de machine virtuelle Azure hello sur l’ordinateur virtuel de hello
Bonjour Azure [agent de machine virtuelle](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) doit être installé sur l’ordinateur virtuel de hello pour hello Site Recovery extension toowork et toohelp protègent hello machine virtuelle.

>[!IMPORTANT]
>Depuis la version 9.7.0.0, sur les machines virtuelles Windows, programme d’installation de service de mobilité hello installe également hello dernière machine virtuelle Azure agent disponible. Sur la migration hello virtual machine répond à l’installation des agents requise pour l’utilisation de toute extension de machine virtuelle, notamment l’extension de Site Recovery hello. Bonjour Azure VM agent besoins toobe manuellement uniquement installée si hello service mobilité installé sur hello migrés machine est 9,6 ou version antérieure.

Hello tableau suivant fournit des informations supplémentaires sur l’installation d’agent de machine virtuelle hello et de validation qu’il a été installé :

| **opération** | **Windows** | **Linux** |
| --- | --- | --- |
| L’installation d’agent de machine virtuelle hello |Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello. |Installer hello dernières [agent Linux](../virtual-machines/linux/agent-user-guide.md). Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello. Nous vous recommandons d’installer l’agent de hello à partir de votre référentiel de distribution. Nous *ne recommandons pas* l’installation de l’agent Linux VM de hello directement à partir de GitHub.  |
| Valider l’installation de l’agent de machine virtuelle hello |1. Parcourir le dossier de C:\WindowsAzure\Packages toohello Bonjour Azure VM. Vous devez voir fichier WaAppAgent.exe de hello. <br>2. Clic droit sur hello fichier, accédez trop**propriétés**, puis sélectionnez hello **détails** hello d’onglet **Version du produit** champ doit être 2.6.1198.718 ou une version ultérieure. |N/A |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Étape 3 : Suppression hello service mobilité de hello migrés machine virtuelle

Si vous avez migré votre machines de VMware locales ou les serveurs physiques sur Windows/Linux, vous devez toomanually suppression et la désinstallation du service hello mobilité à partir de l’ordinateur virtuel migré de hello.

>[!IMPORTANT]
>Cette étape n’est pas nécessaire pour tooAzure migré des ordinateurs virtuels Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Désinstaller le service de mobilité hello sur un ordinateur Windows Server
Utilisez une des hello suivant du service de mobilité de méthodes toouninstall hello sur un ordinateur Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Désinstaller à l’aide de l’interface utilisateur Windows de hello
1. Dans le panneau de configuration de hello, sélectionnez **programmes**.
2. Sélectionnez **Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery**, puis sélectionnez **Désinstaller**.

##### <a name="uninstall-at-a-command-prompt"></a>Désinstallation avec une invite de commandes
1. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
2. service de mobilité hello toouninstall, exécutez hello de commande suivante :

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Désinstaller le service de mobilité hello sur un ordinateur Linux
1. Sur votre serveur Linux, connectez-vous en tant qu’utilisateur **root**.
2. Dans un terminal, accédez trop/utilisateur/local/récupération automatique du système.
3. service de mobilité hello toouninstall, exécutez hello de commande suivante :

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Étape 4 : Redémarrer hello machine virtuelle

Après avoir désinstallé le service de mobilité hello, hello redémarrage machine virtuelle avant de configurer de réplication tooanother région Azure.


## <a name="next-steps"></a>Étapes suivantes
- Commencer à protéger vos charges de travail en [répliquant des machines virtuelles Azure](site-recovery-azure-to-azure.md).
- Découvrir l’[Aide à la mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).
