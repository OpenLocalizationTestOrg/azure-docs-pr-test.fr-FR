---
title: "Service Fabric et le déploiement de conteneurs | Microsoft Docs"
description: "Présentation de Service Fabric et de la méthode à suivre pour déployer des applications de microservices au moyen de conteneurs. Cet article décrit les fonctionnalités que Service Fabric offre pour les conteneurs et explique comment déployer une image de conteneur Windows dans un cluster."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a>Déployer un conteneur Windows sur Service Fabric
> [!div class="op_single_selector"]
> * [Déployer un conteneur Windows](service-fabric-deploy-container.md)
> * [Déployer un conteneur Docker](service-fabric-deploy-container-linux.md)
> 
> 

Cet article vous guide dans le processus de création des services dans des conteneurs Windows.

Service Fabric dispose de plusieurs fonctionnalités qui vous aident à créer des applications composées de microservices exécutés dans des conteneurs. 

Ces fonctionnalités sont les suivantes :

* Activation et déploiement d’images de conteneur
* Gouvernance des ressources
* Authentification de référentiels
* Mappage des ports de conteneur aux ports hôtes
* Découverte et communication entre des conteneurs
* Possibilité de configurer et de définir des variables d’environnement

Examinons à présent le fonctionnement de chacune des fonctionnalités lors de l’empaquetage d’un service en conteneur à inclure dans votre application.

