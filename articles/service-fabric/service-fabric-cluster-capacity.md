---
title: "aaaPlanning hello la capacité de cluster Service Fabric | Documents Microsoft"
description: "Considérations en matière de planification de la capacité du cluster Service Fabric. Types de nœuds, durabilité et niveaux de fiabilité"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Considérations en matière de planification de la capacité du cluster Service Fabric
Pour un déploiement de production, la planification de la capacité est une étape importante. Voici certains éléments hello que vous avez tooconsider dans le cadre de ce processus.

* vos besoins de cluster toostart out avec les types nombre Hello du nœud
* propriétés Hello de chaque type de nœud (taille, principal, et internet en vis-à-vis, le nombre de machines virtuelles, etc.).
* caractéristiques de fiabilité et de durabilité Hello du cluster de hello

Nous allons présenter brièvement chacun de ces éléments.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>vos besoins de cluster toostart out avec les types nombre Hello du nœud
Tout d’abord, vous devez toofigure est en train de toobe utilisé pour le cluster hello que vous créez et quels types d’applications que vous prévoyez toodeploy dans ce cluster. Si vous n’êtes pas effacer dans le but hello du cluster de hello, vous ne sont probablement pas encore prêt du processus de planification de capacité tooenter hello.

Établir le nombre de hello de votre cluster doit toostart out avec des types de nœuds.  Chaque type de nœud est mappé tooa ensemble d’échelle de Machine virtuelle. Chaque type de nœud peut ensuite faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité. Par conséquent, décision hello du nombre de hello des types de nœuds revient essentiellement de toohello suivant considérations :

* Votre application a-t-elle plusieurs services, et certains d'entre eux doivent toobe public ou connecté à internet ? Les applications contiennent un service frontal passerelle qui reçoit l’entrée d’un client et un ou plusieurs services principaux qui communiquent avec les services frontaux hello. Par conséquent, dans ce cas, vous avez besoin d’au moins deux types de nœuds.
* Vos services (qui composent votre application) ont-ils des besoins d’infrastructure différents tels qu’une RAM plus volumineuse ou des cycles processeur plus élevés ? Par exemple, supposons que cette application hello que vous souhaitez toodeploy contient un service frontal et un service principal. Hello service frontal peut s’exécuter sur des machines virtuelles plus petits (les tailles de machine virtuelle comme D2) pour lesquels les ports à ouvrir toohello internet.  service principal de Hello, toutefois, est toorun de calcul intensif et des besoins sur des machines virtuelles plus volumineux (avec des tailles de machine virtuelle comme D4, D6, D15) qui ne sont pas internet face.
  
  Dans cet exemple, bien que vous pouvez décider tooput tous hello services sur le type d’un nœud, il est recommandé que vous les placez dans un cluster avec deux types de nœuds.  Ainsi, pour chaque nœud type toohave distinctes les propriétés telles que la connectivité internet ou de la taille de machine virtuelle. nombre de Hello de machines virtuelles peut être monté en indépendamment, ainsi.  
* Étant donné que vous ne pouvez pas prédire hello futur, accédez avec les informations que vous connaissez et décidez nombre hello des types de nœuds vos applications ont besoin toostart avec. Vous pourrez toujours ajouter ou supprimer des types de nœuds ultérieurement. Un cluster Service Fabric doit comprendre au moins un type de nœud.

## <a name="hello-properties-of-each-node-type"></a>propriétés de Hello de chaque type de nœud
Hello **type de nœud** peut être considéré comme équivalent tooroles dans les Services de cloud computing. Les types de nœud définissent les tailles de machine virtuelle hello, hello nombre de machines virtuelles et leurs propriétés. Chaque type de nœud qui est défini dans un cluster Service Fabric est configuré en tant que groupe de machines virtuelles identiques distinct. Ensemble d’échelle de machine virtuelle est une ressource de calcul Azure, vous pouvez utiliser toodeploy et gérer une collection d’ordinateurs virtuels en tant qu’ensemble. Chaque type de nœud est défini comme un groupe de machines virtuelles identiques distinct et peut faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.

