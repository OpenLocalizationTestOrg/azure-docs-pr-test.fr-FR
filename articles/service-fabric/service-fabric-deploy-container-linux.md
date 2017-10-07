---
title: "aaaService l’ensemble fibre optique et déployer des conteneurs dans Linux | Documents Microsoft"
description: "Service Fabric et hello utilisent les applications Linux conteneurs toodeploy microservice. Cet article décrit les fonctions hello offrant des conteneurs et comment toodeploy un conteneur Linux de l’image dans un cluster Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Déployer un tooService de conteneur Linux l’ensemble fibre optique
> [!div class="op_single_selector"]
> * [Déployer un conteneur Windows](service-fabric-deploy-container.md)
> * [Déployer un conteneur Linux](service-fabric-deploy-container-linux.md)
>
>

Cet article vous guide dans le processus de création des services en conteneur sous Linux.

Service Fabric dispose de plusieurs fonctionnalités de gestion des conteneurs, qui vous aident à créer des applications composées de microservices mis en conteneur. On parle alors de services en conteneur.

incluent les fonctionnalités de Hello ;

* Activation et déploiement d’images de conteneur
* Gouvernance des ressources
* Authentification de référentiels
* Mappage de port de port du conteneur toohost
* Découverte et communication entre des conteneurs
* Capacité tooconfigure et définir des variables d’environnement

## <a name="packaging-a-docker-container-with-yeoman"></a>Empaquetage d’un conteneur Docker avec Yeoman
Lors de l’empaquetage d’un conteneur sur Linux, vous pouvez choisir soit toouse un modèle yeoman ou [créer le package d’application hello manuellement](#manually).

Une application de Service Fabric peut contenir un ou plusieurs conteneurs, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise. Hello SDK de l’infrastructure de Service pour Linux comprend un [Yeoman](http://yeoman.io/) générateur qui rend toocreate facilement votre application et ajouter une image de conteneur. Nous allons utiliser Yeoman toocreate appelée par une application avec un seul conteneur Docker *SimpleContainerApp*. Vous pouvez ajouter davantage de services ultérieurement en modifiant les fichiers manifeste hello généré.

## <a name="install-docker-on-your-development-box"></a>Installer Docker dans votre espace de développement

Suivante d’exécution hello commandes docker tooinstall dans votre boîte de développement Linux (si vous utilisez une image de vagrant hello sur OSX, docker est déjà installé) :

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Créer l’application hello
1. Saisissez `yo azuresfcontainer` dans un terminal.
2. Nommez votre application, par exemple, mycontainerap
3. Indiquez les URL de hello pour l’image de conteneur hello à partir d’un référentiel de docker Hub. Hello image paramètre prend hello formulaire [référentiel] / [nom de l’image]
4. Si les images hello n’ont pas d’un charge de travail-point d’entrée défini, vous devez tooexplicitly spécifier des commandes d’entrée avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur hello, qui conserve conteneur hello en cours d’exécution après le démarrage.

![Générateur Yeoman Service Fabric pour les conteneurs][sf-yeoman]

## <a name="deploy-hello-application"></a>Déployer l’application hello

### <a name="using-xplat-cli"></a>Utilisation de l’interface de ligne de commande XPlat
Une fois que l’application hello est générée, vous pouvez la déployer toohello cluster local à l’aide de hello CLI d’Azure.

1. Connectez le cluster Service Fabric local de toohello.

    ```bash
    azure servicefabric cluster connect
    ```

2. Hello d’utilisation script d’installation fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.

    ```bash
    ./install.sh
    ```

3. Ouvrez un navigateur et accédez tooService Fabric Explorer dans http://localhost:19080/Explorateur (remplacer localhost avec adresse IP privée hello Hello machine virtuelle si vous utilisez Vagrant sur Mac OS X).
4. Développez le nœud Applications de hello et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.
5. Utiliser un script de désinstallation hello fournies dans l’instance de l’application hello modèle toodelete hello et annuler l’inscription du type de l’application hello.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Avec Azure CLI 2.0

Consultez la documentation de référence hello sur la gestion un [à l’aide du cycle de vie application hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Pour un exemple d’application, [hello d’extraction code conteneur de Service Fabric exemples sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Ajout d’application existante de plusieurs services tooan

application tooan déjà créée à l’aide du service un autre conteneur tooadd `yo`, effectuer hello comme suit :

1. Modifier la racine toohello du répertoire d’application existant hello.  Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.
2. Exécutez `yo azuresfcontainer:AddService`.

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

Vous pouvez fournir des commandes d’entrée en spécifiant hello facultatif `Commands` élément avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur de hello.

> [!NOTE]
> Si les images hello n’ont pas d’un charge de travail-point d’entrée défini, vous devez tooexplicitly spécifier des commandes d’entrée à l’intérieur de `Commands` élément avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur de hello, qui conserve conteneur hello en cours d’exécution démarrage.

## <a name="understand-resource-governance"></a>Présentation de la gouvernance des ressources
Gouvernance des ressources sont une fonctionnalité de conteneur hello qui limite les ressources hello hello conteneur peut utiliser sur l’ordinateur hôte de hello. Hello `ResourceGovernancePolicy`, qui est spécifiée dans le manifeste de l’application hello est toodeclare utilisé des limites de ressources pour un package de code de service. Les limites de ressources peuvent être définies pour hello suivant des ressources :

* Mémoire
* MemorySwap
* CpuShares (pondération relative à l’UC)
* MemoryReservationInMB  
* BlkioWeight (poids relatif de l’élément BlockIO)

> [!NOTE]
> Dans une version ultérieure, il sera possible de prendre en charge la spécification de limites relatives aux E/S en mode bloc précises (E/S par seconde, bits par seconde en lecture/écriture...).
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

## <a name="configure-container-port-to-host-port-mapping"></a>Configuration du mappage des ports de conteneur aux ports hôtes
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
À l’aide de hello `PortBinding` stratégie, vous pouvez mapper un port du conteneur de tooan `Endpoint` dans le manifeste de service hello. point de terminaison de Hello `Endpoint1` peut spécifier un port fixe (par exemple, le port 80). Il ne peut également spécifier aucun port, auquel cas un port aléatoire à partir de la plage de ports d’application du cluster hello est choisi pour vous.

Si vous spécifiez un point de terminaison, à l’aide de hello `Endpoint` balise dans le manifeste de service hello d’un conteneur d’invité, l’infrastructure de Service peut publier automatiquement cette toohello de point de terminaison service de noms. Autres services qui s’exécutent dans un cluster de hello peuvent découvrir donc ce conteneur à l’aide de requêtes REST hello pour la résolution.

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

En inscrivant avec hello Naming service, facilement faire communication de conteneur à l’autre dans le code hello dans votre conteneur, à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md). Communication est effectuée en fournissant le port d’écoute http proxy inverse hello et nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement. Pour plus d’informations, consultez la section suivante de hello.

## <a name="configure-and-set-environment-variables"></a>Configurer et définir des variables d’environnement
Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello, à la fois pour les services qui sont déployés dans des conteneurs ou pour les services qui sont déployées sous forme de fichiers exécutables du processus/invité. Ces valeurs de variable d’environnement peuvent être substituées en particulier dans le manifeste de l’application hello ou spécifiés pendant le déploiement en tant que paramètres de l’application.

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
* [Interaction avec les clusters de l’infrastructure de Service à l’aide de hello CLI d’Azure](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Articles connexes

* [Prise en main de Service Fabric et d’Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Prise en main de l’interface de ligne de commande Service Fabric XPlat)
