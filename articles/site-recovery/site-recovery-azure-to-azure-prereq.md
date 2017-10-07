---
title: "aaaPrerequisites pour tooAzure de réplication à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article résume les conditions préalables pour la réplication des machines virtuelles et des machines physiques tooAzure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Configuration requise pour la réplication des machines virtuelles tooanother région à l’aide d’Azure Site Recovery

> [!div class="op_single_selector"]
> * [Répliquer à partir d’Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Répliquer à partir de local tooAzure](site-recovery-prereq.md)

Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence en coordonnant la :
* Réplication des machines virtuelles tooanother région Azure.
* Réplication de local serveurs et les ordinateurs virtuels tooAzure ou tooa secondaire centre de données physique. 

En cas de pannes dans votre emplacement principal, vous pouvez basculer tooa emplacement secondaire tookeep applications et charges de travail disponibles. Vous pouvez échouer emplacement principal d’arrière tooyour lorsqu’elle retourne les opérations de toonormal. Pour plus d’informations sur Site Recovery, voir [Qu’est-ce que Site Recovery ?](site-recovery-overview.md).

Cet article résume les hello conditions préalables toobegin requis réplication de récupération de Site à partir de local tooAzure.

Validez les commentaires en bas de hello d’article de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Conditions requises pour Azure

**Prérequis** | **Détails**
--- | ---
**Compte Azure** | Un compte [Microsoft Azure](http://azure.microsoft.com/) .<br/><br/> Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
**Service Site Recovery** | Pour plus d’informations sur la tarification de Site Recovery, voir [Tarification Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). Nous vous recommandons de créer un coffre de Services de récupération dans la cible de hello région Azure que vous souhaitez toouse comme un emplacement de récupération d’urgence. Par exemple, si votre source de machines virtuelles sont en cours d’exécution dans l’est des États-Unis, et que vous souhaitez tooreplicate tooCentral, nous recommandons de créer hello coffre dans le centre des États-Unis.|
**Capacité Azure** | Pour la cible de hello région Azure que vous souhaitez toouse comme emplacement de récupération d’urgence, vous devez toohave un abonnement avec une capacité suffisante pour les ordinateurs virtuels, les comptes de stockage et les composants réseau. Vous pouvez contacter tooadd prise en charge plus de capacité.
**Conseils de stockage** | Vérifiez que vous suivez hello [conseils de stockage](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) pour votre source Azure virtual machines tooavoid les problèmes de performances. Si vous suivez les paramètres par défaut de hello, Site Recovery crée les comptes de stockage hello requis en fonction de la configuration de la source hello. Si vous personnalisez et sélectionnez vos paramètres, veillez à suivre les hello [objectifs d’évolutivité pour les disques de machine virtuelle](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Conseils de mise en réseau** | Vous devez connectivité sortante de hello toowhitelist à partir de votre machine virtuelle Azure pour les plages d’adresses URL ou une adresse IP spécifique. Pour plus d’informations, consultez toohello [mise en réseau des conseils pour la réplication des machines virtuelles](site-recovery-azure-to-azure-networking-guidance.md) l’article.
**Microsoft Azure** | Assurez-vous que tous les certificats racine de la dernière hello sont présents sur hello Windows ou Linux VM. Si les certificats racine dernières hello ne sont pas présents, hello machine virtuelle ne peut pas être inscrit tooSite récupération en raison de contraintes de toosecurity.

>[!NOTE]
>Pour plus d’informations sur la prise en charge pour des configurations spécifiques, consultez hello [matrice de prise en charge](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Étapes suivantes
- Découvrir l’[Aide à la mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).
- Commencer à protéger vos charges de travail en [répliquant des machines virtuelles Azure](site-recovery-azure-to-azure.md).
