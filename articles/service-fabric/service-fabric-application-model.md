---
title: "modèle d’application Service Fabric aaaAzure | Documents Microsoft"
description: "Comment toomodel et décrire les applications et services dans l’infrastructure de Service."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modéliser une application dans Service Fabric
Cet article fournit une vue d’ensemble du modèle d’application Azure Service Fabric hello et comment toodefine une application et service via les fichiers manifestes.

## <a name="understand-hello-application-model"></a>Comprendre le modèle d’application hello
Une application est une collection de services constitutifs qui exécutent une ou plusieurs fonctions. Un service exécute une fonction complète et autonome, et peut démarrer et s’exécuter indépendamment d’autres services.  Un service est composé d’un code, d’une configuration et de données. Pour chaque service, code se compose de fichiers binaires exécutables de hello, la configuration comprend les paramètres de service qui peuvent être chargés au moment de l’exécution, et se composent de données de toobe arbitraire de données statiques consommée par le service de hello. Chaque composant de ce modèle d'application hiérarchique peut faire l'objet d'une gestion de versions et d'une mise à niveau indépendantes.

![modèle d’application Hello Service Fabric][appmodel-diagram]

Un type d'application est une catégorisation d'une application constituée d'un ensemble de types de service. Un type de service est la catégorisation d’un service. catégorisation de Hello peut avoir différents paramètres et configurations, mais reste de fonctionnalités principales hello hello même. variantes de configuration de service différent hello sont hello instances d’un service de hello même type de service.  

Les classes (ou « types ») d’applications et de services sont décrits dans des fichiers XML (manifestes d’application et manifestes de service).  Hello manifestes sont des modèles de hello par rapport à laquelle les applications peuvent être instanciées à partir du magasin d’images du cluster hello. Hello définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

code Hello pour les instances d’application différents d’identification des processus distincts, même lorsque hébergé par hello même nœud de Service Fabric. En outre, hello de cycle de vie de chaque instance d’application peut être géré (par exemple, la mise à niveau) indépendamment. Hello diagramme suivant montre comment les types d’applications sont composées de types de service, qui à son tour, sont constitués de code, la configuration et les packages de données. diagramme de hello toosimplify, seuls les packages de données/config/code hello pour `ServiceType4` sont affichés, bien que chaque type de service inclut certains ou tous les types de package.

![Types d’application service Fabric et types de service][cluster-imagestore-apptypes]

Deux fichiers manifestes distincts sont utilisés toodescribe applications et services : hello du manifeste de service et le manifeste d’application. Les manifestes sont décrites en détail dans les sections suivantes de hello.

Une ou plusieurs instances d’un type de service peuvent être actives dans le cluster de hello. Par exemple, les instances de service avec état, ou réplicas, obtenir une haute fiabilité en répliquant l’état entre les réplicas situés sur différents nœuds dans un cluster de hello. La réplication fournit essentiellement une redondance pour hello toobe de service disponible même si la défaillance d’un nœud dans un cluster. A [partitionnée service](service-fabric-concepts-partitioning.md) plus divise son état (et l’état d’accès aux modèles toothat) entre les nœuds de cluster de hello.

Hello diagramme suivant montre relation hello entre les applications et les instances de service, les partitions et les réplicas.

