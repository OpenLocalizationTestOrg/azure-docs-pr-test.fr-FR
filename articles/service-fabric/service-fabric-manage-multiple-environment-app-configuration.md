---
title: "Gérer plusieurs environnements dans Fabric Service | Microsoft Docs"
description: "Les applications Fabric Service peuvent être exécutées sur des clusters comportant entre une machine et des milliers. Dans certains cas, vous devez configurer votre application différemment pour les différents environnements. Cet article explique comment définir des paramètres d’application par l’environnement."
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
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="2f77e-105">Gestion des paramètres d’application pour plusieurs environnements</span><span class="sxs-lookup"><span data-stu-id="2f77e-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="2f77e-106">Vous pouvez créer des clusters Service Fabric comportant n’importe quel nombre d’ordinateurs compris entre un et plusieurs milliers.</span><span class="sxs-lookup"><span data-stu-id="2f77e-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="2f77e-107">Bien que les fichiers binaires d’application puissent s’exécuter sans modification dans ce large éventail d’environnements, vous souhaiterez certainement configurer l’application différemment, selon le nombre d’ordinateurs sur lesquels vous la déployez.</span><span class="sxs-lookup"><span data-stu-id="2f77e-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="2f77e-108">À titre d’exemple, envisagez d’utiliser `InstanceCount` pour un service sans état.</span><span class="sxs-lookup"><span data-stu-id="2f77e-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="2f77e-109">Lorsque vous exécutez des applications dans Azure, vous souhaitez généralement définir ce paramètre sur la valeur spéciale « -1 ».</span><span class="sxs-lookup"><span data-stu-id="2f77e-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="2f77e-110">Cette configuration garantit que votre service s’exécute sur chaque nœud du cluster (ou tous les nœuds du type de nœud, si vous avez défini une contrainte de placement).</span><span class="sxs-lookup"><span data-stu-id="2f77e-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="2f77e-111">Cependant, cette configuration ne convient pas à un cluster à une seule machine, car vous ne disposez pas de plusieurs processus à l’écoute du même point de terminaison sur une seule machine.</span><span class="sxs-lookup"><span data-stu-id="2f77e-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="2f77e-112">Au lieu de cela, vous définissez généralement `InstanceCount` sur « 1 ».</span><span class="sxs-lookup"><span data-stu-id="2f77e-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="2f77e-113">Spécification des paramètres spécifiques à l’environnement</span><span class="sxs-lookup"><span data-stu-id="2f77e-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="2f77e-114">La solution à ce problème de configuration est un ensemble de services paramétrables par défaut et des fichiers de paramètres d’application qui remplissent ces valeurs de paramètre pour un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="2f77e-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="2f77e-115">Les services par défaut et paramètres d’application sont configurés dans les manifestes d’applications et de services.</span><span class="sxs-lookup"><span data-stu-id="2f77e-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="2f77e-116">La définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml est installée avec le Kit de développement logiciel (SDK) Service Fabric et les outils sous *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="2f77e-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="2f77e-117">Services par défaut</span><span class="sxs-lookup"><span data-stu-id="2f77e-117">Default services</span></span>
<span data-ttu-id="2f77e-118">Les applications Service Fabric sont constituées d’une collection d’instances de service.</span><span class="sxs-lookup"><span data-stu-id="2f77e-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="2f77e-119">Bien qu’il vous soit possible de créer une application vide, puis toutes les instances de service de manière dynamique, la plupart des applications possèdent un ensemble de services de base qui doivent être créés systématiquement lors de l’instanciation de l’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="2f77e-120">Ils sont nommés « services par défaut » et</span><span class="sxs-lookup"><span data-stu-id="2f77e-120">These are referred to as "default services".</span></span> <span data-ttu-id="2f77e-121">sont spécifiés dans le manifeste d’application avec des espaces réservés à la configuration par environnement inclus entre crochets :</span><span class="sxs-lookup"><span data-stu-id="2f77e-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="2f77e-122">Chacun des paramètres nommés doit être défini dans l’élément Paramètres du manifeste d’application :</span><span class="sxs-lookup"><span data-stu-id="2f77e-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="2f77e-123">L’attribut DefaultValue spécifie la valeur à utiliser en l’absence d’un paramètre plus spécifique pour un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="2f77e-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="2f77e-124">Tous les paramètres d’instance de service conviennent à la configuration par environnement.</span><span class="sxs-lookup"><span data-stu-id="2f77e-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="2f77e-125">Dans l’exemple ci-dessus, les valeurs LowKey et HighKey du schéma de partitionnement du service sont explicitement définies pour toutes les instances du service dans la mesure où la plage de partition est une fonction du domaine de données et non de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="2f77e-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="2f77e-126">Paramètres de configuration de service par environnement</span><span class="sxs-lookup"><span data-stu-id="2f77e-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="2f77e-127">Le [modèle d’application Service Fabric](service-fabric-application-model.md) permet aux services d’inclure des packages de configuration contenant des paires clé-valeur personnalisées lisibles lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="2f77e-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="2f77e-128">Les valeurs de ces paramètres peuvent également être différenciées par l’environnement en spécifiant un `ConfigOverride` dans le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="2f77e-129">Supposons que vous utilisiez le paramètre suivant dans le fichier Config\Settings.xml pour le service `Stateful1` :</span><span class="sxs-lookup"><span data-stu-id="2f77e-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="2f77e-130">Pour remplacer cette valeur par une paire application/environnement spécifique, créez un `ConfigOverride` lors de l’importation du manifeste de service dans le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

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
<span data-ttu-id="2f77e-131">Ce paramètre peut ensuite être configuré par environnement, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2f77e-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="2f77e-132">Vous pouvez réaliser cette opération par le biais d’une déclaration dans la section Paramètres du manifeste d’application et la spécification des valeurs spécifiques à l’environnement dans les fichiers de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="2f77e-133">Dans le cas de paramètres de configuration de service, il existe trois emplacements où la valeur d’une clé peut être définie : le package de configuration du service, le manifeste d’application et le fichier de paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="2f77e-134">Service Fabric choisira toujours dans le fichier de paramètres d’application en premier (s’il est spécifié), puis le manifeste d’application et enfin, le package de configuration.</span><span class="sxs-lookup"><span data-stu-id="2f77e-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="2f77e-135">Définition et utilisation des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="2f77e-135">Setting and using environment variables</span></span> 
<span data-ttu-id="2f77e-136">Vous pouvez spécifier et définir des variables d’environnement dans le fichier ServiceManifest.xml, puis les remplacer dans le fichier ApplicationManifest.xml instance par instance.</span><span class="sxs-lookup"><span data-stu-id="2f77e-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="2f77e-137">L’exemple suivant montre deux variables d’environnement, une avec un ensemble de valeurs et une autre qui est ignorée.</span><span class="sxs-lookup"><span data-stu-id="2f77e-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="2f77e-138">Vous pouvez utiliser les paramètres d’application pour définir les valeurs des variables d’environnement de la même manière que pour les substitutions de configuration.</span><span class="sxs-lookup"><span data-stu-id="2f77e-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="2f77e-139">Pour remplacer les variables d’environnement dans le fichier ApplicationManifest.xml, faites référence au package de code dans ServiceManifest avec l’élément `EnvironmentOverrides`.</span><span class="sxs-lookup"><span data-stu-id="2f77e-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="2f77e-140">Une fois que l’instance de service nommé est créée, vous pouvez accéder aux variables d’environnement à partir du code.</span><span class="sxs-lookup"><span data-stu-id="2f77e-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="2f77e-141">Par exemple, en C#, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f77e-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="2f77e-142">Variables d’environnement de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f77e-142">Service Fabric environment variables</span></span>
<span data-ttu-id="2f77e-143">Des variables d’environnement définies pour chaque instance de service sont intégrées à Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f77e-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="2f77e-144">Vous trouverez ci-dessous la liste complète des variables d’environnement. Vous pourrez utiliser celles en gras dans votre service, tandis que les autres seront utilisées par le runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f77e-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="2f77e-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="2f77e-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="2f77e-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="2f77e-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="2f77e-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="2f77e-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="2f77e-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="2f77e-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="2f77e-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="2f77e-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="2f77e-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="2f77e-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="2f77e-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="2f77e-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="2f77e-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="2f77e-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="2f77e-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="2f77e-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="2f77e-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="2f77e-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="2f77e-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="2f77e-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="2f77e-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="2f77e-156">Fabric_NodeId</span></span>
* <span data-ttu-id="2f77e-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="2f77e-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="2f77e-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="2f77e-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="2f77e-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="2f77e-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="2f77e-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="2f77e-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="2f77e-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="2f77e-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="2f77e-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="2f77e-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="2f77e-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="2f77e-163">FabricPackageFileName</span></span>

