---
title: "aaaHow toocontainerize votre microservices Azure Service Fabric (version préliminaire)"
description: "Azure Service Fabric a ajouté de nouvelles fonctionnalités toocontainerize votre microservices Service Fabric. Actuellement, cette fonctionnalité est uniquement disponible en tant que version préliminaire."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="29571-104">Comment toocontainerize votre fiable de l’infrastructure de Service Services et Reliable Actors (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="29571-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="29571-105">Service Fabric prend en charge la conteneurisation des microservices Service Fabric (services basés sur Reliable Services et Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="29571-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="29571-106">Pour en savoir plus, voir [Service Fabric et conteneurs](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29571-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="29571-107">Cette fonctionnalité est en version préliminaire et cet article fournit hello différentes étapes tooget votre service en cours d’exécution à l’intérieur d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="29571-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="29571-108">Cette fonctionnalité est disponible en préversion et n’est pas prise en charge dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="29571-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="29571-109">Actuellement, cette fonctionnalité fonctionne uniquement pour Windows.</span><span class="sxs-lookup"><span data-stu-id="29571-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="29571-110">Les étapes toocontainerize votre Application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29571-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="29571-111">Ouvrez l’application Service Fabric dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29571-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="29571-112">Ajouter une classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="29571-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="29571-113">code Hello dans cette classe est une application d’assistance toocorrectly charge hello Service Fabric runtime fichiers binaires à l’intérieur de votre application lors de l’exécution à l’intérieur d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="29571-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="29571-114">Pour chaque package de code vous aimeriez toocontainerize, l’initialisation du chargeur de hello au point d’entrée de programme de hello.</span><span class="sxs-lookup"><span data-stu-id="29571-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="29571-115">Ajoutez le constructeur statique de hello indiqué dans le fichier de point d’entrée de code extrait tooyour programme suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="29571-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="29571-116">Générez et [créez un package](service-fabric-package-apps.md#Package-App) de votre projet.</span><span class="sxs-lookup"><span data-stu-id="29571-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="29571-117">toobuild et créer un package, cliquez sur le projet d’application hello dans l’Explorateur de solutions et choisissez hello **Package** commande.</span><span class="sxs-lookup"><span data-stu-id="29571-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="29571-118">Pour chaque package de code, vous devez toocontainerize, hello exécution script PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="29571-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="29571-119">l’utilisation de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="29571-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="29571-120">script de Hello crée un dossier avec des artefacts de Docker à $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="29571-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="29571-121">Modifier hello généré Dockerfile tooexpose tous les ports, exécuter le programme d’installation des scripts etc. selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29571-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="29571-122">Vous devez ensuite trop[générer](service-fabric-get-started-containers.md#Build-Containers) et [push](service-fabric-get-started-containers.md#Push-Containers) votre référentiel de tooyour de package de conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="29571-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="29571-123">Modifier hello ApplicationManifest.xml et ServiceManifest.xml tooadd votre image de conteneur, les informations de référentiel, Registre d’authentification et le mappage de port et l’hôte.</span><span class="sxs-lookup"><span data-stu-id="29571-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="29571-124">Pour modifier les manifestes hello, consultez [créer une application de conteneur Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="29571-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="29571-125">définition du package de code Hello dans hello service besoins manifeste toobe est remplacé par l’image de conteneur correspondant.</span><span class="sxs-lookup"><span data-stu-id="29571-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="29571-126">Assurez-vous que toochange hello EntryPoint tooa ContainerHost type.</span><span class="sxs-lookup"><span data-stu-id="29571-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="29571-127">Ajouter un mappage de port et l’hôte de hello pour votre réplicateur et le point de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="29571-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="29571-128">Étant donné que les deux de ces ports est affectées lors de l’exécution par l’infrastructure de Service, hello ContainerPort a la valeur toozero toouse hello est affecté de port pour le mappage.</span><span class="sxs-lookup"><span data-stu-id="29571-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="29571-129">tootest cette application, vous devez toodeploy il tooa cluster qui exécute la version 5.7 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="29571-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="29571-130">En outre, vous devez tooedit et mettre à jour tooenable de paramètres de cluster hello cette fonctionnalité en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="29571-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="29571-131">Suivez les étapes de hello dans ce [article](service-fabric-cluster-fabric-settings.md) paramètre hello de tooadd montre l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="29571-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="29571-132">Suivant [déployer](service-fabric-deploy-remove-applications.md) hello modifié cluster toothis de package application.</span><span class="sxs-lookup"><span data-stu-id="29571-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="29571-133">Vous devez maintenant disposer d’une application Service Fabric en conteneur exécutant votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29571-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29571-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29571-134">Next steps</span></span>
* <span data-ttu-id="29571-135">En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="29571-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="29571-136">En savoir plus sur hello Service Fabric [cycle de vie des applications](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="29571-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
