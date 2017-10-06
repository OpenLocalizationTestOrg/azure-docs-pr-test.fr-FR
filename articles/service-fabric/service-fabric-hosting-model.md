---
title: "aaaAzure modèle d’hébergement de Service Fabric | Documents Microsoft"
description: "Décrit la relation entre les réplicas (ou instances) d’un service Service Fabric déployé et le processus hôte du service."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Modèle d’hébergement Service Fabric
Cet article fournit une vue d’ensemble des modèles fournis par l’infrastructure de Service d’hébergement d’applications et décrit les différences de hello hello **partagé des processus** et **processus exclusif** modèles. Il décrit le fonctionnement d’une application déployée sur un nœud de l’infrastructure de Service et la relation entre les réplicas ou les instances de service de hello et processus hôte de service de hello.

Avant de continuer, veillez à vous familiariser avec le [modèle d’application Service Fabric][a1] et à comprendre les différents concepts et leurs relations. 

> [!NOTE]
> Dans cet article, par souci de simplicité et sauf indication contraire :
>
> - Toutes les utilisations de word *réplica* fait référence tooboth un réplica d’une instance d’un service statless ou d’un service avec état.
> - *CodePackage* est équivalent traité trop*ServiceHost* processus qui enregistre une *ServiceType* et les réplicas des hôtes de services qui *ServiceType*.
>

toounderstand hello du modèle d’hébergement, nous guider un exemple. Supposons que nous avons un *ApplicationType* appelé « MyAppType » qui possède un *ServiceType* « MyServiceType » fourni par le *ServicePackage* « MyServicePackage », lequel possède un *CodePackage* « MyCodePackage » qui inscrit le *ServiceType* « MyServiceType » lors de son exécution.

Imaginons que nous avons un cluster à 3 nœuds et que nous créons une *application* **fabric:/App1** de type « MyAppType ». À l’intérieur de cette *application* **fabric:/App1**, nous créons un service **fabric:/App1/ServiceA** de type « MyServiceType » qui comporte 2 partitions (par exemple, **P1** & **P2**) avec 3 réplicas par partition. Hello diagramme suivant montre vue hello de cette application tel qu’il finit déployé sur un nœud.

<center>
![Vue de l’application déployée sur un nœud][node-view-one]
</center>

Service Fabric activé 'MyServicePackage' qui a démarré 'MyCodePackage', qui héberge les réplicas à partir de deux partitions hello c'est-à-dire **P1** & **P2**. Notez que tous les nœuds hello cluster de hello aura même vue puisque nous avons choisi le nombre de réplicas par toonumber égale de partition des nœuds de cluster de hello. Nous allons maintenant créer un autre service **fabric:/App1/ServiceB** dans l’application **fabric:/App1** qui comporte 1 partition (par exemple **P3**), avec 3 réplicas pour chaque partition. Diagramme suivant montre la nouvelle vue de hello sur le nœud de hello :

<center>
![Vue de l’application déployée sur un nœud][node-view-two]
</center>

Comme nous pouvons voir Service Fabric placé le nouveau réplica de partition de hello **P3** du service **fabric : / App1/ServiceB** dans hello existant l’activation du service 'MyServicePackage'. Créons maintenant une autre *application* **fabric:/App2** de type « MyAppType » ; à l’intérieur de cette application **fabric:/App2**, nous allons créer le service **fabric: App2/ServiceA** qui comporte 2 partitions (par exemple **P4** & **P5**) avec 3 réplicas pour chaque partition. Suivant les diagrammes affiche hello nouveau nœud :

<center>
![Vue de l’application déployée sur un nœud][node-view-three]
</center>

Cette fois, Service Fabric a activé une nouvelle copie de « MyServicePackage », qui démarre une nouvelle copie de « MyCodePackage », et les réplicas des deux partitions du service **fabric:/App2/ServiceA** (c’est-à-dire **P4** & **P5**) sont placés dans cette nouvelle copie « MyCodePackage ».

## <a name="shared-process-model"></a>Modèle à processus partagé
Ce que nous avons vu ci-dessus est le modèle fourni par l’infrastructure de Service d’hébergement de la valeur par défaut hello et est référencé tooas **partagé des processus** modèle. Dans ce modèle, pour un donné *application*, qu’une seule copie d’un donné *ServicePackage* est activé sur un *nœud* (qui démarre hello tous les *CodePackages* qu’il contient) et tous les hello réplicas de tous les services d’une donnée *ServiceType* sont placés dans hello *CodePackage* qui enregistre que *ServiceType*. En d’autres termes, toutes les hello réplicas de tous les services d’une donnée *ServiceType* partager hello même processus.

