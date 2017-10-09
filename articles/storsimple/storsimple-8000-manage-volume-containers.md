---
title: "aaaManage vos conteneurs de volumes StorSimple sur l’appareil de série StorSimple 8000 de hello | Documents Microsoft"
description: "Explique comment vous pouvez utiliser hello le Gestionnaire de périphériques StorSimple conteneurs de volumes service page tooadd, modifier ou supprimer un conteneur de volume."
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
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Utiliser des conteneurs de volumes StorSimple hello le Gestionnaire de périphériques StorSimple service toomanage

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gérer des conteneurs de volumes StorSimple.

Un conteneur de volumes créé dans un appareil Microsoft Azure StorSimple contient un ou plusieurs volumes hébergeant les paramètres de consommation du compte de stockage, du chiffrement et de la bande passante. Un appareil peut comporter plusieurs conteneurs de volumes pour l’ensemble de ses volumes. 

Un conteneur de volumes a hello suivant d’attributs :

* **Volumes** – hello à plusieurs niveaux ou attaché localement des volumes StorSimple qui sont contenus dans le conteneur de volume hello. 
* **Chiffrement** : clé de chiffrement pouvant être définie pour chaque conteneur de volumes. Cette clé est utilisée pour chiffrer les données de hello sont envoyées à partir de votre cloud toohello du périphérique StorSimple. Une clé de niveau militaire AES-256 bits est utilisée avec la clé de hello entré par l’utilisateur. toosecure vos données, nous vous recommandons de toujours activer le chiffrement de stockage cloud.
* **Compte de stockage** : hello compte de stockage Azure qui sont des données hello toostore utilisé. Tous les volumes de hello résidant dans un conteneur de volume partagent ce compte de stockage. Vous pouvez choisir un compte de stockage à partir d’une liste existante ou créer un nouveau compte lorsque vous créez le conteneur de volume hello puis spécifiez les informations d’identification hello pour ce compte.
* **Bande passante cloud** – hello la bande passante consommée par les appareils hello lorsque hello de données à partir de l’appareil de hello envoyée toohello cloud. Vous pouvez appliquer un contrôle de bande passante en définissant une valeur comprise entre 1 et 1 000 Mbits/s lorsque vous créez ce conteneur. Si vous souhaitez hello appareil tooconsume la bande passante disponible, définissez ce champ trop**illimité**. Vous pouvez également créer et appliquer une bande passante tooallocate du modèle de bande passante selon une planification.

Hello procédures suivantes expliquent comment toouse hello StorSimple **conteneurs de volumes** hello toocomplete de panneau opérations communes suivantes :

* Ajouter un conteneur de volumes
* Modifier un conteneur de volumes
* Supprimer un conteneur de volumes

## <a name="add-a-volume-container"></a>Ajouter un conteneur de volumes
Effectuer hello suivant les étapes tooadd un conteneur de volume.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modifier un conteneur de volumes
Effectuer hello suivant les étapes toomodify un conteneur de volume.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Supprimer un conteneur de volumes
Un conteneur de volumes comporte plusieurs volumes. Il peut être supprimé que si tous les volumes hello qu’il contient sont supprimés en premier. Effectuer hello suivant les étapes toodelete un conteneur de volume.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [gestion des volumes StorSimple](storsimple-8000-manage-volumes-u2.md). 
* En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

