---
title: "aaaView et gérer des tâches de StorSimple | Documents Microsoft"
description: "Décrit la page de travaux du service Gestionnaire StorSimple hello et comment toouse il tootrack récente, en cours et planifiées travaux de sauvegarde."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>Utilisez hello StorSimple Manager service tooview et gérer des travaux de StorSimple (Update 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Vue d'ensemble
Hello **travaux** page fournit un portail centralisé unique pour l’affichage et la gestion des travaux qui ont été démarrées sur les périphériques connectés tooyour le service StorSimple Manager. Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils. Les résultats sont présentés sous forme de tableau. 

![Page Tâches](./media/storsimple-manage-jobs-u2/jobs.png)

Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :

* **État** : les tâches peuvent être en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.
* **Depuis et vers** – travaux peuvent être filtrées hello en fonction de date et la plage horaire.
* **Type** – type de tâche hello peut être une sauvegarde, une sauvegarde manuelle, restauration, clone, basculement de l’appareil, créer un volume attaché localement, modifier le volume, mettez à jour, prennent en charge le package ou la configuration de périphérique virtuel.
* **Appareils** – travaux sont initiés sur un certain service tooyour de périphérique connecté.
  Hello travaux filtrés est ensuite sous forme de tableau sur la base de hello de hello suivant d’attributs :
  
  * **Type** : sauvegarde, sauvegarde manuelle, restauration, clonage, basculement d'appareil, créer un volume épinglé localement, modifier le volume, mettre à jour, prendre en charge le package ou approvisionnement de l'appareil virtuel.
  * **État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.
  * **Entité** – les travaux hello peuvent être associés à un volume, une stratégie de sauvegarde ou un périphérique. Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde. Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.
  * **APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.
  * **Démarré sur** – heure hello auxquelles hello travail a démarré.
  * **Progression** – hello pourcentage de réalisation d’une tâche en cours d’exécution. Pour une tâche terminée, le pourcentage doit toujours être de 100 %.

Hello de la liste des travaux est actualisée toutes les 30 secondes.

Vous pouvez effectuer hello suivant d’actions relatives à la tâche sur cette page :

* Affichage des détails d’une tâche
* Annulation d’une tâche

## <a name="view-job-details"></a>Affichage des détails d’une tâche
Effectuer hello suivant détaille de hello tooview étapes d’un travail.

#### <a name="tooview-job-details"></a>Détails de la tâche tooview
1. Sur hello **travaux** page, affichez ou les travaux hello vous intéressent en exécutant une requête avec les filtres appropriés. Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.
2. Sélectionnez une tâche.
3. Au bas de hello de page de hello, cliquez sur **détails**.
4. Bonjour **détails de la tâche sauvegarde** boîte de dialogue, vous pouvez afficher le statut de hello, détails, les statistiques de temps et les statistiques de données.
   
    ![Page Détails de la tâche](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>Annulation d’une tâche
Effectuer hello suivant les étapes toocancel un travail en cours d’exécution.

> [!NOTE]
> Certaines tâches, telles que la modification d’un type de volume volume toochange hello ou étendre un volume, ne peut pas être annulées.
> 
> 

### <a name="toocancel-a-job"></a>toocancel un travail
1. Sur hello **travaux** page, affichez ou les travaux en cours d’exécution hello que vous souhaitez toocancel en exécutant une requête avec les filtres appropriés.
2. Sélectionnez le travail de hello.
3. Au bas de hello de page de hello, cliquez sur **Annuler**.
4. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.

Cette tâche est à présent annulée.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[gérer vos stratégies de sauvegarde StorSimple](storsimple-manage-backup-policies.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

