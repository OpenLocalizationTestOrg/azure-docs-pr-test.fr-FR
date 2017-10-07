---
title: aaaMonitor votre appareil StorSimple | Documents Microsoft
description: "Décrit comment toouse hello performances toomonitor d’e/s du service StorSimple Manager, utilisation de la capacité, débit du réseau et les performances du périphérique."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>Utilisez hello StorSimple Manager service toomonitor votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser des périphériques spécifiques hello StorSimple Manager service toomonitor au sein de votre solution StorSimple. Vous pouvez créer des graphiques personnalisés basés sur les performances E/S, l’utilisation de la capacité, le débit du réseau et les mesures de performances de l’appareil. 

hello tooview informations pour un périphérique spécifique, Bonjour portail Azure classic, le service StorSimple Manager hello select d’analyse. Cliquez sur hello **moniteur** onglet, puis dans la liste des appareils hello. Hello **moniteur** page contient des informations suivantes de hello.

## <a name="io-performance"></a>Performances E/S
**Les performances d’e/s** suit les mesures liées nombre toohello de lecture et les opérations d’écriture entre iSCSI hello interfaces de l’initiateur sur le serveur hôte de hello hello dispositif ou appareil de hello et nuage de hello. Ces performances peuvent être mesurées pour un volume spécifique, un conteneur de volumes spécifique ou tous les conteneurs de volumes.

graphique de Hello ci-dessous montre les e/s de hello pour appareil de tooyour initiateur hello pour tous les volumes hello pour un périphérique de production. métriques Hello tracées sont en lecture et écrivent d’octets par seconde, lire et écrire des opérations d’e/s par seconde et lire et latences d’écriture.

