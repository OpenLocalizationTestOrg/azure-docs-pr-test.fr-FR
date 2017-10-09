---
title: "basculement aaaStorSimple, récupération d’urgence pour les appareils 8000 series | Documents Microsoft"
description: "Découvrez comment toofail sur votre toohello de périphérique StorSimple même appareil."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Basculer votre unité toosame du périphérique physique StorSimple

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit toofail requis de hello étapes sur un tooitself de périphérique physique StorSimple 8000 series s’il existe un reprise après sinistre. StorSimple utilise des données hello périphérique basculement fonctionnalité toomigrate à partir d’un périphérique physique source dans l’unité physique du tooanother hello centre de données. instructions de Hello dans ce didacticiel s’appliquent à des périphériques physiques série tooStorSimple 8000 exécutant des versions de logiciel mise à jour 3 et versions ultérieures.

toolearn en savoir plus sur le basculement de l’appareil et comment il est utilisé toorecover d’urgence, consultez trop[basculement et récupération d’urgence pour les unités StorSimple 8000 series](storsimple-8000-device-failover-disaster-recovery.md).

toofail sur un périphérique physique tooanother du périphérique physique, allez trop[basculer toohello même appareil physique StorSimple](storsimple-8000-device-failover-physical-device.md). toofail sur un tooa de périphérique physique StorSimple StorSimple Appliance du Cloud, passez trop[basculer tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Composants requis

- Vérifiez que vous avez consulté les considérations hello pour le basculement de l’appareil. Pour plus d’informations, consultez trop[considérations courantes pour le basculement de l’appareil](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Toofail étapes sur toohello même appareil

Effectuer hello comme suit si vous avez besoin de toofail sur toohello même appareil.

1. Prendre des instantanés de cloud de tous les volumes hello dans votre appareil. Pour plus d’informations, consultez trop[sauvegardes toocreate du service Gestionnaire de périphériques StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Réinitialiser votre toofactory d’appareil. Suivez hello des instructions dans [comment tooreset un toofactory de périphérique StorSimple les paramètres par défaut](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Atteindre le service du Gestionnaire de périphériques StorSimple toohello, puis sélectionnez **périphériques**. Bonjour **périphériques** panneau, l’ancien périphérique de hello doit apparaître comme étant **hors connexion**.

    ![Appareil source hors connexion](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Configurez votre appareil et réinscrivez-le auprès de votre service StorSimple Device Manager. Hello appareil nouvellement inscrit doit apparaître comme étant **prêt tooset des**. nom du périphérique pour le nouveau périphérique de hello Hello est hello identique à celle de l’ancien périphérique de hello ajouté, mais avec un chiffre tooindicate cet appareil hello était par défaut de réinitialisation toofactory et inscrite à nouveau.

    ![APPAREIL nouvellement inscrit de prêt tooset des](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Nouvelle unité de hello, terminez l’installation de périphérique hello. Pour plus d’informations, consultez trop[étape 4 : exécuter le programme d’installation minimale de l’appareil](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). Sur hello **périphériques** panneau, hello du périphérique de hello devient trop**Online**.

   > [!IMPORTANT]
   > **Effectuer la configuration minimale hello en premier, ou la récupération d’urgence peut échouer.**

    ![Appareil nouvellement inscrit en ligne](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Sélectionnez périphérique ancien de hello (état hors connexion) et à partir de la barre de commandes hello, cliquez sur **basculer**. Bonjour **basculer** panneau, sélectionnez l’ancien périphérique en tant que source de hello et spécifiez un appareil cible de hello comme hello les appareil nouvellement inscrit.

    ![Synthèse du basculement](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Pour obtenir des instructions détaillées, voir la rubrique trop[basculer sur un périphérique physique de tooanother](#fail-over-to-another-physical-device).

7. Un travail de restauration du périphérique est créé que vous pouvez surveiller de hello **travaux** panneau.

8. Une fois le travail de hello terminé, accéder au nouveau périphérique de hello et accédez toohello **conteneurs de volumes** panneau. Vérifiez que tous les conteneurs de volumes hello à partir de l’ancien périphérique de hello ont été migrés toohello nouveau périphérique.

   ![Conteneurs de volumes migrés](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Une fois le basculement de hello terminée, vous pouvez désactiver et supprimer l’ancien périphérique de hello à partir du portail de hello. Sélectionnez hello ancien périphérique (hors connexion), avec le bouton droit, puis **Deactivate**. Une fois que l’appareil de hello est désactivé, état hello du périphérique de hello est mise à jour.

     ![Appareil source désactivé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Sélectionnez hello désactivé le périphérique, avec le bouton droit et sélectionnez **supprimer**. Cette opération supprime les appareils hello à partir de la liste des appareils hello.

    ![Appareil source supprimé](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Étapes suivantes

* Une fois que vous avez effectué un basculement, vous devrez peut-être trop[désactiver ou supprimer votre appareil StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Pour plus d’informations sur la façon dont toouse hello StorSimple le Gestionnaire de périphériques de service, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

