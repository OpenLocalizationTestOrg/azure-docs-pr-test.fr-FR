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
# <a name="deploy-multiple-guest-executables"></a>Déploiement de plusieurs exécutables invités
Cet article explique comment toopackage et déployer plusieurs tooAzure d’exécutables invité Service Fabric. Pour créer et déployer un seul package Service Fabric lisent comment trop[déployer une infrastructure de tooService exécutable invité](service-fabric-deploy-existing-app.md).

Pendant cette procédure pas à pas montre comment toodeploy une application avec un frontal Node.js qui utilise MongoDB comme magasin de données hello, vous pouvez appliquer une hello étapes tooany application qui a des dépendances sur une autre application.   

Vous pouvez utiliser le package d’application Visual Studio tooproduce hello qui contient plusieurs exécutables invité. Consultez [à l’aide de Visual Studio toopackage une application existante](service-fabric-deploy-existing-app.md). Une fois que vous avez ajouté le premier exécutable d’invité hello, clic droit sur le projet d’application hello et sélectionnez hello **Ajouter -> service du nouveau Service Fabric** tooadd hello deuxième invité projet exécutable toohello solution. Remarque : Si vous choisissez la source de hello toolink Bonjour projet Visual Studio, la création de solutions de Visual Studio hello, sera vous assurer que votre package d’application est de toodate avec les modifications de source de hello. 

## <a name="samples"></a>Exemples
* [Exemple pour empaqueter et déployer un fichier exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Manuellement le package hello plusieurs applications d’exécutable invité
Vous pouvez également créer manuellement package invité hello exécutable. Pour l’empaquetage manuel de hello, cet article utilise outil d’empaquetage Service Fabric hello, qui est disponible à l’adresse [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Hello d’empaquetage application Node.js
Cet article suppose que Node.js n’est pas installé sur les nœuds hello dans le cluster Service Fabric de hello. Par conséquent, vous devez toohello tooadd Node.exe répertoire de votre application de nœud avant l’empaquetage. structure de répertoire Hello d’application de Node.js hello (à l’aide de la structure de web Express et modèle Jade) doit se présenter similaire toohello une ci-dessous :

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

Comme prochaine étape, vous créez un package d’application pour hello application Node.js. code Hello ci-dessous crée un package d’application Service Fabric qui contient l’application hello Node.js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Vous trouverez ci-dessous une description des paramètres de hello sont utilisées :

* **/ source** Active toohello de points de l’application hello qui doit être insérée.
* **/ target** définit le répertoire hello dans le hello package doit être créé. Ce répertoire a toobe différent du répertoire source de hello.
* **appname** définit le nom de l’application hello d’application existant hello. Il est important toounderstand que cela se traduit par le nom de service toohello dans le manifeste de hello et pas toohello Service Fabric nom de l’application.
* **/exe** définit hello exécutable que Service Fabric est supposé dans ce cas la toolaunch, `node.exe`.
* **/Ma** définit l’argument hello hello toolaunch utilisé exécutable en cours. Node.js n’est pas installé, le Service Fabric doit serveur de web Node.js toolaunch hello en exécutant `node.exe bin/www`.  `/ma:'bin/www'`Indique à hello empaquetage outil toouse `bin/ma` en tant qu’argument hello pour node.exe.
* **/ Type d’application** définit le nom de type hello Service Fabric application.

Si vous y accédez répertoire toohello qui a été spécifié dans le paramètre de /target hello, vous pouvez voir que cet outil hello a créé un package de Service Fabric entièrement fonctionnel comme indiqué ci-dessous :

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
Hello ServiceManifest.xml généré a maintenant une section qui décrit la façon dont le serveur web de Node.js hello doit être lancée, comme indiqué dans l’extrait de code hello ci-dessous :

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
Dans cet exemple, serveur web de Node.js hello écoute tooport 3000, vous avez besoin des informations de point de terminaison tooupdate hello dans le fichier de ServiceManifest.xml hello comme indiqué ci-dessous.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Hello d’empaquetage MongoDB application
Maintenant que vous avez empaqueté application Node.js de hello, vous pouvez continuer et MongoDB du package. Comme mentionné précédemment, les étapes hello que vous parcourez désormais ne sont pas tooNode.js spécifique et MongoDB. En fait, elles s’appliquent tooall applications destinés toobe sont fourni comme une application de Service Fabric.  

toopackage MongoDB, que vous souhaitiez toomake que vous créez le package Mongod.exe et Mongo.exe. Les deux fichiers binaires se trouvent dans hello `bin` répertoire de votre répertoire d’installation MongoDB. structure de répertoire Hello recherche similaire toohello un ci-dessous.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric doit toostart MongoDB avec une commande de toohello similaire une ci-dessous, vous devez toouse hello `/ma` paramètre lors de l’empaquetage MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> les données de salutation ne sont pas conservées dans les cas de hello d’une défaillance de nœud si vous placez le répertoire de données MongoDB hello sur le répertoire local de hello du nœud de hello. Vous devez utiliser un stockage durable ou implémenter un jeu en ordre tooprevent une perte de données de réplicas de MongoDB.  
>
>

Dans l’interface de commande PowerShell ou hello, nous exécutez outil d’empaquetage hello avec hello paramètres suivants :

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

Dans l’ordre tooadd MongoDB tooyour Service Fabric package d’application, vous devez toomake Vérifiez ce paramètre de /target hello pointe toohello même répertoire qui contient déjà le manifeste de l’application hello en même temps que l’application de Node.js hello. Vous devez également toomake que vous utilisez hello même applicationtype en nom.

Nous allons Explorer toohello répertoire et examinez quel outil hello a créé.

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
Comme vous pouvez le voir, outil de hello ajouté un nouveau répertoire toohello de dossier, MongoDB, qui contient les fichiers binaires de MongoDB hello. Si vous ouvrez hello `ApplicationManifest.xml` fichier, vous pouvez voir ce package hello contient maintenant des applications de Node.js hello et MongoDB. code Hello ci-dessous affiche hello le contenu du manifeste d’application hello.

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

### <a name="publishing-hello-application"></a>Application de publication hello
dernière étape de Hello est toopublish hello toohello local Service Fabric cluster d’application à l’aide de scripts PowerShell hello ci-dessous :

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Une fois l’application hello toohello a été publié correctement les cluster local, vous pouvez accéder application Node.js de hello sur le port hello que nous avons entré dans le manifeste du service d’application de Node.js hello--http://localhost:3000 par exemple hello.

Dans ce didacticiel, vous avez vu comment tooeasily package deux applications existantes en tant qu’une application de Service Fabric. Vous avez également appris comment toodeploy il tooService Fabric afin qu’elle peut tirer parti des hello des fonctionnalités de l’infrastructure de Service, tels que l’intégration de système haute disponibilité et intégrité des.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Ajout d’une application existante tooan invité exécutables plus à l’aide de Yeoman sur Linux

tooadd une autre application de tooan service déjà créé à l’aide de `yo`, effectuer hello comme suit : 
1. Modifier la racine toohello du répertoire d’application existant hello.  Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.
2. Exécutez `yo azuresfguest:AddService` et fournir les informations nécessaires hello.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le déploiement de conteneurs avec [Service Fabric et vue d’ensemble des conteneurs](service-fabric-containers-overview.md)
* [Exemple pour empaqueter et déployer un fichier exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
