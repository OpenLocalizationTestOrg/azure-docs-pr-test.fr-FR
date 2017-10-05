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
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="62d6e-104">Déployer un conteneur Windows sur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="62d6e-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62d6e-105">Déployer un conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="62d6e-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="62d6e-106">Déployer un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="62d6e-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="62d6e-107">Cet article vous guide dans le processus de création des services dans des conteneurs Windows.</span><span class="sxs-lookup"><span data-stu-id="62d6e-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="62d6e-108">Service Fabric dispose de plusieurs fonctionnalités qui vous aident à créer des applications composées de microservices exécutés dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="62d6e-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="62d6e-109">Ces fonctionnalités sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="62d6e-109">The capabilities include:</span></span>

* <span data-ttu-id="62d6e-110">Activation et déploiement d’images de conteneur</span><span class="sxs-lookup"><span data-stu-id="62d6e-110">Container image deployment and activation</span></span>
* <span data-ttu-id="62d6e-111">Gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="62d6e-111">Resource governance</span></span>
* <span data-ttu-id="62d6e-112">Authentification de référentiels</span><span class="sxs-lookup"><span data-stu-id="62d6e-112">Repository authentication</span></span>
* <span data-ttu-id="62d6e-113">Mappage des ports de conteneur aux ports hôtes</span><span class="sxs-lookup"><span data-stu-id="62d6e-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="62d6e-114">Découverte et communication entre des conteneurs</span><span class="sxs-lookup"><span data-stu-id="62d6e-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="62d6e-115">Possibilité de configurer et de définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="62d6e-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="62d6e-116">Examinons à présent le fonctionnement de chacune des fonctionnalités lors de l’empaquetage d’un service en conteneur à inclure dans votre application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="62d6e-117">Empaquetage d’un conteneur Windows</span><span class="sxs-lookup"><span data-stu-id="62d6e-117">Package a Windows container</span></span>
<span data-ttu-id="62d6e-118">Lors de l’empaquetage d’un conteneur, vous pouvez choisir d’utiliser un modèle de projet Visual Studio ou de [créer le package d’application manuellement](#manually).</span><span class="sxs-lookup"><span data-stu-id="62d6e-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="62d6e-119">Lorsque vous utilisez Visual Studio, la structure de package d’application et les fichiers manifeste sont créés par le modèle de nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="62d6e-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="62d6e-120">Pour empaqueter une image de conteneur existante dans un service, le plus simple consiste à utiliser Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62d6e-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="62d6e-121">Utilisation de Visual Studio pour empaqueter une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="62d6e-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="62d6e-122">Visual Studio fournit un modèle de service Service Fabric pour vous aider à déployer un conteneur sur un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="62d6e-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="62d6e-123">Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="62d6e-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="62d6e-124">Choisissez **Conteneur d’invités** comme modèle de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="62d6e-125">Choisissez **Nom de l’image** et indiquez le chemin d’accès à l’image dans votre référentiel de conteneur.</span><span class="sxs-lookup"><span data-stu-id="62d6e-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="62d6e-126">Par exemple, `myrepo/myimage:v1` dans https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="62d6e-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="62d6e-127">Donnez un nom à votre service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62d6e-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="62d6e-128">Si votre service en conteneur a besoin d’un point de terminaison pour les communications, vous pouvez désormais ajouter le protocole, le port et le type dans le fichier ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="62d6e-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="62d6e-129">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62d6e-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="62d6e-130">En fournissant `UriScheme`, Service Fabric enregistre automatiquement le point de terminaison du conteneur avec le Naming Service pour la découverte.</span><span class="sxs-lookup"><span data-stu-id="62d6e-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="62d6e-131">Le port peut être fixe (comme indiqué dans l’exemple précédent) ou alloué de manière dynamique.</span><span class="sxs-lookup"><span data-stu-id="62d6e-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="62d6e-132">Si vous ne spécifiez pas de port, il est alloué de manière dynamique à partir de la plage de ports d’application (comme avec n’importe quel service).</span><span class="sxs-lookup"><span data-stu-id="62d6e-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="62d6e-133">Vous devez également configurer le mappage conteneur/port hôte en spécifiant une stratégie `PortBinding` dans le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="62d6e-134">Pour plus d’informations, voir [Configurer le mappage conteneur/port hôte](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="62d6e-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="62d6e-135">Si votre conteneur a besoin de gouvernance des ressources, ajoutez un `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="62d6e-136">Si votre conteneur doit s’authentifier auprès d’un référentiel privé, ajoutez `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="62d6e-137">Si vous utilisez un ordinateur Windows Server 2016 avec prise en charge du conteneur, vous pouvez utiliser le package et publier des actions pour déployer sur votre cluster local.</span><span class="sxs-lookup"><span data-stu-id="62d6e-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="62d6e-138">Vous pouvez, quand vous le souhaitez, publier l’application sur un cluster à distance ou archiver la solution pour contrôler le code source.</span><span class="sxs-lookup"><span data-stu-id="62d6e-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="62d6e-139">Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="62d6e-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="62d6e-140">Création d’un cluster Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="62d6e-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="62d6e-141">Pour déployer votre application en conteneur, vous devez créer un cluster exécutant Windows Server 2016 avec la prise en charge du conteneur activée.</span><span class="sxs-lookup"><span data-stu-id="62d6e-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="62d6e-142">Votre cluster peut s’exécuter localement ou être déployé via Azure Resource Manager dans Azure.</span><span class="sxs-lookup"><span data-stu-id="62d6e-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="62d6e-143">Pour déployer un cluster à l’aide d’Azure Resource Manager, choisissez l’option d’image **Windows Server 2016 avec Containers** dans Azure.</span><span class="sxs-lookup"><span data-stu-id="62d6e-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="62d6e-144">Consultez l’article [Création d’un cluster Service Fabric dans Azure à l’aide d’un modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="62d6e-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="62d6e-145">Assurez-vous d’utiliser les paramètres suivants dans Azure Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="62d6e-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="62d6e-146">Vous pouvez également utiliser le [modèle Azure Resource Manager à cinq nœuds](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) pour créer un cluster.</span><span class="sxs-lookup"><span data-stu-id="62d6e-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="62d6e-147">Vous pouvez également lire [l’article de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) de la communauté sur l’utilisation des conteneurs de Service Fabric et Windows.</span><span class="sxs-lookup"><span data-stu-id="62d6e-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="62d6e-148">Empaquetage et déploiement manuel d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="62d6e-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="62d6e-149">Le processus d’empaquetage manuel d’un service avec conteneur est basé sur les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="62d6e-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="62d6e-150">Publiez les conteneurs dans votre référentiel.</span><span class="sxs-lookup"><span data-stu-id="62d6e-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="62d6e-151">Créez la structure de répertoires du package.</span><span class="sxs-lookup"><span data-stu-id="62d6e-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="62d6e-152">Modifiez le fichier de manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="62d6e-153">Modifiez le fichier de manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="62d6e-154">Déploiement et activation d’une image de conteneur</span><span class="sxs-lookup"><span data-stu-id="62d6e-154">Deploy and activate a container image</span></span>
<span data-ttu-id="62d6e-155">Dans le [modèle d’application](service-fabric-application-model.md)Service Fabric, un conteneur représente un hôte d’application sur lequel sont placés plusieurs réplicas de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="62d6e-156">Pour déployer et activer un conteneur, placez le nom de l’image de conteneur dans un élément `ContainerHost` au sein du manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="62d6e-157">Dans le manifeste de service, ajoutez un `ContainerHost` pour le point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="62d6e-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="62d6e-158">Définissez ensuite le nom de référentiel de conteneur et d’image comme `ImageName`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="62d6e-159">Le manifeste partiel suivant affiche un exemple illustrant le déploiement du conteneur appelé `myimage:v1` depuis un référentiel appelé `myrepo` :</span><span class="sxs-lookup"><span data-stu-id="62d6e-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="62d6e-160">Vous pouvez spécifier des commandes facultatives à exécuter lors du démarrage du conteneur sous l’élément `Commands`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="62d6e-161">Si vous avez plusieurs commandes, séparez-les par des virgules.</span><span class="sxs-lookup"><span data-stu-id="62d6e-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="62d6e-162">Présentation de la gouvernance des ressources</span><span class="sxs-lookup"><span data-stu-id="62d6e-162">Understand resource governance</span></span>
<span data-ttu-id="62d6e-163">La gouvernance des ressources est une fonctionnalité du conteneur, qui limite les ressources que le conteneur peut utiliser sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="62d6e-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="62d6e-164">L’élément `ResourceGovernancePolicy`, spécifié dans le manifeste de l’application, est utilisé pour déclarer des limites relatives aux ressources pour un package de code de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="62d6e-165">Des limites de ressources peuvent être définies pour les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="62d6e-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="62d6e-166">Mémoire</span><span class="sxs-lookup"><span data-stu-id="62d6e-166">Memory</span></span>
* <span data-ttu-id="62d6e-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="62d6e-167">MemorySwap</span></span>
* <span data-ttu-id="62d6e-168">CpuShares (pondération relative à l’UC)</span><span class="sxs-lookup"><span data-stu-id="62d6e-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="62d6e-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="62d6e-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="62d6e-170">BlkioWeight (poids relatif de l’élément BlockIO)</span><span class="sxs-lookup"><span data-stu-id="62d6e-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="62d6e-171">La prise en charge de la spécification de limites relatives aux E/S en mode bloc précises (E/S par seconde, bits par seconde en lecture/écriture...) est prévue dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="62d6e-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="62d6e-172">Authentification d’un référentiel</span><span class="sxs-lookup"><span data-stu-id="62d6e-172">Authenticate a repository</span></span>
<span data-ttu-id="62d6e-173">Pour télécharger un conteneur, vous devrez peut-être fournir des informations d’identification dans le référentiel du conteneur.</span><span class="sxs-lookup"><span data-stu-id="62d6e-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="62d6e-174">Les informations d’identification de connexion spécifiées dans le manifeste de l’application sont utilisées pour spécifier les informations de connexion (ou clé SSH) pour le téléchargement de l’image de conteneur à partir du référentiel d’images.</span><span class="sxs-lookup"><span data-stu-id="62d6e-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="62d6e-175">L’exemple suivant utilise un compte appelé *TestUser*, ainsi que le mot de passe en texte clair associé (*non* recommandé) :</span><span class="sxs-lookup"><span data-stu-id="62d6e-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="62d6e-176">Nous vous recommandons de chiffrer le mot de passe à l’aide d’un certificat qui est déployé sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="62d6e-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="62d6e-177">L’exemple suivant utilise un compte appelé *TestUser* avec un mot de passe chiffré à l’aide d’un certificat nommé *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="62d6e-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="62d6e-178">Vous pouvez utiliser la commande PowerShell `Invoke-ServiceFabricEncryptText` pour créer le texte de chiffrement secret du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="62d6e-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="62d6e-179">Pour en savoir plus, consultez l’article [Gestion des secrets dans des applications Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="62d6e-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="62d6e-180">La clé privée du certificat utilisée pour déchiffrer le mot de passe doit être déployée sur l’ordinateur local dans une méthode hors bande</span><span class="sxs-lookup"><span data-stu-id="62d6e-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="62d6e-181">(dans Azure, cette méthode est Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package de service sur l’ordinateur, il peut déchiffrer la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="62d6e-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="62d6e-182">Avec la clé secrète et le nom du compte, il peut ensuite s’authentifier dans le référentiel de conteneur.</span><span class="sxs-lookup"><span data-stu-id="62d6e-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="62d6e-183"><a name ="Portsection"></a> Configurer le mappage conteneur/port hôte</span><span class="sxs-lookup"><span data-stu-id="62d6e-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="62d6e-184">Vous pouvez configurer un port d’hôte utilisé pour communiquer avec le conteneur en spécifiant un élément `PortBinding` dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="62d6e-185">La liaison de port mappe le port sur lequel le service écoute, à l’intérieur du conteneur, à un port sur l’hôte.</span><span class="sxs-lookup"><span data-stu-id="62d6e-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="62d6e-186">Configuration de la découverte et de la communication entre des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="62d6e-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="62d6e-187">Vous pouvez utiliser l’élément `PortBinding` pour mapper un port de conteneur à un point de terminaison dans le manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="62d6e-188">Dans l’exemple suivant, le point de terminaison `Endpoint1` spécifie un port fixe, 8905.</span><span class="sxs-lookup"><span data-stu-id="62d6e-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="62d6e-189">Il peut également ne spécifier aucun port, auquel cas un port aléatoire est sélectionné dans la plage de ports des applications du cluster.</span><span class="sxs-lookup"><span data-stu-id="62d6e-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="62d6e-190">Si vous spécifiez un point de terminaison à l’aide de la balise `Endpoint` dans le manifeste de service d’un conteneur invité, Service Fabric peut publier automatiquement ce point de terminaison au Naming Service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="62d6e-191">D’autres services exécutés dans le cluster peuvent ainsi détecter ce conteneur à l’aide de requêtes REST pour la résolution.</span><span class="sxs-lookup"><span data-stu-id="62d6e-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="62d6e-192">En vous inscrivant auprès du Naming Service, vous pouvez établir des communications entre les conteneurs au sein de votre conteneur à l’aide d’un [proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="62d6e-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="62d6e-193">Pour établir la communication, vous devez fournir le port d’écoute HTTP associé au proxy inverse et le nom des services avec lesquels vous souhaitez communiquer en tant que variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="62d6e-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="62d6e-194">Pour en savoir plus, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="62d6e-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="62d6e-195">Configurer et définir des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="62d6e-195">Configure and set environment variables</span></span>
<span data-ttu-id="62d6e-196">Il est possible de spécifier des variables d’environnement pour chaque package de code dans le manifeste de service.</span><span class="sxs-lookup"><span data-stu-id="62d6e-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="62d6e-197">Cette fonctionnalité est disponible pour tous les services, qu’ils soient déployés sous forme de conteneurs, de processus ou d’exécutables invités.</span><span class="sxs-lookup"><span data-stu-id="62d6e-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="62d6e-198">Vous pouvez remplacer les valeurs de variable d’environnement dans le manifeste de l’application, ou les spécifier lors du déploiement, en tant que paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="62d6e-199">L’extrait de code XML du manifeste de service suivant illustre la méthode à suivre pour spécifier des variables d’environnement pour un package de code :</span><span class="sxs-lookup"><span data-stu-id="62d6e-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="62d6e-200">Ces variables d’environnement peuvent être remplacées au niveau du manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="62d6e-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="62d6e-201">Dans l’exemple ci-dessus, nous avons indiqué une valeur explicite pour la variable d’environnement `HttpGateway` (19000) alors que la valeur du paramètre `BackendServiceName` est définie par le biais du paramètre d’application `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="62d6e-202">De cette manière, vous pouvez spécifier la valeur de l’élément `BackendServiceName`au moment du déploiement de l’application, sans avoir de valeur fixe dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="62d6e-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="62d6e-203">Configurer le mode d’isolation</span><span class="sxs-lookup"><span data-stu-id="62d6e-203">Configure isolation mode</span></span>

<span data-ttu-id="62d6e-204">Windows prend en charge deux modes d’isolation pour les conteneurs : Processus et Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="62d6e-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="62d6e-205">Avec le mode d’isolation Processus, tous les conteneurs s’exécutant sur le même hôte partagent le noyau avec l’hôte.</span><span class="sxs-lookup"><span data-stu-id="62d6e-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="62d6e-206">Avec le mode d’isolation Hyper-V, les noyaux sont isolés entre chaque conteneur Hyper-V et l’hôte du conteneur.</span><span class="sxs-lookup"><span data-stu-id="62d6e-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="62d6e-207">Le mode d’isolation est spécifié dans la balise `ContainerHostPolicies` dans le fichier manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="62d6e-208">Les modes d’isolation qui peuvent être définis sont `process`, `hyperv` et `default`.</span><span class="sxs-lookup"><span data-stu-id="62d6e-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="62d6e-209">Par défaut, le mode d’isolation `default` est défini sur `process` sur les hôtes Windows Server et sur `hyperv` sur les hôtes Windows 10.</span><span class="sxs-lookup"><span data-stu-id="62d6e-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="62d6e-210">L’extrait de code suivant montre comment le mode d’isolation est spécifié dans le fichier manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="62d6e-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="62d6e-211">Exemples complets pour le manifeste de l’application et de service</span><span class="sxs-lookup"><span data-stu-id="62d6e-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="62d6e-212">Voici un exemple de fichier manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="62d6e-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="62d6e-213">Voici un exemple de manifeste de service (indiqué dans le manifeste de l’application ci-dessus) :</span><span class="sxs-lookup"><span data-stu-id="62d6e-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="62d6e-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62d6e-214">Next steps</span></span>
<span data-ttu-id="62d6e-215">Maintenant que vous avez déployé un service en conteneur, découvrez comment gérer son cycle de vie en lisant [Cycle de vie des applications Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="62d6e-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="62d6e-216">Vue d’ensemble de Service Fabric et des conteneurs</span><span class="sxs-lookup"><span data-stu-id="62d6e-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="62d6e-217">Pour un exemple, consultez les [exemples de code de conteneur Service Fabric sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="62d6e-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
