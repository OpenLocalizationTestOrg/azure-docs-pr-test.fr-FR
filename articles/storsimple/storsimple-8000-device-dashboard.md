---
title: "Appareil de série aaaUse StorSimple 8000 résumé | Documents Microsoft"
description: "Décrit le périphérique de service du Gestionnaire de périphériques StorSimple hello résumé et comment toouse il tooview storage metrics et les initiateurs connectés et les rechercher hello numéro de série et le nom qualifié."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Utiliser l’appareil hello résumé dans le service Gestionnaire de périphériques StorSimple

## <a name="overview"></a>Vue d'ensemble
panneau Résumé du périphérique StorSimple Hello vous donne une vue d’ensemble des informations relatives à un périphérique StorSimple spécifique, en revanche toohello service panneau Résumé, qui fournit des informations sur tous les appareils hello inclus dans votre solution Microsoft Azure StorSimple.

panneau Résumé du périphérique Hello fournit un résumé d’un appareil de série StorSimple 8000 est inscrit avec une donnée StorSimple Gestionnaire de périphériques, mise en évidence les problèmes de périphériques qui nécessitent une intervention d’un administrateur système. Ce didacticiel présente panneau Résumé du périphérique hello, explique la fonction et le contenu de hello et décrit les tâches hello que vous pouvez effectuer à partir de ce panneau.

panneau Résumé du périphérique Hello affiche hello informations suivantes :

![Panneau de synthèse de l’appareil](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Barre de commandes de gestion

Dans le panneau de périphérique StorSimple hello, vous voyez les options hello gestion de votre périphérique StorSimple. Vous consultez les commandes de gestion hello haut hello du Panneau de hello et sur le côté gauche de hello. Utilisez ces options tooadd partages ou des volumes, ou mettre à jour ou basculer votre appareil.

![Barre de commandes de gestion](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Essentials

zone d’essentials Hello capture certaines des propriétés importantes de hello comme état de hello, modèle, IQN cible et version du logiciel hello. 

![Éléments principaux des appareils](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Surveillance

* Hello **alertes** vignette fournit un instantané de toutes les alertes actives hello pour votre appareil, regroupée par gravité.

    ![Vignette Alertes](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Cliquez sur Bonjour vignette tooopen Bonjour **alertes** panneau, puis cliquez sur un individu alerte tooview supplémentaire plus d’informations sur cette alerte, y compris les actions recommandées. Vous pouvez également effacer les alerte hello si hello est résolu.

    ![Cliquer sur la vignette Alertes](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Hello **état et l’intégrité** vignette fournit des informations sur l’intégrité du composant hello matériel pour un périphérique, notamment l’état du périphérique hello. état du périphérique Hello peut être hors connexion, en ligne, désactivé ou prêt tooset up.

    ![Vignette État et intégrité](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Hello **Volumes** vignette fournit un résumé du nombre de hello de volumes de votre appareil, regroupés par état.

    ![Vignette Volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Cliquez sur Bonjour vignette tooopen Bonjour **Volumes** liste panneau, puis cliquez sur un volume individuel de tooview ou modifier ses propriétés.
    
    ![Cliquer sur la vignette Volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Pour plus d’informations, consultez Comment trop[gérer les volumes](storsimple-8000-manage-volumes-u2.md).

* Bonjour **utilisation** graphique, vous pouvez afficher les stockage principal hello utilisée sur votre appareil et le stockage en cloud hello consommées sur hello des 7 derniers jours, la valeur par défaut de hello laps de temps.

     ![Mosaïque Utilisation](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose une échelle de temps différente, utilisez hello **modifier** option dans l’angle supérieur droit de hello du graphique de hello.

     ![Modifier le graphique Utilisation](./media/storsimple-8000-device-dashboard/device-summary12.png)

     Dans ce graphique, vous pouvez afficher les métriques de stockage principal total hello (montant hello des données écrites par l’appareil de tooyour hôtes) et hello totale consommé par votre appareil sur une période de temps de stockage cloud.
  
     Dans ce contexte, *stockage principal* fait référence toohello la quantité totale de données écrites par hello hôte et peut être décomposée en type de volume : *principal de stockage hiérarchisé* inclut les deux stockés localement les données et les données cloud toohello à plusieurs niveaux. Le *stockage principal attaché localement* inclut uniquement les données stockées localement. *Stockage cloud*, on hello d’autre part, est une mesure de la quantité totale de hello des données stockées dans le cloud de hello. Ce stockage inclut les données hiérarchisées et les sauvegardes. les données Hello stockées dans le cloud de hello sont dédupliquées et compressées, alors que le stockage principal indique la quantité hello de stockage utilisé avant hello sont dédupliquées et des données compressées. (Vous pouvez comparer ces tooget de deux nombres une idée du taux de compression hello). Pour les deux types et stockage hello les montants indiqués sont basées sur hello suivi fréquence que vous configurez en nuage. Par exemple, si vous choisissez une fréquence hebdomadaire, puis graphique de hello affiche les données pour chaque jour Bonjour semaine précédente.

     quantité de hello toosee de stockage cloud consommé sur le temps, sélectionnez hello **stockage CLOUD utilisé** option. stockage total toosee hello qui a été écrit par hôte hello, sélectionnez hello **hiérarchisé stockage utilisé principal** et **localement ÉPINGLÉ stockage principal utilisé** options. 
     Pour plus d’informations, consultez [utilisez hello toomonitor du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-monitor-device.md).


* Hello **capacité** vignette affiche hello stockage principal qui est configuré et restants dans hello appareil relatif toohello stockage total disponible pour hello identiques. **Configuré** fait référence toohello quantité de stockage qui est préparée et allouée à l’utilisation, **restant** fait référence toohello restant de capacité qui peut être configurée sur ce périphérique. 

    ![Mosaïque Utilisation](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Cliquez sur cette tooview vignette la capacité de hello est configurée sur les volumes attachés localement et hiérarchisés. Hello **hiérarchisé restantes** capacité est la capacité disponible hello qui peut être configurée, y compris le nuage, tout en hello **restant Local** est la capacité hello restant sur des disques hello toothis de périphérique.

    ![Cliquer sur le graphique Utilisation](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [panneau Résumé du service StorSimple](storsimple-8000-service-dashboard.md).
* En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

