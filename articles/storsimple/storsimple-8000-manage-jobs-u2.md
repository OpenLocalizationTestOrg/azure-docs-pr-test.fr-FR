---
title: "aaaView et gérer des tâches pour la série StorSimple 8000 | Documents Microsoft"
description: "Décrit le panneau de travaux de service de gestionnaire de périphériques StorSimple hello et comment toouse il tootrack récente, en cours et planifiées travaux de sauvegarde."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Utilisez tooview de service de gestionnaire de périphériques StorSimple hello et gérer des tâches (Update 3 et versions ultérieur)

## <a name="overview"></a>Vue d'ensemble
Hello **travaux** panneau fournit un portail centralisé unique pour l’affichage et la gestion des travaux qui ont été démarrées sur les périphériques connectés tooyour le Gestionnaire de périphériques StorSimple service. Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées, annulées et en échec pour plusieurs appareils. Les résultats sont présentés sous forme de tableau.

![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

Vous pouvez rechercher rapidement les travaux qui hello que vous intéressent en filtrant sur des champs tels que :

* **État** : les travaux peuvent être en cours, s’être bien déroulés, avoir échoué, avoir été annulés ou s’être bien déroulés mais avec des erreurs.
* **Intervalle de temps** – travaux peuvent être filtrées hello en fonction de date et la plage horaire. les plages de Hello sont après 1 heure, dernières 24 heures, 7 derniers jours, 30 derniers jours, année ou dates personnalisée.
* **Type** – type de tâche hello peut être sauvegarde planifiée, de sauvegarde manuelle, de restauration de sauvegarde, cloner le volume, basculer les conteneurs de volumes, créer le volume attaché localement, modifier le volume, installer les mises à jour, collecter des journaux de prise en charge et créer le dispositif de cloud.
* **Appareils** – travaux sont initiés sur un certain service tooyour de périphérique connecté.
  
Hello travaux filtrés est ensuite sous forme de tableau sur la base de hello de hello suivant d’attributs :
  
* **Nom** : une sauvegarde planifiée, une sauvegarde manuelle, une restauration de sauvegarde, un clonage de volume, un basculement de conteneurs de volumes, une création de volume épinglé localement, une modification de volume, une installation de mises à jour, une collecte de journaux de support ou une création d’appliance cloud.
* **État** : en cours d'exécution, terminées, annulées, en échec, en cours d'annulation ou terminées avec des erreurs.
* **Entité** – les travaux hello peuvent être associés à un volume, une stratégie de sauvegarde ou un périphérique. Par exemple, une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde. Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.
* **APPAREIL** hello – nom de l’appareil hello sur quel hello travail a été démarré.
* **Démarré sur** – heure hello auxquelles hello travail a démarré.
* **Durée** – hello temps requis toocomplete hello tâche.

Hello de la liste des travaux est actualisée toutes les 30 secondes.

Vous pouvez effectuer hello suivant d’actions relatives à la tâche sur cette page :

* Affichage des détails d’une tâche
* Annulation d’une tâche

## <a name="view-job-details"></a>Affichage des détails d’une tâche
Effectuer hello suivant détaille de hello tooview étapes d’un travail.

#### <a name="tooview-job-details"></a>Détails de la tâche tooview
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, puis cliquez sur **travaux**.

2. Bonjour **travaux** panneau, une ou plusieurs tâches hello affichage vous intéressent en exécutant une requête avec les filtres appropriés. Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Sélectionnez un travail et cliquez dessus.

    ![Panneau Tâches](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. Dans le panneau de détails du travail hello, vous pouvez afficher hello état, détails, les statistiques de temps et les données statistiques.
   
    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Annulation d’une tâche
Effectuer hello suivant les étapes toocancel un travail en cours d’exécution.

> [!NOTE]
> Certaines tâches, telles que la modification d’un type de volume volume toochange hello ou étendre un volume, ne peut pas être annulées.


### <a name="toocancel-a-job"></a>toocancel un travail
1. Sur hello **travaux** page, affichez ou les travaux en cours d’exécution hello que vous souhaitez toocancel en exécutant une requête avec les filtres appropriés. Sélectionnez le travail de hello.

2. Avec le bouton droit dans le menu contextuel hello hello travail sélectionné tooinvoke et cliquez sur **Annuler**.

    ![Détails du travail](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. Cette tâche est à présent annulée.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[gérer vos stratégies de sauvegarde StorSimple](storsimple-8000-manage-backup-policies-u2.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

