---
title: "Appareil d’aaaInstall Microsoft Azure StorSimple 8600 | Documents Microsoft"
description: "Décrit comment toounpack, montage en rack et câbler votre appareil StorSimple 8600 avant de déployer et configurer les logiciels hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Déballer, monter en rack et câbler votre appareil StorSimple 8600
## <a name="overview"></a>Vue d'ensemble
Microsoft Azure StorSimple 8600 est un appareil composé d’un boîtier principal et d’un boîtier EBOD. Ce didacticiel explique comment toounpack de montage en rack et câble hello périphérique StorSimple 8600 avant de configurer le logiciel de StorSimple hello.

## <a name="unpack-your-storsimple-8600-device"></a>Déballage de votre appareil StorSimple 8600
Hello étapes suivantes fournissent clear, obtenir des instructions détaillées sur la façon de toounpack votre dispositif de stockage StorSimple 8600. Ce périphérique est livré dans les deux zones, une pour le boîtier principal de hello et l’autre pour hello boîtiers. Ces deux emballages sont ensuite placés dans une seule boîte.

### <a name="prepare-toounpack-your-device"></a>Préparer toounpack votre appareil
Avant de déballer votre appareil, passez en revue hello informations suivantes.

![Icône Avertissement](./media/storsimple-safety/IC740879.png)![icône de poids lourd](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png)**AVERTISSEMENT !**

1. Assurez-vous que vous disposez de deux personnes toomanage disponible hello poids appareil de hello si vous porter. Un boîtier complet peut peser des too32 kg (70 livres.).
2. Placez la zone de hello sur une surface plane.

Ensuite, effectuez hello suivant les étapes toounpack votre appareil.

#### <a name="toounpack-your-device"></a>toounpack votre appareil
1. Vérifiez que la zone de hello et mousse hello pour eaux, morceaux, l’eau ou tout autre type d’endommagement. Si vous constatez le moindre problème hello carton ou l’emballage, n’ouvrez pas la zone de hello. Veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) toohelp vous évaluez si l’appareil de hello est en état de marche.
2. La boîte de hello externe et retirez puis hello deux zones correspondant tooprimary et les boîtiers. Vous pouvez maintenant décompresser hello principal et les boîtiers. Hello figure suivante montre la vue hello décompressé de l’un des boîtiers de hello.
   
    ![Déballage de votre appareil de stockage](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Vue de votre appareil de stockage déballé**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Carton d’emballage |
   |   2 |Câbles SAS (dans le carton des accessoires et des câbles) |
   |   3 |Polystyrène de protection inférieur |
   |   4 |Appareil |
   |   5 |Polystyrène de protection supérieur |
   |   6 |Carton contenant les accessoires |
3. Une fois hello deux boîtiers déballés, vérifiez que vous avez :
   
   * 1 boîtier principal (boîtier principal de hello et le boîtier EBOD se trouvent dans des colis séparés)
   * 1 boîtier EBOD
   * 4 câbles d’alimentation, 2 dans chaque carton
   * 2 câbles SAS (boîtier tooEBOD boîtier principal tooconnect hello)
   * 1 câble Ethernet croisé
   * 2 câbles de console série
   * 1 convertisseur de série USB pour l’accès en série
   * 4 adaptateurs QSFP-SFP+ à utiliser avec les interfaces réseau 10 Gigabit Ethernet
   * 2 kits de montage (4 rails latéraux avec le matériel, 2 pour chaque boîtier principal de hello et le boîtier EBOD de montage), rack 1 dans chaque zone.
   * Documentation de mise en route
     
     Si vous n’avez pas reçu un des éléments hello répertoriées ci-dessus, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md).  

étape suivante de Hello est toorack monter votre appareil.

## <a name="rack-mount-your-storsimple-8600-device"></a>Montage en rack de votre appareil StorSimple 8600
Suivez hello suivant étapes tooinstall votre dispositif de stockage StorSimple 8600 dans un rack standard de 19 pouces avec avant et arrière publications. Cet appareil est fourni avec deux boîtiers : un boîtier principal et un boîtier EBOD. Les deux boîtiers doivent toobe monté en rack.

Hello installation comprend plusieurs étapes, chacune d’elles est décrite dans hello procédures suivantes.

> [!IMPORTANT]
> Les appareils StorSimple doivent être montés en rack pour fonctionner correctement.
> 
> 