## <a name="exclusive-process-model"></a>Modèle à processus exclusif
Bonjour autre modèle d’hébergement fourni par le Service Fabric est **processus exclusif** modèle. Dans ce modèle, sur une donnée *nœud*, pour placer chaque réplica, l’infrastructure de Service Active une nouvelle copie de *ServicePackage* (qui démarre tous les hello *CodePackages* qu’il contient ) et le réplica est placé dans hello *CodePackage* que hello inscrit *ServiceType* de hello service toowhich réplica appartient. En d’autres termes, chaque réplica réside dans son propre processus dédié. 

Ce modèle est pris en charge à partir de la version 5.6 de Service Fabric. **Processus exclusif** modèle peut être choisi au moment de hello de création de service de hello (à l’aide de [PowerShell][p1], [reste] [ r1]ou [fabricclient ne][c1]) en spécifiant **ServicePackageActivationMode** en tant que 'ExclusiveProcess'.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Si votre manifeste d’application comporte un service par défaut, vous pouvez choisir le modèle à **processus exclusif** en spécifiant l’attribut **ServicePackageActivationMode** comme indiqué ci-dessous :

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Pour poursuivre avec notre exemple ci-dessus, vous permet de créer un autre service **fabric : / App1/ServiceC** dans l’application **fabric : / App1** ayant 2 partitions peuvent (dites **P6**  &  **P7**) et 3 réplicas par partition avec **ServicePackageActivationMode** définir too'ExclusiveProcess'. Diagramme suivant montre la nouvelle vue sur le nœud de hello :

<center>
![Vue de l’application déployée sur un nœud][node-view-four]
</center>

Comme vous pouvez le voir, Service Fabric a activé deux nouvelles copies de « MyServicePackage » (une pour chaque réplica des partitions **P6** & **P7**) et placé chaque réplica dans sa copie dédiée de *CodePackage*. Un autre toonote chose ici est, lorsque **processus exclusif** modèle est utilisé, pour une donnée *application*, de plusieurs copies d’une donnée *ServicePackage* peut être actif sur un  *Nœud*. Dans l’exemple ci-dessus, nous voyons que trois copies de « MyServicePackage » sont actives pour **fabric:/App1**. Chacune de ces copies actives de « MyServicePackage » est associé à un **ServicePackageActivationId** qui identifie cette copie dans *l’application* **fabric:/App1**.

Lorsque seul le modèle à **processus partagé** est utilisé pour une *application*, comme **fabric:/App2** dans l’exemple ci-dessus, il n’existe qu’une seule copie active de *ServicePackage* sur un *nœud* et le **ServicePackageActivationId** de cette activation de *ServicePackage* est « chaîne vide ».

> [!NOTE]
>- **Traitement partagé** modèle d’hébergement correspond trop**ServicePackageAtivationMode** égal **SharedProcess**. Modèle d’hébergement de la valeur par défaut hello et **ServicePackageAtivationMode** ne doivent pas être spécifié au moment de hello de création de service de hello.
>
>- **Processus exclusif** modèle d’hébergement correspond trop**ServicePackageAtivationMode** égal **ExclusiveProcess** et devez toobe explicitement spécifiée au moment de hello de création de hello service. 
>
>- Modèle d’hébergement d’un service peut être connu en interrogeant hello [description du service] [ p2] et en examinant la valeur de **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Utilisation d’un package de services déployé
Une copie active d’un *ServicePackage* sur un nœud est appelée [package de services déployé][p3]. Comme mentionné précédemment, lorsque **processus exclusif** modèle est utilisé pour la création de services, pour une donnée *application*, il peut y avoir plusieurs service déployé des packages pour hello même  *ServicePackage*. Lors de l’exécution des opérations comme package de service spécifique toodeployed [création de rapports d’intégrité d’un package de service déployé] [ p4] ou [le redémarrage du package de code d’un package de service déployé] [ p5] etc., **ServicePackageActivationId** besoins toobe fourni tooidentify un package de service déployé spécifique.

 **ServicePackageActivationId** d’un service déployé le package peut être obtenu en interrogeant la liste hello de [déployé des packages de service] [ p3] sur un nœud. Lors de l’interrogation [déployé des types de service][p6], [déployé réplicas] [ p7] et [déployé des packages de code] [ p8] sur un nœud, résultat de la requête hello contient également hello **ServicePackageActivationId** du package de service parent déployée.

