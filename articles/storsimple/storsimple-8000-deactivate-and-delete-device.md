---
title: "aaaDeactivate et supprimer une unité de la série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment l’appareil StorSimple tooremove service en désactiver tout d’abord, puis leur suppression."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Désactiver et supprimer un appareil StorSimple

## <a name="overview"></a>Vue d'ensemble

Cet article décrit comment toodeactivate et supprimer une unité de StorSimple qui est connecté tooa service du Gestionnaire de périphériques StorSimple. conseils Hello dans cet article s’applique uniquement les appareils 8000 series tooStorSimple, y compris les équipements de Cloud hello StorSimple. Si vous utilisez un tableau virtuel StorSimple, puis passez trop[désactiver et supprimer un tableau virtuel StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Désactivation interrompt la connexion hello entre l’appareil de hello et le service de gestionnaire de périphériques StorSimple hello correspondant. Vous souhaiterez peut-être tootake un appareil StorSimple hors service (par exemple, si vous remplacez ou la mise à niveau de votre appareil ou si vous n’utilisez plus StorSimple). Dans ce cas, vous avez besoin toodeactivate hello périphérique avant de pouvoir le supprimer.

Lorsque vous désactivez un périphérique, toutes les données stockées localement sur l’appareil de hello ne sont plus accessibles. Uniquement les données de hello associées hello périphérique qui a été enregistrée dans le cloud de hello peuvent être récupérées.

> [!WARNING]
> La désactivation est une opération DÉFINITIVE et ne peut pas être annulée. Impossible d’inscrire un appareil désactivé avec hello service du Gestionnaire de périphériques StorSimple sauf s’il est de rétablir les valeurs par défaut toofactory.
>
> Hello réinitialisation processus supprime toutes les données hello qui a été stockées localement sur votre appareil. Par conséquent, vous devez impérativement prendre un instantané cloud de toutes vos données avant de désactiver un appareil. Cet instantané cloud vous permet de toorecover tous hello des données à un stade ultérieur.

Après avoir lu ce didacticiel, vous pourrez :

* Désactiver un appareil et supprimer des données de hello.
* Désactiver un appareil et conserver les données de hello.

> [!NOTE]
> Avant de désactiver un appareil physique ou une appliance cloud StorSimple, arrêtez ou supprimez les clients et les hôtes qui en dépendent.


## <a name="deactivate-and-delete-data"></a>Désactiver et supprimer des données

Si vous souhaitez supprimer complètement de périphérique de hello et que vous ne souhaitez pas que les données de salutation tooretain sur l’appareil de hello, puis terminez hello comme suit.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello dispositif et supprimer les données de salutation

1. Avant de désactiver un périphérique, vous devez supprimer tous les hello volume conteneurs (et les volumes hello) associé au périphérique de hello. Vous pouvez supprimer des conteneurs de volumes uniquement après avoir supprimé les sauvegardes hello associé.

    > [!NOTE]
    > Avant de désactiver un appareil physique StorSimple ou un dispositif de cloud, vous assurer que les données de salutation à partir du conteneur de volume hello supprimé sont réellement supprimées à partir de l’appareil de hello. Vous pouvez analyser les graphiques de consommation de cloud hello et lorsque vous voyez l’utilisation du cloud hello supprimer en raison de sauvegardes hello, vous avez supprimé, vous pouvez passer appareil de hello toodeactivate. Si vous désactivez le périphérique hello avant cette liste se produit, hello sont inutilisées hello compte de stockage de données et alloue des frais.

2. Désactiver le dispositif de hello comme suit :
   
   1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Bonjour **périphériques** panneau, appareil hello select que vous souhaitez toodeactivate, avec le bouton droit, puis cliquez sur **Deactivate**.

        ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Bonjour **Deactivate** panneau, tooconfirm de nom de périphérique hello puis tapez **Deactivate**. Hello désactiver le processus démarre et prend quelques minutes toocomplete.

        ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Après la désactivation, vous pouvez supprimer complètement le périphérique de hello. Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service. service de Hello puis ne peut plus gérer les appareils hello supprimé. Utilisez hello suivant l’appareil de hello toodelete comme suit :
   
   1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Bonjour **périphériques** panneau, appareil hello sélectionnez désactivée que vous souhaitez toodelete, avec le bouton droit, puis cliquez sur **supprimer**.

        ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Bonjour **supprimer** panneau, tooconfirm de nom de périphérique hello puis tapez **supprimer**. suppression de Hello prend quelques minutes toocomplete.

        ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Après que la suppression de hello est correctement terminée, vous êtes averti. liste des appareils Hello met également à jour la suppression de hello tooreflect.

## <a name="deactivate-and-retain-data"></a>Désactiver et conserver des données

Si vous intéressent supprimer hello appareil mais les données de salutation tooretain, puis terminez hello comme suit :

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate un appareil et conserver les données de hello
1. Désactiver le dispositif de hello. Tous les hello conteneurs de volumes et instantanés hello du périphérique de hello demeurent.
   
   1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Bonjour **périphériques** panneau, appareil hello select que vous souhaitez toodeactivate, avec le bouton droit, puis cliquez sur **Deactivate**.

         ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. Bonjour **Deactivate** panneau, tooconfirm de nom de périphérique hello puis tapez **Deactivate**. Hello désactiver le processus démarre et prend quelques minutes toocomplete.

         ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. Vous pouvez maintenant basculer les conteneurs de volumes hello et les instantanés de hello associé. Pour les procédures, passez trop[basculement et récupération d’urgence pour votre appareil StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Après la désactivation et de basculement, vous pouvez supprimer les périphériques hello complètement. Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service. service de Hello puis ne peut plus gérer les appareils hello supprimé. périphérique de hello toodelete, hello complète comme suit :
   
   1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Bonjour **périphériques** panneau, appareil hello sélectionnez désactivée que vous souhaitez toodelete, avec le bouton droit, puis cliquez sur **supprimer**.

       ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. Bonjour **supprimer** panneau, tooconfirm de nom de périphérique hello puis tapez **supprimer**. suppression de Hello prend quelques minutes toocomplete.

       ![Désactiver l’appareil StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Après que la suppression de hello est correctement terminée, vous êtes averti. liste des appareils Hello met également à jour la suppression de hello tooreflect.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Désactiver et supprimer une appliance cloud

Pour un dispositif de Cloud StorSimple, désactivation à partir du portail de hello désalloue et supprime des machines virtuelles de hello et ressources hello créés lors de sa préparation. Une fois que le matériel de cloud hello est désactivé, il ne peut pas être restauré tooits l’état précédent.

![Désactiver une instance StorSimple Cloud Appliance](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

Résultats de la désactivation Bonjour suivant des actions :

* Hello StorSimple Appliance de Cloud est supprimé du service de hello.
* machine virtuelle Hello hello StorSimple Appliance de Cloud est supprimé.
* disque de système d’exploitation Hello et des disques de données créés pour hello équipement de Cloud StorSimple sont supprimés.
* service de Hello hébergé et le réseau virtuel qui ont été créés lors de la configuration sont conservés. Si vous n’utilisez pas ces entités, vous devez les supprimer manuellement.
* Les instantanés cloud créés par hello StorSimple Appliance de Cloud sont conservés.

Une fois que le matériel de cloud hello est désactivée, vous pouvez le supprimer à partir de la liste des appareils hello. Sélectionnez hello désactivé le périphérique, avec le bouton droit, puis cliquez sur **supprimer**. StorSimple vous avertit une fois que les appareils hello sont supprimé et hello la liste des mises à jour des appareils.

## <a name="next-steps"></a>Étapes suivantes

* toorestore hello des valeurs par défaut de toofactory appareil désactivé, accédez trop[rétablir les paramètres par défaut de hello appareil toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Pour obtenir une assistance technique, [contactez le support technique de Microsoft](storsimple-8000-contact-microsoft-support.md).
* toolearn savoir plus sur comment toouse hello service du Gestionnaire de périphériques StorSimple, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

