---
title: "aaaService l’infrastructure et le déploiement de conteneurs | Documents Microsoft"
description: "Service Fabric et hello utilisent des applications de conteneurs toodeploy microservice. Cet article décrit les fonctionnalités de hello Service Fabric fournit des conteneurs et comment toodeploy un conteneur Windows de l’image dans un cluster."
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
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Déployer un tooService de conteneur Windows Fabric
> [!div class="op_single_selector"]
> * [Déployer un conteneur Windows](service-fabric-deploy-container.md)
> * [Déployer un conteneur Docker](service-fabric-deploy-container-linux.md)
> 
> 

Cet article vous guide tout au long des processus hello de création des services dans les conteneurs Windows.

Service Fabric dispose de plusieurs fonctionnalités qui vous aident à créer des applications composées de microservices exécutés dans des conteneurs. 

les fonctions Hello incluent :

* Activation et déploiement d’images de conteneur
* Gouvernance des ressources
* Authentification de référentiels
* Mappage des ports de conteneur aux ports hôtes
* Découverte et communication entre des conteneurs
* Capacité tooconfigure et définir des variables d’environnement

Examinons chacune des fonctions fonctionne lorsque vous créez un package une toobe en conteneur service inclus dans votre application.

## <a name="package-a-windows-container"></a>Empaquetage d’un conteneur Windows
Quand vous créez le package un conteneur, vous pouvez choisir toouse un modèle de projet Visual Studio ou [créer le package d’application hello manuellement](#manually).  Lorsque vous utilisez Visual Studio, structure de package d’application hello et fichiers manifestes sont créés par le modèle de projet hello pour vous.

> [!TIP]
> toopackage de façon plus simple Hello une image de conteneur existant dans un service est toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Utilisez Visual Studio toopackage une image de conteneur existant
Visual Studio fournit une infrastructure de Service toohelp de modèle de service vous déployez un cluster Service Fabric de tooa conteneur.

1. Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.
2. Choisissez **invité conteneur** en tant que modèle de service hello.
3. Choisissez **nom de l’Image** et fournir hello chemin d’accès toohello image dans votre référentiel de conteneur. Par exemple, `myrepo/myimage:v1` dans https://hub.docker.com
4. Donnez un nom à votre service et cliquez sur **OK**.
5. Si votre service en conteneur a besoin d’un point de terminaison pour la communication, vous pouvez maintenant ajouter hello protocole, port et fichier de type toohello ServiceManifest.xml. Par exemple : 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    En fournissant hello `UriScheme`, Service Fabric inscrit automatiquement le point de terminaison de conteneur hello avec hello service d’affectation de noms pour la fonctionnalité de découverte. port de Hello peut être résolu (comme indiqué dans le précédent exemple de hello) ou allouée dynamiquement. Si vous ne spécifiez pas un port, il est attribué dynamiquement à partir de la plage de ports d’application hello (comme avec n’importe quel service).
    Vous devez également le mappage port toohost tooconfigure hello conteneur en spécifiant un `PortBinding` stratégie dans le manifeste de l’application hello. Pour plus d’informations, consultez [configurer le mappage de port de conteneur toohost](#Portsection).
6. Si votre conteneur a besoin de gouvernance des ressources, ajoutez un `ResourceGovernancePolicy`.
8. Si votre conteneur doit tooauthenticate avec un référentiel privé, puis ajoutez `RepositoryCredentials`.
7. Si vous exécutez sur un ordinateur Windows Server 2016 avec prise en charge du conteneur activée, vous pouvez utiliser le package de hello et cluster local du tooyour toodeploy action de publication. 
8. Lorsque vous êtes prêt, vous pouvez publier le cluster de l’application hello tooa à distance ou archiver hello solution toosource contrôle. 

Pour obtenir un exemple hello d’extraction [exemples de code de conteneur de Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Création d’un cluster Windows Server 2016
toodeploy votre application en conteneur, vous devez toocreate un cluster exécutant Windows Server 2016 avec prise en charge du conteneur est activé. Votre cluster peut s’exécuter localement ou être déployé via Azure Resource Manager dans Azure. 

toodeploy un cluster à l’aide du Gestionnaire de ressources Azure, choisissez hello **Windows Server 2016 avec des conteneurs** option dans Azure de l’image. Consultez l’article hello [créer un cluster Service Fabric à l’aide du Gestionnaire de ressources Azure](service-fabric-cluster-creation-via-arm.md). Assurez-vous que vous utilisez hello suivant les paramètres du Gestionnaire de ressources Azure :

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Vous pouvez également utiliser hello [modèle cinq nœuds Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un cluster. Vous pouvez également lire [l’article de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la communauté sur l’utilisation des conteneurs de Service Fabric et Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Empaquetage et déploiement manuel d’une image de conteneur
processus Hello d’empaquetage manuel d’un service en conteneur est basée sur hello comme suit :

1. Publier hello conteneurs tooyour référentiel.
2. Créer la structure de répertoire du package hello.
3. Modifiez le fichier de manifeste de service hello.
4. Modifier le fichier manifeste d’application hello.

## <a name="deploy-and-activate-a-container-image"></a>Déploiement et activation d’une image de conteneur
Bonjour Service Fabric [modèle d’application](service-fabric-application-model.md), un conteneur représente un hôte d’application dans le service de plusieurs réplicas sont placés. toodeploy et activer un conteneur, le nom hello put de l’image de conteneur hello dans un `ContainerHost` élément dans le manifeste de service hello.

Dans le manifeste de service hello, ajoutez un `ContainerHost` hello point d’entrée. Puis ensemble hello `ImageName` nom de hello toobe de référentiel de conteneurs hello et image. Hello manifeste partielle suivante montre un exemple de comment le conteneur de hello toodeploy appelée `myimage:v1` à partir d’un référentiel appelé `myrepo`:

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

Vous pouvez spécifier toorun commandes facultatives au démarrage du conteneur hello sous hello `Commands` élément. Si vous avez plusieurs commandes, séparez-les par des virgules. 

## <a name="understand-resource-governance"></a>Présentation de la gouvernance des ressources
Gouvernance des ressources sont une fonctionnalité de conteneur hello qui limite les ressources hello hello conteneur peut utiliser sur l’ordinateur hôte de hello. Hello `ResourceGovernancePolicy`, qui est spécifiée dans le manifeste de l’application hello est toodeclare utilisé des limites de ressources pour un package de code de service. Les limites de ressources peuvent être définies pour hello suivant des ressources :

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
toodownload un conteneur, vous pouvez avoir référentiel de conteneurs toohello tooprovide informations de connexion. Hello informations de connexion, spécifiées dans le manifeste de l’application hello sont utilisées toospecify hello connectez-vous plus d’informations ou d’une clé SSH pour télécharger l’image de conteneur hello hello référentiel d’images. Hello suivant montre un compte appelé *TestUser* , ainsi que le mot de passe hello en texte clair (*pas* recommandé) :

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

Nous vous conseillons de chiffrer un mot de passe hello à l’aide d’un certificat qui a déployé toohello machine.

Hello suivant montre un compte appelé *TestUser*, où le mot de passe hello a été chiffré à l’aide d’un certificat appelé *MonCert*. Vous pouvez utiliser hello `Invoke-ServiceFabricEncryptText` texte PowerShell commande toocreate hello secrète de chiffrement de mot de passe hello. Pour plus d’informations, voir l’article hello [la gestion des clés secrètes dans les applications de Service Fabric](service-fabric-application-secret-management.md).

clé privée de Hello du certificat hello qui a utilisé un mot de passe toodecrypt hello doit être déployé toohello la machine locale dans une méthode hors-bande. (dans Azure, cette méthode est Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package toohello ordinateur hello service, il peut déchiffrer un secret de hello. À l’aide de secret hello avec le nom de compte hello, il peut authentifier puis avec le référentiel de conteneurs hello.

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

## <a name ="Portsection"></a>Configurer le mappage de port de conteneur toohost
Vous pouvez configurer un toocommunicate de port utilisé hôte avec le conteneur de hello en spécifiant un `PortBinding` dans le manifeste de l’application hello. Hello port liaison maps hello port toowhich hello service est à l’écoute à l’intérieur de hello conteneur tooa port sur l’ordinateur hôte de hello.

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
Vous pouvez utiliser hello `PortBinding` élément toomap un point de terminaison tooan port du conteneur dans le manifeste de service hello. Dans l’exemple suivant de hello, hello le point de terminaison `Endpoint1` spécifie un port fixe, 8905. Il ne peut également spécifier aucun port, auquel cas un port aléatoire à partir de la plage de ports d’application du cluster hello est choisi pour vous.


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
Si vous spécifiez un point de terminaison, à l’aide de hello `Endpoint` balise dans le manifeste de service hello d’un conteneur d’invité, l’infrastructure de Service peut publier automatiquement cette toohello de point de terminaison service de noms. Autres services qui s’exécutent dans un cluster de hello peuvent découvrir donc ce conteneur à l’aide de requêtes REST hello pour la résolution.

En inscrivant avec hello Naming service, vous pouvez effectuer communication de conteneur à l’autre au sein de votre conteneur à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md). Communication est effectuée en fournissant le port d’écoute http proxy inverse hello et nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement. Pour plus d’informations, consultez la section suivante de hello. 

## <a name="configure-and-set-environment-variables"></a>Configurer et définir des variables d’environnement
Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello. Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités. Vous pouvez remplacer la variable d’environnement valeurs dans une application hello manifeste ou spécifient durant le déploiement en tant que paramètres de l’application.

Hello service manifeste XML extrait de code suivant illustre un exemple de variables d’environnement toospecify pour un package de code :

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

Ces variables d’environnement peuvent être remplacées au niveau hello du manifeste de l’application :

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Dans l’exemple précédent de hello, que nous avons spécifié une valeur explicite pour hello `HttpGateway` variable d’environnement (19000) pendant la valeur hello pour `BackendServiceName` paramètre via hello `[BackendSvc]` paramètre d’application. Ces paramètres vous permettent de valeur hello toospecify `BackendServiceName`valeur lorsque vous déployez l’application hello et n’avez pas de valeur fixe dans le manifeste de hello.

## <a name="configure-isolation-mode"></a>Configurer le mode d’isolation

Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.  Avec le mode d’isolation du processus de hello, en cours d’exécution tous les conteneurs de hello hello même hôte ordinateur partage hello du noyau avec l’hôte de hello. Avec le mode d’isolation hello Hyper-V, les noyaux hello sont isolées entre chaque conteneur Hyper-V et l’hôte de conteneur hello. le mode d’isolation Hello est spécifié dans hello `ContainerHostPolicies` balise dans le fichier manifeste d’application hello.  modes d’isolation Hello qui peuvent être spécifiées sont `process`, `hyperv`, et `default`. Hello `default` mode d’isolation par défaut est trop`process` sur Windows Server héberge et la valeur par défaut est trop`hyperv` sur des hôtes Windows 10.  Hello extrait de code suivant montre comment le mode d’isolation hello est défini dans le fichier manifeste d’application hello.

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

Un exemple de manifeste de service (spécifié dans hello précédant le manifeste d’application) suivante :

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
Maintenant que vous avez déployé un service en conteneur, découvrez comment toomanage son cycle de vie en lisant [cycle de vie de l’infrastructure de Service application](service-fabric-application-lifecycle.md).

* [Vue d’ensemble de Service Fabric et des conteneurs](service-fabric-containers-overview.md)
* Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
