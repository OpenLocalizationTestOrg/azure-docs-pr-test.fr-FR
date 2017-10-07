---
title: "aaaHealth analyse dans l’infrastructure de Service | Documents Microsoft"
description: "Un présentation toohello Azure Service Fabric d’analyse du fonctionnement modèle, ce qui permet la surveillance de cluster de hello et ses services et applications."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Surveillance de l’intégrité de l’ensemble fibre optique tooService introduction
Azure Service Fabric introduit un modèle d’intégrité qui fournit une évaluation et des rapports d’intégrité riches, flexibles et extensibles. modèle de Hello permet la proximité en temps réel d’analyse d’état hello hello cluster d’et services hello en cours d’exécution qu’il contient. Vous pouvez facilement obtenir les informations de contrôle d’intégrité et corriger les problèmes potentiels avant qu’ils ne s’enchaînent et ne provoquent des pannes massives. Dans le modèle de type hello, services envoient des rapports en fonction de leur point de vue local et que les informations sont agrégées tooprovide une vue globale au niveau du cluster.

Les composants de service Fabric utilisent cette tooreport de modèle d’intégrité riche leur état actuel. Vous pouvez utiliser hello même mécanisme tooreport l’intégrité de vos applications. Si vous investissez dans une fonction de création de rapports sur l’intégrité de qualité élevée, qui capture vos conditions personnalisées, vous pouvez plus facilement détecter et corriger les problèmes liés aux applications en cours d’exécution.

