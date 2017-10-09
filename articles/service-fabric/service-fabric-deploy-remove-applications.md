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
# <a name="deploy-and-remove-applications-using-powershell"></a>Déployer et supprimer des applications avec PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Après avoir [packagé un type d’application][10], celui-ci peut être déployé sur un cluster Azure Service Fabric. Le déploiement implique hello trois comme suit :

1. Télécharger le magasin d’images hello application package toohello
2. Inscrire le type d’application hello
3. Créer l’instance de l’application hello

Après le déploiement d’une application et une instance est en cours d’exécution dans un cluster de hello, vous pouvez supprimer l’instance de l’application hello et son type d’application. suppression de toocompletely une application à partir du cluster de hello implique hello comme suit :

1. Supprimer (ou supprimer) hello instance d’application en cours d’exécution
2. Annuler l’inscription du type de l’application hello si elle n’est plus nécessaire
3. Supprimer le package d’application hello à partir du magasin d’images hello

Si vous utilisez [Visual Studio pour déployer et déboguer des applications](service-fabric-publish-app-remote-cluster.md) sur votre cluster de développement local, tous les hello étapes précédentes sont gérées automatiquement via un script PowerShell.  Ce script se trouve dans hello *Scripts* dossier du projet d’application hello. Cet article des informations générales sur ce que fait ce script afin que vous puissiez effectuer hello les mêmes opérations en dehors de Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster
Avant d’exécuter les commandes PowerShell dans cet article, commencent toujours à l’aide de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cluster Service Fabric de toohello tooconnect. cluster de développement local toohello tooconnect, exécutez hello suivante :

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Pour obtenir des exemples de connexion à distance du cluster tooa ou du cluster sécurisé à l’aide d’Azure Active Directory, X509 des certificats ou les voir Windows Active Directory [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Télécharger le package d’application hello
Téléchargement du package application hello place dans un emplacement accessible par les composants de l’infrastructure de Service internes.
Si vous souhaitez que le package d’application hello tooverify localement, utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) applet de commande.

Hello [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) commande téléchargements hello magasin d’images application package toohello cluster.
Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.  module du Kit de développement logiciel de hello tooimport, exécutez :

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Supposons que vous génériez une application nommée *MyApplication* et que vous créiez un package pour cette application dans Visual Studio 2015. Par défaut, le nom de type l’application hello répertorié dans hello ApplicationManifest.xml est « MyApplicationType ».  package d’application, qui contient le manifeste d’application nécessaire hello, manifestes de service et des packages de code/config/données, Hello se trouve dans *C:\Users\<nom d’utilisateur\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*. 

Hello commande suivante répertorie contenu hello hello du package d’application :

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

