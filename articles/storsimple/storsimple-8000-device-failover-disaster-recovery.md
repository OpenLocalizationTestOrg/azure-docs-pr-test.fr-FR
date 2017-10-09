---
title: "basculement aaaStorSimple, récupération d’urgence pour les appareils 8000 series | Documents Microsoft"
description: "Découvrez comment toofail sur votre tooitself de périphérique StorSimple, une autre unité physique ou un dispositif de cloud."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 9d01ee30b15b77072b1d4dfe9a215abc83ffba28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-8000-series-device"></a>Basculement et récupération d’urgence pour votre appareil de la gamme StorSimple 8000

## <a name="overview"></a>Vue d'ensemble

Cet article décrit la fonctionnalité de basculement d’appareil hello pour les appareils hello StorSimple 8000 series et comment cette fonctionnalité peut être utilisé toorecover StorSimple périphériques si un incident se produit. StorSimple utilise données hello toomigrate de basculement l’appareil à partir d’un appareil source dans l’appareil de cible tooanother hello centre de données. instructions de Hello dans cet article s’appliquent des périphériques physiques tooStorSimple 8000 series et appareils de cloud qui exécutent des versions de logiciel mise à jour 3 et versions ultérieures.

StorSimple utilise hello **périphériques** fonctionnalité de basculement de périphérique panneau toostart hello dans l’événement hello de sinistre. Ce panneau répertorie tous les hello StorSimple périphériques connectés tooyour périphérique le service StorSimple Manager.

![Panneau Appareils](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)


## <a name="disaster-recovery-dr-and-device-failover"></a>Récupération d’urgence et basculement d’appareil

Dans un scénario de récupération d’urgence, périphérique principal de hello cesse de fonctionner. StorSimple utilise le périphérique principal de hello en tant que _source_ et déplace hello associé cloud données tooanother _cible_ appareil. Ce processus est référencé tooas hello *basculement*. Hello graphique suivant illustre le processus hello de basculement.

![Que se passe-t-il dans le basculement de l’appareil ?](./media/storsimple-8000-device-failover-disaster-recovery/failover-dr-flow.png)

unité de cible de Hello pour un basculement peut être un périphérique physique ou même un dispositif de cloud. Hello appareil cible peut être situé dans hello même ou à un emplacement géographique différent à l’appareil source de hello.

Pendant le basculement de hello, vous pouvez sélectionner des conteneurs de volumes pour la migration. StorSimple passe la propriété de hello de ces conteneurs de volumes de hello source toohello cible un périphérique. Une fois que les conteneurs de volumes hello modifier la propriété, StorSimple supprime ces conteneurs de périphérique de source de hello. Après que la suppression de hello est terminée, vous pouvez échouer équipement hello précédent. _La restauration automatique_ transferts hello périphérique source d’origine de la propriété toohello précédent.

### <a name="cloud-snapshot-used-during-device-failover"></a>Capture instantanée cloud utilisée pendant le basculement de l’appareil

