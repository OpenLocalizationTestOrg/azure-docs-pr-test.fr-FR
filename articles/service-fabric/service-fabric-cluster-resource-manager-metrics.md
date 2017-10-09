---
title: "charge de Azure microservice aaaManage à l’aide de mesures | Documents Microsoft"
description: "Découvrez comment tooconfigure et l’utilisation des mesures dans le Service Fabric toomanage la consommation des ressources de service."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Gestion de la consommation des ressources et des charges dans Service Fabric à l’aide de mesures
*Métriques* ressources hello votre attention de services sur et qui sont fourni par les nœuds hello dans un cluster de hello. Une métrique est tout ce que vous souhaitez toomanage commande tooimprove ou l’analyse hello des performances de vos services. Par exemple, vous pourrez surveiller tooknow de consommation de mémoire si votre service est surchargé. Une autre utilisation est toofigure out si le service de hello peut déplacer ailleurs où la mémoire est qu'inférieur contraint ordre tooget améliore les performances.

Il peut s’agir par exemple de l’utilisation de la mémoire, du disque ou du processeur. Ces mesures sont des mesures physiques, les ressources qui correspondent toophysical des ressources sur le nœud hello nécessitant toobe géré. Les mesures peuvent également être (et sont généralement) des mesures logiques. Les mesures logiques sont des éléments tels que « MyWorkQueueDepth », « MessagesToProcess » ou « TotalRecords ». Métriques logiques sont définies par l’application et indirectement correspondent la consommation des ressources physiques toosome. Métriques logiques sont courantes, car il peut être toomeasure dur et la consommation des ressources physiques sur une base par service rapports. complexité Hello de mesure et de rapports de vos propres mesures physique est également pourquoi le Service Fabric fournit certaines mesures par défaut.

## <a name="default-metrics"></a>Mesures par défaut
Supposons que vous souhaitez tooget démarré l’écriture et le déploiement de votre service. À ce stade, vous ne connaissez pas les ressources physiques ou logiques qu’il consomme. Pas de problème ! Hello, Gestionnaire de ressources du Cluster Service Fabric utilise certaines mesures par défaut lorsque aucune autre mesure n’est spécifiés. Il s'agit de :

  - PrimaryCount - nombre de réplicas principaux sur le nœud de hello 
  - ReplicaCount - nombre total de réplicas sur le nœud de hello avec état
  - Count : nombre de tous les objets de service (avec et sans état) sur le nœud de hello

| Mesure | Charge de l’instance sans état | Charge secondaire avec état | Charge principale avec état |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Nombre |1 |1 |1 |

Pour les charges de travail de base, de mesures par défaut hello fournissent une distribution acceptable de travail dans un cluster de hello. Dans l’exemple suivant de hello, voyons que se passe-t-il quand nous créer deux services et reposent sur les mesures par défaut de hello pour équilibrage de charge. Hello premier service est un service avec état avec trois partitions et un réplica de la cible défini de trois. service de deuxième Hello est un service sans état avec une partition et un nombre d’instances de trois.

Voici ce que vous obtenez :

<center>
![Disposition du cluster avec les mesures par défaut][Image1]
</center>

Certains toonote choses :
  - Les réplicas principaux pour un service avec état hello sont réparties entre plusieurs nœuds
  - Réplicas pour hello même partition se trouvent sur différents nœuds
  - Nombre total de Hello des couleurs primaires et secondaires est distribué dans le cluster de hello
  - Nombre total de Hello des objets de service est allouée sur chaque nœud

Bien !

mesures par défaut de Hello fonctionnent très bien en tant qu’un point de départ. Toutefois, de mesures par défaut hello uniquement transitent vous jusqu'à présent. Par exemple : quelle est probabilité hello que hello partitionnement schéma sélectionnées résultats parfaitement même l’utilisation de par toutes les partitions ? Quelle est la probabilité hello hello charge pour un service donné est constante au fil du temps, ou simplement hello identiques sur plusieurs partitions maintenant ?