Hello que suivant Microsoft Virtual Academy vidéo décrit également le modèle de contrôle d’intégrité de Service Fabric hello et comment il est utilisé :<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Nous avons commencé hello intégrité sous-système tooaddress nécessaire pour les mises à niveau analysées. Service Fabric fournit analysés application cluster mises à niveau et qui ne vérifient la disponibilité totale, aucun temps d’arrêt et l’intervention de l’utilisateur toono minimale. tooachieve ces objectifs, la mise à niveau hello vérifie l’intégrité sur configuré des stratégies de mise à niveau. La mise à niveau ne peut être effectuée que si l’intégrité respecte les seuils désirés. Dans le cas contraire, mise à niveau hello est soit automatiquement restaurée ou suspendu toogive administrateurs un problèmes de hello toofix chance. toolearn en savoir plus sur les mises à niveau de l’application, consultez [cet article](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Magasin d’intégrité
le magasin de contrôle d’intégrité Hello conserve relatifs à l’état des informations sur les entités dans le cluster hello pour faciliter leur récupération et d’évaluation. Il est implémenté comme une infrastructure de Service rendues persistantes avec état service tooensure haute disponibilité et extensibilité. magasin de contrôle d’intégrité Hello fait partie de hello **fabric : / système** application et il est disponible lorsque le cluster de hello est disponible et en cours d’exécution.

## <a name="health-entities-and-hierarchy"></a>Entités d'intégrité et hiérarchie
les entités d’intégrité Hello sont organisées dans une hiérarchie logique qui capture les interactions et les dépendances entre les différentes entités. magasin de contrôle d’intégrité Hello génère automatiquement les entités d’intégrité et hiérarchie basée sur les rapports reçus à partir des composants de Service Fabric.

les entités d’intégrité Hello reflètent des entités de Service Fabric hello. (Par exemple, **entité d’intégrité d’application** correspond à une instance d’application déployée dans un cluster de hello, tandis que **entité de nœud de contrôle d’intégrité** correspond à un nœud de cluster Service Fabric.) capture de la hiérarchie de contrôle d’intégrité hello Hello des interactions entre les entités système hello et il sert de hello pour l’évaluation d’intégrité avancées. Vous pouvez découvrir les concepts clés de Service Fabric dans l’article [Présentation technique de Service Fabric](service-fabric-technical-overview.md). Pour plus d’informations sur l’application, consultez [Modèle d’application Service Fabric](service-fabric-application-model.md).

hiérarchie et entités de contrôle d’intégrité hello autorisent hello cluster et les applications toobe efficacement signalée, le débogage et analysées. modèle de contrôle d’intégrité Hello fournit précis, *granulaires* la représentation sous forme de santé hello hello plusieurs fragments mobiles dans le cluster de hello.

![Entités d’intégrité.][1]
entités de contrôle d’intégrité Hello, organisées dans une hiérarchie basée sur les relations parent-enfant.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

les entités d’intégrité Hello sont :

* **Cluster**. Représente un contrôle d’intégrité hello d’un cluster Service Fabric. Rapports d’intégrité de cluster décrivent les conditions qui affectent l’ensemble du cluster hello. Ces conditions affecter plusieurs entités dans le cluster de hello ou hello lui-même. En fonction de la condition de hello, rapporteur de hello ne peuvent pas restreindre l’étendue problème hello tooone ou plus d’enfants non intègres. Exemples cerveau hello du cluster hello fractionnement en raison de problèmes de communication ou de partitionnement toonetwork.
* **Nœud**. Représente un contrôle d’intégrité hello d’un nœud de l’infrastructure de Service. Rapports d’intégrité de nœud décrivent les conditions qui affectent la fonctionnalité de nœud hello. En règle générale, ils affectent toutes les entités hello déployé sont en cours d’exécution sur ce dernier. Exemples : le nœud manque d’espace disque (ou d’une autre propriété au niveau de l’ordinateur comme la mémoire, les connexions, etc.) ou le nœud est inactif. entité de nœud Hello est identifiée par le nom de nœud hello (chaîne).
* **Application**. Représente un contrôle d’intégrité hello d’une instance de l’application en cours d’exécution dans un cluster de hello. Rapports d’intégrité de l’application décrivent les conditions qui affectent hello l’intégrité globale de l’application hello. Ils ne peuvent pas être affinés enfants tooindividual (services ou applications déployées). Exemples : hello bout en bout d’interaction entre différents services dans application hello. entité d’application Hello est identifiée par le nom de l’application hello (URI).
* **Service**. Représente un contrôle d’intégrité hello d’un service en cours d’exécution dans un cluster de hello. Intégrité du service de rapports décrivent les conditions qui affectent hello intégrité globale du service de hello. reporter de Hello ne peut pas réduire hello problème tooan défectueux partition ou un réplica. Exemple : une configuration de service (par exemple, le partage de fichiers externes ou de ports) à l’origine de problèmes pour toutes les partitions. entité de service Hello est identifiée par le nom du service hello (URI).
* **Partition**. Représente un contrôle d’intégrité hello d’une partition de service. Rapports d’intégrité de partition décrivent les conditions qui affectent le jeu de réplicas de hello. Exemples : lorsque nombre hello de réplicas est inférieur à nombre de cibles et lorsqu’une partition est une perte de quorum. Hello partition est identifiée par ID (GUID) de la partition hello.
* **Réplica**. Représente un contrôle d’intégrité hello d’un réplica de service avec état ou d’une instance de service sans état. réplica de Hello est hello plus petite unité de composants du système et les agents de surveillance peuvent établir des rapports pour une application. Pour les services avec état, des exemples un réplica primaire qui ne peut pas répliquer les opérations toosecondaries et réplication lente. Une instance sans état peut également signaler qu’elle manque de ressources ou présente des problèmes de connectivité. Hello réplica est identifiée par hello ID (GUID) et hello replica ou instance ID de partition (longue).
* **DeployedApplication**. Représente hello d’intégrité d’un *application en cours d’exécution sur un nœud*. Rapports de contrôle d’intégrité d’application déployée décrivent application toohello spécifique de conditions sur le nœud hello qui ne peut pas être affiné tooservice les packages déployés sur hello même nœud. Exemples incluent des erreurs lorsque le package d’application ne peut pas être téléchargé sur le nœud et problèmes de configuration d’entités de sécurité d’application sur le nœud de hello. application Hello déployé est identifiée par le nom de l’application (URI) et le nom de nœud (chaîne).
* **Package de service déployé**. Représente un contrôle d’intégrité hello d’un package de service en cours d’exécution sur un nœud de cluster de hello. Il décrit les conditions spécifiques tooa service package qui n’affectent pas hello autres packages de service sur hello même nœud pour hello même application. Un package de code des exemples dans le package de service hello ne peut pas être démarré et un package de configuration qui ne peut pas être lu. package de service Hello déployé est identifié par le nom de l’application (URI), le nom de nœud (chaîne), nom de manifeste de service (chaîne) et ID de l’activation de package de service (chaîne).

granularité Hello du modèle de contrôle d’intégrité hello rend facile toodetect et corriger les problèmes. Par exemple, si un service ne répond pas, il est possible tooreport qui hello instance d’application n’est pas sain. Création de rapports à que niveau n’est pas idéal, toutefois, étant donné que le problème de hello pas susceptibles d’affecter tous les services de hello dans cette application. rapport de Hello doit être appliqué toohello défectueux partition de service ou tooa enfants spécifiques, si plus d’informations pointe toothat partition. les données de salutation automatiquement des surfaces via la hiérarchie de hello et une partition non intègre sont rendues visibles aux niveaux de service et de l’applications. Cette agrégation permet de toopinpoint et résoudre plus rapidement les causes hello du problème de hello.

hiérarchie de contrôle d’intégrité Hello est constitué de relations parent-enfant. Un cluster est composé de nœuds et d’applications. Les applications contiennent des services et des applications déployées. Les applications déployées ont elles-mêmes déployé des packages de service. Les services contiennent des partitions, et chaque partition possède un ou plusieurs réplicas. Il existe une relation spéciale entre les nœuds et les entités déployées. Un nœud défectueux comme indiqué par son composant système autorité, hello Failover Manager service affecte les applications hello déployé, les packages de service et les réplicas déployés sur celui-ci.

hiérarchie de contrôle d’intégrité Hello représente l’état le plus récent hello du système hello basé sur les rapports d’intégrité de la dernière hello, qui est informations presque en temps réel.
Agents de surveillance internes et externes peuvent établir des rapports hello mêmes entités selon une logique spécifique à l’application ou des conditions personnalisées analysées. Rapports sur les utilisateurs coexistent avec les rapports du système hello.

Plan tooinvest dans la méthode de création d’un service cloud volumineux toohealth tooreport et répondre au cours de hello. Cette approuvent fasse rend toodebug plus facile de service hello, surveiller et fonctionner.

## <a name="health-states"></a>États d'intégrité
L’infrastructure de service utilise trois toodescribe d’états d’intégrité si une entité est saine ou non : OK, avertissement et erreur. N’importe quel rapport envoyé le magasin de contrôle d’intégrité toohello doit spécifier un de ces États. résultat de l’évaluation d’intégrité Hello est un de ces États.

Hello possible [les États d’intégrité](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) sont :

* **OK**. entité de Hello est saine. Aucun problème connu n'est signalé sur elle ou ses enfants (le cas échéant).
* **Warning**. entité de Hello présente certains problèmes, mais il continuent de fonctionner correctement. Par exemple, elle connaît des retards, mais ceux-ci n’empêchent pas encore son bon fonctionnement. Dans certains cas, condition d’avertissement hello peut résoudre lui-même sans intervention externe. Dans ce cas, les rapports d’intégrité vous informent de l’avertissement et expliquent ce qui se passe. Dans d’autres cas, la condition d’avertissement hello peut dégrader rencontré un problème grave sans intervention de l’utilisateur.
* **Error**. entité de Hello n’est pas sain. Doit prendre des mesures état de hello toofix d’entité de hello, car il ne peut pas fonctionner correctement.
* **Unknown**. entité de Hello n’existe pas dans le magasin de contrôle d’intégrité hello. Ce résultat peut être obtenu à partir de requêtes distribuée de hello fusionner les résultats de plusieurs composants. Par exemple, requête de liste du nœud hello get devient trop**basculement**, **ClusterManager**, et **HealthManager**; obtenir l’application de requête de liste est trop **ClusterManager** et **HealthManager**. Cette fusion de requêtes est le résultat de plusieurs composants système. Si un autre composant système retourne une entité qui n’est pas présente dans le magasin de contrôle d’intégrité, hello la fusion des résultats sont inconnu l’état d’intégrité. Une entité n’est pas dans le magasin, car les rapports d’intégrité n’ont pas encore été traités ou l’entité de hello a été nettoyée après la suppression.

## <a name="health-policies"></a>Stratégies d'intégrité
magasin de contrôle d’intégrité Hello s’applique toodetermine des stratégies de contrôle d’intégrité si une entité est saine en fonction de ses rapports et ses enfants.

> [!NOTE]
> Stratégies d’intégrité peuvent être spécifiés dans le manifeste du cluster hello (pour l’évaluation d’intégrité de cluster et le nœud) ou dans le manifeste de l’application hello (pour l’évaluation de l’application et un de ses enfants). Les demandes d’évaluation d’intégrité peuvent également transmettre des stratégies d’évaluation d’intégrité personnalisées, utilisées uniquement pour cette évaluation.
> 
> 

Par défaut, le Service Fabric applique des règles strictes (tous les éléments doivent être sains) pour la relation hiérarchique de hello parent-enfant. Si au moins un des enfants de hello possède un événement non intègre, parent de hello est considéré comme non intègre.

### <a name="cluster-health-policy"></a>Stratégie d’intégrité de cluster
Hello [stratégie d’intégrité de cluster](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) est utilisé tooevaluate l’intégrité du cluster hello les États d’intégrité état et de nœud. Hello peut être définie dans le manifeste du cluster hello. Si elle n’est pas présente, la stratégie par défaut de hello (zéro tolérées pannes) est utilisé.
stratégie de contrôle d’intégrité du cluster Hello contient :

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Spécifie si le contrôle d’intégrité de tootreat avertissement signale comme des erreurs lors de l’évaluation d’intégrité. Valeur par défaut : false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Spécifie le pourcentage autorisé maximal de hello des applications qui peuvent être non intègres avant de cluster de hello est considéré comme erreur.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Spécifie le pourcentage autorisé maximal de hello de nœuds qui peuvent être non intègres avant de cluster de hello est considéré comme erreur. Dans les clusters de grande taille, certains nœuds sont toujours bas ou out pour la réparation, par conséquent, ce pourcentage doit être configuré tootolerate qui.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). mappage de stratégie d’intégrité Hello application type peut être utilisé pendant types d’application spéciale toodescribe cluster état d’évaluation. Par défaut, toutes les applications sont placées dans un pool et évaluées avec MaxPercentUnhealthyApplications. Si certains types d’application doivent être traitées différemment, ils peuvent être extraite de pool global de hello. Au lieu de cela, elles sont évaluées par rapport aux pourcentages hello associés à leur nom de type d’application dans le mappage de hello. Par exemple, un cluster contient des milliers d’applications de types différents et plusieurs instances d’application de contrôle d’un type d’application particulier. applications de contrôle Hello ne doivent jamais être dans l’erreur. Vous pouvez spécifier global MaxPercentUnhealthyApplications too20 % tootolerate certains échecs, mais pour hello type d’application « ControlApplicationType » la valeur hello MaxPercentUnhealthyApplications too0. Ainsi, si certains hello de nombreuses applications sont défectueuses, mais sous hello global non intègre de pourcentage, le cluster de hello doit donc être évaluées tooWarning. Un état d’avertissement pour l’intégrité n’affecte pas la mise à niveau du cluster, ni les autres analyse déclenchées par l’état Error (erreur). Mais l’application contrôle même une erreur rendrait cluster défectueux, ce qui déclenche la restauration ou suspend la mise à niveau du cluster hello, selon la configuration de mise à niveau hello.
  Pour les types d’application hello définies dans le mappage de hello, toutes les instances d’application sont retirées de pool global de hello d’applications. Ils sont évalués en fonction du nombre total de hello d’applications hello du type d’application, à l’aide de hello sont mappés MaxPercentUnhealthyApplications spécifiques à partir de hello. Tous les autres hello applications de hello restent dans le pool global de hello et sont évaluées avec MaxPercentUnhealthyApplications.

