---
title: "la base de données aaaDesign et implémenter Oracle sur Azure | Documents Microsoft"
description: "Concevez et implémentez une base de données Oracle dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Concevoir et implémenter une base de données Oracle dans Azure

## <a name="assumptions"></a>Hypothèses

- Vous avez l’intention toomigrate une base de données Oracle locale tooAzure.
- Avoir une vision des hello diverses mesures dans les rapports d’Oracle anticipé.
- Vous avez une connaissance élémentaire des performances d’application et de l’utilisation de la plateforme.

## <a name="goals"></a>Objectifs

- Comprendre comment toooptimize votre déploiement Oracle dans Azure.
- Explorer les options de réglage des performances d’une base de données Oracle dans un environnement Azure

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Hello les différences entre un site local et l’implémentation de Azure 

Voici quelques importantes tookeep choses à l’esprit lorsque vous effectuez une migration tooAzure des applications sur site. 

L’une des principales différences est que, dans une implémentation Azure, les ressources, telles que les machines virtuelles, les disques et les réseaux virtuels, sont partagées avec les autres clients. En outre, les ressources peuvent être limités selon les spécifications de hello. Au lieu de se concentrer sur ce qui évite l’échec (MTBF), Azure plus focu est sur le survivant d’échec de hello (fonction).

Hello tableau suivant répertorie quelques-unes des différences de hello entre une implémentation locale et l’implémentation Azure de base de données Oracle.

