---
title: "aaaMonitor votre appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple le Gestionnaire de périphériques de service toomonitor l’utilisation, les performances d’e/s et l’utilisation des capacités."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>Utilisez hello le Gestionnaire de périphériques StorSimple service toomonitor votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser des périphériques spécifiques hello le Gestionnaire de périphériques StorSimple service toomonitor au sein de votre solution StorSimple. Vous pouvez créer des graphiques personnalisés basés sur les performances d’e/s, capacité, débit du réseau et les métriques de performances de périphérique et épingler ces tableaux de bord toohello. Pour plus d’informations, consultez trop[personnaliser votre tableau de bord de portail](/articles/azure-portal/azure-portal-dashboards.md).

informations d’analyse tooview hello pour un périphérique spécifique, Bonjour portail Azure, sélectionnez service de gestionnaire de périphériques StorSimple hello. À partir de la liste de hello des périphériques, sélectionnez votre appareil et passez trop**analyse**. Vous pouvez ensuite voir hello **capacité**, **utilisation**, et **performances** des graphiques pour le périphérique sélectionné de hello.

## <a name="capacity"></a>Capacity
**Capacité** pistes hello espace mis en service et du hello restant sur le périphérique de hello. Hello capacité restante est ensuite affichée comme attaché localement ou à plusieurs niveaux.

Hello mis en service et la capacité restante est davantage divisée par les volumes attachés localement et hiérarchisés. Pour chaque volume, hello mis en service la capacité et hello capacité sur l’appareil de hello restante s’affiche.

