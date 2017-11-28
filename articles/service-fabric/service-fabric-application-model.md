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
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="6f218-103">Modéliser une application dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6f218-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="6f218-104">Cet article fournit une vue d’ensemble du modèle d’application Azure Service Fabric hello et comment toodefine une application et service via les fichiers manifestes.</span><span class="sxs-lookup"><span data-stu-id="6f218-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="6f218-105">Comprendre le modèle d’application hello</span><span class="sxs-lookup"><span data-stu-id="6f218-105">Understand hello application model</span></span>
<span data-ttu-id="6f218-106">Une application est une collection de services constitutifs qui exécutent une ou plusieurs fonctions.</span><span class="sxs-lookup"><span data-stu-id="6f218-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="6f218-107">Un service exécute une fonction complète et autonome, et peut démarrer et s’exécuter indépendamment d’autres services.</span><span class="sxs-lookup"><span data-stu-id="6f218-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="6f218-108">Un service est composé d’un code, d’une configuration et de données.</span><span class="sxs-lookup"><span data-stu-id="6f218-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="6f218-109">Pour chaque service, code se compose de fichiers binaires exécutables de hello, la configuration comprend les paramètres de service qui peuvent être chargés au moment de l’exécution, et se composent de données de toobe arbitraire de données statiques consommée par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="6f218-110">Chaque composant de ce modèle d'application hiérarchique peut faire l'objet d'une gestion de versions et d'une mise à niveau indépendantes.</span><span class="sxs-lookup"><span data-stu-id="6f218-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![modèle d’application Hello Service Fabric][appmodel-diagram]

<span data-ttu-id="6f218-112">Un type d'application est une catégorisation d'une application constituée d'un ensemble de types de service.</span><span class="sxs-lookup"><span data-stu-id="6f218-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="6f218-113">Un type de service est la catégorisation d’un service.</span><span class="sxs-lookup"><span data-stu-id="6f218-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="6f218-114">catégorisation de Hello peut avoir différents paramètres et configurations, mais reste de fonctionnalités principales hello hello même.</span><span class="sxs-lookup"><span data-stu-id="6f218-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="6f218-115">variantes de configuration de service différent hello sont hello instances d’un service de hello même type de service.</span><span class="sxs-lookup"><span data-stu-id="6f218-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="6f218-116">Les classes (ou « types ») d’applications et de services sont décrits dans des fichiers XML (manifestes d’application et manifestes de service).</span><span class="sxs-lookup"><span data-stu-id="6f218-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="6f218-117">Hello manifestes sont des modèles de hello par rapport à laquelle les applications peuvent être instanciées à partir du magasin d’images du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="6f218-118">Hello définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="6f218-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="6f218-119">code Hello pour les instances d’application différents d’identification des processus distincts, même lorsque hébergé par hello même nœud de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6f218-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="6f218-120">En outre, hello de cycle de vie de chaque instance d’application peut être géré (par exemple, la mise à niveau) indépendamment.</span><span class="sxs-lookup"><span data-stu-id="6f218-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="6f218-121">Hello diagramme suivant montre comment les types d’applications sont composées de types de service, qui à son tour, sont constitués de code, la configuration et les packages de données.</span><span class="sxs-lookup"><span data-stu-id="6f218-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="6f218-122">diagramme de hello toosimplify, seuls les packages de données/config/code hello pour `ServiceType4` sont affichés, bien que chaque type de service inclut certains ou tous les types de package.</span><span class="sxs-lookup"><span data-stu-id="6f218-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Types d’application service Fabric et types de service][cluster-imagestore-apptypes]

