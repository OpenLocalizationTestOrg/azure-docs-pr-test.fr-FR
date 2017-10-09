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
# <a name="package-an-application"></a>Empaqueter une application
Cet article décrit comment toopackage une application de Service Fabric et prêt pour le déploiement.

## <a name="package-layout"></a>Disposition du package
manifeste de l’application Hello, un ou plusieurs manifestes de service et autres fichiers doivent être organisés dans une disposition spécifique pour le déploiement dans un cluster Service Fabric de package nécessaires. manifestes d’exemple Hello dans cet article, vous devez toobe organisé dans hello suivant la structure de répertoires :

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

les dossiers de Hello sont nommés toomatch hello **nom** les attributs de chaque élément correspondant. Par exemple, si hello manifeste de service contenu deux packages de code avec des noms hello **MyCodeA** et **MyCodeB**, puis deux dossiers par hello contient des mêmes noms hello les fichiers binaires nécessaires pour chaque code package.

## <a name="use-setupentrypoint"></a>Utilisation de SetupEntrypoint
Scénarios courants d’utilisation **SetupEntryPoint** sont lorsque vous devez toorun un exécutable avant le démarrage du service hello ou tooperform une opération avec des privilèges élevés. Par exemple :

* Configuration et l’initialisation des variables d’environnement qui hello besoins exécutable du service. Il n’est pas exécutables tooonly limitée par le biais de modèles de programmation de Service Fabric hello. Par exemple, npm.exe a besoin de certaines variables d’environnement configurées pour le déploiement d’une application node.js.
* La configuration d’un contrôle d’accès via l’installation de certificats de sécurité.