![Partitions et réplicas au sein d'un service][cluster-application-instances]

> [!TIP]
> Vous pouvez afficher la mise en page hello d’applications dans un cluster avec l’outil de Service Fabric Explorer hello disponible à http://&lt;yourclusteraddress&gt;: 19080/Explorer. Pour plus d’informations, voir [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Décrire un service
manifeste de service Hello définit de façon déclarative hello service type et la version. Il spécifie les métadonnées de service telles que le type de service, les propriétés du contrôle d’intégrité, des mesures d’équilibrage de charge, des fichiers binaires de service et des fichiers de configuration.  Autrement dit, il décrit les packages de code, la configuration et données hello qui composent un toosupport de package de service un ou plusieurs types de service. Voici un exemple simple de manifeste de service :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**Version** attributs sont des chaînes non structurées et pas analysé par le système de hello. Attributs de version est utilisée tooversion chaque composant pour les mises à niveau.

**ServiceTypes** déclare les types de service pris en charge par des packages de code (**CodePackage**) dans ce manifeste. Quand un service est instancié par rapport à un de ces types de service, tous les packages de code déclarés dans ce manifeste sont activés en exécutant leurs points d'entrée. processus résultant de Hello sont des types de service attendu tooregister hello pris en charge au moment de l’exécution. Types de service sont déclarées au niveau de manifeste hello et pas hello code package. Par conséquent, lorsqu’il existe plusieurs packages de code, ils sont tous activés chaque fois que le système de hello recherche n’importe laquelle d'entre hello déclarés de types de service.

**SetupEntryPoint** est un point d’entrée privilégiés qui s’exécute avec hello même les informations d’identification en tant que Service Fabric (généralement hello *LocalSystem* compte) avant de n’importe quel autre point d’entrée. exécutable Hello spécifié par **EntryPoint** est habituellement hello longue service hôte. présence Hello de point d’entrée d’installation distinct permet d’éviter qu’un hôte de service hello toorun avec des privilèges élevés pendant de longues périodes de temps. exécutable Hello spécifié par **EntryPoint** s’exécute après **SetupEntryPoint** se termine avec succès. Si le processus de hello jamais s’arrête ou se bloque, le processus résultant de hello est surveillé et redémarré (compter à nouveau **SetupEntryPoint**).  

Scénarios courants d’utilisation **SetupEntryPoint** sont lorsque vous exécutez un fichier exécutable avant le démarrage du service hello ou que vous effectuez une opération avec des privilèges élevés. Par exemple :

* Configuration et l’initialisation des variables d’environnement qui hello besoins exécutable du service. Cela n’est pas exécutables tooonly limitée par le biais de modèles de programmation de Service Fabric hello. Par exemple, npm.exe a besoin de certaines variables d’environnement configurées pour le déploiement d’une application node.js.
* La configuration d’un contrôle d’accès via l’installation de certificats de sécurité.

Pour plus d’informations sur la façon de tooconfigure hello **SetupEntryPoint** consultez [configurer une stratégie de hello pour un point d’entrée de service d’installation](service-fabric-application-runas-security.md)

**EnvironmentVariables** fournit une liste des variables d’environnement définies pour ce package de code. Les variables Environmentment peuvent être substituées dans hello `ApplicationManifest.xml` tooprovide des valeurs différentes pour les instances de service différent. 

**DataPackage** déclare un dossier nommé par hello **nom** attribut, qui contient des toobe arbitraire de données statiques consommée par les processus de hello en cours d’exécution.

**ConfigPackage** déclare un dossier nommé par hello **nom** attribut, qui contient un *Settings.xml* fichier. fichier de paramètres Hello contient les sections de paramètres de la paire clé-valeur définies par l’utilisateur qui lit les processus de hello au moment de l’exécution. Pendant une mise à niveau, si seule hello **ConfigPackage** **version** a changé, hello processus en cours d’exécution n’est pas redémarré. Au lieu de cela, un rappel notifie processus hello que les paramètres de configuration ont été modifiés afin qu’ils puissent être rechargées dynamiquement. Voici un exemple de fichier *Settings.xml* :

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Un manifeste de service peut contenir plusieurs packages de code, de configuration et de données. Les versions de chacun de ces packages peuvent être gérées de manière indépendante.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Décrire une application
manifeste de l’application Hello décrit de façon déclarative version et le type d’application hello. Il spécifie les métadonnées de composition de service telles que les noms stables, le schéma de partitionnement, le nombre d'instances/facteur de réplication, la stratégie de sécurité/d'isolation, les contraintes de placement, les remplacements de configuration et les types de service constitutifs. domaines d’équilibrage de charge Hello dans lequel l’application hello est placée sont également décrits.

Par conséquent, un manifeste d’application décrit les éléments au niveau de l’application hello et fait référence à un ou plusieurs service manifestes toocompose un type d’application. Voici un exemple simple de manifeste d'application :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Comme les manifestes de service, **Version** attributs sont des chaînes non structurées et ne sont pas analysés par le système de hello. Attributs de version est également utilisée tooversion chaque composant pour les mises à niveau.

**ServiceManifestImport** contient des manifestes de tooservice de références qui composent ce type d’application. Les manifestes de service importés déterminent les types de service qui sont valides dans ce type d'application. Dans hello ServiceManifestImport, vous substituez les valeurs de configuration dans Settings.xml et environnement de variables dans les fichiers ServiceManifest.xml. 


**DefaultServices** déclare des instances de service qui sont créées automatiquement chaque fois qu'une application est instanciée par rapport à ce type d'application. Les services par défaut peuvent s'avérer pratiques et se comportent à tous égards comme des services normaux une fois qu'ils ont été créés. Ils sont mis à niveau, ainsi que d’autres services dans l’instance de l’application hello et peuvent être également supprimés.

> [!NOTE]
> Un manifeste d'application peut contenir plusieurs importations de manifeste de service et services par défaut. La version de chaque importation de manifeste de service peut être gérée indépendamment.
> 
> 

toolearn comment toomaintain une autre application et les paramètres de service pour des environnements individuels, consultez [la gestion des paramètres d’application de plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Étapes suivantes
[Empaqueter une application](service-fabric-package-apps.md) et le rendre prêt toodeploy.

[Déployer et supprimer des applications] [ 10] décrit comment instances d’application toomanage toouse PowerShell.

[Gestion des paramètres d’application de plusieurs environnements] [ 11] décrit comment tooconfigure paramètres et variables d’environnement pour les instances de l’autre application.

[Configurer des stratégies de sécurité pour votre application] [ 12] décrit comment les services toorun sous toorestrict accès aux stratégies de sécurité.

[Modèles d’hébergement d’applications][13] décrit la relation entre les réplicas (ou instances) d’un service déployé et le processus hôte du service.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
