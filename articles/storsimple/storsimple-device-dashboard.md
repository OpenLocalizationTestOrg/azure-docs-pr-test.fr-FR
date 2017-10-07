---
title: "tableau de bord du périphérique de StorSimple Manager aaaUse hello | Documents Microsoft"
description: "Décrit le tableau de bord du périphérique de service hello StorSimple Manager et comment toouse il tooview storage metrics et les initiateurs connectés et les rechercher hello numéro de série et le nom qualifié."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Utilisez le tableau de bord de périphérique hello dans le service StorSimple Manager  

## <a name="overview"></a>Vue d'ensemble
tableau de bord périphérique Hello StorSimple Manager vous donne une vue d’ensemble des informations relatives à un périphérique StorSimple spécifique, en revanche toohello service tableau de bord, qui fournit des informations sur tous les appareils hello inclus dans votre solution Microsoft Azure StorSimple.

![Page du tableau de bord d’un appareil](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

tableau de bord Hello contient hello informations suivantes :

* **Zone de graphique** – vous pouvez voir des mesures de stockage pertinentes hello dans la zone de graphique hello haut hello du tableau de bord hello. Dans ce graphique, vous pouvez afficher les métriques de stockage principal total hello (montant hello des données écrites par l’appareil de tooyour hôtes) et hello totale consommé par votre appareil sur une période de temps de stockage cloud.
  
     Dans ce contexte, *stockage principal* fait référence toohello la quantité totale de données écrites par hello hôte et peut être décomposée en type de volume : *principal de stockage hiérarchisé* inclut les deux stockés localement les données et les données toohello hiérarchisé cloud ; *principal attaché localement stockage* inclut seulement les données stockées localement. *Stockage cloud*, on hello d’autre part, est une mesure de la quantité totale de hello des données stockées dans le cloud de hello. Cela inclut les données hiérarchisées et les sauvegardes. Notez que les données stockées dans le cloud de hello sont dédupliquées et compressées, alors que le stockage principal indique la quantité hello de stockage utilisé avant hello sont dédupliquées et des données compressées. (Vous pouvez comparer ces tooget de deux nombres une idée du taux de compression hello). Pour les deux types et stockage hello hello suivi fréquence que vous configurez doit reposer les montants indiqués en nuage. Par exemple, si vous choisissez une fréquence hebdomadaire, hello graphique affiche données pour chaque jour de hello semaine précédente.
  
     Vous pouvez configurer les graphique hello comme suit :
  
  * quantité de hello toosee de stockage cloud consommé sur le temps, sélectionnez hello **stockage CLOUD utilisé** option. stockage total toosee hello qui a été écrit par hôte hello, sélectionnez hello **hiérarchisé stockage utilisé principal** et **localement ÉPINGLÉ stockage principal utilisé** options. L’illustration hello, les deux options sont sélectionnées ; Par conséquent, le graphique de hello affiche les quantités de stockage pour le cloud et le stockage principal. Notez que n’importe quel stockage principal utilisé tooinstalling préalable 2 de la mise à jour est représentée par hello **principal hiérarchisé stockage utilisé** ligne.
  * Menu de liste déroulante utiliser hello en hello en haut à droite du graphique de hello toospecify une période de temps de 1 semaine, 1 mois, 3 mois ou 1 an. Notez que hello graphique de niveau supérieur est actualisé qu’une seule fois par jour et par conséquent reflète hello totaux du jour précédent.
    
    Pour plus d’informations, consultez [utilisez hello toomonitor du service StorSimple Manager de votre appareil StorSimple](storsimple-monitor-device.md).
* **Présentation de l’utilisation** : Bonjour **présentation de l’utilisation** zone, vous pouvez voir hello quantité de stockage principal utilisée, quantité hello stockage déployé et la capacité de stockage maximale hello pour votre appareil. En comparant ces quantité maximale d’utilisation des nombres toohello de stockage est disponible, vous pouvez voir en un coup de œil si vous avez besoin d’un stockage supplémentaire tooobtain. Notez que cette vue d’ensemble est de mise à jour toutes les 15 minutes et, en raison de la différence de hello de fréquence de mise à jour, peut-être afficher des chiffres différents de ceux affiché dans hello zone de graphique ci-dessus, qui est mis à jour quotidiennement. Pour plus d’informations, consultez [utilisez hello toomonitor du service StorSimple Manager de votre appareil StorSimple](storsimple-monitor-device.md).
* **Alertes** : hello **alertes** zone contient une vue d’ensemble des alertes hello pour votre appareil. Alertes sont regroupées par niveau de gravité, et est indiqué de nombre de hello d’alertes pour chaque niveau de gravité. En cliquant sur alerte hello gravité ouvre une vue adaptée de hello les alertes onglet tooshow que vous hello uniquement les alertes de ce niveau de gravité pour cet appareil.
* **Travaux** : hello **travaux** zone indique hello de résultat de l’activité des travaux récents. Cela peut vous assurer que hello système fonctionne comme prévu, ou il peut vous informer que vous avez besoin d’une action corrective tootake. toosee plus d’informations sur les travaux effectués récemment, cliquez sur **travaux réussis dans hello des dernières 24 heures**.
* Hello **coup de œil rapide** zone hello à droite du tableau de bord de hello fournit des informations utiles telles que le modèle d’appareil, numéro de série, état, la description et le nombre de volumes.

Vous pouvez également configurer le basculement et afficher les initiateurs connectés à partir du tableau de bord de périphérique hello.

tâches courantes Hello qui peuvent être effectuées sur cette page sont :

* Affichage des initiateurs connectés
* Rechercher le numéro de série du périphérique hello
* Trouver hello IQN cible

## <a name="view-connected-initiators"></a>Affichage des initiateurs connectés
Vous pouvez afficher les initiateurs iSCSI hello qui sont connectés tooyour périphérique en cliquant sur hello **afficher les initiateurs connectés** lien fourni dans hello **coup de œil rapide** zone du tableau de bord de votre appareil. Cette page fournit un tableau qui répertorie les initiateurs hello qui se sont correctement connectés tooyour appareil. Pour chaque initiateur, vous pouvez voir :

* Hello iSCSI nom qualifié (IQN) de hello connectés initiateur.
* nom de Hello de hello contrôle enregistrement accès (ACR) qui autorise cet initiateur connecté.
* adresse IP Hello hello connectés initiateur.
* cet initiateur hello interfaces Hello réseau est connecté tooon votre périphérique de stockage. Ils peuvent aller de DATA 0 tooDATA 5.
* Tous les volumes hello hello initiateur connecté est autorisé tooaccess selon la configuration ACR actuelle de toohello.

Si vous voyez des initiateurs inattendus dans cette liste ou que vous ne voyez pas hello attendus, passez en revue votre configuration ACR. 512 initiateurs maximum permettre se connecter tooyour appareil.

## <a name="find-hello-device-serial-number"></a>Rechercher le numéro de série du périphérique hello
Vous devrez peut-être le numéro de série du périphérique hello lorsque vous configurez Microsoft Multipath i / o (MPIO) sur l’appareil de hello. Effectuer hello suivant le numéro de série de l’appareil d’étapes toofind hello.

#### <a name="toofind-hello-device-serial-number"></a>numéro de série du périphérique toofind hello
1. Accédez trop**périphériques** > **tableau de bord**.
2. Dans le volet de droite hello du tableau de bord hello, recherchez hello **coup de œil rapide** zone.
3. Faites défiler vers le bas et recherchez le numéro de série hello.

## <a name="find-hello-device-target-iqn"></a>Trouver hello IQN cible
Vous devrez peut-être hello IQN cible lorsque vous configurez hello CHAP Challenge Handshake Authentication Protocol () sur votre appareil StorSimple. Effectuer hello suivant les étapes toofind hello IQN cible.

### <a name="toofind-hello-device-target-iqn"></a>toofind hello IQN cible
1. Accédez trop**périphériques** > **tableau de bord**.
2. Dans le volet de droite hello du tableau de bord hello, recherchez hello **coup de œil rapide** zone.
3. Faites défiler la liste et trouver de cible de hello IQN.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur hello [tableau de bord de service StorSimple Manager](storsimple-service-dashboard.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

