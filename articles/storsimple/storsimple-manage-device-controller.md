---
title: "contrôleurs de périphérique StorSimple aaaManage | Documents Microsoft"
description: "Découvrez comment toostop, redémarrer, arrêter ou réinitialiser vos contrôleurs d’appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Gestion de vos contrôleurs d’appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel décrit hello différentes opérations qui peuvent être effectuées sur vos contrôleurs d’appareil StorSimple. les contrôleurs de Hello dans votre appareil StorSimple sont des contrôleurs redondants (homologues) dans une configuration actif / passif. À un moment donné, un seul contrôleur est actif et traite toutes les opérations de disque et réseau hello. Hello autre contrôleur est en mode passif. Si le contrôleur actif de hello échoue, hello contrôleur passif prend automatiquement.

Ce didacticiel inclut des contrôleurs de périphérique de hello toomanage obtenir des instructions à l’aide de la :

* **Contrôleurs** section Hello **Maintenance** page Bonjour service StorSimple Manager
* Windows PowerShell pour StorSimple

Nous vous recommandons de gérer les contrôleurs de périphérique hello via le service StorSimple Manager hello. Si une action peut uniquement être effectuée à l’aide de Windows PowerShell pour StorSimple, didacticiel de hello rend une note.

Après avoir lu ce didacticiel, vous pourrez :

* redémarrer ou arrêter un contrôleur d’appareil StorSimple
* arrêter un appareil StorSimple
* Réinitialiser votre toofactory de périphérique StorSimple

## <a name="restart-or-shut-down-a-single-controller"></a>Redémarrage ou arrêt d’un contrôleur unique
Le redémarrage ou l’arrêt d’un contrôleur n’est pas nécessaire si le système fonctionne normalement. Les opérations d’arrêt d’un contrôleur d’appareil unique ne sont courantes que lorsqu’un composant matériel de l’appareil est défaillant et qu’il doit être remplacé. Le redémarrage d’un contrôleur peut également être nécessaire lorsque les performances sont affectées par une utilisation excessive de la mémoire ou un dysfonctionnement du contrôleur. Vous devez également toorestart un contrôleur après un remplacement de contrôleur réussi, si vous souhaitez tooenable hello remplacé contrôleur de test.

Le redémarrage d’un périphérique n’est pas initiateurs tooconnected interruption de service, en supposant que le contrôleur passif de hello est disponible. Si un contrôleur passif n’est pas disponible ou mis hors tension, puis en redémarrant hello actif contrôleur peut entraîner une interruption de service et les temps morts hello.