Vous pouvez exécuter avec juste les mesures par défaut hello. Toutefois, cette approche signifie que l’utilisation de votre cluster est inférieure et plus irrégulière que ce que vous souhaitez. Il s’agit de mesures par défaut hello ne sont pas adaptatives et supposent que tout est équivalent. Par exemple, un serveur principal est occupé et un qui n’est pas les deux contribuent métrique de PrimaryCount toohello « 1 ». Dans le pire des cas hello, à l’aide uniquement de mesures par défaut hello peut également entraîner nœuds overscheduled, ce qui entraîne des problèmes de performances. Si vous êtes intéressé par mise en route hello pleinement parti de votre cluster et comment éviter les problèmes de performances, vous devez toouse des mesures personnalisées et les rapports de la charge dynamique.

## <a name="custom-metrics"></a>Mesures personnalisées
Métriques sont configurés sur une base par-service-instance nommée lorsque vous créez un service de hello.

N’importe quelle mesure présente un certain nombre de propriétés qui la décrivent : un nom, un poids et une charge par défaut.

* : Métrique hello nom de métrique de hello. nom de la métrique Hello est un identificateur unique pour la métrique hello cluster hello du point de vue du Gestionnaire de ressources hello.
* Poids : Poids (métrique) définit l’importance de cette mesure en toohello relatif autres métriques pour ce service.
* Chargement de la valeur par défaut : charge de hello par défaut est représentée différemment selon que le service de hello est sans état ou avec état.
  * Pour les services sans état, chaque mesure présente une propriété unique nommée DefaultLoad.
  * Pour les services avec état, vous devez définir les éléments suivants :
    * PrimaryDefaultLoad : quantité de cette mesure par défaut de hello ce service consomme lorsqu’il est un serveur principal
    * SecondaryDefaultLoad : délai par défaut hello cette mesure de que ce service utilise lorsqu’il s’agit d’une base de données secondaire

> [!NOTE]
> Si vous définissez des mesures personnalisées et souhaitez too_also_ utiliser les mesures par défaut hello, vous devez too_explicitly_ ajouter de mesures par défaut hello sauvegarder et définissent le poids et des valeurs pour ces. Il s’agit, car vous devez définir la relation hello entre de mesures par défaut hello et des mesures personnalisées. Peut-être accordez-vous plus d’importance au paramètre ConnectionCount ou WorkQueueDepth qu’à la distribution principale. Par poids par défaut hello hello PrimaryCount métrique est élevée, ce qui fait que vous tooreduce il tooMedium lorsque vous ajoutez vos autres tooensure métriques qu’ils sont prioritaires.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Exemple de définition de mesures pour votre service
Supposons que vous souhaitez hello configuration suivante :

  - Votre service signale une mesure nommée « ConnectionCount »
  - Vous souhaitez également que les mesures de toouse hello par défaut 
  - Vous avez effectué des mesures et savez que normalement un réplica principal de ce service utilise jusqu’à 20 unités de la mesure « ConnectionCount »
  - Les réplicas secondaires utilisent 5 unités de la mesure « ConnectionCount »
  - Vous savez que « ConnectionCount » est hello décisif en termes de gestion des performances hello de ce service particulier
  - Mais vous souhaitez néanmoins que les réplicas principaux soient équilibrés. L’équilibrage des réplicas principaux est généralement une bonne solution. Cela permet d’éviter la perte de hello d’un domaine de nœud ou une erreur d’affecter une majorité des réplicas principaux en même temps. 
  - Dans le cas contraire, conviennent de mesures par défaut hello

Voici le code hello que vous écririez toocreate un service avec cette configuration de la métrique :

Code :

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Hello exemples ci-dessus et hello reste de ce document décrivent les mesures de gestion sur une base par nommé-service. Il est également possible toodefine les métriques pour vos services au niveau de service de hello _type_ niveau. Cette opération s’effectue en les spécifiant dans vos manifestes de service. La définition des mesures au niveau du type n’est pas recommandée pour plusieurs raisons. Hello première parce que les noms de métrique sont souvent spécifiques à l’environnement. Sauf s’il existe un contrat entreprise en place, il se peut que vous ne peut pas être sûr de que cette métrique hello « Cœurs » dans un environnement n’est pas « MiliCores » ou « Cœurs » dans d’autres. Si vos métriques sont définis dans votre manifeste, vous devez toocreate nouveaux manifestes par l’environnement. Cela entraîne généralement prolifération tooa de manifestes différents avec que des différences mineures, ce qui peuvent provoquer des difficultés de toomanagement.  
>
> Les charges de mesure sont couramment attribuées pour chaque service nommé. Par exemple, supposons que vous créez une instance de hello entretenir pour ClientA envisage de toouse que peu. Supposons également que vous créez une autre instance de service pour un Client B disposant d’une plus grande charge de travail. Dans ce cas, il vous faudrait par défaut de hello tootweak charge pour ces services. Si vous avez des métriques et charges définies via les manifestes et que vous souhaitez toosupport ce scénario, il requiert l’autre application et les types de service pour chaque client. les valeurs Hello définies au moment de la création du service remplacent ceux définis dans le manifeste de hello, vous pouvez donc utilisez tooset hello spécifique utilisé par défaut par. Toutefois, ce qui entraîne une valeurs hello déclarés dans la correspondance de toonot hello manifestes avec que ces service hello s’exécute. Cela peut entraîner des tooconfusion. 
>