Après une récupération d’urgence, la sauvegarde la plus récente sur le cloud hello est toorestore utilisé hello toohello cible dispositif. Pour plus d’informations sur les instantanés de cloud, consultez [utiliser hello le Gestionnaire de périphériques StorSimple service tootake une sauvegarde manuelle](storsimple-8000-manage-backup-policies-u2.md#take-a-manual-backup).

Sur un appareil de la gamme StorSimple 8000, les stratégies de sauvegarde sont associées à des sauvegardes. S’il existe plusieurs stratégies de sauvegarde pour hello même volume, puis sélectionne des StorSimple hello stratégie de sauvegarde avec hello plus grand nombre de volumes. StorSimple utilise ensuite la sauvegarde la plus récente à partir des données de hello hello sélectionné stratégie de sauvegarde toorestore hello sur le périphérique cible de hello.

Supposons qu’il existe deux stratégies de sauvegarde, *defaultPol* et *customPol* :

* *defaultPol* : un seul volume, *vol1*, s’exécute tous les jours à 22 h 30.
* *customPol* : quatre volumes, *vol1*, *vol2*, *vol3* et *vol4*, s’exécutent tous les jours à 22 h 00.

Dans ce cas, StorSimple donne la priorité pour des raisons de cohérence en cas d’incident et utilise *customPol*, car elle a plus de volumes. sauvegarde la plus récente de cette stratégie Hello donnée toorestore utilisé. Pour plus d’informations sur la façon de toocreate et de gérer les stratégies de sauvegarde, accédez trop[utiliser des stratégies de sauvegarde hello le Gestionnaire de périphériques StorSimple service toomanage](storsimple-8000-manage-backup-policies-u2.md).

## <a name="common-considerations-for-device-failover"></a>Considérations courantes relatives au basculement d’appareil

Avant de basculer sur un appareil, passez en revue hello informations suivantes :

* Avant le début d’un basculement de l’appareil, tous les volumes hello dans des conteneurs de volume hello doivent être en mode hors connexion. Dans un basculement non planifié, les volumes StorSimple seront automatiquement mis hors connexion. Mais si vous effectuez un basculement planifié (tootest DR), vous devez déconnecter tous les volumes hello.
* Hello uniquement les conteneurs de volumes que vous ont associé à un instantané cloud sont répertoriés pour la récupération d’urgence. Il doit exister au moins un conteneur de volumes avec des données de toorecover instantané cloud associé.
* S’il existe des captures instantanées cloud qui s’étendent sur plusieurs conteneurs de volumes, StorSimple bascule ces conteneurs de volumes comme un ensemble. Dans une instance rare, si les instantanés locaux qui s’étendent sur plusieurs conteneurs de volumes mais des instantanés cloud associés ne le faites pas, StorSimple ne bascule les instantanés locaux hello et les données locales hello seront perdues après la récupération d’urgence.
* Hello des périphériques de cibles disponibles pour la récupération d’urgence sont possédant suffisamment d’espace tooaccommodate hello conteneurs de volumes sélectionnés. Tous les appareils ne disposant pas de suffisamment d’espace ne sont pas répertoriés en tant qu’appareils cibles.
* Après une récupération d’urgence (pour une durée limitée), performances d’accès aux données hello peuvent être affectées de manière significative, en tant que périphérique de hello doit tooaccess hello données hello cloud et les stocker localement.

#### <a name="device-failover-across-software-versions"></a>Basculement de l'appareil entre les versions du logiciel

Un service StorSimple Device Manager dans un déploiement peut avoir plusieurs appareils physiques et cloud, exécutant tous des versions différentes du logiciel.

Utilisez hello suivant toodetermine de la table si vous pouvez basculer ou échouer appareil tooanother arrière exécutant une autre version logicielle et le comportement des types de volume hello pendant la récupération d’urgence.

#### <a name="failover-and-failback-across-software-versions"></a>Basculement et restauration automatique entre les versions logicielles

| Basculement/restauration automatique depuis | Appareil physique | Appliance cloud |
| --- | --- | --- |
| Mise à jour 3 tooUpdate 4 |Les volumes hiérarchisés sont basculés en tant qu’éléments hiérarchisés. <br></br>Les volumes épinglés localement sont basculés en tant qu’éléments épinglés localement. <br></br> Après un basculement lorsque vous prenez un instantané sur l’appareil de mise à jour 4 de hello, [suivi heatmap](storsimple-update4-release-notes.md#whats-new-in-update-4) intervient. |Les volumes épinglés localement sont basculés en tant qu’éléments hiérarchisés. |
| Mise à jour 4 tooUpdate 3 |Les volumes hiérarchisés sont basculés en tant qu’éléments hiérarchisés. <br></br>Les volumes épinglés localement sont basculés en tant qu’éléments épinglés localement. <br></br> Sauvegardes toorestore conserver les métadonnées heatmap. <br></br>Le suivi basé sur une carte thermique n’est pas disponible dans Update 3 après une restauration automatique. |Les volumes épinglés localement sont basculés en tant qu’éléments hiérarchisés. |


## <a name="device-failover-scenarios"></a>Scénario de basculement d’appareil

En l’absence d’un incident, vous pouvez choisir toofail sur votre appareil StorSimple :

* [périphérique physique de tooa](storsimple-8000-device-failover-physical-device.md).
* [tooitself](storsimple-8000-device-failover-same-device.md).
* [Dispositif de cloud tooa](storsimple-8000-device-failover-cloud-appliance.md).

Hello précédents articles fournissent des instructions détaillées pour chacun des hello au-dessus de cas de basculement.


## <a name="failback"></a>Restauration automatique

Pour Update 3 et les versions ultérieures, StorSimple prend également en charge la restauration automatique. La restauration automatique est simplement hello inverse de basculement, cible de hello devient la source de hello et hello d’origine source pendant le basculement hello maintenant devient équipement hello. 

Lors du retour arrière, StorSimple RE-synchronise les emplacement principal du précédent toohello données hello, arrête hello d’e/s et l’activité de l’application et passe l’emplacement d’origine de toohello précédent.

Après qu’un basculement est terminé, StorSimple exécute hello suivant des actions :

* StorSimple nettoie les conteneurs de volumes hello ayant basculé à partir de l’appareil source de hello.
* StorSimple lance une tâche en arrière-plan par conteneur de volumes (basculé) sur l’appareil source de hello. Si vous essayez de toofail lors de hello est en cours, vous recevez un effet toothat de notification. Patienter jusqu'à ce que le travail de hello est la restauration automatique de hello toostart terminée.
* Durée Hello de la suppression de hello toocomplete de conteneurs de volumes dépend de divers facteurs tels que la quantité de données, la durée de vie de données de hello, nombre de sauvegardes et hello la bande passante disponible pour l’opération de hello.

Si vous envisagez de tester les basculements ou restaurations automatiques, nous vous recommandons de tester des conteneurs de volumes comprenant moins de données (Go). En règle générale, vous pouvez démarrer la restauration automatique hello 24 heures après que le basculement de hello est terminé.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

Q : **Que se passe-t-il si hello récupération d’urgence échoue ou succès partiel ?**

R : En cas de récupération d’urgence de hello, nous vous recommandons d’essayer à nouveau. travail de basculement Hello deuxième périphérique a connaissance de progression hello de tâche hello et commence à partir de ce point et les versions ultérieures.

Q : **Puis-je supprimer une unité pendant que le basculement de l’appareil hello est en cours ?**

R : Vous ne pouvez pas supprimer un appareil lorsqu’une récupération d’urgence est en cours. Vous pouvez uniquement supprimer votre appareil après que hello récupération d’urgence est terminée. Vous pouvez surveiller la progression du travail de basculement hello appareil Bonjour **travaux** panneau.

Q : **Lorsque le garbage collection de hello ne démarre pas sur l’appareil source de hello afin que les données locales de hello sur l’appareil source sont supprimées ?**

R : Le garbage collection est activé sur l’appareil source de hello uniquement après que l’appareil de hello est complètement nettoyé. nettoyage de Hello inclut le nettoyage des objets qui ont échoué sur périphérique source de hello tels que des volumes, des objets de sauvegarde (pas de données), des conteneurs de volumes et des stratégies.

Q : **Que se passe-t-il si hello supprimer le travail associé à des conteneurs de volumes hello dans l’appareil source de hello échoue ?**

R :  Si hello supprimer un travail échoue, vous pouvez supprimer manuellement les conteneurs de volumes hello. Bonjour **périphériques** panneau, sélectionnez votre appareil source et cliquez sur **conteneurs de volumes**. Cliquez sur les conteneurs de volumes hello SELECT qui vous a échoué sur et en bas hello du Panneau de hello, **supprimer**. Après avoir supprimé tous les hello a échoué sur les conteneurs de volumes sur l’appareil source de hello, vous pouvez démarrer la restauration automatique hello. Pour plus d’informations, consultez trop[supprimer un conteneur de volume](storsimple-8000-manage-volume-containers.md#delete-a-volume-container).

## <a name="business-continuity-disaster-recovery-bcdr"></a>Continuité d’activité et récupération d’urgence (Business Continuity Disaster Recovery - BCDR)

Un scénario de récupération d’urgence d’entreprise la continuité des activités se produit lorsque le centre de données Azure entier hello cesse de fonctionner. Ce scénario peut affecter votre service de gestionnaire de périphériques StorSimple et hello associés appareils StorSimple.

Si un appareil StorSimple a été inscrit juste avant un incident, cet appareil peut-être tooundergo une réinitialisation. Après sinistre de hello, l’appareil StorSimple hello s’affiche dans hello portail Azure comme étant hors connexion. Ce périphérique doit être supprimé hello portail. Paramètres par défaut de hello appareil toofactory et enregistrez-le à nouveau avec le service de hello.

## <a name="next-steps"></a>Étapes suivantes

Si vous êtes prêt tooperform un basculement de l’appareil, choisissez une des hello pour obtenir des instructions détaillées, les scénarios suivants :

- [Basculer le périphérique physique de tooanother](storsimple-8000-device-failover-physical-device.md)
- [Basculer toohello même appareil](storsimple-8000-device-failover-same-device.md)
- [Basculer tooStorSimple dispositif de Cloud](storsimple-8000-device-failover-cloud-appliance.md)

Si vous avez basculé votre appareil, choisissez une des options suivantes de hello :

* [Deactivate and delete a StorSimple device](storsimple-8000-deactivate-and-delete-device.md) (Désactiver et supprimer un appareil StorSimple).
* [Utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

