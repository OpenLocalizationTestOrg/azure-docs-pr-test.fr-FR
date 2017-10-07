---
title: aaaScalability de services de Fabric du Service | Documents Microsoft
description: "Décrit comment les services Service Fabric tooscale"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Mise à l’échelle dans Service Fabric
Azure Service Fabric rend toobuild facilement des applications évolutives grâce à la gestion des services de hello, partitions et réplicas sur les nœuds hello d’un cluster. Exécute de nombreuses charges de travail sur hello même l’utilisation du matériel active maximale de ressources, mais fournit également une flexibilité en termes de la façon dont vous choisissez tooscale vos charges de travail. 

Dans Service Fabric, la mise à l’échelle s’effectue de plusieurs manières :

1. En créant ou en supprimant des instances de services sans état
2. En créant ou en supprimant de nouveaux services nommés
3. En créant ou en supprimant de nouvelles instances d’application nommées
4. En utilisant des services partitionnés
5. Mise à l’échelle en ajoutant et supprimant des nœuds de cluster de hello 
6. En utilisant des métriques Cluster Resource Manager

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>En créant ou en supprimant des instances de services sans état
Un des hello tooscale de façons la plus simple au sein de l’infrastructure de Service fonctionne avec les services sans état. Lorsque vous créez un service sans état, vous obtenez une chance toodefine un `InstanceCount`. `InstanceCount`définit le nombre de copies en cours d’exécution de code de ce service est créé lorsque le démarrage du service hello. Supposons par exemple, qu’il n’y a 100 nœuds dans un cluster de hello. Supposons également qu’un service soit créé avec un `InstanceCount` défini sur 10. Pendant l’exécution, ces 10 copies en cours d’exécution de code de hello pu tous être trop occupés (ou peut-être pas suffisamment occupés). Une façon tooscale cette charge de travail est le nombre de hello toochange d’instances. Par exemple, une partie du code de suivi ou de gestion peut modifier hello existant différentes instances too50 ou too5, selon si la charge de travail hello doit tooscale in ou out hello en fonction de chargement. 

C# :

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell :

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Utilisation du nombre d’instances dynamiques
Spécifiquement pour les services sans état, l’infrastructure de Service offre un nombre d’instances de façon automatique toochange hello. Cela permet de tooscale de service hello dynamiquement avec le nombre de hello de nœuds qui sont disponibles. tooopt de façon Hello dans ce comportement est le nombre d’instances hello tooset = -1. InstanceCount = -1 est une instruction de tooService Fabric indiquant que « Exécuter ce service sans état sur chaque nœud. » Si nombre hello de nœuds change, Service Fabric change automatiquement hello instance nombre toomatch, garantissant que le service de hello s’exécute sur tous les nœuds valides. 

C# :

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>En créant ou en supprimant de nouveaux services nommés
Une instance de service nommé est une instance spécifique d’un type de service (voir [cycle de vie d’application Service Fabric](service-fabric-application-lifecycle.md)) au sein d’une instance de l’application nommée dans un cluster de hello. 

