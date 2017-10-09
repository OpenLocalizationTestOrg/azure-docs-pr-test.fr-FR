---
title: "basculement aaaStorSimple, appareil physique de série tooa StorSimple 8000 récupération d’urgence | Documents Microsoft"
description: "Découvrez comment toofail sur votre appareil physique StorSimple 8000 series périphérique physique tooanother."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Basculer le périphérique physique de tooa StorSimple 8000 series

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit toofail de hello étapes requis sur un appareil StorSimple 8000 series périphérique physique tooanother StorSimple physique s’il existe un reprise après sinistre. StorSimple utilise des données hello périphérique basculement fonctionnalité toomigrate à partir d’un périphérique physique source dans l’unité physique du tooanother hello centre de données. instructions de Hello dans ce didacticiel s’appliquent à des périphériques physiques série tooStorSimple 8000 exécutant des versions de logiciel mise à jour 3 et versions ultérieures.

toolearn en savoir plus sur le basculement de l’appareil et comment il est utilisé toorecover d’urgence, consultez trop[basculement et récupération d’urgence pour les unités StorSimple 8000 series](storsimple-8000-device-failover-disaster-recovery.md).

toofail sur un tooa de périphérique physique StorSimple StorSimple Appliance du Cloud, passez trop[basculer tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md). toofail sur un périphérique physique tooitself, accédez trop[basculer toohello même appareil physique StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Composants requis

- Vérifiez que vous avez consulté les considérations hello pour le basculement de l’appareil. Pour plus d’informations, consultez trop[considérations courantes pour le basculement de l’appareil](storsimple-8000-device-failover-disaster-recovery.md).

- Vous devez disposer d’un périphérique physique StorSimple 8000 series déployé dans le centre de données hello. Appareil de Hello doit exécuter Update 3 ou version ultérieure du logiciel. Pour plus d’informations, consultez trop[déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Toofail étapes sur l’unité physique de tooa

Effectuer hello suivant les étapes toorestore périphérique tooa cible appareil physique.

1. Vérifiez que hello conteneur de volume toofail sur a associé à des instantanés cloud. Pour plus d’informations, consultez trop[sauvegardes toocreate du service Gestionnaire de périphériques StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Accédez tooyour StorSimple le Gestionnaire de périphériques, puis cliquez sur **périphériques**. Bonjour **périphériques** panneau, accédez toohello la liste des périphériques connectés à votre service.
    ![Sélectionner l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Sélectionnez votre appareil source et cliquez dessus. Appareil de source de Hello dispose des conteneurs de volumes hello que vous souhaitez toofail par. Accédez trop**Paramètres > conteneurs de volumes**.
4. Sélectionnez un conteneur de volumes que vous aimeriez toofail sur tooanother appareil. Cliquez sur hello volume conteneur toodisplay hello liste des volumes de ce conteneur. Sélectionnez un volume, avec le bouton droit, puis cliquez sur **mettre hors connexion** tootake le volume hello hors connexion. Répétez ce processus pour tous les volumes hello dans le conteneur de volume hello.
5. Étape précédente de hello Répétez ces étapes pour tous les hello conteneurs de volumes vous aimeriez toofail sur tooanother appareil.
6. Revenir en arrière toohello **périphériques** panneau. Dans la barre de commandes hello, cliquez sur **basculer**.
    ![Cliquer sur Effectuer un basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. Bonjour **basculer** panneau, effectuer hello comme suit :
   
   1. Cliquez sur **Source**. conteneurs de volumes Hello avec des volumes associés avec des instantanés cloud sont affichés. Uniquement les conteneurs hello affichés sont éligibles pour le basculement. Dans la liste de hello des conteneurs de volumes, sélectionnez vous aimeriez toofail sur les conteneurs de volumes hello. **Hello uniquement les conteneurs de volumes avec des instantanés cloud associés et les volumes hors connexion sont affichés.**

       ![Sélectionner une source](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Cliquez sur **Cible**. Pour les conteneurs de volumes hello sélectionnés à l’étape précédente de hello, sélectionnez un périphérique cible à partir de la liste déroulante de hello de périphériques disponibles. Uniquement hello pour les appareils qui ont des conteneurs de volumes source suffisamment capacité tooaccommodate sont affichent dans la liste de hello.

        ![Sélectionner la cible](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Enfin, passez en revue tous les paramètres de basculement hello sous **Résumé**. Après avoir examiné les paramètres de hello, sélectionnez hello case à cocher indiquant que les volumes hello dans les conteneurs de volumes sélectionnés sont hors connexion. Cliquez sur **OK**.

       ![Passer en revue les paramètres de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple crée un travail de basculement. Cliquez sur hello notification toomonitor hello basculement projet via hello **travaux** panneau.

    Si le conteneur de volume hello ayant basculé possède des volumes locaux, vous consultez des travaux de restauration individuels pour chaque volume local (et non de volumes hiérarchisés) dans le conteneur de hello. Ces travaux de restauration peut prendre un certain toocomplete de temps. Il est probable que ce travail de basculement hello peut terminer plus tôt. Ces volumes aura garanties locales uniquement après que les travaux de restauration hello est terminées.

    ![Surveiller le travail de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Une fois hello basculement terminé, accédez à toohello **périphériques** panneau.
   
   1. Sélectionnez le périphérique hello qui a été utilisé en tant que périphérique cible de hello pour les processus de basculement hello.

       ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Accédez toohello **conteneurs de volumes** panneau. Tous les conteneurs de volume hello, ainsi que les volumes hello à partir de l’ancien périphérique de hello, doivent être répertoriés.

       ![Afficher les conteneurs de volumes cibles](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Étapes suivantes

* Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Pour plus d’informations sur la façon dont toouse hello StorSimple le Gestionnaire de périphériques de service, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