Bonjour à l’exemple suivant est un extrait d’un manifeste de cluster. toodefine les entrées de mappage de type hello application, nom du paramètre hello préfixe avec « ApplicationTypeMaxPercentUnhealthyApplications- », suivi par le nom de type d’application hello.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Stratégie d’intégrité d’application
Hello [stratégie de contrôle d’intégrité des applications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) décrit la procédure d’évaluation hello d’agrégation d’événements et les États d’enfants pour les applications et leurs enfants. Elle peut être définie dans le manifeste de l’application hello **ApplicationManifest.xml**, dans le package d’application hello. Si aucune stratégie n’est spécifié, Service Fabric part du principe que l’entité de hello est non intègre si elle a un état d’intégrité ou un enfant à l’état d’intégrité d’avertissement ou erreur hello.
les règles configurables Hello sont :

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Spécifie si le contrôle d’intégrité de tootreat avertissement signale comme des erreurs lors de l’évaluation d’intégrité. Valeur par défaut : false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Spécifie le pourcentage hello maximale tolérée des applications déployées qui peuvent être non intègres avant de l’application hello est considéré comme erreur. Ce pourcentage est calculé en divisant le nombre de hello des applications déployées défectueuses sur nombre hello de nœuds hello applications sont actuellement déployées sur dans le cluster de hello. calcul de Hello arrondit tootolerate une défaillance sur un petit nombre de nœuds. Pourcentage par défaut : zéro.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Spécifie les hello par défaut service type stratégie d’intégrité, qui remplace la stratégie de contrôle d’intégrité hello par défaut pour tous les types de service dans l’application hello.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Fournit une liste de stratégies d’intégrité de service par type de service. Ces stratégies remplacent les stratégies de contrôle d’intégrité de type hello par défaut service pour chaque type de service spécifié. Par exemple, si une application a un type de service sans état passerelle et un type de service de moteur avec état, vous pouvez configurer les stratégies de contrôle d’intégrité hello pour leur évaluation différemment. Lorsque vous spécifiez la stratégie par le type de service, vous pouvez obtenir un contrôle plus précis de la santé du service de hello hello.

