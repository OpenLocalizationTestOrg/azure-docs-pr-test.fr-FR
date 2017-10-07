---
title: "aaaReplace un contrôleur de l’appareil StorSimple | Documents Microsoft"
description: "Explique comment tooremove et remplacer un ou deux modules de contrôleur sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e25b52b7-60f5-47f3-bffc-6c157d57ab5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/03/2017
ms.author: alkohli
ms.openlocfilehash: ebf5c5830120857f69909113e3a111f4dda30e57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Remplacement d’un module de contrôleur sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooremove et remplacer un ou deux modules de contrôleur dans un appareil StorSimple. Elle explique également hello sous-jacent logique pour les scénarios de remplacement de contrôleur simple et double hello.

> [!NOTE]
> Tooperforming préalable un remplacement de contrôleur, nous vous recommandons de toujours à jour votre version la plus récente toohello contrôleur du microprogramme.
> 
> tooprevent endommager l’appareil StorSimple tooyour, n’éjectez pas le contrôleur de hello tant que hello DEL hello suivantes :
> 
> * Tous les témoins lumineux sont éteints.
> * Le voyant LED 3, ![icône en forme de coche verte](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), et ![icône en forme de croix rouge](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) clignotent, et les voyants LED 0 et 7 sont **allumés**.
> 
> 

Hello tableau suivant montre les scénarios de remplacement de contrôleur hello pris en charge.

