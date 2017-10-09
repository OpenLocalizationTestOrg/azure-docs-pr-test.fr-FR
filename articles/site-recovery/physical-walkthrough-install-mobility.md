---
title: "aaaInstall hello service mobilité pour la réplication de serveur physique tooAzure | Documents Microsoft"
description: "Cet article décrit comment tooinstall hello agent du service mobilité sur les serveurs physiques réplication tooAzure avec le service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Étape 9 : Installer le service de mobilité hello


Cet article décrit comment composant de service de mobilité tooinstall hello lors de la réplication locale tooAzure de serveurs physiques Windows/Linux, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Hello service mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello. Il doit être installé sur chaque serveur que vous souhaitez tooreplicate tooAzure.

Vous pouvez installer le service de mobilité hello manuellement ou à l’aide d’une installation push de hello Site Recovery traiter serveur lors de la réplication est activée, ou à l’aide d’un outil tel que System Center Configuration Manager. Si vous utilisez installation push, service de hello est installé sur le serveur de hello lorsque vous activez la réplication.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Installer manuellement

1. Vérifiez hello [conditions préalables](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.
2. Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail de hello.
3. Si vous préférez tooinstall à partir de la ligne de commande hello, procédez comme [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installer hello serveur de processus

Si vous souhaitez toopush hello installation du service mobilité hello du serveur de processus lorsque vous activez la réplication pour un ordinateur, vous avez besoin d’un compte peut être utilisé par hello processus tooaccess hello du serveur. Hello compte est uniquement utilisé pour l’installation push de hello.

1. Si vous n’avez pas créé de compte, faites-le à l’aide de ces instructions :

    - Vous pouvez utiliser un compte local ou de domaine
    - Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo, Bonjour Enregistrer sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajouter l’entrée DWORD de hello **LocalAccountTokenFilterPolicy**, avec la valeur 1.
    - Si vous souhaitez l’entrée de Registre tooadd hello pour Windows à partir d’une interface CLI, tapez :

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Pour Linux, hello doit être racine sur le serveur de Linux hello source.

2. Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez que le service de mobilité hello toopush sur des machines virtuelles exécutant Windows ou Linux.

## <a name="other-installation-methods"></a>Autres méthodes d’installation

- [En savoir plus sur](site-recovery-install-mobility-service-using-sccm.md) installation à l’aide du Gestionnaire de Configuration du service mobilité hello
- [En savoir plus sur](site-recovery-automate-mobility-service-install.md) l’installation avec Azure Automation DSC.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 10 : activer la réplication](physical-walkthrough-enable-replication.md)
