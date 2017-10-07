---
title: "contrôleurs de périphérique aaaManage StorSimple 8000 series | Documents Microsoft"
description: "Découvrez comment toostop, redémarrer, arrêter ou réinitialiser vos contrôleurs d’appareil StorSimple."
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
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gestion de vos contrôleurs d’appareil StorSimple

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit hello différentes opérations qui peuvent être effectuées sur vos contrôleurs d’appareil StorSimple. les contrôleurs de Hello dans votre appareil StorSimple sont des contrôleurs redondants (homologues) dans une configuration actif / passif. À un moment donné, un seul contrôleur est actif et traite toutes les opérations de disque et réseau hello. Hello autre contrôleur est en mode passif. Si le contrôleur actif de hello échoue, contrôleur passif de hello devient automatiquement actif.

Ce didacticiel inclut des contrôleurs de périphérique de hello toomanage obtenir des instructions à l’aide de la :

* **Contrôleurs** panneau pour votre appareil dans hello service du Gestionnaire de périphériques StorSimple.
* Windows PowerShell pour StorSimple

Nous vous recommandons de gérer les contrôleurs de périphérique hello via le service de gestionnaire de périphériques StorSimple hello. Si une action peut uniquement être effectuée à l’aide de Windows PowerShell pour StorSimple, didacticiel de hello rend une note.

Après avoir lu ce didacticiel, vous pourrez :

* redémarrer ou arrêter un contrôleur d’appareil StorSimple
* arrêter un appareil StorSimple
* Réinitialiser votre toofactory de périphérique StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Redémarrage ou arrêt d’un contrôleur unique
Le redémarrage ou l’arrêt d’un contrôleur n’est pas nécessaire si le système fonctionne normalement. Les opérations d’arrêt d’un contrôleur d’appareil unique ne sont courantes que lorsqu’un composant matériel de l’appareil est défaillant et qu’il doit être remplacé. Le redémarrage d’un contrôleur peut également être nécessaire lorsque les performances sont affectées par une utilisation excessive de la mémoire ou un dysfonctionnement du contrôleur. Vous devez également toorestart un contrôleur après un remplacement de contrôleur réussi, si vous souhaitez tooenable hello remplacé contrôleur de test.

Le redémarrage d’un périphérique n’est pas initiateurs tooconnected interruption de service, en supposant que le contrôleur passif de hello est disponible. Si un contrôleur passif n’est pas disponible ou mis hors tension, puis en redémarrant hello actif contrôleur peut entraîner une interruption de service et les temps morts hello.