![Performances d’e/s à partir de l’initiateur toodevice](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Pourquoi même périphérique, les opérations d’e/s de hello sont tracées pour les données à partir de hello appareil toohello cloud hello pour tous les hello conteneurs de volumes. Sur ce périphérique, les données de salutation sont uniquement dans la couche de linéaire hello et rien a répandues toohello cloud. Il n’y a aucune opération de lecture-écriture qui se produisent à partir de l’appareil toohello cloud. Par conséquent, les pics de hello dans le graphique de hello sont à un intervalle de 5 minutes correspondant fréquence toohello auquel les pulsations hello sont vérifiée entre l’appareil de hello et service de hello. 

![Performances des e/s du périphérique toocloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Pour hello même périphérique, un instantané cloud a été effectuée pour les données de volume en commençant à 2 h 00. Cela générait des données circulant de hello appareil toohello cloud. Opérations de lecture-écriture ont été pris en charge toohello cloud pendant cette opération. Hello e/s graphique indique un pic dans hello diverses métriques correspondant temps toohello lorsque hello instantané. 

![Performances d’e/s de périphérique toocloud après un instantané cloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Utilisation de la capacité
**Utilisation de la capacité** montant de toohello connexes assure le suivi des métriques d’espace de stockage utilisé par les volumes hello, conteneurs de volumes ou périphérique. Vous pouvez créer des rapports basés sur l’utilisation des capacités hello de votre stockage principal, votre stockage en cloud ou votre stockage de l’appareil. L’utilisation de la capacité peut être mesurée sur un volume spécifique, un conteneur de volumes spécifique ou tous les conteneurs de volumes.

Hello principal cloud et capacité de stockage d’appareil peuvent être décrite comme suit :

### <a name="primary-storage-capacity-utilization"></a>Utilisation de la capacité de stockage principal
Ces graphiques montrent la quantité hello des données écrites tooStorSimple volumes avant hello sont dédupliquées et des données compressées. Vous pouvez afficher l’utilisation du stockage principal hello par tous les volumes ou d’un seul volume.

Lorsque vous affichez des graphiques de l’utilisation de capacité hello stockage principal volume pour tous les volumes par rapport à chacun des volumes individuels de hello et additionner des données primaires de hello dans ces deux cas, il existe peut-être une incompatibilité entre deux nombres de hello. Hello totale des données primaires sur tous les volumes ne peuvent pas ajouter des toohello la somme totale de données des volumes hello hello. Cela peut être dû tooone suivants de hello :

* **Données d’instantané incluses pour tous les volumes**: ce comportement se produit uniquement si vous utilisez une version antérieure à Update 3. données primaires de Hello affichées pour tous les volumes hello sont sum hello de hello de données principal pour chaque volume et les données de capture instantanée de hello. données primaires de Hello indiquées pour un volume donné correspondant la quantité de hello tooonly de données allouées sur le volume de hello (et n’incluent pas les données d’instantanés de volume correspondant hello).
  
    Cela peut également s’expliquer par hello suivant l’équation :
  
    *Données principales (tous les volumes) = Somme (données principales (volume i) + volume de données d’instantané (volume i))*
  
    *WHERE, de données primaire (volume i) = taille de données principal allouées toovolume i*
  
    Si les instantanés hello sont supprimés via le service de hello, suppression de hello est effectuée de manière asynchrone en arrière-plan de la hello. Il peut prendre un certain temps pour hello volume données taille toobe mis à jour après la suppression de l’instantané hello. 
  
    Si l’exécution de Update 3 ou version ultérieure, données d’instantané hello ne sont pas incluses dans les données de volume hello. Et l’utilisation du principal de hello est calculé comme suit :
  
    Données principales (tous les volumes) = Somme (données principales (volume i)
  
    *WHERE, de données primaire (volume i) = taille de données principal allouées toovolume i*
* **Volumes avec l’analyse désactivée inclus dans tous les volumes**: Si vous avez des volumes sur votre appareil pour lequel la surveillance est désactivée, hello données d’analyse de ces volumes individuels ne sera pas disponible dans les graphiques de hello. Toutefois, les données de salutation pour tous les volumes dans le graphique de hello incluent les volumes de hello pour lequel la surveillance est désactivée. 
* **Supprimer des volumes avec les sauvegardes associées dynamiques inclus pour tous les volumes**: si volumes contenant des données de l’instantané sont supprimés mais les instantanés hello associé existent toujours, vous pouvez voir une incompatibilité.
* **Volumes supprimés inclus pour tous les volumes**: dans certains cas, les anciens volumes peuvent exister même si ceux-ci ont été supprimés. effet Hello de suppression n’est pas visible et les appareils hello peuvent afficher moins de la capacité disponible. Vous devez tooremove de Support technique de Microsoft toocontact ces volumes.

Hello graphiques suivants montrent hello stockage principal l’utilisation des capacités d’un périphérique StorSimple avant et après la réalisation d’un instantané cloud. Comme il s’agit uniquement des données de volume, un instantané cloud ne doit pas changer de stockage principal de hello. Comme vous pouvez le voir, graphique de hello ne montre aucune différence dans hello principal l’utilisation des capacités à la suite d’un instantané de cloud. instantané de cloud Hello démarré à environ 2 h 00 sur l’appareil.

![Utilisation de la capacité principale avant l’instantané cloud](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Utilisation de la capacité principale après l’instantané cloud](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Si vous exécutez Update 2 ou une version ultérieure, vous pouvez décomposer l’utilisation des capacités hello stockage principal par un volume individuel, tous les volumes, tous les volumes à plusieurs niveaux et tous les volumes attachés localement comme indiqué ci-dessous. Division par tous les localement les volumes attachés vous permettra de tooquickly vérifier la quantité de niveau de local hello est utilisé.

![Utilisation de la capacité principale pour tous les volumes épinglés localement](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Utilisation de la capacité de stockage dans le cloud
Ces graphiques montrent la quantité hello de stockage cloud utilisé. Les données sont dédupliquées et compressées. Cette quantité inclut les instantanés cloud qui peuvent contenir des données qui ne sont pas reflétées dans un volume principal et qui sont conservées à des fins de rétention obligatoire ou héritée. Vous pouvez comparer hello principal et le cloud stockage consommation chiffres tooget une idée de la réduction des données hello taux, bien que le nombre de hello ne seront pas exact. Hello graphiques suivants montrent hello cloud capacité l’utilisation du stockage d’un appareil StorSimple avant et après la réalisation d’un instantané cloud. Hello instantané cloud a démarré à environ 2:00 pm sur l’appareil et que l’utilisation des capacités hello cloud sont passées au hello même temps, augmentant de 5.73 Mo too4.04 Go.

![Utilisation de la capacité cloud avant l’instantané cloud](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Utilisation de la capacité cloud après l’instantané cloud](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Utilisation de la capacité de stockage de l’appareil
Ces graphiques montrent l’utilisation totale de hello pour périphérique hello, qui est supérieur à l’utilisation du stockage principal, car il inclut le niveau de hello SSD linéaire. Ce niveau contient une quantité de données qui existe également sur hello autres niveaux de l’appareil. la capacité de Hello en niveau linéaire de hello SSD apparaissent afin que lors de nouvelles données, les données anciennes hello sont déplacé toohello niveau (moment où il est dédupliqué et compressé) et par la suite toohello cloud.

Au fil du temps, l’utilisation des capacités principal et l’utilisation des capacités appareil augmentera probablement ensemble jusqu'à ce que les données de salutation commencent toobe hiérarchisé toohello cloud. À ce stade, l’utilisation des capacités hello périphérique commence probablement tooplateau, mais augmente l’utilisation des capacités principales hello que davantage de données est écrites.

Hello graphiques suivants montrent hello stockage principal l’utilisation des capacités d’un périphérique StorSimple avant et après la réalisation d’un instantané cloud. instantané de cloud Hello démarré à 2 h 00 et l’utilisation des capacités hello périphérique démarré diminution à ce moment-là. capacité de stockage de périphérique Hello s’est arrêté à partir de 11.58 Go too7.48 Go. Cela indique que très probablement hello des données non compressées dans le niveau SSD linéaire de hello a été dédupliquées, compressées et déplacées dans la couche de disque dur hello. Notez que si l’appareil de hello possède déjà une grande quantité de données hello SSD et des niveaux de disque dur, vous pouvez voir pas cette baisse. Dans cet exemple, le périphérique de hello a une petite quantité de données.

![Utilisation de la capacité de l’appareil avant l’instantané cloud](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Utilisation de la capacité de l’appareil après l’instantané cloud](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Débit du réseau
**Débit du réseau** montant de toohello connexes métriques assure le suivi des données transférées de hello iSCSI initiator les interfaces réseau sur le serveur hôte de hello et appareils de hello et entre les appareils hello et de cloud de hello. Vous pouvez surveiller cette mesure pour chacune des interfaces de réseau iSCSI hello sur votre appareil.

Hello suivant le débit du réseau graphiques afficher hello pour hello Data 0 et 4 de données, les deux interfaces de réseau 1 Gigabit Ethernet sur votre appareil. Dans le cas présent, le cloud a été activé pour Data 0, et iSCSI a été activé pour Data 4. Vous pouvez voir les deux hello entrants et hello le trafic sortant de votre appareil StorSimple. ligne plate Hello graphique hello depuis 24 h est en raison de faits toohello que nous collecter des données uniquement toutes les 5 minutes et doit être ignorées. 

![Débit du réseau pour Data 4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Débit du réseau pour Data 4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Performances de l’appareil
**Performances de l’appareil** suit les mesures liées toohello les performances de votre appareil. Hello graphique suivant affiche statistiques de l’utilisation du processeur hello pour un périphérique en production.

![Utilisation du processeur pour l’appareil](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le tableau de bord du périphérique de service hello StorSimple Manager](storsimple-device-dashboard.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

