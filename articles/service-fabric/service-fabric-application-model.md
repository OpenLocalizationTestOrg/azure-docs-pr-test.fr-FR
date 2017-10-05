---
title: "Modèle d’application Azure Service Fabric | Microsoft Docs"
description: "Comment modéliser et décrire des applications et des services dans Service Fabric."
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
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="24b0c-103">Modéliser une application dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="24b0c-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="24b0c-104">Cet article fournit une vue d’ensemble du modèle d’application Azure Service Fabric et explique comment définir une application et un service via des fichiers manifestes.</span><span class="sxs-lookup"><span data-stu-id="24b0c-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="24b0c-105">Comprendre le modèle d'application</span><span class="sxs-lookup"><span data-stu-id="24b0c-105">Understand the application model</span></span>
<span data-ttu-id="24b0c-106">Une application est une collection de services constitutifs qui exécutent une ou plusieurs fonctions.</span><span class="sxs-lookup"><span data-stu-id="24b0c-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="24b0c-107">Un service exécute une fonction complète et autonome, et peut démarrer et s’exécuter indépendamment d’autres services.</span><span class="sxs-lookup"><span data-stu-id="24b0c-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="24b0c-108">Un service est composé d’un code, d’une configuration et de données.</span><span class="sxs-lookup"><span data-stu-id="24b0c-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="24b0c-109">Pour chaque service, le code se compose de fichiers binaires exécutables, la configuration comprend des paramètres de service qui peuvent être chargés pendant l'exécution, tandis que les données comportent des données statiques arbitraires destinées à être consommées par le service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="24b0c-110">Chaque composant de ce modèle d'application hiérarchique peut faire l'objet d'une gestion de versions et d'une mise à niveau indépendantes.</span><span class="sxs-lookup"><span data-stu-id="24b0c-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Modèle d'application Service Fabric][appmodel-diagram]

<span data-ttu-id="24b0c-112">Un type d'application est une catégorisation d'une application constituée d'un ensemble de types de service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="24b0c-113">Un type de service est la catégorisation d’un service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="24b0c-114">La catégorisation peut avoir différents paramètres et différentes configurations, mais la fonctionnalité principale reste la même.</span><span class="sxs-lookup"><span data-stu-id="24b0c-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="24b0c-115">Les instances d'un service représentent les variantes de configuration de service d'un même type de service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="24b0c-116">Les classes (ou « types ») d’applications et de services sont décrits dans des fichiers XML (manifestes d’application et manifestes de service).</span><span class="sxs-lookup"><span data-stu-id="24b0c-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="24b0c-117">Les manifestes sont les modèles par rapport auxquels des applications peuvent être instanciées à partir du magasin d’images du cluster.</span><span class="sxs-lookup"><span data-stu-id="24b0c-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="24b0c-118">La définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml est installée avec le SDK Service Fabric et les outils sous *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="24b0c-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="24b0c-119">Le code de différentes instances d’application s’exécute sous forme de processus distincts, même si elles sont hébergées par le même nœud Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24b0c-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="24b0c-120">En outre, le cycle de vie de chaque instance d’application peut être géré (par exemple, mis à jour) de façon indépendante.</span><span class="sxs-lookup"><span data-stu-id="24b0c-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="24b0c-121">Comme le montre le diagramme suivant, les types d’application sont composés de types de service, eux-mêmes constitués de packages de code, de configuration et de données.</span><span class="sxs-lookup"><span data-stu-id="24b0c-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="24b0c-122">Pour simplifier le diagramme, seuls les packages code/configuration/données pour `ServiceType4` sont affichés, même si chaque type de service inclut tout ou partie de ces types de packages.</span><span class="sxs-lookup"><span data-stu-id="24b0c-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Types d’application service Fabric et types de service][cluster-imagestore-apptypes]