De nouvelles instances de services nommées peuvent être créées (ou supprimées) si les services sont trop ou trop peu occupés. Cela permet de toobe demandes réparties sur plusieurs instances de service, généralement ce qui charge sur toodecrease de services existant. Lorsque vous créez des services, hello Gestionnaire de ressources du Cluster Service Fabric place les services hello cluster hello en mode distribué. les décisions exacte Hello sont régies par hello [métriques](service-fabric-cluster-resource-manager-metrics.md) dans un cluster de hello et d’autres règles de sélection élective. Les services peuvent être créés de différentes façons, mais hello plus courantes sont soit par le biais des actions administratives comme toute autre personne [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), ou par le code appelant [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`peut même être appelée à partir d’autres services qui s’exécutent dans un cluster de hello.

La création dynamique de services peut être utilisée dans toutes sortes de scénarios et constitue un modèle commun. Prenons par exemple un service avec état représentant un workflow particulier. Appels de travail sont appelés tooshow toothis service, et ce service est continu tooexecute hello étapes toothat flux de travail et d’enregistrement de cours. 

Comment pouvez-vous rendre cette échelle de service particulier ? Hello service peut être plusieurs locataires dans une forme et accepte les appels et déclencher étapes de nombreuses instances différentes de hello même flux de travail à la fois. Toutefois, qui peut rendre le hello code plus complexe, car il a tooworry sur nombreuses instances différentes de hello même flux de travail, en différentes étapes et de différents clients. En outre, la gestion de plusieurs flux de travail à hello ne résout pas simultanément hello problème de mise à l’échelle. Il s’agit, car à un moment donné, ce service consommera trop toofit de ressources sur un ordinateur particulier. De nombreux services ne pas été créés pour ce modèle dans le premier emplacement dans hello également des difficultés en raison de goulot d’étranglement inhérente de toosome ou de ralentissement dans leur code. Ces types de problèmes empêcher le service de hello toowork pas également lorsque nombre hello de workflows simultanés qu’il effectue le suivi d’Obtient la plus grande.  

Une solution est toocreate une instance de ce service pour chaque autre instance de flux de travail hello souhaité tootrack. Ceci est un excellent modèle et fonctionne si le service hello est sans état ou avec état. Pour ce modèle toowork, il est généralement un autre service qui agit comme un « Service de gestionnaire de charge de travail ». tâche Hello de ce service sont tooreceive demandes et tooroute ces services tooother de demandes. Gestionnaire de Hello peut créer dynamiquement une instance du service de charge de travail hello lorsqu’il reçoit le message de type hello et ensuite passer sur les services toothose de demandes. le service manager Hello peut également recevoir des rappels lorsqu’un service de workflow donné a terminé son travail. Lorsque le Gestionnaire de hello reçoit ces rappels il pourrait supprimer cette instance du service de workflow hello ou laissez-le si d’autres appels sont attendus. 

Versions avancées de ce type de gestionnaire peuvent même créer des pools de services hello qu’il gère. pool de Hello garantit que lorsqu’une nouvelle demande arrive qu’il n’a pas toowait pour hello service toospin. Au lieu de cela, le gestionnaire hello peut simplement en choisir un service de flux de travail qui n’est pas actuellement occupé à partir du pool de hello ou acheminer de manière aléatoire. En conservant un pool de services disponibles accélère la gestion des nouvelles demandes, car il est moins probable que demande hello a toowait pour une nouvelle toobe de service lancé. La création de services est rapide, mais elle n’est ni gratuite ni instantanée. pool de Hello permet de réduire la durée hello demande de hello a toowait avant d’en cours de maintenance. Vous verrez souvent ce modèle de gestionnaire et le pool lorsque le temps de réponse intéressent hello. Demande de hello files d’attente et de création de service hello en arrière-plan de hello et _puis_ en lui passant est également un modèle de gestionnaire populaires, création et suppression des services en fonction de certains suivi de quantité hello de travail que le service actuellement est en attente. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>En créant ou en supprimant de nouvelles instances d’application nommées
Création et suppression d’instances de l’ensemble de l’application sont un modèle toohello semblable de la création et la suppression des services. Pour ce modèle, il existe certains service manager qui est prise de décision hello en fonction des demandes de hello il voit et informations hello il reçoit de hello autres services à l’intérieur du cluster de hello. 

Dans quels cas faut-il créer une instance d’application nommée au lieu de créer des instances de services nommées dans une application existante ? Voici quelques cas :

  * nouvelle instance d’application Hello est pour un client dont le code doit toorun sous une identité particulière ou les paramètres de sécurité.
    * Service Fabric permet de définir toorun de packages de code différents sous des identités particuliers. Dans l’ordre toolaunch hello même package de code sous des identités différentes, les activations hello devez toooccur dans les instances de l’autre application. Prenons le cas où vous avez déployé des charges de travail d’un client existant. Ceux-ci peuvent s’exécuter sous une identité particulière afin de pouvoir analyser et contrôler leurs tooother accéder aux ressources, telles que les bases de données ou d’autres systèmes. Dans ce cas, lorsqu’un nouveau client s’inscrit, probablement non désirés tooactivate leur code Bonjour même contexte (espace de processus). Pendant que vous le pouvez, cela rend plus difficile pour votre tooact de code de service dans le contexte de hello d’une identité particulière. Vous devez généralement disposer de plus de sécurité, d’isolation et de code de gestion d’identité. Au lieu d’utiliser différents nommé service instances dans hello la même instance d’application et par conséquent hello même espace de processus, vous pouvez utiliser différentes instances d’Application Service Fabric nommées. Il est ainsi plus faciles contextes d’identité toodefine.
  * nouvelle instance d’application Hello sert également un moyen de configuration
    * Par défaut, tous hello nommé d’un type de service particulier dans une instance d’application, les instances de service seront exécute dans le même processus sur un nœud donné de hello. Cela signifie que, même si vous pouvez configurer chaque instance de service différemment, cela se révèlera complexe. Services doivent avoir un jeton qu’ils utilisent toolook de leur configuration dans un package de configuration. Cela est généralement simplement les nom du service hello. Cela fonctionne correctement, mais il associe les noms de toohello configuration hello hello individuels nommée d’instances de service dans cette instance de l’application. Cela peut prêter à confusion et toomanage dur depuis la configuration est normalement un artefact au moment du design avec les valeurs spécifiques d’instance application. Création de services plus toujours signifie plus mises à niveau de l’application toochange hello les informations dans les packages de configuration hello ou toodeploy nouveaux afin que les nouveaux services de hello vous peuvent rechercher des informations spécifiques. Il est souvent plus facile toocreate une toute nouvelle instance d’application nommée. Puis vous pouvez utiliser tooset de paramètres d’application hello quelle que soit la configuration est nécessaire pour les services de hello. Ainsi que tous les services de hello qui sont créés dans ce nommé instance d’application peut hériter des paramètres de configuration particulier. Par exemple, au lieu d’avoir un seul fichier de configuration avec les paramètres de hello et de personnalisations pour tous les clients, telles que les clés secrètes ou par les limites de ressources client, vous au lieu de cela aurait une instance d’application différent pour chaque client avec ces paramètres substitution. 
  * nouvelle application de Hello sert d’une limite de mise à niveau
    * Dans Service Fabric, plusieurs instances d’application nommées servent de limites pour la mise à niveau. Une mise à niveau d’une instance de l’application nommée n’affectera pas de code hello une autre instance de l’application nommée est en cours d’exécution. Hello différentes applications se retrouvent exécutant des versions différentes du même code de hello sur hello mêmes nœuds. Cela peut être un facteur lorsque vous devez toomake une décision de mise à l’échelle, car vous pouvez choisir que si le nouveau code de hello doit suivre hello même met à niveau qu’un autre service ou non. Par exemple, qu’un appel arrive au niveau de service manager hello qui est responsable de la mise à l’échelle de charges de travail d’un client spécifique en créant et en suppression des services de manière dynamique. Dans ce cas toutefois, l’appel de hello est pour une charge de travail associé à un _nouveau_ client. La plupart des clients comme en étant isolées les unes des autres non seulement pour des raisons de sécurité et de configuration hello répertoriées précédemment, mais, car elle offre plus de souplesse en termes d’exécutant des versions spécifiques du logiciel de hello en choisissant quand ils mis à niveau. Vous pouvez également créer une nouvelle instance de l’application et créer le service de hello il simplement toofurther partition hello montant de vos services qui impliquent l’une mise à niveau. La séparation des instances d’application permet une plus grande granularité lors des mises à niveau d’application, et permet également d’effectuer des test A/B et des déploiements Blue/Green. 
  * instance d’application existante Hello est plein
    * Dans l’infrastructure de Service, [capacité de l’application](service-fabric-cluster-resource-manager-application-groups.md) est un concept que vous pouvez utiliser la quantité de hello toocontrol de ressources disponibles pour les instances d’application particulière. Par exemple, vous pouvez décider qu’un service donné doit toohave une autre instance créée dans l’ordre tooscale. Toutefois, cette instance d’application n’a plus de capacité pour une certaine métrique. Si cette charge de travail ou un client spécifique doit toujours être accordé davantage de ressources, puis vous pouvez augmenter la capacité existante de hello pour cette application ou créer une application. 

## <a name="scaling-at-hello-partition-level"></a>Mise à l’échelle au niveau de partition hello
Service Fabric prend en charge le partitionnement. Le partitionnement divise un service en plusieurs sections logiques et physiques, indépendantes les unes des autres. Cela est utile pour les services avec état, car aucun jeu de réplicas a toohandle tous les appels hello et ensemble de hello état manipuler en même temps. Hello [vue d’ensemble de partitionnement](service-fabric-concepts-partitioning.md) fournit des informations sur les types hello de schémas de partitionnement qui sont pris en charge. réplicas de Hello de chaque partition sont répartis entre les nœuds hello dans un cluster, la distribution de charge du service et de s’assurer qu’aucun service hello dans son ensemble ou n’importe quelle partition a un point de défaillance unique. 

Imaginez un service qui utilise un schéma de partitionnement par plage avec une clé basse de 0, une clé haute de 99 et 4 partitions. Dans un cluster de trois nœuds, service de hello peut-être être présenté avec quatre réplicas qui partagent des ressources hello sur chaque nœud, comme illustré ici :

<center>
![Disposition de partition avec trois nœuds](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Si vous augmentez le nombre de hello de nœuds, l’infrastructure de Service parmi les réplicas existants hello déplacer il. Par exemple, supposons que nombre hello de nœuds augmente toofour et les réplicas hello obtient redistribuées. Service de hello a maintenant trois réplicas sont en cours d’exécution sur chaque nœud, chacune appartenant toodifferent partitions. Cela permet une meilleure utilisation des ressources, car le nouveau nœud de hello n’est pas à froid. En règle générale, améliore les performances car chaque service a plusieurs tooit de ressources disponibles.

<center>
![Disposition de partition avec quatre nœuds](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Mise à l’échelle à l’aide de hello Gestionnaire de ressources du Cluster Service Fabric et métriques
[Mesures](service-fabric-cluster-resource-manager-metrics.md) sont comment services express leur tooService de consommation des ressources Fabric. Utilisation des mesures donne hello Gestionnaire de ressources du Cluster une tooreorganize opportunité et optimiser la disposition hello du cluster de hello. Par exemple, il peut y avoir suffisamment de ressources de cluster de hello, mais ils ne peuvent pas être alloués toohello les services qui sont actuellement du travail. À l’aide de mesures hello tooreorganize du Gestionnaire de ressources du Cluster permet de hello tooensure de cluster que les services ont accès toohello des ressources disponibles. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Mise à l’échelle en ajoutant et supprimant des nœuds de cluster de hello 
Une autre option de mise à l’échelle avec Service Fabric est taille de hello toochange du cluster de hello. Modification de la taille de hello du cluster de hello signifie l’ajout ou la suppression de nœuds pour un ou plusieurs des types de nœuds hello dans un cluster de hello. Par exemple, considérez un cas dans lequel tous les nœuds hello dans un cluster de hello sont à chaud. Cela signifie que les ressources du cluster hello sont presque tous consommée. Dans ce cas, cluster Ajout de plusieurs nœuds toohello est hello meilleure manière tooscale. Une fois que les nouveaux nœuds de hello joindre hello de cluster hello Gestionnaire de ressources du Cluster Service Fabric déplace toothem de services, ce qui entraîne une charge inférieure totale sur les nœuds existants hello. Pour les services sans état avec « instance count = -1 », des instances de service supplémentaires sont créées automatiquement. Ainsi, certains toomove d’appels de hello nœuds toohello nouvelle les nœuds existants. 

Ajout et suppression de nœuds toohello cluster peut être effectuée via module PowerShell de gestionnaire de ressources Azure Service Fabric de hello.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Exemple complet
Nous allons prendre toutes les idées hello que nous avez présentées ici et communiquer avec un exemple. Envisagez de hello après service : vous essayez de toobuild un service qui agit comme un carnet d’adresses, contenant les informations de contact et de toonames. 

À droite au préalable, vous avez un certain nombre de questions des tooscale connexes : le nombre d’utilisateurs est toohave de cours vous ? Combien de contacts chaque utilisateur va-t-il stocker ? Tentez toofigure toutes les lorsque vous sont permanent votre service pour hello première est difficile. Supposons que vous alliez toogo avec un seul service statique avec un nombre de partitions spécifiques. conséquences Hello de prélèvement hello incorrect le nombre de partitions peut entraîner les problèmes de mise à l’échelle toohave plus tard. De même, même si vous sélectionnez le nombre de droite hello qu'est peut-être pas toutes les informations de hello vous avez besoin. Par exemple, vous sont également toodecide en taille hello du cluster hello, à la fois en termes de nombre hello de nœuds et leur taille. Toopredict dur généralement son nombre de ressources un service est en cours tooconsume pendant sa durée de vie. Il peut également être tooknow dur avance le modèle de trafic hello heure que le service de hello voit réellement. Par exemple, peut-être personnes et supprimer leurs contacts uniquement première chose que matin de hello, ou peut-être qu’il est distribué uniformément cours hello du jour de hello. En fonction de cela que vous devrez peut-être tooscale et dans dynamiquement. Vous trouverez peut-être toopredict lorsque vous souhaitez tooneed tooscale et dans, mais dans les deux cas que vous allez probablement la consommation des ressources tooneed tooreact toochanging par votre service. Cela peut impliquer la modification de taille hello du cluster hello dans l’ordre tooprovide davantage de ressources lors de la réorganisation d’utilisation des ressources existantes ne suffit pas. 

Mais pourquoi même toopick un schéma de partition unique out pour tous les utilisateurs ? Pourquoi vous limiter tooone service et un seul cluster statique ? situation réelle de Hello est généralement plus dynamique. 

Lors de la génération de l’échelle, envisagez de hello modèle dynamique. Vous devrez peut-être tooadapt il tooyour situation :

1. Au lieu de tenter toopick un schéma de partitionnement pour tout le monde au préalable, générez un « service manager ».
2. tâche Hello du service du gestionnaire hello est toolook au niveau des informations sur les clients quand ils se connectent à votre service. Ensuite, en fonction de ces informations, le service manager hello créer une instance de votre _réel_ service de stockage de contact _juste pour que le client_. Si elles nécessitent une configuration particulière, l’isolation ou mises à niveau, vous pouvez également décider toospin d’une instance d’Application pour ce client. 

Ce modèle de création dynamique présente de nombreux avantages :

  - Vous n’essayez pas de nombre de partition correct tooguess hello pour tous les utilisateurs au préalable ou créez un service unique qui est très évolutif à lui seul. 
  - Différents utilisateurs n’ont pas hello toohave même partition nombre, nombre de réplica, les contraintes de placement, métriques, les charges par défaut, les noms de service, les paramètres dns ou l’un des hello autres propriétés spécifiées au niveau de service de hello ou niveau de l’application. 
  - Vous bénéficiez d’une segmentation des données supplémentaire. Chaque client possède sa propre copie du service de hello
    - Chaque service client peut être configuré différemment et avoir accès à plus ou moins de ressources, avec plus ou moins de partitions ou de réplicas, en fonction de l’échelle attendue.
      - Par exemple, hello client a payé hello niveau « Gold » - qu’ils puissent accéder plus réplicas ou nombre de partitions supérieur, et éventuellement les ressources dédiées services tootheir via les capacités de métriques et d’application.
      - Ou prétendent fourni des informations indiquant le nombre hello de contacts qu’ils nécessaire a été « Petite » : ils obtiendriez uniquement certaines partitions, ou peut même être intégrées à un pool de service partagé avec d’autres clients.
  - Vous n’exécutez pas un ensemble de réplicas ou les instances de service pendant que vous patientez pour tooshow clients des
  - Si un client quitte, puis en supprimant leurs informations de votre service est aussi simple que Gestionnaire de hello de supprimer ce service ou cette application qu’il a créées.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les concepts de l’infrastructure de Service, consultez hello suivant des articles :

* [Disponibilité des services Service Fabric](service-fabric-availability-services.md)
* [Partitionnement des services Service Fabric](service-fabric-concepts-partitioning.md)
