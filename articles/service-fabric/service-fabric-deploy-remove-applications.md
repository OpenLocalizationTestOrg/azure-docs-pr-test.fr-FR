---
title: "aaaAzure déploiement d’application Service Fabric | Documents Microsoft"
description: "Comment toodeploy et supprimez les applications dans l’infrastructure de Service à l’aide de PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="be0f0-103">Déployer et supprimer des applications avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="be0f0-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be0f0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be0f0-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="be0f0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="be0f0-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="be0f0-106">API FabricClient</span><span class="sxs-lookup"><span data-stu-id="be0f0-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="be0f0-107">Après avoir [packagé un type d’application][10], celui-ci peut être déployé sur un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="be0f0-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="be0f0-108">Le déploiement implique hello trois comme suit :</span><span class="sxs-lookup"><span data-stu-id="be0f0-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="be0f0-109">Télécharger le magasin d’images hello application package toohello</span><span class="sxs-lookup"><span data-stu-id="be0f0-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="be0f0-110">Inscrire le type d’application hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-110">Register hello application type</span></span>
3. <span data-ttu-id="be0f0-111">Créer l’instance de l’application hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-111">Create hello application instance</span></span>

<span data-ttu-id="be0f0-112">Après le déploiement d’une application et une instance est en cours d’exécution dans un cluster de hello, vous pouvez supprimer l’instance de l’application hello et son type d’application.</span><span class="sxs-lookup"><span data-stu-id="be0f0-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="be0f0-113">suppression de toocompletely une application à partir du cluster de hello implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="be0f0-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="be0f0-114">Supprimer (ou supprimer) hello instance d’application en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="be0f0-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="be0f0-115">Annuler l’inscription du type de l’application hello si elle n’est plus nécessaire</span><span class="sxs-lookup"><span data-stu-id="be0f0-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="be0f0-116">Supprimer le package d’application hello à partir du magasin d’images hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="be0f0-117">Si vous utilisez [Visual Studio pour déployer et déboguer des applications](service-fabric-publish-app-remote-cluster.md) sur votre cluster de développement local, tous les hello étapes précédentes sont gérées automatiquement via un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be0f0-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="be0f0-118">Ce script se trouve dans hello *Scripts* dossier du projet d’application hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="be0f0-119">Cet article des informations générales sur ce que fait ce script afin que vous puissiez effectuer hello les mêmes opérations en dehors de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be0f0-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="be0f0-120">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="be0f0-120">Connect toohello cluster</span></span>
<span data-ttu-id="be0f0-121">Avant d’exécuter les commandes PowerShell dans cet article, commencent toujours à l’aide de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cluster Service Fabric de toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="be0f0-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="be0f0-122">cluster de développement local toohello tooconnect, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="be0f0-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="be0f0-123">Pour obtenir des exemples de connexion à distance du cluster tooa ou du cluster sécurisé à l’aide d’Azure Active Directory, X509 des certificats ou les voir Windows Active Directory [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="be0f0-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="be0f0-124">Télécharger le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-124">Upload hello application package</span></span>
<span data-ttu-id="be0f0-125">Téléchargement du package application hello place dans un emplacement accessible par les composants de l’infrastructure de Service internes.</span><span class="sxs-lookup"><span data-stu-id="be0f0-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="be0f0-126">Si vous souhaitez que le package d’application hello tooverify localement, utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="be0f0-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="be0f0-127">Hello [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) commande téléchargements hello magasin d’images application package toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="be0f0-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="be0f0-128">Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be0f0-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="be0f0-129">module du Kit de développement logiciel de hello tooimport, exécutez :</span><span class="sxs-lookup"><span data-stu-id="be0f0-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="be0f0-130">Supposons que vous génériez une application nommée *MyApplication* et que vous créiez un package pour cette application dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="be0f0-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="be0f0-131">Par défaut, le nom de type l’application hello répertorié dans hello ApplicationManifest.xml est « MyApplicationType ».</span><span class="sxs-lookup"><span data-stu-id="be0f0-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="be0f0-132">package d’application, qui contient le manifeste d’application nécessaire hello, manifestes de service et des packages de code/config/données, Hello se trouve dans *C:\Users\<nom d’utilisateur\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="be0f0-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="be0f0-133">Hello commande suivante répertorie contenu hello hello du package d’application :</span><span class="sxs-lookup"><span data-stu-id="be0f0-133">hello following command lists hello contents of hello application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="be0f0-134">Si le package d’application hello est grande et/ou de fichiers, vous pouvez [compresser](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="be0f0-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="be0f0-135">la compression de Hello réduit la taille de hello et nombre hello de fichiers.</span><span class="sxs-lookup"><span data-stu-id="be0f0-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="be0f0-136">Hello effet secondaire est que hello inscription et désinscription type d’application sont plus rapides.</span><span class="sxs-lookup"><span data-stu-id="be0f0-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="be0f0-137">Temps de téléchargement peut être plus lent actuellement, notamment si vous incluez le package de hello temps toocompress hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="be0f0-138">toocompress un package, utilisez hello même [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) commande.</span><span class="sxs-lookup"><span data-stu-id="be0f0-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="be0f0-139">La compression peut faire distinct à partir de téléchargement, à l’aide hello `SkipCopy` indicateur ou opération de téléchargement avec hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="be0f0-140">L’application d’une compression sur un package compressé n’a aucun effet.</span><span class="sxs-lookup"><span data-stu-id="be0f0-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="be0f0-141">toouncompress un package compressé, utilisez hello même [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec hello `UncompressPackage` basculer.</span><span class="sxs-lookup"><span data-stu-id="be0f0-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="be0f0-142">Hello applet de commande suivante compresse les package hello sans le copier toohello magasin d’images.</span><span class="sxs-lookup"><span data-stu-id="be0f0-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="be0f0-143">package de Hello inclut désormais les fichiers compressés pour hello `Code` et `Config` packages.</span><span class="sxs-lookup"><span data-stu-id="be0f0-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="be0f0-144">Hello manifestes d’application et hello service ne sont pas compressés, car ils sont nécessaires pour de nombreuses opérations internes (par exemple, le package d’application type nom et la version d’extraction pour certains contrôles, de partage).</span><span class="sxs-lookup"><span data-stu-id="be0f0-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="be0f0-145">Les manifestes hello zip rend ces opérations inefficaces.</span><span class="sxs-lookup"><span data-stu-id="be0f0-145">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="be0f0-146">Pour les packages d’application de grande taille, la compression de hello du temps.</span><span class="sxs-lookup"><span data-stu-id="be0f0-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="be0f0-147">Pour obtenir de meilleurs résultats, utilisez un disque SSD rapide.</span><span class="sxs-lookup"><span data-stu-id="be0f0-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="be0f0-148">les durées de compression Hello et taille hello de package compressé de hello diffèrent également selon le contenu du package hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="be0f0-149">Par exemple, Voici des statistiques de compression de certains packages affichent hello initiale et hello taille du package compressé, avec le temps de compression hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="be0f0-150">Taille initiale (Mo)</span><span class="sxs-lookup"><span data-stu-id="be0f0-150">Initial size (MB)</span></span>|<span data-ttu-id="be0f0-151">Nombre de fichiers</span><span class="sxs-lookup"><span data-stu-id="be0f0-151">File count</span></span>|<span data-ttu-id="be0f0-152">Temps de compression</span><span class="sxs-lookup"><span data-stu-id="be0f0-152">Compression Time</span></span>|<span data-ttu-id="be0f0-153">Taille du package compressé (Mo)</span><span class="sxs-lookup"><span data-stu-id="be0f0-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="be0f0-154">100</span><span class="sxs-lookup"><span data-stu-id="be0f0-154">100</span></span>|<span data-ttu-id="be0f0-155">100</span><span class="sxs-lookup"><span data-stu-id="be0f0-155">100</span></span>|<span data-ttu-id="be0f0-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="be0f0-156">00:00:03.3547592</span></span>|<span data-ttu-id="be0f0-157">60</span><span class="sxs-lookup"><span data-stu-id="be0f0-157">60</span></span>|
|<span data-ttu-id="be0f0-158">512</span><span class="sxs-lookup"><span data-stu-id="be0f0-158">512</span></span>|<span data-ttu-id="be0f0-159">100</span><span class="sxs-lookup"><span data-stu-id="be0f0-159">100</span></span>|<span data-ttu-id="be0f0-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="be0f0-160">00:00:16.3850303</span></span>|<span data-ttu-id="be0f0-161">307</span><span class="sxs-lookup"><span data-stu-id="be0f0-161">307</span></span>|
|<span data-ttu-id="be0f0-162">1 024</span><span class="sxs-lookup"><span data-stu-id="be0f0-162">1024</span></span>|<span data-ttu-id="be0f0-163">500</span><span class="sxs-lookup"><span data-stu-id="be0f0-163">500</span></span>|<span data-ttu-id="be0f0-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="be0f0-164">00:00:32.5907950</span></span>|<span data-ttu-id="be0f0-165">615</span><span class="sxs-lookup"><span data-stu-id="be0f0-165">615</span></span>|
|<span data-ttu-id="be0f0-166">2 048</span><span class="sxs-lookup"><span data-stu-id="be0f0-166">2048</span></span>|<span data-ttu-id="be0f0-167">1 000</span><span class="sxs-lookup"><span data-stu-id="be0f0-167">1000</span></span>|<span data-ttu-id="be0f0-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="be0f0-168">00:01:04.3775554</span></span>|<span data-ttu-id="be0f0-169">1231</span><span class="sxs-lookup"><span data-stu-id="be0f0-169">1231</span></span>|
|<span data-ttu-id="be0f0-170">5012</span><span class="sxs-lookup"><span data-stu-id="be0f0-170">5012</span></span>|<span data-ttu-id="be0f0-171">100</span><span class="sxs-lookup"><span data-stu-id="be0f0-171">100</span></span>|<span data-ttu-id="be0f0-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="be0f0-172">00:02:45.2951288</span></span>|<span data-ttu-id="be0f0-173">3074</span><span class="sxs-lookup"><span data-stu-id="be0f0-173">3074</span></span>|

<span data-ttu-id="be0f0-174">Une fois qu’un package est compressé, il peut être téléchargé tooone plusieurs Service Fabric de clusters ou en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="be0f0-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="be0f0-175">mécanisme de déploiement Hello est identique pour les packages compressées et non compressées.</span><span class="sxs-lookup"><span data-stu-id="be0f0-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="be0f0-176">Si le package de hello est compressé, il est compressé sur le nœud de hello avant l’exécution d’application hello et il est stocké en tant que tel dans le magasin d’images hello cluster.</span><span class="sxs-lookup"><span data-stu-id="be0f0-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="be0f0-177">Hello exemple suivant télécharge magasin d’images package toohello hello, dans un dossier nommé « MyApplicationV1 » :</span><span class="sxs-lookup"><span data-stu-id="be0f0-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="be0f0-178">Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be0f0-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="be0f0-179">module du Kit de développement logiciel de hello tooimport, exécutez :</span><span class="sxs-lookup"><span data-stu-id="be0f0-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="be0f0-180">Si vous ne spécifiez pas hello *- ApplicationPackagePathInImageStore* paramètre, le package d’application hello est copié dans le dossier de « Debug » hello dans le magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="be0f0-181">Hello temps tooupload un package diffère selon plusieurs facteurs.</span><span class="sxs-lookup"><span data-stu-id="be0f0-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="be0f0-182">Certains de ces facteurs sont nombre hello de fichiers dans le package de hello, la taille du package hello et tailles de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="be0f0-183">vitesse du réseau entre l’ordinateur de source de hello et cluster Service Fabric de hello Hello affecte également le temps de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="be0f0-184">Hello de délai d’attente par défaut pour [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) est de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="be0f0-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="be0f0-185">En fonction de hello facteurs décrits, vous devrez peut-être le délai d’attente de tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="be0f0-186">Si vous compressez des package hello dans l’appel de copie hello, vous devez tooalso prendre en compte le temps de compression hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="be0f0-187">Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be0f0-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="be0f0-188">Enregistrer le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-188">Register hello application package</span></span>
<span data-ttu-id="be0f0-189">type d’application Hello et la version déclaré dans le manifeste de l’application hello deviennent disponible lorsque le package d’application hello est inscrit.</span><span class="sxs-lookup"><span data-stu-id="be0f0-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="be0f0-190">système de Hello lit package hello téléchargé à l’étape précédente de hello, vérifie les package hello, traite le contenu du package hello et copie l’emplacement du système interne hello traité package tooan.</span><span class="sxs-lookup"><span data-stu-id="be0f0-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="be0f0-191">Exécutez hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister de l’applet de commande hello du type d’application dans un cluster de hello et le rendre disponible pour le déploiement :</span><span class="sxs-lookup"><span data-stu-id="be0f0-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="be0f0-192">« MyApplicationV1 » est hello dans le magasin d’images hello où se trouve le package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="be0f0-193">type d’application Hello avec le nom « MyApplicationType » et la version « 1.0.0 » (les deux se trouvent dans le manifeste de l’application hello) est maintenant inscrit dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="be0f0-194">Hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) commande retourne uniquement une fois le système de hello a package d’application hello correctement inscrit.</span><span class="sxs-lookup"><span data-stu-id="be0f0-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="be0f0-195">La durée pendant laquelle l’enregistrement prend dépend de taille de hello et le contenu du package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="be0f0-196">Si nécessaire, hello **- TimeoutSec** paramètre peut être utilisé toosupply un délai d’attente plus long (le délai d’attente de hello par défaut est 60 secondes).</span><span class="sxs-lookup"><span data-stu-id="be0f0-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="be0f0-197">Si vous avez une grande application du package ou si vous rencontrez des délais d’attente, utilisez hello **- Async** paramètre.</span><span class="sxs-lookup"><span data-stu-id="be0f0-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="be0f0-198">commande Hello retourne lorsque le cluster de hello accepte une commande de Registre hello et le traitement de hello continue en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="be0f0-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="be0f0-199">Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="be0f0-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="be0f0-200">Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="be0f0-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="be0f0-201">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-201">Create hello application</span></span>
<span data-ttu-id="be0f0-202">Vous pouvez instancier une application à partir de n’importe quelle version de type d’application qui a été inscrit avec succès à l’aide de hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="be0f0-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="be0f0-203">nom Hello de chaque application doit commencer par hello *« fabric : «* schéma et doit être unique pour chaque instance d’application.</span><span class="sxs-lookup"><span data-stu-id="be0f0-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="be0f0-204">Tous les services par défaut définis dans le manifeste de l’application hello hello cible du type d’application sont également créés.</span><span class="sxs-lookup"><span data-stu-id="be0f0-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="be0f0-205">Plusieurs instances d'application peuvent être créées pour une version donnée d'un type d'application enregistré.</span><span class="sxs-lookup"><span data-stu-id="be0f0-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="be0f0-206">Chaque instance de l’application s’exécute en isolement, avec ses propres répertoire de travail et processus.</span><span class="sxs-lookup"><span data-stu-id="be0f0-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="be0f0-207">toosee dont le nom des applications et services sont en cours d’exécution dans le cluster hello, exécutez hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) et [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) applets de commande :</span><span class="sxs-lookup"><span data-stu-id="be0f0-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="be0f0-208">Supprimer une application</span><span class="sxs-lookup"><span data-stu-id="be0f0-208">Remove an application</span></span>
<span data-ttu-id="be0f0-209">Lorsqu’une instance d’application n’est plus nécessaire, vous pouvez le supprimer définitivement par son nom hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="be0f0-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="be0f0-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) supprime automatiquement tous les services qui appartiennent application toohello également, définitivement suppression de tous les États de service.</span><span class="sxs-lookup"><span data-stu-id="be0f0-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="be0f0-211">Cette opération ne peut pas être annulée et l’état de l’application ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="be0f0-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="be0f0-212">Désinscrire un type d’application</span><span class="sxs-lookup"><span data-stu-id="be0f0-212">Unregister an application type</span></span>
<span data-ttu-id="be0f0-213">Lorsqu’une version particulière d’un type d’application n’est plus nécessaire, vous devez annuler l’inscription de type d’application hello à l’aide de hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="be0f0-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="be0f0-214">Lors de la désinscription application inutilisées types versions espace de stockage utilisé par le magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="be0f0-215">Vous pouvez désinscrire un type d’application s’il ne contient aucune instance d’application et s’il n’est référencé par aucune mise à niveau d’application en attente.</span><span class="sxs-lookup"><span data-stu-id="be0f0-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="be0f0-216">Exécutez [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) types d’application hello toosee actuellement inscrits dans le cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="be0f0-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="be0f0-217">Exécutez [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un type d’application spécifique :</span><span class="sxs-lookup"><span data-stu-id="be0f0-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="be0f0-218">Supprimer un package d’application à partir du magasin d’images hello</span><span class="sxs-lookup"><span data-stu-id="be0f0-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="be0f0-219">Lorsqu’un package d’application n’est plus nécessaire, vous pouvez la supprimer hello image store toofree des ressources système.</span><span class="sxs-lookup"><span data-stu-id="be0f0-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="be0f0-220">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="be0f0-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="be0f0-221">Copy-ServiceFabricApplicationPackage demande un ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="be0f0-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="be0f0-222">environnement de Service Fabric SDK Hello doit déjà avoir hello correct à configurer des paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="be0f0-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="be0f0-223">Mais si nécessaire, hello ImageStoreConnectionString pour toutes les commandes doit correspondre à hello valeur ce hello Service Fabric à l’aide de cluster.</span><span class="sxs-lookup"><span data-stu-id="be0f0-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="be0f0-224">Vous pouvez trouver hello ImageStoreConnectionString dans le manifeste du cluster hello, récupéré à l’aide de hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) et les commandes Get-ImageStoreConnectionStringFromClusterManifest :</span><span class="sxs-lookup"><span data-stu-id="be0f0-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="be0f0-225">Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be0f0-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="be0f0-226">module du Kit de développement logiciel de hello tooimport, exécutez :</span><span class="sxs-lookup"><span data-stu-id="be0f0-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="be0f0-227">Hello ImageStoreConnectionString se trouve dans le manifeste du cluster hello :</span><span class="sxs-lookup"><span data-stu-id="be0f0-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="be0f0-228">Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be0f0-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="be0f0-229">Déployer un package d’application volumineux</span><span class="sxs-lookup"><span data-stu-id="be0f0-229">Deploy large application package</span></span>
<span data-ttu-id="be0f0-230">Problème : la commande [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) expire pour un package d’application volumineux (de l’ordre du gigaoctet).</span><span class="sxs-lookup"><span data-stu-id="be0f0-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="be0f0-231">Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="be0f0-231">Try:</span></span>
- <span data-ttu-id="be0f0-232">Spécifiez un délai d’expiration supérieur pour la commande[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec le paramètre `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="be0f0-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="be0f0-233">Par défaut, le délai d’attente hello est 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="be0f0-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="be0f0-234">Vérifiez la connexion de réseau hello entre votre ordinateur source et le cluster.</span><span class="sxs-lookup"><span data-stu-id="be0f0-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="be0f0-235">Si hello connexion est lente, envisagez d’utiliser un ordinateur avec une connexion réseau mieux.</span><span class="sxs-lookup"><span data-stu-id="be0f0-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="be0f0-236">Si l’ordinateur client de hello est dans une autre région que le cluster de hello, envisagez d’utiliser un ordinateur client dans une région proche ou même en tant que cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="be0f0-237">Vérifiez si vous êtes confronté à des limitations externes.</span><span class="sxs-lookup"><span data-stu-id="be0f0-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="be0f0-238">Par exemple, lorsque le magasin d’images hello est configuré toouse azure storage, téléchargement peut être limité.</span><span class="sxs-lookup"><span data-stu-id="be0f0-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="be0f0-239">Problème : le chargement du package s’est terminé avec succès, mais la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) expire. Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="be0f0-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="be0f0-240">[Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="be0f0-241">la compression de Hello réduit la taille de hello et nombre hello de fichiers, qui à son tour réduit le trafic hello et utiliser ce Service Fabric doit effectuer.</span><span class="sxs-lookup"><span data-stu-id="be0f0-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="be0f0-242">opération de téléchargement de Hello peut être plus lente (surtout si vous incluez des temps de compression hello), mais le type d’application hello inscrire et désinscrire sont plus rapides.</span><span class="sxs-lookup"><span data-stu-id="be0f0-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="be0f0-243">Spécifiez un délai d’expiration supérieur pour la commande[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) avec le paramètre `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="be0f0-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="be0f0-244">Spécifiez le commutateur `Async` pour la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="be0f0-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="be0f0-245">commande Hello retourne lorsque le cluster de hello accepte une commande hello et inscription hello hello du type d’application se poursuit de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="be0f0-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="be0f0-246">Pour cette raison, il est sans toospecify besoin un délai d’attente plus élevé dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="be0f0-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="be0f0-247">Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="be0f0-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="be0f0-248">Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="be0f0-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="be0f0-249">Déployer un package d’application contenant de nombreux fichiers</span><span class="sxs-lookup"><span data-stu-id="be0f0-249">Deploy application package with many files</span></span>
<span data-ttu-id="be0f0-250">Problème : la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) expire pour un package d’application contenant un grand nombre de fichiers (de l’ordre de plusieurs milliers).</span><span class="sxs-lookup"><span data-stu-id="be0f0-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="be0f0-251">Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="be0f0-251">Try:</span></span>
- <span data-ttu-id="be0f0-252">[Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.</span><span class="sxs-lookup"><span data-stu-id="be0f0-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="be0f0-253">la compression de Hello réduit le nombre de hello de fichiers.</span><span class="sxs-lookup"><span data-stu-id="be0f0-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="be0f0-254">Spécifiez un délai d’expiration supérieur pour la commande[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) avec le paramètre `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="be0f0-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="be0f0-255">Spécifiez le commutateur `Async` pour la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="be0f0-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="be0f0-256">commande Hello retourne lorsque le cluster de hello accepte une commande hello et inscription hello hello du type d’application se poursuit de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="be0f0-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="be0f0-257">Pour cette raison, il est sans toospecify besoin un délai d’attente plus élevé dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="be0f0-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="be0f0-258">Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="be0f0-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="be0f0-259">Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="be0f0-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="be0f0-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be0f0-260">Next steps</span></span>
[<span data-ttu-id="be0f0-261">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be0f0-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="be0f0-262">Présentation de l’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be0f0-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="be0f0-263">Diagnostiquer et résoudre les problèmes d'un service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be0f0-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="be0f0-264">Modéliser une application dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="be0f0-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
