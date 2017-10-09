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
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Installer le Service mobilité (VMware ou tooAzure physique)
Le Service Azure Site Recovery mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello. Déployer Service mobilité tooevery ordinateur (VMware VM ou serveur physique) que vous souhaitez tooreplicate tooAzure. Vous pouvez déployer le Service mobilité toohello serveurs que tooprotect à l’aide des méthodes suivantes de hello :


* [Installation du service Mobilité à l’aide d’outils de déploiement de logiciels tels que System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Installation du Service Mobilité à l’aide d’Azure Automation et de la Configuration de l’état souhaité (Automation DSC)](site-recovery-automate-mobility-service-install.md)
* [Installer le Service mobilité manuellement en utilisant l’interface utilisateur graphique de hello (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Installation manuelle du service Mobilité à l’aide d’une ligne de commande](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Depuis la version 9.7.0.0, sur les machines virtuelles (VM), Windows installer du Service mobilité hello installe également hello dernière version disponible [agent Azure VM](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Lorsqu’un ordinateur bascule tooAzure, ordinateur de hello satisfait hello agent requis pour l’installation à l’aide de n’importe quelle extension de machine virtuelle.

## <a name="prerequisites"></a>Composants requis
Effectuez ces étapes préalables avant d’installer manuellement le service Mobilité sur votre serveur :
1. Connectez-vous au serveur de configuration tooyour, puis ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
2. Modifier le dossier bin de hello répertoire toohello, puis créer un fichier de mot de passe :

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Stockez le fichier de mot de passe de hello dans un emplacement sécurisé. Vous utilisez des fichiers de hello pendant hello installation du Service mobilité.
4. Programmes d’installation du Service mobilité pour tous les systèmes d’exploitation pris en charge se trouvent dans le dossier de %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Correspondance entre le programme d’installation du service Mobilité et le système d’exploitation

| Nom du modèle de fichier de programme d’installation| Système d’exploitation |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 bits) </br> Windows Server 2012 (64 bits) </br> Windows Server 2012 R2 (64 bits) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64 bits uniquement) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64 bits uniquement) </br> CentOS 7.0, 7.1, 7.2 (64 bits uniquement)</br> CentOs 7.3 (migration uniquement) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (64 bits uniquement)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (64 bits uniquement)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (64 bits uniquement)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (64 bits uniquement)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Installer le Service mobilité manuellement à l’aide de l’interface graphique utilisateur hello

>[!IMPORTANT]
> Si vous utilisez un **serveur de Configuration** tooreplicate **machines virtuelles Azure IaaS** à partir d’un tooanother abonnement Azure ou la région puis **utiliser hello d’installation en fonction de ligne de commande**  (méthode)

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Installation manuelle du service Mobilité à l’aide d’une ligne de commande

### <a name="command-line-installation-on-a-windows-computer"></a>Installation avec une ligne de commande sur un ordinateur Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Installation avec une ligne de commande sur un ordinateur Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Installation du service Mobilité à l’aide de l’installation de transmission (push) à partir d’Azure Site Recovery
toodo une installation push du Service mobilité à l’aide de récupération de Site, tous les ordinateurs cibles doivent respecter hello suivant des conditions préalables.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Après l’installation du Service mobilité, Bonjour portail Azure, sélectionnez hello **répliquer** toostart bouton protéger ces ordinateurs virtuels.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Désinstallation d’un service Mobilité sur un ordinateur Windows Server
Utilisez une des hello suivant les méthodes toouninstall Service mobilité sur un ordinateur Windows Server.

### <a name="uninstall-by-using-hello-gui"></a>Désinstaller à l’aide de l’interface graphique utilisateur hello
1. Dans le panneau de configuration, sélectionnez **Programmes**.
2. Sélectionnez **Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery**, puis sélectionnez **Désinstaller**.

### <a name="uninstall-at-a-command-prompt"></a>Désinstallation avec une invite de commandes
1. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
2. toouninstall Service mobilité, exécutez hello de commande suivante :

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Désinstaller le service Mobilité sur un ordinateur Linux
1. Sur votre serveur Linux, connectez-vous en tant qu’utilisateur **root**.
2. Dans un terminal, accédez trop/utilisateur/local/récupération automatique du système.
3. toouninstall Service mobilité, exécutez hello de commande suivante :

```
uninstall.sh -Y
```