Lecture [ce document](service-fabric-cluster-nodetypes.md) pour plus d’informations sur la relation hello de Nodetypes toovirtual machines identiques, comment tooRDP dans une des instances de hello, ouverture de nouveaux ports etc..

Votre cluster peut avoir plus d’un type de nœud, mais type de nœud principal hello (hello un premier que vous définissez sur le portail hello) doit avoir au moins cinq ordinateurs virtuels de clusters utilisés pour les charges de production (ou au moins trois machines virtuelles pour les clusters de test). Si vous créez à l’aide d’un modèle de gestionnaire de ressources de cluster de hello, puis recherchez **est Primary** attribut sous la définition de type de nœud hello. type de nœud principal Hello est type de nœud hello où sont placés les services de système de Service Fabric.  

### <a name="primary-node-type"></a>Type de nœud principal
Pour un cluster avec plusieurs types de nœuds, vous devez toochoose un d’eux toobe principal. Voici les caractéristiques hello d’un type de nœud principal :

* Hello **taille minimale des machines virtuelles** type de nœud principal hello est déterminé par hello **le niveau de durabilité** vous choisissez. valeur par défaut de Hello pour le niveau de durabilité hello est Bronze. Faites défiler la liste pour plus d’informations sur le niveau de durabilité hello est hello peut prendre les valeurs.  
* Hello **nombre minimal d’ordinateurs virtuels** type de nœud principal hello est déterminé par hello **niveau de fiabilité** vous choisissez. valeur par défaut de Hello pour le niveau de fiabilité hello est argent. Faites défiler la liste pour plus d’informations sur le niveau de fiabilité hello est hello peut prendre les valeurs. 


* les services de système de Service Fabric Hello (par exemple, le service de gestionnaire du Cluster de hello ou le service de banque d’Image) sont placés sur le type de nœud principal hello et c’est le cas hello la fiabilité et de durabilité du cluster de hello est déterminée par hello fiabilité couche valeur et la durabilité de niveau valeur que vous sélectionnez pour le type de nœud principal hello.

![Capture d’écran d’un cluster qui a deux types de nœuds ][SystemServices]

### <a name="non-primary-node-type"></a>Type de nœud non principal
Pour un cluster avec plusieurs types de nœud, il existe un type de nœud principal et rest hello d'entre eux sont non primaire. Voici les caractéristiques hello d’un type de nœud principal :

* Hello de taille minimale des machines virtuelles pour ce type de nœud est déterminée par le niveau de durabilité hello que vous choisissez. valeur par défaut de Hello pour le niveau de durabilité hello est Bronze. Faites défiler la liste pour plus d’informations sur le niveau de durabilité hello est hello peut prendre les valeurs.  
* nombre de Hello minimal d’ordinateurs virtuels pour ce type de nœud peut être un. Toutefois, vous devez choisir ce numéro en fonction du nombre de hello de réplicas de hello/services d’application que vous aimeriez toorun dans ce type de nœud. nombre de Hello d’ordinateurs virtuels dans un type de nœud peut être augmenté après le déploiement de cluster de hello.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>caractéristiques de durabilité Hello du cluster de hello
le niveau de durabilité Hello est utilisé tooindicate toohello système hello des privilèges dont vos machines virtuelles avec l’infrastructure Azure sous-jacente de hello. Dans le type de nœud principal hello, ce privilège permet à Service Fabric toopause toute demande de niveau infrastructure de machine virtuelle (par exemple, un redémarrage de l’ordinateur virtuel, créer une nouvelle image de machine virtuelle ou migration d’ordinateurs virtuels) qui a un impact sur les exigences de quorum hello pour les services de système de hello et vos services avec état. Dans les types de nœud principal hello, ce privilège permet à Service Fabric toopause toutes les demandes de niveau infrastructure de machine virtuelle telles que le redémarrage de l’ordinateur virtuel, créer une nouvelle image de machine virtuelle, etc., migration d’ordinateurs virtuels ayant un impact sur la configuration requise du quorum hello pour vos services avec état en cours d’exécution qu’il contient.

