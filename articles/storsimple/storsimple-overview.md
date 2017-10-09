---
title: "Présentation de la solution aaaStorSimple 8000 series | Documents Microsoft"
description: "Décrit StorSimple hiérarchisation du périphérique de hello, périphérique virtuel, services et de gestion du stockage et présente des termes clés utilisés dans StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>StorSimple série 8000 : une solution de stockage de cloud hybride
## <a name="overview"></a>Vue d'ensemble
Bienvenue dans tooMicrosoft Azure StorSimple, une solution de stockage intégrée qui gère les tâches de stockage entre les appareils locaux et de stockage en cloud Microsoft Azure. StorSimple est une solution de réseau SAN de zone de stockage efficace, rentable et facile à gérer facilement qui élimine la plupart des problèmes de hello et les dépenses liées à la protection des données et de stockage d’entreprise. Il utilise l’appareil de série StorSimple 8000 hello propriétaire s’intègre aux services de cloud et fournit un ensemble d’outils de gestion pour une vue claire de tout le stockage enterprise, y compris le stockage cloud. (informations de déploiement de StorSimple hello publiées sur le site Web de Microsoft Azure hello s’applique tooStorSimple 8000 series appareils uniquement. Si vous utilisez un appareil de série StorSimple 5000/7000, accédez trop[StorSimple aide](http://onlinehelp.storsimple.com/).)

StorSimple utilise [hiérarchisation du stockage](#automatic-storage-tiering) toomanage les données stockées sur des supports de stockage différents. jeu de travail actuel Hello est stockée localement sur des lecteurs solid state Drive (SSD), les données moins souvent utilisées sont stockées sur des lecteurs de disque dur (HDD) et données d’archivage sont transmises toohello cloud. En outre, StorSimple utilise la déduplication et compression tooreduce hello quantité stockage hello données consomme. Pour plus d’informations, consultez trop[de déduplication et compression](#deduplication-and-compression). Pour les définitions d’autres termes et concepts clés utilisés dans la documentation de la série hello StorSimple 8000, accédez trop[la terminologie StorSimple](#storsimple-terminology) à fin hello de cet article.

En outre toostorage management, fonctionnalités de protection des données StorSimple activer vous toocreate à la demande et les sauvegardes planifiées et stocker les localement ou dans hello de cloud computing. Les sauvegardes sont effectuées dans l’écran hello d’instantanés incrémentiels, ce qui signifie qu’ils peuvent être créés et restaurés rapidement. Instantanés cloud peuvent être extrêmement importants dans les scénarios de récupération d’urgence, car elles remplacement les systèmes de stockage secondaire (par exemple, une sauvegarde sur bande) et autoriser des sites de centre de données ou tooalternate la tooyour des données toorestore si nécessaire.

![icône de vidéo](./media/storsimple-overview/video_icon.png) Regardez la vidéo hello pour une présentation rapide de tooMicrosoft Azure StorSimple.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Pourquoi utiliser StorSimple ?
Hello tableau suivant décrit quelques-uns des avantages clés hello qui fournit de Microsoft Azure StorSimple.

| Fonctionnalité | Avantage |
| --- | --- |
| Intégration transparente |Utilise des installations de stockage hello iSCSI protocole tooinvisibly lien données. Ainsi, les données stockées dans le cloud hello, au centre de données hello, ou sur des serveurs distants s’affiche toobe stocké à un emplacement unique. |
| Coûts de stockage réduits |Alloue suffisamment local ou cloud de demandes en cours de stockage toomeet et étend le stockage cloud uniquement lorsque cela est nécessaire. Il réduit également les besoins de stockage et les dépenses en éliminant les versions redondantes des hello mêmes données (déduplication) et en utilisant la compression. |
| Gestion simplifiée du stockage |Fournit des tooconfigure d’Outils d’administration système et de gérer les données stockées localement, sur un serveur distant et dans le cloud de hello. En outre, vous pouvez gérer la sauvegarde et la restauration des fonctions depuis un composant logiciel enfichable Microsoft Management Console (MMC).|
| Récupération d’urgence et conformité améliorées |Ne nécessite pas un long délai de récupération. Au contraire, il restaure les données lorsque vous en avez besoin. Cela signifie que les opérations normales peuvent se poursuivre, avec une interruption minimale. En outre, vous pouvez configurer des planifications de sauvegarde toospecify stratégies et de rétention des données. |
| Mobilité des données |Données téléchargées tooMicrosoft Azure cloud services sont accessibles à partir d’autres sites à des fins de récupération et de migration. En outre, vous pouvez utiliser des équipements de StorSimple tooconfigure StorSimple Cloud sur des machines virtuelles (VM) s’exécutant dans Microsoft Azure. Hello machines virtuelles permettre ensuite utiliser les périphériques virtuels tooaccess stockées données pour à des fins de test ou de récupération. |
| Continuité de l’activité |Permet de StorSimple-7000 5000 série utilisateurs toomigrate leur appareil de série de données tooa StorSimple 8000. |
| Disponibilité Bonjour Azure Government portail |StorSimple est disponible dans hello portail Azure du gouvernement. Pour plus d’informations, consultez [déployer l’appareil StorSimple local Bonjour gouvernement Portal](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Disponibilité et protection des données |Hello série StorSimple 8000 prend en charge la Zone Redundant Storage (ZRS), dans Ajout tooLocally stockage redondant (LRS) et stockage géo-redondant (GRS). Consultez trop[cet article sur les options de redondance de stockage Azure](https://azure.microsoft.com/documentation/articles/storage-redundancy/) pour plus d’informations ZRS. |
| Prise en charge des applications critiques |StorSimple vous permet de qu'identifier les volumes appropriés comme attaché localement qui à son tour permet de s’assurer que les données requises par les applications critiques ne sont pas toohello à plusieurs niveaux de cloud computing. Les volumes attachés localement ne sont pas des latences de toocloud sujet ou des problèmes de connectivité. Pour plus d’informations sur les volumes attachés localement, consultez [utiliser le Gestionnaire de périphériques StorSimple hello service des volumes toomanage](storsimple-8000-manage-volumes-u2.md). |
| Faible latence et hautes performances |Vous pouvez créer des appareils cloud qui tirent parti de hello performances élevées, à des fonctionnalités de faible latence de stockage Azure premium. Pour plus d’informations sur les appliances cloud StorSimple Premium, consultez la page [Déployer et gérer une appliance cloud StorSimple dans Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Composants de StorSimple
Hello solution Microsoft Azure StorSimple comprend hello suivant des composants :

* **Appareil Microsoft Azure StorSimple** : une baie de stockage hybride local qui contient des disques SSD et des disques durs, ainsi que des contrôleurs redondants et des fonctionnalités de basculement automatique. les contrôleurs de Hello gèrent la hiérarchisation du stockage plaçant actuellement utilisées (ou à chaud) des données sur le stockage local (dans hello périphérique ou local serveurs), lors du déplacement des données moins souvent utilisées dans le cloud toohello.
* **Équipement de Cloud StorSimple** – également appelé hello équipement virtuel StorSimple, il s’agit d’une version du logiciel de l’appareil StorSimple hello qui réplique l’architecture de hello et la plupart des fonctionnalités du périphérique de stockage hybride physique hello. Hello StorSimple Cloud Appliance s’exécute sur un seul nœud dans une machine virtuelle Azure. Les appareils virtuels Premium, qui tirent parti d’Azure Premium Storage, sont disponibles dans Update 2 et version ultérieure.
* **Le Gestionnaire de périphériques StorSimple service** : extension de hello portail Azure qui vous permet de gérer un appareil StorSimple ou un dispositif de StorSimple de Cloud à partir d’une seule interface web. Vous pouvez utiliser toocreate de service de gestionnaire de périphériques StorSimple hello et gérer les services, afficher et gérer les appareils, afficher les alertes, gérer les volumes et afficher et gérer les stratégies de sauvegarde et de catalogue de sauvegarde hello.
* **Windows PowerShell pour StorSimple** – une interface de ligne de commande que vous pouvez utiliser toomanage hello appareil StorSimple. Windows PowerShell pour StorSimple a des fonctionnalités qui vous permettent de tooregister votre appareil StorSimple, configurez hello interface réseau sur votre appareil, installer certains types de mises à jour, résoudre les problèmes de votre appareil en accédant à la session de support hello et modifier hello état de l’appareil. Vous pouvez accéder à Windows PowerShell pour StorSimple par connexion série toohello ou à l’aide de la communication à distance de Windows PowerShell.
* **Applets de commande PowerShell StorSimple Azure** – une collection d’applets de commande Windows PowerShell qui vous tooautomate des tâches de niveau de service et la migration à partir de la ligne de commande hello. Pour plus d’informations sur hello applets de commande Azure PowerShell pour StorSimple, accédez à toohello [référence d’applet de commande](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **Gestionnaire d’instantanés StorSimple** – un composant logiciel enfichable MMC qui utilise des groupes de volumes et sauvegardes cohérentes avec les applications de hello Windows Volume Shadow Copy Service toogenerate. En outre, vous pouvez utiliser les clone et Gestionnaire d’instantanés StorSimple toocreate les planifications de sauvegarde ou restaurer des volumes.
* **L’adaptateur StorSimple pour SharePoint** – un outil qui étend de manière transparente protection de données et de stockage Microsoft Azure StorSimple tooSharePoint de batteries de serveurs, tout en effectuant le stockage StorSimple visible et administrable à partir de hello centrale de SharePoint. Portail d’administration.

diagramme de Hello ci-dessous fournit une vue d’ensemble de hello Microsoft Azure StorSimple architecture et des composants.

![Architecture de StorSimple](./media/storsimple-overview/overview-big-picture.png)

Hello sections suivantes décrivent chacun de ces composants de manière plus détaillée et expliquent comment les solutions hello organise les données, alloue du stockage et facilitent la gestion du stockage et protection des données. dernière section de Hello fournit les définitions des termes importants de hello et concepts connexes tooStorSimple composants et leur gestion.

## <a name="storsimple-device"></a>Appareil StorSimple
Appareil de Microsoft Azure StorSimple Hello est un groupe de stockage hybride local qui fournit le stockage principal et toodata d’accès iSCSI stocké sur celui-ci. Il gère la communication avec le stockage cloud et vous aide à la sécurité de hello tooensure et la confidentialité de toutes les données stockées sur hello solution Microsoft Azure StorSimple.

l’appareil StorSimple Hello inclut les disques SSD et disques durs de lecteurs de disque dur, ainsi que la prise en charge pour le clustering de basculement automatique. Il contient un processeur partagé, un stockage partagé et deux contrôleurs en miroir. Chaque contrôleur fournit des éléments suivants de hello :

* Ordinateur hôte de tooa connexion
* Des toosix réseau ports tooconnect toohello réseau local (LAN)
* Surveillance du matériel
* Mémoire vive non volatile (NVRAM), qui conserve les informations même si l’alimentation est interrompue
* Adaptée aux clusters mise à jour toomanage les mises à jour logicielles sur des serveurs dans un cluster de basculement afin que les mises à jour hello sont minimal ou aucun effet sur la disponibilité du service
* Service de cluster, fonctionnant comme un cluster principal, pour fournir une haute disponibilité et réduire les effets négatifs pouvant se produire si un lecteur de disque dur ou un disque SSD est défaillant ou passe hors connexion

Un seul contrôleur est actif à un instant donné. Si le contrôleur actif de hello échoue, second contrôleur de hello devient active automatiquement.

Pour plus d’informations, consultez trop[StorSimple composants matériels et l’état](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
Vous pouvez utiliser StorSimple toocreate un dispositif de cloud qui réplique l’architecture de hello et les fonctionnalités du périphérique de stockage hybride physique hello. Hello StorSimple Appliance de Cloud (également appelé hello équipement virtuel StorSimple) s’exécute sur un seul nœud dans une machine virtuelle Azure. (Une appliance cloud peut uniquement être créée sur une machine virtuelle Azure. Il est impossible d’en créer un sur un serveur local ou sur un appareil StorSimple.)

Dispositif de cloud Hello a hello suivant de fonctionnalités :

* Il se comporte comme un matériel physique et peut offrir un iSCSI interface toovirtual ordinateurs hello cloud.
* Vous pouvez créer un nombre illimité d’équipements de cloud dans le cloud de hello et les activer et désactiver selon les besoins.
* Il peut aider à simuler les environnements locaux dans les scénarios de test et de développement ou de récupération d’urgence, tout en facilitant la récupération au niveau des éléments à partir de sauvegardes.

Hello StorSimple Appliance de Cloud est disponible dans les deux modèles : périphérique hello 8010 (anciennement appelé modèle de hello 1100) et hello 8020 dispositif. Appareil de 8010 Hello a une capacité maximale de 30 To. APPAREIL 8020 Hello, qui tire parti du stockage Azure premium, a une capacité maximale de 64 To. (Dans des niveaux locaux, Azure Premium Storage stocke les données sur des disques SSD, alors que les données sont stockées sur des disques durs avec un stockage standard.) Notez que vous devez disposer d’un stockage premium toouse de compte de stockage Azure premium. Pour plus d’informations sur le stockage premium, consultez trop[stockage Premium : stockage hautes performances pour les charges de travail de Machine virtuelle Azure](../storage/common/storage-premium-storage.md).

Pour plus d’informations sur hello StorSimple Cloud Appliance, accédez trop[déployer et gérer un dispositif de StorSimple de Cloud dans Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Service StorSimple Device Manager
Microsoft Azure StorSimple fournit une interface utilisateur web (hello service du Gestionnaire de périphériques StorSimple) qui vous permet de toocentrally gérer le centre de données et le stockage cloud. Vous pouvez utiliser hello de tooperform du service de gestionnaire de périphériques StorSimple hello tâches suivantes :

* Configurer les paramètres système pour les appareils StorSimple.
* Configurer et gérer les paramètres de sécurité pour les appareils StorSimple.
* Configurer les propriétés et les informations d’identification cloud.
* Configurer et gérer des volumes sur un serveur.
* Configurer des groupes de volumes.
* Sauvegarder et restaurer des données.
* Analyser les performances.
* Passer en revue les paramètres système et identifier les problèmes possibles.

Vous pouvez utiliser tooperform de service de gestionnaire de périphériques StorSimple hello toutes les tâches d’administration, à l’exception de celles qui nécessitent l’arrêt, telles que le programme d’installation initiale et l’installation des mises à jour du système.

Pour plus d’informations, consultez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell pour StorSimple
Windows PowerShell pour StorSimple fournit une interface de ligne de commande que vous pouvez utiliser toocreate et gérer le service de Microsoft Azure StorSimple hello et configurer et surveiller les périphériques StorSimple. C’est une interface de ligne de commande Windows PowerShell, qui inclut des applets de commande dédiées à la gestion de votre appareil StorSimple. Windows PowerShell pour StorSimple dispose de fonctionnalités qui vous permettent d’effectuer les opérations suivantes :

* Enregistrer un appareil.
* Configurer l’interface de réseau hello sur un appareil.
* Installer certains types de mises à jour.
* Dépannage de votre appareil en accédant à la session de support hello.
* Modifier l’état de l’appareil hello.

Vous pouvez accéder à Windows PowerShell pour StorSimple à partir d’une console série (sur un ordinateur hôte ordinateur connecté directement toohello appareil) ou à distance à l’aide de la communication à distance de Windows PowerShell. Notez que certains Windows PowerShell pour StorSimple des tâches, telles que l’inscription initiale de l’appareil, peut uniquement être effectuée sur la console série de hello.

Pour plus d’informations, consultez trop[utiliser Windows PowerShell pour StorSimple tooadminister votre appareil](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Cmdlets PowerShell d’Azure StorSimple
applets de commande Azure PowerShell StorSimple Hello sont un ensemble d’applets de commande Windows PowerShell qui autorisent tooautomate au niveau du service et les tâches de migration à partir de la ligne de commande hello. Pour plus d’informations sur hello applets de commande Azure PowerShell pour StorSimple, accédez à toohello [référence d’applet de commande](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
Gestionnaire d’instantanés StorSimple est un composant logiciel enfichable Microsoft Management Console (MMC) que vous pouvez utiliser toocreate cohérente et point-à-temps copies de sauvegarde local et du cloud. le composant logiciel enfichable Hello s’exécute sur un hôte Windows Server. Vous pouvez utiliser StorSimple Snapshot Manager pour :

* Configurer, sauvegarder et supprimer des volumes.
* Configurer le volume tooensure de groupes les données sauvegardées est cohérente avec les applications.
* Gérer les stratégies de sauvegarde afin que les données sont sauvegardées selon une planification prédéterminée et stockées dans un emplacement désigné (localement ou dans le cloud de hello).
* Restaurer des volumes et des fichiers individuels.

Les sauvegardes sont capturées en tant que des instantanés, qui enregistrent uniquement les modifications de hello depuis hello dernière capture instantanée et nécessitent beaucoup moins d’espace que les sauvegardes complètes. Vous pouvez créer des planifications de sauvegarde ou effectuer des sauvegardes immédiates en fonction de vos besoins. En outre, vous pouvez utiliser les stratégies de rétention de gestionnaire d’instantanés StorSimple tooestablish qui contrôlent le nombre d’instantanés seront enregistrés. Si vous avez ensuite besoin toorestore des données à partir d’une sauvegarde, permet de gestionnaire d’instantanés StorSimple vous sélectionnez catalogue hello locaux ou des instantanés cloud. 

Si un incident se produit ou si vous avez besoin des données de toorestore pour une autre raison, le Gestionnaire d’instantanés StorSimple restaure de façon incrémentielle car il est nécessaire. La restauration des données ne nécessite pas d’arrêter la totalité du système hello pendant que vous restaurez un fichier, remplacez un équipement ou déplacez les opérations tooanother site.

Pour plus d’informations, consultez trop[Nouveautés du Gestionnaire d’instantanés StorSimple ?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adaptateur StorSimple pour SharePoint
Microsoft Azure StorSimple comprend hello adaptateur StorSimple pour SharePoint, un composant facultatif qui étend en toute transparence les batteries de serveurs de fonctionnalités tooSharePoint StorSimple stockage et protection des données. adaptateur de Hello fonctionne avec un fournisseur de stockage d’objets Blob distants (RBS) et la fonctionnalité de SQL Server RBS hello, ce qui permet de vous toomove BLOB tooa server sauvegardée par le système de Microsoft Azure StorSimple hello. Microsoft Azure StorSimple stocke ensuite les données d’objet BLOB hello localement ou dans le cloud de hello, basée sur l’utilisation.

Hello adaptateur StorSimple pour SharePoint est gérée à partir de portail d’Administration centrale de SharePoint hello. Par conséquent, gestion de SharePoint reste centralisée, et tout le stockage s’affiche toobe dans une batterie de serveurs SharePoint hello.

Pour plus d’informations, consultez trop[l’adaptateur StorSimple pour SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Technologies de gestion de stockage
En outre toohello dédié appareil StorSimple, un appareil virtuel et autres composants, Microsoft Azure StorSimple utilise hello suivant software technologies tooprovide accès rapide toodata et tooreduce la consommation du stockage :

* [Hiérarchisation automatique du stockage](#automatic-storage-tiering) 
* [Allocation dynamique](#thin-provisioning) 
* [Déduplication et compression](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Hiérarchisation automatique du stockage
Microsoft Azure StorSimple organise automatiquement les données en niveaux logiques en fonction de l’utilisation actuelle, l’âge et les données de tooother relation. Données qui sont plus actifs sont stockées localement, moins d’active et les données inactives sont automatiquement migrés toohello cloud. Hello suivant le diagramme illustre cette approche du stockage.

![Niveaux de stockage StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

accès rapide de tooenable, StorSimple stocke des données très actifs (données à chaud) sur des disques SSD dans l’appareil StorSimple hello. Il stocke les données occasionnellement utilisées (à chaud des données) sur des disques durs dans l’appareil de hello ou sur des serveurs dans le centre de données hello. Il déplace les données inactives, les données de sauvegarde, et les données conservées archivage ou à des fins de conformité toohello cloud. 

> [!NOTE]
> Dans Update 2 ou version ultérieure, vous pouvez spécifier un volume attaché localement, auquel cas les données de salutation restent sur le périphérique local de hello et ne sont pas hiérarchisé toohello cloud. 


StorSimple ajuste et réorganise les données et modifie les affectations de stockage conformément aux modifications du schéma d’utilisation. Par exemple, certaines informations peuvent devenir moins actives au fil du temps. Dès qu’il sera progressivement moins actif, il est migré à partir de disques SSD tooHDDs, puis toohello cloud. Si ces mêmes données redevient actives, il est dispositif de stockage migré toohello précédent.

processus de hiérarchisation du stockage Hello s’effectue comme suit :

1. Un administrateur système configure un compte de stockage cloud Microsoft Azure.
2. administrateur de Hello utilise hello série console et hello le Gestionnaire de périphériques StorSimple service (en cours d’exécution dans hello portail Azure) tooconfigure hello appareil et le fichier de serveur, création de stratégies de protection des volumes et les données. Les machines locales (telles que les serveurs de fichiers) utilisent l’appareil StorSimple hello hello Internet Small Computer System Interface (iSCSI) tooaccess.
3. Au départ, StorSimple stocke les données sur hello rapide niveau SSD de périphérique de hello.
4. En tant que hello capacité approches du niveau SSD, StorSimple deduplicates compresse les blocs de données plus anciennes hello et les déplace toohello niveau.
5. En tant que la capacité du disque dur niveau approches de hello, StorSimple chiffre hello les blocs de données plus anciennes et les envoie en toute sécurité de compte de stockage Microsoft Azure toohello via HTTPS.
6. Microsoft Azure crée plusieurs réplicas de données de hello dans son centre de données et dans un centre de données à distance, garantissant que les données de salutation peuvent être récupérées en cas de sinistre.
7. Lorsque le serveur de fichiers hello demande des données stockées dans le cloud de hello, StorSimple renvoie de manière transparente et stocke une copie sur le niveau SSD de hello de l’appareil StorSimple hello.

#### <a name="how-storsimple-manages-cloud-data"></a>Gestion des données cloud par StorSimple

StorSimple deduplicates les données des clients sur tous les instantanés de hello hello principal et les données et (écrit par les hôtes). Alors que la déduplication est idéal pour l’efficacité du stockage, il est question « Quel est dans le cloud de hello » compliquée hello. Hello à plusieurs niveaux de données primaire et les données de capture instantanée hello se chevauchent entre eux. Un bloc de données dans le cloud de hello unique peut être utilisé comme données primaires à plusieurs niveaux et également être référencé par plusieurs instantanés. Chaque instantané cloud garantit qu’une copie de toutes les données de point-à-temps hello est verrouillée dans le cloud de hello jusqu'à la suppression de cet instantané.

Données sont supprimées uniquement à partir du cloud de hello lorsqu’il n’y a aucune donnée de toothat de références. Par exemple, si nous prenons un instantané cloud de toutes les données hello dans l’appareil StorSimple hello et ensuite supprimer certaines données principales, nous verriez hello _données primaires_ supprimer immédiatement. Hello _du cloud_ qui inclut hello données hiérarchisées hello sauvegardes et reste hello même. Il s’agit, car il existe un instantané de référence encore des données du cloud hello. Après le cloud de hello snapshot est supprimé (et tous les autres instantanés qui référencé hello les mêmes données), supprime de la consommation de cloud computing. Avant de supprimer les données cloud, vérifiez qu’aucune capture instantanée ne fait référence à ces données. Ce processus est appelé _le garbage collection_ et est un service en arrière-plan en cours d’exécution sur l’appareil de hello. La suppression de données du cloud n’est pas immédiatement que le contrôle de service hello garbage collection pour les autres références à des données toothat avant la suppression de hello. vitesse Hello du garbage collection dépend du nombre total de hello d’instantanés et le total des données hello. En règle générale, les données du cloud hello nettoyées dans moins d’une semaine.


### <a name="thin-provisioning"></a>Allocation dynamique
Allocation dynamique est une technologie de virtualisation dans lequel le stockage disponible apparaît tooexceed des ressources physiques. Plutôt que de réserver suffisamment de stockage à l’avance, StorSimple utilise tooallocate provisionnement dynamique juste assez toomeet d’espace nécessaire en cours. nature évolutive de Hello de stockage cloud simplifie cette approche, car StorSimple peut augmenter ou diminuer les besoins changeants de toomeet de stockage cloud.

> [!NOTE]
> Les volumes épinglés localement ne sont pas alloués de façon dynamique. Stockage alloué tooa local volume est configuré dans son intégralité lors de la création du volume de hello.


### <a name="deduplication-and-compression"></a>Déduplication et compression
Microsoft Azure StorSimple utilise la déduplication et toofurther de compression de données réduisent les besoins de stockage.

La déduplication réduit hello quantité globale des données stockées en éliminant les redondances dans le jeu de données stockée hello. Informations que les modifications apportées, StorSimple ignore les données de salutation inchangée et captures hello uniquement les modifications. En outre, StorSimple réduit la quantité hello de données stockées en identifiant et en supprimant les informations inutiles. 

> [!NOTE]
> Les données sur les volumes épinglés localement ne sont pas dédupliquées ou compressées. Toutefois, les sauvegardes de volumes épinglés localement sont dédupliquées et compressées.


## <a name="storsimple-workload-summary"></a>Résumé des charges de travail StorSimple
Un résumé des charges de travail StorSimple hello pris en charge est sous forme de tableau ci-dessous.

| Scénario | Charge de travail | Pris en charge | Restrictions | Version |
| --- | --- | --- | --- | --- |
| Collaboration |Partage de fichiers |Oui | |Toutes les versions |
| Collaboration |Partage de fichiers distribués |Oui | |Toutes les versions |
| Collaboration |SharePoint |Oui* |Pris en charge uniquement avec des volumes épinglés localement |Update 2 et versions ultérieures |
| Archivage |Archivage de fichiers simple |Oui | |Toutes les versions |
| Virtualisation |Machines virtuelles |Oui* |Pris en charge uniquement avec des volumes épinglés localement |Update 2 et versions ultérieures |
| Base de données |SQL |Oui* |Pris en charge uniquement avec des volumes épinglés localement |Update 2 et versions ultérieures |
| Surveillance vidéo |Surveillance vidéo |Oui* |Prise en charge lorsque l’appareil StorSimple est dédié uniquement toothis la charge de travail |Update 2 et versions ultérieures |
| Backup  |Sauvegarde de la cible principale |Oui* |Prise en charge lorsque l’appareil StorSimple est dédié uniquement toothis la charge de travail |Update 3 et versions ultérieures |
| Backup  |Sauvegarde de la cible secondaire |Oui* |Prise en charge lorsque l’appareil StorSimple est dédié uniquement toothis la charge de travail |Update 3 et versions ultérieures |

*Oui&amp;#42; - Des restrictions et des recommandations sur la solution doivent s’appliquer.*

Hello suivant les charges de travail n’est pas pris en charge par les unités StorSimple 8000 series. En cas de déploiement sur StorSimple, ces charges de travail entraîneront une configuration non prise en charge.

* Imagerie médicale
* Microsoft Exchange
* VDI
* Oracle
* SAP
* Données volumineuses (« Big Data »)
* Distribution de contenu
* Démarrage à partir de SCSI

Voici une liste de composants d’infrastructure hello StorSimple pris en charge.

| Scénario | Charge de travail | Pris en charge | Restrictions | Version |
| --- | --- | --- | --- | --- |
| Généralités |ExpressRoute |Oui | |Toutes les versions |
| Généralités |DataCore FC |Oui* |Prise en charge avec DataCore SANsymphony |Toutes les versions |
| Généralités |DFSR |Oui* |Pris en charge uniquement avec des volumes épinglés localement |Toutes les versions |
| Généralités |Indexation |Oui* |Pour les volumes hiérarchisés, seule l’indexation des métadonnées est prise en charge (aucune donnée).<br>Pour les volumes épinglés localement, l’indexation complète est prise en charge. |Toutes les versions |
| Généralités |Protection contre les virus |Oui* |Pour les volumes hiérarchisés, seule l’analyse des ouvertures et des fermetures est prise en charge.<br> Pour les volumes épinglés localement, l’analyse complète est prise en charge. |Toutes les versions |

*Oui&amp;#42; - Des restrictions et des recommandations sur la solution doivent s’appliquer.*

Voici une liste d’autres logiciels qui sont utilisés avec les solutions toobuild StorSimple.

| Type de charge de travail | Logiciels utilisés avec StorSimple | Versions prises en charge|Guide des liens toosolution| 
| --- | --- | --- | --- |
| Cible de sauvegarde |Veeam |Veeam v 9 et versions ultérieures |[StorSimple comme cible de sauvegarde avec Veeam](storsimple-configure-backup-target-veeam.md)|
| Cible de sauvegarde |Veritas Backup Exec |Backup Exec 16 et versions ultérieures |[StorSimple comme cible de sauvegarde avec Backup Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Cible de sauvegarde |Veritas NetBackup |NetBackup 7.7.x et versions ultérieures  |[StorSimple comme cible de sauvegarde avec NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Partage de fichiers global <br></br> Collaboration |Talon  |[StorSimple avec Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminologie StorSimple
Avant de déployer votre solution Microsoft Azure StorSimple, nous vous recommandons de consulter les suivant hello termes et définitions.

### <a name="key-terms-and-definitions"></a>Termes et définitions clés
| Terme (acronyme ou abréviation) | Description |
| --- | --- |
| enregistrement de contrôle d’accès (ACR) |Un enregistrement associé à un volume sur votre appareil Microsoft Azure StorSimple qui détermine les hôtes qui peuvent se connecter à tooit. détermination de Hello est basée sur iSCSI de hello nom qualifié (IQN) d’hôtes hello (contenus dans hello ACR) qui sont connectent à l’appareil StorSimple tooyour. |
| AES-256 |Un algorithme Advanced Encryption Standard (AES) 256 bits pour chiffrer les données lors de leur déplacement tooand du cloud de hello. |
| taille d’unité d’allocation |Hello plus petite quantité d’espace disque qui peut être allouée toohold un fichier dans vos systèmes de fichiers Windows. Si une taille de fichier n’est pas un multiple pair de la taille de cluster hello, un espace supplémentaire doit être fichier hello de toohold utilisé (haut toohello prochain multiple de la taille de cluster hello) ce qui entraîne une perte d’espace et la fragmentation du disque dur de hello. <br>Hello recommandé QU'AUS pour des volumes StorSimple de Azure est de 64 Ko, car elle fonctionne bien avec les algorithmes de déduplication hello. |
| hiérarchisation du stockage automatisé |Déplacement automatique des données les moins actives à partir de disques SSD tooHDDs et puis couche tooa dans le cloud de hello et la gestion de tout le stockage à partir d’une interface utilisateur centrale. |
| catalogue de sauvegarde |Collection de sauvegardes habituellement liées par type d’application hello qui a été utilisée. Cette collection est affichée dans le panneau de catalogue de sauvegarde hello Hello interface utilisateur du service Gestionnaire de périphériques StorSimple. |
| fichier de catalogue de sauvegarde |Un fichier contenant une liste des instantanés disponibles actuellement stockés dans hello sauvegarde de base de données du Gestionnaire d’instantanés StorSimple. |
| stratégie de sauvegarde |Sélection de volumes, type de sauvegarde et un calendrier qui vous permet de toocreate sauvegardes selon une planification prédéfinie. |
| objets blob (BLOB) |Ensemble de données binaires stockées sous forme d’une seule entité dans un système de gestion de base de données. Les objets blob sont généralement des images, du contenu audio ou d’autres objets multimédias, bien que parfois le code exécutable binaire soit aussi stocké sous forme d’objet blob. |
| protocole CHAP |Protocole utilisé homologue de hello tooauthenticate d’une connexion, en fonction de l’homologue hello partage un mot de passe ou un secret. CHAP peut être unidirectionnel ou mutuel. Authentification CHAP unidirectionnelle, la cible de hello authentifie un initiateur. Authentification CHAP mutuelle, que la cible de hello authentifier l’initiateur de hello et cet initiateur hello authentifie la cible de hello. |
| clone |Copie dupliquée d’un volume. |
| Cloud as a Tier (CaaT) |Stockage cloud intégré sous un niveau au sein de l’architecture de stockage hello afin que tout le stockage apparaît partie toobe du réseau de stockage d’une entreprise. |
| fournisseur de services cloud (CSP) |Fournisseur de services de cloud computing. |
| instantané cloud |Copie des données du volume qui sont stockées dans le cloud de hello point-à-temps. Un instantané cloud est équivalent instantané tooa répliqué sur un système de stockage hors site, distinct. Les instantanés cloud sont particulièrement utiles dans les scénarios de récupération d’urgence. |
| clé de chiffrement de stockage cloud |Un mot de passe ou une clé utilisée par vos données de hello chiffré StorSimple périphérique tooaccess envoyées par votre appareil toohello cloud. |
| mise à jour adaptée aux clusters |La gestion des mises à jour logicielles sur des serveurs dans un cluster de basculement afin que les mises à jour hello sont minimal ou aucun effet sur la disponibilité du service. |
| chemin de données |Ensemble d’unités fonctionnelles qui effectuent des opérations de traitement de données interconnectées. |
| désactiver |Action permanente que sauts hello connexion entre l’appareil StorSimple hello et hello associés service cloud. Instantanés cloud de l’appareil de hello sont conservés après ce processus et peuvent être clonés ou utilisés pour la récupération d’urgence. |
| mise en miroir de disques |Réplication logique de volumes de disques durs distincts sur les lecteurs dans une disponibilité continue tooensure en temps réel. |
| mise en miroir de disques dynamiques |Réplication de volumes de disques logiques sur des disques dynamiques. |
| disques dynamiques |Un format de volume de disque qui utilise hello toostore du Gestionnaire de disque logique (LDM) et de gérer les données sur plusieurs disques physiques. Les disques dynamiques peut être agrandie tooprovide davantage d’espace libre. |
| boîtier EBOD |Boîtier secondaire de votre appareil Microsoft Azure StorSimple contenant des disques durs supplémentaires pour étendre la capacité de stockage. |
| allocation fixe |Un stockage classique approvisionnement dans le stockage est alloué en fonction d’anticipées besoins (et est généralement au-delà besoin actuel de hello). Voir aussi *allocation dynamique*. |
| lecteur de disque dur (HDD) |Un lecteur qui utilise des données toostore plateaux la rotation. |
| stockage cloud hybride |Architecture de stockage qui utilise des ressources locales et hors site, y compris le stockage cloud. |
| Internet Small Computer System Interface (iSCSI) |Norme réseau de stockage basée sur le protocole IP. Elle permet de lier les équipements ou les installations de stockage de données. |
| initiateur iSCSI |Un composant logiciel qui permet à un ordinateur hôte exécutant le réseau de stockage iSCSI externe Windows tooconnect tooan. |
| nom complet iSCSI (IQN) |Nom unique qui identifie une cible ou un initiateur iSCSI. |
| cible iSCSI |Composant logiciel qui fournit des sous-systèmes de disque iSCSI centralisés dans les réseaux de zone de stockage. |
| archivage dynamique |Une approche du stockage dans lequel les données d’archivage sont accessibles tout temps hello (il n'est pas stockée hors site sur bande, par exemple). Microsoft Azure StorSimple utilise l’archivage dynamique. |
| volume épinglé localement |un volume qui réside sur l’appareil de hello et n’est jamais hiérarchisé toohello cloud. |
| instantané local |Copie des données du volume qui sont stockées sur le périphérique de Microsoft Azure StorSimple hello point-à-temps. |
| Microsoft Azure StorSimple |Une solution efficace, consistant en un dispositif de stockage de centre de données et le logiciel qui permet d’informatique organisations tooleverage stockage cloud comme s’il s’agissait de stockage du centre de données. StorSimple simplifie la protection et la gestion des données tout en réduisant les coûts. solution de Hello consolide principale stockage, archivage, sauvegarde et récupération d’urgence (DR) grâce à une intégration transparente avec le cloud de hello. En associant le stockage SAN et la gestion des données cloud sur une plateforme d’entreprise, les appareils StorSimple fournissent la vitesse, la simplicité et la fiabilité recherchées pour tous les besoins relatifs au stockage. |
| module d’alimentation et de refroidissement (PCM) |Par conséquent, les composants matériels de votre appareil StorSimple comportant des alimentations hello et hello ventilateur, hello module d’alimentation et de refroidissement nom. boîtier principal de Hello du périphérique de hello a deux modules PCM de 764 w tandis que hello boîtier EBOD a deux modules PCM de 580 w. |
| boîtier principal |Boîtier principal de votre appareil StorSimple qui contient des contrôleurs de plateforme d’application hello. |
| objectif de délai de récupération (RTO) |Hello durée maximale avant un processus d’entreprise ou un système cœur est entièrement restaurée après un sinistre. |
| Serial Attached SCSI (SAS) |Type de lecteur de disque dur (HDD). |
| clé de chiffrement de données du service |Une clé apportées appareil StorSimple nouveau tooany disponibles qui s’enregistre avec hello service du Gestionnaire de périphériques StorSimple. les données de configuration Hello transférées entre le service du Gestionnaire de périphériques StorSimple hello et appareils de hello sont chiffrées à l’aide d’une clé publique et peuvent ensuite être déchiffrées uniquement sur un appareil hello à l’aide d’une clé privée. Clé de chiffrement de données de service permet de hello service tooobtain cette clé privée pour le déchiffrement. |
| clé d’inscription du service |Une clé qui permet d’inscrire l’appareil StorSimple hello auprès hello service du Gestionnaire de périphériques StorSimple afin qu’il apparaisse dans hello portail Azure pour les actions de gestion plus. |
| Small Computer System Interface (SCSI) |Ensemble de normes permettant de connecter physiquement des ordinateurs et de transférer des données entre ces derniers. |
| Solid State Drive (SSD) |Disque qui ne contient aucune pièce mobile, par exemple un disque mémoire flash. |
| compte de stockage |Un ensemble d’informations d’identification de l’accès lié compte de stockage tooyour pour un fournisseur de services de cloud donné. |
| Adaptateur StorSimple pour SharePoint |Un composant de Microsoft Azure StorSimple qui étend de manière transparente StorSimple stockage et protection des données tooSharePoint les batteries de serveurs. |
| Service StorSimple Device Manager |Une extension de hello portail Azure qui vous permet de toomanage vos locaux StorSimple Azure et les périphériques virtuels. |
| StorSimple Snapshot Manager |Composant logiciel enfichable Microsoft Management Console (MMC) pour la gestion des opérations de sauvegarde et de restauration dans Microsoft Azure StorSimple. |
| exécuter une sauvegarde |Une fonctionnalité qui permet à une sauvegarde interactive d’un volume hello utilisateur tootake. Il s’agit d’une autre façon d’effectuer une sauvegarde manuelle d’un volume en tant que tootaking opposé une sauvegarde automatisée via une stratégie définie. |
| Allocation dynamique |Une méthode permettant d’optimiser l’efficacité de hello avec quels hello espace de stockage disponible est utilisé dans les systèmes de stockage. Dans l’allocation dynamique, stockage de hello est allouée par plusieurs utilisateurs en fonction de l’espace minimal de hello requis par chaque utilisateur à un moment donné. Voir aussi *allocation fixe*. |
| hiérarchisation |Organisation des données en regroupements logiques basés sur l’utilisation actuelle, l’âge et les données de tooother relation. StorSimple organise automatiquement les données en niveaux. |
| volume |Zones de stockage logiques présentées sous forme de hello de lecteurs. Les volumes StorSimple correspondent toohello les volumes montés par hôte hello, y compris ceux détectés via l’utilisation de hello d’iSCSI et un appareil StorSimple. |
| conteneur de volumes |Un groupe de volumes et des paramètres hello qui s’appliquent toothem. Tous les volumes de votre appareil StorSimple sont regroupés dans des conteneurs de volumes. Paramètres de conteneur de volume incluent les comptes de stockage, les paramètres de chiffrement pour les données envoyées toocloud avec les clés de chiffrement associées et la bande passante consommée pour les opérations impliquant le cloud de hello. |
| groupe de volumes |Dans Gestionnaire d’instantanés StorSimple, un groupe de volumes est une collection de volumes configurés toofacilitate le processus de sauvegarde. |
| service VSS |Un service de système d’exploitation Windows Server qui facilite la cohérence des applications en communiquant avec prenant en charge VSS applications toocoordinate hello la création d’instantanés incrémentiels. Service VSS vérifie que les applications de hello sont temporairement inactives quand les instantanés sont créés. |
| Windows PowerShell pour StorSimple |Une interface de ligne de commande Windows PowerShell utilisée toooperate et gérer votre appareil StorSimple. Tout en conservant certaines hello des fonctionnalités de base de Windows PowerShell, cette interface possède les applets de commande dédiées supplémentaires pour la gestion d’un appareil StorSimple. |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la [sécurité StorSimple](storsimple-8000-security.md).