> [!IMPORTANT]
> * **Un contrôleur en cours d’exécution ne doit jamais être physiquement supprimé, car cela entraînerait une perte de redondance et une augmentation des risques d’interruption.**
> * Hello procédure suivante s’applique uniquement toohello appareil physique StorSimple. Pour plus d’informations sur comment toostart, arrêt et redémarrage hello StorSimple Appliance du Cloud, consultez [fonctionne avec le matériel de cloud hello](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

Vous pouvez redémarrer ou arrêter un contrôleur de périphérique unique via hello Azure portal de service du Gestionnaire de périphériques StorSimple hello ou Windows PowerShell pour StorSimple.

effectuer des contrôleurs d’appareil à partir de hello portail Azure, toomanage hello comme suit.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart ou arrêter un contrôleur dans le portail Azure
1. Dans votre service StorSimple le Gestionnaire de périphériques, accédez trop**périphériques**. Sélectionnez votre appareil dans la liste des appareils hello. 

    ![Choisir un appareil](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Accédez trop**Paramètres > contrôleurs**.
   
    ![Vérifiez que les contrôleurs d’appareil StorSimple sont en bon état de fonctionnement](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. Bonjour **contrôleurs** panneau, vérifiez que hello de deux contrôleurs hello sur votre appareil sont **sain**. Sélectionnez un contrôleur, cliquez dessus avec le bouton droit, puis sélectionnez **Redémarrer** ou **Arrêter**.

    ![Sélectionner Redémarrer ou Arrêter des contrôleurs d’appareil StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Un travail est créé toorestart ou arrêter le contrôleur de hello et vous sont présentées avec des avertissements applicables, le cas échéant. toomonitor hello redémarrage ou arrêt, passez trop**Service > journal d’activité de** , puis filtrez par service tooyour spécifiques de paramètres. Si un contrôleur a été arrêté, vous devez toopush hello power bouton tooturn sur hello contrôleur tooturn sur.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart ou arrêter un contrôleur dans Windows PowerShell pour StorSimple
Effectuer hello suivant les étapes tooshut vers le bas ou redémarrer un contrôleur unique sur votre appareil StorSimple à partir de hello Windows PowerShell pour StorSimple.

1. Périphérique de hello accès via la console série de hello ou d’une session telnet à partir d’un ordinateur distant. tooconnect tooController 0 ou 1, suivez les étapes de hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.
3. Dans le message de bannière hello, prenez note de contrôleur hello que vous êtes connecté trop (contrôleur 0 ou 1) et qu’il soit hello active ou contrôleur (de secours) passif de hello.
   
   * tooshut vers le bas un seul contrôleur, à l’invite de hello, tapez :
     
       `Stop-HcsController`
     
       Cette opération arrête contrôleur hello que vous êtes connecté. Si vous arrêtez le contrôleur actif de hello, hello périphérique tombe en panne sur le contrôleur passif de toohello.

   * toorestart un contrôleur, à l’invite de hello, tapez :
     
       `Restart-HcsController`
     
       Cette action redémarre le contrôleur hello que vous êtes connecté. Si vous redémarrez le contrôleur actif de hello, il bascule contrôleur passif de toohello avant de redémarrer la hello.

## <a name="shut-down-a-storsimple-device"></a>arrêter un appareil StorSimple

Cette section explique comment tooshut vers le bas en cours d’exécution ou d’un appareil StorSimple a échoué à partir d’un ordinateur distant. Un périphérique est désactivé une fois que les deux contrôleurs de périphérique hello sont arrêtés. Un arrêt de l’appareil est effectué lors de l’appareil de hello est déplacée ou est mis hors service.

> [!IMPORTANT]
> Avant d’arrêter l’appareil de hello, vérifier l’intégrité de hello de composants de l’appareil hello. Accédez tooyour appareil, puis **Paramètres > intégrité du matériel**. Bonjour **contrôle d’intégrité de l’état et le matériel** panneau, vérifiez que hello LED de tous les composants de hello sont verts. Un appareil en bon état de fonctionnement a un état vert. Si votre appareil est arrêt tooreplace un composant défectueux, vous verrez un échec (rouge) ou un état détérioré (jaune) pour hello ou les composants respectifs.


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut vers le bas un appareil StorSimple

1. Hello d’utilisation [redémarrer ou arrêter un contrôleur de](#restart-or-shut-down-a-single-controller) tooidentify de procédure et arrêter le contrôleur passif de hello sur votre appareil. Vous pouvez effectuer cette opération dans hello portail Azure ou dans Windows PowerShell pour StorSimple.
2. Répétez hello ci-dessus tooshut étape vers le bas du contrôleur actif de hello.
3. Vous devez maintenant examiner hello arrière plan du périphérique de hello. Une fois que les deux contrôleurs de hello complètement arrêtés, hello DEL d’état sur les deux contrôleurs hello clignotent en rouge. Si vous devez tooturn hors tension de l’appareil de hello complètement à ce stade, les interrupteurs d’alimentation de la rotation hello sur les deux Modules de refroidissement (PCM) toohello OFF position. Ceci doit désactiver le dispositif de hello.

## <a name="reset-hello-device-toofactory-default-settings"></a>Rétablir les paramètres par défaut de hello appareil toofactory

> [!IMPORTANT]
> Si vous devez tooreset les paramètres par défaut des appareils toofactory, contactez le Support Microsoft. procédure Hello décrite ci-dessous doit être utilisé qu’en association avec le Support technique de Microsoft.

Cette procédure décrit comment tooreset vos paramètres de valeur par défaut de Microsoft Azure StorSimple périphérique toofactory à l’aide de Windows PowerShell pour StorSimple.
Réinitialiser un appareil supprime toutes les données et les paramètres à partir de l’ensemble du cluster hello par défaut.

Effectuez hello suivant les étapes tooreset vos paramètres par défaut de Microsoft Azure StorSimple périphérique toofactory :

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault paramètres de périphérique dans Windows PowerShell pour StorSimple
1. Périphérique de hello accès via sa console série. Vérifiez tooensure de message de bannière hello que vous êtes connecté toohello **Active** contrôleur.
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.
3. À l’invite de hello, tapez Bonjour suivant commande tooreset hello ensemble du cluster, la suppression de tous les paramètres de contrôleur, les métadonnées et les données :
   
    `Reset-HcsFactoryDefault`
   
    tooinstead réinitialiser un seul contrôleur, utilisez hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) applet de commande avec hello `-scope` paramètre.)
   
    système de Hello va redémarrer plusieurs fois. Vous serez averti lorsque hello réinitialisation est terminée. Selon le modèle de système de hello, il peut prendre 45 à 60 minutes pour un appareil 8100 et 60 à 90 minutes pour un toofinish 8600 ce processus.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Questions et réponses sur la gestion des contrôleurs d’appareil
Dans cette section, nous avons résumé des hello questions fréquemment posées concernant la gestion des contrôleurs de périphérique StorSimple.

**Q.** Que se passe-t-il si les deux hello contrôleurs sur mon appareil sont sain et activé sur et redémarrer ou arrêter le contrôleur actif de hello ?

**A.** Si les deux contrôleurs hello sur votre appareil sont sains et activés, vous êtes invité à confirmer l’opération. Vous pouvez choisir de :

* **Redémarrez le contrôleur actif de hello** : vous êtes informé que le redémarrage d’un contrôleur actif a provoqué hello appareil toofail sur le contrôleur passif de toohello. Hello contrôleur redémarre.
* **Arrêter un contrôleur actif** : un message vous avertit que l’arrêt d’un contrôleur actif entraîne une coupure du service. Vous devez également le bouton d’alimentation hello toopush sur tooturn de périphérique hello sur le contrôleur de hello.

**Q.** Que se passe-t-il si le contrôleur passif hello mon appareil est indisponible ou désactivé off et que je redémarre ou arrête contrôleur actif de hello ?

**A.** Si le contrôleur passif de hello sur votre appareil est indisponible ou désactivé et vous choisissez de :

* **Redémarrez le contrôleur actif de hello** : vous êtes informé que la poursuite de l’opération de hello entraîne une interruption temporaire du service de hello, et vous êtes invité à confirmer l’opération.
* **Arrêter un contrôleur actif** : vous êtes informé qu’opération hello continue entraîne des temps d’arrêt. Vous devez également le bouton d’alimentation hello toopush sur un ou deux tooturn contrôleurs sur l’appareil de hello. Vous êtes invité à confirmer l’opération.

**Q.** Lorsque ne hello contrôleur redémarrage ou l’arrêt a échoué tooprogress ?

**A.** Le redémarrage ou l’arrêt d’un contrôleur peut échouer si :

* Une mise à jour de l’appareil est en cours.
* Le redémarrage d’un contrôleur est déjà en cours.
* L’arrêt d’un contrôleur est déjà en cours.

**Q.** Comment pouvez-vous déterminer si un contrôleur a été redémarré ou arrêté ?

**A.** Vous pouvez vérifier l’état du contrôleur hello sur le panneau de contrôleur. état du contrôleur Hello indique si un contrôleur est en cours de hello de redémarrer ou arrêter. En outre, hello **alertes** panneau contiennent une alerte d’information si le contrôleur de hello est redémarré ou arrêté. opérations de redémarrage et d’arrêt du contrôleur Hello sont également enregistrées dans les journaux de l’activité Receive hello. Pour plus d’informations sur les journaux de l’activité Receive, accédez trop[afficher les journaux d’activité hello](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**Q.** Existe-t-il des toohello impact d’e/s en raison du basculement du contrôleur ?

**A.** les connexions TCP Hello entre les initiateurs et le contrôleur actif sont réinitialisées suite au basculement du contrôleur, mais rétablies lorsque le contrôleur passif de hello suppose que l’opération. Il peut exister une pause temporaire (moins de 30 secondes) dans l’activité d’e/s entre les initiateurs et les appareils hello hello pendant cette opération.

**Q.** Comment retourner mon tooservice contrôleur une fois qu’il a été arrêté et supprimé ?

**A.** tooreturn un tooservice de contrôleur, vous devez l’insérer dans le châssis de hello comme décrit dans [remplacer un module de contrôleur sur votre appareil StorSimple](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Étapes suivantes
* Si vous rencontrez des problèmes avec vos contrôleurs d’appareil StorSimple que vous ne pouvez pas résoudre à l’aide de procédures hello répertoriées dans ce didacticiel, [contactez le Support Microsoft](storsimple-8000-contact-microsoft-support.md).
* toolearn plus sur l’utilisation de service du Gestionnaire de périphériques StorSimple hello, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