<span data-ttu-id="24b0c-124">Deux fichiers manifestes différents sont utilisés pour décrire des applications et des services : le manifeste de service et le manifeste d'application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="24b0c-125">Les manifestes sont décrits en détail dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="24b0c-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="24b0c-126">Une ou plusieurs instances d'un type de service peuvent être actives dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="24b0c-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="24b0c-127">Par exemple, les instances de service avec état, ou réplicas, assurent une grande fiabilité en répliquant l'état entre les réplicas situés sur différents nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="24b0c-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="24b0c-128">La réplication garantit essentiellement la redondance du service en cas de défaillance d’un nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="24b0c-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="24b0c-129">Un [service partitionné](service-fabric-concepts-partitioning.md) subdivise son état (et les modèles d'accès à cet état) entre les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="24b0c-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="24b0c-130">Le diagramme suivant montre la relation entre les applications et les instances de service, les partitions et les réplicas.</span><span class="sxs-lookup"><span data-stu-id="24b0c-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Partitions et réplicas au sein d'un service][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="24b0c-132">Vous pouvez afficher la disposition des applications dans un cluster à l’aide de l’outil Service Fabric Explorer disponible à l’adresse http://&lt;adresse_cluster&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="24b0c-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="24b0c-133">Pour plus d’informations, voir [Visualisation de votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="24b0c-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="24b0c-134">Décrire un service</span><span class="sxs-lookup"><span data-stu-id="24b0c-134">Describe a service</span></span>
<span data-ttu-id="24b0c-135">Le manifeste de service définit de manière déclarative le type de service et la version.</span><span class="sxs-lookup"><span data-stu-id="24b0c-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="24b0c-136">Il spécifie les métadonnées de service telles que le type de service, les propriétés du contrôle d’intégrité, des mesures d’équilibrage de charge, des fichiers binaires de service et des fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="24b0c-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="24b0c-137">Autrement dit, il décrit les packages de code, de configuration et de données qui composent un package de service pour prendre en charge un ou plusieurs types de service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="24b0c-138">Voici un exemple simple de manifeste de service :</span><span class="sxs-lookup"><span data-stu-id="24b0c-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="24b0c-139">**Version** sont des chaînes non structurées et ne sont pas analysés par le système.</span><span class="sxs-lookup"><span data-stu-id="24b0c-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="24b0c-140">Les attributs de version permettent de gérer les versions de chaque composant au moment des mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="24b0c-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="24b0c-141">**ServiceTypes** déclare les types de service pris en charge par des packages de code (**CodePackage**) dans ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="24b0c-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="24b0c-142">Quand un service est instancié par rapport à un de ces types de service, tous les packages de code déclarés dans ce manifeste sont activés en exécutant leurs points d'entrée.</span><span class="sxs-lookup"><span data-stu-id="24b0c-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="24b0c-143">Les processus qui en résultent sont censés inscrire les types de service pris en charge au moment de l'exécution.</span><span class="sxs-lookup"><span data-stu-id="24b0c-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="24b0c-144">Les types de service sont déclarés au niveau du manifeste et non au niveau du package de code.</span><span class="sxs-lookup"><span data-stu-id="24b0c-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="24b0c-145">Ainsi, s'il existe plusieurs packages de code, ceux-ci sont tous activés chaque fois que le système recherche l'un des types de service déclarés.</span><span class="sxs-lookup"><span data-stu-id="24b0c-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="24b0c-146">**SetupEntryPoint** est un point d'entrée privilégié qui s'exécute avec les mêmes informations d'identification que Service Fabric (généralement le compte *LocalSystem* ) avant tout autre point d'entrée.</span><span class="sxs-lookup"><span data-stu-id="24b0c-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="24b0c-147">Le fichier exécutable spécifié par **EntryPoint** est généralement l’hôte de service à exécution longue.</span><span class="sxs-lookup"><span data-stu-id="24b0c-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="24b0c-148">La présence d’un point d’entrée de configuration distinct évite d’avoir à exécuter l’hôte de service avec des privilèges élevés pendant de longues périodes de temps.</span><span class="sxs-lookup"><span data-stu-id="24b0c-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="24b0c-149">Le fichier exécutable spécifié par **EntryPoint** est exécuté une fois que **SetupEntryPoint** se termine correctement.</span><span class="sxs-lookup"><span data-stu-id="24b0c-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="24b0c-150">En cas d’interruption ou de défaillance du processus, le processus résultant fait l’objet d’une surveillance et est redémarré (à partir de **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="24b0c-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="24b0c-151">**SetupEntryPoint** est généralement utilisé lorsque vous exécutez un fichier exécutable avant le démarrage du service ou si vous effectuez une opération avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="24b0c-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="24b0c-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="24b0c-152">For example:</span></span>

* <span data-ttu-id="24b0c-153">la configuration et l’initialisation de variables d'environnement dont le fichier exécutable du service a besoin,</span><span class="sxs-lookup"><span data-stu-id="24b0c-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="24b0c-154">sans limitation aux seuls exécutables écrits via les modèles de programmation de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="24b0c-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="24b0c-155">Par exemple, npm.exe a besoin de certaines variables d’environnement configurées pour le déploiement d’une application node.js.</span><span class="sxs-lookup"><span data-stu-id="24b0c-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="24b0c-156">La configuration d’un contrôle d’accès via l’installation de certificats de sécurité.</span><span class="sxs-lookup"><span data-stu-id="24b0c-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="24b0c-157">Pour plus d’informations sur la façon de configurer **SetupEntryPoint** consultez [Configurer la stratégie pour un point d’entrée de configuration de service](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="24b0c-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="24b0c-158">**EnvironmentVariables** fournit une liste des variables d’environnement définies pour ce package de code.</span><span class="sxs-lookup"><span data-stu-id="24b0c-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="24b0c-159">Les variables d’environnement peuvent être remplacées dans le fichier `ApplicationManifest.xml` pour fournir différentes valeurs pour différentes instances de service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="24b0c-160">**DataPackage** déclare un dossier, nommé par l’attribut **Name**, qui contient des données statiques arbitraires destinées à être consommées par le processus pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="24b0c-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="24b0c-161">**ConfigPackage** déclare un dossier, nommé par l’attribut **Name**, qui contient un fichier *Settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="24b0c-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="24b0c-162">Ce fichier de paramètres contient des sections de paramètres clé-valeur définis par l’utilisateur, que le processus lit pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="24b0c-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="24b0c-163">Le processus en cours d’exécution n’est pas redémarré pendant la mise à niveau si seule la **version** de **ConfigPackage** a changé.</span><span class="sxs-lookup"><span data-stu-id="24b0c-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="24b0c-164">Au lieu de cela, un rappel indique au processus que les paramètres de configuration ont été modifiés afin qu'ils puissent être rechargés dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="24b0c-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="24b0c-165">Voici un exemple de fichier *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="24b0c-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="24b0c-166">Un manifeste de service peut contenir plusieurs packages de code, de configuration et de données.</span><span class="sxs-lookup"><span data-stu-id="24b0c-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="24b0c-167">Les versions de chacun de ces packages peuvent être gérées de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="24b0c-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="24b0c-168">Décrire une application</span><span class="sxs-lookup"><span data-stu-id="24b0c-168">Describe an application</span></span>
<span data-ttu-id="24b0c-169">Le manifeste d’application décrit le type et la version de manière déclarative.</span><span class="sxs-lookup"><span data-stu-id="24b0c-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="24b0c-170">Il spécifie les métadonnées de composition de service telles que les noms stables, le schéma de partitionnement, le nombre d'instances/facteur de réplication, la stratégie de sécurité/d'isolation, les contraintes de placement, les remplacements de configuration et les types de service constitutifs.</span><span class="sxs-lookup"><span data-stu-id="24b0c-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="24b0c-171">Les domaines d'équilibrage de charge dans lesquels l'application est placée sont également décrits.</span><span class="sxs-lookup"><span data-stu-id="24b0c-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="24b0c-172">Ainsi, un manifeste d'application décrit les éléments au niveau de l'application et fait référence à un ou plusieurs des manifestes de service pour composer un type d'application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="24b0c-173">Voici un exemple simple de manifeste d'application :</span><span class="sxs-lookup"><span data-stu-id="24b0c-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="24b0c-174">Comme dans le cas des manifestes de service, les attributs **Version** sont des chaînes non structurées et ne sont pas analysés par le système.</span><span class="sxs-lookup"><span data-stu-id="24b0c-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="24b0c-175">Les attributs de version permettent également de gérer les versions de chaque composant au moment des mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="24b0c-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="24b0c-176">**ServiceManifestImport** contient des références aux manifestes de service qui composent ce type d'application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="24b0c-177">Les manifestes de service importés déterminent les types de service qui sont valides dans ce type d'application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="24b0c-178">Dans ServiceManifestImport, vous remplacez les valeurs de configuration dans le fichier Settings.xml, et les variables d’environnement dans le fichier ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="24b0c-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="24b0c-179">**DefaultServices** déclare des instances de service qui sont créées automatiquement chaque fois qu'une application est instanciée par rapport à ce type d'application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="24b0c-180">Les services par défaut peuvent s'avérer pratiques et se comportent à tous égards comme des services normaux une fois qu'ils ont été créés.</span><span class="sxs-lookup"><span data-stu-id="24b0c-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="24b0c-181">Ils sont mis à niveau avec tous les autres services dans l'instance d'application et peuvent également être supprimés.</span><span class="sxs-lookup"><span data-stu-id="24b0c-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="24b0c-182">Un manifeste d'application peut contenir plusieurs importations de manifeste de service et services par défaut.</span><span class="sxs-lookup"><span data-stu-id="24b0c-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="24b0c-183">La version de chaque importation de manifeste de service peut être gérée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="24b0c-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="24b0c-184">Pour savoir comment mettre à jour différents paramètres d’application et de service dans des environnements individuels, consultez [Gestion des paramètres d’application pour plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="24b0c-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="24b0c-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24b0c-185">Next steps</span></span>
<span data-ttu-id="24b0c-186">[Empaquetez une application](service-fabric-package-apps.md) et préparez-la pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="24b0c-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="24b0c-187">[Déployer et supprimer des applications][10] explique comment utiliser PowerShell pour gérer des instances d’application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="24b0c-188">[Gestion des paramètres d’application pour plusieurs environnements][11] décrit comment configurer les paramètres et les variables d’environnement pour différentes instances d’application.</span><span class="sxs-lookup"><span data-stu-id="24b0c-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="24b0c-189">[Configurer les stratégies de sécurité de votre application][12] décrit comment exécuter des services dans le cadre de stratégies de sécurité pour restreindre l’accès.</span><span class="sxs-lookup"><span data-stu-id="24b0c-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="24b0c-190">[Modèles d’hébergement d’applications][13] décrit la relation entre les réplicas (ou instances) d’un service déployé et le processus hôte du service.</span><span class="sxs-lookup"><span data-stu-id="24b0c-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
