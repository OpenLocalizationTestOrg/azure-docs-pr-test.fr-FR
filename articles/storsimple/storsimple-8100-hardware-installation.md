---
title: "Appareil d’aaaInstall Microsoft Azure StorSimple 8100 | Documents Microsoft"
description: "Décrit comment toounpack, montage en rack et câbler votre appareil StorSimple 8100 avant de déployer et configurer les logiciels hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Déballer, monter en rack et câbler votre appareil StorSimple 8100
## <a name="overview"></a>Vue d'ensemble
Votre appareil Microsoft Azure StorSimple 8100 doit être monté en rack sur un boîtier unique. Ce didacticiel explique comment toounpack de montage en rack et câble hello périphérique StorSimple 8100 avant de configurer et déployer l’appareil StorSimple hello.

## <a name="unpack-your-storsimple-8100-device"></a>Déballage de votre appareil StorSimple 8100
Hello étapes suivantes fournissent clear, des instructions détaillées sur la façon toounpack votre dispositif de stockage StorSimple 8100. Cet appareil est livré dans un seul carton.

### <a name="prepare-toounpack-your-device"></a>Préparer toounpack votre appareil
Avant de déballer votre appareil, passez en revue hello informations suivantes.

![Icône Avertissement](./media/storsimple-safety/IC740879.png)![icône de poids lourd](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png)**AVERTISSEMENT !**

1. Assurez-vous que vous disposez de deux personnes toomanage disponible hello poids boîtier de hello si vous porter. Un boîtier complet peut peser des too32 kg (70 livres.).
2. Placez la zone de hello sur une surface plane.

Ensuite, effectuez hello suivant les étapes toounpack votre appareil.

#### <a name="toounpack-your-device"></a>toounpack votre appareil
1. Vérifiez que la zone de hello et mousse hello pour eaux, morceaux, l’eau ou tout autre type d’endommagement. Si vous constatez le moindre problème hello carton ou l’emballage, n’ouvrez pas la zone de hello. Veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) toohelp vous évaluez si l’appareil de hello est en état de marche.
2. Décompressez les boîte hello. de votre appareil StorSimple, Hello suivant image affiche hello décompressé.
   
     ![Déballage de votre appareil de stockage](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Vue de votre appareil de stockage déballé**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Carton d’emballage |
   |   2 |Polystyrène de protection inférieur |
   |   3 |Appareil |
   |   4 |Polystyrène de protection supérieur |
   |   5 |Carton contenant les accessoires |
3. Après avoir décompressé le boîte de hello, assurez-vous que vous avez :
   
   * 1 appareil dans son boîtier
   * 2 câbles d’alimentation
   * 1 câble Ethernet croisé
   * 2 câbles de console série
   * 1 convertisseur de série USB pour l’accès en série
   * 1 tournevis T10 inaltérable
   * 4 adaptateurs QSFP-SFP+ à utiliser avec les interfaces réseau 10 GbE
   * 1 kit de montage en rack (2 rails latéraux avec matériel de montage)
   * Documentation de mise en route
     
     Si vous n’avez pas reçu un des éléments hello répertoriées ci-dessus, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).

étape suivante de Hello est toorack monter votre appareil.

## <a name="rack-mount-your-storsimple-8100-device"></a>Montage en rack de votre appareil StorSimple 8100
Suivez hello suivant étapes tooinstall votre dispositif de stockage StorSimple 8100 dans un rack standard de 19 pouces avec avant et arrière publications. le périphérique de Hello StorSimple 8100 comporte un seul boîtier principal.

Hello installation comprend plusieurs étapes, chacune d’elles est décrite dans hello procédures suivantes.

> [!IMPORTANT]
> Les appareils StorSimple doivent être montés en rack pour fonctionner correctement.
> 
> 