Si le package d’application hello est grande et/ou de fichiers, vous pouvez [compresser](service-fabric-package-apps.md#compress-a-package). la compression de Hello réduit la taille de hello et nombre hello de fichiers.
Hello effet secondaire est que hello inscription et désinscription type d’application sont plus rapides. Temps de téléchargement peut être plus lent actuellement, notamment si vous incluez le package de hello temps toocompress hello. 

toocompress un package, utilisez hello même [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) commande. La compression peut faire distinct à partir de téléchargement, à l’aide hello `SkipCopy` indicateur ou opération de téléchargement avec hello. L’application d’une compression sur un package compressé n’a aucun effet.
toouncompress un package compressé, utilisez hello même [copie-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec hello `UncompressPackage` basculer.

Hello applet de commande suivante compresse les package hello sans le copier toohello magasin d’images. package de Hello inclut désormais les fichiers compressés pour hello `Code` et `Config` packages. Hello manifestes d’application et hello service ne sont pas compressés, car ils sont nécessaires pour de nombreuses opérations internes (par exemple, le package d’application type nom et la version d’extraction pour certains contrôles, de partage). Les manifestes hello zip rend ces opérations inefficaces.

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

Pour les packages d’application de grande taille, la compression de hello du temps. Pour obtenir de meilleurs résultats, utilisez un disque SSD rapide. les durées de compression Hello et taille hello de package compressé de hello diffèrent également selon le contenu du package hello.
Par exemple, Voici des statistiques de compression de certains packages affichent hello initiale et hello taille du package compressé, avec le temps de compression hello.

|Taille initiale (Mo)|Nombre de fichiers|Temps de compression|Taille du package compressé (Mo)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1 024|500|00:00:32.5907950|615|
|2 048|1 000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Une fois qu’un package est compressé, il peut être téléchargé tooone plusieurs Service Fabric de clusters ou en cas de besoin. mécanisme de déploiement Hello est identique pour les packages compressées et non compressées. Si le package de hello est compressé, il est compressé sur le nœud de hello avant l’exécution d’application hello et il est stocké en tant que tel dans le magasin d’images hello cluster.


Hello exemple suivant télécharge magasin d’images package toohello hello, dans un dossier nommé « MyApplicationV1 » :

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.  module du Kit de développement logiciel de hello tooimport, exécutez :

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Si vous ne spécifiez pas hello *- ApplicationPackagePathInImageStore* paramètre, le package d’application hello est copié dans le dossier de « Debug » hello dans le magasin d’images hello.

Hello temps tooupload un package diffère selon plusieurs facteurs. Certains de ces facteurs sont nombre hello de fichiers dans le package de hello, la taille du package hello et tailles de fichier hello. vitesse du réseau entre l’ordinateur de source de hello et cluster Service Fabric de hello Hello affecte également le temps de téléchargement hello. Hello de délai d’attente par défaut pour [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) est de 30 minutes.
En fonction de hello facteurs décrits, vous devrez peut-être le délai d’attente de tooincrease hello. Si vous compressez des package hello dans l’appel de copie hello, vous devez tooalso prendre en compte le temps de compression hello.

Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.

## <a name="register-hello-application-package"></a>Enregistrer le package d’application hello
type d’application Hello et la version déclaré dans le manifeste de l’application hello deviennent disponible lorsque le package d’application hello est inscrit. système de Hello lit package hello téléchargé à l’étape précédente de hello, vérifie les package hello, traite le contenu du package hello et copie l’emplacement du système interne hello traité package tooan.  

Exécutez hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister de l’applet de commande hello du type d’application dans un cluster de hello et le rendre disponible pour le déploiement :

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

« MyApplicationV1 » est hello dans le magasin d’images hello où se trouve le package d’application hello. type d’application Hello avec le nom « MyApplicationType » et la version « 1.0.0 » (les deux se trouvent dans le manifeste de l’application hello) est maintenant inscrit dans le cluster de hello.

Hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) commande retourne uniquement une fois le système de hello a package d’application hello correctement inscrit. La durée pendant laquelle l’enregistrement prend dépend de taille de hello et le contenu du package d’application hello. Si nécessaire, hello **- TimeoutSec** paramètre peut être utilisé toosupply un délai d’attente plus long (le délai d’attente de hello par défaut est 60 secondes).

Si vous avez une grande application du package ou si vous rencontrez des délais d’attente, utilisez hello **- Async** paramètre. commande Hello retourne lorsque le cluster de hello accepte une commande de Registre hello et le traitement de hello continue en fonction des besoins.
Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription. Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Créer l’application hello
Vous pouvez instancier une application à partir de n’importe quelle version de type d’application qui a été inscrit avec succès à l’aide de hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) applet de commande. nom Hello de chaque application doit commencer par hello *« fabric : «* schéma et doit être unique pour chaque instance d’application. Tous les services par défaut définis dans le manifeste de l’application hello hello cible du type d’application sont également créés.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Plusieurs instances d'application peuvent être créées pour une version donnée d'un type d'application enregistré. Chaque instance de l’application s’exécute en isolement, avec ses propres répertoire de travail et processus.

toosee dont le nom des applications et services sont en cours d’exécution dans le cluster hello, exécutez hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) et [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) applets de commande :

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

## <a name="remove-an-application"></a>Supprimer une application
Lorsqu’une instance d’application n’est plus nécessaire, vous pouvez le supprimer définitivement par son nom hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) applet de commande. [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) supprime automatiquement tous les services qui appartiennent application toohello également, définitivement suppression de tous les États de service. 

