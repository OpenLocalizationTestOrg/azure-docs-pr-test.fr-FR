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
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="83760-104">Déployer un tooService de conteneur Linux l’ensemble fibre optique</span><span class="sxs-lookup"><span data-stu-id="83760-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83760-105">Déployer un conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="83760-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="83760-106">Déployer un conteneur Linux</span><span class="sxs-lookup"><span data-stu-id="83760-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="83760-107">Cet article vous guide dans le processus de création des services en conteneur sous Linux.</span><span class="sxs-lookup"><span data-stu-id="83760-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="83760-108">Service Fabric dispose de plusieurs fonctionnalités de gestion des conteneurs, qui vous aident à créer des applications composées de microservices mis en conteneur.</span><span class="sxs-lookup"><span data-stu-id="83760-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="83760-109">On parle alors de services en conteneur.</span><span class="sxs-lookup"><span data-stu-id="83760-109">These services are called containerized services.</span></span>

<span data-ttu-id="83760-110">incluent les fonctionnalités de Hello ;</span><span class="sxs-lookup"><span data-stu-id="83760-110">hello capabilities include;</span></span>

* <span data-ttu-id="83760-111">Activation et déploiement d’images de conteneur</span><span class="sxs-lookup"><span data-stu-id="83760-111">Container image deployment and activation</span></span>
* <span data-ttu-id="83760-112">Gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="83760-112">Resource governance</span></span>
* <span data-ttu-id="83760-113">Authentification de référentiels</span><span class="sxs-lookup"><span data-stu-id="83760-113">Repository authentication</span></span>
* <span data-ttu-id="83760-114">Mappage de port de port du conteneur toohost</span><span class="sxs-lookup"><span data-stu-id="83760-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="83760-115">Découverte et communication entre des conteneurs</span><span class="sxs-lookup"><span data-stu-id="83760-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="83760-116">Capacité tooconfigure et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="83760-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="83760-117">Empaquetage d’un conteneur Docker avec Yeoman</span><span class="sxs-lookup"><span data-stu-id="83760-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="83760-118">Lors de l’empaquetage d’un conteneur sur Linux, vous pouvez choisir soit toouse un modèle yeoman ou [créer le package d’application hello manuellement](#manually).</span><span class="sxs-lookup"><span data-stu-id="83760-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="83760-119">Une application de Service Fabric peut contenir un ou plusieurs conteneurs, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise.</span><span class="sxs-lookup"><span data-stu-id="83760-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="83760-120">Hello SDK de l’infrastructure de Service pour Linux comprend un [Yeoman](http://yeoman.io/) générateur qui rend toocreate facilement votre application et ajouter une image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="83760-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="83760-121">Nous allons utiliser Yeoman toocreate appelée par une application avec un seul conteneur Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="83760-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="83760-122">Vous pouvez ajouter davantage de services ultérieurement en modifiant les fichiers manifeste hello généré.</span><span class="sxs-lookup"><span data-stu-id="83760-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="83760-123">Installer Docker dans votre espace de développement</span><span class="sxs-lookup"><span data-stu-id="83760-123">Install Docker on your development box</span></span>

<span data-ttu-id="83760-124">Suivante d’exécution hello commandes docker tooinstall dans votre boîte de développement Linux (si vous utilisez une image de vagrant hello sur OSX, docker est déjà installé) :</span><span class="sxs-lookup"><span data-stu-id="83760-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="83760-125">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="83760-125">Create hello application</span></span>
1. <span data-ttu-id="83760-126">Saisissez `yo azuresfcontainer` dans un terminal.</span><span class="sxs-lookup"><span data-stu-id="83760-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="83760-127">Nommez votre application, par exemple, mycontainerap</span><span class="sxs-lookup"><span data-stu-id="83760-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="83760-128">Indiquez les URL de hello pour l’image de conteneur hello à partir d’un référentiel de docker Hub.</span><span class="sxs-lookup"><span data-stu-id="83760-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="83760-129">Hello image paramètre prend hello formulaire [référentiel] / [nom de l’image]</span><span class="sxs-lookup"><span data-stu-id="83760-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="83760-130">Si les images hello n’ont pas d’un charge de travail-point d’entrée défini, vous devez tooexplicitly spécifier des commandes d’entrée avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur hello, qui conserve conteneur hello en cours d’exécution après le démarrage.</span><span class="sxs-lookup"><span data-stu-id="83760-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Générateur Yeoman Service Fabric pour les conteneurs][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="83760-132">Déployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="83760-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="83760-133">Utilisation de l’interface de ligne de commande XPlat</span><span class="sxs-lookup"><span data-stu-id="83760-133">Using XPlat CLI</span></span>
<span data-ttu-id="83760-134">Une fois que l’application hello est générée, vous pouvez la déployer toohello cluster local à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="83760-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="83760-135">Connectez le cluster Service Fabric local de toohello.</span><span class="sxs-lookup"><span data-stu-id="83760-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="83760-136">Hello d’utilisation script d’installation fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="83760-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="83760-137">Ouvrez un navigateur et accédez tooService Fabric Explorer dans http://localhost:19080/Explorateur (remplacer localhost avec adresse IP privée hello Hello machine virtuelle si vous utilisez Vagrant sur Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="83760-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="83760-138">Développez le nœud Applications de hello et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="83760-139">Utiliser un script de désinstallation hello fournies dans l’instance de l’application hello modèle toodelete hello et annuler l’inscription du type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="83760-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="83760-140">Avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="83760-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="83760-141">Consultez la documentation de référence hello sur la gestion un [à l’aide du cycle de vie application hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="83760-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="83760-142">Pour un exemple d’application, [hello d’extraction code conteneur de Service Fabric exemples sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="83760-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="83760-143">Ajout d’application existante de plusieurs services tooan</span><span class="sxs-lookup"><span data-stu-id="83760-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="83760-144">application tooan déjà créée à l’aide du service un autre conteneur tooadd `yo`, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="83760-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="83760-145">Modifier la racine toohello du répertoire d’application existant hello.</span><span class="sxs-lookup"><span data-stu-id="83760-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="83760-146">Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="83760-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="83760-147">Exécutez `yo azuresfcontainer:AddService`.</span><span class="sxs-lookup"><span data-stu-id="83760-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="83760-148">Empaquetage et déploiement manuel d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="83760-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="83760-149">processus Hello d’empaquetage manuel d’un service en conteneur est basée sur hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="83760-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="83760-150">Publier hello conteneurs tooyour référentiel.</span><span class="sxs-lookup"><span data-stu-id="83760-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="83760-151">Créer la structure de répertoire du package hello.</span><span class="sxs-lookup"><span data-stu-id="83760-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="83760-152">Modifiez le fichier de manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="83760-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="83760-153">Modifier le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="83760-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="83760-154">Déploiement et activation d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="83760-154">Deploy and activate a container image</span></span>
<span data-ttu-id="83760-155">Bonjour Service Fabric [modèle d’application](service-fabric-application-model.md), un conteneur représente un hôte d’application dans le service de plusieurs réplicas sont placés.</span><span class="sxs-lookup"><span data-stu-id="83760-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="83760-156">toodeploy et activer un conteneur, le nom hello put de l’image de conteneur hello dans un `ContainerHost` élément dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="83760-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="83760-157">Dans le manifeste de service hello, ajoutez un `ContainerHost` hello point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="83760-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="83760-158">Puis ensemble hello `ImageName` nom de hello toobe de référentiel de conteneurs hello et image.</span><span class="sxs-lookup"><span data-stu-id="83760-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="83760-159">Hello manifeste partielle suivante montre un exemple de comment le conteneur de hello toodeploy appelée `myimage:v1` à partir d’un référentiel appelé `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="83760-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="83760-160">Vous pouvez fournir des commandes d’entrée en spécifiant hello facultatif `Commands` élément avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="83760-161">Si les images hello n’ont pas d’un charge de travail-point d’entrée défini, vous devez tooexplicitly spécifier des commandes d’entrée à l’intérieur de `Commands` élément avec un jeu délimité par des virgules de toorun de commandes à l’intérieur du conteneur de hello, qui conserve conteneur hello en cours d’exécution démarrage.</span><span class="sxs-lookup"><span data-stu-id="83760-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="83760-162">Présentation de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="83760-162">Understand resource governance</span></span>
<span data-ttu-id="83760-163">Gouvernance des ressources sont une fonctionnalité de conteneur hello qui limite les ressources hello hello conteneur peut utiliser sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="83760-164">Hello `ResourceGovernancePolicy`, qui est spécifiée dans le manifeste de l’application hello est toodeclare utilisé des limites de ressources pour un package de code de service.</span><span class="sxs-lookup"><span data-stu-id="83760-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="83760-165">Les limites de ressources peuvent être définies pour hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="83760-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="83760-166">Mémoire</span><span class="sxs-lookup"><span data-stu-id="83760-166">Memory</span></span>
* <span data-ttu-id="83760-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="83760-167">MemorySwap</span></span>
* <span data-ttu-id="83760-168">CpuShares (pondération relative à l’UC)</span><span class="sxs-lookup"><span data-stu-id="83760-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="83760-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="83760-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="83760-170">BlkioWeight (poids relatif de l’élément BlockIO)</span><span class="sxs-lookup"><span data-stu-id="83760-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="83760-171">Dans une version ultérieure, il sera possible de prendre en charge la spécification de limites relatives aux E/S en mode bloc précises (E/S par seconde, bits par seconde en lecture/écriture...).</span><span class="sxs-lookup"><span data-stu-id="83760-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="83760-172">Authentification d’un référentiel</span><span class="sxs-lookup"><span data-stu-id="83760-172">Authenticate a repository</span></span>
<span data-ttu-id="83760-173">toodownload un conteneur, vous pouvez avoir référentiel de conteneurs toohello tooprovide informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="83760-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="83760-174">Hello informations de connexion, spécifiées dans le manifeste de l’application hello sont utilisées toospecify hello connectez-vous plus d’informations ou d’une clé SSH pour télécharger l’image de conteneur hello hello référentiel d’images.</span><span class="sxs-lookup"><span data-stu-id="83760-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="83760-175">Hello suivant montre un compte appelé *TestUser* , ainsi que le mot de passe hello en texte clair (*pas* recommandé) :</span><span class="sxs-lookup"><span data-stu-id="83760-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="83760-176">Nous vous conseillons de chiffrer un mot de passe hello à l’aide d’un certificat qui a déployé toohello machine.</span><span class="sxs-lookup"><span data-stu-id="83760-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="83760-177">Hello suivant montre un compte appelé *TestUser*, où le mot de passe hello a été chiffré à l’aide d’un certificat appelé *MonCert*.</span><span class="sxs-lookup"><span data-stu-id="83760-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="83760-178">Vous pouvez utiliser hello `Invoke-ServiceFabricEncryptText` texte PowerShell commande toocreate hello secrète de chiffrement de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="83760-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="83760-179">Pour plus d’informations, voir l’article hello [la gestion des clés secrètes dans les applications de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="83760-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="83760-180">clé privée de Hello du certificat hello qui a utilisé un mot de passe toodecrypt hello doit être déployé toohello la machine locale dans une méthode hors-bande.</span><span class="sxs-lookup"><span data-stu-id="83760-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="83760-181">(dans Azure, cette méthode est Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package toohello ordinateur hello service, il peut déchiffrer un secret de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="83760-182">À l’aide de secret hello avec le nom de compte hello, il peut authentifier puis avec le référentiel de conteneurs hello.</span><span class="sxs-lookup"><span data-stu-id="83760-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="83760-183">Configuration du mappage des ports de conteneur aux ports hôtes</span><span class="sxs-lookup"><span data-stu-id="83760-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="83760-184">Vous pouvez configurer un toocommunicate de port utilisé hôte avec le conteneur de hello en spécifiant un `PortBinding` dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="83760-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="83760-185">Hello port liaison maps hello port toowhich hello service est à l’écoute à l’intérieur de hello conteneur tooa port sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="83760-186">Configuration de la découverte et de la communication entre des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="83760-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="83760-187">À l’aide de hello `PortBinding` stratégie, vous pouvez mapper un port du conteneur de tooan `Endpoint` dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="83760-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="83760-188">point de terminaison de Hello `Endpoint1` peut spécifier un port fixe (par exemple, le port 80).</span><span class="sxs-lookup"><span data-stu-id="83760-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="83760-189">Il ne peut également spécifier aucun port, auquel cas un port aléatoire à partir de la plage de ports d’application du cluster hello est choisi pour vous.</span><span class="sxs-lookup"><span data-stu-id="83760-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="83760-190">Si vous spécifiez un point de terminaison, à l’aide de hello `Endpoint` balise dans le manifeste de service hello d’un conteneur d’invité, l’infrastructure de Service peut publier automatiquement cette toohello de point de terminaison service de noms.</span><span class="sxs-lookup"><span data-stu-id="83760-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="83760-191">Autres services qui s’exécutent dans un cluster de hello peuvent découvrir donc ce conteneur à l’aide de requêtes REST hello pour la résolution.</span><span class="sxs-lookup"><span data-stu-id="83760-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="83760-192">En inscrivant avec hello Naming service, facilement faire communication de conteneur à l’autre dans le code hello dans votre conteneur, à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="83760-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="83760-193">Communication est effectuée en fournissant le port d’écoute http proxy inverse hello et nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="83760-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="83760-194">Pour plus d’informations, consultez la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="83760-195">Configurer et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="83760-195">Configure and set environment variables</span></span>
<span data-ttu-id="83760-196">Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello, à la fois pour les services qui sont déployés dans des conteneurs ou pour les services qui sont déployées sous forme de fichiers exécutables du processus/invité.</span><span class="sxs-lookup"><span data-stu-id="83760-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="83760-197">Ces valeurs de variable d’environnement peuvent être substituées en particulier dans le manifeste de l’application hello ou spécifiés pendant le déploiement en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="83760-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="83760-198">Hello service manifeste XML extrait de code suivant illustre un exemple de variables d’environnement toospecify pour un package de code :</span><span class="sxs-lookup"><span data-stu-id="83760-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="83760-199">Ces variables d’environnement peuvent être remplacées au niveau hello du manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="83760-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="83760-200">Dans l’exemple précédent de hello, que nous avons spécifié une valeur explicite pour hello `HttpGateway` variable d’environnement (19000) pendant la valeur hello pour `BackendServiceName` paramètre via hello `[BackendSvc]` paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="83760-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="83760-201">Ces paramètres vous permettent de valeur hello toospecify `BackendServiceName`valeur lorsque vous déployez l’application hello et n’avez pas de valeur fixe dans le manifeste de hello.</span><span class="sxs-lookup"><span data-stu-id="83760-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="83760-202">Exemples complets pour le manifeste de l’application et de service</span><span class="sxs-lookup"><span data-stu-id="83760-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="83760-203">Voici un exemple de fichier manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="83760-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="83760-204">Un exemple de manifeste de service (spécifié dans hello précédant le manifeste d’application) suivante :</span><span class="sxs-lookup"><span data-stu-id="83760-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="83760-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83760-205">Next steps</span></span>
<span data-ttu-id="83760-206">Maintenant que vous avez déployé un service en conteneur, découvrez comment toomanage son cycle de vie en lisant [cycle de vie de l’infrastructure de Service application](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="83760-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="83760-207">Vue d’ensemble de Service Fabric et des conteneurs</span><span class="sxs-lookup"><span data-stu-id="83760-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="83760-208">Interaction avec les clusters de l’infrastructure de Service à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="83760-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="83760-209">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="83760-209">Related articles</span></span>

* [<span data-ttu-id="83760-210">Prise en main de Service Fabric et d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="83760-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* <span data-ttu-id="83760-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Prise en main de l’interface de ligne de commande Service Fabric XPlat)</span><span class="sxs-lookup"><span data-stu-id="83760-211">[Getting started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
