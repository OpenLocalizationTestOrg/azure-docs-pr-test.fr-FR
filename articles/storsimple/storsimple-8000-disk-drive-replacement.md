---
title: "aaaReplace un lecteur de disque sur un appareil de série StorSimple 8000 | Documents Microsoft"
description: "Explique comment tooreplace un disque du lecteur sur un boîtier principal StorSimple ou d’un boîtier EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a>Remplacer un lecteur de disque sur votre appareil de la gamme StorSimple 8000

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment vous pouvez retirer et remplacer un lecteur de disque dur défectueux ou défaillant sur un appareil Microsoft Azure StorSimple. tooreplace un lecteur de disque, vous devez :

* Désactiver le dispositif de sécurisation hello
* Supprimer le lecteur de disque hello
* Installer le lecteur de disque de remplacement hello

> [!IMPORTANT]
> Avant de retrait et le remplacement d’un disque dur, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-8000-hardware-component-replacement.md).
 

## <a name="disengage-hello-antitamper-lock"></a>Désactiver le dispositif de sécurisation hello
Cette procédure explique comment dispositifs de hello sur votre appareil StorSimple peuvent verrouiller ou déverrouiller lorsque vous remplacez les lecteurs de disque hello. dispositifs de Hello sont montés dans des poignées de transport de lecteur hello et ils sont accessibles via une petite ouverture dans hello loquet de handle de hello. Les lecteurs sont fournis avec les verrous hello définir la position toohello verrouillé.

#### <a name="toounlock-hello-antitamper-lock"></a>Dispositif de sécurisation de toounlock hello
1. Insérez soigneusement la clé de verrouillage de hello (tournevis « infalsifiables « T10 fourni par Microsoft) en ouverture hello du handle hello et le socket. 
   
   Si le dispositif de sécurisation hello est activé, indicateur de hello rouge est visible dans l’ouverture de hello.
  
    ![Lecteur de disque verrouillé](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Figure 1** : Verrou anti-effraction engagé
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |Ouverture de l’indicateur |
   | 2 |Verrou anti-effraction |
2. Clé de rotation hello dans un sens inverse des aiguilles jusqu'à ce que l’indicateur de hello rouge n’est pas visible dans l’ouverture de hello au-dessus de la clé de hello.
3. Supprimez la clé de hello.
   
    ![ : Lecteur de disque déverrouillé](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Figure 2** : Lecteur de disque déverrouillé
4. lecteur de disque Hello peut maintenant être supprimée.

Suivez les étapes de hello de verrou de hello tooengage inverse.

## <a name="remove-hello-disk-drive"></a>Supprimer le lecteur de disque hello
Votre appareil StorSimple prend en charge une configuration des espaces de stockage en RAID 10. Ceci implique qu’il peut fonctionner normalement avec un disque défectueux, qui peut être un disque SSD ou un disque dur.

> [!IMPORTANT]
> * Si votre système a plus d’un disque en panne, ne supprimez pas plus d’un disque SSD ou HDD système hello à n’importe quel point dans le temps. Ceci peut entraîner la perte de données.
> * Veillez à placer un disque SSD de remplacement à un emplacement qui contenait auparavant un disque SSD. De même, veillez à placer un disque dur de remplacement à un emplacement qui contenait auparavant un disque dur.
> * Bonjour portail Azure, les emplacements sont numérotés de 0 à 11. Par conséquent, si le portail de hello montre qu’un disque dans l’emplacement 2 a échoué sur l’appareil de hello, recherchez hello disque en panne dans l’emplacement de tiers hello hello en haut à gauche.
> 
> 

Lecteurs peuvent être supprimés et remplacés pendant le fonctionnement du système de hello.

#### <a name="tooremove-a-drive"></a>tooremove un lecteur
1. tooidentify hello Échec de disque, Bonjour portail Azure, accédez tooyour périphérique **Paramètres > intégrité du matériel**. Car un disque peut échouer dans le boîtier principal de hello et/ou un boîtier EBOD (si vous utilisez un modèle 8600), examinez état hello de disques hello sous **des composants partagés** et sous **composants partagés EBOD** . Un disque défectueux dans un des boîtiers est affiché avec un état rouge.
2. Recherchez hello lecteurs à l’avant du boîtier principal de hello ou boîtiers hello hello. 
3. Si le disque de hello est déverrouillé, passez toohello prochaine étape. Si le disque de hello est verrouillé, déverrouillez-le en suivant la procédure hello dans [désactiver le dispositif de sécurisation hello](#disengage-the-antitamper-lock).
4. Appuyez sur hello noir de verrous internes sur le module de transport hello et extraient retirer poignée hello avant de hello du châssis de hello.
   
    ![Libération de la poignée du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Figure 3** poignée hello libération
5. Lors de la poignée du lecteur hello est entièrement développée, faites glisser hello lecteur hors du châssis de hello. 
   
    ![Retrait du disque hors du lecteur de disque](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Figure 4** glissante disque hello en dehors de l’opérateur de hello

## <a name="install-hello-replacement-disk-drive"></a>Installer le lecteur de disque de remplacement hello
Après un lecteur de disque défectueux dans votre appareil StorSimple et vous l’avez supprimé, suivez cette procédure tooreplace avec un nouveau lecteur.

#### <a name="tooinsert-a-drive"></a>tooinsert un lecteur
1. Vérifiez la poignée hello est entièrement développée, comme indiqué dans hello suivant l’image.
   
    ![Lecteur de disque avec la poignée en extension](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Figure 5** : Lecteur avec la poignée en extension
2. Faites glisser hello lecteur moyen de tous les hello dans le châssis de hello.
   
    ![Insertion du disque dans le support de lecteur disque](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Figure 6** support hello décalé dans le châssis de hello
3. Avec hello lecteur transporteur hello inséré, fermez sa poignée lors de la poursuite de l’opération toopush hello support dans le châssis hello, jusqu'à ce que la poignée du lecteur hello s’aligne en position verrouillée.
4. Utilisez hello clé de verrouillage a été fournie par la poignée du support Microsoft (tournevis de Torx inviolable) toosecure hello en place en activant le hello verrou vis un quart de tour dans le sens horaire.
5. Vérifiez que hello remplacement a réussi et hello lecteur est opérationnel. Accéder au portail Azure de hello et accédez trop**paramètres** > **l’intégrité du matériel**. Sous **des composants partagés** ou **composants partagés EBOD**, état du lecteur hello doit être vert, indiquant qu’il est sain.
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > Il peut prendre plusieurs heures hello disque état tooturn vert après le remplacement de hello.
  
## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).

