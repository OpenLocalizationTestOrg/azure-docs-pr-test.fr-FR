---
title: "aaaTurn votre appareil de série StorSimple 8000 ou désactiver | Documents Microsoft"
description: "Explique comment activer un périphérique qui a été arrêté ou coupure tooturn d’un nouvel appareil StorSimple, et désactiver un périphérique en cours d’exécution."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Activation ou désactivation de votre appareil StorSimple série 8000
## <a name="overview"></a>Vue d'ensemble
L'arrêt d'un appareil Microsoft Azure StorSimple n'est pas requis dans le cadre du fonctionnement normal du système. Toutefois, vous devrez peut-être tooturn sur un nouveau périphérique ou un appareil qui a toobe arrêté. En règle générale, un arrêt est nécessaire dans les cas où vous devez remplacer du matériel défectueux, physiquement déplacer une unité ou mettre un appareil hors service. Ce didacticiel décrit hello requis de mise sous tension et arrêter votre appareil StorSimple dans différents scénarios.

## <a name="turn-on-a-new-device"></a>Activer un nouvel appareil
Hello étapes d’activation sur un appareil StorSimple pourquoi la première fois diffèrent selon que hello périphérique se trouve un 8100 ou un modèle 8600. Hello 8100 possède un boîtier principal, tandis que hello 8600 possède un double boîtier combinant un boîtier principal et un boîtier EBOD. Hello des étapes détaillées pour les deux modèles sont décrites dans les sections suivantes de hello.