| Cas | Scénario de remplacement | Procédure applicable |
|:--- |:--- |:--- |
| 1 |Un seul contrôleur est dans un état d’échec, hello autre contrôleur est intègre et actif. |[Unique de remplacement du contrôleur](#replace-a-single-controller), qui décrit hello [logique derrière un remplacement de contrôleur unique](#single-controller-replacement-logic), ainsi que de hello [procédure de remplacement](#single-controller-replacement-steps). |
| 2 |Les deux contrôleurs hello ont échoué et doivent être remplacés. châssis de Hello, les disques et boîtier sont intègres. |[Remplacement du double contrôleur](#replace-both-controllers), qui décrit hello [logique derrière un double remplacement de contrôleur](#dual-controller-replacement-logic), ainsi que de hello [procédure de remplacement](#dual-controller-replacement-steps). |
| 3 |Contrôleurs de hello même appareil ou à partir de différents appareils sont échangés. châssis de Hello, les disques et les boîtiers sont intègres. |Un message d’alerte s’affiche pour signaler la mauvaise correspondance d’un emplacement. |
| 4 |Un seul contrôleur est manquant et hello autres échoue de contrôleur. |[Remplacement du double contrôleur](#replace-both-controllers), qui décrit hello [logique derrière un double remplacement de contrôleur](#dual-controller-replacement-logic), ainsi que de hello [procédure de remplacement](#dual-controller-replacement-steps). |
| 5 |Un seul contrôleur ou les deux sont en panne. Impossible d’accéder à des périphériques de hello via la console série de hello ou la communication à distance de Windows PowerShell. |[contacter le support Microsoft](storsimple-contact-microsoft-support.md) pour suivre une procédure de remplacement de contrôleur manuelle. |
| 6 |les contrôleurs de Hello ont une autre version, qui peut être due à :<ul><li>Les versions de logiciel des contrôleurs sont différentes.</li><li>Les versions de microprogramme des contrôleurs sont différentes.</li></ul> |Si les versions des logiciels hello contrôleurs sont différentes, la logique de remplacement hello détecte qu’et mises à jour hello version du logiciel sur un contrôleur de remplacement hello.<br><br>Si les versions de microprogramme hello contrôleurs sont différentes et hello ancienne version du microprogramme **pas** automatiquement mise à niveau, un message d’alerte s’affiche dans hello portail Azure classic. Vous devez rechercher les mises à jour et installer les mises à jour du microprogramme hello.</br></br>Si les versions de microprogramme hello contrôleurs sont différentes et ancienne version de microprogramme hello est automatiquement mise à niveau, logique de remplacement de contrôleur hello détecte et après le démarrage du contrôleur de hello, microprogramme de hello sera mis à jour automatiquement. |

Vous devez tooremove un module de contrôleur en cas d’échec. Un ou deux modules de contrôleur hello peuvent échouer, ce qui peut entraîner un remplacement d’un contrôleur unique ou un double remplacement de contrôleur. Pour les procédures de remplacement et la logique de hello derrière eux, voir hello :

* [Remplacer un seul contrôleur](#replace-a-single-controller)
* [Remplacer les deux contrôleurs](#replace-both-controllers)
* [Retirer un contrôleur](#remove-a-controller)
* [Insérer un contrôleur](#insert-a-controller)
* [Identifier le contrôleur actif de hello sur votre appareil](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Avant de supprimer et remplacement d’un contrôleur, passez en revue les informations de sécurité de hello dans [remplacement de composant matériel StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Remplacer un seul contrôleur
Lorsqu’un des contrôleurs hello deux sur l’appareil de Microsoft Azure StorSimple hello a échoué, est défectueux ou est manquant, vous devez tooreplace un seul contrôleur. 

### <a name="single-controller-replacement-logic"></a>Logique de remplacement d’un seul contrôleur
Dans un remplacement de contrôleur simple, vous devez tout d’abord supprimer contrôleur hello. (contrôleur restant de hello dans l’appareil de hello est contrôleur actif de hello). Lorsque vous insérez le contrôleur de remplacement hello, hello actions suivantes se produisent :

1. contrôleur de remplacement Hello commence immédiatement à communiquer avec l’appareil StorSimple hello.
2. Un instantané d’hello disque dur virtuel (VHD) pour le contrôleur actif de hello est copié sur le contrôleur de remplacement hello.
3. instantané d’Hello est modifié afin que lorsque le contrôleur de remplacement hello démarre à partir de ce disque dur virtuel, il est reconnu comme un contrôleur de secours.
4. Lorsque des modifications de hello sont terminées, contrôleur de remplacement hello démarrera en tant que contrôleur de secours hello.
5. Lorsque les deux contrôleurs hello sont en cours d’exécution, le cluster de hello est en ligne.

### <a name="single-controller-replacement-steps"></a>Procédure de remplacement d’un seul contrôleur
Terminer hello comme suit si un des contrôleurs de hello dans votre appareil Microsoft Azure StorSimple échoue. (hello autre contrôleur doit être actif et en cours d’exécution. Si les deux contrôleurs de panne ou de dysfonctionnement, passez trop[procédure de remplacement des deux contrôleurs](#dual-controller-replacement-steps).)

> [!NOTE]
> Il peut prendre 30 et 45 minutes hello contrôleur toorestart et complètement récupérer à partir de la procédure de remplacement d’un contrôleur unique hello. durée totale Hello hello ensemble de la procédure, y compris le branchement des câbles de hello, est 2 heures environ.
> 
> 

#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove un module de contrôleur unique
1. Bonjour portail Azure classic, accédez toohello le service StorSimple Manager, cliquez sur hello **périphériques** onglet, puis cliquez sur nom hello du périphérique hello que vous souhaitez toomonitor.
2. Accédez trop**Maintenance > état du matériel**. état Hello contrôleur 0 ou contrôleur 1 doit être rouge, ce qui indique un échec.
   
   > [!NOTE]
   > Hello de contrôleur défectueux dans un remplacement de contrôleur unique est toujours un contrôleur de secours.
   > 
   > 
3. Utilisez la Figure 1 et hello suivant table toolocate hello Échec du module de contrôleur.  
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-controller-replacement/IC740994.png)
   
    **Figure 1** Arrière de l’appareil StorSimple
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Contrôleur 0 |
   | 4 |Contrôleur 1 |
4. Sur le contrôleur défectueux de hello, supprimez tous les câbles de réseau hello connecté hello ports de données. Si vous utilisez un modèle 8600, également supprimer hello que qui connectent du contrôleur EBOD hello contrôleur toohello les câbles SAS.
5. Suivez les étapes de hello dans [supprimer un contrôleur de](#remove-a-controller) tooremove hello Échec de contrôleur. 
6. Remplacement de fabrique hello installation Bonjour même emplacement à partir de quel contrôleur défectueux hello a été supprimé. Cela déclenche la logique de remplacement de contrôleur simple hello. Pour plus d’informations, voir [Logique de remplacement d’un seul contrôleur](#single-controller-replacement-logic).
7. Alors que la logique de remplacement de contrôleur simple hello progresse en arrière-plan de hello, rebranchez les câbles de hello. Prendre tooconnect soins tous les câbles hello hello exactement identique, qu’ils ont été connectés avant le remplacement de hello.
8. Une fois hello contrôleur a redémarré, vérifiez hello **état du contrôleur** et hello **état du Cluster** Bonjour Azure classic tooverify portail qui hello contrôleur tooa précédent état est sain et est en mode veille .

> [!NOTE]
> Si vous analysez un appareil hello via la console série de hello, vous pouvez voir plusieurs redémarrages pendant que la récupération à partir de la procédure de remplacement hello de contrôleur de hello. Lorsque le menu de console série hello est présent, vous savez que le remplacement de hello est terminée. Si le menu de hello n’apparaît pas dans les deux heures de remplacement du contrôleur hello, veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).
>
> À partir de mise à jour 4, vous pouvez également utiliser les applets de commande hello `Get-HCSControllerReplacementStatus` dans l’interface Windows PowerShell hello de hello toomonitor hello état du processus de remplacement de contrôleur hello.
> 

## <a name="replace-both-controllers"></a>Remplacer les deux contrôleurs
Lorsque les deux contrôleurs sur l’appareil de Microsoft Azure StorSimple hello ont échoué, sont défectueux ou sont manquantes, vous devez tooreplace les deux contrôleurs. 

### <a name="dual-controller-replacement-logic"></a>Logique de remplacement de deux contrôleurs
Dans un remplacement de deux contrôleurs, vous devez d’abord retirer les deux contrôleurs en panne, puis insérer les contrôleurs de rechange. Lors de l’insertion de deux contrôleurs de remplacement hello, hello actions suivantes se produisent :

1. contrôleur de remplacement Hello dans l’emplacement 0 vérifie suivant de hello :
   
   1. Il utilise les versions actuelles de hello microprogrammes et logiciels ?
   2. Il est une partie du cluster de hello ?
   3. Contrôleur d’homologue hello en cours d’exécution et en cluster ?
      
      Si aucune de ces conditions sont remplies, hello contrôleur recherche sauvegarde quotidienne la plus récente hello (situé dans hello **nonDOMstorage** sur le lecteur S). Hello contrôleur copies hello instantané le plus récent de hello disque dur virtuel à partir de la sauvegarde de hello.
2. contrôleur Hello dans l’emplacement 0 utilise tooimage d’instantané hello lui-même.
3. Pendant ce temps, contrôleur hello dans l’emplacement 1 attend pour l’acquisition d’images de contrôleur 0 toocomplete hello et démarrer.
4. Une fois que le contrôleur 0 démarre, le contrôleur 1 détecte cluster hello créé par le contrôleur 0, ce qui déclenche la logique de remplacement de contrôleur simple hello. Pour plus d’informations, voir [Logique de remplacement d’un seul contrôleur](#single-controller-replacement-logic).
5. Ensuite, les deux contrôleurs sont en cours d’exécution et cluster de hello est mis en ligne.

> [!IMPORTANT]
> Après un double remplacement de contrôleur, après avoir configuré l’appareil StorSimple hello, il est essentiel de prendre un manuel de sauvegarde de l’appareil de hello. Les sauvegardes quotidiennes de la configuration de l’appareil se déclenchent uniquement après un délai de 24 heures. Travailler avec [Support technique de Microsoft](storsimple-contact-microsoft-support.md) toomake une sauvegarde manuelle de votre appareil.
> 
> 

### <a name="dual-controller-replacement-steps"></a>Procédure de remplacement des deux contrôleurs
Ce flux de travail est requis lorsque les deux contrôleurs hello dans votre appareil Microsoft Azure StorSimple ont échoué. Cela peut se produire dans un centre de données dans laquelle système de refroidissement hello cesse de fonctionner, et par conséquent, les deux contrôleurs hello échouent sur une courte période de temps. Selon si l’appareil StorSimple hello est désactivé ou activé, si vous utilisez un 8600 ou un modèle 8100, un autre ensemble d’étapes est nécessaire.

> [!IMPORTANT]
> Il peut accepter des heures de too1 45 minutes pour hello contrôleur toorestart et complètement récupérer à partir d’une procédure de remplacement des deux contrôleurs. durée totale Hello hello ensemble de la procédure, y compris le branchement des câbles de hello, est approximativement de 2 heures.
> 
> 

#### <a name="tooreplace-both-controller-modules"></a>tooreplace deux modules de contrôleur
1. Si l’appareil de hello est mis hors tension, ignorez cette étape et passez toohello prochaine étape. Si l’appareil de hello est activée, désactiver le dispositif de hello.
   
   1. Si vous utilisez un modèle 8600, boîtier principal de hello préalable désactiver, puis désactivez hello boîtiers.
   2. Attendez que l’appareil de hello arrêt complet. Hello toutes les DEL Bonjour arrière appareil de hello sera désactivée.
2. Supprimez tous les câbles réseau hello qui sont des ports de données toohello connecté. Si vous utilisez un modèle 8600, également supprimer hello que qui connectent les boîtiers de hello boîtier principal toohello les câbles SAS.
3. Supprimez les deux contrôleurs de l’appareil StorSimple hello. Pour plus d’informations, consultez [Retrait d’un contrôleur](#remove-a-controller).
4. Insérer le modèle de remplacement hello du contrôleur 0 tout d’abord, puis insérez le contrôleur 1. Pour plus d’informations, voir [Insertion d’un contrôleur](#insert-a-controller). Cela déclenche la logique de remplacement de contrôleur double hello. Pour plus d’informations, voir [Logique de remplacement de deux contrôleurs](#dual-controller-replacement-logic).
5. Alors que la logique de remplacement de contrôleur hello progresse en arrière-plan de hello, rebranchez les câbles de hello. Prendre tooconnect soins tous les câbles hello hello exactement identique, qu’ils ont été connectés avant le remplacement de hello. Consultez hello des instructions détaillées pour votre modèle Bonjour câble votre section du périphérique de [installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md) ou [installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md).
6. Activer l’appareil StorSimple hello. Si vous utilisez un modèle 8600 :
   
   1. Assurez-vous que hello boîtiers est activée en premier.
   2. Attendez que hello boîtiers est en cours d’exécution.
   3. Allumez le boîtier principal de hello.
   4. Une fois le premier contrôleur de hello redémarre et est dans un état sain, système de hello s’exécute.
      
      > [!NOTE]
      > Si vous analysez un appareil hello via la console série de hello, vous pouvez voir plusieurs redémarrages pendant que la récupération à partir de la procédure de remplacement hello de contrôleur de hello. Lorsque le menu de console série hello s’affiche, vous savez que le remplacement de hello est terminée. Si le menu de hello n’apparaît pas dans les 2 heures de remplacement du contrôleur hello, veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).
      > 
      > 

## <a name="remove-a-controller"></a>Retirer un contrôleur
Utilisez hello suivant la procédure tooremove un module de contrôleur défectueux à partir de votre appareil StorSimple.

> [!NOTE]
> Hello suivant illustrations est pour le contrôleur 0. Pour le contrôleur 1, leur présentation doit être inversée.
> 
> 

#### <a name="tooremove-a-controller-module"></a>tooremove un module de contrôleur
1. Saisissez le verrou du module hello entre votre pouce et.
2. Pressez doucement votre pouce et votre index toorelease ensemble hello verrou du contrôleur.
   
    ![Libération du verrou du contrôleur](./media/storsimple-controller-replacement/IC741047.png)
   
    **Figure 2** Libération du verrou du contrôleur
3. Utilisation des verrous de hello en tant que handle tooslide hello contrôleur hors du châssis de hello.
   
    ![Glissement du contrôleur hors du châssis](./media/storsimple-controller-replacement/IC741048.png)
   
    **Figure 3** insertion du contrôleur hors du châssis de hello hello

## <a name="insert-a-controller"></a>Insérer un contrôleur
Utilisez hello suivant la procédure tooinstall un module de contrôleur lorsque vous supprimez un module est défectueux de votre appareil StorSimple.

#### <a name="tooinstall-a-controller-module"></a>tooinstall un module de contrôleur
1. Vérifiez toosee en n’importe quel toohello dommages connecteurs d’interface. N’installez pas de module de hello si des broches du connecteur hello sont endommagées ou tordues.
2. Faites glisser le module de contrôleur hello dans le châssis de hello tandis que hello loquet entièrement libéré. 
   
    ![Insertion du contrôleur dans le châssis](./media/storsimple-controller-replacement/IC741053.png)
   
    **Figure 4** insertion du contrôleur dans le châssis de hello
3. Module de contrôleur hello inséré, commencer fermeture du verrou de hello lors de la poursuite de l’opération du module de contrôleur toopush hello dans le châssis de hello. Hello engagement du loquet entraîne contrôleur de hello tooguide en place.
   
    ![Fermeture du verrou du contrôleur](./media/storsimple-controller-replacement/IC741054.png)
   
    **Figure 5** fermeture du verrou du contrôleur hello
4. Vous avez terminé quand le loquet de hello s’enclenche. Hello **OK** DEL doit maintenant s’allumer.  
   
   > [!NOTE]
   > Il peut prendre jusqu'à minutes too5 pour contrôleur de hello et hello LED tooactivate.
   > 
   > 
5. tooverify remplacement de hello a réussi, dans hello Azure classic, accédez trop**périphériques** > **Maintenance** > **état du matériel**et assurez-vous que les contrôleurs 0 et 1 sont intègres (état est vert).

## <a name="identify-hello-active-controller-on-your-device"></a>Identifier le contrôleur actif de hello sur votre appareil
Il existe de nombreuses situations, notamment la première fois l’inscription ou contrôleur de remplacement, nécessitant de votre contrôleur actif de hello toolocate sur un appareil StorSimple. contrôleur actif de Hello traite tous les hello mise en réseau et microprogramme opérations de disque. Vous pouvez utiliser une des hello suivant le contrôleur actif de méthodes tooidentify hello :

* [Utiliser le contrôleur actif de hello tooidentify de portail classique Azure hello](#use-the-azure-classic-portal-to-identify-the-active-controller)
* [Utiliser Windows PowerShell pour le contrôleur actif de StorSimple tooidentify hello](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Vérifier le contrôleur actif de hello périphérique physique tooidentify hello](#check-the-physical-device-to-identify-the-active-controller)

Chacune de ces procédures est décrite ci-dessous.

### <a name="use-hello-azure-classic-portal-tooidentify-hello-active-controller"></a>Utiliser le contrôleur actif de hello tooidentify de portail classique Azure hello
Dans hello portail Azure classic, accédez trop**périphériques** > **Maintenance**, faites défiler la fenêtre toohello **contrôleurs** section. Dans cette section, vous pouvez vérifier quel contrôleur est actif.

![Identifier le contrôleur actif dans le portail Azure Classic](./media/storsimple-controller-replacement/IC752072.png)

**Figure 6** contrôleur actif de hello montrant de portail classique Azure

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Utiliser Windows PowerShell pour le contrôleur actif de StorSimple tooidentify hello
Lorsque vous accédez à votre appareil via la console série de hello, un message de bannière est présenté. message de bannière Hello contient des informations de base telles que le modèle de hello, nom, version du logiciel installé et l’état du contrôleur hello vous accédez à. Hello suivant image montre un exemple de message de bannière :

![Message de bannière série](./media/storsimple-controller-replacement/IC741098.png)

**Figure 7** Message de bannière indiquant que le contrôleur 0 est actif

Vous pouvez utiliser toodetermine de message de bannière hello que hello contrôleur que vous soyez connecté toois actives ou passives.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Vérifier le contrôleur actif de hello périphérique physique tooidentify hello
contrôleur actif de hello tooidentify sur votre appareil, recherchez hello bleu DEL au-dessus du port hello DATA 5 sur hello arrière du boîtier principal de hello.

Si cette LED clignote, hello contrôleur est actif et hello autre contrôleur est en mode veille. Utilisez hello suivant schéma et de table comme une aide.

![Fond de panier du boîtier principal de l’appareil avec ports de données](./media/storsimple-controller-replacement/IC741055.png)

**Figure 8** Arrière du boîtier principal, avec les ports de données et les voyants LED de contrôle

| Étiquette | Description |
|:--- |:--- |
| 1 à 6 |Ports réseau DATA 0 – 5 |
| 7 |Voyant LED bleu |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).