> [!NOTE]
>- Sous le modèle d’hébergement à **processus partagé**, une seule copie d’un *ServicePackage* est activée sur un *nœud* donné et pour une *application* donnée. Il a **ServicePackageActivationId** égal trop*une chaîne vide* et ne doit pas être spécifié lors de l’exécution de package de service déployé operations. 
>
> - Sous le modèle d’hébergement à **processus exclusif**, une ou plusieurs copies d’un *ServicePackage* peuvent être actives sur un *nœud* donné et pour une *application* donnée. Chaque activation a un *non vide* **ServicePackageActivationId** et doit être toobe spécifié lors de l’exécution de package de service déployé operations. 
>
> - Si **ServicePackageActivationId** est ommited too'empty chaîne la valeur par défaut ». Si un service déployé package qui a été activée sous **partagé des processus** modèle est présent, l’opération sera exécutée, sinon hello opération échouera.
>
> - Il n’est pas recommandé tooquery qu’une seule fois et cache **ServicePackageActivationId** lorsqu’il est généré dynamiquement et peut changer pour différentes raisons. Avant d’effectuer une opération nécessitant une **ServicePackageActivationId**, vous devez tout d’abord interroger les liste hello de [déployé des packages de service] [ p3] sur un nœud et l’utiliser ensuite  *ServicePackageActivationId** à partir de l’opération d’origine de hello de tooperform de résultats de requête.
>
>

## <a name="guest-executable-and-container-applications"></a>Applications d’exécutables invités et de conteneurs
Service Fabric traite les applications [d’exécutables invités][a2] et de [conteneurs][a3] en tant que services sans état autonomes ; autrement dit, il n’y a aucun runtime Service Fabric dans *ServiceHost* (un processus ou un conteneur). Étant donné que ces services sont autonomes, le nombre de réplicas par *ServiceHost* n’est pas applicable à ces services. Bonjour configuration la plus courante utilisée avec ces services est à partition unique avec [InstanceCount] [ c2] égal trop-1 (autrement dit, une seule copie hello du code de service en cours d’exécution sur chaque nœud du cluster). 

par défaut de Hello **ServicePackageActivationMode** pour ces services est **SharedProcess** auquel cas l’infrastructure de Service Active uniquement une seule copie de *ServicePackage* sur un *Nœud* pour une donnée *application* ce qui ne signifie qu’une seule copie du code de service s’exécutera une *nœud*. Si vous souhaitez plusieurs copies de votre toorun de code de service sur un *nœud* lorsque vous créez plusieurs services (*Service1* trop*ServiceN*) de *ServiceType* (spécifié dans *ServiceManifest*) ou lorsque votre service est de plusieurs partitions, vous devez spécifier **ServicePackageActivationMode** en tant que **ExclusiveProcess**au moment de hello de création de service de hello.

## <a name="changing-hosting-model-of-an-existing-service"></a>Modification du modèle d’hébergement d’un service existant
La modification de modèle d’hébergement d’un service existant à partir de **partagé des processus** trop**processus exclusif** et vice versa à mettre à niveau ou de mise à jour (ou par défaut de spécification dans l’application de service manifeste) n’est actuellement pas pris en charge. Cette fonctionnalité sera prise en charge dans les futures versions.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Choix entre un modèle à processus partagé et un modèle à processus exclusif
À la fois ces modèles d’hébergement ont ses avantages et inconvénients utilisateur les besoins et tooevaluate celui qui convient le mieux à leurs besoins. **Traitement partagé** modèle permet d’optimiser l’utilisation des ressources du système d’exploitation, car le processus moins sont générés, plusieurs réplicas dans hello même processus peuvent partager des ports, etc.. Toutefois, si un des réplicas de hello rencontre une erreur où il doit toobring hôte de service hello vers le bas, il aura un impact sur tous les autres réplicas dans le même processus.

 Le modèle à **processus exclusif** isole mieux les réplicas en les associant à un processus dédié. Aussi, un dysfonctionnement d’un réplica n’aura aucune incidence sur les autres réplicas. Il est utile pour les cas où le partage de port n'est pas pris en charge par le protocole de communication hello. Il facilite hello capacité tooapply la gouvernance des ressources au niveau du réplica. Hello de d’autre part, **processus exclusif** consomme plus de ressources du système d’exploitation qu’il génère un processus pour chaque réplica sur le nœud de hello.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Considérations relatives au modèle à processus exclusif et au modèle d’application
Hello recommandé toomodel de la façon dont votre application dans le Service Fabric est tookeep une *ServiceType* par *ServicePackage* et ce modèle fonctionne bien pour la plupart des applications de hello. 

Toutefois, les scénarios particuliers tooenable où un *ServiceType* par *ServicePackage* peut-être pas souhaitable, d’un point de vue fonctionnel, Service Fabric permet toohave plusieurs *ServiceType* par *ServicePackage* (un seul *CodePackage* peut inscrire plusieurs fois *ServiceType*). Voici quelques-uns des scénarios hello où ces configurations peuvent être utiles :

- Vous voulez toooptimize l’utilisation des ressources du système d’exploitation par génération dynamique des processus moins et ayant une densité plus élevée de réplica par processus.
- Réplicas à partir de différents ServiceTypes doivent tooshare certaines données communes ayant une initialisation haute ou la mémoire de coût.
- Vous avez une offre de service gratuit et que vous souhaitez tooput une limite l’utilisation des ressources en plaçant tous les réplicas du service de hello dans le même processus.

