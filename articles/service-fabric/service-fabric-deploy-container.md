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
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="a85d0-104">Déployer un tooService de conteneur Windows Fabric</span><span class="sxs-lookup"><span data-stu-id="a85d0-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a85d0-105">Déployer un conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="a85d0-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="a85d0-106">Déployer un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="a85d0-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="a85d0-107">Cet article vous guide tout au long des processus hello de création des services dans les conteneurs Windows.</span><span class="sxs-lookup"><span data-stu-id="a85d0-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="a85d0-108">Service Fabric dispose de plusieurs fonctionnalités qui vous aident à créer des applications composées de microservices exécutés dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a85d0-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="a85d0-109">les fonctions Hello incluent :</span><span class="sxs-lookup"><span data-stu-id="a85d0-109">hello capabilities include:</span></span>

* <span data-ttu-id="a85d0-110">Activation et déploiement d’images de conteneur</span><span class="sxs-lookup"><span data-stu-id="a85d0-110">Container image deployment and activation</span></span>
* <span data-ttu-id="a85d0-111">Gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="a85d0-111">Resource governance</span></span>
* <span data-ttu-id="a85d0-112">Authentification de référentiels</span><span class="sxs-lookup"><span data-stu-id="a85d0-112">Repository authentication</span></span>
* <span data-ttu-id="a85d0-113">Mappage des ports de conteneur aux ports hôtes</span><span class="sxs-lookup"><span data-stu-id="a85d0-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="a85d0-114">Découverte et communication entre des conteneurs</span><span class="sxs-lookup"><span data-stu-id="a85d0-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="a85d0-115">Capacité tooconfigure et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="a85d0-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="a85d0-116">Examinons chacune des fonctions fonctionne lorsque vous créez un package une toobe en conteneur service inclus dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a85d0-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="a85d0-117">Empaquetage d’un conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="a85d0-117">Package a Windows container</span></span>
<span data-ttu-id="a85d0-118">Quand vous créez le package un conteneur, vous pouvez choisir toouse un modèle de projet Visual Studio ou [créer le package d’application hello manuellement](#manually).</span><span class="sxs-lookup"><span data-stu-id="a85d0-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="a85d0-119">Lorsque vous utilisez Visual Studio, structure de package d’application hello et fichiers manifestes sont créés par le modèle de projet hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="a85d0-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="a85d0-120">toopackage de façon plus simple Hello une image de conteneur existant dans un service est toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a85d0-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="a85d0-121">Utilisez Visual Studio toopackage une image de conteneur existant</span><span class="sxs-lookup"><span data-stu-id="a85d0-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="a85d0-122">Visual Studio fournit une infrastructure de Service toohelp de modèle de service vous déployez un cluster Service Fabric de tooa conteneur.</span><span class="sxs-lookup"><span data-stu-id="a85d0-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="a85d0-123">Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a85d0-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="a85d0-124">Choisissez **invité conteneur** en tant que modèle de service hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="a85d0-125">Choisissez **nom de l’Image** et fournir hello chemin d’accès toohello image dans votre référentiel de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a85d0-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="a85d0-126">Par exemple, `myrepo/myimage:v1` dans https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="a85d0-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="a85d0-127">Donnez un nom à votre service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a85d0-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="a85d0-128">Si votre service en conteneur a besoin d’un point de terminaison pour la communication, vous pouvez maintenant ajouter hello protocole, port et fichier de type toohello ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a85d0-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="a85d0-129">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a85d0-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="a85d0-130">En fournissant hello `UriScheme`, Service Fabric inscrit automatiquement le point de terminaison de conteneur hello avec hello service d’affectation de noms pour la fonctionnalité de découverte.</span><span class="sxs-lookup"><span data-stu-id="a85d0-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="a85d0-131">port de Hello peut être résolu (comme indiqué dans le précédent exemple de hello) ou allouée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="a85d0-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="a85d0-132">Si vous ne spécifiez pas un port, il est attribué dynamiquement à partir de la plage de ports d’application hello (comme avec n’importe quel service).</span><span class="sxs-lookup"><span data-stu-id="a85d0-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="a85d0-133">Vous devez également le mappage port toohost tooconfigure hello conteneur en spécifiant un `PortBinding` stratégie dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="a85d0-134">Pour plus d’informations, consultez [configurer le mappage de port de conteneur toohost](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="a85d0-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="a85d0-135">Si votre conteneur a besoin de gouvernance des ressources, ajoutez un `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="a85d0-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="a85d0-136">Si votre conteneur doit tooauthenticate avec un référentiel privé, puis ajoutez `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="a85d0-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="a85d0-137">Si vous exécutez sur un ordinateur Windows Server 2016 avec prise en charge du conteneur activée, vous pouvez utiliser le package de hello et cluster local du tooyour toodeploy action de publication.</span><span class="sxs-lookup"><span data-stu-id="a85d0-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="a85d0-138">Lorsque vous êtes prêt, vous pouvez publier le cluster de l’application hello tooa à distance ou archiver hello solution toosource contrôle.</span><span class="sxs-lookup"><span data-stu-id="a85d0-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="a85d0-139">Pour obtenir un exemple hello d’extraction [exemples de code de conteneur de Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="a85d0-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="a85d0-140">Création d’un cluster Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a85d0-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="a85d0-141">toodeploy votre application en conteneur, vous devez toocreate un cluster exécutant Windows Server 2016 avec prise en charge du conteneur est activé.</span><span class="sxs-lookup"><span data-stu-id="a85d0-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="a85d0-142">Votre cluster peut s’exécuter localement ou être déployé via Azure Resource Manager dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a85d0-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="a85d0-143">toodeploy un cluster à l’aide du Gestionnaire de ressources Azure, choisissez hello **Windows Server 2016 avec des conteneurs** option dans Azure de l’image.</span><span class="sxs-lookup"><span data-stu-id="a85d0-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="a85d0-144">Consultez l’article hello [créer un cluster Service Fabric à l’aide du Gestionnaire de ressources Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a85d0-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="a85d0-145">Assurez-vous que vous utilisez hello suivant les paramètres du Gestionnaire de ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="a85d0-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="a85d0-146">Vous pouvez également utiliser hello [modèle cinq nœuds Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="a85d0-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="a85d0-147">Vous pouvez également lire [l’article de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la communauté sur l’utilisation des conteneurs de Service Fabric et Windows.</span><span class="sxs-lookup"><span data-stu-id="a85d0-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="a85d0-148">Empaquetage et déploiement manuel d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="a85d0-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="a85d0-149">processus Hello d’empaquetage manuel d’un service en conteneur est basée sur hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a85d0-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="a85d0-150">Publier hello conteneurs tooyour référentiel.</span><span class="sxs-lookup"><span data-stu-id="a85d0-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="a85d0-151">Créer la structure de répertoire du package hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="a85d0-152">Modifiez le fichier de manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="a85d0-153">Modifier le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="a85d0-154">Déploiement et activation d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="a85d0-154">Deploy and activate a container image</span></span>
<span data-ttu-id="a85d0-155">Bonjour Service Fabric [modèle d’application](service-fabric-application-model.md), un conteneur représente un hôte d’application dans le service de plusieurs réplicas sont placés.</span><span class="sxs-lookup"><span data-stu-id="a85d0-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="a85d0-156">toodeploy et activer un conteneur, le nom hello put de l’image de conteneur hello dans un `ContainerHost` élément dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="a85d0-157">Dans le manifeste de service hello, ajoutez un `ContainerHost` hello point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="a85d0-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="a85d0-158">Puis ensemble hello `ImageName` nom de hello toobe de référentiel de conteneurs hello et image.</span><span class="sxs-lookup"><span data-stu-id="a85d0-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="a85d0-159">Hello manifeste partielle suivante montre un exemple de comment le conteneur de hello toodeploy appelée `myimage:v1` à partir d’un référentiel appelé `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="a85d0-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="a85d0-160">Vous pouvez spécifier toorun commandes facultatives au démarrage du conteneur hello sous hello `Commands` élément.</span><span class="sxs-lookup"><span data-stu-id="a85d0-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="a85d0-161">Si vous avez plusieurs commandes, séparez-les par des virgules.</span><span class="sxs-lookup"><span data-stu-id="a85d0-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="a85d0-162">Présentation de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="a85d0-162">Understand resource governance</span></span>
<span data-ttu-id="a85d0-163">Gouvernance des ressources sont une fonctionnalité de conteneur hello qui limite les ressources hello hello conteneur peut utiliser sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="a85d0-164">Hello `ResourceGovernancePolicy`, qui est spécifiée dans le manifeste de l’application hello est toodeclare utilisé des limites de ressources pour un package de code de service.</span><span class="sxs-lookup"><span data-stu-id="a85d0-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="a85d0-165">Les limites de ressources peuvent être définies pour hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="a85d0-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="a85d0-166">Mémoire</span><span class="sxs-lookup"><span data-stu-id="a85d0-166">Memory</span></span>
* <span data-ttu-id="a85d0-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="a85d0-167">MemorySwap</span></span>
* <span data-ttu-id="a85d0-168">CpuShares (pondération relative à l’UC)</span><span class="sxs-lookup"><span data-stu-id="a85d0-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="a85d0-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="a85d0-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="a85d0-170">BlkioWeight (poids relatif de l’élément BlockIO)</span><span class="sxs-lookup"><span data-stu-id="a85d0-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="a85d0-171">La prise en charge de la spécification de limites relatives aux E/S en mode bloc précises (E/S par seconde, bits par seconde en lecture/écriture...) est prévue dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a85d0-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="a85d0-172">Authentification d’un référentiel</span><span class="sxs-lookup"><span data-stu-id="a85d0-172">Authenticate a repository</span></span>
<span data-ttu-id="a85d0-173">toodownload un conteneur, vous pouvez avoir référentiel de conteneurs toohello tooprovide informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="a85d0-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="a85d0-174">Hello informations de connexion, spécifiées dans le manifeste de l’application hello sont utilisées toospecify hello connectez-vous plus d’informations ou d’une clé SSH pour télécharger l’image de conteneur hello hello référentiel d’images.</span><span class="sxs-lookup"><span data-stu-id="a85d0-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="a85d0-175">Hello suivant montre un compte appelé *TestUser* , ainsi que le mot de passe hello en texte clair (*pas* recommandé) :</span><span class="sxs-lookup"><span data-stu-id="a85d0-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="a85d0-176">Nous vous conseillons de chiffrer un mot de passe hello à l’aide d’un certificat qui a déployé toohello machine.</span><span class="sxs-lookup"><span data-stu-id="a85d0-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="a85d0-177">Hello suivant montre un compte appelé *TestUser*, où le mot de passe hello a été chiffré à l’aide d’un certificat appelé *MonCert*.</span><span class="sxs-lookup"><span data-stu-id="a85d0-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="a85d0-178">Vous pouvez utiliser hello `Invoke-ServiceFabricEncryptText` texte PowerShell commande toocreate hello secrète de chiffrement de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="a85d0-179">Pour plus d’informations, voir l’article hello [la gestion des clés secrètes dans les applications de Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="a85d0-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="a85d0-180">clé privée de Hello du certificat hello qui a utilisé un mot de passe toodecrypt hello doit être déployé toohello la machine locale dans une méthode hors-bande.</span><span class="sxs-lookup"><span data-stu-id="a85d0-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="a85d0-181">(dans Azure, cette méthode est Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package toohello ordinateur hello service, il peut déchiffrer un secret de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="a85d0-182">À l’aide de secret hello avec le nom de compte hello, il peut authentifier puis avec le référentiel de conteneurs hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <span data-ttu-id="a85d0-183"><a name ="Portsection"></a>Configurer le mappage de port de conteneur toohost</span><span class="sxs-lookup"><span data-stu-id="a85d0-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="a85d0-184">Vous pouvez configurer un toocommunicate de port utilisé hôte avec le conteneur de hello en spécifiant un `PortBinding` dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="a85d0-185">Hello port liaison maps hello port toowhich hello service est à l’écoute à l’intérieur de hello conteneur tooa port sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="a85d0-186">Configuration de la découverte et de la communication entre des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a85d0-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="a85d0-187">Vous pouvez utiliser hello `PortBinding` élément toomap un point de terminaison tooan port du conteneur dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="a85d0-188">Dans l’exemple suivant de hello, hello le point de terminaison `Endpoint1` spécifie un port fixe, 8905.</span><span class="sxs-lookup"><span data-stu-id="a85d0-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="a85d0-189">Il ne peut également spécifier aucun port, auquel cas un port aléatoire à partir de la plage de ports d’application du cluster hello est choisi pour vous.</span><span class="sxs-lookup"><span data-stu-id="a85d0-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="a85d0-190">Si vous spécifiez un point de terminaison, à l’aide de hello `Endpoint` balise dans le manifeste de service hello d’un conteneur d’invité, l’infrastructure de Service peut publier automatiquement cette toohello de point de terminaison service de noms.</span><span class="sxs-lookup"><span data-stu-id="a85d0-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="a85d0-191">Autres services qui s’exécutent dans un cluster de hello peuvent découvrir donc ce conteneur à l’aide de requêtes REST hello pour la résolution.</span><span class="sxs-lookup"><span data-stu-id="a85d0-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="a85d0-192">En inscrivant avec hello Naming service, vous pouvez effectuer communication de conteneur à l’autre au sein de votre conteneur à l’aide de hello [proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a85d0-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a85d0-193">Communication est effectuée en fournissant le port d’écoute http proxy inverse hello et nom hello de services hello que vous souhaitez toocommunicate avec comme variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="a85d0-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="a85d0-194">Pour plus d’informations, consultez la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="a85d0-195">Configurer et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="a85d0-195">Configure and set environment variables</span></span>
<span data-ttu-id="a85d0-196">Variables d’environnement peuvent être spécifiées pour chaque package de code dans le manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="a85d0-197">Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités.</span><span class="sxs-lookup"><span data-stu-id="a85d0-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="a85d0-198">Vous pouvez remplacer la variable d’environnement valeurs dans une application hello manifeste ou spécifient durant le déploiement en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="a85d0-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="a85d0-199">Hello service manifeste XML extrait de code suivant illustre un exemple de variables d’environnement toospecify pour un package de code :</span><span class="sxs-lookup"><span data-stu-id="a85d0-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="a85d0-200">Ces variables d’environnement peuvent être remplacées au niveau hello du manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="a85d0-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="a85d0-201">Dans l’exemple précédent de hello, que nous avons spécifié une valeur explicite pour hello `HttpGateway` variable d’environnement (19000) pendant la valeur hello pour `BackendServiceName` paramètre via hello `[BackendSvc]` paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="a85d0-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="a85d0-202">Ces paramètres vous permettent de valeur hello toospecify `BackendServiceName`valeur lorsque vous déployez l’application hello et n’avez pas de valeur fixe dans le manifeste de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="a85d0-203">Configurer le mode d’isolation</span><span class="sxs-lookup"><span data-stu-id="a85d0-203">Configure isolation mode</span></span>

<span data-ttu-id="a85d0-204">Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a85d0-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="a85d0-205">Avec le mode d’isolation du processus de hello, en cours d’exécution tous les conteneurs de hello hello même hôte ordinateur partage hello du noyau avec l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="a85d0-206">Avec le mode d’isolation hello Hyper-V, les noyaux hello sont isolées entre chaque conteneur Hyper-V et l’hôte de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="a85d0-207">le mode d’isolation Hello est spécifié dans hello `ContainerHostPolicies` balise dans le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="a85d0-208">modes d’isolation Hello qui peuvent être spécifiées sont `process`, `hyperv`, et `default`.</span><span class="sxs-lookup"><span data-stu-id="a85d0-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="a85d0-209">Hello `default` mode d’isolation par défaut est trop`process` sur Windows Server héberge et la valeur par défaut est trop`hyperv` sur des hôtes Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a85d0-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="a85d0-210">Hello extrait de code suivant montre comment le mode d’isolation hello est défini dans le fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a85d0-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="a85d0-211">Exemples complets pour le manifeste de l’application et de service</span><span class="sxs-lookup"><span data-stu-id="a85d0-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="a85d0-212">Voici un exemple de fichier manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="a85d0-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="a85d0-213">Un exemple de manifeste de service (spécifié dans hello précédant le manifeste d’application) suivante :</span><span class="sxs-lookup"><span data-stu-id="a85d0-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a85d0-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a85d0-214">Next steps</span></span>
<span data-ttu-id="a85d0-215">Maintenant que vous avez déployé un service en conteneur, découvrez comment toomanage son cycle de vie en lisant [cycle de vie de l’infrastructure de Service application](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="a85d0-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="a85d0-216">Vue d’ensemble de Service Fabric et des conteneurs</span><span class="sxs-lookup"><span data-stu-id="a85d0-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="a85d0-217">Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="a85d0-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
