---
title: aaaPackage une application Azure Service Fabric | Documents Microsoft
description: "Comment toopackage une application de Service Fabric avant le déploiement de cluster de tooa."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="926ef-103">Empaqueter une application</span><span class="sxs-lookup"><span data-stu-id="926ef-103">Package an application</span></span>
<span data-ttu-id="926ef-104">Cet article décrit comment toopackage une application de Service Fabric et prêt pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="926ef-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="926ef-105">Disposition du package</span><span class="sxs-lookup"><span data-stu-id="926ef-105">Package layout</span></span>
<span data-ttu-id="926ef-106">manifeste de l’application Hello, un ou plusieurs manifestes de service et autres fichiers doivent être organisés dans une disposition spécifique pour le déploiement dans un cluster Service Fabric de package nécessaires.</span><span class="sxs-lookup"><span data-stu-id="926ef-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="926ef-107">manifestes d’exemple Hello dans cet article, vous devez toobe organisé dans hello suivant la structure de répertoires :</span><span class="sxs-lookup"><span data-stu-id="926ef-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="926ef-108">les dossiers de Hello sont nommés toomatch hello **nom** les attributs de chaque élément correspondant.</span><span class="sxs-lookup"><span data-stu-id="926ef-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="926ef-109">Par exemple, si hello manifeste de service contenu deux packages de code avec des noms hello **MyCodeA** et **MyCodeB**, puis deux dossiers par hello contient des mêmes noms hello les fichiers binaires nécessaires pour chaque code package.</span><span class="sxs-lookup"><span data-stu-id="926ef-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="926ef-110">Utilisation de SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="926ef-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="926ef-111">Scénarios courants d’utilisation **SetupEntryPoint** sont lorsque vous devez toorun un exécutable avant le démarrage du service hello ou tooperform une opération avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="926ef-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="926ef-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="926ef-112">For example:</span></span>

* <span data-ttu-id="926ef-113">Configuration et l’initialisation des variables d’environnement qui hello besoins exécutable du service.</span><span class="sxs-lookup"><span data-stu-id="926ef-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="926ef-114">Il n’est pas exécutables tooonly limitée par le biais de modèles de programmation de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="926ef-115">Par exemple, npm.exe a besoin de certaines variables d’environnement configurées pour le déploiement d’une application node.js.</span><span class="sxs-lookup"><span data-stu-id="926ef-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="926ef-116">La configuration d’un contrôle d’accès via l’installation de certificats de sécurité.</span><span class="sxs-lookup"><span data-stu-id="926ef-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="926ef-117">Pour plus d’informations sur la façon de tooconfigure hello **SetupEntryPoint**, consultez [configurer une stratégie de hello pour un point d’entrée de service d’installation](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="926ef-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="926ef-118">Configuration</span><span class="sxs-lookup"><span data-stu-id="926ef-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="926ef-119">Création d'un package à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="926ef-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="926ef-120">Si vous utilisez Visual Studio 2015 toocreate votre application, vous pouvez utiliser hello Package tooautomatically de la commande Créer un package qui correspond à la disposition de hello décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="926ef-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="926ef-121">toocreate un package, avec le bouton droit de projet d’application hello dans l’Explorateur de solutions et choisissez la commande de Package hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="926ef-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Empaquetage d'une application avec Visual Studio][vs-package-command]

