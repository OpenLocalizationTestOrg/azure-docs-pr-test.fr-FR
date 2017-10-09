---
title: "aaaPlan la capacité et de mise à l’échelle pour tooAzure de réplication (avec VMM) d’un ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Utiliser cette capacité tooplan de l’article et la mise à l’échelle lors de la réplication des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure, avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Étape 3 : Planifier la capacité et de mise à l’échelle pour la réplication Hyper-V (avec VMM) tooAzure

Une fois que vous avez consulté hello [conditions préalables au déploiement](vmm-to-azure-walkthrough-prerequisites.md), utiliser ce toofigure article hors de la planification de la capacité et la mise à l’échelle lors de la réplication locale des ordinateurs virtuels Hyper-V dans System Center Virtual Machine Manager (VMM) clouds tooAzure, avec [Azure Site Recovery](site-recovery-overview.md).

Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Comment dois-je commencer la planification de la capacité ?


Vous rassemblez des informations sur votre environnement de réplication et la capacité de plan à l’aide de données hello, ainsi que des considérations hello mis en surbrillance dans cet article.


## <a name="gather-information"></a>Collecter des informations

1. collecter les informations relatives à votre environnement de réplication, notamment les machines virtuelles, le nombre de disques par machine virtuelle et le stockage par disque ;
2. Déterminer le taux de modification (l’évolution) quotidienne des données répliquées. Télécharger hello [outil de planification des capacités de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) taux de modification tooget hello. Nous vous recommandons de qu'exécuter cet outil sur un toocapture semaine moyennes.
 

## <a name="figure-out-capacity"></a>Déterminer la capacité

Selon que vous avez collecte d’informations hello, vous exécutez hello [Site Recovery outil Capacity Planner](http://aka.ms/asr-capacity-planner-excel) tooanalyze votre environnement source et les charges de travail, estimer les besoins en bande passante et ressources du serveur pour l’emplacement de source de hello et hello ressources (machines virtuelles et stockage, etc.) dont vous avez besoin dans l’emplacement cible de hello. Vous pouvez exécuter l’outil de hello dans deux modes :

- Planification rapide : exécuter les outil hello dans ce mode tooget réseau et serveur les projections basées sur un nombre moyen de machines virtuelles, de disques, de stockage et de taux de modification.
- Planification détaillée : exécutez l’outil de hello dans ce mode et fournissent des détails de chaque charge de travail au niveau de la machine virtuelle. Analysez la compatibilité de machine virtuelle et obtenez des projections réseau et serveur.

Maintenant, exécutez les outil hello :

1. Télécharger hello [outil](http://aka.ms/asr-capacity-planner-excel)
2. module rapide de toorun hello, procédez comme [ces instructions](site-recovery-capacity-planner.md#run-the-quick-planner)et sélectionnez hello scénario **Hyper-V tooAzure**.
3. toorun hello de planification détaillée, suivez [ces instructions](site-recovery-capacity-planner.md#run-the-detailed-planner)et sélectionnez hello scénario **Hyper-V tooAzure**.

## <a name="control-network-bandwidth"></a>Contrôler la bande passante réseau

Une fois que vous êtes la bande passante calculée hello que vous avez besoin, vous avez deux options pour la quantité de hello contrôle de bande passante utilisée pour la réplication :

* **Limiter la bande passante**: le trafic de Hyper-V qui réplique tooAzure passe par un hôte Hyper-V spécifique. Vous pouvez limiter la bande passante sur le serveur hôte de hello.
* **Influencer la bande passante**: vous pouvez influer sur la bande passante hello utilisée pour la réplication à l’aide de deux clés de Registre.

### <a name="throttle-bandwidth"></a>Limiter la bande passante
1. Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur le serveur hôte de Hyper-V hello. Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **limitation** onglet sélectionnez **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation**et définir des limites de hello pour le travail et non liés au travail heures. Les plages valides sont de Mbits/s des too102 de 512 Kbits/s par seconde.

    ![Limiter la bande passante](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

Vous pouvez également utiliser hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) de limitation tooset applet de commande. Voici un exemple :

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.

### <a name="influence-network-bandwidth"></a>Influer sur la bande passante réseau
1. Dans le Registre de hello accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * le trafic de la bande passante de hello tooinfluence sur un disque de réplication, modifiez hello de valeur hello **UploadThreadsPerVM**, ou créez la clé de hello si elle n’existe pas.
   * la bande passante de hello tooinfluence pour le trafic de la restauration automatique d’Azure, modifier la valeur de hello **DownloadThreadsPerVM**.
2. Hello par défaut est 4. Dans un réseau « surapprovisionnée », ces clés de Registre doivent être modifiées à partir des valeurs par défaut de hello. Hello maximal est 32. Surveiller le trafic toooptimize hello valeur.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 4 : planifier la mise en réseau](vmm-to-azure-walkthrough-network.md).