<span data-ttu-id="2f77e-164">Le code ci-dessous montre comment répertorier les variables d’environnement de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f77e-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="2f77e-165">Vous trouverez ci-après un exemple de variables d’environnement pour un type d’application nommé `GuestExe.Application` avec un type de service appelé `FrontEndService` lorsque vous travaillez sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="2f77e-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="2f77e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="2f77e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="2f77e-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="2f77e-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="2f77e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="2f77e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="2f77e-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="2f77e-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="2f77e-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="2f77e-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="2f77e-171">Fichiers de paramètre d’application</span><span class="sxs-lookup"><span data-stu-id="2f77e-171">Application parameter files</span></span>
<span data-ttu-id="2f77e-172">Le projet d’application Service Fabric peut inclure un ou plusieurs fichiers de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="2f77e-173">Chacun d’eux définit les valeurs spécifiques pour les paramètres qui sont définis dans le manifeste d’application :</span><span class="sxs-lookup"><span data-stu-id="2f77e-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

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
<span data-ttu-id="2f77e-174">Par défaut, une nouvelle application contient trois fichiers de paramètres, nommés Local.1Node.xml, Local.5Node.xml et Cloud.xml :</span><span class="sxs-lookup"><span data-stu-id="2f77e-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Fichiers de paramètres d’application dans l’Explorateur de solutions][app-parameters-solution-explorer]

