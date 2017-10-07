---
title: pratiques aaaBest pour StorSimple Virtual Array | Documents Microsoft
description: "Décrit les meilleures pratiques de hello pour déployer et gérer hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Bonnes pratiques liées à StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Microsoft Azure StorSimple Virtual Array est une solution de stockage intégrée qui gère les tâches de stockage entre un appareil virtuel local exécuté dans un hyperviseur et le stockage cloud Microsoft Azure. StorSimple Virtual Array est efficace et économique, toohello autre 8000 series physique tableau. unité de stockage virtuelle Hello peut s’exécuter sur votre infrastructure de l’hyperviseur prend en charge hello iSCSI et protocoles SMB de hello et convient bien pour les scénarios impliquant des bureaux distants. Pour plus d’informations sur les solutions de StorSimple hello accédez trop[vue d’ensemble de Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

Cet article traite des recommandations hello implémentées au cours de la configuration initiale de hello, de déploiement et gestion de hello StorSimple Virtual Array. Ces meilleures pratiques fournissent des instructions validées pour le programme d’installation hello et la gestion de votre tableau virtuel. Cet article est ciblé vers hello informatique, administrateurs de déploiement et gérer hello des réseaux virtuels dans leurs centres de données.

Nous recommandons un examen périodique de hello meilleures pratiques toohelp vérifier que votre appareil est toujours en conformité lorsque des modifications sont apportées toohello le programme d’installation ou l’opération de flux. Si vous rencontrez des problèmes lors de l’implémentation de ces bonnes pratiques sur votre baie virtuelle, [contactez le support Microsoft](storsimple-virtual-array-log-support-ticket.md) pour obtenir une assistance.

## <a name="configuration-best-practices"></a>Bonnes pratiques de configuration
Ces meilleures pratiques couvrent les instructions hello nécessitant toobe suivi lors du déploiement de réseaux virtuels de hello et de la configuration initiale de hello. Ces meilleures pratiques incluent ces toohello associées de configuration de machine virtuelle de hello, les paramètres de stratégie de groupe, dimensionnement, paramétrage hello mise en réseau, la configuration des comptes de stockage et la création de partages et de volumes pour hello tableau virtuel. 