> [!WARNING]
> Cette opération ne peut pas être annulée et l’état de l’application ne peut pas être récupéré.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Désinscrire un type d’application
Lorsqu’une version particulière d’un type d’application n’est plus nécessaire, vous devez annuler l’inscription de type d’application hello à l’aide de hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) applet de commande. Lors de la désinscription application inutilisées types versions espace de stockage utilisé par le magasin d’images hello. Vous pouvez désinscrire un type d’application s’il ne contient aucune instance d’application et s’il n’est référencé par aucune mise à niveau d’application en attente.

Exécutez [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) types d’application hello toosee actuellement inscrits dans le cluster de hello :

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Exécutez [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un type d’application spécifique :

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Supprimer un package d’application à partir du magasin d’images hello
Lorsqu’un package d’application n’est plus nécessaire, vous pouvez la supprimer hello image store toofree des ressources système.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage demande un ImageStoreConnectionString
environnement de Service Fabric SDK Hello doit déjà avoir hello correct à configurer des paramètres par défaut. Mais si nécessaire, hello ImageStoreConnectionString pour toutes les commandes doit correspondre à hello valeur ce hello Service Fabric à l’aide de cluster. Vous pouvez trouver hello ImageStoreConnectionString dans le manifeste du cluster hello, récupéré à l’aide de hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) et les commandes Get-ImageStoreConnectionStringFromClusterManifest :

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.  module du Kit de développement logiciel de hello tooimport, exécutez :

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Hello ImageStoreConnectionString se trouve dans le manifeste du cluster hello :

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.

### <a name="deploy-large-application-package"></a>Déployer un package d’application volumineux
Problème : la commande [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) expire pour un package d’application volumineux (de l’ordre du gigaoctet).
Essayez de procéder comme suit :
- Spécifiez un délai d’expiration supérieur pour la commande[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) avec le paramètre `TimeoutSec`. Par défaut, le délai d’attente hello est 30 minutes.
- Vérifiez la connexion de réseau hello entre votre ordinateur source et le cluster. Si hello connexion est lente, envisagez d’utiliser un ordinateur avec une connexion réseau mieux.
Si l’ordinateur client de hello est dans une autre région que le cluster de hello, envisagez d’utiliser un ordinateur client dans une région proche ou même en tant que cluster de hello.
- Vérifiez si vous êtes confronté à des limitations externes. Par exemple, lorsque le magasin d’images hello est configuré toouse azure storage, téléchargement peut être limité.

Problème : le chargement du package s’est terminé avec succès, mais la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) expire. Essayez de procéder comme suit :
- [Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.
la compression de Hello réduit la taille de hello et nombre hello de fichiers, qui à son tour réduit le trafic hello et utiliser ce Service Fabric doit effectuer. opération de téléchargement de Hello peut être plus lente (surtout si vous incluez des temps de compression hello), mais le type d’application hello inscrire et désinscrire sont plus rapides.
- Spécifiez un délai d’expiration supérieur pour la commande[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) avec le paramètre `TimeoutSec`.
- Spécifiez le commutateur `Async` pour la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). commande Hello retourne lorsque le cluster de hello accepte une commande hello et inscription hello hello du type d’application se poursuit de façon asynchrone. Pour cette raison, il est sans toospecify besoin un délai d’attente plus élevé dans ce cas. Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription. Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Déployer un package d’application contenant de nombreux fichiers
Problème : la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) expire pour un package d’application contenant un grand nombre de fichiers (de l’ordre de plusieurs milliers).
Essayez de procéder comme suit :
- [Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello. la compression de Hello réduit le nombre de hello de fichiers.
- Spécifiez un délai d’expiration supérieur pour la commande[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) avec le paramètre `TimeoutSec`.
- Spécifiez le commutateur `Async` pour la commande [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). commande Hello retourne lorsque le cluster de hello accepte une commande hello et inscription hello hello du type d’application se poursuit de façon asynchrone.
Pour cette raison, il est sans toospecify besoin un délai d’attente plus élevé dans ce cas. Hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) commande répertorie toutes les versions de type d’application a été inscrit et leur état de l’inscription. Vous pouvez utiliser cette commande toodetermine lors de l’inscription de hello est terminée.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Étapes suivantes
[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)

[Présentation de l’intégrité de Service Fabric](service-fabric-health-introduction.md)

[Diagnostiquer et résoudre les problèmes d'un service Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modéliser une application dans Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
