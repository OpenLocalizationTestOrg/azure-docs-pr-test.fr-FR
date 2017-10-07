---
title: "batterie aaaReplace sur l’appareil Microsoft Azure StorSimple | Documents Microsoft"
description: "Décrit comment remplacer les tooremove et mettre à jour le module de batterie de secours hello sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Remplacez le module de batterie de secours hello sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
boîtier principal de Hello d’alimentation et de Module de refroidissement (PCM) sur votre appareil Microsoft Azure StorSimple a un pack batterie supplémentaire. Ce pack fournit power afin que hello appareil StorSimple peut enregistrer les données si la perte de boîtier principal du toohello d’alimentation secteur. Ce pack batterie est référencé tooas hello *module de batterie de secours*. module de batterie de secours Hello existe uniquement pour le boîtier principal de hello dans votre appareil StorSimple (hello boîtiers ne contient pas un module de batterie de secours). 

Ce didacticiel explique comment :

* Supprimer le module de batterie de secours hello 
* Installer un nouveau module de batterie de secours
* Mettre à jour le module de batterie de secours hello

> [!IMPORTANT]
> Avant la suppression et le remplacement d’un module de batterie de secours, passez en revue les informations de sécurité hello Bonjour [remplacement de composant matériel Introduction tooStorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-backup-battery-module"></a>Supprimer le module de batterie de secours hello
module de batterie de secours Hello pour votre appareil StorSimple est une unité remplaçable. Avant son installation Bonjour PCM, module de batterie hello doit être stockée dans son emballage d’origine. Effectuer hello suivant la batterie de secours étapes tooremove hello.

#### <a name="tooremove-hello-backup-battery-module"></a>module de batterie de secours hello tooremove
1. Dans hello portail Azure classic, accédez trop**périphériques** > **Maintenance** > **état du matériel**. Sous **composants partagés**, regardez statut hello de batterie de hello.
2. Identifier le PCM hello dans le hello batterie a échoué. La figure 1 montre hello arrière de l’appareil StorSimple hello.
   
    ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-battery-replacement/IC740994.png)
   
    **Figure 1** Arrière de l’appareil principal avec les modules PCM et de contrôleur
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Contrôleur 0 |
   | 4 |Contrôleur 1 |
   
    Comme indiqué par le numéro 3 Bonjour Figure 2, hello analyse indicateur LED sur PCM 0 qui correspond trop**panne** doit être allumée.
   
    ![Fond du panier du module PCM de l’appareil avec voyants LED de surveillance](./media/storsimple-battery-replacement/IC740992.png)
   
    **Figure 2** hello d’affichage arrière du PCM des témoins DEL
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |Panne d’alimentation secteur |
   | 2 |Panne de ventilateur |
   | 3 |Panne de batterie |
   | 4 |PCM OK |
   | 5 |Panne d’alimentation secteur |
   | 6 |Batterie saine |
3. tooremove hello PCM avec la batterie est défectueuse, suivez les étapes de hello dans [retirer un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Hello PCM supprimé, courbes d’élévation et une batterie de rotation hello module gérer vers le haut, comme indiqué dans la figure suivante de hello et tirez dessus pour les batteries de hello tooremove.
   
    ![Retrait de la batterie du module PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Figure 3** supprime les batterie hello hello PCM
5. Placez le module de hello dans hello remplaçable emballage de l’unité.
6. Retourner tooMicrosoft d’unité défectueuse hello de maintenance et de gestion appropriée.

## <a name="install-a-new-backup-battery-module"></a>Installer un nouveau module de batterie de secours
Effectuer hello suivant du module de batterie de rechange étapes tooinstall hello Bonjour PCM dans le boîtier principal de hello de votre appareil StorSimple.

#### <a name="tooinstall-hello-battery-module"></a>module de batterie hello tooinstall
1. Placez le module de batterie de secours hello dans l’orientation appropriée de hello Bonjour PCM.
2. Module de batterie hello appuyez gérer connecteur hello de tous les hello moyen tooseat.
3. Remplacez hello PCM dans le boîtier principal de hello en suivant les instructions de hello dans [remplacer un Module de refroidissement et de puissance de votre appareil StorSimple](storsimple-power-cooling-module-replacement.md).
4. Une fois le remplacement de hello terminée, accédez trop**périphériques** > **Maintenance** > **état du matériel** Bonjour portail Azure classic. Vérifiez l’état hello de hello toomake de batterie que que hello installation a réussi. Un état vert indique que la batterie de hello est sain.

## <a name="maintain-hello-backup-battery-module"></a>Mettre à jour le module de batterie de secours hello
Dans votre appareil StorSimple, module de batterie de secours hello fournit contrôleur toohello de l’alimentation pendant un événement de perte d’alimentation. Il permet de hello StorSimple périphérique toosave données critiques de tooshutting de préalable vers le bas de manière contrôlée. Avec deux batteries entièrement chargées Bonjour PCM, système de hello peut gérer deux d’affilée.

Bonjour portail Azure classic, hello **état du matériel** sur hello **Maintenance** page indique si la batterie de hello est défectueux ou hello en fin de vie est proche. état de la batterie Hello est indiqué par **batterie dans PCM 0** ou **batterie dans PCM 1** sous **composants partagés**. Cette page indique l’état **DÉTÉRIORÉ** si la fin de durée de vie approche et l’état **ÉCHEC** si elle est atteinte. 

> [!NOTE]
> batterie de Hello peut signaler **n’a pas pu** lorsqu’elle doit simplement toobe facturé.
> 
> 

Si hello **détérioré** état s’affiche, nous vous recommandons de hello suivant la marche à suivre :

* système de Hello a peut-être rencontré une panne de courant récentes ou les piles hello peuvent être en cours de maintenance périodique. Observez le système de hello pendant 12 heures avant de continuer.
  
  * Si l’état de hello est toujours **détérioré** après 12 heures d’alimentation de tooAC connexion permanente avec hello contrôleurs et les PCM sont en cours d’exécution, puis hello batterie doit toobe remplacé. Veuillez [contacter le support Microsoft](storsimple-contact-microsoft-support.md) pour obtenir un module de batterie de secours de remplacement.
  * Si l’état de hello devient OK après 12 heures, hello batterie est opérationnelle, et il nécessaire uniquement les frais de maintenance.
* S’il n’a pas été une entraîne une perte d’alimentation secteur et hello PCM est allumée et connecté tooAC power, batterie de hello doit toobe remplacé. [Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) tooorder un module de batterie de secours.

> [!IMPORTANT]
> Dispose de hello Échec de la batterie en fonction de toonational et réglementations régionales. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).