## <a name="package-a-windows-container"></a>Empaquetage d’un conteneur Windows
Lors de l’empaquetage d’un conteneur, vous pouvez choisir d’utiliser un modèle de projet Visual Studio ou de [créer le package d’application manuellement](#manually).  Lorsque vous utilisez Visual Studio, la structure de package d’application et les fichiers manifeste sont créés par le modèle de nouveau projet.

> [!TIP]
> Pour empaqueter une image de conteneur existante dans un service, le plus simple consiste à utiliser Visual Studio.

## <a name="use-visual-studio-to-package-an-existing-container-image"></a>Utilisation de Visual Studio pour empaqueter une image de conteneur
Visual Studio fournit un modèle de service Service Fabric pour vous aider à déployer un conteneur sur un cluster Service Fabric.

1. Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.
2. Choisissez **Conteneur d’invités** comme modèle de service.
3. Choisissez **Nom de l’image** et indiquez le chemin d’accès à l’image dans votre référentiel de conteneur. Par exemple, `myrepo/myimage:v1` dans https://hub.docker.com
4. Donnez un nom à votre service et cliquez sur **OK**.
5. Si votre service en conteneur a besoin d’un point de terminaison pour les communications, vous pouvez désormais ajouter le protocole, le port et le type dans le fichier ServiceManifest.xml. Par exemple : 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    En fournissant `UriScheme`, Service Fabric enregistre automatiquement le point de terminaison du conteneur avec le Naming Service pour la découverte. Le port peut être fixe (comme indiqué dans l’exemple précédent) ou alloué de manière dynamique. Si vous ne spécifiez pas de port, il est alloué de manière dynamique à partir de la plage de ports d’application (comme avec n’importe quel service).
    Vous devez également configurer le mappage conteneur/port hôte en spécifiant une stratégie `PortBinding` dans le manifeste d’application. Pour plus d’informations, voir [Configurer le mappage conteneur/port hôte](#Portsection).
6. Si votre conteneur a besoin de gouvernance des ressources, ajoutez un `ResourceGovernancePolicy`.
8. Si votre conteneur doit s’authentifier auprès d’un référentiel privé, ajoutez `RepositoryCredentials`.
7. Si vous utilisez un ordinateur Windows Server 2016 avec prise en charge du conteneur, vous pouvez utiliser le package et publier des actions pour déployer sur votre cluster local. 
8. Vous pouvez, quand vous le souhaitez, publier l’application sur un cluster à distance ou archiver la solution pour contrôler le code source. 

Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Création d’un cluster Windows Server 2016
Pour déployer votre application en conteneur, vous devez créer un cluster exécutant Windows Server 2016 avec la prise en charge du conteneur activée. Votre cluster peut s’exécuter localement ou être déployé via Azure Resource Manager dans Azure. 

Pour déployer un cluster à l’aide d’Azure Resource Manager, choisissez l’option d’image **Windows Server 2016 avec Containers** dans Azure. Consultez l’article [Création d’un cluster Service Fabric dans Azure à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Assurez-vous d’utiliser les paramètres suivants dans Azure Resource Manager :

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Vous pouvez également utiliser le [modèle Azure Resource Manager à cinq nœuds](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) pour créer un cluster. Vous pouvez également lire [l’article de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la communauté sur l’utilisation des conteneurs de Service Fabric et Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Empaquetage et déploiement manuel d’une image de conteneur
Le processus d’empaquetage manuel d’un service avec conteneur est basé sur les étapes suivantes :

1. Publiez les conteneurs dans votre référentiel.
2. Créez la structure de répertoires du package.
3. Modifiez le fichier de manifeste de service.
4. Modifiez le fichier de manifeste d’application.

## <a name="deploy-and-activate-a-container-image"></a>Déploiement et activation d’une image de conteneur
Dans le [modèle d’application](service-fabric-application-model.md)Service Fabric, un conteneur représente un hôte d’application sur lequel sont placés plusieurs réplicas de service. Pour déployer et activer un conteneur, placez le nom de l’image de conteneur dans un élément `ContainerHost` au sein du manifeste de service.

Dans le manifeste de service, ajoutez un `ContainerHost` pour le point d’entrée. Définissez ensuite le nom de référentiel de conteneur et d’image comme `ImageName`. Le manifeste partiel suivant affiche un exemple illustrant le déploiement du conteneur appelé `myimage:v1` depuis un référentiel appelé `myrepo` :

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

Vous pouvez spécifier des commandes facultatives à exécuter lors du démarrage du conteneur sous l’élément `Commands`. Si vous avez plusieurs commandes, séparez-les par des virgules. 

## <a name="understand-resource-governance"></a>Présentation de la gouvernance des ressources
La gouvernance des ressources est une fonctionnalité du conteneur, qui limite les ressources que le conteneur peut utiliser sur l’hôte. L’élément `ResourceGovernancePolicy`, spécifié dans le manifeste de l’application, est utilisé pour déclarer des limites relatives aux ressources pour un package de code de service. Des limites de ressources peuvent être définies pour les ressources suivantes :

* Mémoire
* MemorySwap
* CpuShares (pondération relative à l’UC)
* MemoryReservationInMB  
* BlkioWeight (poids relatif de l’élément BlockIO)

> [!NOTE]
> La prise en charge de la spécification de limites relatives aux E/S en mode bloc précises (E/S par seconde, bits par seconde en lecture/écriture...) est prévue dans une version ultérieure.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Authentification d’un référentiel
Pour télécharger un conteneur, vous devrez peut-être fournir des informations d’identification dans le référentiel du conteneur. Les informations d’identification de connexion spécifiées dans le manifeste de l’application sont utilisées pour spécifier les informations de connexion (ou clé SSH) pour le téléchargement de l’image de conteneur à partir du référentiel d’images. L’exemple suivant utilise un compte appelé *TestUser*, ainsi que le mot de passe en texte clair associé (*non* recommandé) :

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Nous vous recommandons de chiffrer le mot de passe à l’aide d’un certificat qui est déployé sur l’ordinateur.

L’exemple suivant utilise un compte appelé *TestUser* avec un mot de passe chiffré à l’aide d’un certificat nommé *MyCert*. Vous pouvez utiliser la commande PowerShell `Invoke-ServiceFabricEncryptText` pour créer le texte de chiffrement secret du mot de passe. Pour en savoir plus, consultez l’article [Gestion des secrets dans des applications Service Fabric](service-fabric-application-secret-management.md).

La clé privée du certificat utilisée pour déchiffrer le mot de passe doit être déployée sur l’ordinateur local dans une méthode hors bande (dans Azure, cette méthode est Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package de service sur l’ordinateur, il peut déchiffrer la clé secrète. Avec la clé secrète et le nom du compte, il peut ensuite s’authentifier dans le référentiel de conteneur.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a> Configurer le mappage conteneur/port hôte
Vous pouvez configurer un port d’hôte utilisé pour communiquer avec le conteneur en spécifiant un élément `PortBinding` dans le manifeste de l’application. La liaison de port mappe le port sur lequel le service écoute, à l’intérieur du conteneur, à un port sur l’hôte.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Configuration de la découverte et de la communication entre des conteneurs.
Vous pouvez utiliser l’élément `PortBinding` pour mapper un port de conteneur à un point de terminaison dans le manifeste de service. Dans l’exemple suivant, le point de terminaison `Endpoint1` spécifie un port fixe, 8905. Il peut également ne spécifier aucun port, auquel cas un port aléatoire est sélectionné dans la plage de ports des applications du cluster.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Si vous spécifiez un point de terminaison à l’aide de la balise `Endpoint` dans le manifeste de service d’un conteneur invité, Service Fabric peut publier automatiquement ce point de terminaison au Naming Service. D’autres services exécutés dans le cluster peuvent ainsi détecter ce conteneur à l’aide de requêtes REST pour la résolution.

En vous inscrivant auprès du Naming Service, vous pouvez établir des communications entre les conteneurs au sein de votre conteneur à l’aide d’un [proxy inverse](service-fabric-reverseproxy.md). Pour établir la communication, vous devez fournir le port d’écoute HTTP associé au proxy inverse et le nom des services avec lesquels vous souhaitez communiquer en tant que variables d’environnement. Pour en savoir plus, consultez la section suivante. 

## <a name="configure-and-set-environment-variables"></a>Configurer et définir des variables d’environnement
Il est possible de spécifier des variables d’environnement pour chaque package de code dans le manifeste de service. Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités. Vous pouvez remplacer les valeurs de variable d’environnement dans le manifeste de l’application, ou les spécifier lors du déploiement, en tant que paramètres d’application.

L’extrait de code XML du manifeste de service suivant illustre la méthode à suivre pour spécifier des variables d’environnement pour un package de code :

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Ces variables d’environnement peuvent être remplacées au niveau du manifeste de l’application :

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Dans l’exemple ci-dessus, nous avons indiqué une valeur explicite pour la variable d’environnement `HttpGateway` (19000) alors que la valeur du paramètre `BackendServiceName` est définie par le biais du paramètre d’application `[BackendSvc]`. De cette manière, vous pouvez spécifier la valeur de l’élément `BackendServiceName`au moment du déploiement de l’application, sans avoir de valeur fixe dans le manifeste.

## <a name="configure-isolation-mode"></a>Configurer le mode d’isolation

Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.  Avec le mode d’isolation Processus, tous les conteneurs s’exécutant sur le même hôte partagent le noyau avec l’hôte. Avec le mode d’isolation Hyper-V, les noyaux sont isolés entre chaque conteneur Hyper-V et l’hôte du conteneur. Le mode d’isolation est spécifié dans la balise `ContainerHostPolicies` dans le fichier manifeste de l’application.  Les modes d’isolation qui peuvent être définis sont `process`, `hyperv` et `default`. Par défaut, le mode d’isolation `default` est défini sur `process` sur les hôtes Windows Server et sur `hyperv` sur les hôtes Windows 10.  L’extrait de code suivant montre comment le mode d’isolation est spécifié dans le fichier manifeste de l’application.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Exemples complets pour le manifeste de l’application et de service

Voici un exemple de fichier manifeste de l’application :

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Voici un exemple de manifeste de service (indiqué dans le manifeste de l’application ci-dessus) :

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez déployé un service en conteneur, découvrez comment gérer son cycle de vie en lisant [Cycle de vie des applications Service Fabric](service-fabric-application-lifecycle.md).

* [Vue d’ensemble de Service Fabric et des conteneurs](service-fabric-containers-overview.md)
* Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