### <a name="service-type-health-policy"></a>Stratégie d’intégrité de type de service
Hello [service stratégie de contrôle d’intégrité de type](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) Spécifie le mode tooevaluate et agrégat hello services et hello enfants de services. stratégie de Hello contient :

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Spécifie le pourcentage de hello maximale tolérée de partitions non intègres avant un service est considéré comme non intègre. Pourcentage par défaut : zéro.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Spécifie le pourcentage hello maximale tolérée de réplicas non intègres avant une partition est considéré comme non intègre. Pourcentage par défaut : zéro.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Spécifie le pourcentage hello maximale tolérée de services non intègres avant de l’application hello est considéré comme non intègre. Pourcentage par défaut : zéro.

Bonjour à l’exemple suivant est un extrait d’un manifeste d’application :

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Évaluation de l'intégrité
Les utilisateurs et les services automatisés peuvent évaluer l’intégrité de toutes les entités à tout moment. tooevaluate contrôle d’intégrité d’une entité, les agrégats de magasin de contrôle d’intégrité hello l’intégrité de tous les rapports sur l’entité de hello et évalue tous ses enfants (le cas échéant). algorithme d’agrégation de contrôle d’intégrité Hello utilise des stratégies de contrôle d’intégrité qui spécifient comment les rapports de contrôle d’intégrité tooevaluate et comment le contrôle d’intégrité de tooaggregate enfant États (le cas échéant).

