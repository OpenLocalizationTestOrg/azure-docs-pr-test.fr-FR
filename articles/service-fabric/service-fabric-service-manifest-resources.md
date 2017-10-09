---
title: points de terminaison de service aaaSpecifying Service Fabric | Documents Microsoft
description: "Comment se manifeste toodescribe des ressources de point de terminaison d’un service, y compris la manière tooset des points de terminaison HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a>Spécifier des ressources dans un manifeste de service
## <a name="overview"></a>Vue d'ensemble
manifeste de service Hello permet aux ressources utilisées par toobe de service hello déclaré/modifié sans modifier le code de hello compilé. Azure Service Fabric prend en charge la configuration des ressources du point de terminaison pour le service de hello. Hello accès toohello ressources qui sont spécifiés dans le manifeste de service hello peuvent être contrôlés via hello groupe de sécurité dans le manifeste de l’application hello. déclaration de Hello de ressources permet d’enregistrer ces toobe ressources modifiées au moment du déploiement, ce qui signifie que le service de hello n’a pas besoin toointroduce un nouveau mécanisme de configuration. Hello définition de schéma pour le fichier ServiceManifest.xml de hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Points de terminaison
Lorsqu’une ressource de point de terminaison est définie dans le manifeste de service hello, Service Fabric assigne des ports à partir de la plage de ports d’application hello réservé lorsqu’un port n’est pas spécifié explicitement. Par exemple, présenter au point de terminaison hello *ServiceEndpoint1* spécifiée dans le manifeste extrait de code hello fourni après ce point. En outre, les services peuvent également demander un port spécifique d’une ressource. Réplicas de service en cours d’exécution sur différents nœuds de cluster peuvent avoir des numéros de ports différents, tandis que les réplicas d’un service en cours d’exécution hello même port hello de partage de nœud. réplicas de service Hello peuvent ensuite utiliser ces ports selon vos besoins pour la réplication et écoute les demandes du client.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Consultez trop[configuration des Services fiables avec état](service-fabric-reliable-services-configuration.md) tooread plus sur la référence à des points de terminaison à partir du fichier de paramètres de package hello config (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Exemple : spécification d’un point de terminaison HTTP pour votre service
Hello manifeste de service suivant définit une ressource de point de terminaison TCP et les deux ressources de point de terminaison HTTP Bonjour &lt;ressources&gt; élément.

Les points de terminaison HTTP sont automatiquement répertoriés dans la liste de contrôle d’accès par Service Fabric.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Exemple : spécification d’un point de terminaison HTTPS pour votre service
Hello le protocole HTTPS assure l’authentification du serveur et est également utilisé pour le chiffrement des communications client-serveur. tooenable HTTPS sur votre service Service Fabric, spécifiez le protocole de hello Bonjour *ressources -> points de terminaison -> point de terminaison* section hello du manifeste de service, comme indiqué précédemment pour le point de terminaison hello *ServiceEndpoint3* .

> [!NOTE]
> Il est impossible de modifier le protocole d’un service lors de la mise à niveau de l’application. En effet, il s’agit d’une modification avec rupture.
> 
> 

Voici un exemple ApplicationManifest que vous avez besoin de tooset pour le protocole HTTPS. l’empreinte numérique Hello pour votre certificat doit être fourni. Hello EndpointRef est une référence tooEndpointResource dans ServiceManifest, pour lequel vous définissez le protocole HTTPS hello. Vous pouvez ajouter plusieurs EndpointCertificate.  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Écraser des points de terminaison dans ServiceManifest.xml

Bonjour ApplicationManifest ajouter une section ResourceOverrides qui sera une section de tooConfigOverrides frère. Dans cette section, vous pouvez spécifier remplacement hello pour la section de points de terminaison de hello de section de ressources hello spécifiée dans le manifeste de Service hello.

Dans l’ordre toooverride point de terminaison dans un ServiceManifest à l’aide de la modification de ApplicationParameters hello ApplicationManifest comme suit :

Bonjour ServiceManifestImport section, ajoutez une nouvelle section « ResourceOverrides »

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

Bonjour qu'ajoutent des paramètres ci-dessous :

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Lors du déploiement d’application hello maintenant vous pouvez passer ces valeurs comme ApplicationParameters par exemple :

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Remarque : Si les valeurs hello fournissent pour hello ApplicationParameters est vide nous revenir en arrière par défaut de toohello la valeur fournie pour hello ServiceManifest pour hello correspondant EndPointName.

Par exemple :

En cas de hello ServiceManifest que vous avez spécifié

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Hello Port1 et valeur Protocol1 pour les paramètres d’Application est null ou vide. port de Hello est toujours décidé par ServiceFabric. Et hello protocole est tcp.

Supposons que vous spécifiez une valeur incorrecte. Par exemple, pour Port, vous avez spécifié la valeur de chaîne « Foo » au lieu d’un entier.  Nouveau-ServiceFabricApplication commande échouera avec une erreur : paramètre de remplacement hello avec l’attribut de nom « ServiceEndpoint1 » « Port1 » dans la section 'ResourceOverrides' n’est pas valide. valeur Hello spécifiée est « Foo » et est de 'type int' requis.