<span data-ttu-id="6f218-124">Deux fichiers manifestes distincts sont utilisés toodescribe applications et services : hello du manifeste de service et le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="6f218-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="6f218-125">Les manifestes sont décrites en détail dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="6f218-126">Une ou plusieurs instances d’un type de service peuvent être actives dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="6f218-127">Par exemple, les instances de service avec état, ou réplicas, obtenir une haute fiabilité en répliquant l’état entre les réplicas situés sur différents nœuds dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="6f218-128">La réplication fournit essentiellement une redondance pour hello toobe de service disponible même si la défaillance d’un nœud dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="6f218-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="6f218-129">A [partitionnée service](service-fabric-concepts-partitioning.md) plus divise son état (et l’état d’accès aux modèles toothat) entre les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="6f218-130">Hello diagramme suivant montre relation hello entre les applications et les instances de service, les partitions et les réplicas.</span><span class="sxs-lookup"><span data-stu-id="6f218-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Partitions et réplicas au sein d'un service][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="6f218-132">Vous pouvez afficher la mise en page hello d’applications dans un cluster avec l’outil de Service Fabric Explorer hello disponible à http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="6f218-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="6f218-133">Pour plus d’informations, voir [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6f218-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="6f218-134">Décrire un service</span><span class="sxs-lookup"><span data-stu-id="6f218-134">Describe a service</span></span>
<span data-ttu-id="6f218-135">manifeste de service Hello définit de façon déclarative hello service type et la version.</span><span class="sxs-lookup"><span data-stu-id="6f218-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="6f218-136">Il spécifie les métadonnées de service telles que le type de service, les propriétés du contrôle d’intégrité, des mesures d’équilibrage de charge, des fichiers binaires de service et des fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="6f218-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="6f218-137">Autrement dit, il décrit les packages de code, la configuration et données hello qui composent un toosupport de package de service un ou plusieurs types de service.</span><span class="sxs-lookup"><span data-stu-id="6f218-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="6f218-138">Voici un exemple simple de manifeste de service :</span><span class="sxs-lookup"><span data-stu-id="6f218-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="6f218-139">**Version** attributs sont des chaînes non structurées et pas analysé par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="6f218-140">Attributs de version est utilisée tooversion chaque composant pour les mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="6f218-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="6f218-141">**ServiceTypes** déclare les types de service pris en charge par des packages de code (**CodePackage**) dans ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="6f218-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="6f218-142">Quand un service est instancié par rapport à un de ces types de service, tous les packages de code déclarés dans ce manifeste sont activés en exécutant leurs points d'entrée.</span><span class="sxs-lookup"><span data-stu-id="6f218-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="6f218-143">processus résultant de Hello sont des types de service attendu tooregister hello pris en charge au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6f218-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="6f218-144">Types de service sont déclarées au niveau de manifeste hello et pas hello code package.</span><span class="sxs-lookup"><span data-stu-id="6f218-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="6f218-145">Par conséquent, lorsqu’il existe plusieurs packages de code, ils sont tous activés chaque fois que le système de hello recherche n’importe laquelle d'entre hello déclarés de types de service.</span><span class="sxs-lookup"><span data-stu-id="6f218-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="6f218-146">**SetupEntryPoint** est un point d’entrée privilégiés qui s’exécute avec hello même les informations d’identification en tant que Service Fabric (généralement hello *LocalSystem* compte) avant de n’importe quel autre point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="6f218-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="6f218-147">exécutable Hello spécifié par **EntryPoint** est habituellement hello longue service hôte.</span><span class="sxs-lookup"><span data-stu-id="6f218-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="6f218-148">présence Hello de point d’entrée d’installation distinct permet d’éviter qu’un hôte de service hello toorun avec des privilèges élevés pendant de longues périodes de temps.</span><span class="sxs-lookup"><span data-stu-id="6f218-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="6f218-149">exécutable Hello spécifié par **EntryPoint** s’exécute après **SetupEntryPoint** se termine avec succès.</span><span class="sxs-lookup"><span data-stu-id="6f218-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="6f218-150">Si le processus de hello jamais s’arrête ou se bloque, le processus résultant de hello est surveillé et redémarré (compter à nouveau **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="6f218-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="6f218-151">Scénarios courants d’utilisation **SetupEntryPoint** sont lorsque vous exécutez un fichier exécutable avant le démarrage du service hello ou que vous effectuez une opération avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="6f218-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="6f218-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6f218-152">For example:</span></span>

* <span data-ttu-id="6f218-153">Configuration et l’initialisation des variables d’environnement qui hello besoins exécutable du service.</span><span class="sxs-lookup"><span data-stu-id="6f218-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="6f218-154">Cela n’est pas exécutables tooonly limitée par le biais de modèles de programmation de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="6f218-155">Par exemple, npm.exe a besoin de certaines variables d’environnement configurées pour le déploiement d’une application node.js.</span><span class="sxs-lookup"><span data-stu-id="6f218-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="6f218-156">La configuration d’un contrôle d’accès via l’installation de certificats de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6f218-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="6f218-157">Pour plus d’informations sur la façon de tooconfigure hello **SetupEntryPoint** consultez [configurer une stratégie de hello pour un point d’entrée de service d’installation](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="6f218-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="6f218-158">**EnvironmentVariables** fournit une liste des variables d’environnement définies pour ce package de code.</span><span class="sxs-lookup"><span data-stu-id="6f218-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="6f218-159">Les variables Environmentment peuvent être substituées dans hello `ApplicationManifest.xml` tooprovide des valeurs différentes pour les instances de service différent.</span><span class="sxs-lookup"><span data-stu-id="6f218-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="6f218-160">**DataPackage** déclare un dossier nommé par hello **nom** attribut, qui contient des toobe arbitraire de données statiques consommée par les processus de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6f218-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="6f218-161">**ConfigPackage** déclare un dossier nommé par hello **nom** attribut, qui contient un *Settings.xml* fichier.</span><span class="sxs-lookup"><span data-stu-id="6f218-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="6f218-162">fichier de paramètres Hello contient les sections de paramètres de la paire clé-valeur définies par l’utilisateur qui lit les processus de hello au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6f218-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="6f218-163">Pendant une mise à niveau, si seule hello **ConfigPackage** **version** a changé, hello processus en cours d’exécution n’est pas redémarré.</span><span class="sxs-lookup"><span data-stu-id="6f218-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="6f218-164">Au lieu de cela, un rappel notifie processus hello que les paramètres de configuration ont été modifiés afin qu’ils puissent être rechargées dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="6f218-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="6f218-165">Voici un exemple de fichier *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="6f218-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="6f218-166">Un manifeste de service peut contenir plusieurs packages de code, de configuration et de données.</span><span class="sxs-lookup"><span data-stu-id="6f218-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="6f218-167">Les versions de chacun de ces packages peuvent être gérées de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="6f218-167">Each of those can be versioned independently.</span></span>
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

## <a name="describe-an-application"></a><span data-ttu-id="6f218-168">Décrire une application</span><span class="sxs-lookup"><span data-stu-id="6f218-168">Describe an application</span></span>
<span data-ttu-id="6f218-169">manifeste de l’application Hello décrit de façon déclarative version et le type d’application hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="6f218-170">Il spécifie les métadonnées de composition de service telles que les noms stables, le schéma de partitionnement, le nombre d'instances/facteur de réplication, la stratégie de sécurité/d'isolation, les contraintes de placement, les remplacements de configuration et les types de service constitutifs.</span><span class="sxs-lookup"><span data-stu-id="6f218-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="6f218-171">domaines d’équilibrage de charge Hello dans lequel l’application hello est placée sont également décrits.</span><span class="sxs-lookup"><span data-stu-id="6f218-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="6f218-172">Par conséquent, un manifeste d’application décrit les éléments au niveau de l’application hello et fait référence à un ou plusieurs service manifestes toocompose un type d’application.</span><span class="sxs-lookup"><span data-stu-id="6f218-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="6f218-173">Voici un exemple simple de manifeste d'application :</span><span class="sxs-lookup"><span data-stu-id="6f218-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="6f218-174">Comme les manifestes de service, **Version** attributs sont des chaînes non structurées et ne sont pas analysés par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="6f218-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="6f218-175">Attributs de version est également utilisée tooversion chaque composant pour les mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="6f218-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="6f218-176">**ServiceManifestImport** contient des manifestes de tooservice de références qui composent ce type d’application.</span><span class="sxs-lookup"><span data-stu-id="6f218-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="6f218-177">Les manifestes de service importés déterminent les types de service qui sont valides dans ce type d'application.</span><span class="sxs-lookup"><span data-stu-id="6f218-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="6f218-178">Dans hello ServiceManifestImport, vous substituez les valeurs de configuration dans Settings.xml et environnement de variables dans les fichiers ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="6f218-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="6f218-179">**DefaultServices** déclare des instances de service qui sont créées automatiquement chaque fois qu'une application est instanciée par rapport à ce type d'application.</span><span class="sxs-lookup"><span data-stu-id="6f218-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="6f218-180">Les services par défaut peuvent s'avérer pratiques et se comportent à tous égards comme des services normaux une fois qu'ils ont été créés.</span><span class="sxs-lookup"><span data-stu-id="6f218-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="6f218-181">Ils sont mis à niveau, ainsi que d’autres services dans l’instance de l’application hello et peuvent être également supprimés.</span><span class="sxs-lookup"><span data-stu-id="6f218-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="6f218-182">Un manifeste d'application peut contenir plusieurs importations de manifeste de service et services par défaut.</span><span class="sxs-lookup"><span data-stu-id="6f218-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="6f218-183">La version de chaque importation de manifeste de service peut être gérée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="6f218-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="6f218-184">toolearn comment toomaintain une autre application et les paramètres de service pour des environnements individuels, consultez [la gestion des paramètres d’application de plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="6f218-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="6f218-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f218-185">Next steps</span></span>
<span data-ttu-id="6f218-186">[Empaqueter une application](service-fabric-package-apps.md) et le rendre prêt toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6f218-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="6f218-187">[Déployer et supprimer des applications] [ 10] décrit comment instances d’application toomanage toouse PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f218-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="6f218-188">[Gestion des paramètres d’application de plusieurs environnements] [ 11] décrit comment tooconfigure paramètres et variables d’environnement pour les instances de l’autre application.</span><span class="sxs-lookup"><span data-stu-id="6f218-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="6f218-189">[Configurer des stratégies de sécurité pour votre application] [ 12] décrit comment les services toorun sous toorestrict accès aux stratégies de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6f218-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="6f218-190">[Modèles d’hébergement d’applications][13] décrit la relation entre les réplicas (ou instances) d’un service déployé et le processus hôte du service.</span><span class="sxs-lookup"><span data-stu-id="6f218-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