Ce privilège est exprimé en hello valeurs suivantes :

* Gold - infrastructure hello travaux peuvent être suspendues pour une durée de deux heures par UD. La durabilité Gold ne peut être activée que sur les références de machine virtuelle à nœud complet comme D15_V2, G5, etc.
* Silver - hello travaux de l’infrastructure peut être suspendu pour une durée de 10 minutes par UD et est disponible sur tous les ordinateurs virtuels standards de cœur et versions ultérieures.
* Bronze : Aucun privilège. Il s’agit par défaut de hello. Réservez ce niveau de durabilité aux types de nœud qui peuvent exécuter _seulement_ des charges de travail sans état. 

> [!WARNING]
> Les types de nœud s’exécutant avec un niveau de durabilité Bronze n’obtiennent _aucun privilège_. Cela signifie que les travaux d’infrastructure qui affectent vos charges de travail sans état ne seront ni arrêtés ni différés. Il est possible que ces travaux continuent d’affecter vos charges de travail, entraînant ainsi des temps d’arrêt ou d’autres problèmes. Pour tout type de charge de travail de production, il est recommandé d’opter pour une exécution avec au moins le niveau Silver. 
> 

Vous obtenez le niveau de durabilité toochoose pour chacun de vos types de nœud. Vous pouvez choisir un type de nœud toohave un niveau de durabilité or ou silver hello autres ont du Bronze Bonjour même cluster. **Vous devez maintenir un nombre minimum de 5 nœuds pour n’importe quel type de nœud qui a une durabilité d’argent ou or**. 

**Avantages de l’utilisation des niveaux de durabilité Silver ou Gold**
 
1. Réduit le nombre hello des étapes requises dans une opération de mise à l’échelle (autrement dit, la désactivation du nœud et Remove-ServiceFabricNodeState est appelée automatiquement)
2. Réduit les risques de hello de perte de données d’échéance tooa initiée par l’utilisateur sur place VM SKU opération de modification du ou des opérations d’infrastructure Azure.
     
**Inconvénients de l’utilisation des niveaux de durabilité Silver ou Gold**
 