> 
> |  | **Implémentation locale** | **Implémentation Azure** |
> | --- | --- | --- |
> | **Mise en réseau** |LAN/WAN  |SDN (Software-Defined Networking)|
> | **Groupe de sécurité** |Outils de restriction d’adresse IP/de port |[Groupe de sécurité réseau](https://azure.microsoft.com/blog/network-security-groups) |
> | **Résilience** |MTBF (temps moyen entre les défaillances) |Rationaliser (durée moyenne toorecovery)|
> | **Maintenance planifiée** |Correctifs/mises à niveau|[Groupes à haute disponibilité](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (correctifs/mises à niveau gérés par Azure) |
> | **Ressource** |Dédié  |Partagée avec d’autres clients|
> | **Régions** |Centres de données |[Paires de régions](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Stockage** |SAN/disques physiques |[Stockage géré par Azure](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Mettre à l'échelle** |Mise à l’échelle verticale |Mise à l’échelle horizontale|


### <a name="requirements"></a>Configuration requise

- Déterminer le taux de croissance et de la taille de base de données hello.
- Déterminez les spécifications d’IOPS hello, qui vous pouvez estimer basé sur Oracle anticipé des rapports ou d’autres outils d’analyse de réseau.

## <a name="configuration-options"></a>Options de configuration

Il existe quatre zones potentiels que vous pouvez régler les performances de tooimprove dans un environnement Azure :

- Taille de la machine virtuelle
- Débit du réseau
- Types de disque et configurations
- Paramètres de cache des disques

### <a name="generate-an-awr-report"></a>Générer un rapport AWR

Si vous avez une base de données Oracle existant et que vous envisagez de toomigrate tooAzure, vous disposez de plusieurs options. Vous pouvez exécuter hello Oracle anticipé rapport tooget hello métriques (IOPS, Mbits/s, GiBs et ainsi de suite). Choisissez ensuite hello que machine virtuelle basée sur des métriques hello que vous avez collectées. Ou vous pouvez contacter votre infrastructure équipe tooget des informations similaires.

Pour comparer, vous pouvez exécuter votre rapport AWR lors de charges de travail normales et maximales. En fonction de ces rapports, vous pouvez redimensionner hello machines virtuelles en fonction de la charge de travail moyenne hello ou de charge de travail maximale hello.

Voici un exemple d’un rapport anticipé de toogenerate :

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Mesures clés

Voici les métriques hello que vous pouvez obtenir à partir de hello les rapports anticipé :

- Nombre total de cœurs
- Vitesse d’horloge du processeur
- Quantité totale de mémoire en Go
- Utilisation du processeur
- Taux maximal de transfert de données
- Taux de modification d’E/S (lecture/écriture)
- Taux d’enregistrement de la restauration par progression (Mbits/s)
- Débit du réseau
- Taux de latence réseau (élevée/basse)
- Taille de la base de données en Go
- Octets reçus via SQL * Net / tooclient

### <a name="virtual-machine-size"></a>Taille de la machine virtuelle

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Estimer la taille de machine virtuelle sur l’utilisation du processeur, mémoire et d’e/s de hello anticipé rapport dynamique

Vous pouvez examiner est hello cinq principaux a dépassé le délai de premier plan événements qui indiquent où se trouvent les goulots d’étranglement de hello système.

Par exemple, Bonjour suivant schéma, synchronisation de fichier journal hello est haut hello. Il indique le nombre de hello d’attentes qui sont nécessaires avant que hello LGWR écrit le fichier journal de la restauration par progression hello journal tampon toohello. Ces résultats indiquent qu’un stockage ou des disques plus performants sont nécessaires. En outre, le diagramme de hello montre également nombre hello du processeur (cœurs) et hello de mémoire.

![Capture d’écran de la page de rapport hello anticipé](./media/oracle-design/cpu_memory_info.png)

Hello diagramme suivant montre hello une total d’e/s de lecture et d’écriture. Comportaient 59 Lisez et 247.3 Go écrite au moment de hello du rapport de hello.

![Capture d’écran de la page de rapport hello anticipé](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Choisir une machine virtuelle

Selon les informations de hello que vous avez recueillies à partir de hello les rapports anticipé, étape suivante de hello est toochoose une machine virtuelle de taille similaire qui répond à vos besoins. Vous trouverez une liste des machines virtuelles disponibles dans l’article de hello [optimisées en mémoire](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Ajuster le dimensionnement de machine virtuelle hello avec une série de machine virtuelle similaire selon hello ACU

Une fois que vous avez choisi hello VM, payer attention toohello ACU pour hello machine virtuelle. Vous pouvez choisir une VM différente en fonction de hello valeur ACU qui correspond le mieux à vos besoins. Pour plus d’informations, consultez [Unité de calcul Azure (ACU)](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Capture d’écran de la page d’unités hello ACU](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Débit du réseau

Hello diagramme montre hello relation entre un débit et des IOPS suivante :

![Capture d’écran du débit](./media/oracle-design/throughput.png)

débit total Hello est estimé en fonction de hello informations suivantes :
- Trafic SQL*Net
- Mbits/s x nombre de serveurs (flux sortant tel qu’Oracle Data Guard)
- Autres facteurs, comme la réplication de l’application

![Capture d’écran de hello SQL * Net débit](./media/oracle-design/sqlnet_info.png)

Selon vos besoins en bande passante réseau, il existe différents types de passerelle pour vous toochoose à partir de. notamment une passerelle de base, VpnGw ou Azure ExpressRoute. Pour plus d’informations, consultez hello [passerelle VPN page de tarification](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Recommandations**

- Latence du réseau est plus élevée déploiement local de tooan comparés. La diminution des allers-retours réseau peut considérablement améliorer les performances.
- tooreduce allers-retours, consolider les applications qui ont des transactions élevées ou applications « bavardes » sur hello même machine virtuelle.

### <a name="disk-types-and-configurations"></a>Types de disque et configurations

- *Disques du système d’exploitation par défaut* : ces types de disques permettent la persistance et la mise en cache des données. Ils sont optimisés pour un accès au système d’exploitation au moment du démarrage, mais ils ne sont pas conçus pour les charges de travail transactionnelles ou d’entrepôt de données (analytiques).

- *Non managée disques*: avec ces types de disques, vous gérez les comptes de stockage hello qui stockent des fichiers de disque dur virtuel (VHD) hello qui correspondent tooyour les disques de machine virtuelle. Les fichiers VHD sont stockés en tant qu’objets blob de pages dans les comptes de stockage Azure.

- *Des disques gérés par*: Azure gère les comptes de stockage hello que vous utilisez pour vos disques de machine virtuelle. Vous spécifiez le type de disque de hello (standard ou premium) et la taille de hello du disque hello dont vous avez besoin. Azure crée et gère les disques de hello pour vous.

- *Disques de stockage Premium* : ces types de disques sont mieux adaptés aux charges de production. Disques de machine virtuelle Premium stockage prend en charge qui peuvent être joint toospecific taille-série machines virtuelles, telles que de la série DS, DSv2, GS et F machines virtuelles. disque premium de Hello est fourni avec des tailles différentes, et vous pouvez choisir entre les disques allant de 32 Go too4, 096 Go. Chaque taille de disque a ses propres spécifications en matière de performances. Selon les exigences de votre application, vous pouvez attacher un ou plusieurs disques tooyour machine virtuelle.

Lorsque vous créez un nouveau disque géré à partir du portail de hello, vous pouvez choisir hello **type de compte** de type hello de disque souhaité toouse. Gardez à l’esprit que tous les disques disponibles sont affichés dans le menu déroulant de hello. Une fois que vous choisissez une taille de machine virtuelle particulière, menu de hello affiche uniquement hello disponible stockage premium SKU qui reposent sur cette taille de machine virtuelle.

![Capture d’écran de la page de disque géré hello](./media/oracle-design/premium_disk01.png)

Pour plus d’informations, consultez [Stockage Premium hautes performances et disques managés pour les machines virtuelles](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Après avoir configuré votre stockage sur un ordinateur virtuel, vous pouvez choisir les disques hello tooload test avant de créer une base de données. Connaître le taux d’e/s de hello en termes de latence et débit peut vous aider à déterminer si prend en charge les machines virtuelles de hello hello attendu débit avec les cibles de latence.

Divers outils sont dédiés au test de charge d’application, comme Oracle Orion, Sysbench et Fio.

Exécutez à nouveau test de charge hello après avoir déployé une base de données Oracle. Démarrez vos charges de travail régulières et aux pics et hello affichent hello de ligne de base de votre environnement.

Il peut être plus important toosize le stockage hello basé sur les taux d’IOPS hello plutôt que la taille de stockage hello. Par exemple, si hello nécessaire IOPS est de 5 000, mais vous ne devez 200 Go, vous pouvez obtenir encore premium, disque hello P30 classe même s’il est fourni avec plus de 200 Go de stockage.

taux d’IOPS Hello peut être obtenu à partir de hello les rapports anticipé. Il est déterminé par le journal de restauration par progression hello, lectures physiques et le taux d’écritures.

![Capture d’écran de la page de rapport hello anticipé](./media/oracle-design/awr_report.png)

Par exemple, taille de restauration par progression hello est 12,200,000 octets par seconde, ce qui est Mbits/s too11.63 égale.
Hello IOPS est 12 200 000 / 2,358 = 5,174.

Après avoir une vision claire des exigences d’e/s de hello, vous pouvez choisir une combinaison de lecteurs qui sont mieux adaptée toomeet ces exigences.

**Recommandations**

- Pour l’espace de stockage de données, répartir la charge de travail d’e/s hello sur un nombre de disques à l’aide de stockage géré ou Oracle ASM.
- Augmente la taille de bloc hello d’e/s pour les opérations gourmandes en écriture et de lecture intensive, ajouter de disques de données.
- Augmenter la taille du bloc hello pour les processus séquentiels volumineux.
- Utiliser des e/s de données compression tooreduce (pour les données et les index).
- Placez les flux de transport Redo, System, Temp et Undo sur des disques de données distincts.
- Ne placez pas de fichiers d’application sur les disques du système d’exploitation par défaut (/dev/sda). Ces disques sont optimisés pour les démarrages rapides de machine virtuelle et risquent de ne pas fournir de performances optimales pour votre application.

### <a name="disk-cache-settings"></a>Paramètres de cache des disques

Il existe trois solutions pour la mise en cache de l’hôte :

- *Lecture seule* : toutes les demandes sont mises en cache pour les lectures ultérieures. Toutes les écritures sont rendues persistantes directement tooAzure stockage d’objets Blob.

- *Lecture-écriture* : il s’agit d’un algorithme de type « lecture anticipée ». Hello lit et écrit est mises en cache pour les lectures ultérieures. Non-write-through écritures sont d’abord maintenue toohello le cache local. Pour SQL Server, les écritures sont persistante tooAzure stockage, car elle utilise à l’écriture. Il fournit également la plus faible latence de disque hello pour les charges de travail claires.

- *Aucun* (désactivé) : À l’aide de cette option, vous pouvez contourner le cache de hello. Toutes les données hello est transféré toodisk et persistante tooAzure stockage. Cette méthode donne vous hello plus élevé d’e/s pour les charges de travail intensives d’e/s. Vous devez également tootake « coût de transaction » en considération.

**Recommandations**

débit de hello toomaximize, nous vous recommandons de commencer avec **aucun** pour caching d’hôte. Pour le stockage Premium, gardez à l’esprit que vous devez désactiver les barrières « hello » lorsque vous montez le système de fichiers hello avec hello **ReadOnly** ou **aucun** options. Mettre à jour le fichier/etc/fstab de hello avec des disques toohello hello UUID.

Pour plus d’informations, consultez [Stockage Premium pour les machines virtuelles Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Capture d’écran de la page de disque géré hello](./media/oracle-design/premium_disk02.png)

- Pour les disques du système d’exploitation, utilisez la mise en cache par défaut **Lecture/Écriture**.
- Pour SYSTEM, TEMP et UNDO, utilisez **Aucun** pour la mise en cache.
- Pour DATA, utilisez **Aucun** pour la mise en cache. Toutefois, si votre base de données est en lecture seule ou en lecture intensive, utilisez la mise en cache **Lecture seule**.

Après l’enregistrement de votre paramètre de disque de données, vous ne pouvez pas modifier le paramètre de cache d’hôte hello, sauf si vous démontez le lecteur hello en hello au niveau du système d’exploitation et la réinstallation d’une fois que vous avez modifié hello.


## <a name="security"></a>Sécurité

Après avoir configuré et configuré votre environnement Azure, hello prochaine étape consiste toosecure votre réseau. Voici quelques recommandations :

- *Stratégie du groupe de sécurité réseau* : le groupe de sécurité réseau peut être défini par un sous-réseau ou une carte réseau. Il est plus simple accès toocontrol au niveau du sous-réseau hello pour forcer le routage pour les éléments tels que les pare-feux de l’application et la sécurité.

- *Jumpbox*: pour un accès plus sécurisé, les administrateurs ne doivent pas se connecter directement toohello service d’application ou de la base de données. Un jumpbox est utilisé comme un support entre l’ordinateur d’administrateur de hello et des ressources Azure.
![Capture d’écran de la page de la topologie hello Jumpbox](./media/oracle-design/jumpbox.png)

    machine d’administrateur Hello doit offrir à accès restreint IP toohello jumpbox uniquement. Hello jumpbox doit avoir accès toohello application et base de données.

- *Réseau privé* (sous-réseaux) : nous vous recommandons d’avoir service de l’application hello et la base de données sur des sous-réseaux distincts, afin de mieux contrôler qui peut être définie par la stratégie de groupe de sécurité réseau.


## <a name="additional-reading"></a>Documentation supplémentaire

- [Configurer Oracle ASM](configure-oracle-asm.md)
- [Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure](configure-oracle-dataguard.md)
- [Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure](configure-oracle-golden-gate.md)
- [Sauvegarde et récupération Oracle](oracle-backup-recovery.md)

## <a name="next-steps"></a>Étapes suivantes

- [Didacticiel : créer des machines virtuelles hautement disponibles](../../linux/create-cli-complete.md)
- [Explorer des exemples Azure CLI de déploiement de machines virtuelles](../../linux/cli-samples.md)