### <a name="site-preparation"></a>Préparation du site
les boîtiers Hello doivent être installés dans un rack standard 19 pouces qui possède à la fois avant et arrière publications. Utilisez hello suivant tooprepare procédure pour l’installation du rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>site de hello tooprepare pour l’installation du rack
1. Vérifiez que hello principal et les boîtiers sont repos en toute sécurité sur une surface plane, stable et niveau de travail (ou similaire).
2. Vérifiez que ce site hello où vous avez l’intention tooset des a CA standard d’alimentation à partir d’une source indépendante ou d’un unité de Distribution d’alimentation (PDU) du rack avec un onduleur (UPS).
3. Assurez-vous qu’un 4U (2 X 2U) est disponible sur le rack hello dans lequel vous avez l’intention de boîtiers de hello toomount.

![Icône Avertissement](./media/storsimple-safety/IC740879.png)![icône de poids lourd](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png)**AVERTISSEMENT !**

 Assurez-vous que vous disposez des poids de hello deux personnes toomanage disponible si vous gérez les paramètres de périphérique hello manuellement. Un boîtier complet peut peser des too32 kg (70 livres.).

### <a name="rack-prerequisites"></a>Configuration requise pour le rack
les boîtiers Hello sont conçus pour une installation dans un rack standard de 19 pouces armoire :

* Profondeur minimale de 27,84 pouces d’un rack valider toopost
* Poids maximal de 32 kg pour l’appareil de hello
* Contre-pression maximale de 5 pascals (colonne d’eau de 0,5 mm)