### <a name="prepare-hello-site"></a>Préparer le site de hello
périphérique de Hello doit être installé dans un rack standard 19 pouces qui possède à la fois avant et arrière publications. Utilisez hello suivant tooprepare procédure pour l’installation du rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>site de hello tooprepare pour l’installation du rack
1. Assurez-vous que cet appareil hello positionne en toute sécurité sur un travail plat, stable et niveau surface (ou similaire).
2. Vérifiez que site hello où vous avez l’intention tooset d’alimentation standard provenant d’une source indépendante ou une unité de distribution d’alimentation (PDU) rack avec un onduleur (UPS supply).
3. Assurez-vous que cet emplacement une 2U est disponible sur le rack hello dans lequel vous envisagez d’appareil de hello toomount.

![Icône Avertissement](./media/storsimple-safety/IC740879.png)![icône de poids lourd](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png)**AVERTISSEMENT !**

Assurez-vous que vous disposez des poids de hello deux personnes toomanage disponible si vous gérez les paramètres de périphérique hello manuellement. Un boîtier complet peut peser des too32 kg (70 livres.).

### <a name="rack-prerequisites"></a>Configuration requise pour le rack
boîtier de 8100 Hello est conçu pour une installation dans un rack standard de 19 pouces armoire :

* Profondeur minimale de 27,84 pouces d’un rack post toopost.
* Poids maximal de 32 kg pour l’appareil de hello
* Contre-pression maximale de 5 pascals (colonne d’eau de 0,5 mm).