> [!IMPORTANT]
> * **Un contrôleur en cours d’exécution ne doit jamais être physiquement supprimé, car cela entraînerait une perte de redondance et une augmentation des risques d’interruption.**
> * Hello procédure suivante s’applique uniquement toohello appareil physique StorSimple. Pour plus d’informations sur comment toostart, arrêt et redémarrage hello périphérique d’appel virtuel, consultez [travailler avec un appareil virtuel hello](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

Vous pouvez redémarrer ou arrêter un contrôleur de périphérique unique à l’aide de hello portail classique Azure du service de StorSimple Manager hello ou Windows PowerShell pour StorSimple

effectuer des contrôleurs d’appareil à partir de hello portail Azure classic, toomanage hello comme suit.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart ou arrêter un contrôleur dans le portail classique
1. Accédez trop**appareils > Maintenance**.
2. Accédez trop**état du matériel** et vérifiez que hello de deux contrôleurs hello sur votre appareil sont **sain**.
   
    ![Vérifiez que les contrôleurs d’appareil StorSimple sont en bon état de fonctionnement](./media/storsimple-manage-device-controller/IC766017.png)
3. À partir du bas hello Hello **Maintenance** , cliquez sur **gérer les contrôleurs**.
   
    ![Gestion des contrôleurs d’appareil StorSimple](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Si vous ne voyez pas **gérer les contrôleurs**, vous avez besoin de mises à jour tooinstall. Pour plus d’informations, consultez [Mise à jour de votre appareil StorSimple](storsimple-update-device.md).
   > 
   > 
4. Bonjour **modifier les paramètres de contrôleur** boîte de dialogue zone, hello suivant :
   
   1. À partir de hello **sélectionner un contrôleur** liste déroulante, sélectionnez hello contrôleur que toomanage. options de Hello sont des contrôleurs 0 et 1. Ces contrôleurs sont également identifiés comme actifs ou passifs.
      
      > [!NOTE]
      > Un contrôleur ne peut pas être géré si elle est indisponible ou désactivé, et il n’apparaîtra pas dans la liste déroulante de hello.
      > 
      > 
   2. À partir de hello **sélectionner une Action** liste déroulante, sélectionnez **redémarrage du contrôleur** ou **arrêter contrôleur**.
      
       ![Redémarrage du contrôleur passif de l’appareil StorSimple](./media/storsimple-manage-device-controller/IC766020.png)
   3. Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-manage-device-controller/IC740895.png).

Cela redémarrer ou arrêter hello contrôleur. tableau Hello ci-dessous résume les détails de hello ce qui se produit en fonction des sélections hello que vous avez apportées dans hello **modifier les paramètres de contrôleur** boîte de dialogue.  

| # de sélection | Si vous choisissez de... | Ceci se produira. |
| --- | --- | --- |
| 1. |Redémarrer le contrôleur passif hello. |Une tâche sera créée le contrôleur de hello toorestart, et vous serez averti une fois hello tâche est créée. Ceci lancera le redémarrage du contrôleur hello. Vous pouvez surveiller le processus de redémarrage hello en accédant à **Service > tableau de bord > Afficher les journaux des opérations** , puis en filtrant par service tooyour spécifiques de paramètres. |
| 2. |Redémarrez le contrôleur actif de hello. |Hello suivant d’avertissement s’affiche : « Si vous redémarrez le contrôleur actif de hello, hello appareil basculera sur le contrôleur passif de toohello. Voulez-vous toocontinue ? » </br>Si vous choisissez tooproceed avec cette opération, les étapes suivantes hello sera contrôleur passif de toothose identiques utilisé toorestart hello (voir Sélection 1). |
| 3. |Arrêtez le contrôleur passif de hello. |Vous verrez hello message suivant : « une fois arrêté, vous devez toopush hello bouton d’alimentation sur votre contrôleur tooturn il sur. Êtes-vous sûr de que vouloir tooshut vers le bas de ce contrôleur ? » </br>Si vous choisissez tooproceed avec cette opération, les étapes suivantes hello sera contrôleur passif de toothose identiques utilisé toorestart hello (voir Sélection 1). |
| 4. |Arrêtez le contrôleur actif de hello. |Vous verrez hello message suivant : « une fois arrêté, vous devez toopush hello bouton d’alimentation sur votre contrôleur tooturn il sur. Êtes-vous sûr de que vouloir tooshut vers le bas de ce contrôleur ? » </br>Si vous choisissez tooproceed avec cette opération, les étapes suivantes hello sera contrôleur passif de toothose identiques utilisé toorestart hello (voir Sélection 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart ou arrêter un contrôleur dans Windows PowerShell pour StorSimple
Effectuer hello suivant les étapes tooshut vers le bas ou redémarrer un contrôleur unique sur votre appareil StorSimple à partir de hello portail Azure classic.

1. Équipement hello d’accès à l’aide de la console série de hello ou d’une session telnet à partir d’un ordinateur distant. Se connecter tooController 0 ou contrôleur 1 par hello suivant les étapes [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.
3. Dans le message de bannière hello, prenez note de contrôleur hello que vous êtes connecté trop (contrôleur 0 ou 1) et qu’il soit hello active ou contrôleur (de secours) passif de hello.
   
   * tooshut vers le bas un seul contrôleur, à l’invite de hello, tapez :
     
       `Stop-HcsController`
     
       Cela arrêtera contrôleur hello auquel vous êtes connecté à. Si vous arrêtez le contrôleur actif de hello, puis il échouera sur le contrôleur passif de toohello avant son arrêt.
   * toorestart un contrôleur, à l’invite de hello, tapez :
     
       `Restart-HcsController`
     
       Cette opération redémarre le contrôleur hello auquel vous êtes connecté à. Si vous redémarrez le contrôleur actif de hello, il échouera sur le contrôleur passif de toohello avant de redémarrer la hello.

## <a name="shut-down-a-storsimple-device"></a>arrêter un appareil StorSimple
Cette section explique comment tooshut vers le bas en cours d’exécution ou d’un appareil StorSimple a échoué à partir d’un ordinateur distant. Un périphérique est désactivé après l’arrêt des deux contrôleurs de périphérique hello. Un arrêt de l’appareil est effectué lors de l’appareil de hello est physiquement déplacé ou est mis hors service.

> [!IMPORTANT]
> Avant d’arrêter l’appareil de hello, vérifier l’intégrité de hello de composants de l’appareil hello. Accédez trop**appareils > Maintenance > état du matériel** et vérifiez que hello LED de tous les composants de hello sont verts. Un appareil en bon état de fonctionnement aura un état vert. Si votre appareil est arrêt tooreplace un composant défectueux, vous verrez un échec (rouge) ou un état détérioré (jaune) pour hello ou les composants respectifs.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut vers le bas un appareil StorSimple
1. Hello d’utilisation [redémarrer ou arrêter un contrôleur de](#restart-or-shut-down-a-single-controller) tooidentify de procédure et arrêter le contrôleur passif de hello sur votre appareil. Vous pouvez effectuer cette opération dans hello portail Azure classic ou dans Windows PowerShell pour StorSimple.
2. Répétez hello ci-dessus tooshut étape vers le bas du contrôleur actif de hello.
3. Vous devez désormais toolook à hello fond de panier de périphérique de hello. Une fois que les deux contrôleurs de hello complètement arrêtés, hello DEL d’état sur les deux contrôleurs hello clignotent en rouge. Si vous devez tooturn hors tension de l’appareil de hello complètement à ce stade, les interrupteurs d’alimentation de la rotation hello sur les deux Modules de refroidissement (PCM) toohello OFF position. Ceci doit désactiver le dispositif de hello.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Rétablir les paramètres par défaut de hello appareil toofactory
> [!IMPORTANT]
> Si vous devez tooreset les paramètres par défaut des appareils toofactory, contactez le Support Microsoft. procédure Hello décrite ci-dessous doit être utilisé qu’en association avec le Support technique de Microsoft.
> 
> 

Cette procédure décrit comment tooreset vos paramètres de valeur par défaut de Microsoft Azure StorSimple périphérique toofactory à l’aide de Windows PowerShell pour StorSimple.
Réinitialiser un appareil supprime toutes les données et les paramètres à partir de l’ensemble du cluster hello par défaut.

Effectuez hello suivant les étapes tooreset vos paramètres par défaut de Microsoft Azure StorSimple périphérique toofactory :

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault paramètres de périphérique dans Windows PowerShell pour StorSimple
1. Périphérique de hello accès via sa console série. Vérifiez tooensure de message de bannière hello que vous êtes connecté toohello les contrôleur actif.
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.
3. À l’invite de hello, tapez Bonjour suivant commande tooreset hello ensemble du cluster, la suppression de tous les paramètres de contrôleur, les métadonnées et les données :
   
    `Reset-HcsFactoryDefault`
   
    tooinstead réinitialiser un seul contrôleur, utilisez hello [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) applet de commande avec hello `-scope` paramètre.)
   
    système de Hello va redémarrer plusieurs fois. Vous serez averti lorsque hello réinitialisation est terminée. Selon le modèle de système de hello, il peut prendre 45 à 60 minutes pour un appareil 8100 et 60 à 90 minutes pour un toofinish 8600 ce processus.
   
   > [!TIP]
   > * Si vous utilisez la mise à jour 1.2 ou antérieure utiliser hello `–SkipFirmwareVersionCheck` vérification de la version du microprogramme hello tooskip paramètre (dans le cas contraire, vous verrez une erreur d’incompatibilité du microprogramme : paramètres d’usine ne peut pas continuer en raison d’incompatibilité tooa dans les versions de microprogramme hello. Sinon, une erreur d’incompatibilité du microprogramme s’affiche : la réinitialisation aux paramètres d’usine ne peut pas se poursuivre en raison d’une incohérence dans les versions du microprogramme.
   > * procédure de réinitialisation des paramètres d’usine Hello peut échouer pour les appareils StorSimple qui sont en cours d’exécution 1.1 ou mise à jour 1 dans le portail d’administration hello et ont effectué un remplacement de contrôleur de simples ou doubles réussi (avec des contrôleurs de remplacement qui ont été expédiées avec avant mise à jour 1 logiciel). Cela se produit lors de la réinitialisation hello image est validée présence hello d’un fichier SHA1 sur contrôleur hello qui n’existe pas pour les logiciels de 1 avant mise à jour. Si vous voyez cette fabrique de réinitialiser l’échec, contactez le Support technique de Microsoft tooassist vous hello étapes suivantes. Ce problème n’est pas affiché avec des contrôleurs de remplacement qui ont été expédiées à partir de la fabrique de hello avec Update 1 ou ultérieure du logiciel.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Questions et réponses sur la gestion des contrôleurs d’appareil
Dans cette section, nous avons résumé des hello questions fréquemment posées concernant la gestion des contrôleurs de périphérique StorSimple.

**Q.** Que se passe-t-il si les deux hello contrôleurs sur mon appareil sont sain et activé sur et redémarrer ou arrêter le contrôleur actif de hello ?

**A.** Si les deux contrôleurs hello sur votre appareil sont sains et activés, vous serez invité à confirmer l’opération. Vous pouvez choisir de :

* **Redémarrez le contrôleur actif de hello** – vous serez averti que le redémarrage d’un contrôleur actif provoquera hello appareil toofail sur le contrôleur passif de toohello. Hello redémarre.
* **Arrêter un contrôleur actif** : un message vous avertit que l’arrêt d’un contrôleur actif entraîne une coupure du service. Vous devez également bouton d’alimentation hello toopush sur tooturn de périphérique hello sur le contrôleur de hello.

**Q.** Que se passe-t-il si le contrôleur passif hello mon appareil est indisponible ou désactivé off et que je redémarre ou arrête contrôleur actif de hello ?

**A.** Si le contrôleur passif de hello sur votre appareil est indisponible ou désactivé et vous choisissez de :

* **Redémarrez le contrôleur actif de hello** – vous serez averti que la poursuite de l’opération de hello entraîne une interruption temporaire du service de hello, et vous serez invité à confirmer l’opération.
* **Arrêter un contrôleur actif** : vous êtes averti que poursuite de l’opération de hello provoquera un temps mort et que vous avez besoin de bouton d’alimentation hello toopush sur un ou deux tooturn contrôleurs sur l’appareil de hello. Vous êtes invité à confirmer l’opération.

**Q.** Lorsque ne hello contrôleur redémarrage ou l’arrêt a échoué tooprogress ?

**A.** Le redémarrage ou l’arrêt d’un contrôleur peut échouer si :

* Une mise à jour de l’appareil est en cours.
* Le redémarrage d’un contrôleur est déjà en cours.
* L’arrêt d’un contrôleur est déjà en cours.

**Q.** Comment pouvez-vous déterminer si un contrôleur a été redémarré ou arrêté ?

**A.** Vous pouvez vérifier l’état du contrôleur hello sur la page Maintenance de hello. état du contrôleur Hello indique si un contrôleur a été redémarré ou arrêté. En outre, page des alertes hello contiendra une alerte d’information si le contrôleur de hello a été redémarré ou arrêté. opérations de redémarrage et d’arrêt du contrôleur Hello sont également enregistrées dans les journaux des opérations de hello. Pour plus d’informations sur les journaux des opérations, consultez trop[afficher les journaux des opérations de hello](storsimple-service-dashboard.md#view-the-operations-logs).

**Q.** Existe-t-il des toohello impact des e/s en raison du basculement du contrôleur ?

**A.** les connexions TCP Hello entre les initiateurs et le contrôleur actif sont réinitialisées suite au basculement du contrôleur, mais rétablies lorsque le contrôleur passif de hello suppose que l’opération. Il peut exister une pause temporaire (moins de 30 secondes) dans l’activité d’e/s entre les initiateurs et les appareils hello hello pendant cette opération.

**Q.** Comment retourner mon tooservice contrôleur une fois qu’il a été arrêté et supprimé ?

**A.** tooreturn un tooservice de contrôleur, vous devez l’insérer dans le châssis de hello comme décrit dans [remplacer un module de contrôleur sur votre appareil StorSimple](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Étapes suivantes
* Si vous rencontrez des problèmes avec vos contrôleurs d’appareil StorSimple que vous ne pouvez pas résoudre à l’aide de procédures hello répertoriées dans ce didacticiel, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).
* toolearn plus sur l’utilisation de service de StorSimple Manager hello, accédez trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