Le modèle d’hébergement à **processus exclusif** n’est pas cohérent avec le modèle d’application qui utilise plusieurs *ServiceTypes* par *ServicePackage*. Il s’agit, car plusieurs *ServiceTypes* par *ServicePackage* est tooachieve conçue supérieur partage de ressources entre les réplicas et permet une densité plus élevée de réplica par processus. Cela est contraire toowhat **processus exclusif** modèle est conçu tooachieve.

Considérez les cas de hello de plusieurs *ServiceTypes* par *ServicePackage* avec différents *CodePackage* chaque enregistrement *ServiceType*. Supposons que nous avons un *ServicePackage* « MultiTypeServicePackage » qui comporte deux *CodePackages* :

- « MyCodePackageA » inscrit le *ServiceType* « MyServiceTypeA ».
- « MyCodePackageB » inscrit le *ServiceType* « MyServiceTypeB ».

Supposons, à présent, que nous créons une *application* **fabric:/SpecialApp** et que, à l’intérieur de cette application **fabric:/SpecialApp**, nous créons les deux services suivants avec le modèle à **processus exclusif** :

- Le service **fabric:/SpecialApp/ServiceA** de type « MyServiceTypeA » avec deux partitions (par exemple, **P1** et **P2**) et 3 réplicas par partition.
- Le service **fabric:/SpecialApp/ServiceB** de type « MyServiceTypeB » avec deux partitions (par exemple, **P3** et **P4**) et 3 réplicas par partition.

Sur un nœud donné, les deux services hello aura deux réplicas. Étant donné que nous avons utilisé **processus exclusif** services hello du modèle toocreate, Service Fabric seront activent une nouvelle copie de 'MyServicePackge' pour chaque réplica. Chaque activation de «MultiTypeServicePackage » démarre une copie de « MyCodePackageA » et « MyCodePackageB ». Toutefois, seul 'MyCodePackageA' ou 'MyCodePackageB' héberge le réplica de hello pour laquelle 'MultiTypeServicePackge' a été activé. Diagramme suivant montre le mode de nœud hello :

<center>
![Vue de l’application déployée sur un nœud][node-view-five]
</center>

 Comme nous pouvons le constater, l’activation de hello de 'MultiTypeServicePackge' pour le réplica de partition **P1** du service **fabric : / SpecialApp/services**, 'MyCodePackageA' héberge un réplica de hello et ' MyCodePackageB' est simplement en cours d’exécution. De même, dans l’activation de 'MultiTypeServicePackge' pour le réplica de partition **P3** du service **fabric : / SpecialApp/ServiceB**, 'MyCodePackageB' héberge un réplica de hello et 'MyCodePackageA' est juste en cours d’exécution et ainsi de suite. Par conséquent, plus de hello nombre de *CodePackages* (inscription différents *ServiceTypes*) par *ServicePackage*, plue sera l’utilisation des ressources redondant. 
 
 Hello d’autre part, si nous créons des services **fabric : / SpecialApp/services** et **fabric : / SpecialApp/ServiceB** avec **partagé des processus** de modèle, est de l’infrastructure de Service activer qu’une seule copie de 'MultiTypeServicePackge' pour *application* **fabric : / SpecialApp** (comme nous l’avons vu précédemment). 'MyCodePackageA' destiné à héberger tous les réplicas de service **fabric : / SpecialApp/services** (ou de n’importe quel service de type toobe 'MyServiceTypeA' plus précise) et 'MyCodePackageB' destiné à héberger tous les réplicas de service **fabric : / SpecialApp/ServiceB** (ou de n’importe quel service de type toobe 'MyServiceTypeB' plus précis). Diagramme suivant montre le mode de nœud hello dans ce paramètre : 

<center>
![Vue de l’application déployée sur un nœud][node-view-six]
</center>

Bonjour exemple ci-dessus, vous pouvez penser si 'MyCodePackageA' inscrit 'MyServiceTypeA' et 'MyServiceTypeB' et il n’existe aucune « MyCodePackageB », puis il y aura non redondant *CodePackage* en cours d’exécution. Cela est correct, cependant, comme mentionné précédemment, ce modèle d’application n’est pas aligné sur modèle d’hébergement à **processus exclusif**. Si l’objectif est tooput chaque réplica dans son propre dédiée de processus, puis inscrire les *ServiceTypes* de même *CodePackage* n’est pas nécessaire et en les mettant chacune *ServiceType* dans son propre *ServicePacakge* est un choix plus naturel.

## <a name="next-steps"></a>Étapes suivantes
[Empaqueter une application] [ a4] et toodeploy prêt.

[Déployer et supprimer des applications] [ a5] décrit comment instances d’application toomanage toouse PowerShell.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage