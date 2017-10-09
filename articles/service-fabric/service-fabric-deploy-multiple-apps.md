---
title: aaaDeploy une application Node.js qui utilise MongoDB | Documents Microsoft
description: "Procédure pas à pas sur la façon de toopackage cluster à plusieurs tooan invité exécutables toodeploy Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="572ff-103">Déploiement de plusieurs exécutables invités</span><span class="sxs-lookup"><span data-stu-id="572ff-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="572ff-104">Cet article explique comment toopackage et déployer plusieurs tooAzure d’exécutables invité Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="572ff-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="572ff-105">Pour créer et déployer un seul package Service Fabric lisent comment trop[déployer une infrastructure de tooService exécutable invité](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="572ff-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="572ff-106">Pendant cette procédure pas à pas montre comment toodeploy une application avec un frontal Node.js qui utilise MongoDB comme magasin de données hello, vous pouvez appliquer une hello étapes tooany application qui a des dépendances sur une autre application.</span><span class="sxs-lookup"><span data-stu-id="572ff-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="572ff-107">Vous pouvez utiliser le package d’application Visual Studio tooproduce hello qui contient plusieurs exécutables invité.</span><span class="sxs-lookup"><span data-stu-id="572ff-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="572ff-108">Consultez [à l’aide de Visual Studio toopackage une application existante](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="572ff-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="572ff-109">Une fois que vous avez ajouté le premier exécutable d’invité hello, clic droit sur le projet d’application hello et sélectionnez hello **Ajouter -> service du nouveau Service Fabric** tooadd hello deuxième invité projet exécutable toohello solution.</span><span class="sxs-lookup"><span data-stu-id="572ff-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="572ff-110">Remarque : Si vous choisissez la source de hello toolink Bonjour projet Visual Studio, la création de solutions de Visual Studio hello, sera vous assurer que votre package d’application est de toodate avec les modifications de source de hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="572ff-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="572ff-111">Samples</span></span>
* [<span data-ttu-id="572ff-112">Exemple pour empaqueter et déployer un fichier exécutable invité</span><span class="sxs-lookup"><span data-stu-id="572ff-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="572ff-113">Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="572ff-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="572ff-114">Manuellement le package hello plusieurs applications d’exécutable invité</span><span class="sxs-lookup"><span data-stu-id="572ff-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="572ff-115">Vous pouvez également créer manuellement package invité hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="572ff-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="572ff-116">Pour l’empaquetage manuel de hello, cet article utilise outil d’empaquetage Service Fabric hello, qui est disponible à l’adresse [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="572ff-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="572ff-117">Hello d’empaquetage application Node.js</span><span class="sxs-lookup"><span data-stu-id="572ff-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="572ff-118">Cet article suppose que Node.js n’est pas installé sur les nœuds hello dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="572ff-119">Par conséquent, vous devez toohello tooadd Node.exe répertoire de votre application de nœud avant l’empaquetage.</span><span class="sxs-lookup"><span data-stu-id="572ff-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="572ff-120">structure de répertoire Hello d’application de Node.js hello (à l’aide de la structure de web Express et modèle Jade) doit se présenter similaire toohello une ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="572ff-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="572ff-121">Comme prochaine étape, vous créez un package d’application pour hello application Node.js.</span><span class="sxs-lookup"><span data-stu-id="572ff-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="572ff-122">code Hello ci-dessous crée un package d’application Service Fabric qui contient l’application hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="572ff-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="572ff-123">Vous trouverez ci-dessous une description des paramètres de hello sont utilisées :</span><span class="sxs-lookup"><span data-stu-id="572ff-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="572ff-124">**/ source** Active toohello de points de l’application hello qui doit être insérée.</span><span class="sxs-lookup"><span data-stu-id="572ff-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="572ff-125">**/ target** définit le répertoire hello dans le hello package doit être créé.</span><span class="sxs-lookup"><span data-stu-id="572ff-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="572ff-126">Ce répertoire a toobe différent du répertoire source de hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="572ff-127">**appname** définit le nom de l’application hello d’application existant hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="572ff-128">Il est important toounderstand que cela se traduit par le nom de service toohello dans le manifeste de hello et pas toohello Service Fabric nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="572ff-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="572ff-129">**/exe** définit hello exécutable que Service Fabric est supposé dans ce cas la toolaunch, `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="572ff-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="572ff-130">**/Ma** définit l’argument hello hello toolaunch utilisé exécutable en cours.</span><span class="sxs-lookup"><span data-stu-id="572ff-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="572ff-131">Node.js n’est pas installé, le Service Fabric doit serveur de web Node.js toolaunch hello en exécutant `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="572ff-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="572ff-132">`/ma:'bin/www'`Indique à hello empaquetage outil toouse `bin/ma` en tant qu’argument hello pour node.exe.</span><span class="sxs-lookup"><span data-stu-id="572ff-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="572ff-133">**/ Type d’application** définit le nom de type hello Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="572ff-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="572ff-134">Si vous y accédez répertoire toohello qui a été spécifié dans le paramètre de /target hello, vous pouvez voir que cet outil hello a créé un package de Service Fabric entièrement fonctionnel comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="572ff-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="572ff-135">Hello ServiceManifest.xml généré a maintenant une section qui décrit la façon dont le serveur web de Node.js hello doit être lancée, comme indiqué dans l’extrait de code hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="572ff-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="572ff-136">Dans cet exemple, serveur web de Node.js hello écoute tooport 3000, vous avez besoin des informations de point de terminaison tooupdate hello dans le fichier de ServiceManifest.xml hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="572ff-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="572ff-137">Hello d’empaquetage MongoDB application</span><span class="sxs-lookup"><span data-stu-id="572ff-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="572ff-138">Maintenant que vous avez empaqueté application Node.js de hello, vous pouvez continuer et MongoDB du package.</span><span class="sxs-lookup"><span data-stu-id="572ff-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="572ff-139">Comme mentionné précédemment, les étapes hello que vous parcourez désormais ne sont pas tooNode.js spécifique et MongoDB.</span><span class="sxs-lookup"><span data-stu-id="572ff-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="572ff-140">En fait, elles s’appliquent tooall applications destinés toobe sont fourni comme une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="572ff-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="572ff-141">toopackage MongoDB, que vous souhaitiez toomake que vous créez le package Mongod.exe et Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="572ff-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="572ff-142">Les deux fichiers binaires se trouvent dans hello `bin` répertoire de votre répertoire d’installation MongoDB.</span><span class="sxs-lookup"><span data-stu-id="572ff-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="572ff-143">structure de répertoire Hello recherche similaire toohello un ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="572ff-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="572ff-144">Service Fabric doit toostart MongoDB avec une commande de toohello similaire une ci-dessous, vous devez toouse hello `/ma` paramètre lors de l’empaquetage MongoDB.</span><span class="sxs-lookup"><span data-stu-id="572ff-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="572ff-145">les données de salutation ne sont pas conservées dans les cas de hello d’une défaillance de nœud si vous placez le répertoire de données MongoDB hello sur le répertoire local de hello du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="572ff-146">Vous devez utiliser un stockage durable ou implémenter un jeu en ordre tooprevent une perte de données de réplicas de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="572ff-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="572ff-147">Dans l’interface de commande PowerShell ou hello, nous exécutez outil d’empaquetage hello avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="572ff-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="572ff-148">Dans l’ordre tooadd MongoDB tooyour Service Fabric package d’application, vous devez toomake Vérifiez ce paramètre de /target hello pointe toohello même répertoire qui contient déjà le manifeste de l’application hello en même temps que l’application de Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="572ff-149">Vous devez également toomake que vous utilisez hello même applicationtype en nom.</span><span class="sxs-lookup"><span data-stu-id="572ff-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="572ff-150">Nous allons Explorer toohello répertoire et examinez quel outil hello a créé.</span><span class="sxs-lookup"><span data-stu-id="572ff-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="572ff-151">Comme vous pouvez le voir, outil de hello ajouté un nouveau répertoire toohello de dossier, MongoDB, qui contient les fichiers binaires de MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="572ff-152">Si vous ouvrez hello `ApplicationManifest.xml` fichier, vous pouvez voir ce package hello contient maintenant des applications de Node.js hello et MongoDB.</span><span class="sxs-lookup"><span data-stu-id="572ff-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="572ff-153">code Hello ci-dessous affiche hello le contenu du manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="572ff-154">Application de publication hello</span><span class="sxs-lookup"><span data-stu-id="572ff-154">Publishing hello application</span></span>
<span data-ttu-id="572ff-155">dernière étape de Hello est toopublish hello toohello local Service Fabric cluster d’application à l’aide de scripts PowerShell hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="572ff-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="572ff-156">Une fois l’application hello toohello a été publié correctement les cluster local, vous pouvez accéder application Node.js de hello sur le port hello que nous avons entré dans le manifeste du service d’application de Node.js hello--http://localhost:3000 par exemple hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="572ff-157">Dans ce didacticiel, vous avez vu comment tooeasily package deux applications existantes en tant qu’une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="572ff-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="572ff-158">Vous avez également appris comment toodeploy il tooService Fabric afin qu’elle peut tirer parti des hello des fonctionnalités de l’infrastructure de Service, tels que l’intégration de système haute disponibilité et intégrité des.</span><span class="sxs-lookup"><span data-stu-id="572ff-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="572ff-159">Ajout d’une application existante tooan invité exécutables plus à l’aide de Yeoman sur Linux</span><span class="sxs-lookup"><span data-stu-id="572ff-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="572ff-160">tooadd une autre application de tooan service déjà créé à l’aide de `yo`, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="572ff-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="572ff-161">Modifier la racine toohello du répertoire d’application existant hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="572ff-162">Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="572ff-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="572ff-163">Exécutez `yo azuresfguest:AddService` et fournir les informations nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="572ff-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="572ff-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="572ff-164">Next steps</span></span>
* <span data-ttu-id="572ff-165">En savoir plus sur le déploiement de conteneurs avec [Service Fabric et vue d’ensemble des conteneurs](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="572ff-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="572ff-166">Exemple pour empaqueter et déployer un fichier exécutable invité</span><span class="sxs-lookup"><span data-stu-id="572ff-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="572ff-167">Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="572ff-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