Pour plus d’informations sur la façon de tooconfigure hello **SetupEntryPoint**, consultez [configurer une stratégie de hello pour un point d’entrée de service d’installation](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configuration
### <a name="build-a-package-by-using-visual-studio"></a>Création d'un package à l'aide de Visual Studio
Si vous utilisez Visual Studio 2015 toocreate votre application, vous pouvez utiliser hello Package tooautomatically de la commande Créer un package qui correspond à la disposition de hello décrite ci-dessus.

toocreate un package, avec le bouton droit de projet d’application hello dans l’Explorateur de solutions et choisissez la commande de Package hello, comme indiqué ci-dessous :

![Empaquetage d'une application avec Visual Studio][vs-package-command]

Lors de l’empaquetage est terminé, vous pouvez trouver emplacement hello du package de hello Bonjour **sortie** fenêtre. étape d’empaquetage Hello se produit automatiquement lorsque vous déployez ou que vous déboguez votre application dans Visual Studio.

### <a name="build-a-package-by-command-line"></a>Développer un package par ligne de commande
Il est également possible tooprogrammatically package votre application à l’aide de `msbuild.exe`. Dans les coulisses hello, Visual Studio est en cours d’exécution il afin de la sortie de hello est identique.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Package de test de hello
Vous pouvez vérifier la structure du package hello localement par le biais de PowerShell à l’aide de hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) commande.
Cette commande vérifie la présence de problèmes liés à l’analyse du manifeste, ainsi que toutes les références. Cette commande vérifie uniquement l’exactitude structurelle de hello de répertoires de hello et fichiers de package de hello.
Il ne vérifie pas les hello code ou les données du contenu du package au-delà de la vérification que tous les fichiers nécessaires sont présents.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Cette erreur indique que hello *MySetup.bat* fichier référencé dans le manifeste de service hello **SetupEntryPoint** est absent du package de code hello. Après avoir ajouté les fichiers manquants hello, vérification des applications hello passe :

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

Si des [paramètres d’application](service-fabric-manage-multiple-environment-app-configuration.md) sont définis pour votre application, vous pouvez les transmettre dans [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) pour assurer une validation correcte.

Si vous connaissez le cluster hello où hello application sera déployée, il est recommandé de vous transmettez hello `ImageStoreConnectionString` paramètre. Dans ce cas, le package de hello est également validée par rapport aux versions précédentes de l’application hello qui sont déjà en cours d’exécution dans un cluster de hello. Par exemple, la validation hello peut détecter si un package avec hello même version mais un contenu différent a déjà été déployé.  

Une fois que l’application hello est correctement empaquetée et passe la validation, évaluer en fonction de la taille de hello et nombre hello de fichiers si la compression n’est nécessaire.

## <a name="compress-a-package"></a>Compresser un package
Lorsqu’un package est volumineux ou contient de nombreux fichiers, vous pouvez le compresser afin d’accélérer le déploiement. La compression réduit le nombre de hello de fichiers et de la taille du package hello.
Pour un package d’application compressé [package d’application hello transfert](service-fabric-deploy-remove-applications.md#upload-the-application-package) peut prendre plus de comparés toouploading hello package décompressé (spécialement si le temps de la compression est pris en compte), mais [inscription](service-fabric-deploy-remove-applications.md#register-the-application-package) et [type désinscription de l’application hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sont plus rapides pour un package d’application compressé.

mécanisme de déploiement Hello est identique pour les packages compressées et non compressées. Si le package de hello est compressé, il est compressé sur le nœud de hello avant l’exécution d’application hello et il est stocké en tant que tel dans le magasin d’images hello cluster.
la compression de Hello remplace le package de Service Fabric hello valide avec une version compressée de hello. dossier de Hello doit autoriser des autorisations en écriture. L’exécution d’une compression sur un package déjà compressé ne produit aucun effet.

Vous pouvez compresser un package en exécutant la commande Powershell de hello [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec `CompressPackage` basculer. Vous pouvez décompresser hello le package avec hello identique à l’aide de la commande `UncompressPackage` basculer.

Hello commande suivant compresse les package hello sans le copier toohello magasin d’images. Vous pouvez copier un tooone package compressé ou plus de clusters Service Fabric, si nécessaire, à l’aide de [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sans hello `SkipCopy` indicateur.
package de Hello inclut désormais les fichiers compressés pour hello `code`, `config`, et `data` packages. manifeste de l’application Hello et hello manifestes ne sont pas compressés, car ils sont nécessaires pour de nombreuses opérations internes (par exemple, le package d’application type nom et la version d’extraction pour certains contrôles, de partage).
Les manifestes hello zip rend ces opérations inefficaces.

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

Ou bien, vous pouvez compresser et copier le package hello avec [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) en une seule étape.
Si le package de hello est volumineux, fournissent un délai tooallow suffisamment élevé pour la compression du package hello et cluster de toohello téléchargement hello.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

En interne, l’infrastructure de Service calcule les sommes de contrôle pour les packages d’application hello pour la validation. Lorsque vous utilisez la compression, les sommes de contrôle hello sont calculées sur hello compressé des versions de chaque package.
Si vous avez copié une version non compressée de votre package d’application et que vous souhaitez la compression toouse hello même package, vous devez modifier les versions hello Hello `code`, `config`, et `data` non-concordance de somme de contrôle tooavoid de packages. Si les packages hello restent inchangées, au lieu de modifier la version de hello, vous pouvez utiliser [diff approvisionnement](service-fabric-application-upgrade-advanced.md). Avec cette option, n’incluez pas de package d’inchangée hello à la place de la référence de manifeste de service hello.

De même, si vous avez téléchargé une version compressée du package de hello et que vous souhaitez toouse un package décompressé, vous devez mettre à jour non-concordance de somme de contrôle hello versions tooavoid hello.

Hello package est désormais correctement empaqueté, validé et compressé (si nécessaire), par conséquent, il est prêt pour [déploiement](service-fabric-deploy-remove-applications.md) tooone ou plus Service Fabric des clusters.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Compresser les packages lors du déploiement via Visual Studio
Vous pouvez demander à des packages de toocompress Visual Studio sur le déploiement, en ajoutant hello `CopyPackageParameters` élément tooyour profil de publication et définissez hello `CompressPackage` trop d’attributs`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Étapes suivantes
[Déployer et supprimer des applications] [ 10] décrit comment instances d’application toomanage toouse PowerShell

[Gestion des paramètres d’application de plusieurs environnements] [ 11] décrit comment tooconfigure paramètres et variables d’environnement pour les instances de l’autre application.

[Configurer des stratégies de sécurité pour votre application] [ 12] décrit comment les services toorun sous toorestrict accès aux stratégies de sécurité.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
