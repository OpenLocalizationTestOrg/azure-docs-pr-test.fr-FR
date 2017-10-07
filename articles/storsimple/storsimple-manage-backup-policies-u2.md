---
title: "aaaManage vos stratégies de sauvegarde StorSimple | Documents Microsoft"
description: "Explique comment vous pouvez utiliser toocreate de service StorSimple Manager hello et gérer des sauvegardes manuelles, des planifications de sauvegarde et la rétention de sauvegarde."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a>Utilisez hello StorSimple Manager service toomanage stratégies de sauvegarde (Update 2)
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment toouse hello service StorSimple Manager **les stratégies de sauvegarde** page toocontrol les processus de sauvegarde et de rétention de sauvegarde pour vos volumes StorSimple. Elle décrit également comment toocomplete une sauvegarde manuelle.

Lorsque vous sauvegardez un volume, vous pouvez choisir toocreate un instantané local ou un instantané cloud. Si vous sauvegardez un volume épinglé localement, nous vous recommandons de spécifier un instantané cloud. Le fait de prendre un grand nombre d'instantanés locaux d’un volume épinglé localement associé à un jeu de données qui possède une attrition élevée entraîne une situation dans laquelle vous pourriez rapidement manquer d'espace local. Si vous choisissez tootake instantanés locaux, nous vous recommandons que vous occupent moins tooback instantanés quotidiens de l’état le plus récent hello, les conservez pendant un jour, puis supprimez.

Lorsque vous prenez un instantané cloud d’un volume attaché localement, vous copiez uniquement hello modifié données toohello dans le cloud, où il est dédupliqué et compressé. 

## <a name="hello-backup-policies-page"></a>page de stratégies de sauvegarde Hello
Hello **les stratégies de sauvegarde** page vous permet de toomanage les stratégies de sauvegarde et planification local et les instantanés cloud. (Les stratégies de sauvegarde sont tooconfigure utilisé les planifications de sauvegarde et de rétention de sauvegarde pour une collection de volumes). Stratégies de sauvegarde permettent de tootake un instantané de plusieurs volumes simultanément. Cela signifie que les sauvegardes de hello créées par une stratégie de sauvegarde sera copies cohérentes en cas d’incident. Hello **les stratégies de sauvegarde** page répertorie les stratégies de sauvegarde hello, leurs types, les volumes de hello associé, le nombre de hello de sauvegardes conservées, et hello option tooenable ces stratégies.

Hello **les stratégies de sauvegarde** page vous permet également de toofilter hello stratégies de sauvegarde existantes par un ou plusieurs des hello champs qui suivent :

* **Nom de la stratégie** : hello nom associé à la stratégie de hello. Hello différents types de stratégies sont les suivantes :
  
  * Stratégies planifiées, créées explicitement par l’utilisateur de hello.
  * Stratégies automatiques, qui sont créés lors de la sauvegarde par défaut de hello pour cette option de volume a été activée lors de la création du volume hello. Ces stratégies sont nommées *NomVolume*_Default où *NomVolume* fait référence nom toohello Hello volume StorSimple configuré par l’utilisateur hello Bonjour portail Azure classic. Hello les stratégies automatiques génèrent des instantanés cloud quotidiens commençant à l’heure de l’appareil 22:30.
  * Stratégies importées, initialement créées dans hello Gestionnaire d’instantanés StorSimple. Ils ont une balise qui décrit l’hôte de gestionnaire d’instantanés StorSimple de hello stratégies de hello ont été importées à partir de.
* **Volumes** – hello volumes associés à la stratégie de hello. Tous les volumes de hello sont associés à une stratégie de sauvegarde sont regroupés ensemble lorsque les sauvegardes sont créées.
* **Dernière sauvegarde réussie** : hello date et heure de hello dernière sauvegarde réussie qui a été effectuée avec cette stratégie.
* **Sauvegarde suivante** : hello date et heure de hello la prochaine sauvegarde planifiée qui sera initiée par cette stratégie.
* **Planifications** – hello nombre de planifications associées à stratégie de sauvegarde hello.

opérations Hello plus fréquemment que vous pouvez effectuer à partir de cette page sont :

* Ajout d’une stratégie de sauvegarde 
* Ajouter ou modifier une planification 
* Supprimer une stratégie de sauvegarde 
* Exécuter une sauvegarde manuelle 
* Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications 

## <a name="add-a-backup-policy"></a>Ajout d’une stratégie de sauvegarde
Ajouter une planification de tooautomatically de stratégie de sauvegarde de vos sauvegardes. Effectuer hello Bonjour tooadd portail classique Azure une stratégie de sauvegarde de votre appareil StorSimple comme suit. Après avoir ajouté la stratégie de hello, vous pouvez définir une planification (consultez [ajouter ou modifier une planification](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

![Vidéo disponible](./media/storsimple-manage-backup-policies-u2/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment toocreate local ou cloud de sauvegarde stratégie, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Ajouter ou modifier une planification
Vous pouvez ajouter ou modifier une planification qui est attaché tooan stratégie de sauvegarde existant sur votre appareil StorSimple. Effectuer hello Bonjour tooadd de portail classique Azure comme suit ou modifier une planification.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a>Supprimer une stratégie de sauvegarde
Effectuer hello suivant les étapes décrites dans hello toodelete portail classique Azure une stratégie de sauvegarde sur votre appareil StorSimple.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Exécuter une sauvegarde manuelle
Effectuer hello comme suit dans la sauvegarde (manuel) de hello toocreate portail classique Azure une demande pour un volume unique.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Créer une stratégie de sauvegarde personnalisée comportant plusieurs volumes et planifications
Effectuer hello Bonjour toocreate portail classique Azure une stratégie de sauvegarde personnalisée qui a plusieurs volumes et planifications, comme suit.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

