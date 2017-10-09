---
title: "un cluster d’Azure Service Fabric autonomes d’aaaCreate | Documents Microsoft"
description: "Créez un cluster Azure Service Fabric sur n’importe quel ordinateur (physique ou virtuel) exécutant Windows Server, qu’il soit local ou dans un cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="48fa8-103">Créer un cluster autonome s’exécutant sur Windows Server</span><span class="sxs-lookup"><span data-stu-id="48fa8-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="48fa8-104">Vous pouvez utiliser Azure Service Fabric toocreate Service Fabric clusters sur des ordinateurs virtuels ou des ordinateurs exécutant Windows Server.</span><span class="sxs-lookup"><span data-stu-id="48fa8-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="48fa8-105">Cela signifie que vous pouvez déployer et exécuter des applications Service Fabric dans n’importe quel environnement contenant un ensemble d’ordinateurs Windows Server interconnectés, que ce soit en local ou avec un fournisseur cloud.</span><span class="sxs-lookup"><span data-stu-id="48fa8-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="48fa8-106">L’infrastructure de service fournit un toocreate du package d’installation de clusters Service Fabric appelé package de Windows Server autonome hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="48fa8-107">Cet article vous guide tout au long des étapes hello pour créer un cluster autonome de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48fa8-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="48fa8-108">Ce package de Windows Server autonome est commercialisé et peut être utilisé pour les déploiements de production.</span><span class="sxs-lookup"><span data-stu-id="48fa8-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="48fa8-109">Ce package peut contenir de nouvelles fonctionnalités Service Fabric en version « préliminaire ».</span><span class="sxs-lookup"><span data-stu-id="48fa8-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="48fa8-110">Faites défiler la liste trop »[incluses dans ce package de fonctionnalités en version préliminaire](#previewfeatures_anchor). »</span><span class="sxs-lookup"><span data-stu-id="48fa8-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="48fa8-111">section de la liste de hello de fonctionnalités en version préliminaire hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="48fa8-112">Vous pouvez [télécharger une copie du CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) maintenant.</span><span class="sxs-lookup"><span data-stu-id="48fa8-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="48fa8-113">Obtenir un support technique pour le package de Service Fabric pour Windows Server hello</span><span class="sxs-lookup"><span data-stu-id="48fa8-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="48fa8-114">Demandez les Communautés hello package autonome de Service Fabric hello pour Windows Server Bonjour [forum d’Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="48fa8-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="48fa8-115">Ouvrez un ticket pour obtenir le [support professionnel Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="48fa8-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="48fa8-116">En savoir plus sur le support professionnel Microsoft [ici](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="48fa8-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="48fa8-117">Vous pouvez également bénéficier du support pour ce package dans le cadre du [Support Premier Microsoft](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="48fa8-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="48fa8-118">Pour plus d’informations, consultez [Options de support d’Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="48fa8-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="48fa8-119">journaux toocollect pour des raisons de prise en charge, exécutez hello [Service Fabric autonomes Log collector](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="48fa8-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="48fa8-120">Téléchargez hello Service Fabric pour Windows Server</span><span class="sxs-lookup"><span data-stu-id="48fa8-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="48fa8-121">cluster de hello toocreate, utiliser le package Service Fabric pour Windows Server hello (Windows Server 2012 R2 et version ultérieure) est disponible ici :</span><span class="sxs-lookup"><span data-stu-id="48fa8-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="48fa8-122">
[Lien de téléchargement - Package autonome Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="48fa8-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="48fa8-123">Plus d’informations sur le contenu du package de hello [ici](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="48fa8-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="48fa8-124">package de runtime Service Fabric Hello est automatiquement téléchargé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="48fa8-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="48fa8-125">Si le déploiement à partir d’un ordinateur non connecté toohello internet, téléchargez le package de runtime hello hors bande à partir d’ici :</span><span class="sxs-lookup"><span data-stu-id="48fa8-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="48fa8-126">
[Lien de téléchargement - Runtime Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="48fa8-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="48fa8-127">Recherchez des exemples de configuration de cluster autonome sous :</span><span class="sxs-lookup"><span data-stu-id="48fa8-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="48fa8-128">
[Exemples de configuration de cluster autonome](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="48fa8-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="48fa8-129">Créer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="48fa8-129">Create hello cluster</span></span>
<span data-ttu-id="48fa8-130">Service Fabric peut être un cluster de développement d’une machine tooa déployé à l’aide de hello *ClusterConfig.Unsecure.DevCluster.json* fichier inclus dans [exemples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="48fa8-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="48fa8-131">Décompressez le package tooyour ordinateur hello autonome, copie hello exemple config fichier toohello ordinateur local, puis exécution hello *CreateServiceFabricCluster.ps1* script via une session PowerShell d’administrateur, de hello autonome dossier du package :</span><span class="sxs-lookup"><span data-stu-id="48fa8-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="48fa8-132">Étape 1A : Créer un cluster de développement local non sécurisé</span><span class="sxs-lookup"><span data-stu-id="48fa8-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="48fa8-133">Consultez hello de section de configuration de l’environnement à [planifier et préparer le déploiement de clusters](service-fabric-cluster-standalone-deployment-preparation.md) pour les détails de résolution.</span><span class="sxs-lookup"><span data-stu-id="48fa8-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="48fa8-134">Si vous avez terminé les scénarios de développement en cours d’exécution, vous pouvez supprimer cluster Service Fabric de hello à partir de l’ordinateur de hello en vous reportant toosteps dans la section «[supprimer un cluster](#removecluster_anchor)».</span><span class="sxs-lookup"><span data-stu-id="48fa8-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="48fa8-135">Étape 1B : Créer un cluster de plusieurs ordinateurs</span><span class="sxs-lookup"><span data-stu-id="48fa8-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="48fa8-136">Une fois que vous avez parcouru hello planification et des étapes de préparation détaillés au hello sous le lien, vous êtes prêt à toocreate votre cluster de production à l’aide de votre fichier de configuration de cluster.</span><span class="sxs-lookup"><span data-stu-id="48fa8-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="48fa8-137">
[Planifier et préparer le déploiement de cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="48fa8-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="48fa8-138">Valider le fichier de configuration hello que vous avez écrit en exécutant hello *TestConfiguration.ps1* script à partir du dossier du package autonome hello :</span><span class="sxs-lookup"><span data-stu-id="48fa8-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="48fa8-139">Un résultat similaire à ce qui suit s’affiche normalement.</span><span class="sxs-lookup"><span data-stu-id="48fa8-139">You should see output like below.</span></span> <span data-ttu-id="48fa8-140">Si le champ du bas hello « Réussite » est retourné comme « True », les vérifications des tests ont réussi et cluster de hello recherche toobe déployable en fonction de la configuration d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="48fa8-141">Créer le cluster de hello : exécutez hello *CreateServiceFabricCluster.ps1* cluster de script toodeploy hello Service Fabric sur chaque ordinateur dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="48fa8-142">Les traces de déploiement sont écrites toohello VM/ordinateur sur lequel vous avez exécuté hello CreateServiceFabricCluster.ps1 de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48fa8-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="48fa8-143">Vous la trouverez dans le sous-dossier de hello DeploymentTraces, dans le répertoire hello à partir de quels hello script a été exécuté.</span><span class="sxs-lookup"><span data-stu-id="48fa8-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="48fa8-144">toosee si l’infrastructure de Service a été déployé correctement tooa machine, hello installé se trouvent dans le répertoire de FabricDataRoot hello, comme indiqué dans le fichier de configuration de cluster hello FabricSettings section (valeur par défaut c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="48fa8-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="48fa8-145">De même, vous pouvez consulter l’exécution des processus FabricHost.exe et Fabric.exe dans le Gestionnaire des tâches.</span><span class="sxs-lookup"><span data-stu-id="48fa8-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="48fa8-146">Étape 1C : Créer un cluster hors connexion (déconnecté d’Internet)</span><span class="sxs-lookup"><span data-stu-id="48fa8-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="48fa8-147">package de runtime Service Fabric Hello est automatiquement téléchargé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="48fa8-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="48fa8-148">Lorsque la déployer un cluster de toomachines ne pas connecté toohello internet, vous devez le hello toodownload Service Fabric runtime package séparément et fournir tooit de chemin d’accès hello lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="48fa8-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="48fa8-149">Hello package runtime peut être téléchargé séparément, à partir d’un autre ordinateur connecté toohello internet, à [lien Télécharger - Runtime du Service de l’ensemble fibre optique - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="48fa8-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="48fa8-150">Copiez hello runtime package toowhere vous déployez cluster hors connexion de hello à partir d’et créez un cluster de hello en exécutant `CreateServiceFabricCluster.ps1` avec hello `-FabricRuntimePackagePath` paramètre inclus, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="48fa8-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="48fa8-151">où `.\ClusterConfig.json` et `.\MicrosoftAzureServiceFabric.cab` sont respectivement de configuration du cluster toohello hello chemins d’accès et un fichier .cab d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="48fa8-152">Étape 2 : Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="48fa8-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="48fa8-153">cluster sécurisée de tooa tooconnect, consultez [Service fabric connecter toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="48fa8-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="48fa8-154">cluster non sécurisée de la tooan du tooconnect, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="48fa8-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="48fa8-155">Exemple :</span><span class="sxs-lookup"><span data-stu-id="48fa8-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="48fa8-156">Étape 3 : Afficher Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="48fa8-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="48fa8-157">Maintenant vous pouvez vous connecter toohello cluster avec Service Fabric Explorer directement à partir d’un des ordinateurs hello http://localhost:19080/Explorer/index.html ou à distance avec http://&lt*IPAddressofaMachine*> : 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="48fa8-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="48fa8-158">Ajouter et supprimer des nœuds</span><span class="sxs-lookup"><span data-stu-id="48fa8-158">Add and remove nodes</span></span>
<span data-ttu-id="48fa8-159">Vous pouvez ajouter ou supprimer le cluster Service Fabric de nœuds tooyour autonome comme l’évolution des besoins de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="48fa8-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="48fa8-160">Consultez [ajouter ou supprimer le cluster de nœuds tooa Service Fabric autonomes](service-fabric-cluster-windows-server-add-remove-nodes.md) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="48fa8-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="48fa8-161">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="48fa8-161">Remove a cluster</span></span>
<span data-ttu-id="48fa8-162">tooremove un cluster, exécutez hello *RemoveServiceFabricCluster.ps1* script PowerShell à partir de dossier du package hello et passe hello chemin d’accès toohello fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="48fa8-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="48fa8-163">Vous pouvez éventuellement spécifier un emplacement pour le journal de hello de suppression de hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="48fa8-164">Ce script peut être exécuté sur n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds dans le fichier de configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="48fa8-165">ordinateur Hello ce script s’exécute n’a pas de partie toobe du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="48fa8-166">Données de télémétrie recueillies et la manière dont tooopt sortie</span><span class="sxs-lookup"><span data-stu-id="48fa8-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="48fa8-167">Par défaut, les produits hello collecte une télémétrie sur le produit hello tooimprove hello Service Fabric d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="48fa8-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="48fa8-168">Hello Best Practice Analyzer qui s’exécute comme une partie du programme d’installation hello vérifie pour la connectivité trop[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="48fa8-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="48fa8-169">Si elle n’est pas accessible, le programme d’installation hello échoue, sauf si vous refuser de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="48fa8-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="48fa8-170">pipeline de télémétrie Hello tente hello tooupload suivant des données trop[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="48fa8-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="48fa8-171">Il est un téléchargement de meilleur effort et n’a aucun impact sur les fonctionnalités de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="48fa8-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="48fa8-172">les données de télémétrie Hello sont envoyée uniquement à partir du nœud de hello que s’exécute hello principal de gestionnaire de basculement.</span><span class="sxs-lookup"><span data-stu-id="48fa8-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="48fa8-173">Aucun autre nœud n’envoie des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="48fa8-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="48fa8-174">les données de télémétrie Hello se compose de suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="48fa8-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="48fa8-175">Nombre de services</span><span class="sxs-lookup"><span data-stu-id="48fa8-175">Number of services</span></span>
* <span data-ttu-id="48fa8-176">Nombre de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="48fa8-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="48fa8-177">Nombre de Applications</span><span class="sxs-lookup"><span data-stu-id="48fa8-177">Number of Applications</span></span>
* <span data-ttu-id="48fa8-178">Nombre de ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="48fa8-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="48fa8-179">Nombre de FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="48fa8-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="48fa8-180">Nombre de InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="48fa8-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="48fa8-181">Nombre de UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="48fa8-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="48fa8-182">Nombre de Replicas</span><span class="sxs-lookup"><span data-stu-id="48fa8-182">Number of Replicas</span></span>
* <span data-ttu-id="48fa8-183">Nombre de InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="48fa8-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="48fa8-184">Nombre de StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="48fa8-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="48fa8-185">Nombre de OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="48fa8-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="48fa8-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="48fa8-186">CommonQueueLength</span></span>
* <span data-ttu-id="48fa8-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="48fa8-187">QueryQueueLength</span></span>
* <span data-ttu-id="48fa8-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="48fa8-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="48fa8-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="48fa8-189">CommitQueueLength</span></span>
* <span data-ttu-id="48fa8-190">Nombre de nœuds</span><span class="sxs-lookup"><span data-stu-id="48fa8-190">Number of Nodes</span></span>
* <span data-ttu-id="48fa8-191">IsContextComplete : True/False</span><span class="sxs-lookup"><span data-stu-id="48fa8-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="48fa8-192">ClusterId : GUID généré de manière aléatoire pour chaque cluster</span><span class="sxs-lookup"><span data-stu-id="48fa8-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="48fa8-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="48fa8-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="48fa8-194">Adresse IP de la machine virtuelle de hello ou téléchargée à partir de quels hello télémétrie</span><span class="sxs-lookup"><span data-stu-id="48fa8-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="48fa8-195">données de télémétrie toodisable, ajouter hello suivant trop*propriétés* dans votre configuration de cluster : *enableTelemetry : false*.</span><span class="sxs-lookup"><span data-stu-id="48fa8-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="48fa8-196">Fonctionnalités préliminaires incluses dans ce package</span><span class="sxs-lookup"><span data-stu-id="48fa8-196">Preview features included in this package</span></span>
<span data-ttu-id="48fa8-197">Aucune.</span><span class="sxs-lookup"><span data-stu-id="48fa8-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="48fa8-198">En commençant par hello nouvelle [version générale d’un cluster d’autonome hello pour Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), vous pouvez mettre à niveau votre cluster toofuture les versions, manuellement ou automatiquement.</span><span class="sxs-lookup"><span data-stu-id="48fa8-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="48fa8-199">Consultez trop[mise à niveau d’une version autonome du cluster Service Fabric](service-fabric-cluster-upgrade-windows-server.md) document pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="48fa8-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="48fa8-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48fa8-200">Next steps</span></span>
* [<span data-ttu-id="48fa8-201">Déployer et supprimer des applications avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="48fa8-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="48fa8-202">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="48fa8-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="48fa8-203">Ajouter ou supprimer le cluster Service Fabric de nœuds tooa autonome</span><span class="sxs-lookup"><span data-stu-id="48fa8-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="48fa8-204">Mettre à niveau une version autonome du cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="48fa8-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="48fa8-205">Créer un cluster Service Fabric autonome avec des machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="48fa8-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="48fa8-206">Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows</span><span class="sxs-lookup"><span data-stu-id="48fa8-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="48fa8-207">Sécuriser un cluster autonome sur Windows à l’aide de certificats X509</span><span class="sxs-lookup"><span data-stu-id="48fa8-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