### <a name="rack-mounting-rail-kit"></a>Kit du rail de montage en rack
Un ensemble de rails de montage est fourni pour une utilisation avec l’armoire pour rack de 19 pouces hello. les rails Hello ont été testées poids maximal du boîtier de hello toohandle. Ces rails permettent également l’installation de plusieurs boîtiers sans perte de l’espace dans le rack de hello.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>Appareil de hello tooinstall sur les rails hello
1. Effectuez cette étape uniquement si les rails internes ne sont pas installés sur votre appareil. En règle générale, les rails interne hello sont installés en usine de hello. Si les rails ne sont pas installés, installez les côtés de toohello hello diapositives rails gauche et droit du boîtier hello. Six vis métriques permettent de les fixer de chaque côté. toohelp avec l’orientation, rail hello diapositives sont marqués **LH-Front** et **RH – Front**, et de fin hello correspondant à l’arrière de hello du boîtier de hello est de forme conique.<br/>
   
    ![Attachement de rail diapositives tooenclosure châssis](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Fixation des rails interne diapositives toohello les côtés du boîtier de hello**
   
    Étiquette | Description
    ----- | -----------
    1     | M 3 x 4 vis à tête ronde
    2     | Glissières du châssis

2. Joindre des rails gauche externe de hello et externe droite assemblys toohello rack fixez. Hello sont marqués **LH**, **RH**, et **ce côté de** tooguide vous via hello corriger l’orientation.
3. Localisez les broches hello à hello avant et arrière de l’ensemble de rails hello. Étendre toofit de rail hello entre des publications de rack hello et insérez les broches de hello avant et arrière trous hello. N’oubliez pas que rail hello est.
4. Utiliser deux hello fourni vis toosecure hello rail assembly toohello rack rail aux montants verticaux. Utilisez une vis pour avant de hello et une vis arrière de hello.
5. Répétez ces étapes pour hello autres rails.<br/>
   
     ![Attachement toorack diapositives rail CAB](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Attachement externe assemblys toohello en rack**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Vis de serrage |
   |   2 |Ouverture carrée pour vis du poteau avant du rack |
   |   3 |Ergots de positionnement avant du rail gauche |
   |   4 |Vis de serrage |
   |   5 |Ergots de positionnement arrière du rail gauche |

### <a name="mounting-hello-device-in-hello-rack"></a>Montage appareil hello dans un rack de hello
À l’aide des rails hello que vous venez d’installer, effectuez hello suivant l’appareil de hello toomount étapes dans un rack de hello.

#### <a name="toomount-hello-device"></a>Appareil de hello toomount
1. Avec un assistant, soulever hello boîtier et l’aligner sur les rails de rack hello.
2. Insérez soigneusement les appareil hello dans les rails hello et puis transmettre les appareil hello complètement à rack de hello CAB.<br/>
   
    ![Insérer l’unité dans le rack de hello](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montage appareil hello dans un rack de hello**
3. Supprimez hello gauche et les extrémités de bride avant droit en extrayant des majuscules de hello libres. BRIDE Hello s’enclenchent sur les brides hello.
4. Sécurisez le boîtier hello dans un rack de hello en installant une vis cruciforme fournie chaque bride, gauche et droite.
5. Installer les extrémités de bride hello en appuyant sur les dans la position et de leur alignement en place.<br/>
   
     ![Installation des capuchons d’embase](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Lors de l’installation de bride hello**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Vis de fixation du boîtier |

étape suivante de Hello est toocable votre appareil pour l’alimentation, réseau et accès série.

## <a name="cable-your-storsimple-8100-device"></a>Branchement des câbles de votre appareil StorSimple 8100
Hello procédures suivantes expliquent comment toocable votre appareil StorSimple 8100 d’alimentation, réseau et les connexions séries.

### <a name="prerequisites"></a>Composants requis
Avant de commencer, hello câbler votre appareil, vous devez :

* Votre appareil de stockage, complètement déballé et monté en rack.
* 2 câbles d’alimentation livrés avec votre appareil
* Accès too2 unités d’alimentation (recommandé).
* Câbles réseau
* Câbles série fournis
* Convertisseur série-USB avec le pilote approprié de hello installé sur votre PC (le cas échéant)
* 4 adaptateurs QSFP-SFP+ fournis à utiliser avec les interfaces réseau 10 Gigabit Ethernet
* [Matériel pris en charge pour les interfaces de réseau hello 10 GbE sur votre appareil StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Branchement des câbles d’alimentation
Votre appareil est doté de modules d’alimentation et de refroidissement (PCM) en double. Les deux modules PCM doivent être installés et connecté toodifferent power sources tooensure haut niveau de disponibilité.

Effectuer hello suivant les étapes toocable votre appareil pour l’alimentation.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Branchement des câbles réseau
Votre appareil est une configuration de type actif / passif : à un moment donné, un module de contrôleur est actif et traite toutes les opérations de disque et réseau hello lors de l’autre module de contrôleur est en veille. Si un contrôleur échoue, contrôleur de secours hello est immédiatement activé et continue de toutes les opérations de mise en réseau et disque hello.

toosupport ce basculement de contrôleur redondant, vous devez toocable votre périphérique réseau comme décrit dans hello comme suit.

#### <a name="toocable-for-network-connection"></a>toocable pour la connexion réseau
1. Votre appareil possède six interfaces réseau sur chaque contrôleur : quatre ports Ethernet de 1 Gbit/s et deux de 10 Gbit/s. Identifiez hello diverses données ports hello de fond de panier de votre appareil.
   
    ![Fond de panier de l’appareil 8100](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Arrière appareil hello montrant les ports de données**
   
   | Étiquette | Description |
   | --- | --- |
   |   0/1/4/5 |Interfaces réseau de 1 Gigabit Ethernet |
   |   2/3 |Interfaces réseau de 10 Gigabit Ethernet |
   |   6 |Ports série |
2. Consultez hello suivant le schéma de câblage réseau. (la configuration réseau minimale de hello est indiquée par des lignes bleues pleines. La configuration supplémentaire requise pour une disponibilité et des performances élevées est représentée par des lignes en pointillés.)

    ![Câble réseau de votre appareil 2U](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Branchement des câbles réseau de votre appareil**

   |Étiquette | Description |
   |----- | ----------- |
   | Une    | LAN avec accès à Internet |
   | B    | Contrôleur 0 |
   | C    | PCM 0 |
   | D    | Contrôleur 1 |
   | E    | PCM 1 |
   | F, G | Hôtes |
   | 0-5  | Interfaces réseau |



Lorsque le câblage d’appareil de hello, la configuration minimale hello nécessite :

* Au moins deux interfaces réseau connectées sur chaque contrôleur : l’une pour l’accès au cloud et l’autre pour iSCSI. Hello DATA 0 port est automatiquement activé et configuré via la console série de hello du périphérique de hello. En dehors de DATA 0, un autre port de données doit également toobe configuré via hello portail Azure classic. Dans ce cas, connectez-vous DATA 0 port toohello principal (réseau LAN avec accès à Internet). Hello autres données ports peuvent être connectées segment de réseau local tooSAN/iSCSI du réseau hello, en fonction du rôle de hello destiné.
* Les interfaces identiques de chaque toohello contrôleur connecté même réseau tooensure disponibilité si un basculement de contrôleur. Par exemple, si vous choisissez tooconnect DATA 0 et 3 de données pour un des contrôleurs de hello, vous devez hello tooconnect correspondant DATA 0 et DATA 3 sur hello autre contrôleur.

Gardez à l’esprit la disponibilité et les performances élevées :

* Dans la mesure du possible, configurez une paire d’interface réseau pour l’accès au cloud (1 GbE) et une autre paire pour iSCSI (10 GbE recommandé) sur chaque contrôleur.
* Si possible, connectez-vous interfaces réseau à partir de chaque tootwo différents commutateurs tooensure la disponibilité du contrôleur contre une défaillance du commutateur. Hello illustre hello deux 10 interfaces réseau GbE, DATA 2 et 3 de données, à partir de chaque contrôleur connecté tootwo différents commutateurs.

Pour plus d’informations, consultez toohello **interfaces réseau** sous hello [les exigences de haute disponibilité pour votre appareil StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Si vous utilisez SFP + transmetteurs avec les interfaces réseau 10 GbE, utilisez hello fourni QSFP-SFP + adaptateurs. Pour plus d’informations, consultez trop[matériel pris en charge pour les interfaces de réseau hello 10 GbE sur votre appareil StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Branchement des câbles de port série
Effectuer hello suivant les étapes toocable votre port série.

#### <a name="toocable-for-serial-connection"></a>toocable pour une connexion série
1. Votre appareil possède un port série sur chaque contrôleur, qui est identifié par une icône en forme de clé. Consultez l’illustration toohello Bonjour [câblage réseau](#network-cabling) section ports série de hello toolocate hello de fond de panier de votre appareil.
2. Identifier le contrôleur actif de hello sur votre appareil de fond de panier. Une LED bleue clignotante indique ce contrôleur hello est actif.
3. Utilisez les câbles série hello fourni (si nécessaire, convertisseur hello USB-série de votre ordinateur portable), connectez votre console ou ordinateur (avec l’appareil de toohello d’émulation de terminal) toohello port série du contrôleur actif de hello.
4. Installer des pilotes de série-USB de hello (fournis avec le périphérique de hello) sur votre ordinateur.
5. Configurer la connexion de série hello comme suit : 115 200 bauds, 8 bits de données, 1 bit d’arrêt, pas de parité et contrôle de flux défini tooNone.
6. Vérifiez que hello connexion fonctionne en appuyant sur entrée sur la console de hello. Un menu de la console série doit apparaître.

> [!NOTE]
> **Gestion des pannes**: hello périphérique installé dans un centre de données distant ou dans une salle informatique avec un accès limité, vous assurer que hello connexions série tooboth contrôleurs sont toujours commutateur de console série tooa connectée ou un équipement équivalent. Cela permet de commander à distance hors bande et de prendre en charge les opérations en cas d’interruptions du réseau ou en cas de défaillance inattendue.
> 
> 

Votre appareil est désormais branché à l’alimentation, au réseau et au port série. étape suivante de Hello tooconfigure hello et un logiciel et déployer votre appareil.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[déployer et configurer l’appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).