![Capacité d’E/S](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>Usage
**L’utilisation** montant de toohello connexes assure le suivi des métriques d’espace de stockage utilisé par les volumes hello, conteneurs de volumes ou périphérique. Vous pouvez créer des rapports basés sur l’utilisation des capacités hello de votre stockage principal, votre stockage en cloud ou votre stockage de l’appareil. L’utilisation de la capacité peut être mesurée sur un volume spécifique, un conteneur de volumes spécifique ou tous les conteneurs de volumes.
Par défaut, l’utilisation de hello pour les dernières 24 heures est signalée. Vous pouvez modifier la durée d’hello hello graphique toochange sur le hello utilisation est indiquée en sélectionnant à partir de :
* Dernières 24 heures
* 7 derniers jours
* 30 derniers jours
* 90 derniers jours
* Année dernière


Hello principal, cloud et le stockage local utilisé peuvent être décrite comme suit :

### <a name="primary-storage-usage"></a>Utilisation du stockage principal
Ces graphiques montrent la quantité hello des données écrites tooStorSimple volumes avant hello sont dédupliquées et des données compressées. Vous pouvez afficher hello principal de stockage utilisée par tous les volumes dans un conteneur de volume ou d’un seul volume. stockage principal de Hello utilisé est davantage divisée par principal à plusieurs niveaux de stockage utilisé et principal attaché localement le stockage utilisé.

Hello graphiques suivants montrent les stockage principal hello utilisé pour un appareil StorSimple avant et après la réalisation d’un instantané cloud. Comme il s’agit uniquement des données de volume, un instantané cloud ne doit pas changer de stockage principal de hello. Comme vous pouvez le voir, graphique de hello ne montre aucune différence dans le stockage de plusieurs niveaux ou attaché localement principal hello utilisé à la suite d’un instantané de cloud. instantané de cloud Hello a démarré à environ 11:50 pm sur l’appareil.

![Utilisation de la capacité principale après l’instantané cloud](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

Si vous exécutez maintenant des e/s sur l’appareil StorSimple hello hôte connecté tooyour, vous verrez une augmentation de stockage hiérarchisé principal ou principal localement épinglé en fonction de stockage utilisé sur les volumes (à plusieurs niveaux ou attaché localement) vous écrivez des données hello pour. Vous trouverez ici les graphiques de l’utilisation de stockage principal hello pour un appareil StorSimple. Sur ce périphérique, hôte de StorSimple hello démarré desservant écrit à environ 2 h 30 sur un volume hiérarchisé sur l’unité de hello. Vous pouvez voir pointe hello en hello écriture octets/s correspondant e/s toohello en cours d’exécution sur l’ordinateur hôte de hello.

![Performances avec E/S exécutées sur des volumes hiérarchisés](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

Si vous examinez hello hiérarchisé stockage principal utilisé, qui a augmenté alors que l’utilisation de hello principal attaché localement reste inchangée, qu’il y a aucune écriture pris en charge les volumes toohello attaché localement sur l’appareil de hello.

![Utilisation de la capacité principale lorsque les E/S s’exécutent sur les volumes hiérarchisés](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

Si vous exécutez Update 3 ou une version ultérieure, vous pouvez décomposer l’utilisation des capacités hello stockage principal par un volume individuel, tous les volumes, tous les volumes à plusieurs niveaux et tous les volumes attachés localement comme indiqué ci-dessous. Division par tous les localement les volumes attachés vous permettra de tooquickly vérifier la quantité de niveau de local hello est utilisé.

![Utilisation de la capacité principale pour tous les volumes hiérarchisés](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![Utilisation de la capacité principale pour tous les volumes épinglés localement](./media/storsimple-8000-monitor-device/monitor-usage4.png)

Vous pouvez cliquer sur chaque volume hello dans la liste de hello et d’utilisation correspondante de hello.

![Utilisation de la capacité principale pour tous les volumes épinglés localement](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>Utilisation du stockage cloud
Ces graphiques montrent la quantité hello de stockage cloud utilisé. Les données sont dédupliquées et compressées. Cette quantité inclut les instantanés cloud qui peuvent contenir des données qui ne sont pas reflétées dans un volume principal et qui sont conservées à des fins de rétention obligatoire ou héritée. Vous pouvez comparer hello principal et le cloud stockage consommation chiffres tooget une idée de la réduction des données hello taux, bien que le nombre de hello ne seront pas exact.

Hello graphiques suivants montrent l’utilisation de stockage cloud hello d’un appareil StorSimple lorsqu’un instantané cloud.

* instantané de cloud Hello a démarré à environ 11 h 50 sur l’appareil et vous pouvez voir qu’avant l’instantané de cloud hello, il n’a aucun stockage cloud utilisé. 
* Une fois instantané de cloud hello terminée, l’utilisation du stockage de hello cloud capture des 0,89 go. 
* Pendant l’exécution de capture instantanée de hello cloud, il existe également un pic correspondant Bonjour e/s de périphérique toocloud.

    ![Utilisation du stockage cloud avant l’instantané cloud](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![Utilisation du stockage cloud après l’instantané cloud](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![E/s de toocloud appareil durant un instantané cloud](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>Utilisation du stockage local
Ces graphiques montrent l’utilisation totale de hello pour périphérique hello, qui est supérieur à l’utilisation du stockage principal, car il inclut le niveau de hello SSD linéaire. Ce niveau contient une quantité de données qui existe également sur hello autres niveaux de l’appareil. la capacité de Hello en niveau linéaire de hello SSD apparaissent afin que lors de nouvelles données, les données anciennes hello sont déplacé toohello niveau (moment où il est dédupliqué et compressé) et par la suite toohello cloud.

Au fil du temps, le stockage principal utilisé et local de stockage utilisé augmentera probablement ensemble jusqu'à ce que les données de salutation commencent toobe hiérarchisé toohello cloud. À ce stade, stockage local de hello utilisé commence probablement tooplateau, mais le stockage principal de hello utilisé augmente avec des données sont écrites.

Hello graphiques suivants montrent les stockage principal hello utilisé pour un appareil StorSimple lorsqu’un instantané cloud. instantané de cloud Hello a démarré à 11 h 50 et stockage local de hello démarré diminution à ce moment-là. stockage local de Hello utilisé s’est arrêté à partir de 1.445 Go too1.09 go. Cela indique que très probablement hello des données non compressées dans le niveau SSD linéaire de hello a été dédupliquées, compressées et déplacées dans la couche de disque dur hello. Notez que si l’appareil de hello possède déjà une grande quantité de données hello SSD et des niveaux de disque dur, vous pouvez voir pas cette baisse. Dans cet exemple, le périphérique de hello a une petite quantité de données.

![Utilisation du stockage local après l’instantané cloud](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>Performances
**Performances** suit les mesures liées nombre toohello de lecture et les opérations d’écriture entre iSCSI hello interfaces de l’initiateur sur le serveur hôte de hello hello dispositif ou appareil de hello et nuage de hello. Ces performances peuvent être mesurées pour un volume spécifique, un conteneur de volumes spécifique ou tous les conteneurs de volumes. Performances incluent également l’utilisation du processeur et le débit du réseau pour hello diverses interfaces réseau sur votre appareil.

### <a name="io-performance-for-initiator-toodevice"></a>Performances d’e/s pour l’initiateur toodevice
graphique de Hello ci-dessous montre les e/s de hello pour appareil de tooyour initiateur hello pour tous les volumes hello pour un périphérique de production. les métriques Hello tracées sont lire et écrivent des octets par seconde. Vous pouvez également tracer les E/S de lecture, d’écriture et en attente, ou les latences de lecture et d’écriture.

![Performances d’e/s pour l’initiateur toodevice](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>Performances d’e/s de périphérique toocloud
Pourquoi même périphérique, les opérations d’e/s de hello sont tracées pour les données à partir de hello appareil toohello cloud hello pour tous les hello conteneurs de volumes. Sur ce périphérique, les données de salutation sont uniquement dans la couche de linéaire hello et rien a répandues toohello cloud. Il n’y a aucune opération de lecture-écriture qui se produisent à partir de l’appareil toohello cloud. Par conséquent, les pics de hello dans le graphique de hello sont à un intervalle de 5 minutes correspondant fréquence toohello auquel les pulsations hello sont vérifiée entre l’appareil de hello et service de hello.

Pour hello même périphérique, un instantané cloud a été effectuée pour les données de volume en commençant à 11 h 50. Cela générait des données circulant de hello appareil toohello cloud. Écritures ont été pris en charge toohello cloud pendant cette opération. graphique d’e/s Hello présente un pic instant hello octets/s d’écriture correspondante toohello lorsque hello instantané.

![E/s de toocloud appareil durant un instantané cloud](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>Débit du réseau pour les interfaces réseau de l’appareil
**Débit du réseau** montant de toohello connexes métriques assure le suivi des données transférées de hello iSCSI initiator les interfaces réseau sur le serveur hôte de hello et appareils de hello et entre les appareils hello et de cloud de hello. Vous pouvez surveiller cette mesure pour chacune des interfaces de réseau iSCSI hello sur votre appareil.

Hello après le débit du réseau graphiques afficher hello pour hello Data 0, 1 1 réseau Gigabit Ethernet sur votre appareil, ce qui a été activé pour le cloud (par défaut) et compatible iSCSI. Sur ce périphérique 14 juin à environ 21 h 00, les données a été hiérarchisées en nuage hello (aucun nuage instantanés ont été pris à qui les tootiering points en cours ne hello données de mécanisme toomove hello dans le cloud de hello) qui a entraîné les e/s sont traitées toohello cloud. Il est un pic correspondant dans le graphique de débit réseau hello pour hello même temps et la plupart du trafic réseau de hello est sortant toohello cloud.

![Débit du réseau pour Data 0](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

Si nous examinons le graphique de débit interface hello Data 1, un autre 1 GbE network interface qui était uniquement compatible iSCSI, puis pratiquement pas de trafic réseau est survenu pendant cette opération.

![Débit du réseau pour Data 1](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>Utilisation du processeur pour l’appareil
**L’utilisation du processeur** suit les mesures liées toohello utilisation du processeur sur votre appareil. Hello graphique suivant affiche statistiques de l’utilisation du processeur hello pour un périphérique en production.

![Utilisation du processeur pour l’appareil](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser tableau de bord périphérique hello le Gestionnaire de périphériques StorSimple service](storsimple-device-dashboard.md).
* Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-manager-service-administration.md).

