---
title: "basculement aaaStorSimple, tooa de récupération d’urgence StorSimple Cloud Appliance | Documents Microsoft"
description: "Découvrez le matériel de cloud toofail sur votre tooa de périphérique physique StorSimple 8000 series."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Basculer tooyour StorSimple Appliance de Cloud

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit toofail requis de hello étapes sur un tooa de périphérique physique StorSimple 8000 series StorSimple Appliance de Cloud s’il existe un reprise après sinistre. StorSimple utilise des données hello périphérique basculement fonctionnalité toomigrate à partir d’un périphérique physique source dans le dispositif de cloud hello datacenter tooa s’exécutant dans Azure. conseils Hello dans ce didacticiel s’applique des périphériques physiques tooStorSimple 8000 series et appareils de cloud qui exécutent des versions de logiciel mise à jour 3 et versions ultérieures.

toolearn en savoir plus sur le basculement de l’appareil et comment il est utilisé toorecover d’urgence, consultez trop[basculement et récupération d’urgence pour les unités StorSimple 8000 series](storsimple-8000-device-failover-disaster-recovery.md).

toofail sur un appareil StorSimple appareil physique tooanother physique, allez trop[basculer sur un appareil physique StorSimple de tooa](storsimple-8000-device-failover-physical-device.md). toofail sur un appareil tooitself, accédez trop[basculer toohello même appareil physique StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Composants requis

- Vérifiez que vous avez consulté les considérations hello pour le basculement de l’appareil. Pour plus d’informations, consultez trop[considérations courantes pour le basculement de l’appareil](storsimple-8000-device-failover-disaster-recovery.md).

- Vous devez avoir créé et configuré une StorSimple Cloud Appliance avant d’exécuter cette procédure. Si en cours d’exécution mettre à jour la version du logiciel 3 ou version ultérieure, envisagez d’utiliser un dispositif 8020 cloud pour hello récupération d’urgence. modèle 8020 de Hello a 64 To et utilise le stockage Premium. Pour plus d’informations, consultez trop[déployer et gérer une application de Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Toofail étapes cloud via tooa

Effectuer hello suivant les étapes toorestore hello appareil tooa cible StorSimple Appliance de Cloud.

1.  Vérifiez que hello conteneur de volume toofail sur a associé à des instantanés cloud. Pour plus d’informations, consultez trop[sauvegardes toocreate du service Gestionnaire de périphériques StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Bonjour **périphériques** panneau, accédez toohello la liste des périphériques connectés à votre service.
    ![Sélectionner l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Sélectionnez votre appareil source et cliquez dessus. Appareil de source de Hello dispose des conteneurs de volumes hello que vous souhaitez toofail par. Accédez trop**Paramètres > conteneurs de volumes**.

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Sélectionnez un conteneur de volumes que vous aimeriez toofail sur tooanother appareil. Cliquez sur hello volume conteneur toodisplay hello liste des volumes de ce conteneur. Sélectionnez un volume, avec le bouton droit, puis cliquez sur **mettre hors connexion** tootake le volume hello hors connexion.

    ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Répétez ce processus pour tous les volumes hello dans le conteneur de volume hello.

     ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Étape précédente de hello Répétez ces étapes pour tous les hello conteneurs de volumes vous aimeriez toofail sur tooanother appareil.

7. Revenir en arrière toohello **périphériques** panneau. Dans la barre de commandes hello, cliquez sur **basculer**.

    ![Cliquer sur Effectuer un basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. Bonjour **basculer** panneau, effectuer hello comme suit :
   
    1. Cliquez sur **Source**. Sélectionnez toofail de conteneurs de volume hello sur. **Hello uniquement les conteneurs de volumes avec des instantanés cloud associés et les volumes hors connexion sont affichés.**
        ![Sélectionner une source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Cliquez sur **Cible**. Sélectionnez une cible cloud à partir de la liste déroulante de hello de périphériques disponibles. **Uniquement hello pour les appareils qui ont des conteneurs de volumes source suffisamment capacité tooaccommodate sont affichent dans la liste de hello.**

        ![Sélectionner la cible](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Passez en revue les paramètres de basculement hello sous **Résumé** et sélectionnez la case à cocher de hello indiquant que les volumes hello dans les conteneurs de volumes sélectionnés sont hors connexion. 

        ![Passer en revue les paramètres de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Un travail de basculement est créé. basculement de hello toomonitor des tâches, cliquez sur la notification de travail hello.

    ![Surveiller le travail de basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Une fois que hello basculement terminé, revenez toohello **périphériques** panneau.

    1. Sélectionnez le périphérique hello qui a été utilisé en tant que cible de hello pour le basculement de hello.

       ![Sélectionnez l’appareil](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Cliquez sur **Conteneurs de volumes**. Tous les conteneurs de volume hello, ainsi que les volumes hello à partir de l’ancien périphérique de hello, doivent être répertoriés.

       Si le conteneur de volume hello ayant basculé a attaché localement les volumes, les volumes sont basculés en tant que volumes hiérarchisés. Les volumes épinglés localement ne sont pas pris en charge sur une StorSimple Cloud Appliance.

       ![Afficher les conteneurs de volumes cibles](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Étapes suivantes

* Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Pour plus d’informations sur la façon dont toouse hello StorSimple le Gestionnaire de périphériques de service, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