### <a name="health-report-aggregation"></a>Agrégation de rapports d’intégrité
Une entité peut avoir plusieurs rapports d'intégrité envoyés par différents rapporteurs (composants système ou agents de surveillance) sur différentes propriétés. Hello d’agrégation utilise hello des stratégies d’intégrité associés, en particulier hello ConsiderWarningAsError les membres de l’application ou stratégie de contrôle d’intégrité de cluster. ConsiderWarningAsError spécifie comment les avertissements tooevaluate.

état d’intégrité agrégé Hello est déclenchée par hello *pire* rapports de contrôle d’intégrité sur l’entité de hello. S’il existe des rapports de contrôle d’intégrité d’au moins une erreur, hello état d’intégrité agrégé est une erreur.

![Agrégation de rapports d’intégrité avec un état Error.][2]

Une entité d’intégrité qui inclut un ou plusieurs rapports d’intégrité en erreur est considérée comme à l’état Error. Hello même a la valeur true pour un état d’intégrité expirée, quel que soit son état d’intégrité.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

S’il y a aucun rapport d’erreurs et d’un ou plusieurs avertissements, hello état d’intégrité agrégé est Avertissement ou erreur, en fonction de l’indicateur de stratégie ConsiderWarningAsError hello.

![Agrégation de rapports d’intégrité avec un état Warning et une valeur ConsiderWarningAsError égale à false.][3]

