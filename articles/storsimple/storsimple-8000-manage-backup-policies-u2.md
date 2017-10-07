---
title: "stratégies de sauvegarde aaaManage StorSimple 8000 series | Documents Microsoft"
description: "Explique comment vous pouvez utiliser toocreate de service de gestionnaire de périphériques StorSimple hello et gérer des sauvegardes manuelles, de planifications de sauvegarde et de rétention des sauvegardes sur un appareil de série StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Utiliser le service du Gestionnaire de périphériques StorSimple hello dans les stratégies de sauvegarde toomanage portail Azure


## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment toouse hello service du Gestionnaire de périphériques StorSimple **stratégie de sauvegarde** les processus de sauvegarde toocontrol lame et de rétention de sauvegarde pour vos volumes StorSimple. Elle décrit également comment toocomplete une sauvegarde manuelle.

Lorsque vous sauvegardez un volume, vous pouvez choisir toocreate un instantané local ou un instantané cloud. Si vous sauvegardez un volume épinglé localement, nous vous recommandons de spécifier un instantané cloud. Le fait de prendre un grand nombre d'instantanés locaux d’un volume épinglé localement associé à un jeu de données qui possède une attrition élevée entraîne une situation dans laquelle vous pourriez rapidement manquer d'espace local. Si vous choisissez tootake instantanés locaux, nous vous recommandons que vous occupent moins tooback instantanés quotidiens de l’état le plus récent hello, les conservez pendant un jour, puis supprimez.

Lorsque vous prenez un instantané cloud d’un volume attaché localement, vous copiez uniquement hello modifié données toohello dans le cloud, où il est dédupliqué et compressé.

## <a name="hello-backup-policy-blade"></a>panneau Hello de la stratégie de sauvegarde

Hello **stratégie de sauvegarde** Panneau de votre appareil StorSimple vous permet de toomanage les stratégies de sauvegarde et planification local et les instantanés cloud. Stratégies de sauvegarde sont tooconfigure utilisé les planifications de sauvegarde et de rétention des sauvegardes pour un ensemble de volumes. Stratégies de sauvegarde permettent de tootake un instantané de plusieurs volumes simultanément. Cela signifie que les sauvegardes de hello créées par une stratégie de sauvegarde sera copies cohérentes en cas d’incident.

Liste tabulaire des stratégies de sauvegarde de Hello permet également de vous toofilter hello stratégies de sauvegarde existantes par un ou plusieurs des hello champs qui suivent :

* **Nom de la stratégie** : hello nom associé à la stratégie de hello. Hello différents types de stratégies sont les suivantes :

  * Stratégies planifiées, créées explicitement par l’utilisateur de hello.
  * Stratégies importées, initialement créées dans hello Gestionnaire d’instantanés StorSimple. Ils ont une balise qui décrit l’hôte de gestionnaire d’instantanés StorSimple de hello stratégies de hello ont été importées à partir de.

  > [!NOTE]
  > Stratégies de sauvegarde automatique ou par défaut ne sont plus activés lors de la création du volume hello.

* **Dernière sauvegarde réussie** : hello date et heure de hello dernière sauvegarde réussie qui a été effectuée avec cette stratégie.

* **Sauvegarde suivante** : hello date et heure de hello la prochaine sauvegarde planifiée qui sera initiée par cette stratégie.

* **Volumes** – hello volumes associés à la stratégie de hello. Tous les volumes de hello sont associés à une stratégie de sauvegarde sont regroupés ensemble lorsque les sauvegardes sont créées.

* **Planifications** – hello nombre de planifications associées à stratégie de sauvegarde hello.

opérations Hello plus fréquemment que vous pouvez effectuer pour les stratégies de sauvegarde sont :

* Ajout d’une stratégie de sauvegarde
* Ajouter ou modifier une planification
* Ajouter ou supprimer un volume
* Supprimer une stratégie de sauvegarde
* Exécuter une sauvegarde manuelle

## <a name="add-a-backup-policy"></a>Ajout d’une stratégie de sauvegarde

Ajouter une planification de tooautomatically de stratégie de sauvegarde de vos sauvegardes. Lorsque vous créez un volume, aucune stratégie de sauvegarde par défaut n’est associée à votre volume. Vous devez tooadd et affectez un stratégie de sauvegarde tooprotect volume de données.

Effectuer hello Bonjour tooadd portail Azure pour votre appareil StorSimple une stratégie de sauvegarde comme suit. Après avoir ajouté la stratégie de hello, vous pouvez définir une planification (consultez [ajouter ou modifier une planification](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Ajouter ou modifier une planification

Vous pouvez ajouter ou modifier une planification qui est attaché tooan stratégie de sauvegarde existant sur votre appareil StorSimple. Effectuer hello comme suit dans hello tooadd portail Azure ou modifier une planification.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Ajouter ou supprimer un volume

Vous pouvez ajouter ou supprimer un volume stratégie de sauvegarde tooa sur votre appareil StorSimple. Effectuer hello comme suit dans hello tooadd portail Azure ou supprimer un volume.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Supprimer une stratégie de sauvegarde

Effectuer hello suivant les étapes décrites dans hello toodelete portail Azure une stratégie de sauvegarde sur votre appareil StorSimple.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Exécuter une sauvegarde manuelle

Effectuer hello comme suit dans la sauvegarde (manuel) de hello toocreate portail Azure une demande pour un volume unique.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

