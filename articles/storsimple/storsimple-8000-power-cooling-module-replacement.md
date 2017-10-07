---
title: "aaaReplace un PCM sur votre appareil de série StorSimple 8000 | Documents Microsoft"
description: Explique comment tooremove et remplacer hello Module de refroidissement (PCM) sur votre appareil StorSimple
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Remplacer un module d’alimentation et de refroidissement (PCM, Power and Cooling Module) sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Hello d’alimentation et Module de refroidissement (PCM) dans votre appareil Microsoft Azure StorSimple se compose d’un bloc d’alimentation et des ventilateurs contrôlés par l’intermédiaire de type hello principal et les boîtiers. Il n’existe qu’un seul modèle de PCM certifié pour chaque boîtier. boîtier principal de Hello est certifié pour un PCM de 764 W et boîtiers hello est certifié pour un PCM de 580 W. Bien que hello PCM pour le boîtier principal de hello et boîtiers hello sont différentes, la procédure de remplacement hello est identique.

Ce didacticiel explique comment :

* Retirer un PCM
* Installer un PCM de remplacement

> [!IMPORTANT]
> Avant de supprimer et remplacer un PCM, passez en revue les informations de sécurité hello dans [remplacement de composant matériel StorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="before-you-replace-a-pcm"></a>Avant de remplacer un PCM
Tenez compte des hello suivant des problèmes importants avant de remplacer votre PCM :

* Si hello d’alimentation de hello PCM tombe en panne, laissez hello module défectueux installé mais Retirez le cordon d’alimentation hello. ventilateur de Hello sera power tooreceive de boîtier de hello et poursuivre tooprovide un refroidissement adéquat. Si le ventilateur de hello échoue, hello PCM doit toobe immédiatement remplacé.
* Avant de supprimer hello PCM, débranchez hello alimentation hello PCM en désactivant le commutateur principal de hello (le cas échéant) ou en retirant physiquement le cordon d’alimentation hello. Cela fournit un système d’avertissement tooyour qu’un arrêt de l’alimentation est imminent.
* Vérifiez que hello pour qu'autre PCM est opérationnel la poursuite de système avant remplacement hello PCM défectueux. Un PCM défectueux doit être remplacé dès que possible par un PCM totalement opérationnel.
* Remplacement d’un module PCM prend uniquement de quelques minutes toocomplete, mais il doit être effectuée dans 10 minutes de la suppression de hello échoué PCM tooprevent surchauffe.
* Notez que hello remplacement 764 W modules PCM à la sortie d’usine de hello ne contiennent pas de module de batterie de secours hello. Vous avez besoin de batterie de hello tooremove à partir de votre PCM défectueux et puis insérez-le dans le remplacement de hello hello remplacement module tooperforming préalable. Pour plus d’informations, consultez Comment trop[supprimer et insérer un module de batterie de secours](storsimple-8000-battery-replacement.md).

## <a name="remove-a-pcm"></a>Retirer un PCM
Suivez ces instructions lorsque vous êtes prêt tooremove une puissance et Module de refroidissement (PCM) à partir de votre appareil Microsoft Azure StorSimple.

> [!NOTE]
> Avant de retirer le PCM, vérifiez que vous disposez d’un remplacement approprié (764 W pour le boîtier principal de hello) ou 580 W pour hello boîtiers.

#### <a name="tooremove-a-pcm"></a>tooremove un PCM
1. Bonjour portail Azure classic, cliquez sur **Paramètres > Analyse > état du matériel**. Vérifier l’état de hello des composants PCM hello sous **des composants partagés** tooidentify le PCM défectueux :
   
   * Si un bloc d’alimentation dans PCM 0 a échoué, hello état de **d’alimentation dans PCM 0** apparaîtra en rouge.
   * Si un bloc d’alimentation dans PCM 1 a échoué, hello état de **alimentation dans PCM 1** apparaîtra en rouge.
   * Si le ventilateur hello dans PCM 1 a échoué, hello statut de **de refroidissement 0 pour PCM 0** ou **refroidissement 1 pour PCM 0** apparaîtra en rouge.
2. Recherchez hello PCM défectueux à hello arrière du boîtier principal de hello. Si vous exécutez un modèle 8600, identifier le boîtier principal de hello en examinant hello numéro d’Identification système unité affiché en hello DEL du panneau avant. Hello par défaut affiché sur le boîtier principal de hello est **00**, alors que la valeur par défaut hello ID d’unité est affiché sur hello boîtiers est **01**. Hello diagramme et le tableau suivants expliquent façade de hello d’affichage de hello DEL.
   
    ![ID du système sur le panneau avant des opérations](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Figure 1** panneau avant de l’appareil de hello  
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |Bouton Muet |
   | 2 |Alimentation du système |
   | 3 |Panne de module |
   | 4 |Erreur logique |
   | 5 |Affichage de l’ID de l’unité |
3. Hello des témoins DEL Bonjour à l’arrière du boîtier principal de hello peut également être utilisé tooidentify hello PCM défectueux. Voir hello diagramme et tableau toounderstand comment toouse hello DEL toolocate hello PCM défectueux. Par exemple, si hello conduit correspondant toohello **panne du ventilateur** est allumée, hello panne de ventilateur. De même, si hello conduit correspondant trop**panne** est allumée, alimentation hello a échoué. 
   
    ![Fond de panier des voyants LED de surveillance du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Figure 2** : Arrière du PCM avec les voyants LED
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |Panne d’alimentation secteur |
   | 2 |Panne de ventilateur |
   | 3 |Panne de batterie |
   | 4 |PCM OK |
   | 5 |Panne d’alimentation secteur |
   | 6 |Batterie saine |
4. Consultez toohello suivant schéma Hello arrière module PCM de hello StorSimple périphérique toolocate hello a échoué. PCM 0 est sur hello gauche et PCM 1 est à droite de hello. table Hello qui suit décrit les modules hello.
   
     ![Fond du panier des modules du boîtier principal de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Figure 3** : Arrière de l’appareil avec des modules enfichables 
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Contrôleur 0 |
   | 4 |Contrôleur 1 |
5. Activer off hello PCM défectueux et débranchez d’alimentation hello. Vous pouvez supprimer hello PCM.
6. Saisissez le loquet de hello et côté hello Hello PCM gérer entre votre pouce et et serrez vos doigts handle de hello tooopen ensemble.
   
    ![Ouverture de la poignée du PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Figure 4** hello d’ouverture PCM gérer
7. Saisissez la poignée de hello et supprimer hello PCM.
   
    ![Retrait du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Figure 5** suppression hello PCM

## <a name="install-a-replacement-pcm"></a>Installer un PCM de remplacement
Suivez ces instructions de tooinstall un PCM de votre appareil StorSimple. Assurez-vous que vous avez inséré le remplacement de hello tooinstalling préalable hello batterie de secours module PCM (s’applique uniquement les PCM W too764). Pour plus d’informations, consultez Comment trop[supprimer et insérer un module de batterie de secours](storsimple-8000-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall un PCM
1. Vérifiez que vous avez hello PCM de rechange correct pour ce boîtier. boîtier principal de Hello a besoin d’un PCM de 764 W et hello boîtiers doit être un PCM de 580 W. Vous ne devez pas essayer toouse hello PCM de 580 W dans le boîtier principal de hello ou hello de 764 W Bonjour boîtiers. Hello suivant montre l’illustration où tooidentify ces informations sur hello d’étiquette qui est apposée toohello PCM.
   
    ![Étiquette du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Figure 6** : Étiquette du PCM
2. Recherchez le boîtier toohello de dommages, en faisant particulièrement attention toohello connecteurs. 
   
   > [!NOTE]
   > **N’installez pas de module de hello si les broches sont tordues.**
   > 
   > 
3. Ouvrez hello PCM gérer Bonjour position, module de hello diapositive dans boîtier de hello.
   
    ![Installation du PCM de l’appareil](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Figure 7** installation hello PCM
4. Fermez manuellement la poignée PCM hello. Vous devez entendre un clic comme hello loquet de la poignée se met en place.
   
   > [!NOTE]
   > tooensure qui hello connecteur broches, vous pouvez doucement CIL sur hello handle sans libérer le verrou de hello. Si hello PCM sort, cela implique ce verrou hello a été fermé avant des connecteurs hello.
   
5. Se connecter hello câbles toohello power d’alimentation et toohello PCM.
6. Sécuriser les déformation hello dispositif anti-traction de relief.
7. Activez hello PCM.
8. Vérifiez que le remplacement de hello a réussi : Bonjour portail Azure de votre service StorSimple le Gestionnaire de périphériques, accédez à tooyour appareil, puis trop**Paramètres > Analyse > l’intégrité du matériel**. Sous hello **des composants partagés**, état hello Hello PCM doit être verte.
   
   > [!NOTE]
   > Il peut prendre quelques minutes pour initialiser la toocompletely hello remplacement PCM.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).