<span data-ttu-id="926ef-123">Lors de l’empaquetage est terminé, vous pouvez trouver emplacement hello du package de hello Bonjour **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="926ef-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="926ef-124">étape d’empaquetage Hello se produit automatiquement lorsque vous déployez ou que vous déboguez votre application dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="926ef-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="926ef-125">Développer un package par ligne de commande</span><span class="sxs-lookup"><span data-stu-id="926ef-125">Build a package by command line</span></span>
<span data-ttu-id="926ef-126">Il est également possible tooprogrammatically package votre application à l’aide de `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="926ef-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="926ef-127">Dans les coulisses hello, Visual Studio est en cours d’exécution il afin de la sortie de hello est identique.</span><span class="sxs-lookup"><span data-stu-id="926ef-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="926ef-128">Package de test de hello</span><span class="sxs-lookup"><span data-stu-id="926ef-128">Test hello package</span></span>
<span data-ttu-id="926ef-129">Vous pouvez vérifier la structure du package hello localement par le biais de PowerShell à l’aide de hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) commande.</span><span class="sxs-lookup"><span data-stu-id="926ef-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="926ef-130">Cette commande vérifie la présence de problèmes liés à l’analyse du manifeste, ainsi que toutes les références.</span><span class="sxs-lookup"><span data-stu-id="926ef-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="926ef-131">Cette commande vérifie uniquement l’exactitude structurelle de hello de répertoires de hello et fichiers de package de hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="926ef-132">Il ne vérifie pas les hello code ou les données du contenu du package au-delà de la vérification que tous les fichiers nécessaires sont présents.</span><span class="sxs-lookup"><span data-stu-id="926ef-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="926ef-133">Cette erreur indique que hello *MySetup.bat* fichier référencé dans le manifeste de service hello **SetupEntryPoint** est absent du package de code hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="926ef-134">Après avoir ajouté les fichiers manquants hello, vérification des applications hello passe :</span><span class="sxs-lookup"><span data-stu-id="926ef-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="926ef-135">Si des [paramètres d’application](service-fabric-manage-multiple-environment-app-configuration.md) sont définis pour votre application, vous pouvez les transmettre dans [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) pour assurer une validation correcte.</span><span class="sxs-lookup"><span data-stu-id="926ef-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="926ef-136">Si vous connaissez le cluster hello où hello application sera déployée, il est recommandé de vous transmettez hello `ImageStoreConnectionString` paramètre.</span><span class="sxs-lookup"><span data-stu-id="926ef-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="926ef-137">Dans ce cas, le package de hello est également validée par rapport aux versions précédentes de l’application hello qui sont déjà en cours d’exécution dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="926ef-138">Par exemple, la validation hello peut détecter si un package avec hello même version mais un contenu différent a déjà été déployé.</span><span class="sxs-lookup"><span data-stu-id="926ef-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="926ef-139">Une fois que l’application hello est correctement empaquetée et passe la validation, évaluer en fonction de la taille de hello et nombre hello de fichiers si la compression n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="926ef-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="926ef-140">Compresser un package</span><span class="sxs-lookup"><span data-stu-id="926ef-140">Compress a package</span></span>
<span data-ttu-id="926ef-141">Lorsqu’un package est volumineux ou contient de nombreux fichiers, vous pouvez le compresser afin d’accélérer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="926ef-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="926ef-142">La compression réduit le nombre de hello de fichiers et de la taille du package hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="926ef-143">Pour un package d’application compressé [package d’application hello transfert](service-fabric-deploy-remove-applications.md#upload-the-application-package) peut prendre plus de comparés toouploading hello package décompressé (spécialement si le temps de la compression est pris en compte), mais [inscription](service-fabric-deploy-remove-applications.md#register-the-application-package) et [type désinscription de l’application hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sont plus rapides pour un package d’application compressé.</span><span class="sxs-lookup"><span data-stu-id="926ef-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="926ef-144">mécanisme de déploiement Hello est identique pour les packages compressées et non compressées.</span><span class="sxs-lookup"><span data-stu-id="926ef-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="926ef-145">Si le package de hello est compressé, il est compressé sur le nœud de hello avant l’exécution d’application hello et il est stocké en tant que tel dans le magasin d’images hello cluster.</span><span class="sxs-lookup"><span data-stu-id="926ef-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="926ef-146">la compression de Hello remplace le package de Service Fabric hello valide avec une version compressée de hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="926ef-147">dossier de Hello doit autoriser des autorisations en écriture.</span><span class="sxs-lookup"><span data-stu-id="926ef-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="926ef-148">L’exécution d’une compression sur un package déjà compressé ne produit aucun effet.</span><span class="sxs-lookup"><span data-stu-id="926ef-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="926ef-149">Vous pouvez compresser un package en exécutant la commande Powershell de hello [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec `CompressPackage` basculer.</span><span class="sxs-lookup"><span data-stu-id="926ef-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="926ef-150">Vous pouvez décompresser hello le package avec hello identique à l’aide de la commande `UncompressPackage` basculer.</span><span class="sxs-lookup"><span data-stu-id="926ef-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="926ef-151">Hello commande suivant compresse les package hello sans le copier toohello magasin d’images.</span><span class="sxs-lookup"><span data-stu-id="926ef-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="926ef-152">Vous pouvez copier un tooone package compressé ou plus de clusters Service Fabric, si nécessaire, à l’aide de [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sans hello `SkipCopy` indicateur.</span><span class="sxs-lookup"><span data-stu-id="926ef-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="926ef-153">package de Hello inclut désormais les fichiers compressés pour hello `code`, `config`, et `data` packages.</span><span class="sxs-lookup"><span data-stu-id="926ef-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="926ef-154">manifeste de l’application Hello et hello manifestes ne sont pas compressés, car ils sont nécessaires pour de nombreuses opérations internes (par exemple, le package d’application type nom et la version d’extraction pour certains contrôles, de partage).</span><span class="sxs-lookup"><span data-stu-id="926ef-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="926ef-155">Les manifestes hello zip rend ces opérations inefficaces.</span><span class="sxs-lookup"><span data-stu-id="926ef-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="926ef-156">Ou bien, vous pouvez compresser et copier le package hello avec [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) en une seule étape.</span><span class="sxs-lookup"><span data-stu-id="926ef-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="926ef-157">Si le package de hello est volumineux, fournissent un délai tooallow suffisamment élevé pour la compression du package hello et cluster de toohello téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="926ef-158">En interne, l’infrastructure de Service calcule les sommes de contrôle pour les packages d’application hello pour la validation.</span><span class="sxs-lookup"><span data-stu-id="926ef-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="926ef-159">Lorsque vous utilisez la compression, les sommes de contrôle hello sont calculées sur hello compressé des versions de chaque package.</span><span class="sxs-lookup"><span data-stu-id="926ef-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="926ef-160">Si vous avez copié une version non compressée de votre package d’application et que vous souhaitez la compression toouse hello même package, vous devez modifier les versions hello Hello `code`, `config`, et `data` non-concordance de somme de contrôle tooavoid de packages.</span><span class="sxs-lookup"><span data-stu-id="926ef-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="926ef-161">Si les packages hello restent inchangées, au lieu de modifier la version de hello, vous pouvez utiliser [diff approvisionnement](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="926ef-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="926ef-162">Avec cette option, n’incluez pas de package d’inchangée hello à la place de la référence de manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="926ef-163">De même, si vous avez téléchargé une version compressée du package de hello et que vous souhaitez toouse un package décompressé, vous devez mettre à jour non-concordance de somme de contrôle hello versions tooavoid hello.</span><span class="sxs-lookup"><span data-stu-id="926ef-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="926ef-164">Hello package est désormais correctement empaqueté, validé et compressé (si nécessaire), par conséquent, il est prêt pour [déploiement](service-fabric-deploy-remove-applications.md) tooone ou plus Service Fabric des clusters.</span><span class="sxs-lookup"><span data-stu-id="926ef-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="926ef-165">Compresser les packages lors du déploiement via Visual Studio</span><span class="sxs-lookup"><span data-stu-id="926ef-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="926ef-166">Vous pouvez demander à des packages de toocompress Visual Studio sur le déploiement, en ajoutant hello `CopyPackageParameters` élément tooyour profil de publication et définissez hello `CompressPackage` trop d’attributs`true`.</span><span class="sxs-lookup"><span data-stu-id="926ef-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="926ef-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="926ef-167">Next steps</span></span>
<span data-ttu-id="926ef-168">[Déployer et supprimer des applications] [ 10] décrit comment instances d’application toomanage toouse PowerShell</span><span class="sxs-lookup"><span data-stu-id="926ef-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="926ef-169">[Gestion des paramètres d’application de plusieurs environnements] [ 11] décrit comment tooconfigure paramètres et variables d’environnement pour les instances de l’autre application.</span><span class="sxs-lookup"><span data-stu-id="926ef-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="926ef-170">[Configurer des stratégies de sécurité pour votre application] [ 12] décrit comment les services toorun sous toorestrict accès aux stratégies de sécurité.</span><span class="sxs-lookup"><span data-stu-id="926ef-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
