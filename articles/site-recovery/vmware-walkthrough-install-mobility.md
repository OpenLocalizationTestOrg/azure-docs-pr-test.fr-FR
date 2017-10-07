---
title: "aaaInstall hello service mobilité pour la réplication VMware tooAzure | Documents Microsoft"
description: "Cet article décrit comment tooinstall hello agent du service mobilité pour la réplication tooAzure VMware avec le service d’Azure Site Recovery hello."
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Étape 10 : Installer le service de mobilité hello


Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels VMware, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Hello service mobilité capture les écritures de données sur un ordinateur et les transfère de serveur de processus toohello. Il doit être installé sur chaque ordinateur que vous souhaitez tooreplicate tooAzure.

Vous pouvez installer manuel de service de mobilité hello, à l’aide d’une installation push du serveur de processus de récupération de Site hello lorsque la réplication est activée, ou utiliser un outil de System Center Configuration Manager. Si vous utilisez installation push, service de hello est installé sur hello machine virtuelle lorsque la réplication est activée.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Installer manuellement

1. Vérifiez hello [conditions préalables](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) pour l’installation manuelle.
2. Suivez [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) pour l’installation manuelle à l’aide du portail de hello.
3. Si vous préférez tooinstall à partir de la ligne de commande hello, procédez comme [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Installer hello serveur de processus

Installation du service mobilité toopush hello hello du serveur de processus lorsque vous activez la réplication pour une machine virtuelle, vous devez un compte qui peut être utilisé par hello processus serveur tooaccess hello machine virtuelle. Hello compte est uniquement utilisé pour l’installation push de hello.

1. Vous devriez avoir [créé un compte](vmware-walkthrough-prepare-vmware.md) qui peut être utilisé pour l’installation push. Puis, vous spécifiez hello compte toouse lorsque vous configurez des paramètres de la source pendant le déploiement de Site Recovery.
2. Suivez ensuite [ces instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) si vous souhaitez que le service de mobilité hello toopush sur des machines virtuelles exécutant Windows ou Linux.

## <a name="other-methods"></a>Autres méthodes

En savoir plus sur [installation à l’aide du Gestionnaire de Configuration du service mobilité hello](site-recovery-install-mobility-service-using-sccm.md), ou à l’aide de [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)
