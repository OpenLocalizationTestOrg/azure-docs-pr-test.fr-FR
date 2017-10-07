---
title: "aaaReplace un contrôleur StorSimple 8600 EBOD | Documents Microsoft"
description: "Explique comment tooremove et remplacer un ou deux contrôleurs EBOD sur un appareil StorSimple 8600."
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
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Remplacer un contrôleur EBOD sur votre appareil StorSimple

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooreplace un module de contrôleur EBOD défaillant sur votre appareil Microsoft Azure StorSimple. tooreplace un module de contrôleur EBOD, vous devez :

* Supprimer le contrôleur EBOD en panne hello
* Installer un nouveau contrôleur EBOD

Tenez compte des hello informations suivantes avant de commencer :

* Des modules EBOD vides doivent être insérés dans tous les emplacements non utilisés. boîtier de Hello ne se refroidira pas correctement si un emplacement est laissé ouvert.
* le contrôleur EBOD Hello est remplaçables à chaud et peut être supprimé ou remplacé. Ne retirez pas un module défectueux tant que vous ne disposez pas d’un remplacement. Lorsque vous lancez le processus de remplacement hello, vous devez la terminer pendant les 10 minutes.

> [!IMPORTANT]
> Avant de tenter de tooremove ou remplacer n’importe quel composant StorSimple, assurez-vous que vous passez en revue les hello [conventions des icônes de sécurité](storsimple-safety.md#safety-icon-conventions) et d’autres [précautions de sécurité](storsimple-safety.md).

## <a name="remove-an-ebod-controller"></a>Retirer un contrôleur EBOD
Avant de l’échec du module de contrôleur EBOD dans votre appareil StorSimple remplacement hello, assurez-vous que hello autre module de contrôleur EBOD est actif et en cours d’exécution. Hello procédure et le tableau suivants expliquent comment tooremove hello module de contrôleur EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove un module EBOD
1. Ouvrez hello portail Azure.
2. Accédez tooyour appareil et accédez trop**paramètres** > **l’intégrité du matériel**et vérifiez l’état hello du hello DEL de module de contrôleur EBOD actif hello est vert et hello DEL pour hello a échoué Module de contrôleur EBOD est rouge.
3. Localiser le module de contrôleur EBOD hello a échoué à hello arrière appareil de hello.
4. Débranchez les câbles hello qui se connectent hello EBOD module toohello contrôleur avant d’effectuer le module EBOD hello système de hello.
5. Prenez note de hello exact du port SAS du module de contrôleur EBOD hello qui était connecté toohello contrôleur. Vous sera nécessaire toorestore hello système toothis après le remplacement du module EBOD hello.
   
   > [!NOTE]
   > En règle générale, il s’agit du Port A, qui porte le nom **héberger dans** Bonjour suivant schéma.
   
    ![Fond de panier du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Figure 1** : Arrière du module EBOD
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |LED indiquant une panne |
   | 2 |LED d’alimentation |
   | 3 |Connecteurs SaaS |
   | 4 |LED SAS |
   | 5 |Ports série (utilisation en usine uniquement) |
   | 6 |Port A (Entrée hôte) |
   | 7 |Port B (Sortie hôte) |
   | 8 |Port C (utilisation en usine uniquement) |

## <a name="install-a-new-ebod-controller"></a>Installer un nouveau contrôleur EBOD
Hello procédure et le tableau suivants expliquent comment tooinstall un module de contrôleur EBOD dans votre appareil StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall un contrôleur EBOD
1. Vérifiez le périphérique, EBOD hello est endommagé, le connecteur d’interface toohello en particulier. N’installez pas le contrôleur EBOD nouveau hello si des broches sont tordues.
2. Avec les loquets hello Bonjour ouvrez position, module de hello diapositive dans boîtier hello jusqu'à ce que hello loquets s’engagent.
   
    ![Installation du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Figure 2** module de contrôleur EBOD installation Bonjour
3. Verrou de fermer hello. Vous devez entendre un clic comme les verrous hello s’engage.
   
    ![Libération du verrou EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Figure 3** fermeture du verrou du module EBOD hello
4. Rebranchez les câbles hello. Utiliser la configuration exacte hello qui existait avant le remplacement de hello. Consultez hello suivant schéma et de table pour plus d’informations sur la façon de câbles de hello tooconnect.
   
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Figure 4**. Reconnexion des câbles
   
   | Étiquette | Description |
   |:--- |:--- |
   | 1 |Boîtier principal |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Contrôleur 0 |
   | 5 |Contrôleur 1 |
   | 6 |Contrôleur 0 du boîtier EBOD |
   | 7 |Contrôleur 1 du boîtier EBOD |
   | 8 |Boîtier EBOD |
   | 9 |Unités de distribution de l’alimentation |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-8000-hardware-component-replacement.md).