1. Tooyour déploiements ensemble d’échelle de Machine virtuelle et autres ressources Azure associées) peuvent être retardées, peuvent dépasser le délai ou peuvent être bloqués entièrement par des problèmes dans votre cluster ou au niveau d’infrastructure hello. 
2. Augmente hello nombre de [événements de cycle de vie de réplica](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (par exemple, les échanges primaires) en raison de désactivations de nœud tooautomated lors des opérations d’infrastructure Azure.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Recommandations sur les niveaux de la durabilité ou toouse

Durabilité utiliser ou pour tous les types de nœuds que stateful hôte services vous attendent dans tooscale (réduire le nombre d’instances de machine virtuelle) fréquemment, et vous aimeriez que les opérations de déploiement être retardée en faveur de simplification de ces opérations de mise à l’échelle. scénarios de montée en puissance parallèle Hello (l’ajout d’instances de machines virtuelles) ne sont pas lus dans le choix du niveau de durabilité hello, dans l’échelle uniquement.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Recommandations opérationnelles pour le nœud de hello type que vous avez défini la durabilité toosilver ou OR au niveau.

1. Garder votre cluster et les applications à tout moment et vous assurer que les applications répondent tooall [événements de cycle de vie de réplica de Service](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (par exemple, le réplica dans la build est bloqué) en temps voulu.
2. Adopter les plus sûres manières toomake une modification VM SKU (échelle haut/bas) : la modification hello SKU VM d’un ensemble d’échelle de Machine virtuelle est fondamentalement une opération risquée, de sorte que doivent être évitées si possible. Voici le processus de hello vous pouvez suivre tooavoid les problèmes courants.
    - **Pour non primaire nodetypes :** il est recommandé de créer le nouvel ensemble d’échelle de Machine virtuelle, modifiez hello service placement contrainte tooinclude hello échelle de machines virtuelles ensemble/type de nœud et puis réduire hello ancien ensemble d’échelle de Machine virtuelle instance nombre too0, un seul nœud à la fois (il s’agit de toomake assurer que la suppression de nœuds de hello n’affecte pas la fiabilité hello du cluster de hello).
    - **Nodetype principal de hello pour :** notre recommandation est que vous ne modifiez pas VM SKU de type de nœud principal hello. Si hello la raison de nouvelles références SKU hello est la capacité, nous vous recommandons d’ajouter plusieurs instances ou si possible, créez un nouveau cluster. Si vous ne disposez d’aucun choix, vérifiez les modifications toohello tooreflect de définition de modèle de jeu de Machine virtuelle mise à l’échelle hello nouvelle référence (SKU). Si votre cluster n'a qu’un seul nodetype, puis assurez-vous que toutes vos applications avec état répondent tooall [événements de cycle de vie de réplica de Service](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (par exemple, le réplica dans la build est bloqué) dans un délai raisonnable et que le réplica de votre service reconstruire durée est inférieure à cinq minutes (pour le niveau de durabilité argent). 


> [!WARNING]
> Modification hello taille de référence (SKU) de machine virtuelle pour les jeux de mise à l’échelle de machine virtuelle n’exécute ne pas la durabilité Silver au moins n’est pas recommandé. Modifier la taille de référence (SKU) des machines virtuelles est une opération d’infrastructure sur place destructrice de données. Au moins une certaine capacité toodelay ou l’analyse de cette modification, il est possible que l’opération de hello peut entraîner la perte des services avec état ou provoquer d’autres problèmes opérationnels inattendues, même pour les charges de travail sans état. 
> 
    
3. Conservez au minimum cinq nœuds pour tout groupe de machines virtuelles identiques sur lequel MR est activé.
4. Ne supprimez pas d’instances de machine virtuelle aléatoires. Opérez toujours une descente en puissance du groupe de machines virtuelles identiques. la suppression d’instances de machine virtuelle aléatoires Hello a un risque potentiel de la création des déséquilibres dans l’instance de machine virtuelle hello réparties sur UD et FD. Ce déséquilibre peut nuire aux hello systèmes capacité tooproperly équilibrage de la charge entre les réplicas de Service/instances de service hello.
6. Si l’échelle automatique, puis définissez les règles hello telles que l’échelle dans (en supprimant des instances de machine virtuelle) sont effectuées qu’un seul nœud à la fois. La descente en puissance de plusieurs instances en même temps présente des risques.
7. Si la mise à l’échelle vers le bas d’un type de nœud principal, que doit son échelle jamais plus à quel niveau de fiabilité hello autorise bas.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>Hello fiabilité du cluster de hello
Hello niveau de fiabilité sert nombre de hello tooset de réplicas des services de système de hello que vous souhaitez toorun dans ce cluster sur le type de nœud principal hello. Hello plus grand nombre de hello de réplicas, hello plus fiable hello système services se trouvent dans votre cluster.  

niveau de fiabilité Hello peut prendre hello valeurs suivantes :

* Platinum - services de système de hello exécuter avec un réplica cible définie le nombre de 9
* Gold - services de système de hello exécuter avec un nombre de jeu de réplicas cible de 7
* Silver - exécuter des services système hello avec un nombre de jeu de réplicas cible de 5 
* Bronze - services de système de hello exécuter avec un nombre de jeu de réplicas cible 3

> [!NOTE]
> niveau de fiabilité Hello que vous choisissez détermine le nombre minimal de hello de votre type de nœud principal doit avoir des nœuds. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Recommandations pour le niveau de fiabilité hello.

 Lorsque vous augmentez ou réduisez la taille de hello de votre cluster (somme de hello des instances de machine virtuelle dans tous les types de nœud), vous devez mettre à jour de fiabilité hello de votre cluster à partir d’une couche tooanother. Cette opération déclenche hello cluster mises à niveau nécessaires toochange hello système services réplica ensemble count. Attendez la mise à niveau de hello en cours toocomplete avant d’effectuer toutes les autres modifications toohello cluster, telles que l’ajout de nœuds.  Vous pouvez surveiller la progression hello de mise à niveau hello Service Fabric Explorer ou en exécutant [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Voici une recommandation hello sur le choix du niveau de fiabilité hello.

| **Taille du cluster** | **Niveau de fiabilité** |
| --- | --- |
| 1 |Ne spécifiez pas hello du paramètre de niveau de fiabilité, de système de hello calcule |
| 3 |Bronze |
| 5 ou 6|Silver |
| 7 ou 8 |Gold |
| 9 et plus |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>Type de nœud principal - Recommandations en matière de capacité

Voici des conseils de hello pour la planification de capacité de type hello nœud principal

1. **Nombre d’ordinateurs virtuels instances toorun toute charge de travail de production dans Azure :** vous devez spécifier une taille de type de nœud principal minimale de 5. 
2. **Nombre d’ordinateurs virtuels instances les charges de travail de test toorun dans Azure** vous pouvez spécifier une taille de type de nœud principal minimale de 1 ou 3. Hello d’un cluster de nœud, s’exécute avec une configuration spéciale et donc, échelle hors de ce cluster n’est pas prise en charge. Hello un cluster de nœuds, ne dispose d’aucune fiabilité et par conséquent, dans votre modèle de gestionnaire de ressources, des tooremove/non spécifier que la configuration (ne définissez ne pas de valeur de configuration hello n’est pas suffisant). Si vous configurez cluster d’un nœud hello configuré via le portail, puis configuration de hello est automatiquement prise en charge. Les clusters à 1 et 3 nœuds ne sont pas pris en charge pour l’exécution des charges de travail de production. 
3. **VM SKU :** type de nœud principal est l’emplacement d’exécution de services de système de hello, donc hello SKU VM vous choisissez, doive tenir hello compte globale pointe charger vous prévoyez tooplace dans un cluster de hello. Voici une tooillustrate analogie ce que je veux dire ici - pensez de type de nœud principal hello comme votre « poumons », il s’agit de ce que fournit le cerveau de tooyour oxygène et par conséquent, si les cerveau hello n’obtient pas d’assez d’oxygène, le corps de votre subit. 

Étant donné que les besoins en capacité hello d’un cluster est déterminée par la charge de travail vous envisagez de toorun dans un cluster de hello, nous ne pouvons vous fournir des conseils qualitative pour votre charge de travail spécifique, toutefois ici est toohelp de conseils large hello commencer

Pour les charges de travail de production 


- Hello recommandé VM SKU D3 Standard ou D3_V2 Standard ou l’équivalent avec un minimum de 14 Go de disque SSD local.
- utilisation de Hello minimale prise en charge VM SKU est D1 Standard ou D1_V2 Standard ou l’équivalent avec un minimum de 14 Go de disque SSD local. 
- Les références de machine virtuelle à cœur partiel telles que Standard A0 ne sont pas prises en charge pour les charges de travail de production.
- La référence Standard A1 n’est pas prise en charge pour les charges de production pour des raisons de performances.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Type de nœud non principal - Recommandations en matière de capacité pour les charges de travail avec état

Ces instructions sont fournies pour les charges de travail avec état à l’aide de l’infrastructure de Service [collections fiables ou reliable Actors](service-fabric-choose-framework.md) qui vous sont en cours d’exécution dans le type de nœud principal hello.


**Nombre d’instances de machine virtuelle :** pour les charges de travail de production avec état, il est recommandé de les exécuter avec un nombre de réplicas minimal et cible de 5. Cela signifie qu’à l’état stationnaire, vous vous retrouvez avec un réplica (issu d’un jeu de réplicas) dans chaque domaine d’erreur et de mise à niveau. concept de niveau de fiabilité ensemble Hello pour le type de nœud principal hello est un toospecify de façon à ce paramètre pour les services système. Par conséquent, hello même remarque s’applique également les services avec état tooyour.

Par conséquent, pour les charges de production, la taille minimale recommandée non - nœud primaire hello est 5, si vous exécutez les charges de travail avec état qu’elle contient.


**VM SKU :** cela n’est hello nœud type où des services d’application sont en cours d’exécution, donc hello VM SKU vous choisissez, doivent prendre en charge de pointe hello compte vous prévoyez tooplace dans chaque nœud. Bonjour des besoins en capacité de hello nodetype, est déterminée par la charge de travail que vous envisagez de toorun dans un cluster de hello, donc nous ne pouvons pas vous fournir conseils qualitative pour votre charge de travail spécifique, toutefois ici est toohelp de conseils large hello commencer

Pour les charges de travail de production 

- Hello recommandé VM SKU D3 Standard ou D3_V2 Standard ou l’équivalent avec un minimum de 14 Go de disque SSD local.
- utilisation de Hello minimale prise en charge VM SKU est D1 Standard ou D1_V2 Standard ou l’équivalent avec un minimum de 14 Go de disque SSD local. 
- Les références de machine virtuelle à cœur partiel telles que Standard A0 ne sont pas prises en charge pour les charges de travail de production.
- La référence Standard A1 n’est pas non plus prise en charge pour les charges de production pour des raisons de performances.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Type de nœud non principal - Recommandations en matière de capacité pour les charges de travail sans état

Ce guide de charges de travail sans état qui vous sont en cours d’exécution sur hello non primaire nodetype.

**Nombre d’instances de machine virtuelle :** pour les charges de travail qui sont sans état, taille hello minimale prise en charge du type de nœud non principal est 2. Cela vous permet de toorun vous deux instances sans état de votre application et en permettant à votre toosurvive service hello perte d’une instance de la machine virtuelle. 

> [!NOTE]
> Si votre cluster est en cours d’exécution sur le service fabric version est inférieure à 5.6, en raison de défauts tooa Bonjour exécution (ce problème est résolu dans 5.6), mise à l’échelle vers le bas un accessible sans type de nœud principal à 5, entraîne l’activation non intègre, jusqu'à ce que vous appelez l’intégrité du cluster [ Remove-ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) avec le nom de nœud approprié hello. Pour plus d’informations, consultez [Augmenter ou diminuer la taille des instances d’un cluster Service Fabric](service-fabric-cluster-scale-up-down.md).
> 
>

**VM SKU :** cela n’est hello nœud type où des services d’application sont en cours d’exécution, donc hello VM SKU vous choisissez, doivent prendre en charge de pointe hello compte vous prévoyez tooplace dans chaque nœud. Bonjour des besoins en capacité de hello nodetype, est déterminée par la charge de travail que vous envisagez de toorun dans un cluster de hello, donc nous ne pouvons pas vous fournir conseils qualitative pour votre charge de travail spécifique, toutefois ici est toohelp de conseils large hello commencer

Pour les charges de travail de production 


- Hello recommandé VM SKU D3 Standard ou D3_V2 Standard ou équivalent. 
- utilisation de Hello minimale prise en charge VM SKU est D1 Standard ou D1_V2 Standard ou équivalent. 
- Les références de machine virtuelle à cœur partiel telles que Standard A0 ne sont pas prises en charge pour les charges de travail de production.
- La référence Standard A1 n’est pas prise en charge pour les charges de production pour des raisons de performances.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous terminez votre planification de la capacité et que vous configurez un cluster, consultez les informations suivantes hello :

* [Sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md)
* [Présentation du modèle d’intégrité de Service Fabric](service-fabric-health-introduction.md)
* [Relation d’échelle de machines Nodetypes tooVirtual définie](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