L’agrégation de rapport d’intégrité avec l’état d’avertissement et ConsiderWarningAsError définie toofalse (par défaut).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Agrégation d’intégrité des enfants
Hello état d’intégrité agrégé d’une entité reflète les États d’intégrité de hello enfant (le cas échéant). algorithme de Hello pour agréger les États d’intégrité enfant utilise hello stratégies d’intégrité applicables selon le type d’entité hello.

![Agrégation d’intégrité des entités enfants.][4]

Agrégation d’enfants basée sur les stratégies d’intégrité.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Une fois que le magasin de contrôle d’intégrité hello a évalué tous les enfants de hello, elle agrège leurs États d’intégrité basées sur un pourcentage maximal de hello configuré des enfants non intègres. Ce pourcentage est extraite de la stratégie hello selon le type d’entité et enfant hello.

* Si tous les enfants ont des États OK, état d’intégrité agrégé des enfants hello est OK.
* Si les enfants ont OK et états d’avertissement, état d’intégrité agrégé des enfants hello est un avertissement.
* S’il existe des enfants avec les États d’erreur qui ne respectent pas le pourcentage d’enfants non intègres nombre maximum hello, hello état d’intégrité agrégé est une erreur.
* Si les enfants hello avec erreur États égard hello maximale autorisée du pourcentage d’enfants non intègres, hello est en état d’intégrité agrégé avertissement.

## <a name="health-reporting"></a>Rapports d'intégrité
Les composants système, les applications System Fabric et les agents de surveillance internes/externes peuvent établir des rapports sur les entités Service Fabric. rapporteurs de Hello rendre *local* analyses d’intégrité hello d’entités hello analysé, en fonction des conditions de hello sont surveillés. Toolook à n’importe quel état global ou des données d’agrégation n’est nécessaire. Hello souhaité comportement est rapporteurs simple de toohave et organismes pas complexes qui doivent toolook à nombreuses choses tooinfer le toosend plus d’informations.

toosend d’intégrité toohello d’intégrité magasin de données un rapporteur a besoin d’entité de hello affectée tooidentify et créer un rapport d’intégrité. rapport de hello toosend, utilisez hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, le signalement d’intégrité API exposé sur hello `Partition` ou `CodePackageActivationContext` objets, des applets de commande PowerShell ou REST.

### <a name="health-reports"></a>Rapports d'intégrité
Hello [rapports d’intégrité](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) pour chacune des entités hello dans un cluster de hello contenir hello informations suivantes :

