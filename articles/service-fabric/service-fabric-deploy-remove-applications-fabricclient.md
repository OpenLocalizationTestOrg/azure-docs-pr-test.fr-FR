---
title: "aaaAzure déploiement d’application Service Fabric | Documents Microsoft"
description: "Utilisez hello FabricClient APIs toodeploy et supprimer des applications dans l’infrastructure de Service."
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
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Déployer et supprimer des applications avec FabricClient
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
Se connecter toohello cluster en créant un [fabricclient ne](/dotnet/api/system.fabric.fabricclient) instance avant d’exécuter une des hello exemples de code dans cet article. Pour obtenir des exemples de cluster de développement local tooa connexion ou d’un cluster à distance ou cluster sécurisé à l’aide d’Azure Active Directory, X509 des certificats ou les voir Windows Active Directory [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). cluster de développement local toohello tooconnect, exécutez hello suivante :

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Télécharger le package d’application hello
Supposons que vous génériez une application nommée *MyApplication* et que vous créiez un package pour cette application dans Visual Studio. Par défaut, le nom de type l’application hello répertorié dans hello ApplicationManifest.xml est « MyApplicationType ».  package d’application, qui contient le manifeste d’application nécessaire hello, manifestes de service et des packages de code/config/données, Hello se trouve dans *C:\Users\&lt ; nom d’utilisateur&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.

Téléchargement du package application hello place dans un emplacement accessible par les composants Service Fabric internes hello. Service Fabric vérifie le package d’application hello pendant l’inscription de hello du package d’application hello. Toutefois, si vous souhaitez le package d’application hello tooverify localement (par exemple, avant de le télécharger), utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) applet de commande.

Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API télécharge le magasin d’images hello application package toohello cluster. 

Si le package d’application hello est grande et/ou de fichiers, vous pouvez [compresser](service-fabric-package-apps.md#compress-a-package) et copiez-le toohello magasin d’images à l’aide de PowerShell. la compression de Hello réduit la taille de hello et nombre hello de fichiers.

Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.

## <a name="register-hello-application-package"></a>Enregistrer le package d’application hello
type d’application Hello et la version déclaré dans le manifeste de l’application hello deviennent disponible lorsque le package d’application hello est inscrit. système de Hello lit package hello téléchargé à l’étape précédente de hello, vérifie les package hello, traite le contenu du package hello et copie l’emplacement du système interne hello traité package tooan.  

Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registres hello du type d’application dans un cluster de hello et le rendre disponible pour le déploiement.

Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fournit des informations sur tous les types d’application a été inscrit. Vous pouvez utiliser cette toodetermine API lors de l’inscription de hello est terminée.

## <a name="create-an-application-instance"></a>Créer une instance d’application
Vous pouvez instancier une application à partir de n’importe quel type d’application qui a été inscrit avec succès à l’aide de hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. nom Hello de chaque application doit commencer par hello *« fabric : «* schéma et doit être unique pour chaque instance d’application (au sein d’un cluster). Tous les services par défaut définis dans le manifeste de l’application hello hello cible du type d’application sont également créés.

Plusieurs instances d'application peuvent être créées pour une version donnée d'un type d'application enregistré. Chaque instance de l’application s’exécute en isolement, avec son propre répertoire de travail et son ensemble de processus.

toosee dont le nom des applications et services sont en cours d’exécution dans le cluster hello, exécutez hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) et [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.

## <a name="create-a-service-instance"></a>Créer une instance de service
Vous pouvez instancier un service à partir d’un type de service à l’aide de hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Si le service de hello est déclaré comme un service par défaut dans le manifeste de l’application hello, service de hello est instancié lors de l’application hello est instanciée.  Appel hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API pour un service qui est déjà instancié renvoie une exception de type FabricException contenant un code d’erreur avec la valeur FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Supprimer une instance de service
Lorsqu’une instance de service n’est plus nécessaire, vous pouvez le supprimer hello instance d’application en cours d’exécution en appelant hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Cette opération ne peut pas être annulée et l’état du service ne peut pas être récupéré.

## <a name="remove-an-application-instance"></a>Supprimer une instance d’application
Lorsqu’une instance d’application n’est plus nécessaire, vous pouvez le supprimer définitivement par son nom hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) supprime automatiquement tous les services qui appartiennent application toohello également, définitivement suppression de tous les États de service.

> [!WARNING]
> Cette opération ne peut pas être annulée et l’état de l’application ne peut pas être récupéré.

## <a name="unregister-an-application-type"></a>Désinscrire un type d’application
Lorsqu’une version particulière d’un type d’application n’est plus nécessaire, vous devez annuler l’inscription de cette version particulière du type d’application hello à l’aide de hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Annulation de l’inscription des versions inutilisées application types versions d’espace de stockage utilisé par le magasin d’images hello. Une version d’un type d’application peut être effectuée tant qu’aucune application n’est instanciées par rapport à cette version du type d’application hello et aucune mise à niveau de l’application en attente n’est faisant référence à cette version du type d’application hello.

## <a name="remove-an-application-package-from-hello-image-store"></a>Supprimer un package d’application à partir du magasin d’images hello
Lorsqu’un package d’application n’est plus nécessaire, vous pouvez la supprimer hello image store toofree des ressources système à l’aide de hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

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
Problème : l’API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) expire pour un package d’application volumineux (de l’ordre du Go).
Essayez de procéder comme suit :
- Spécifiez un délai d’expiration supérieur pour la méthode [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) avec le paramètre `timeout`. Par défaut, le délai d’attente hello est 30 minutes.
- Vérifiez la connexion de réseau hello entre votre ordinateur source et le cluster. Si hello connexion est lente, envisagez d’utiliser un ordinateur avec une connexion réseau mieux.
Si l’ordinateur client de hello est dans une autre région que le cluster de hello, envisagez d’utiliser un ordinateur client dans une région proche ou même en tant que cluster de hello.
- Vérifiez si vous êtes confronté à des limitations externes. Par exemple, lorsque le magasin d’images hello est configuré toouse azure storage, téléchargement peut être limité.

Problème : le chargement du package s’est terminé avec succès, mais l’API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) expire. Essayez de procéder comme suit :
- [Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.
la compression de Hello réduit la taille de hello et nombre hello de fichiers, qui à son tour réduit le trafic hello et utiliser ce Service Fabric doit effectuer. opération de téléchargement de Hello peut être plus lente (surtout si vous incluez des temps de compression hello), mais le type d’application hello inscrire et désinscrire sont plus rapides.
- Spécifiez un délai d’expiration supérieur pour l’API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) avec le paramètre `timeout`.

### <a name="deploy-application-package-with-many-files"></a>Déployer un package d’application contenant de nombreux fichiers
Problème : [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) expire pour un package d’application contenant un grand nombre de fichiers (de l’ordre de plusieurs milliers).
Essayez de procéder comme suit :
- [Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello. la compression de Hello réduit le nombre de hello de fichiers.
- Spécifiez un délai d’expiration supérieur pour [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) avec le paramètre `timeout`.

## <a name="code-example"></a>Exemple de code
Hello exemple suivant copie un magasin d’image application package toohello, configure le type de l’application hello, crée une instance d’application, crée une instance de service, instance de l’application hello supprime,-configure un type d’application hello, et Supprime le package d’application hello à partir du magasin d’images hello.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Étapes suivantes
[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)

[Présentation de l’intégrité de Service Fabric](service-fabric-health-introduction.md)

[Diagnostiquer et résoudre les problèmes d'un service Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modéliser une application dans Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