<span data-ttu-id="2f77e-176">Pour créer un fichier de paramètres, il vous suffit de copier et coller un fichier de paramètres existant et de lui donner un nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="2f77e-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="2f77e-177">Identification des paramètres spécifiques à l’environnement au cours du déploiement</span><span class="sxs-lookup"><span data-stu-id="2f77e-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="2f77e-178">Au moment du déploiement, vous devez choisir le fichier de paramètres approprié à utiliser avec votre application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="2f77e-179">Vous pouvez le faire via la boîte de dialogue Publier de Visual Studio ou via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f77e-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="2f77e-180">Déploiement depuis Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f77e-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="2f77e-181">Vous pouvez choisir dans la liste des fichiers de paramètres disponibles lors de la publication de votre application dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f77e-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Choisir un fichier de paramètres dans la boîte de dialogue Publier][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="2f77e-183">Déploiement depuis PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f77e-183">Deploy from PowerShell</span></span>
<span data-ttu-id="2f77e-184">Le script PowerShell `Deploy-FabricApplication.ps1` inclus dans le modèle de projet d’application accepte un profil de publication en tant que paramètre et le profil PublishProfile contient une référence au fichier de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="2f77e-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="2f77e-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f77e-185">Next steps</span></span>
<span data-ttu-id="2f77e-186">Pour en savoir plus sur certains des principaux concepts abordés dans cette rubrique, consultez la [Présentation technique de Fabric Service](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f77e-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="2f77e-187">Pour plus d’informations sur les autres fonctionnalités de gestion d’application disponibles dans Visual Studio, consultez la section [Gestion de vos applications de Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="2f77e-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