* **SourceId**. Chaîne qui identifie de façon unique reporter hello d’événement de contrôle d’intégrité hello.
* **Entity identifier**. Identifie l’entité hello où les rapports hello sont appliquée. Il diffère selon le hello [type d’entité](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Cluster. Aucune.
  * Nœud. Nom du nœud (chaîne).
  * console. Nom de l’application (URI). Représente le nom hello d’instance d’application hello déployé dans un cluster de hello.
  * Service. Nom du service (URI). Représente le nom hello hello des instances de service déployé dans un cluster de hello.
  * Partition. ID de la partition (GUID). Représente l’identificateur unique de partition hello.
  * Réplica. ID de réplica de service avec état Hello ou ID d’instance de service sans état hello (INT64).
  * DeployedApplication. Nom de l’application (URI) et nom du nœud (chaîne).
  * DeployedServicePackage. Nom de l’application (URI), nom du nœud (chaîne) et nom du manifeste de service (chaîne).
* **Property**. A *chaîne* (pas une énumération fixe) qui permet de reporter des hello d’intégrité de hello toocategorize événement pour une propriété spécifique de l’entité de hello. Par exemple, reporter A peut signaler Santé hello de propriété de « Stockage » hello Node01 et reporter B peut signaler Santé hello de propriété « Connectivité » de hello Node01. Dans le magasin de contrôle d’intégrité hello, ces rapports sont traités en tant qu’événements d’intégrité distinct pour hello Node01 entité.
* **Description**. Une chaîne qui autorise un tooprovide reporter des informations détaillées sur événement d’état hello. **SourceId**, **propriété**, et **HealthState** doit décrire complètement les rapports hello. description de Hello ajoute des informations explicites sur les rapports de hello. texte Hello rend plus facile pour les administrateurs et les utilisateurs du rapport de contrôle d’intégrité toounderstand hello.
* **HealthState**. Un [énumération](service-fabric-health-introduction.md#health-states) qui décrit l’état d’intégrité hello du rapport de hello. Hello valeurs acceptées sont OK, avertissement et erreur.
* **TimeToLive**. Valeur de type timespan qui indique la durée pendant laquelle rapport d’intégrité de hello est valide. Couplée avec **RemoveWhenExpired**, il informe la banque de contrôle d’intégrité hello comment tooevaluate expiré des événements. Par défaut, valeur de hello est infinie, et les rapports hello sont toujours valide.
* **RemoveWhenExpired**. Valeur booléenne. Si défini tootrue, hello d’intégrité expirée rapport est automatiquement supprimé du magasin de contrôle d’intégrité hello et rapport de hello n’affecte l’évaluation de l’intégrité d’entité. Utilisé lorsque le rapport de hello est valide pour une période de temps uniquement et hello reporter ne devez tooexplicitly désactivez-la. Il a également utilisé toodelete des rapports à partir du magasin de contrôle d’intégrité hello (par exemple, une surveillance est modifié et cesse d’envoyer des rapports avec source précédente et la propriété). Il peut envoyer un rapport avec une brève TimeToLive avec RemoveWhenExpired tooclear d’un état antérieur à partir du magasin de contrôle d’intégrité hello. Si hello a la valeur toofalse, hello expirées de rapport est traité comme une erreur lors de l’évaluation d’intégrité hello. la valeur false Hello signale au magasin de contrôle d’intégrité toohello que cette source de hello doit signaler périodiquement sur cette propriété. Si ce n’est pas le cas, puis il doit exister un problème au niveau de surveillance de hello. contrôle d’intégrité de surveillance Hello est capturé en tenant compte des événements hello en tant qu’erreur.
* **SequenceNumber**. Entier positif qui doit toobe en constante augmentation, il représente l’ordre de hello des rapports de hello. Il est utilisé par hello rapports d’intégrité magasin toodetect obsolètes qui arrivent en retard en raison des délais réseau ou d’autres problèmes. Un rapport est rejeté si le numéro de séquence hello est inférieur ou égal nombre toohello dernièrement appliquée pour hello même entité, source et propriété. S’il n’est pas spécifié, le numéro de séquence hello est généré automatiquement. Il est nécessaire tooput dans le numéro de séquence hello uniquement lors de la création de rapports sur les transitions d’état. Dans ce cas, hello source doit également tooremember quels rapports il envoyé et conserver les informations de hello pour la récupération lors du basculement.

Les informations SourceId, entity identifier, Property et HealthState sont requises pour tous les rapports d’intégrité. Hello SourceId chaîne n’est pas autorisée toostart avec le préfixe de hello »**système.**», qui est réservé pour les rapports du système. Pourquoi même entité, il existe un seul rapport pour hello même source et propriété. Plusieurs rapports pour hello même source et de substitution de propriété, côté hello d’intégrité client (si elles sont traitées par lot) ou sur le côté de magasin de contrôle d’intégrité hello. remplacement de Hello est basé sur les numéros de séquence ; des rapports plus récents (avec des numéros de séquence plus élevés) remplacent des rapports plus anciens.

### <a name="health-events"></a>Événements d'intégrité
En interne, le magasin de contrôle d’intégrité hello conserve [événements d’intégrité](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), qui contiennent toutes les informations hello hello rapports et des métadonnées supplémentaires. Hello métadonnées incluent des temps de hello rapport de hello a été attribué le client de contrôle d’intégrité toohello et l’heure de hello qu'il a été modifié sur le côté du serveur hello. événements de contrôle d’intégrité Hello sont retournés par [requêtes d’intégrité](service-fabric-view-entities-aggregated-health.md#health-queries).

Hello métadonnées ajouté contient :

* **SourceUtcTimestamp**. Hello temps hello, rapport a été attribué le client de contrôle d’intégrité toohello (temps universel).
* **LastModifiedUtcTimestamp**. dernière modification du rapport de hello Hello temps côté serveur de hello (temps universel).
* **IsExpired**. Un indicateur tooindicate si le rapport de hello a expiré lors de la requête de hello a été exécutée par le magasin de contrôle d’intégrité hello. Un événement peut avoir expiré uniquement si RemoveWhenExpired a la valeur false. Sinon, les événements hello ne sont pas retournée par la requête et sont supprimé du magasin de hello.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. heure de la dernière pour les transitions OK/avertissement/erreur de Hello. Ces champs fournissent un historique hello hello d’intégrité des transitions d’état pour les événements hello.

champs de transition d’état Hello peuvent servir pour les alertes plus intelligents ou des informations sur les événements de contrôle d’intégrité « historique ». Ils permettent les scénarios suivants :

* Alerte quand une propriété a eu la valeur Error/Warning pendant plus de X minutes. La vérification de la condition de hello pour une période de temps évite les alertes sur les conditions temporaires. Par exemple, une alerte si l’état d’intégrité hello a été un avertissement pendant plus de cinq minutes permettre être traduite (HealthState == avertissement et LastWarningTransitionTime maintenant - > 5 minutes).
* Alerte uniquement sur les conditions qui ont été modifiés dans hello dernière X minutes. Si un rapport a été déjà au niveau de l’erreur avant hello spécifié de fois, il peut être ignoré, car il était déjà signalé précédemment.
* Si une propriété oscille entre Warning et Error, détermine la durée pendant laquelle elle a été défectueuse (donc pas à l’état OK). Par exemple, une alerte si la propriété de hello n’a pas été intègre pendant plus de cinq minutes permettre être traduite (HealthState ! = Ok et maintenant - LastOkTransitionTime > 5 minutes).

## <a name="example-report-and-evaluate-application-health"></a>Exemple : évaluer et établir un rapport sur l’intégrité de l’application
Hello exemple suivant envoie un rapport d’intégrité via PowerShell application hello **fabric : / WordCount** à partir de la source de hello **MyWatchdog**. rapport d’intégrité de Hello contient des informations sur la propriété de contrôle d’intégrité hello « disponibilité » dans un état d’intégrité d’erreur avec la propriété TimeToLive infinie. Ensuite, elle interroge l’intégrité d’application hello, qui retourne agrégé des erreurs de l’état d’intégrité et hello a signalé des événements de contrôle d’intégrité dans la liste hello des événements d’état.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Utilisation du modèle d'intégrité
modèle de contrôle d’intégrité Hello permet de services de cloud computing et tooscale de plateforme Service Fabric sous-jacent hello, étant donné que les décisions de surveillance et de contrôle d’intégrité sont réparties entre plusieurs écrans de hello au sein du cluster de hello.
Autres systèmes ont un service unique et centralisé au niveau de cluster hello qui analyse tous les hello *potentiellement* émises par les services des informations utiles. Cette approche empêche leur évolutivité. Il également n’autorise pas les informations spécifiques de toocollect toohelp permet d’identifier les problèmes et les problèmes potentiels comme cause première toohello fermer que possible.

modèle de contrôle d’intégrité Hello est utilisée pour la surveillance et de diagnostic, pour l’évaluation d’intégrité de cluster et des applications et mises à niveau analysées. Autres services d’état tooperform données automatique répare générer l’historique de contrôle d’intégrité de cluster et émettre des alertes sous certaines conditions.

## <a name="next-steps"></a>Étapes suivantes
[Affichage rapports d’intégrité de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Utilisation des rapports d’intégrité système pour la résolution des problèmes](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Comment tooreport et vérification du service d’intégrité](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Ajout de rapports d’intégrité Service Fabric personnalisés](service-fabric-report-health.md)

[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)

