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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Comment toocontainerize votre fiable de l’infrastructure de Service Services et Reliable Actors (version préliminaire)

Service Fabric prend en charge la conteneurisation des microservices Service Fabric (services basés sur Reliable Services et Reliable Actors). Pour en savoir plus, voir [Service Fabric et conteneurs](service-fabric-containers-overview.md).


 Cette fonctionnalité est en version préliminaire et cet article fournit hello différentes étapes tooget votre service en cours d’exécution à l’intérieur d’un conteneur.  

> [!NOTE]
> Cette fonctionnalité est disponible en préversion et n’est pas prise en charge dans les environnements de production. Actuellement, cette fonctionnalité fonctionne uniquement pour Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Les étapes toocontainerize votre Application Service Fabric

1. Ouvrez l’application Service Fabric dans Visual Studio.

2. Ajouter une classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projet. code Hello dans cette classe est une application d’assistance toocorrectly charge hello Service Fabric runtime fichiers binaires à l’intérieur de votre application lors de l’exécution à l’intérieur d’un conteneur.

3. Pour chaque package de code vous aimeriez toocontainerize, l’initialisation du chargeur de hello au point d’entrée de programme de hello. Ajoutez le constructeur statique de hello indiqué dans le fichier de point d’entrée de code extrait tooyour programme suivant de hello.

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

4. Générez et [créez un package](service-fabric-package-apps.md#Package-App) de votre projet. toobuild et créer un package, cliquez sur le projet d’application hello dans l’Explorateur de solutions et choisissez hello **Package** commande.

5. Pour chaque package de code, vous devez toocontainerize, hello exécution script PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). l’utilisation de Hello est comme suit :
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  script de Hello crée un dossier avec des artefacts de Docker à $dockerPackageOutputDirectoryPath. Modifier hello généré Dockerfile tooexpose tous les ports, exécuter le programme d’installation des scripts etc. selon vos besoins.

6. Vous devez ensuite trop[générer](service-fabric-get-started-containers.md#Build-Containers) et [push](service-fabric-get-started-containers.md#Push-Containers) votre référentiel de tooyour de package de conteneur Docker.

7. Modifier hello ApplicationManifest.xml et ServiceManifest.xml tooadd votre image de conteneur, les informations de référentiel, Registre d’authentification et le mappage de port et l’hôte. Pour modifier les manifestes hello, consultez [créer une application de conteneur Azure Service Fabric](service-fabric-get-started-containers.md). définition du package de code Hello dans hello service besoins manifeste toobe est remplacé par l’image de conteneur correspondant. Assurez-vous que toochange hello EntryPoint tooa ContainerHost type.

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

8. Ajouter un mappage de port et l’hôte de hello pour votre réplicateur et le point de terminaison de service. Étant donné que les deux de ces ports est affectées lors de l’exécution par l’infrastructure de Service, hello ContainerPort a la valeur toozero toouse hello est affecté de port pour le mappage.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest cette application, vous devez toodeploy il tooa cluster qui exécute la version 5.7 ou une version ultérieure. En outre, vous devez tooedit et mettre à jour tooenable de paramètres de cluster hello cette fonctionnalité en version préliminaire. Suivez les étapes de hello dans ce [article](service-fabric-cluster-fabric-settings.md) paramètre hello de tooadd montre l’illustration suivante.
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
10. Suivant [déployer](service-fabric-deploy-remove-applications.md) hello modifié cluster toothis de package application.

Vous devez maintenant disposer d’une application Service Fabric en conteneur exécutant votre cluster.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur l’exécution des [conteneurs sur Service Fabric](service-fabric-get-started-containers.md).
* En savoir plus sur hello Service Fabric [cycle de vie des applications](service-fabric-application-lifecycle.md).
