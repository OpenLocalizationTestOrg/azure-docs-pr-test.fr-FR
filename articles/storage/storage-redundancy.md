---
title: "la réplication dans le stockage Azure aaaData | Documents Microsoft"
description: "Les données de votre compte Stockage Microsoft Azure sont répliquées à des fins de durabilité et de haute disponibilité. Les options de réplication incluent le stockage localement redondant (LRS), le stockage redondant dans une zone (ZRS), le stockage géo-redondant (GRS) et le stockage géo-redondant avec accès en lecture (RA-GRS)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 539bc54f57fe8cb661665d2788961a0783b5ae7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Réplication Azure Storage

Hello dans votre compte de stockage est toujours de Microsoft Azure répliquées tooensure la durabilité et la haute disponibilité. Copies de réplication hello de vos données, au sein même centre de données ou la deuxième centre de données tooa, selon l’option de réplication que vous choisissez. La réplication protège vos données et préserve votre application un temps d’exécution dans l’événement hello de défaillances matérielles temporaires. Si vos données sont répliquées tooa deuxième centre de données, il est protégé à partir d’une défaillance irrémédiable dans l’emplacement principal de hello.

La réplication garantit que votre compte de stockage répond aux hello [contrat de niveau de Service (SLA) pour le stockage](https://azure.microsoft.com/support/legal/sla/storage/) même en face de hello d’échecs. Consultez hello SLA pour plus d’informations sur le stockage Azure des garanties de durabilité et de disponibilité.

Lorsque vous créez un compte de stockage, vous pouvez sélectionner un des hello options de réplication suivantes :

* [Stockage localement redondant (LRS)](#locally-redundant-storage)
* [Stockage redondant dans une zone (ZRS)](#zone-redundant-storage)
* [Stockage géo-redondant (GRS)](#geo-redundant-storage)
* [Stockage géo-redondant avec accès en lecture (RA-GRS)](#read-access-geo-redundant-storage)

Stockage de géo-redondant avec accès en lecture (RA-GRS) est l’option par défaut de hello lorsque vous créez un compte de stockage.

Hello tableau suivant fournit une vue d’ensemble rapide des différences de hello entre LRS, ZRS, GRS et RA-GRS, tandis que les sections suivantes décrivent chaque type de réplication plus en détail.

| Stratégie de réplication | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Les données sont répliquées entre plusieurs centres de données. |Non |Oui |Oui |Oui |
| Données peuvent être lues à partir d’un emplacement secondaire, ainsi que les emplacement principal hello. |Non |Non |Non |Oui |
| Nombre de copies de données conservées sur des nœuds distincts. |3 |3 |6 |6 |

Consultez [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/) pour les informations de tarification pour les options de redondance différents hello.

> [!NOTE]
> Stockage Premium prend en charge uniquement un stockage localement redondant (LRS). Pour plus d’informations sur Stockage Premium, consultez [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md).
>

> [!NOTE]
> Le stockage de fichiers Azure prend uniquement en charge les comptes de stockage localement redondant (LRS) et les comptes de stockage géoredondant (GRS). Pour plus d’informations sur le stockage de fichiers Azure, consultez [Azure File storage overview](storage-files-introduction.md) (Vue d’ensemble du stockage de fichiers Azure).
>

## <a name="locally-redundant-storage"></a>Stockage localement redondant
Stockage localement redondant (LRS) réplique vos données trois fois au sein d’une unité d’échelle de stockage, qui est hébergée dans un centre de données dans la région de hello dans lequel vous avez créé votre compte de stockage. Une demande d’écriture retournée avec succès uniquement une fois qu’elle a été écrite tooall trois réplicas. Ces trois réplicas se trouvent dans des domaines d’erreur et de mise à niveau distincts dans une unité d’échelle de stockage.

Une unité d’échelle de stockage est un ensemble de racks de nœuds de stockage. Un domaine d’erreur (DP) est un groupe de nœuds qui représentent une unité physique de l’échec et peut être considéré comme nœuds appartenant toohello même rack physique. Un domaine de mise à niveau (ID) est un groupe de nœuds qui sont mis à jour ensemble pendant hello d’une mise à niveau de service (déploiement). Hello trois réplicas sont répartis entre les domaines d’erreur et de groupes au sein d’un stockage échelle unité tooensure que les données sont disponibles même si une défaillance matérielle affecte un rack ou lorsque les nœuds sont mis à niveau pendant un déploiement.

LRS est l’option hello moins coûteuse et offre des options de tooother la durabilité par rapport au moins. Dans événement hello d’un incident au niveau du centre de données (incendie, inondation etc.) les trois réplicas peuvent être perdues ou irrécupérable. toomitigate ce risque, stockage redondant de géo-réplication (GRS) est recommandé pour la plupart des applications.

Le stockage localement redondant peut toujours être adapté dans certains scénarios :

* Fournit la bande passante maximale la plus élevée de toutes les options de réplication Stockage Azure.
* Si votre application stocke des données qui peuvent être recréées facilement, vous pouvez opter pour un stockage LRS.
* Certaines applications sont tooreplicating restreint les données dans un pays en raison des exigences de gouvernance toodata. Une région jumelée peut être située dans un autre pays. Pour plus d’informations sur les régions jumelées, voir [Régions Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Stockage redondant dans une zone
Stockage à redondance de zone (ZRS) réplique vos données de façon asynchrone entre centres de données au sein d’une ou deux régions dans Ajout toostoring trois réplicas similaire tooLRS, et offrir ainsi une durabilité élevée au stockage LRS. Les données stockées dans le stockage ZRS sont durables même si hello de centre de données principal est indisponible ou irrécupérable.
Clients qui prévoient toouse ZRS Sachez que :

* Le stockage ZRS n’est disponible que pour les objets blob de blocs dans les comptes de stockage à usage général et est pris en charge uniquement dans les versions de service de stockage 2014-02-14 et ultérieures.
* Étant donné que la réplication asynchrone implique un délai, en cas de hello d’un sinistre local, qu'il est possible que les modifications qui n’ont pas encore été répliquées toohello secondaire seront perdue si les données de salutation ne peut pas être récupérées à partir de hello principal.
* réplica de Hello n’est peut-être pas disponible jusqu'à ce que Microsoft lance toohello basculement secondaire.
* Impossible de convertir les comptes ZRS ultérieurement tooLRS ou GRS. De même, un compte de stockage LRS ou GRS existant ne peut pas être converti du compte ZRS tooa.
* Les comptes ZRS n’ont pas de métriques ni de fonctionnalités de journalisation.

## <a name="geo-redundant-storage"></a>Stockage géo-redondant
Stockage géo-redondant (GRS) réplique vos données tooa région secondaire des centaines de miles en dehors de la région principale de hello. Si votre compte de stockage GRS est activé, vos données sont durables même en cas de hello de panne régionale totale ou de sinistre quels Bonjour la région principale n’est pas récupérable.

Pour un compte de stockage avec GRS est activé, une mise à jour est la première région principale toohello validée, où elle est répliquée trois fois. Puis répliquée de manière asynchrone le mise à jour hello région secondaire toohello, où il est aussi répliquée trois fois.

GRS, les deux régions principales et secondaires de hello gérer les réplicas sur plusieurs domaines d’erreur distincts et mettre à niveau des domaines au sein d’une unité d’échelle de stockage comme décrit avec LRS.

Considérations :

* Étant donné que la réplication asynchrone implique un délai, en cas de hello d’un sinistre régional, qu'il est possible que les modifications apportées et qui n’ont pas encore été répliqués toohello la région secondaire seront perdue si les données de salutation ne peut pas être récupérées à partir de la région principale de hello.
* réplica de Hello n’est pas disponible, sauf si Microsoft lance la région secondaire de basculement toohello. Si Microsoft n’initie pas une région secondaire toohello de basculement, vous aurez accès en lecture et écriture des données de toothat après que le basculement hello est terminé. Pour plus d’informations, consultez [Conseils sur la récupération d’urgence](storage-disaster-recovery-guidance.md). 
* Si une application veut tooread à partir de la région secondaire de hello, utilisateur de hello doit activer RA-GRS.

Lorsque vous créez un compte de stockage, vous sélectionnez la région principale de hello pour le compte de hello. région secondaire de Hello est déterminée en fonction de la région principale hello et ne peut pas être modifiée. Hello tableau suivant montre les couplages de région primaire et secondaire hello.

| Primaire | Secondaire |
| --- | --- |
| États-Unis - partie centrale septentrionale |Centre-Sud des États-Unis |
| Centre-Sud des États-Unis |États-Unis - partie centrale septentrionale |
| Est des États-Unis |Ouest des États-Unis |
| Ouest des États-Unis |Est des États-Unis |
| Est des États-Unis 2 |Centre des États-Unis |
| Centre des États-Unis |Est des États-Unis 2 |
| Europe du Nord |Europe de l'Ouest |
| Europe de l'Ouest |Europe du Nord |
| Asie du Sud-Est |Est de l'Asie |
| Est de l'Asie |Asie du Sud-Est |
| Chine orientale |Chine du Nord |
| Chine du Nord |Chine orientale |
| Est du Japon |Ouest du Japon |
| Ouest du Japon |Est du Japon |
| Sud du Brésil |Centre-Sud des États-Unis |
| Est de l’Australie |Sud-est de l’Australie |
| Sud-est de l’Australie |Est de l’Australie |
| Sud de l'Inde |Inde-Centre |
| Inde-Centre |Sud de l'Inde |
| Inde-Ouest |Sud de l'Inde |
| Gouvernement américain - Iowa |Gouvernement américain - Virginie |
| Gouvernement américain - Virginie |Gouvernement des États-Unis – Texas |
| Gouvernement des États-Unis – Texas |Gouvernement des États-Unis – Arizona |
| Gouvernement des États-Unis – Arizona |Gouvernement des États-Unis – Texas |
| Centre du Canada |Est du Canada |
| Est du Canada |Centre du Canada |
| Ouest du Royaume-Uni |Sud du Royaume-Uni |
| Sud du Royaume-Uni |Ouest du Royaume-Uni |
| Centre de l’Allemagne |Nord-Est de l’Allemagne |
| Nord-Est de l’Allemagne |Centre de l’Allemagne |
| Ouest des États-Unis 2 |Centre-Ouest des États-Unis |
| Centre-Ouest des États-Unis |Ouest des États-Unis 2 |

Pour obtenir des informations à jour sur les régions prises en charge par Azure, voir [Régions Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> La région secondaire du Gouvernement des États-Unis - Virginie est le Gouvernement des États-Unis - Texas. Auparavant, il s’agissait du Gouvernement des États-Unis - Iowa. Les comptes de stockage en utilisant nous Gov Iowa comme une région secondaire soient migrés tooUS Gov Texas comme une région secondaire. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Stockage géo-redondant avec accès en lecture
Stockage de géo-redondant avec accès en lecture (RA-GRS) optimise la disponibilité de votre compte de stockage, en fournissant des données de toohello d’accès en lecture seule dans l’emplacement secondaire de hello, en outre la réplication entre deux régions toohello fournie par GRS.

Lorsque vous activez des données de tooyour d’accès en lecture seule dans la région secondaire hello, vos données sont disponibles sur un point de terminaison secondaire, dans le point de terminaison addition toohello principal pour votre compte de stockage. point de terminaison secondaire Hello est le point de terminaison principal similaire toohello, mais ajoute le suffixe de hello `–secondary` toohello nom du compte. Par exemple, si votre point de terminaison principal pour hello service Blob est `myaccount.blob.core.windows.net`, votre point de terminaison secondaire est `myaccount-secondary.blob.core.windows.net`. clés d’accès Hello pour votre compte de stockage sont hello même pour les deux hello des points de terminaison principales et secondaire.

Considérations :

* Votre application a toomanage de point de terminaison qui interagit avec lors de l’utilisation de RA-GRS.
* Étant donné que la réplication asynchrone implique un délai, en cas de hello d’un sinistre régional, qu'il est possible que les modifications apportées et qui n’ont pas encore été répliqués toohello la région secondaire seront perdue si les données de salutation ne peut pas être récupérées à partir de la région principale de hello.
* Si Microsoft initie la région secondaire toohello de basculement, vous aurez accès en lecture et écriture des données de toothat après que le basculement hello est terminé. Pour plus d’informations, consultez [Conseils sur la récupération d’urgence](storage-disaster-recovery-guidance.md). 
* Le stockage RA-GRS est destiné à des fins de haute disponibilité. Pour obtenir des conseils d’évolutivité, passez en revue hello [liste de vérification de performances](storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Forum Aux Questions

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Comment puis-je modifier le type de réplication géo-réplication hello de mon compte de stockage ?

   Vous pouvez modifier le type de réplication hello géo-réplication de votre compte de stockage entre LRS, GRS, et à l’aide de RA-GRS hello [portail Azure](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) ou par programmation à l’aide d’un de nos nombreuses Client de stockage Bibliothèques. Notez que les comptes de stockage ZRS ne peuvent pas être convertis en comptes de stockage LRS ni GRS. De même, un compte de stockage LRS ou GRS existant ne peut pas être converti du compte ZRS tooa.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Il sera tout temps mort si je modifie le type de réplication hello de mon compte de stockage ?

   Non, il n’y a pas de temps d’arrêt.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Sera-t-il tous les coûts supplémentaires si je modifie le type de réplication hello de mon compte de stockage ?

   Oui. Si vous remplacez LRS tooGRS (ou RA-GRS) pour votre compte de stockage, il serait encourir des frais supplémentaires pour les sorties impliqués lors de la copie des données existantes à partir de l’emplacement secondaire de toohello emplacement principal. Une fois que les données initiales hello sont copiées n’est plus les frais de sortie supplémentaires pour géo réplication de données de hello d’emplacement de toosecondary principal hello. Détails de Hello pour les frais de bande passante sont accessibles sur hello [page de tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Si vous remplacez GRS tooLRS, il n’existe aucun coût supplémentaire, mais vos données seront supprimées à partir de l’emplacement secondaire de hello.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. En quoi un stockage RA-GRS peut-il m’aider ?
   
   Stockage GRS assure la réplication de vos données à partir d’une région secondaire tooa principal des centaines de miles en dehors de la région principale de hello. Dans ce cas, vos données sont durables même en cas de hello de panne régionale totale ou de sinistre quels Bonjour la région principale n’est pas récupérable. Stockage de RA-GRS comprend ce, plus il ajoute les données de salutation hello capacité tooread à partir de l’emplacement secondaire de hello. Pour quelques idées sur la façon tooleverage cette possibilité, consultez trop[conception hautement disponible d’Applications à l’aide du stockage de RA-GRS](storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Existe-t-il un moyen pour moi toofigure hors de sa durée tooreplicate mes données à partir de la région de hello toohello principal secondaire ?
   
   Si vous utilisez un stockage de RA-GRS, vous pouvez vérifier hello dernière heure de synchronisation de votre compte de stockage. Dernière heure de synchronisation est une valeur de date/heure GMT ; toutes les écritures principales avant hello dernière heure de synchronisation ont été correctement écrits toohello de site secondaire, ce qui signifie qu’ils sont disponible toobe lire à partir de l’emplacement secondaire de hello. Les écritures principales après hello dernière heure de synchronisation peut être ou non disponible pour les lectures encore. Vous pouvez interroger cette valeur à l’aide de hello [portail Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), ou par programme à l’aide de hello API REST ou l’un des hello bibliothèques clientes de stockage. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Comment puis-je basculer la région secondaire toohello s’il existe une panne dans la région principale de hello ?
   
   Consultez l’article de toohello [le toodo en cas de panne de stockage Azure](storage-disaster-recovery-guidance.md) pour plus d’informations.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. Ce qui est hello RPO et RTO avec GRS ?
   
   Objectif de Point de récupération (RPO) : Dans GRS et RA-GRS, stockage de hello asynchrone géo-réplication hello données de service à partir de l’emplacement secondaire de hello toohello principal. S’il existe un sinistre régional principal et un basculement a toobe effectuée, les modifications delta récentes qui n’ont pas été répliquées peuvent être perdues. nombre de Hello de minutes de perte de données potentielles est référencé tooas hello RPO (ce qui signifie point hello dans les données de temps toowhich peut être récupérée). En général, notre point RPO est inférieur à 15 minutes, même s’il n’existe actuellement aucun contrat de niveau de service sur la durée de la géoréplication.

   Objectif de temps de récupération (RTO) : Il s’agit d’une mesure de la durée pendant laquelle il nous prend toodo hello basculement et revenir compte de stockage hello en ligne si nous avons toodo un basculement. Hello temps toodo hello basculement inclut hello qui suit :
    * temps d’Hello nous nécessaire tooinvestigate et déterminer si nous pouvons récupérer des données de hello à l’emplacement principal de hello ou si nous devons toodo un basculement.
    * Compte hello en modifiant hello DNS entrées toopoint toohello secondaire emplacement principal.

   Nous prenons la responsabilité hello de préserver vos données très au sérieux, s’il existe toute possibilité de récupérer les données de hello, nous avons sera pas retenue procéder hello basculement et vous concentrer sur la récupération de données hello dans l’emplacement principal de hello. Bonjour future, nous prévoyons de tooprovide une API tooallow vous tootrigger un basculement à un niveau de compte, puis pour vous permettre de toocontrol hello RTO vous-même, mais cela n'est pas encore disponible.
   
## <a name="next-steps"></a>Étapes suivantes
* [Conception d’applications hautement disponibles à l’aide du stockage RA-GRS](storage-designing-ha-apps-with-ragrs.md)
* [Tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/)
* [À propos des comptes de stockage Azure](storage-create-storage-account.md)
* [Objectifs de performance et d’extensibilité du Stockage Azure](storage-scalability-targets.md)
* [Options de redondance et stockage géo-redondant avec accès en lecture de Stockage Microsoft Azure ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Document SOSP - Stockage Azure : service de stockage cloud à haute disponibilité et à cohérence forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

