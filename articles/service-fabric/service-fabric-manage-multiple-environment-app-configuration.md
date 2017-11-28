---
title: aaaManage plusieurs environnements dans le Service Fabric | Documents Microsoft
description: "Applications de service Fabric peuvent être exécutées sur des clusters dont la taille à partir d’un ordinateur toothousands, des ordinateurs. Dans certains cas, vous devez tooconfigure votre application différemment pour les différents environnements. Cet article décrit comment toodefine les paramètres d’application par l’environnement."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="a27d4-105">Gestion des paramètres d’application pour plusieurs environnements</span><span class="sxs-lookup"><span data-stu-id="a27d4-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="a27d4-106">Vous pouvez créer des clusters d’Azure Service Fabric à l’aide de n’importe où à partir d’un seul réduire des milliers d’ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="a27d4-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="a27d4-107">Alors que les fichiers binaires d’application peuvent s’exécuter sans modification sur ce large éventail d’environnements, il est souvent nécessaire application hello de tooconfigure différemment, en fonction du nombre de hello d’ordinateurs que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="a27d4-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="a27d4-108">À titre d’exemple, envisagez d’utiliser `InstanceCount` pour un service sans état.</span><span class="sxs-lookup"><span data-stu-id="a27d4-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="a27d4-109">Quand vous exécutez des applications dans Azure, vous devez généralement tooset ce paramètre toohello valeur spéciale « -1 ».</span><span class="sxs-lookup"><span data-stu-id="a27d4-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="a27d4-110">Cette configuration garantit que votre service s’exécute sur chaque nœud de cluster de hello (ou tous les nœuds de type de nœud hello si vous avez défini une contrainte de placement).</span><span class="sxs-lookup"><span data-stu-id="a27d4-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="a27d4-111">Toutefois, cette configuration n’est pas appropriée pour un seul ordinateur cluster, car vous ne peut pas avoir plusieurs processus à l’écoute sur hello même point de terminaison sur un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a27d4-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="a27d4-112">Au lieu de cela, vous définissez généralement `InstanceCount` trop « 1 ».</span><span class="sxs-lookup"><span data-stu-id="a27d4-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="a27d4-113">Spécification des paramètres spécifiques à l’environnement</span><span class="sxs-lookup"><span data-stu-id="a27d4-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="a27d4-114">problème de configuration toothis Hello solution est un ensemble de services paramétrable par défaut et les fichiers de paramètres d’application qui remplissent ces valeurs de paramètre pour un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="a27d4-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="a27d4-115">Services par défaut et les paramètres de l’application sont configurés dans l’application hello et manifestes de service.</span><span class="sxs-lookup"><span data-stu-id="a27d4-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="a27d4-116">Hello définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="a27d4-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="a27d4-117">Services par défaut</span><span class="sxs-lookup"><span data-stu-id="a27d4-117">Default services</span></span>
<span data-ttu-id="a27d4-118">Les applications Service Fabric sont constituées d’une collection d’instances de service.</span><span class="sxs-lookup"><span data-stu-id="a27d4-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="a27d4-119">Il est possible que vous toocreate une application vide et ensuite créer dynamiquement toutes les instances de service, la plupart des applications dispose un ensemble de services principaux qui doit toujours être créé lors de l’application hello est instanciée.</span><span class="sxs-lookup"><span data-stu-id="a27d4-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="a27d4-120">Il s’agit tooas référencé « services par défaut ».</span><span class="sxs-lookup"><span data-stu-id="a27d4-120">These are referred tooas "default services".</span></span> <span data-ttu-id="a27d4-121">Ils sont spécifiés dans le manifeste de l’application hello, avec des espaces réservés pour la configuration per-environnement inclus entre crochets :</span><span class="sxs-lookup"><span data-stu-id="a27d4-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="a27d4-122">Chacun des paramètres nommé de hello doit être défini dans l’élément des paramètres hello hello du manifeste d’application :</span><span class="sxs-lookup"><span data-stu-id="a27d4-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="a27d4-123">attribut de DefaultValue Hello spécifie hello toobe de valeur utilisé dans l’absence de hello d’un paramètre plus spécifique pour un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="a27d4-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="a27d4-124">Tous les paramètres d’instance de service conviennent à la configuration par environnement.</span><span class="sxs-lookup"><span data-stu-id="a27d4-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="a27d4-125">Dans l’exemple hello ci-dessus, hello LowKey et HighKey valeurs pour le schéma de partitionnement du service hello sont explicitement définies pour toutes les instances de service de hello, car la plage de partition hello est une fonction de domaine de données hello, pas l’environnement hello.</span><span class="sxs-lookup"><span data-stu-id="a27d4-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="a27d4-126">Paramètres de configuration de service par environnement</span><span class="sxs-lookup"><span data-stu-id="a27d4-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="a27d4-127">Hello [modèle d’application Service Fabric](service-fabric-application-model.md) tooinclude les packages de configuration qui contiennent des paires clé-valeur personnalisées qui peuvent être lus au moment de l’exécution des services Active.</span><span class="sxs-lookup"><span data-stu-id="a27d4-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="a27d4-128">valeurs Hello de ces paramètres peuvent également être différenciées par l’environnement en spécifiant un `ConfigOverride` dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a27d4-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="a27d4-129">Supposons que vous ayez hello suivant paramètre dans le fichier de Config\Settings.xml hello pour hello `Stateful1` service :</span><span class="sxs-lookup"><span data-stu-id="a27d4-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="a27d4-130">Création de cette valeur pour une paire d’application/environnement spécifique, toooverride un `ConfigOverride` lorsque vous importez le manifeste de service hello dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a27d4-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="a27d4-131">Ce paramètre peut ensuite être configuré par environnement, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a27d4-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="a27d4-132">Vous pouvez le faire en déclarant dans la section Paramètres de hello hello du manifeste d’application et en spécifiant des valeurs spécifiques à l’environnement dans les fichiers de paramètres d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a27d4-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="a27d4-133">Dans les cas de hello des paramètres de configuration de service, il existe trois emplacements où hello d’une clé peut avoir la valeur : package de configuration du service hello, manifeste de l’application hello et fichier de paramètres d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a27d4-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="a27d4-134">L’infrastructure de service seront toujours choisir à partir du fichier de paramètres d’application hello tout d’abord (si spécifié), hello du manifeste d’application, puis enfin hello package de configuration.</span><span class="sxs-lookup"><span data-stu-id="a27d4-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="a27d4-135">Définition et utilisation des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="a27d4-135">Setting and using environment variables</span></span> 
<span data-ttu-id="a27d4-136">Vous pouvez spécifier et définir des variables d’environnement dans le fichier ServiceManifest.xml de hello et ensuite substituer ces éléments dans le fichier ApplicationManifest.xml de hello sur chaque instance.</span><span class="sxs-lookup"><span data-stu-id="a27d4-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="a27d4-137">exemple Hello ci-dessous montre les deux variables d’environnement, une avec une valeur définie et hello autres est remplacé.</span><span class="sxs-lookup"><span data-stu-id="a27d4-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="a27d4-138">Vous pouvez utiliser les paramètres de valeurs de variables d’environnement tooset Bonjour même façon que ces ont été utilisés pour les remplacements de configuration d’application.</span><span class="sxs-lookup"><span data-stu-id="a27d4-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="a27d4-139">variables d’environnement toooverride hello Bonjour ApplicationManifest.xml, package de code hello référence Bonjour ServiceManifest avec hello `EnvironmentOverrides` élément.</span><span class="sxs-lookup"><span data-stu-id="a27d4-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="a27d4-140">Une fois hello nommé l’instance de service est créé, vous pouvez accéder variables d’environnement hello à partir du code.</span><span class="sxs-lookup"><span data-stu-id="a27d4-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="a27d4-141">par exemple, en c# vous pouvez effectuer suivant de hello</span><span class="sxs-lookup"><span data-stu-id="a27d4-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="a27d4-142">Variables d’environnement de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a27d4-142">Service Fabric environment variables</span></span>
<span data-ttu-id="a27d4-143">Des variables d’environnement définies pour chaque instance de service sont intégrées à Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a27d4-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="a27d4-144">Hello la liste complète des variables d’environnement est ci-dessous, où hello celles en gras sont hello ceux que vous utiliserez dans votre service, hello autre étant utilisé par le runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a27d4-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="a27d4-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="a27d4-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="a27d4-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="a27d4-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="a27d4-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="a27d4-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="a27d4-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="a27d4-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="a27d4-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="a27d4-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="a27d4-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="a27d4-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="a27d4-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="a27d4-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="a27d4-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="a27d4-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="a27d4-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="a27d4-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="a27d4-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="a27d4-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="a27d4-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="a27d4-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="a27d4-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="a27d4-156">Fabric_NodeId</span></span>
* <span data-ttu-id="a27d4-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="a27d4-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="a27d4-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="a27d4-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="a27d4-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="a27d4-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="a27d4-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="a27d4-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="a27d4-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="a27d4-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="a27d4-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="a27d4-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="a27d4-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="a27d4-163">FabricPackageFileName</span></span>