### <a name="rack-mounting-rail-kit"></a>Kit du rail de montage en rack
Un ensemble de rails de montage sera fourni pour une utilisation avec l’armoire pour rack de 19 pouces hello. les rails Hello ont été testées poids maximal du boîtier de hello toohandle. Ces rails permettent également l’installation de plusieurs boîtiers sans perte de l’espace dans le rack de hello. Installez d’abord les boîtiers hello.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>tooinstall hello boîtiers sur les rails hello
1. Effectuez cette étape uniquement si les rails internes ne sont pas installés sur votre appareil. En règle générale, les rails interne hello sont installés en usine de hello. Si les rails ne sont pas installés, installez les côtés de toohello hello diapositives rails gauche et droit du boîtier hello. Six vis métriques permettent de les fixer de chaque côté. toohelp avec l’orientation, rail hello diapositives sont marqués **LH-Front** et **RH – Front**, et de fin hello correspondant à l’arrière de hello du boîtier de hello est de forme conique.
   
    ![Attachement de rail diapositives tooenclosure châssis](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Attachement de rail diapositives toohello les côtés du boîtier de hello**
   
   | Étiquette | Description |
   | --- | --- |
   |  1 |M 3 x 4 vis à tête ronde |
   |  2 |Glissières du châssis |
2. Attachez les rails gauche hello et le côté droit assemblys toohello rack fixez. Hello sont marqués **LH**, **RH**, et **ce côté de** tooguide vous guident dans l’orientation appropriée.
3. Localisez les broches hello à hello avant et arrière de l’ensemble de rails hello. Étendre toofit de rail hello entre des publications de rack hello et insérez les broches hello hello avant et arrière rack trous. N’oubliez pas que rail hello est.
4. Sécuriser hello assembly toohello en rack rail aux montants verticaux à l’aide des deux vis hello fourni. Utilisez une vis pour avant de hello et une vis arrière de hello.
5. Répétez ces étapes pour hello autres rails.
   
     ![Attachement toorack diapositives rail CAB](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Attachement assemblys toohello en rack**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Vis de serrage |
   |   2 |Ouverture carrée pour vis du poteau avant du rack |
   |   3 |Ergots de positionnement du rail avant gauche |
   |   4 |Vis de serrage |
   |   5 |Ergots de positionnement du rail arrière gauche |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Le montage de boîtiers hello dans un rack de hello
À l’aide des rails hello que vous venez d’installer, effectuez hello suivant boîtiers des hello de toomount des étapes dans un rack de hello.

#### <a name="toomount-hello-ebod-enclosure"></a>toomount hello boîtiers
1. Avec un assistant, soulever hello boîtier et l’aligner sur les rails de rack hello.
2. Insérez soigneusement boîtier de hello dans les rails hello et puis poussez-le rack de hello CAB.
   
    ![Insérer l’unité dans le rack de hello](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Le montage du boîtier hello dans un rack de hello**
3. Supprimez hello gauche et les extrémités de bride avant droit en extrayant des majuscules de hello libres. BRIDE Hello s’enclenchent sur les brides hello.
4. Sécurisez le boîtier de hello en rack de hello en installant une vis cruciforme fournie chaque bride, gauche et droite.
5. Installer les extrémités de bride hello en appuyant sur les dans la position et de leur alignement en place.
   
     ![Installation des capuchons d’embase](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Lors de l’installation de bride hello**
   
   | Étiquette | Description |
   | --- | --- |
   |   1 |Vis de fixation du boîtier |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Le montage du boîtier principal de hello dans un rack de hello
Après avoir fini de boîtiers hello de montage, vous devez boîtier principal de hello toomount suivant hello les mêmes étapes.

> [!NOTE]
> * Il est possible toohave quelques emplacements vides dans hello en rack entre le boîtier principal hello et les boîtiers hello.
> * Utilisez hello fourni 2m SAS câble tooconnect hello boîtier principal toohello boîtiers.
> * Il n’y a aucune contrainte de placement relatif de hello de hello principal toohello EBOD d’unité. Par conséquent, le boîtier principal de hello peut être placé dans l’emplacement du haut hello et boîtiers hello ci-dessous, ou vice versa.
> 
> 

étape suivante de Hello est toocable votre appareil pour l’alimentation, réseau et accès série.

## <a name="cable-your-storsimple-8600-device"></a>Branchement des câbles de votre appareil StorSimple 8600
Hello procédures suivantes expliquent comment toocable votre appareil StorSimple 8600 d’alimentation, réseau et les connexions séries.

### <a name="prerequisites"></a>Composants requis
Avant de commencer, toocable votre appareil, vous devez :

* Votre boîtier principal et les boîtiers de hello, entièrement déballés
* 4 câbles d’alimentation (2 pour chaque hello principal et hello boîtiers) fournie avec votre appareil
* 2 câbles SAS fournis avec hello tooconnect de périphérique hello boîtier principal de toohello de boîtier EBOD
* Accès too2 unités d’alimentation (PDU) (recommandé)
* Câbles réseau
* Câbles série fournis
* Convertisseur série-USB et hello de pilote approprié installé sur votre PC (le cas échéant)
* 4 adaptateurs QSFP-SFP+ fournis à utiliser avec les interfaces réseau 10 Gigabit Ethernet
* [Matériel pris en charge pour les interfaces de réseau hello 10 GbE sur votre appareil StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>Branchement des câbles d’alimentation et SAS
Votre appareil possède un boîtier principal et un boîtier EBOD. Cela nécessite toobe d’unités hello brancher les câbles d’alimentation et de connectivité de SCSI SAS (Serial Attached) ensemble.

Lorsque vous configurez cet appareil pour hello le première fois, effectuez les opérations de hello pour tout d’abord un câblage SAS et les étapes de hello puis terminée pour le câblage d’alimentation.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Branchement des câbles réseau
Votre appareil est dans une configuration de type actif / passif : à un moment donné, un module de contrôleur est actif et traite toutes les opérations de disque et réseau hello lors de l’autre module de contrôleur est en veille. En cas d’une défaillance du contrôleur, contrôleur de secours hello active et continue de toutes les opérations de mise en réseau et disque hello immédiatement.

toosupport ce basculement de contrôleur redondant, vous devez toocable votre périphérique réseau comme indiqué dans hello comme suit.

#### <a name="toocable-for-network-connection"></a>toocable pour la connexion réseau
1. Votre appareil possède six interfaces réseau sur chaque contrôleur : quatre ports Ethernet de 1 Gbit/s et deux de 10 Gbit/s. Consultez toohello suivant des ports de données d’illustration tooidentify hello hello de fond de panier de votre appareil.
   
     ![Fond de panier de l’appareil 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Arrière de l’appareil montrant hello ports de données**
   
   | Étiquette | Description |
   | --- | --- |
   |   0/1/4/5 |Interfaces réseau de 1 Gigabit Ethernet |
   |   2/3 |Interfaces réseau de 10 Gigabit Ethernet |
   |   6 |Ports série |
2. Consultez hello suivant le schéma de câblage réseau. (la configuration réseau minimale de hello est indiquée par des lignes bleues pleines. Pour une haute disponibilité et des performances, la configuration supplémentaire requise est représentée par des lignes en pointillés.)

![Câble réseau de votre appareil 4U](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Branchement des câbles réseau de votre appareil**

| Étiquette | Description |
| --- | --- |
| Une |LAN avec accès à Internet |
| B |Contrôleur 0 |
| C |PCM 0 |
| D |Contrôleur 1 |
| E |PCM 1 |
| F |Contrôleur 0 du boîtier EBOD |
| G |Contrôleur 1 du boîtier EBOD |
| H/I |Hôtes (par exemple, les serveurs de fichiers) |
| 0-5 |Interfaces réseau |
| 6 |Boîtier principal |
| 7 |Boîtier EBOD |

Lorsque le câblage d’appareil de hello, la configuration minimale hello nécessite :

* Au moins deux interfaces réseau connectées sur chaque contrôleur : l’une pour l’accès au cloud et l’autre pour iSCSI. Hello DATA 0 port est automatiquement activé et configuré via la console série de hello du périphérique de hello. En dehors de DATA 0, un autre port de données doit également toobe configuré via hello portail Azure classic. Dans ce cas, connectez-vous DATA 0 port toohello principal (réseau LAN avec accès à Internet). Hello autres données ports peuvent être connectées segment de réseau local tooSAN/iSCSI du réseau hello, en fonction du rôle de hello destiné.
* Les interfaces identiques de chaque toohello contrôleur connecté même réseau tooensure disponibilité si un basculement de contrôleur. Par exemple, si vous choisissez tooconnect DATA 0 et 3 de données pour un des contrôleurs de hello, vous devez hello tooconnect correspondant DATA 0 et DATA 3 sur hello autre contrôleur.

Gardez à l’esprit la disponibilité et les performances élevées :

* Dans la mesure du possible, configurez une paire d’interface réseau pour l’accès au cloud (1 GbE) et une autre paire pour iSCSI (10 GbE recommandé) sur chaque contrôleur.
* Si possible, connectez-vous interfaces réseau à partir de chaque tootwo différents commutateurs tooensure la disponibilité du contrôleur contre une défaillance du commutateur. Hello illustre hello deux 10 interfaces réseau GbE, DATA 2 et 3 de données, à partir de chaque contrôleur connecté tootwo différents commutateurs. Pour plus d’informations, consultez toohello **interfaces réseau** sous hello [les exigences de haute disponibilité pour votre appareil StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Si vous utilisez SFP + transmetteurs avec les interfaces réseau 10 GbE, utilisez hello fourni QSFP-SFP + adaptateurs. Pour plus d’informations, consultez trop[matériel pris en charge pour les interfaces de réseau hello 10 GbE sur votre appareil StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Branchement des câbles de port série
Effectuer hello suivant les étapes toocable votre port série.

#### <a name="toocable-for-serial-connection"></a>toocable pour une connexion série
1. Votre appareil possède un port série sur chaque contrôleur, qui est identifié par une icône en forme de clé. ports série de toolocate hello, voir la rubrique illustration toohello des ports de données hello sur hello arrière de l’appareil.
2. Identifier le contrôleur actif de hello sur votre appareil de fond de panier. Une LED bleue clignotante indique ce contrôleur hello est actif.
3. Utilisez hello fourni le câble série (si nécessaire, convertisseur hello USB-série de votre ordinateur portable) et connectez votre console ou ordinateur (avec l’appareil de toohello d’émulation de terminal) toohello port série du contrôleur actif de hello.
4. Installer des pilotes de série-USB de hello (fournis avec le périphérique de hello) sur votre ordinateur.
5. Vous pouvez configurer la connexion de série hello comme suit :
   
   * 115 200 bauds
   * 8 bits de données
   * 1 bit d’arrêt
   * Aucune parité
   * Flux de contrôle défini trop**None**
6. Vérifiez que hello connexion fonctionne en appuyant sur entrée sur la console de hello. Un menu de la console série doit apparaître.

> [!NOTE]
> **Gestion des pannes :** lors de l’appareil de hello est installé dans un centre de données distant ou dans une salle informatique avec un accès limité, assurez-vous que hello connexions série tooboth contrôleurs sont toujours commutateur de console série tooa connectée ou un équipement équivalent. Cela permet de commander à distance hors bande et de prendre en charge les opérations en cas d’interruption du réseau ou en cas de défaillance inattendue.
> 
> 

Vous avez terminé le câblage d’alimentation, l’accès réseau, et étape suivante de série connection.hello est un logiciel de hello tooconfigure sur votre appareil.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt trop[déployer et configurer l’appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).