En guise de rappel : Si vous souhaitez simplement des mesures de toouse hello par défaut, vous ne la collecte de métriques tootouch hello du tout besoin ou effectuer d’action particulière lorsque vous créez votre service. mesures par défaut de Hello obtient automatiquement utilisées lorsque aucun autre ne sont définies. 

À présent, passons en revue chacun de ces paramètres plus en détail et discutez de comportement de hello son influence sur.

## <a name="load"></a>charger
Hello point ensemble de mesures est toorepresent une charge. Une *charge* correspond à la quantité d’une mesure spécifique qui est consommée par une instance ou un réplica de service sur un nœud donné. La charge peut être configurée en presque n’importe quel point. Par exemple :

  - La charge peut être définie lors de la création d’un service. Il s’agit d’une _charge par défaut_.
  - Hello métrique, y compris la valeur par défaut chargées, pour un service peut mis à jour une fois que le service de hello est créé. Il s’agit de la _mise à jour d’un service_. 
  - charges Hello pour une partition donnée peuvent être réinitialisation toohello les valeurs par défaut pour ce service. Il s’agit de la _réinitialisation d’une charge de partition_.
  - La charge peut être dynamiquement signalée pour chaque objet de service lors de l’exécution. Il s’agit du _signalement d’une charge_. 
  
Ces stratégies peuvent être utilisés au sein de hello même pendant sa durée de vie du service. 

## <a name="default-load"></a>Charge par défaut
*Par défaut charge* est la quantité de mesure hello consomme de chaque objet de service (instance sans état ou réplica avec état) de ce service. Hello Gestionnaire de ressources de Cluster utilise ce numéro pour la charge de l’objet de service hello hello jusqu'à ce qu’il reçoit d’autres informations, tels qu’un rapport de charge dynamique. Pour les services plus simples, charge de hello par défaut est une définition statique. charge de Hello par défaut n’est jamais mis à jour et est utilisé pour la durée de vie hello du service de hello. Par défaut charge fonctionne très bien pour les scénarios où certaines quantités de ressources sont des charges de travail dédié toodifferent et ne changent pas de planification simple.