### <a name="provisioning"></a>Approvisionnement
StorSimple Virtual Array est un ordinateur virtuel (VM) configuré sur un hyperviseur hello (Hyper-V ou VMware) de votre serveur hôte. Lors de la configuration d’ordinateur virtuel de hello, assurez-vous que votre hôte est en mesure de toodedicate suffisamment de ressources. Pour plus d’informations, consultez trop[besoins en ressources minimale](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision un tableau.

Implémenter hello suivant les meilleures pratiques lors de la configuration d’unité de stockage virtuelle hello :

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Type de machine virtuelle** |**génération 2** à utiliser avec Windows Server 2012 ou version ultérieure et une image *.vhdx* . <br></br> **génération 1** à utiliser avec un serveur Windows Server 2008 ou version ultérieure et une image *.vhd* . |Utilisez la machine virtuelle version 8 - 11 lorsque vous utilisez une image *.vmdk* . |
| **Type de mémoire** |Configurez-la en tant que **mémoire statique**. <br></br> N’utilisez pas hello **mémoire dynamique** option. | |
| **Type de disque de données** |Sélectionnez **Taille dynamique**.<br></br> **Taille fixe** prend beaucoup de temps. <br></br> N’utilisez pas hello **différenciation** option. |Hello d’utilisation **mince disposition** option. |
| **Modification du disque de données** |L’expansion et la réduction ne sont pas autorisées. Une tentative toodo entraîne donc une perte de hello de toutes les données locales hello sur l’appareil. |L’expansion et la réduction ne sont pas autorisées. Une tentative toodo entraîne donc une perte de hello de toutes les données locales hello sur l’appareil. |

### <a name="sizing"></a>Dimensionnement
Lorsque vous dimensionnez vos StorSimple Virtual Array, tenez compte des hello suivant facteurs :

* Réservation locale pour des volumes ou des partages. Environ 12 % d’espace de hello est réservée au niveau local de hello pour chaque volume hiérarchisé configuré ou le partage. Environ 10 % d’espace de hello est également réservé pour un volume attaché localement pour le système de fichiers.
* Charge des instantanés. À peu près espace de 15 % sur le niveau de local hello est réservé pour les instantanés.
* Besoins liés aux restaurations. Si vous effectuez la restauration comme une nouvelle opération, dimensionnement doit prendre en compte pour l’espace hello nécessaire pour la restauration. Restauration est effectuée tooa partage ou volume Hello même taille.
* Une certaine mémoire tampon doit être allouée pour toute croissance inattendue.

Selon hello précédant les facteurs, hello exigences de dimensionnement peut être représenté par hello suivant l’équation :

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Hello exemples suivants illustrent comment vous pouvez redimensionner un tableau virtuel selon vos besoins.

#### <a name="example-1"></a>Exemple 1 :
Sur votre tableau virtuel, vous souhaitez toobe en mesure de

* configurer un partage ou un volume hiérarchisé de 2 To ;
* configurer un partage ou un volume hiérarchisé de 1 To ;
* configurer un partage ou un volume épinglé localement de 300 Go.

Pourquoi précédent volumes ou partages, faites-nous part calculer hello l’espace nécessaire sur le niveau de local hello.

Tout d’abord, pour chaque volume/partage hiérarchisé, réservation locale serait % too12 égale de taille du volume/partage hello. Pour hello attaché localement volume/partage, réservation locale est de 10 % de hello localement épinglé taille de volume/partage (en outre toohello configuré taille). Dans cet exemple, vous avez besoin

* d’une réservation locale de 240 Go (pour un partage/volume hiérarchisé de 2 To) ;
* d’une réservation locale de 120 Go (pour un partage/volume hiérarchisé de 1 To) ;
* 330 Go pour le volume attaché localement ou partage (en ajoutant 10 % de la taille de réservation locale toohello configuré de 300 Go)

Bonjour espace total nécessaire au niveau local de hello jusqu'à présent est : 240 Go + 120 Go + 330 = 690 go.

En second lieu, nous avons besoin d’au moins autant d’espace sur le niveau de local hello réservation unique plus grand de hello. Ce montant supplémentaire est utilisé en cas de besoin toorestore à partir d’un instantané cloud. Dans cet exemple, réservation locale plus grand de hello est 330 Go (y compris la réservation pour le système de fichiers), donc vous devez ajouter ce toohello 690 Go : 690 + 330 Go = 1020 go.
Si nous avons effectué les restaurations supplémentaires suivantes, nous pouvons toujours libérer hello à partir de l’opération de restauration précédente hello.

Troisièmement, nous avons besoin de 15 % de vos données totale d’espace jusqu'à présent toostore les instantanés locaux, afin que que 85 % de celui-ci est disponible. Dans cet exemple, cela représente environ 1 020 Go = 0,85&ast;To du disque de données configuré. Par conséquent, disque de données configurés hello serait (1020&ast;(1/0,85)) = 1 200 Go = 1,20 To ~ 1,25 To (arrondi à toonearest quartile)

En tenant compte de la croissance inattendue et de nouvelles restaurations, vous devez configurer un disque local d’environ 1,25 - 1,5 To.

> [!NOTE]
> Nous vous recommandons également de que ce disque local hello est alloué. Cette recommandation est, car l’espace de restauration hello est nécessaire uniquement lorsque vous souhaitez que les données toorestore datant de plus de cinq jours. Récupération au niveau de l’élément vous permet de données toorestore pour hello cinq jours sans nécessiter de hello espace supplémentaire pour la restauration.


#### <a name="example-2"></a>Exemple 2 :
Sur votre tableau virtuel, vous souhaitez toobe en mesure de

* configurer un volume hiérarchisé de 2 To ;
* configurer un volume épinglé localement de 300 Go.

En tenant compte des 12 % de réservation de l’espace local pour les partages/volumes hiérarchisés et des 10 % pour les partages/volumes épinglés localement, nous avons besoin

* d’une réservation locale de 240 Go (pour un partage/volume hiérarchisé de 2 To) ;
* 330 Go pour le volume attaché localement ou partage (en ajoutant 10 % d’espace de réservation locale toohello configuré de 300 Go)

Espace total nécessaire au niveau local de hello est : 240 Go + 330 = 570 Go

espace minimal local Hello nécessaire pour la restauration est 330 go.

15 % de votre disque total est utilisé toostore instantanés afin que seuls 0,85 est disponible. Par conséquent, la taille du disque hello est (900&ast;(1/0,85)) = to 1,06 ~ 1,25 To (arrondi à toonearest quartile)

En tenant compte d’une éventuelle croissance inattendue, vous pouvez configurer un disque local de 1,25 - 1,5 To.

### <a name="group-policy"></a>Stratégie de groupe
Stratégie de groupe est une infrastructure qui vous permet de tooimplement des configurations spécifiques pour les utilisateurs et ordinateurs. Les paramètres de stratégie de groupe sont contenus dans les objets de stratégie de groupe (GPO), qui sont lié toohello suivant des conteneurs de Services de domaine Active Directory (AD DS) : sites, domaines ou unités d’organisation (UO). 

Si votre tableau virtuel est joint au domaine, stratégie de groupe peut être appliquée tooit. Ces objets de stratégie de groupe peuvent installer des applications telles qu’un logiciel antivirus qui peut nuire aux opération hello Hello StorSimple Virtual Array.

Par conséquent, nous vous recommandons de :

* vous assurer que votre baie virtuelle figure dans sa propre unité d’organisation (UO) pour Active Directory ;
* Assurez-vous qu’aucun objet de stratégie de groupe (GPO) n’est tableau virtuel de tooyour appliquée. Vous pouvez bloquer l’héritage tooensure qui hello tableau virtuel (nœud enfant) n’hérite pas automatiquement les objets de stratégie du parent de hello. Pour plus d’informations, consultez trop[bloquer l’héritage](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Mise en réseau
configuration du réseau de votre tableau virtuel Hello est effectuée via l’interface utilisateur de web locale hello. Une interface réseau virtuelle est activée via l’hyperviseur hello dans lequel l’unité de stockage virtuelle hello est approvisionnée. Hello d’utilisation [paramètres réseau](storsimple-virtual-array-deploy3-fs-setup.md) page tooconfigure hello réseau virtuel interface adresse IP, sous-réseau et passerelle.  Vous pouvez également configurer le serveur DNS hello principaux et secondaire, les paramètres de temps et paramètres proxy pour votre appareil. La majeure partie de la configuration du réseau hello est une configuration unique. Hello de révision [StorSimple mise en réseau des exigences](storsimple-ova-system-requirements.md#networking-requirements) tableau virtuel de hello toodeploying préalable.

Lorsque vous déployez une baie virtuelle, nous vous recommandons d’appliquer les bonnes pratiques suivantes :

* Assurez-vous que ce réseau hello dans le hello tableau virtuel est toujours déployé a hello capacité toodedicate la bande passante de 5 Mbits/s Internet (ou plus).
  
  * Besoin de la bande passante Internet varie selon votre caractéristiques de charge de travail et le taux de hello de modification des données.
  * modification de données Hello qui peut être gérée est directement proportionnelle tooyour de bande passante Internet. Par exemple, lorsque vous effectuez une sauvegarde, une bande passante de 5 Mbits/s peut prendre en charge une modification des données d’environ 18 Go en 8 heures. Avec une bande passante quatre fois supérieure (20 Mbits/s), vous pouvez gérer une modification des données quatre fois supérieure (72 Go).
* Vérifiez la connectivité toohello Internet est toujours disponible. Périphériques de toohello de connexions Internet est sporadiques ou non fiables peuvent entraîner une perte de toodata d’accès dans le cloud de hello et entraîner une configuration non prise en charge.
* Si vous envisagez de votre appareil en tant que serveur iSCSI toodeploy :
  
  * Nous vous conseillons de désactiver hello **obtenir adresse IP automatiquement** option (DHCP).
  * Configurez des adresses IP statiques. Vous devez configurer un serveur DNS principal et un serveur DNS secondaire.
  * Si vous définissez plusieurs interfaces réseau sur votre tableau virtuel, uniquement hello première interface réseau (par défaut, cette interface est **Ethernet**) peut atteindre cloud de hello. type de hello toocontrol de trafic, vous pouvez créer plusieurs interfaces réseau virtuelles sur votre tableau virtuel (configuré comme un serveur iSCSI) et connecter ces sous-réseaux de toodifferent d’interfaces.
* toothrottle hello bande passante du cloud uniquement (utilisé par unité de stockage virtuelle hello), configurer la limitation sur le routeur de hello ou un pare-feu de hello. Si vous définissez la limitation dans votre hyperviseur, il sera limiter tous les protocoles de hello notamment iSCSI et SMB au lieu de la bande passante hello cloud uniquement.
* Assurez-vous que la synchronisation date/heure des hyperviseurs est activée. Si à l’aide de Hyper-V, sélectionnez votre tableau virtuel Bonjour Gestionnaire Hyper-V, passez trop**paramètres &gt; Integration Services**et vérifiez que hello **synchronisation de l’heure** est activée.

### <a name="storage-accounts"></a>Comptes de stockage
Une baie virtuelle StorSimple Virtual Array peut être associée à un compte de stockage unique. Ce compte de stockage peut être un compte de stockage généré automatiquement, un compte Bonjour même abonnement que le service de hello ou un compte de stockage liés tooanother abonnement. Pour plus d’informations, consultez Comment trop[gérer les comptes de stockage pour votre tableau virtuel](storsimple-virtual-array-manage-storage-accounts.md).

Hello utilisez conformément aux recommandations pour les comptes de stockage associés à votre tableau virtuel.

* Lors de la liaison de plusieurs réseaux virtuels avec un seul compte de stockage, du facteur de capacité maximale hello (64 To) pour un tableau virtuel et la taille maximale de hello (500 To) pour un compte de stockage. Cela limite le nombre de hello de réseaux virtuels en taille réelle qui peut être associé à cette tooabout de compte de stockage 7.
* Lors de la création d’un compte de stockage
  
  * Nous recommandons de créer dans hello région le plus proche toohello bureau distant/succursale où votre StorSimple Virtual Array est déployé toominimize latences.
  * N’oubliez pas que vous ne pouvez pas déplacer un compte de stockage d’une région à une autre. De plus, vous ne pouvez pas déplacer un service d’un abonnement à un autre.
  * Utilisez un compte de stockage qui implémente une redondance entre les centres de données hello. Le stockage géoredondant (GRS), le stockage redondant dans une zone (ZRS) et le stockage localement redondant (LRS) sont tous pris en charge avec votre baie virtuelle. Pour plus d’informations sur hello différents types de comptes de stockage, accédez trop[la réplication du stockage Azure](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Partages et volumes
Pour votre baie virtuelle StorSimple Virtual Array, vous pouvez mettre en service des partages lorsqu’elle est configurée comme un serveur de fichiers et des volumes lorsqu’elle est configurée comme un serveur iSCSI. Hello meilleures pratiques pour la création de partages et les volumes associés à ce type de taille et hello toohello configuré.

#### <a name="volumeshare-size"></a>Taille des volumes/partages
Sur votre baie virtuelle, vous pouvez mettre en service des partages lorsqu’elle est configurée comme un serveur de fichiers et des volumes lorsqu’elle est configurée comme un serveur iSCSI. Hello meilleures pratiques pour la création de partages et les volumes rapportent toohello taille et hello type configuré. 

Conservez Bonjour esprit suivant les meilleures pratiques lors de la configuration des partages ou volumes sur votre appareil virtuel.

* Hello tailles toohello relatif configuré une taille de fichier un partage hiérarchisé peut affecter les performances de hiérarchisation hello. L'utilisation de fichiers volumineux peut entraîner une montée en charge lente. Lorsque vous travaillez avec des fichiers volumineux, nous vous recommandons de que ce fichier le plus volumineux hello est inférieur à 3 % de la taille du partage hello.
* Un maximum de 16 volumes/partages peut être créé sur l’unité de stockage virtuelle hello. Pour les limites de taille hello Hello épinglé localement et à plusieurs niveaux de volumes/partages, font toujours référence toohello [StorSimple Virtual Array limite](storsimple-ova-limits.md).
* Lorsque vous créez un volume, le facteur de consommation de données hello attendu ainsi une croissance future. Impossible d’étendre le volume de Hello plus tard.
* Une fois que le volume de hello a été créé, vous ne peut pas réduire la taille hello du volume hello sur StorSimple.
* Lors de l’écriture de tooa à plusieurs niveaux volume sur StorSimple, lorsque des données de volume hello atteint un certain seuil (toohello relatif local espace réservé pour le volume de hello), e/s hello est limitée. Continuer toowrite toothis volume ralentit considérablement le hello e/s. Bien que vous pouvez écrire tooa à plusieurs niveaux de volume au-delà de sa capacité déployée (nous n’activement arrêtez pas utilisateur hello à partir de l’écriture au-delà de la capacité de hello configuré), vous voyez un effet de toohello de notification d’alerte que vous avez excédentaire. Une fois que vous voyez hello alerte, il est impératif de prendre des mesures correctives telles que supprimer des données de volume hello (extension de volume est actuellement pas pris en charge).
* Pour les cas d’utilisation de récupération d’urgence, comme nombre hello autorisée de volumes/partages est 16 et hello maximale nombre de partages/volumes pouvant être traités en parallèle est également 16, quantité, hello pour les volumes/partages n’a pas une incidence sur vos RPO et le RTO.

#### <a name="volumeshare-type"></a>Type de volume/partage
StorSimple prend en charge deux types de volume/partage basées sur l’utilisation de hello : localement épinglé et à plusieurs niveaux. Volumes/partages attachés localement sont approvisionnés tandis que hello hiérarchisés volumes/partages sont alloués dynamiquement. Impossible de convertir un tootiered volume/partage attaché localement ou *inversement* après sa création.

Nous vous recommandons d’implémenter hello suivant les meilleures pratiques lors de la configuration de volumes/partages de StorSimple :

* Identifier le type de volume hello selon les charges de travail hello que vous avez l’intention de toodeploy avant de créer un volume. Utilisez des volumes épinglés localement pour les charges de travail qui requièrent des garanties locales de données (même pendant une panne du cloud) et qui nécessitent de faibles temps de latence du cloud. Une fois que vous créez un volume sur votre tableau virtuel, vous ne pouvez pas modifier hello du type de volume à partir de tootiered attaché localement ou *inversement*. Par exemple, créez des volumes épinglés localement lors du déploiement de charges de travail SQL ou de charges de travail hébergeant des machines virtuelles ; utilisez des volumes hiérarchisés pour des charges de travail de partage de fichiers.
* Vérifiez l’option hello pour les données d’archive moins fréquemment utilisées lors du traitement de fichiers volumineux. Une plus grande taille de segment de la déduplication de 512 Ko est utilisée lorsque cette option est activée toohello cloud de transfert de données de hello tooexpedite.

#### <a name="volume-format"></a>Format des volumes
Après avoir créé des volumes StorSimple sur votre serveur iSCSI, vous devez tooinitialize et montage hello du format des volumes. Cette opération est effectuée sur l’appareil StorSimple hello hôte connecté tooyour. Meilleures pratiques suivantes sont recommandées lorsque monter et formater des volumes sur l’ordinateur hôte de hello StorSimple.

* Effectuez un formatage rapide sur tous les volumes StorSimple.
* Lorsque vous formatez un volume StorSimple, utilisez une taille d’unité d’allocation de 64 Ko (la valeur par défaut est de 4 Ko). Hello AUS de 64 Ko est basée sur les tests effectués en interne pour les charges de travail courantes StorSimple et autres charges de travail.
* Lorsque, à l’aide de hello StorSimple Virtual Array est configuré comme serveur iSCSI, n’utilisez pas des volumes fractionnés ou disques dynamiques en tant que ces volumes ou disques ne sont pas pris en charge par StorSimple.

#### <a name="share-access"></a>Accès aux partages
Lorsque vous créez des partages sur le serveur de fichiers de votre baie virtuelle, suivez ces instructions :

* Lorsque vous créez un partage, affectez un groupe d’utilisateurs en tant qu’administrateur de partage à la place d’un utilisateur individuel.
* Vous pouvez gérer les autorisations NTFS hello après avoir créé le partage de hello en modifiant les partages hello via l’Explorateur Windows.

#### <a name="volume-access"></a>Accès aux volumes
Lors de la configuration des volumes iSCSI hello sur votre tableau virtuel StorSimple, il est important de toocontrol accès chaque fois que nécessaire. toodetermine qui hébergent les serveurs permettre accéder aux volumes, créer et associer les enregistrements de contrôle d’accès (ACR) avec des volumes StorSimple.

Utilisez hello suivant les meilleures pratiques lors de la configuration ACR pour des volumes StorSimple :

* Associez toujours au moins un ACR à un volume.

* Lorsque vous affectez plusieurs volumes de tooa ACR, assurez-vous que le volume de hello n’est pas exposée d’une manière où il simultanément accessibles par plusieurs hôtes non cluster. Si vous avez attribué le volume de tooa plusieurs ACR, un message d’avertissement s’affiche pour vous tooreview votre configuration.

### <a name="data-security-and-encryption"></a>Chiffrement et sécurité des données
Votre StorSimple Virtual Array a contenant des fonctionnalités de sécurité et de chiffrement de données qui garantissent l’intégrité de vos données et de la confidentialité de hello. Lorsque vous utilisez ces fonctionnalités, nous vous recommandons de suivre ces bonnes pratiques : 

* Définir un chiffrement de clé toogenerate AES-256 de chiffrement de stockage cloud avant les données hello sont envoyées à partir de votre cloud de toohello tableau virtuel. Cette clé n’est pas requise si vos données sont chiffrée toobegin avec. Hello clé peut être générée et protégée à l’aide d’un système de gestion de clés comme [coffre de clés Azure](../key-vault/key-vault-whatis.md).
* Lors de la configuration du compte de stockage hello via le service StorSimple Manager hello, assurez-vous que vous activez hello SSL en mode toocreate un canal sécurisé pour la communication réseau entre votre appareil StorSimple et le hello cloud.
* Clés de régénérer hello pour vos comptes de stockage (par accéder au service de stockage Azure hello) tooaccount pour toute change régulièrement tooaccess selon hello modifié la liste des administrateurs.
* Données sur votre tableau virtuel sont compressées et dédupliquées avant d’être envoyée tooAzure. Nous ne recommandons pas à l’aide du service de rôle déduplication des données hello sur votre hôte Windows Server.

## <a name="operational-best-practices"></a>Bonnes pratiques opérationnelles
meilleures pratiques Hello sont des recommandations à suivre au cours de la gestion quotidienne de hello ou au fonctionnement de l’unité de stockage virtuelle hello. Ces pratiques couvrent les tâches de gestion spécifiques telles que la réalisation de sauvegardes, la restauration à partir d’un jeu de sauvegarde, effectuez un basculement, la désactivation et suppression hello groupe, surveiller l’utilisation de système et le contrôle d’intégrité, et en cours d’exécution antivirus analyse sur votre tableau virtuel.

### <a name="backups"></a>Sauvegardes
sauvegarde de données Hello sur votre tableau virtuel cloud toohello de deux manières, par défaut automatisée de sauvegarde quotidienne de hello appareil entière en commençant à 22 h 30, ou via une sauvegarde manuelle de la demande. Par défaut, les appareils hello crée automatiquement des instantanés cloud quotidiens de toutes les données hello résidant sur ce dernier. Pour plus d’informations, consultez trop[sauvegarder votre StorSimple Virtual Array](storsimple-virtual-array-backup.md).

Hello fréquence et rétention associé aux sauvegardes de hello par défaut ne peut pas être modifiées, mais vous pouvez configurer des temps de hello à quels hello les sauvegardes quotidiennes sont lancées chaque jour. Lors de la configuration d’heure de début hello hello des sauvegardes automatisées, nous vous recommandons :

* Planifiez vos sauvegardes pendant les heures creuses. L’heure de début de la sauvegarde ne doit pas coïncider avec un grand nombre d’E/S d’hôte.
* Lancer une sauvegarde manuelle de la demande lors de la planification tooperform un basculement de l’appareil ou de la fenêtre de maintenance toohello préalable, les données de salutation tooprotect sur votre tableau virtuel.

### <a name="restore"></a>Restauration
Vous pouvez restaurer une jeu de sauvegarde de deux manières : restaurer tooanother volume ou un partage ou d’effectuer une récupération au niveau élément (disponible uniquement sur un groupe virtuel configuré comme un serveur de fichiers). Récupération au niveau de l’élément vous permet de toodo une récupération granulaire de fichiers et dossiers à partir d’une sauvegarde sur le cloud de tous les partages de hello sur l’appareil StorSimple hello. Pour plus d’informations, consultez trop[restaurer à partir d’une sauvegarde](storsimple-virtual-array-clone.md).

Lorsque vous effectuez une restauration, gardez hello suivant les instructions à l’esprit :

* Votre baie virtuelle StorSimple Virtual Array ne prend pas en charge la restauration sur place. Il peut cependant être facilement atteints par un processus en deux étapes : libérer de l’espace sur hello virtual array, puis restaurez tooanother volume/partage.
* Lors de la restauration à partir d’un volume local, conserver dans la restauration de hello esprit sera une opération longue. Bien que le volume de hello peut rapidement en ligne, les données de salutation continuent toobe intégré dans l’arrière-plan de hello.
* type de volume Hello restent hello même pendant le processus de restauration hello. Restauration d’un volume hiérarchisé tooanother à plusieurs niveaux de volume et un volume attaché localement de tooanother de volume attaché localement.
* Lorsque la tentative de toorestore un volume ou un partage à partir d’un jeu de sauvegarde, si le travail de restauration hello échoue, un volume cible ou un partage peut toujours être créé dans le portail de hello. Il est important que vous supprimez ce volume cible inutilisées ou partagez dans toominimize de portail hello des problèmes futurs découlant de cet élément.

### <a name="failover-and-disaster-recovery"></a>Basculement et récupération d'urgence
Un basculement de l’appareil vous permet de toomigrate vos données à partir d’un *source* appareil dans hello datacenter tooanother *cible* périphérique trouver Bonjour même ou à un emplacement géographique différent. basculement de l’appareil Hello est pour l’ensemble de l’unité hello. Pendant le basculement, modification des données de cloud hello pour appareil de source de hello toothat de la propriété de l’appareil cible de hello.

Pour votre tableau virtuel StorSimple, vous ne pouvez basculer tooanother les tableau virtuel géré par hello même service StorSimple Manager. Un appareil de série tooan 8000 basculement ou un tableau géré par un autre service StorSimple Manager (que hello un périphérique de source de hello) n’est pas autorisé. toolearn en savoir plus sur les considérations de basculement hello, accédez trop[configuration requise pour le basculement de l’appareil hello](storsimple-virtual-array-failover-dr.md).

Lorsque vous effectuez un basculement sur de votre tableau virtuel, gardez les points suivants hello à l’esprit :

* Pour un basculement planifié, il s’agit d’un recommandée recommandées tootake hello basculement de tous les hello volumes/partages tooinitiating préalable hors connexion. Suivez les instructions de système d’exploitation spécifique hello tootake hello volumes/partages hors connexion sur hello héberger tout d’abord, puis d’exécuter celles hors connexion sur votre appareil virtuel.
* Une fichier serveur récupération d’urgence (DR), nous vous recommandons que vous joignez hello cible appareil toohello même domaine comme source de hello afin que hello des autorisations de partage sont résolues automatiquement. Uniquement hello basculement tooa appareil cible dans le même domaine est pris en charge dans cette version de hello.
* Une fois que hello récupération d’urgence est terminée avec succès, hello source appareil est automatiquement supprimé. Bien que l’appareil de hello n’est plus disponible, hello virtuels que vous avez configuré sur le système hôte de hello toujours consomme des ressources. Nous vous recommandons de supprimer cet ordinateur virtuel à partir de votre tooprevent de système hôte des frais d’accumulation.
* Notez que même si le basculement hello est infructueuse, **hello données sont toujours sécurisées dans le cloud de hello**. Tenez compte des hello dans quel hello basculement n’a pas réussi les trois scénarios suivants :
  
  * Une erreur s’est produite dans étapes initiales de hello du basculement hello telles que lorsque les vérifications préalables hello récupération d’urgence sont en cours d’exécution. Dans ce cas, votre appareil cible est toujours utilisable. Vous pouvez réessayer basculement hello sur hello même appareil cible.
  * Une erreur s’est produite pendant le processus de basculement réel hello. Dans ce cas, le périphérique cible de hello est marqué inutilisable. Vous devez mettre en service et configurer une autre baie virtuelle cible, et l’utiliser pour le basculement.
  * Hello basculement terminée suivant périphérique hello source a été supprimé mais équipement hello présente des problèmes, et vous ne pouvez pas accéder aux données. les données de salutation sont toujours sécurisées dans le cloud de hello et peuvent être facilement récupérées par la création d’un autre tableau virtuel, puis son utilisation en tant qu’un appareil cible pour la récupération d’urgence de hello.

### <a name="deactivate"></a>Désactivation
Lorsque vous désactivez un StorSimple Virtual Array, serveur de connexion hello entre l’appareil de hello et le service StorSimple Manager correspondant hello. La désactivation est une opération **définitive** et ne peut pas être annulée. Un appareil désactivé ne peut pas être inscrit à nouveau avec hello service StorSimple Manager. Pour plus d’informations, consultez trop[désactiver et supprimer vos StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).

Gardez hello suivant les meilleures pratiques à l’esprit lors de la désactivation de votre tableau virtuel :

* Prendre un instantané cloud de tous les toodeactivating du précédent en données hello un périphérique virtuel. Lorsque vous désactivez un tableau virtuel, toutes les données de l’appareil local hello est perdue. Un instantané de cloud vous permettra de toorecover données à un stade ultérieur.
* Avant de désactiver un StorSimple Virtual Array, assurez-vous que toostop ou supprimer des clients et les hôtes qui dépendent de cet appareil.
* Supprimez un appareil désactivé si vous ne l’utilisez plus, afin qu’il n’engendre pas de frais.

### <a name="monitoring"></a>Surveillance
tooensure votre StorSimple Virtual Array est dans un état sain en continu, vous devez toomonitor hello tableau et vous assurer que vous recevez des informations de système hello, y compris les alertes. toomonitor hello l’intégrité globale du tableau virtuel hello, hello implémentent suivant les meilleures pratiques :

* Configurer la surveillance tootrack hello l’utilisation du disque de votre disque de données de tableau virtuel ainsi que le disque du système d’exploitation hello. Si vous exécutez Hyper-V, vous pouvez utiliser une combinaison de System Center Virtual Machine Manager (SCVMM) et System Center Operations Manager (SCOM) toomonitor vos hôtes de virtualisation.
* Configurer des notifications par courrier électronique sur vos alertes de toosend tableau virtuel des niveaux d’utilisation.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Applications d’analyse antivirus et de recherche d’index
Un tableau virtuel StorSimple peut automatiquement de niveau données hello couche local toohello cloud Microsoft Azure. Lorsqu’une application telle qu’une recherche d’index ou une analyse antivirus est utilisé tooscan hello présentes sur StorSimple, vous devez les soins tootake que les données du cloud hello ne pas obtenir accessibles et extraite nouveau niveau de local toohello.

Nous vous recommandons d’implémenter hello suivant les meilleures pratiques lors de la configuration d’analyse d’index hello recherche ou virus sur votre tableau virtuel :

* Désactivez toutes les opérations d’analyse complète configurées automatiquement.
* Pour les volumes hiérarchisés, configurez hello index recherche ou virus analyse application tooperform une analyse incrémentielle. Cette recherche uniquement hello nouvelle données susceptibles de résidant sur le niveau de local hello. données Hello toohello hiérarchisé cloud ne sont pas accessible lors d’une opération incrémentielle.
* Vérifiez hello des filtres de recherche correcte et est configuré afin que seuls les types hello prévu des fichiers sont analysés. Par exemple, les fichiers (GIF, JPEG et TIFF) de l’image et dessins techniques ne doivent pas être analysés au cours de la reconstruction de l’index incrémentielle ou complète hello.

Si vous utilisez le processus d’indexation de Windows, suivez ces instructions :

* N’utilisez pas hello indexeur de Windows pour les volumes hiérarchisés comme il rappelle les grandes quantités de données (To) à partir du cloud de hello si l’index hello doit toobe reconstruit fréquemment. La reconstruction d’index de hello doit extraire tous les tooindex de types de fichier leur contenu.
* Utiliser Windows hello l’indexation de processus pour les volumes attachés localement qu’il serait accéder aux données uniquement sur l’index de hello toobuild hello niveaux local (cloud hello données ne seront pas accessible).

### <a name="byte-range-locking"></a>Verrouillage de plage d’octets
Les applications peuvent verrouiller une plage d’octets spécifiée dans les fichiers de hello. Si le verrouillage de plage d’octets est activé sur les applications hello écrivent tooyour StorSimple, puis hiérarchisation ne fonctionne pas sur votre tableau virtuel. Pour toowork de hiérarchisation hello, toutes les zones de hello les fichiers doivent être déverrouillées. Le verrouillage de plage d’octets n’est pas pris en charge avec les volumes hiérarchisés sur votre baie virtuelle.

Recommandé de mesures de verrouillage de plage d’octets tooalleviate incluent :

* Désactivez le verrouillage de plage d'octets dans la logique de votre application.
* Utilisez localement épinglé volumes (au lieu de niveaux) pour les données hello associées à cette application. Les volumes attachés localement ne pas de niveau dans le cloud de hello.
* Lorsque vous à l’aide d’attaché localement de volumes avec le verrouillage de plage octets est activé, volume de hello peut provenir d’en ligne avant la restauration hello est terminée. Dans ce cas, vous devez attendre hello toobe de restauration complète.

## <a name="multiple-arrays"></a>Baies multiples
Plusieurs réseaux virtuels peut-être toobe déployé tooaccount pour un jeu de travail croissante des données peuvent déborder sur le cloud hello affectant ainsi les performances hello du périphérique de hello. Dans ce cas, il est meilleure tooscale périphériques comme jeu de travail hello augmente. Cela nécessite un ou plusieurs toobe périphériques ajoutés dans le centre de données local hello. Lors de l’ajout de périphériques de hello, vous pouvez :

* Hello fractionnement actuel jeu de données.
* Déployer des charges de travail toonew de nouveaux périphériques.
* Si vous déployez plusieurs réseaux virtuels, nous recommandons que l’équilibrage de charge de point de vue, distribuer de tableau de hello sur les hôtes hyperviseur différents.
* Plusieurs baies virtuelles (lorsqu’elles sont configurées en tant que serveur de fichiers ou serveur iSCSI) peuvent être déployées dans un espace de noms de système de fichiers distribué. Pour des instructions détaillées, consultez trop[Distributed File System Namespace Solution avec le Guide de déploiement du stockage Cloud hybride](https://www.microsoft.com/download/details.aspx?id=45507). Réplication de système de fichiers distribués n’est actuellement pas recommandée pour une utilisation avec l’unité de stockage virtuelle hello. 

## <a name="see-also"></a>Voir aussi
Découvrez comment trop[administrer votre StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md) via hello service StorSimple Manager.

