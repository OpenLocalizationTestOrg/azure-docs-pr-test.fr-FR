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
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="2998b-103">Spécifier des ressources dans un manifeste de service</span><span class="sxs-lookup"><span data-stu-id="2998b-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="2998b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2998b-104">Overview</span></span>
<span data-ttu-id="2998b-105">manifeste de service Hello permet aux ressources utilisées par toobe de service hello déclaré/modifié sans modifier le code de hello compilé.</span><span class="sxs-lookup"><span data-stu-id="2998b-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="2998b-106">Azure Service Fabric prend en charge la configuration des ressources du point de terminaison pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="2998b-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="2998b-107">Hello accès toohello ressources qui sont spécifiés dans le manifeste de service hello peuvent être contrôlés via hello groupe de sécurité dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2998b-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="2998b-108">déclaration de Hello de ressources permet d’enregistrer ces toobe ressources modifiées au moment du déploiement, ce qui signifie que le service de hello n’a pas besoin toointroduce un nouveau mécanisme de configuration.</span><span class="sxs-lookup"><span data-stu-id="2998b-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="2998b-109">Hello définition de schéma pour le fichier ServiceManifest.xml de hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="2998b-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="2998b-110">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="2998b-110">Endpoints</span></span>
<span data-ttu-id="2998b-111">Lorsqu’une ressource de point de terminaison est définie dans le manifeste de service hello, Service Fabric assigne des ports à partir de la plage de ports d’application hello réservé lorsqu’un port n’est pas spécifié explicitement.</span><span class="sxs-lookup"><span data-stu-id="2998b-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="2998b-112">Par exemple, présenter au point de terminaison hello *ServiceEndpoint1* spécifiée dans le manifeste extrait de code hello fourni après ce point.</span><span class="sxs-lookup"><span data-stu-id="2998b-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="2998b-113">En outre, les services peuvent également demander un port spécifique d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="2998b-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="2998b-114">Réplicas de service en cours d’exécution sur différents nœuds de cluster peuvent avoir des numéros de ports différents, tandis que les réplicas d’un service en cours d’exécution hello même port hello de partage de nœud.</span><span class="sxs-lookup"><span data-stu-id="2998b-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="2998b-115">réplicas de service Hello peuvent ensuite utiliser ces ports selon vos besoins pour la réplication et écoute les demandes du client.</span><span class="sxs-lookup"><span data-stu-id="2998b-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="2998b-116">Consultez trop[configuration des Services fiables avec état](service-fabric-reliable-services-configuration.md) tooread plus sur la référence à des points de terminaison à partir du fichier de paramètres de package hello config (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="2998b-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="2998b-117">Exemple : spécification d’un point de terminaison HTTP pour votre service</span><span class="sxs-lookup"><span data-stu-id="2998b-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="2998b-118">Hello manifeste de service suivant définit une ressource de point de terminaison TCP et les deux ressources de point de terminaison HTTP Bonjour &lt;ressources&gt; élément.</span><span class="sxs-lookup"><span data-stu-id="2998b-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="2998b-119">Les points de terminaison HTTP sont automatiquement répertoriés dans la liste de contrôle d’accès par Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2998b-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="2998b-120">Exemple : spécification d’un point de terminaison HTTPS pour votre service</span><span class="sxs-lookup"><span data-stu-id="2998b-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="2998b-121">Hello le protocole HTTPS assure l’authentification du serveur et est également utilisé pour le chiffrement des communications client-serveur.</span><span class="sxs-lookup"><span data-stu-id="2998b-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="2998b-122">tooenable HTTPS sur votre service Service Fabric, spécifiez le protocole de hello Bonjour *ressources -> points de terminaison -> point de terminaison* section hello du manifeste de service, comme indiqué précédemment pour le point de terminaison hello *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="2998b-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="2998b-123">Il est impossible de modifier le protocole d’un service lors de la mise à niveau de l’application.</span><span class="sxs-lookup"><span data-stu-id="2998b-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="2998b-124">En effet, il s’agit d’une modification avec rupture.</span><span class="sxs-lookup"><span data-stu-id="2998b-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="2998b-125">Voici un exemple ApplicationManifest que vous avez besoin de tooset pour le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2998b-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="2998b-126">l’empreinte numérique Hello pour votre certificat doit être fourni.</span><span class="sxs-lookup"><span data-stu-id="2998b-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="2998b-127">Hello EndpointRef est une référence tooEndpointResource dans ServiceManifest, pour lequel vous définissez le protocole HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="2998b-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="2998b-128">Vous pouvez ajouter plusieurs EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="2998b-128">You can add more than one EndpointCertificate.</span></span>  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="2998b-129">Écraser des points de terminaison dans ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="2998b-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="2998b-130">Bonjour ApplicationManifest ajouter une section ResourceOverrides qui sera une section de tooConfigOverrides frère.</span><span class="sxs-lookup"><span data-stu-id="2998b-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="2998b-131">Dans cette section, vous pouvez spécifier remplacement hello pour la section de points de terminaison de hello de section de ressources hello spécifiée dans le manifeste de Service hello.</span><span class="sxs-lookup"><span data-stu-id="2998b-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="2998b-132">Dans l’ordre toooverride point de terminaison dans un ServiceManifest à l’aide de la modification de ApplicationParameters hello ApplicationManifest comme suit :</span><span class="sxs-lookup"><span data-stu-id="2998b-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="2998b-133">Bonjour ServiceManifestImport section, ajoutez une nouvelle section « ResourceOverrides »</span><span class="sxs-lookup"><span data-stu-id="2998b-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="2998b-134">Bonjour qu'ajoutent des paramètres ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2998b-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="2998b-135">Lors du déploiement d’application hello maintenant vous pouvez passer ces valeurs comme ApplicationParameters par exemple :</span><span class="sxs-lookup"><span data-stu-id="2998b-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="2998b-136">Remarque : Si les valeurs hello fournissent pour hello ApplicationParameters est vide nous revenir en arrière par défaut de toohello la valeur fournie pour hello ServiceManifest pour hello correspondant EndPointName.</span><span class="sxs-lookup"><span data-stu-id="2998b-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="2998b-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2998b-137">For example:</span></span>

<span data-ttu-id="2998b-138">En cas de hello ServiceManifest que vous avez spécifié</span><span class="sxs-lookup"><span data-stu-id="2998b-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="2998b-139">Hello Port1 et valeur Protocol1 pour les paramètres d’Application est null ou vide.</span><span class="sxs-lookup"><span data-stu-id="2998b-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="2998b-140">port de Hello est toujours décidé par ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="2998b-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="2998b-141">Et hello protocole est tcp.</span><span class="sxs-lookup"><span data-stu-id="2998b-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="2998b-142">Supposons que vous spécifiez une valeur incorrecte.</span><span class="sxs-lookup"><span data-stu-id="2998b-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="2998b-143">Par exemple, pour Port, vous avez spécifié la valeur de chaîne « Foo » au lieu d’un entier.  Nouveau-ServiceFabricApplication commande échouera avec une erreur : paramètre de remplacement hello avec l’attribut de nom « ServiceEndpoint1 » « Port1 » dans la section 'ResourceOverrides' n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="2998b-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="2998b-144">valeur Hello spécifiée est « Foo » et est de 'type int' requis.</span><span class="sxs-lookup"><span data-stu-id="2998b-144">hello value specified is 'Foo' and required is 'int'.</span></span>