* [Nouvel appareil avec boîtier principal uniquement](#new-device-with-primary-enclosure-only)
* [Nouvel appareil avec boîtier EBOD](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Nouvel appareil avec boîtier principal uniquement
modèle de Hello StorSimple 8100 est un appareil à boîtier unique. Votre appareil est doté de modules d’alimentation et de refroidissement (PCM) en double. Les deux modules PCM doivent être installés et connecté toodifferent power sources tooensure haut niveau de disponibilité.

Effectuer hello suivant les étapes toocable votre appareil pour l’alimentation.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Pour les instructions de câblage et la configuration de périphérique terminée, accédez trop[installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md). Assurez-vous que vous suivez les instructions de hello exactement.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Nouvel appareil avec boîtier EBOD
modèle de Hello StorSimple 8600 a un boîtier principal et un boîtier EBOD. Cela nécessite toobe d’unités hello brancher les câbles d’alimentation et de connectivité de SCSI SAS (Serial Attached) ensemble.

Lorsque vous configurez cet appareil pour hello le première fois, effectuez les opérations de hello pour tout d’abord un câblage SAS et les étapes de hello puis terminée pour le câblage d’alimentation.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Pour les instructions de câblage et la configuration de périphérique terminée, accédez trop[installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md). Assurez-vous que vous suivez les instructions de hello exactement.

## <a name="turn-on-a-device-after-shutdown"></a>Activer un appareil après l'arrêt
étapes de Hello d’activation sur un appareil StorSimple après que qu’il a été arrêté sont différentes selon que hello périphérique se trouve un 8100 ou un modèle 8600. Hello 8100 possède un boîtier principal, tandis que hello 8600 possède un double boîtier combinant un boîtier principal et un boîtier EBOD.

* [Appareil avec boîtier principal uniquement](#device-with-primary-enclosure-only)
* [Appareil avec boîtier EBOD](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Appareil avec boîtier principal uniquement
Après un arrêt, utilisez hello suivant la procédure tooturn sur un appareil StorSimple avec un boîtier principal et aucune boîtiers.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn sur un appareil doté d’un boîtier principal uniquement
1. Assurez-vous que les interrupteurs d’alimentation de hello sur les deux d’alimentation et Modules de refroidissement (PCM) sont en position OFF de hello. Si les commutateurs hello ne sont pas en position OFF de hello, puis les retourner toohello OFF position et attendez hello lumières toogo hors tension.
2. Activer sur l’appareil de hello en basculant les interrupteurs d’alimentation hello allumer les deux PCM toohello ON. Appareil de Hello doit s’allumer.
3. Hello cocher suivant tooverify qui hello périphérique est complètement sous tension :
   
   1. Hello OK LED sur les deux modules PCM sont verts.
   2. Hello DEL d’état sur les deux contrôleurs sont vert.
   3. Hello que LED bleue sur l’un des contrôleurs de hello clignote, ce qui indique que ce contrôleur hello est actif.
      
      Si l'une de ces conditions n'est pas respectée, votre appareil n'est pas intègre. Veuillez [contacter le support Microsoft](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Appareil avec boîtier EBOD
Après un arrêt, utilisez hello suivant la procédure tooturn sur un appareil StorSimple avec un boîtier principal et un boîtier EBOD. Exécutez chaque étape dans l'ordre, exactement comme indiqué. Échec toodo donc peut entraîner une perte de données.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn sur un appareil avec un serveur principal et un boîtier EBOD
1. Assurez-vous que hello boîtiers boîtier principal de toohello connecté. Pour plus d'informations, consultez [Installation de votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Assurez-vous que Power hello et Modules de refroidissement (PCM) sur les deux hello EBOD et les boîtiers principales sont en position OFF de hello. Si les commutateurs hello ne sont pas en position OFF de hello, puis les retourner toohello OFF position et attendez hello lumières toogo hors tension.
3. Tension hello boîtiers premier en basculant les interrupteurs d’alimentation hello allumer les deux PCM toohello ON. Hello DEL PCM doit être verte. Une DEL de contrôleur EBOD verte sur cette unité indique que les boîtiers hello est activé.
4. Allumez le boîtier principal de hello en basculant les interrupteurs d’alimentation hello allumer les deux PCM toohello ON. tout système de Hello doit maintenant s’allumer.
5. Vérifiez que hello LED SAS sont verts, ce qui garantit la connexion entre hello boîtiers hello et hello boîtier principal est bonne.

## <a name="turn-on-a-device-after-a-power-loss"></a>Activer un appareil après une panne de courant
Une panne de courant ou une interruption peut entraîner l’arrêt d’un appareil StorSimple. panne d’alimentation Hello peut se produire sur une des alimentations hello ou les deux alimentations. procédure de récupération Hello est différente selon que hello périphérique se trouve un 8100 ou un modèle 8600. Hello 8100 possède un boîtier principal, tandis que hello 8600 possède un double boîtier combinant un boîtier principal et un boîtier EBOD. Cette section décrit la procédure de récupération hello pour chaque scénario.

* [Appareil avec boîtier principal uniquement](#8100)
* [Appareil avec boîtier EBOD](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Appareil avec boîtier principal uniquement <a name="8100">
système de Hello peut poursuivre ses opérations normalement s’il existe tooone de perte d’alimentation des alimentations. Toutefois, tooensure haute disponibilité du périphérique hello, restauration power toohello alimentation dès que possible.

S’il existe une coupure de courant ou d’une coupure de courant sur les deux alimentations, système de hello s’arrête de façon ordonnée et contrôlée. Lorsque l’alimentation de hello est restaurée, système de hello redémarre automatiquement.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Appareil avec boîtier EBOD <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Panne de courant sur une alimentation
système de Hello peut poursuivre ses opérations normalement s’il existe tooone de perte d’alimentation des alimentations sur le boîtier principal de hello ou boîtiers hello. Toutefois, tooensure haute disponibilité de l’appareil de hello, Veuillez restaurer bloc d’alimentation toohello d’alimentation dès que possible.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Panne de courant sur les deux alimentations du boîtier principal et du boîtier EBOD
S’il existe une coupure de courant d’alimentation ou une interruption sur les deux alimentations, hello boîtiers s’arrêtent immédiatement et le boîtier principal de hello va arrêter de façon ordonnée et contrôlée. Lorsque l’alimentation est restaurée, équipement de hello démarrera automatiquement.

Si hello est mis hors tension manuellement, puis prendre hello étapes toorestore power toohello système de suivi.

1. Activez hello boîtiers.
2. Une fois hello boîtiers sur, activez boîtier principal de hello.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Panne de courant sur les deux alimentations du boîtier EBOD
Lorsque vous configurez vos câbles, vous devez vous assurer que hello EBOD n’est jamais connecté tooa uniquement séparer UDA. Si hello EBOD et le boîtier principal ne parviennent pas à hello simultanément, hello système effectuera une récupération.

Si une seule hello boîtiers échoue sur les deux alimentations, système de hello ne récupérera pas automatiquement. Prendre hello suivant les étapes tooturn de système de hello et restaurer l’état intègre tooa :

1. Si le boîtier principal de hello est activée, désactivez d’alimentation et de refroidissement (PCM).
2. Attendez quelques minutes pour tooshut de système de hello vers le bas.
3. Activez hello boîtiers.
4. Une fois hello boîtiers sur, activez boîtier principal de hello.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Activer un périphérique après hello principal et de connexion du boîtier EBOD est perdue
Si la connexion de hello est perdue entre le contrôleur de secours hello et un contrôleur EBOD correspondant de hello, appareil de hello continue toowork. En cas de perte de connexion hello entre le contrôleur actif du système hello et un contrôleur EBOD correspondant de hello, basculement doit se produire et les appareils hello doivent continuer toowork comme d’habitude.

Lorsque les deux câbles SCSI SAS (Serial Attached) sont supprimés ou connexion hello entre hello boîtier EBOD et le boîtier principal de hello est interrompue, hello appareil arrête de fonctionner. À ce stade, effectuer hello comme suit.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn sur l’appareil hello après la perte de connexion
1. Hello accès arrière appareil de hello.
2. Si hello câble SAS entre les boîtiers hello et le boîtier principal de hello est interrompue, toutes les DEL des voies SAS sur hello boîtiers sera désactivée.
3. Arrêter d’alimentation et de refroidissement (PCM) sur les boîtiers hello et le boîtier principal de hello.
4. Attendez que tous les témoins lumineux de hello sur hello arrière les deux boîtiers hello désactiver.
5. Réinsérez les câbles SAS hello et vérifiez qu’il existe une bonne connexion entre les boîtiers hello et le boîtier principal de hello.
6. Tension hello boîtiers premier en basculant les deux position de PCM commutateurs toohello ON.
7. Assurez-vous que les boîtiers hello est sur en vérifiant que les DEL de hello verte est allumée.
8. Allumez le boîtier principal de hello.
9. Assurez-vous que le boîtier principal de hello est sur en vérifiant que la DEL verte du contrôleur de hello est sur.
10. Vérifiez que hello connexion du boîtier EBOD avec un boîtier principal hello est correct en vérifiant que les DEL (quatre par contrôleur EBOD) des voies SAS hello se trouvent tous sur.

> [!IMPORTANT]
> Si les câbles SAS hello sont défectueux ou connexion hello entre hello boîtier EBOD et le boîtier principal de hello n’est pas correcte, lorsque vous activez le système de hello, il passe en mode de récupération. Dans ce cas, veuillez [contacter le support Microsoft](storsimple-8000-contact-microsoft-support.md) .


## <a name="turn-off-a-running-device"></a>Désactiver un appareil en cours d'exécution
Un appareil StorSimple en cours d’exécution peut-être toobe arrêté s’il est déplacé, mettre hors service ou un composant défectueux nécessitant toobe remplacé. étapes de Hello sont différentes selon que l’appareil StorSimple hello est un 8100 ou un modèle 8600. Hello 8100 possède un boîtier principal, tandis que hello 8600 possède un double boîtier combinant un boîtier principal et un boîtier EBOD. Cette section détaille tooshut d’étapes hello vers le bas un périphérique en cours d’exécution.

* [Appareil avec boîtier principal](#8100a)
* [Appareil avec boîtier EBOD](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Appareil avec boîtier principal <a name="8100a">
tooshut bas appareil hello de façon ordonnée et contrôlée, vous pouvez le faire via hello portail Azure classic ou hello Windows PowerShell pour StorSimple. 

> [!IMPORTANT]
> N’arrêtez pas un appareil en cours d’exécution à l’aide du bouton d’alimentation hello sur hello arrière appareil de hello.
> 
> Avant d’arrêter l’appareil de hello, assurez-vous que tous les composants du périphérique hello sont intègres. Dans hello portail Azure classic, accédez trop**périphériques** > **Maintenance** > **état du matériel**et vérifiez l’état de tous les hello composants est vert. Cela est vrai uniquement pour un système sain. Si le système hello est d’arrêt tooreplace un composant défectueux, vous verrez un échec (rouge) ou dégradé (jaune) état de composant respectif hello hello **état du matériel**.
> 
> 

Une fois que vous accédez à hello Windows PowerShell pour StorSimple ou hello portail Azure classic, suivez les étapes de hello dans [arrêter un appareil StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Appareil avec boîtier EBOD <a name="8600a">
> [!IMPORTANT]
> Avant d’arrêter le boîtier principal de hello et boîtiers hello, assurez-vous que tous les composants du périphérique hello sont intègres. Dans l’hello portail Azure, accédez trop**périphériques** > **moniteur** > **l’intégrité du matériel**et vérifiez que tous les composants de hello sont intègres.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut vers le bas un périphérique en cours d’exécution avec boîtier EBOD
1. Suivez toutes les étapes de hello répertoriées dans [arrêter un appareil StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) pour le boîtier principal de hello.
2. Après hello boîtier principal est s’arrête, arrêtez hello EBOD en basculant les commutateurs d’alimentation et de Module de refroidissement (PCM).
3. tooverify qui hello EBOD est arrêté, vérifiez que tous les voyants hello arrière des boîtiers hello sont désactivés.

> [!NOTE]
> câbles SAS Hello boîtier principal toohello du boîtier EBOD tooconnect utilisé hello ne doivent pas être supprimés tant qu’après que hello système est arrêté.

## <a name="next-steps"></a>Étapes suivantes
[Contactez le support Microsoft](storsimple-8000-contact-microsoft-support.md) si vous rencontrez des problèmes lors de l'activation ou l'arrêt d'un appareil StorSimple.

