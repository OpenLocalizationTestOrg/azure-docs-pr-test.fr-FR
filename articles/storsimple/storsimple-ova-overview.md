---
title: "vue d’ensemble de Azure StorSimple Virtual Array aaaMicrosoft | Documents Microsoft"
description: "Décrit les hello StorSimple Virtual Array, une solution de stockage intégrée qui gère les tâches de stockage entre un tableau de virtuel local et le stockage en cloud Microsoft Azure."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Introduction toohello StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Hello Microsoft Azure StorSimple Virtual Array est une solution de stockage intégrée qui gère les tâches de stockage entre un tableau virtuel local en cours d’exécution dans un hyperviseur et le stockage en cloud Microsoft Azure. unité de stockage virtuelle Hello est une solution de serveur iSCSI qui élimine la plupart des problèmes de hello et les dépenses liées à la protection des données et de stockage d’entreprise ou un serveur de fichiers efficace, rentable et facile à gérer. unité de stockage virtuelle Hello est particulièrement bien adaptée pour les scénarios impliquant des bureaux distants.

Cette rubrique fournit une vue d’ensemble du tableau de virtuel hello - Voici quelques autres ressources :

* Pour parcourir les bonnes pratiques, voir [Bonnes pratiques liées à StorSimple Virtual Array](storsimple-ova-best-practices.md).
* Pour une vue d’ensemble de périphériques hello StorSimple 8000, accédez trop[série StorSimple 8000 : une solution de cloud hybride](storsimple-overview.md). 
* Pour plus d’informations sur les périphériques série hello StorSimple 5000/7000, consultez trop[aide en ligne StorSimple](http://onlinehelp.storsimple.com/).

unité de stockage virtuelle Hello prend en charge hello iSCSI ou le protocole (Server Message Block). Il s’exécute sur votre infrastructure existante de l’hyperviseur et fournit la hiérarchisation du cloud de toohello, sauvegarde sur le cloud, une restauration rapide, récupération au niveau élément et les fonctionnalités de récupération d’urgence.

Hello tableau suivant résume les hello fonctionnalités importantes de hello StorSimple Virtual Array.

| Fonctionnalité | Baie virtuelle StorSimple |
| --- | --- |
| Configuration requise |Utilise l'infrastructure de virtualisation (Hyper-V ou VMware) |
| Availability |Nœud unique |
| Capacité totale (y compris le cloud) |Des too64 to de capacité utilisable par tableau virtuel |
| Capacité locale |390 too6.4 To utilisable Go par unité de stockage virtuelle (besoin tooprovision 500 Go too8 to d’espace disque) |
| Protocoles natifs |iSCSI ou SMB |
| Objectif de délai de récupération (RTO) |iSCSI : moins de 2 minutes, quelle que soit la taille |
| Objectif de point de récupération (RPO) |Sauvegardes quotidiennes et sauvegardes à la demande |
| Hiérarchisation du stockage |Chaleur toodetermine mappage quelles données doivent être placées in ou out |
| Support |Infrastructure de virtualisation pris en charge par le fournisseur de hello |
| Performances |Varie en fonction de l'infrastructure sous-jacente |
| Mobilité des données |Peut restaurer toohello même appareil ou au niveau élément recovery (serveur de fichiers) |
| Niveaux de stockage |Cloud et stockage sur l'hyperviseur local |
| Taille du partage |À plusieurs niveaux : jusqu'à too20 to ; attaché localement : jusqu'à too2 to |
| Taille du volume |À plusieurs niveaux : To de too5 de 500 Go ; attaché localement : 50 Go too500 Go |
| Taille du volume |À plusieurs niveaux : jusqu'à too5 to ; attaché localement : jusqu'à too500 Go |
| Instantanés |Cohérence en cas d’incident |
| Récupération au niveau de l'élément |Oui. Les utilisateurs peuvent restaurer à partir de partages |

## <a name="why-use-storsimple"></a>Pourquoi utiliser StorSimple ?
StorSimple connecte à des utilisateurs et des serveurs de stockage de tooAzure en minutes, sans modification de l’application.

Hello tableau suivant décrit quelques-uns des avantages clés de hello que hello StorSimple Virtual Array fournit des solutions.

| Fonctionnalité | Avantage |
| --- | --- |
| Intégration transparente |unité de stockage virtuelle Hello prend en charge hello iSCSI ou le protocole SMB de hello. déplacement des données entre les couches locales hello et hello cloud Hello est transparente et transparent toohello utilisateur. |
| Coûts de stockage réduits |StorSimple, vous fournir suffisamment toomeet des besoins actuels de stockage local pour les données à chaud hello plus utilisé. Lorsque les besoins de stockage augmentent, StorSimple fait passer les données brutes vers le stockage cloud économique. Hello dédupliquées et données compressées avant d’envoyer toohello cloud toofurther réduire les besoins de stockage et les coûts. |
| Gestion simplifiée du stockage |StorSimple offre une gestion centralisée dans le cloud hello à l’aide du Gestionnaire de périphériques StorSimple toomanage plusieurs appareils. |
| Récupération d’urgence et conformité améliorées |StorSimple facilite la récupération d’urgence plus rapide en restaurant les métadonnées de hello immédiatement et de restauration des données de hello en fonction des besoins. Cela signifie que les opérations normales peuvent se poursuivre, avec une interruption minimale. |
| Mobilité des données |Données à plusieurs niveaux toohello cloud sont accessibles à partir d’autres sites à des fins de récupération et de migration. Notez que vous pouvez restaurer les données uniquement toohello tableau d’origine virtuel. Toutefois, vous utilisez d’urgence récupération fonctionnalités toorestore hello tableau virtuel entier tooanother virtuel tableau. |

## <a name="storsimple-workload-summary"></a>Résumé des charges de travail StorSimple

Voici un tableau résumant les charges de travail StorSimple prises en charge.

|Scénario     |Charge de travail     |Pris en charge      |Restrictions               |
|-------------|-------------|---------------|---------------------------|
|Collaboration ROBO |Partage de fichiers     |Oui      |Consultez les [limites maximales pour le serveur de fichiers](storsimple-ova-limits.md).<br></br>Consultez la [configuration système requise pour les versions SMB prises en charge](storsimple-ova-system-requirements.md).| Toutes les versions     |

## <a name="workflows"></a>Flux de travail
Hello StorSimple Virtual Array est particulièrement adaptée pour hello suivant du flux de travail :

* [Gestion du stockage sur le cloud](#cloud-based-storage-management)
* [Sauvegarde indépendante de l'emplacement](#location-independent-backup)
* [Récupération d'urgence et protection des données](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>Gestion du stockage sur le cloud
Vous pouvez utiliser le service de gestionnaire de périphériques StorSimple hello Bonjour Azure toomanage portail les données stockées sur plusieurs appareils et dans plusieurs emplacements en cours d’exécution. Ceci est particulièrement utile dans les scénarios de succursales distribuées. Notez que vous devez créer des instances distinctes de tableaux de toomanage de service Gestionnaire de périphériques StorSimple hello virtuel et les appareils StorSimple physiques. Notez également qu’un groupe virtuel hello utilise désormais le nouveau portail de Azure hello au lieu de hello portail Azure classic.

![Gestion du stockage sur le cloud](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Sauvegarde indépendante de l'emplacement
Tableau de virtuel hello, instantanés cloud de fournir une copie indépendante de l’emplacement point-à-temps d’un volume ou un partage. Les instantanés cloud sont activés par défaut et ne peuvent pas être désactivés. Tous les volumes et les partages sont la sauvegarde à hello même moment, via une stratégie de sauvegarde quotidienne unique et effectuer les sauvegardes ad-hoc supplémentaires chaque fois que nécessaire.

### <a name="data-protection-and-disaster-recovery"></a>Récupération d'urgence et protection des données
unité de stockage virtuelle Hello prend en charge hello suivant des scénarios de récupération d’urgence et de protection de données :

* **Restauration de volume ou partage** : utiliser hello restauration en tant que nouveau flux de travail toorecover un volume ou partage. Utilisez cette approche toorecover hello tout le volume ou le partage.
* **Récupération au niveau de l’élément** – partages autoriser un accès simplifié toorecent sauvegardes. Vous pouvez facilement récupérer un fichier individuel à partir d’un spécial *.backup* dossier disponible dans le cloud de hello. Cette fonctionnalité de restauration est contrôlée par l'utilisateur et aucune intervention de l'administrateur n'est nécessaire.
* **Récupération d’urgence** – utilisez hello toorecover de capacité de basculement de tous les volumes ou partages tooa nouveau tableau virtuel. Vous créez tableau virtuel hello et inscrivez auprès de hello service du Gestionnaire de périphériques StorSimple, puis basculez tableau virtuel d’origine de hello. nouveau tableau de virtuel Hello puis suppose que les ressources hello configuré. 

## <a name="storsimple-virtual-array-components"></a>Composants du système StorSimple Virtual Array
unité de stockage virtuelle Hello inclut hello suivant des composants :

* [Groupe virtuel](#virtual-array) : appareil de stockage cloud hybride basé sur une machine virtuelle, configurée dans votre hyperviseur ou environnement virtualisé.  
* [Le Gestionnaire de périphériques StorSimple service](#storsimple-device-manager-service) : extension de hello portail Azure qui vous permet de gérer un ou plusieurs périphériques StorSimple à partir d’une seule interface web que vous pouvez accéder à partir de différents emplacements géographiques. Vous pourrez utiliser toocreate de service de gestionnaire de périphériques StorSimple hello et gérer les services, afficher et gérer les périphériques et les alertes et gérer les volumes, partages et les instantanés existants.
* [Interface utilisateur web locale](#local-web-user-interface) – une interface utilisateur web que tooconfigure utilisé hello appareil afin qu’il peut se connecter le réseau local de toohello et puis inscrire hello auprès de service du Gestionnaire de périphériques StorSimple hello. 
* [Interface de ligne de commande](#command-line-interface) – une interface Windows PowerShell que vous pouvez utiliser toostart une session de prise en charge sur l’unité de stockage virtuelle hello.
  Hello sections suivantes décrivent chacun de ces composants de manière plus détaillée et expliquent comment les solutions hello organise les données, alloue du stockage et facilitent la gestion du stockage et protection des données.

### <a name="virtual-array"></a>Virtual Array
tableau virtuel de Hello est une solution de stockage d’à nœud unique qui fournit le stockage principal, gère la communication avec le stockage cloud et vous aide à la sécurité de hello tooensure et la confidentialité de toutes les données stockées sur le périphérique de hello.

unité de stockage virtuelle Hello est disponible dans un modèle qui est disponible en téléchargement. unité de stockage virtuelle Hello a une capacité maximale de 6,4 To sur un périphérique hello (avec une exigence de stockage sous-jacent de 8 To) et 64 To, y compris le stockage cloud. 

unité de stockage virtuelle Hello a hello suivant de fonctionnalités :

* Il est économique. Il utilise votre infrastructure de virtualisation existante et peut être déployé sur votre hyperviseur Hyper-V ou VMware existant.
* Il se trouve dans le centre de données hello et peut être configuré comme un serveur iSCSI ou un serveur de fichiers. 
* Il est intégré avec le cloud de hello.
* Sauvegardes sont stockées dans le cloud hello, ce qui peut faciliter la récupération d’urgence et de simplifier la récupération au niveau de l’élément (ILR). 
* Vous pouvez appliquer tableau virtuel toohello de mises à jour, tout comme vous pouvez l’appliquer les tooa des périphériques physiques.

> [!NOTE]
> Une instance Virtual Array ne peut pas être développée. Par conséquent, il est important tooprovision du stockage approprié lorsque vous créez l’unité de stockage virtuelle hello. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Service StorSimple Device Manager
Microsoft Azure StorSimple fournit une interface utilisateur basée sur le web, hello service StorSimple le Gestionnaire de périphériques, ce qui permet de vous toocentrally gérer le stockage StorSimple. Vous pouvez utiliser hello de tooperform du service de gestionnaire de périphériques StorSimple hello tâches suivantes :

* Gérer plusieurs StorSimple Virtual Arrays à partir d'un service unique. 
* Configurer et gérer les paramètres de sécurité pour les instances StorSimple Virtual Array. (Le chiffrement dans le cloud de hello est dépendant de l’API Microsoft Azure.)
* Configurer les propriétés et les informations d'identification du compte de stockage.
* Configurer et gérer des volumes ou des partages.
* Sauvegarder et restaurer des données sur des volumes ou des partages.
* Analyser les performances.
* Passer en revue les paramètres système et identifier les problèmes possibles.

Vous utilisez hello le Gestionnaire de périphériques StorSimple service tooperform administration quotidiennes de votre tableau virtuel.

Pour plus d’informations, consultez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interface utilisateur web locale
unité de stockage virtuelle Hello inclut une interface utilisateur web qui est utilisée pour une configuration unique et l’inscription de l’unité de hello avec hello service du Gestionnaire de périphériques StorSimple. Vous pouvez l’utiliser tooshut vers le bas et redémarrer tableau virtuel de hello, exécuter les tests de diagnostic, mettre à jour de logiciel, modifier le mot de passe administrateur de périphérique hello, afficher les journaux système et contactez le Support technique de Microsoft toofile une demande de service. 

Pour plus d’informations sur l’utilisation de hello interface utilisateur basée sur le web, accédez trop[utilisez hello tooadminister de l’interface utilisateur basée sur le web de votre tableau virtuel StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interface de ligne de commande
interface de Windows PowerShell Hello inclus vous permet de tooinitiate une session de prise en charge avec le Support technique de Microsoft afin qu’ils peuvent vous aider à dépanner et résoudre les problèmes que vous pouvez rencontrer sur votre tableau virtuel.

## <a name="storage-management-technologies"></a>Technologies de gestion de stockage
En outre les tableau virtuel toohello et autres composants, hello StorSimple solution utilise hello suivant software technologies tooprovide accès rapide tooimportant données, réduire la consommation de stockage et protéger les données stockées sur votre tableau virtuel :

* [Hiérarchisation automatique du stockage](#automatic-storage-tiering) 
* [Partages et volumes épinglés localement](#locally-pinned-shares-and-volumes)
* [La déduplication et compression de données à plusieurs niveaux ou sauvegardées toohello cloud](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Sauvegardes à la demande et planifiées](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Hiérarchisation automatique du stockage
unité de stockage virtuelle Hello utilise une nouvelle hiérarchisation système toomanage stockée les données sur cloud de tableau et hello virtuel hello. Il existe deux niveaux : unité de stockage virtuelle hello local et Azure le stockage cloud. Hello StorSimple Virtual Array organise automatiquement les données en niveaux hello basés sur une carte thermique, qui effectue le suivi des données de tooother en cours d’utilisation, l’âge et les relations. Les données qui sont plus actifs (la plus sensible) sont stockées localement, tandis que les données les moins actives et inactives sont automatiquement migrées toohello cloud. (Toutes les sauvegardes sont stockées dans le cloud de hello). StorSimple ajuste et réorganise les données et modifie les affectations de stockage conformément aux modifications du schéma d’utilisation. Par exemple, certaines informations peuvent devenir moins actives au fil du temps. Dès qu’il sera progressivement moins actif, il est hiérarchisé out toohello cloud. Si ces mêmes données redevient actives, il est hiérarchisé dans la baie de stockage toohello.

Les données d’un partage ou d’un volume spécifique à plusieurs niveaux sont sûres de disposer de leur propre espace de niveau local (environ 10 % de l’espace total alloués, hello pour ce partage ou de volume). Alors que cela réduit le stockage disponible de hello sur tableau virtuel de hello pour ce partage ou le volume, elle garantit que hiérarchisation pour un partage ou volume n'est pas affecté par des impératifs de hiérarchisation hello de partages ou des autres volumes. Par conséquent, une charge de travail très occupé sur un partage ou volume ne peut pas forcer tous les autres cloud toohello de charges de travail. 

![Hiérarchisation automatique du stockage](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Vous pouvez spécifier un volume attaché localement, auquel cas les données de salutation restent sur l’unité de stockage virtuelle hello et ne sont jamais hiérarchisé toohello cloud. Pour plus d’informations, consultez trop[attaché localement les partages et les volumes](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Partages et volumes épinglés localement
Vous pouvez créer des partages et volumes appropriés comme étant épinglés localement. Cette fonctionnalité garantit que les données requises par les applications critiques restent dans le tableau de virtuel hello et qu’il ne sont jamais hiérarchisé toohello cloud. Partages attachés localement et les volumes ont hello suivant de fonctionnalités : 

* Ils ne sont pas les latences toocloud sujet ou des problèmes de connectivité.
* Ils bénéficient toujours des fonctionnalités de récupération d'urgence et de sauvegarde cloud de StorSimple.

Vous pouvez restaurer un partage ou volume épinglé localement sous la forme à plusieurs niveaux, ou restaurer un partage ou volume à plusieurs niveaux sous la forme épinglé localement. 

Pour plus d’informations sur les volumes attachés localement, accédez trop[utiliser le Gestionnaire de périphériques StorSimple hello service des volumes toomanage](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>La déduplication et compression de données à plusieurs niveaux ou sauvegardées toohello cloud
StorSimple utilise la déduplication et données compression toofurther réduire les besoins de stockage dans le cloud de hello. La déduplication réduit hello quantité globale des données stockées en éliminant les redondances dans le jeu de données stockée hello. Informations que les modifications apportées, StorSimple ignore les données de salutation inchangée et captures hello uniquement les modifications. En outre, StorSimple réduit la quantité hello de données stockées en identifiant et en supprimant les informations en double. 

> [!NOTE]
> Données stockées sur l’unité de stockage virtuelle hello ne sont pas dédupliquées ou compressées. Toutes la déduplication et la compression se produit juste avant que les données hello sont envoyées toohello cloud.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Sauvegardes à la demande et planifiées
Fonctionnalités de protection des données StorSimple permettent de toocreate des sauvegardes à la demande. En outre, une planification de sauvegarde par défaut garantit que les données sont sauvegardées quotidiennement. Les sauvegardes sont effectuées sous forme de hello d’instantanés incrémentiels, qui sont stockés dans le cloud de hello. Instantanés, qui enregistrent uniquement les modifications de hello depuis la dernière sauvegarde de hello, peuvent être créés et restaurés rapidement. Ces instantanés peuvent être extrêmement importants dans les scénarios de récupération d’urgence, car elles remplacement les systèmes de stockage secondaire (par exemple, une sauvegarde sur bande) et autoriser des sites de centre de données ou tooalternate la tooyour des données toorestore si nécessaire.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[préparer le portail de tableau virtuel hello](storsimple-virtual-array-deploy1-portal-prep.md).