<span data-ttu-id="a27d4-164">Hello code belows montre comment toolist hello variables d’environnement Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a27d4-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="a27d4-165">Hello ci-dessous des exemples de variables d’environnement pour un type d’application appelé `GuestExe.Application` avec un type de service appelé `FrontEndService` sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="a27d4-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="a27d4-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="a27d4-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="a27d4-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="a27d4-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="a27d4-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="a27d4-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="a27d4-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="a27d4-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="a27d4-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="a27d4-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="a27d4-171">Fichiers de paramètre d’application</span><span class="sxs-lookup"><span data-stu-id="a27d4-171">Application parameter files</span></span>
<span data-ttu-id="a27d4-172">projet d’application Service Fabric Hello peut inclure un ou plusieurs fichiers de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="a27d4-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="a27d4-173">Chacun d’eux définit des valeurs spécifiques hello pour les paramètres hello qui sont définis dans le manifeste de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="a27d4-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="a27d4-174">Par défaut, une nouvelle application contient trois fichiers de paramètres, nommés Local.1Node.xml, Local.5Node.xml et Cloud.xml :</span><span class="sxs-lookup"><span data-stu-id="a27d4-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Fichiers de paramètres d’application dans l’Explorateur de solutions][app-parameters-solution-explorer]

<span data-ttu-id="a27d4-176">toocreate un fichier de paramètres, simplement copier et coller un et lui donner un nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="a27d4-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="a27d4-177">Identification des paramètres spécifiques à l’environnement au cours du déploiement</span><span class="sxs-lookup"><span data-stu-id="a27d4-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="a27d4-178">Au moment du déploiement, vous devez tooapply de fichier toochoose hello paramètre approprié à votre application.</span><span class="sxs-lookup"><span data-stu-id="a27d4-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="a27d4-179">Vous pouvez le faire via la boîte de dialogue Publier hello dans Visual Studio ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a27d4-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="a27d4-180">Déploiement depuis Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a27d4-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="a27d4-181">Lorsque vous publiez votre application dans Visual Studio, vous pouvez choisir à partir de la liste de hello des fichiers de paramètres disponibles.</span><span class="sxs-lookup"><span data-stu-id="a27d4-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Choisissez un fichier de paramètres dans la boîte de dialogue Publier hello][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="a27d4-183">Déploiement depuis PowerShell</span><span class="sxs-lookup"><span data-stu-id="a27d4-183">Deploy from PowerShell</span></span>
<span data-ttu-id="a27d4-184">Hello `Deploy-FabricApplication.ps1` script PowerShell inclus dans le modèle de projet application hello accepte un profil de publication en tant que paramètre et hello PublishProfile contient un fichier de paramètres de référence toohello application.</span><span class="sxs-lookup"><span data-stu-id="a27d4-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="a27d4-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a27d4-185">Next steps</span></span>
<span data-ttu-id="a27d4-186">toolearn savoir plus sur certains concepts fondamentaux hello qui sont décrites dans cette rubrique, consultez hello [vue d’ensemble technique du Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a27d4-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="a27d4-187">Pour plus d’informations sur les autres fonctionnalités de gestion d’application disponibles dans Visual Studio, consultez la section [Gestion de vos applications de Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="a27d4-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
