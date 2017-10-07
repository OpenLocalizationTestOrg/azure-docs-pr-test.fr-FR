---
title: "aaaView et gérer des tâches de StorSimple Virtual Array | Documents Microsoft"
description: "Décrit la page de travaux du service de gestionnaire de périphérique StorSimple hello et comment toouse il tootrack des travaux récents et en cours pour hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Utilisez des tâches de tooview de service de gestionnaire de périphériques StorSimple hello pour hello StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Hello **travaux** panneau fournit un portail centralisé unique pour afficher et gérer des travaux qui est démarrés sur les réseaux virtuels sont connecté tooyour service du Gestionnaire de périphériques StorSimple. Vous pouvez consulter les tâches en cours d’exécution, terminées et en échec pour plusieurs appareils virtuels. Les résultats sont présentés sous forme de tableau.

![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :

* **Intervalle de temps** – travaux peuvent être filtrées hello en fonction de date et la plage horaire.
* **Appareils** – travaux sont initiés sur un service de tooyour périphérique connecté. Hello travaux filtrés est ensuite sous forme de tableau en fonction de hello suivant d’attributs :
  
  * **Nom** – nom de la tâche hello peut être **tous les**, **sauvegarde**, **Clone**, **basculer**, **télécharger les mises à jour** , ou **installer les mises à jour**.
  * **État** : l’état des tâches peut présenter la valeur **Toutes**, **En cours**, **Réussite**, **Échec** ou **Annulé**.
  * **Entité** – les travaux hello peuvent être associés à un volume, partage ou périphérique.
  * **APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.
  * **Démarré sur** – heure hello auxquelles hello travail a démarré.
  * **Durée** : hello durée sur laquelle travail hello a été exécutée.
* **État** : vous pouvez rechercher la totalité des tâches ou celles en cours d’exécution, terminées ou en échec.
* **Type de tâche** – type de tâche hello peut être all, sauvegarde, restauration, basculement, télécharger des mises à jour ou installer des mises à jour.

Hello de la liste des travaux est actualisée toutes les 30 secondes.

## <a name="view-job-details"></a>Affichage des détails d’une tâche
Effectuer hello suivant détaille de hello tooview étapes d’un travail.

#### <a name="tooview-job-details"></a>Détails de la tâche tooview
1. Sur hello **travaux** panneau, une ou plusieurs tâches hello affichage vous intéressent en exécutant une requête avec les filtres appropriés. Vous pouvez rechercher des tâches terminées ou en cours d’exécution.
2. Sélectionnez une tâche à partir de la liste tabulaire de hello des tâches.
   
    ![Panneau Tâches](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. Au bas de hello de page de hello, cliquez sur **détails**.
4. Bonjour **détails** boîte de dialogue, vous pouvez afficher le statut, les détails et les statistiques de temps. Hello l’illustration suivante montre un exemple de hello **détails de la tâche sauvegarde** boîte de dialogue.
   
    ![Détails du travail](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Échecs des tâches lors de la machine virtuelle de hello est suspendu dans hello hyperviseur
Lorsqu’une tâche est en cours sur votre StorSimple Virtual Array et le périphérique de hello (ordinateur virtuel configuré dans l’hyperviseur) est en pause est supérieure à 15 minutes, échec du travail de hello. Cela en raison du temps de StorSimple Virtual Array tooyour est synchronisée avec l’heure de Microsoft Azure hello. 

Vous verrez hello l’erreur suivante : « votre heure de l’appareil est synchronisé avec le temps de Microsoft Azure hello de plus de 15 minutes. Vérifiez que hello hyperviseur et les heures d’unité de hello sont synchronisées avec un serveur NTP. Verify that there are no connectivity issues. tootroubleshoot des problèmes de connectivité, exécutez les tests de diagnostic à partir de hello local interface utilisateur web de votre appareil virtuel. »

Ces échecs s’appliquent à des travaux toobackup, de restauration, de mise à jour et de basculement. Si votre machine virtuelle est configurée dans Hyper-V, machine de hello synchronise finalement heure avec votre hyperviseur. Une fois que ce sera le cas, vous pourrez redémarrer votre tâche.

## <a name="next-steps"></a>Étapes suivantes
[Découvrez comment toouse hello tooadminister de l’interface utilisateur web locale votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