> [!NOTE]
> Pour plus d’informations sur la gestion de la capacité et en définissant des capacités pour les nœuds hello dans votre cluster, consultez [cet article](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Hello Gestionnaire de ressources du Cluster permet aux services avec état toospecify une charge par défaut différent de couleurs primaires et secondaires. Services sans état peuvent spécifier uniquement une valeur qui applique des instances de tooall. Pour les services avec état, chargement par défaut de hello pour les réplicas principal et secondaire sont généralement différentes dans la mesure où les réplicas effectuer différents types de travail dans chaque rôle. Par exemple, indistinctement généralement traiter les lectures et écritures et gérer la plupart des charges de calcul hello, tandis que les bases de données secondaires ne sont pas. Charge par défaut de hello pour un réplica principal est généralement supérieure à la charge de valeur par défaut hello pour les réplicas secondaires. nombres réels de Hello doit dépendre de vos propres mesures.

## <a name="dynamic-load"></a>Charge dynamique
Supposons que vous exécutiez votre service depuis un certain temps. En procédant à certaines analyses, vous avez observé que :

1. Certaines partitions ou instances d’un service donné consomment plus de ressources que d’autres.
2. La charge de certains services varie au fil du temps.

De nombreux facteurs peuvent causer ces types de fluctuations de charge. Par exemple, différents services ou partitions sont associés à différents clients présentant différentes exigences. Charge peut également changer, car hello du service hello de travail varie dans le cours hello du jour de hello. Quelle que soit la raison de hello, il n’est généralement aucun numéro unique que vous pouvez utiliser pour la valeur par défaut. Cela est particulièrement vrai si vous souhaitez que tooget hello pour la plupart des taux d’utilisation en dehors du cluster de hello. N’importe quelle valeur choisie pour la charge de la valeur par défaut est incorrecte des temps de hello. Par défaut incorrecte charge résultat Bonjour Gestionnaire de ressources de Cluster sur ou sous l’allocation de ressources. Par conséquent, vous disposez de nœuds qui sont au-dessus ou au-dessous d’utilisé même si hello Gestionnaire de ressources de Cluster considère comme cluster de hello est équilibrée. Les charges par défaut sont toujours adaptées car elles fournissent certaines informations pour le placement initial, mais elles n’offrent pas un tableau complet des charges de travail réelles. capture tooaccurately la modification des besoins en ressources, hello Gestionnaire de ressources du Cluster permet de son propre charge chaque tooupdate d’objet de service pendant l’exécution. On parle de « rapports de charge dynamique ».

Les rapports de charge dynamique permettent tooadjust réplicas ou les instances de leur charge a signalé l’allocation/de métriques pendant leur durée de vie. Des réplicas ou des instances de service inactifs signalent généralement qu’ils utilisent une faible quantité d’une mesure spécifique. Des réplicas ou des instances de service actifs signalent quant à eux qu’ils en utilisent une quantité plus importante.

Charge par le réplica ou l’instance de Reporting permet hello tooreorganize du Gestionnaire de ressources de Cluster des objets de service individuels hello hello cluster. La réorganisation des services de hello permet de s’assurer qu’ils d’obtenir les ressources hello que dont ils ont besoin. Services occupés efficacement obtient trop « libérer » les ressources d’autres réplicas ou les instances qui sont actuellement à froid ou du moins de travail.

Dans les Services fiables, hello code tooreport charge dynamiquement l’aspect suivant :

Code :

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Un service peut signaler sur une des métriques hello définie au moment de la création. Si une charge de rapports de service pour une mesure qui n’est pas configuré toouse, Service Fabric ignore ce rapport. S’il existe d’autres métriques signalées à hello même temps qui sont valides, ces rapports sont acceptées. Code de service peut mesurer et signaler toutes hello métriques il sait comment, et les opérateurs peuvent spécifier toouse de configuration de la métrique hello sans avoir de code de service toochange hello. 

### <a name="updating-a-services-metric-configuration"></a>Mise à jour de la configuration des mesures d’un service
la liste des métriques Hello associée avec le service de hello et propriétés hello de ces mesures peuvent être modifiées dynamiquement tandis que hello service live. Cela permet une meilleure expérimentation et plus de flexibilité. Voici quelques exemples :

  - désactivation d’une mesure avec un état incorrect pour un service particulier
  - reconfiguration des poids de hello des métriques en fonction du comportement souhaité
  - l’activation d’une mesure une fois hello code a déjà été déployé et validé via d’autres mécanismes
  - la modification d’une charge par défaut hello pour un service basé sur la consommation et le comportement observé

Hello API principale pour la modification de configuration de la métrique sont `FabricClient.ServiceManagementClient.UpdateServiceAsync` en c# et `Update-ServiceFabricService` dans PowerShell. Les informations que vous spécifiez avec ces API remplacent les informations existantes métrique hello pour le service de hello immédiatement. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Mélange des valeurs de charge par défaut et des rapports de charge dynamique
Chargement de la valeur par défaut et des charges dynamiques peuvent servir pour hello même service. Lorsqu’un service utilise à la fois une charge par défaut et des rapports de charge dynamique, la charge par défaut sert d’estimation jusqu’à ce que les rapports dynamiques arrivent. Chargement de la valeur par défaut est correct, car il donne hello Gestionnaire de ressources du Cluster quelque chose toowork avec. charge de Hello par défaut permet aux hello tooplace du Gestionnaire de ressources du Cluster hello service objets dans des emplacements bon lorsqu’ils sont créés. Si aucune information n’est fournie pour la charge par défaut, le positionnement des services est aléatoire. Lorsque les rapports de charge arrivent ultérieurement la sélection élective aléatoire hello initiale est souvent le problème et hello Gestionnaire de ressources du Cluster a toomove services.

Reprenons l’exemple précédent et voyons ce qui se passe lorsque nous ajoutons des mesures personnalisées et les rapports de charge dynamique. Dans cet exemple, nous utilisons « MemoryInMb » comme exemple de mesure.

> [!NOTE]
> La mémoire est une des métriques du système hello Service Fabric peut [ressource régissent](service-fabric-resource-governance.md), et il est généralement difficile de reporting vous-même. Nous ne prévoyez réellement vous tooreport sur la consommation de mémoire ; La mémoire est utilisée ici comme un toolearning d’aide sur les fonctionnalités de hello Hello Gestionnaire de ressources du Cluster.
>

Supposons que nous avons créé un service avec état hello initialement avec hello de commande suivante :

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Pour rappel, la syntaxe utilisée est ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

Voyons quelle pourrait être une disposition de cluster possible :

<center>
![Cluster équilibré avec les mesures par défaut et des mesures personnalisées][Image2]
</center>

Informations importantes à noter :

* Les réplicas secondaires dans une partition peuvent avoir chacun leur propre charge
* Ensemble des métriques de hello rechercher à charge équilibrée. Pour la mémoire, hello rapport entre hello maximale et minimale de la charge est de 1,75 (nœud de hello avec hello charge la plupart des N3, hello est moins N2 et 28/16 = 1,75).

Il existe certaines choses que nous devons encore tooexplain :

* Quel élément a permis de déterminer qu’un rapport de 1,75 était raisonnable ou non ? Comment hello Gestionnaire de ressources du Cluster de savoir si c’est assez perfectionné ou s’il existe plusieurs toodo de travail ?
* À quel moment l’équilibrage se produit-il ?
* Qu’est-ce que cela signifie que Memory (mémoire) était pondérée comme étant « High » (haute) ?

## <a name="metric-weights"></a>Poids des mesures
Suivi hello même métriques sur différents services est important. Que la vue globale est ce que permet de hello consommation tootrack de gestionnaire de ressources de Cluster dans un cluster de hello, équilibrer la consommation des nœuds et assurez-vous que les nœuds ne dépasser la capacité. Toutefois, les services peuvent avoir différentes vues comme importance toohello Hello même mesure. Par ailleurs, dans un cluster qui présente un grand nombre de mesures et de services, il se peut qu’il n’existe pas de solution parfaitement équilibrée pour toutes les mesures. Comment hello Gestionnaire de ressources du Cluster doit gérer ces situations ?

Poids métriques autoriser hello toodecide du Gestionnaire de ressources de Cluster comment toobalance hello cluster lorsqu’il n’existe aucune solution idéale. Poids métriques permettent également de hello toobalance du Gestionnaire de ressources de Cluster des services spécifiques différemment. Les mesures peuvent avoir quatre niveaux de poids : Zero, Low, Medium et High (zéro, faible, moyen et haut). Une mesure avec un poids de Zero n’entre aucunement en compte dans la décision d’équilibrage des éléments. Toutefois, sa charge contribue toujours toocapacity management. Les mesures avec un poids nul sont toujours utiles et sont fréquemment utilisées dans le cadre de l’analyse des performances et du comportement d’un service. [Cet article](service-fabric-diagnostics-event-generation-infra.md) fournit plus d’informations sur l’utilisation de hello des métriques de surveillance et de diagnostics de vos services. 

impact réel de Hello de poids de métriques différents dans le cluster de hello est que ce gestionnaire de ressources du Cluster hello génère les différentes solutions. Poids de métriques indiquent hello Gestionnaire de ressources de Cluster que certaines métriques sont plus importants que d’autres. Lorsqu’il n’existe aucun hello solution idéale Gestionnaire de ressources de Cluster peuvent préférer solutions équilibrer hello supérieur pondérée métriques mieux. Si un service considère qu’une mesure particulière n’est pas importante, il peut trouver que l’utilisation de cette mesure cause un déséquilibre. Cela permet à un autre service tooget une distribution uniforme de certains métrique est tooit important.

Examinons un exemple de certains rapports charge et une métrique de quelle manière les différentes pondère les résultats dans les différentes affectations de cluster de hello. Dans cet exemple, nous constatons que passage d’une pondération relative de hello des métriques de hello provoque hello toocreate du Gestionnaire de ressources de Cluster des dispositions différentes des services.

<center>
Exemple de poids de mesures et impact sur les solutions d’équilibrage![][Image3]
</center>

Dans cet exemple, nous avons quatre services différents qui signalent tous des valeurs différentes pour deux mesures, MetricA et MetricB. Dans certains cas, tous les services hello définissent MetricA hello n’est plus importante (poids = élevé) et MetricB comme sans importance (poids = faible). Par conséquent, nous constatons que hello du Gestionnaire de ressources de Cluster place les services hello afin que MetricA est mieux que MetricB équilibrage de charge. « Mieux équilibrée » signifie que la mesure MetricA présente un écart type plus faible que celui de la mesure MetricB. Dans les cas de deuxième hello, nous inverser les poids métrique hello. Par conséquent, hello Gestionnaire du Cluster de ressource échange services A et B toocome avec une allocation MetricB étant mieux à charge équilibrée à MetricA.

> [!NOTE]
> Poids métriques déterminent comment doit équilibrer hello Gestionnaire de ressources du Cluster, mais pas lorsque l’équilibrage doit se produire. Pour plus d’informations sur l’équilibrage, consultez [cet article](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Poids globaux des mesures
Supposons que les services définit MetricA comme poids élevé et ServiceB définit le poids hello pour MetricA tooLow ou zéro. Quel est le poids réel hello qui finit par en cours d’utilisation ?

Plusieurs poids sont suivis pour chaque mesure. épaisseur du premier Hello est hello celui défini pour la métrique de hello lorsque hello service est créé. Bonjour autres poids est un poids global, qui est calculé automatiquement. Hello Gestionnaire du Cluster de ressource utilise les deux ces poids lors de l’évaluation des solutions. Il est important de tenir compte de ces deux poids. Cela permet à hello toobalance du Gestionnaire de ressources de Cluster de chaque service tooits conséquente possèdent des priorités et également vous assurer que le cluster hello dans son ensemble est alloué correctement.

Que se passerait-il si hello Gestionnaire de ressources de Cluster n’a pas d’intérêt solde global et local ? C’est facile tooconstruct solutions qui sont équilibrées de manière globale, mais ce qui entraîne l’équilibre des ressources faibles pour des services individuels. Bonjour l’exemple suivant, nous allons examiner un service configuré avec uniquement les mesures par défaut hello et consultez que se passe-t-il lorsque seul le solde global est considérée comme :

<center>
![Hello Impact d’une Solution globale uniquement][Image4]
</center>

Dans hello supérieur exemple basé uniquement sur le solde global, cluster hello dans son ensemble est en effet équilibré. Tous les nœuds ont hello même nombre de couleurs primaires et hello même nombre total de réplicas. Toutefois, si vous examinez l’impact réel de hello de cette allocation il n’est pas tellement bien : perte hello de n’importe quel nœud a un impact sur une charge de travail particulier disproportionnellement, car il accepte toutes ses couleurs primaires. Par exemple, si le premier nœud de hello échoue trois couleurs primaires de hello pour hello trois différentes partitions de hello service du cercle tous seraient perdues. À l’inverse, hello Triangle et des services de hexagone ont leurs partitions perdre un réplica. Ainsi, sans interruption, autre qu’ayant hello toorecover réplica vers le bas.

Dans l’exemple hello du bas, hello Gestionnaire de ressources du Cluster a distribué réplicas hello basées sur les deux solde de hello global et par service. Lors du calcul de score hello de solution de hello elle constitue la majeure partie de la solution globale de hello poids toohello et services tooindividual partie (configurable). Solde global pour une mesure est calculée en fonction en moyenne hello de poids de métrique hello à partir de chaque service. Chaque service est équilibré tooits de poids métrique conséquente propre défini. Cela garantit que les services de hello sont équilibrées entre eux en fonction des besoins propres tootheir. Par conséquent, en cas de hello même nœud de premier échec de hello est réparti sur toutes les partitions de tous les services. Hello impact tooeach est hello identiques.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md) (service-fabric-cluster-resource-manager-configure-services.md).
- Défragmentation des mesures sont charge tooconsolidate monodirectionnelle sur les nœuds au lieu de la propagation de. toolearn comment tooconfigure défragmentation, reportez-vous à la section trop[cet article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)
- Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- Le coût du mouvement constitue une méthode de signalisation toohello Gestionnaire de ressources de Cluster que certains services sont toomove plus coûteuse que d’autres. toolearn en savoir plus sur le coût du mouvement, consultez trop[cet article](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
