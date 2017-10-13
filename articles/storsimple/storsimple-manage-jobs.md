---
title: "Affichage et gestion des tâches StorSimple | Microsoft Docs"
description: "Décrit la page Tâches du service StorSimple Manager et explique comment l’utiliser pour effectuer le suivi des tâches de sauvegarde planifiées, actuelles et récentes."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 7d9377bb8f3cb8c587823c2d71d61dfb9b50f52f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a>Utiliser le service StorSimple Manager pour afficher et gérer les tâches StorSimple
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Vue d'ensemble
La page **Tâches** est un portail centralisé unique qui permet de consulter et de gérer les tâches qui ont été lancées sur les appareils connectés à votre service StorSimple Manager. Vous pouvez consulter les tâches planifiées, en cours d'exécution, terminées et en échec pour plusieurs appareils. Les résultats sont présentés sous forme de tableau. 

![Page Tâches](./media/storsimple-manage-jobs/HCS_JobsPage.png)

Vous pouvez rechercher rapidement les tâches qui vous intéressent en filtrant sur les champs, à savoir :

* **État** : les tâches peuvent être en cours d’exécution, planifiées, en échec, terminées, en cours d’annulation ou annulées.
* **Type** : les tâches peuvent être créées suite à une sauvegarde planifiée ou à la demande (**Exécuter la sauvegarde**), un clonage, une restauration d’appareil ou une mise à jour.
* **Appareils** : les tâches sont initiées sur un certain appareil connecté à votre service.
* **De et À** : les tâches peuvent être filtrées selon la date et l’heure.

Les tâches filtrées sont ensuite affichées sous forme de tableau sur la base des attributs suivants :

* **Type** : sauvegarde, clonage, restauration, basculement ou mise à jour.
* **État** : en cours d’exécution, planifié, en échec, terminé, en cours d’annulation ou annulé.
* **Entité** : les tâches peuvent être associées à un volume, une stratégie de sauvegarde ou un appareil. Une tâche de clonage est associée à un volume, tandis qu'une tâche de sauvegarde planifiée est associée à une stratégie de sauvegarde. Une tâche d’appareil est créée à la suite d’une récupération d'urgence ou d’une opération de restauration.
* **Appareil** : nom de l’appareil sur lequel la tâche a été lancée.
* **Démarré le** : date à laquelle la tâche a été lancée.
* **Progression** : pourcentage d’achèvement d’une tâche en cours d’exécution. Pour une tâche terminée, le pourcentage doit toujours être de 100 %.

La liste des tâches est actualisée toutes les 30 secondes.

Cette page vous permet d’effectuer diverses actions liées aux tâches, à savoir :

* Affichage des détails d’une tâche
* Annulation d’une tâche

## <a name="view-job-details"></a>Affichage des détails d’une tâche
Pour afficher les détails d’une tâche, procédez comme suit.

#### <a name="to-view-job-details"></a>Pour afficher les détails d’une tâche
1. Dans la page **Tâches** , affichez la ou les tâches qui vous intéressent en exécutant une requête avec les filtres appropriés. Vous pouvez rechercher des tâches terminées, en cours d'exécution ou annulées.
2. Sélectionnez une tâche.
3. En bas de la page, cliquez sur **Détails**.
4. Dans la boîte de dialogue **Détails de la tâche de sauvegarde** , vous pouvez consulter l’état, les détails, les statistiques temporelles et les statistiques de données.

## <a name="cancel-a-job"></a>Annulation d’une tâche
Pour annuler une tâche en cours d’exécution, procédez comme suit.

### <a name="to-cancel-a-job"></a>Pour annuler une tâche
1. Dans la page **Tâches** , affichez les tâches en cours d’exécution que vous voulez annuler en exécutant une requête avec les filtres appropriés.
2. Sélectionnez la tâche.
3. En bas de la page, cliquez sur **Annuler**.
4. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.

Cette tâche est à présent annulée.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [gestion de vos stratégies de sauvegarde StorSimple](storsimple-manage-backup-policies.md).
* Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).

