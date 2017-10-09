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
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="c698a-103">Déployer et supprimer des applications avec FabricClient</span><span class="sxs-lookup"><span data-stu-id="c698a-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c698a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c698a-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="c698a-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c698a-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="c698a-106">API FabricClient</span><span class="sxs-lookup"><span data-stu-id="c698a-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="c698a-107">Après avoir [packagé un type d’application][10], celui-ci peut être déployé sur un cluster Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c698a-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="c698a-108">Le déploiement implique hello trois comme suit :</span><span class="sxs-lookup"><span data-stu-id="c698a-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="c698a-109">Télécharger le magasin d’images hello application package toohello</span><span class="sxs-lookup"><span data-stu-id="c698a-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="c698a-110">Inscrire le type d’application hello</span><span class="sxs-lookup"><span data-stu-id="c698a-110">Register hello application type</span></span>
3. <span data-ttu-id="c698a-111">Créer l’instance de l’application hello</span><span class="sxs-lookup"><span data-stu-id="c698a-111">Create hello application instance</span></span>

<span data-ttu-id="c698a-112">Après le déploiement d’une application et une instance est en cours d’exécution dans un cluster de hello, vous pouvez supprimer l’instance de l’application hello et son type d’application.</span><span class="sxs-lookup"><span data-stu-id="c698a-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="c698a-113">suppression de toocompletely une application à partir du cluster de hello implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c698a-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="c698a-114">Supprimer (ou supprimer) hello instance d’application en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="c698a-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="c698a-115">Annuler l’inscription du type de l’application hello si elle n’est plus nécessaire</span><span class="sxs-lookup"><span data-stu-id="c698a-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="c698a-116">Supprimer le package d’application hello à partir du magasin d’images hello</span><span class="sxs-lookup"><span data-stu-id="c698a-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="c698a-117">Si vous utilisez [Visual Studio pour déployer et déboguer des applications](service-fabric-publish-app-remote-cluster.md) sur votre cluster de développement local, tous les hello étapes précédentes sont gérées automatiquement via un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c698a-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="c698a-118">Ce script se trouve dans hello *Scripts* dossier du projet d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="c698a-119">Cet article des informations générales sur ce que fait ce script afin que vous puissiez effectuer hello les mêmes opérations en dehors de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c698a-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="c698a-120">Se connecter toohello cluster</span><span class="sxs-lookup"><span data-stu-id="c698a-120">Connect toohello cluster</span></span>
<span data-ttu-id="c698a-121">Se connecter toohello cluster en créant un [fabricclient ne](/dotnet/api/system.fabric.fabricclient) instance avant d’exécuter une des hello exemples de code dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c698a-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="c698a-122">Pour obtenir des exemples de cluster de développement local tooa connexion ou d’un cluster à distance ou cluster sécurisé à l’aide d’Azure Active Directory, X509 des certificats ou les voir Windows Active Directory [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="c698a-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="c698a-123">cluster de développement local toohello tooconnect, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="c698a-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="c698a-124">Télécharger le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="c698a-124">Upload hello application package</span></span>
<span data-ttu-id="c698a-125">Supposons que vous génériez une application nommée *MyApplication* et que vous créiez un package pour cette application dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c698a-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="c698a-126">Par défaut, le nom de type l’application hello répertorié dans hello ApplicationManifest.xml est « MyApplicationType ».</span><span class="sxs-lookup"><span data-stu-id="c698a-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="c698a-127">package d’application, qui contient le manifeste d’application nécessaire hello, manifestes de service et des packages de code/config/données, Hello se trouve dans *C:\Users\&lt ; nom d’utilisateur&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="c698a-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="c698a-128">Téléchargement du package application hello place dans un emplacement accessible par les composants Service Fabric internes hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="c698a-129">Service Fabric vérifie le package d’application hello pendant l’inscription de hello du package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="c698a-130">Toutefois, si vous souhaitez le package d’application hello tooverify localement (par exemple, avant de le télécharger), utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c698a-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="c698a-131">Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API télécharge le magasin d’images hello application package toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="c698a-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="c698a-132">Si le package d’application hello est grande et/ou de fichiers, vous pouvez [compresser](service-fabric-package-apps.md#compress-a-package) et copiez-le toohello magasin d’images à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c698a-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="c698a-133">la compression de Hello réduit la taille de hello et nombre hello de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c698a-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="c698a-134">Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c698a-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="c698a-135">Enregistrer le package d’application hello</span><span class="sxs-lookup"><span data-stu-id="c698a-135">Register hello application package</span></span>
<span data-ttu-id="c698a-136">type d’application Hello et la version déclaré dans le manifeste de l’application hello deviennent disponible lorsque le package d’application hello est inscrit.</span><span class="sxs-lookup"><span data-stu-id="c698a-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="c698a-137">système de Hello lit package hello téléchargé à l’étape précédente de hello, vérifie les package hello, traite le contenu du package hello et copie l’emplacement du système interne hello traité package tooan.</span><span class="sxs-lookup"><span data-stu-id="c698a-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="c698a-138">Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registres hello du type d’application dans un cluster de hello et le rendre disponible pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c698a-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="c698a-139">Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fournit des informations sur tous les types d’application a été inscrit.</span><span class="sxs-lookup"><span data-stu-id="c698a-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="c698a-140">Vous pouvez utiliser cette toodetermine API lors de l’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="c698a-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="c698a-141">Créer une instance d’application</span><span class="sxs-lookup"><span data-stu-id="c698a-141">Create an application instance</span></span>
<span data-ttu-id="c698a-142">Vous pouvez instancier une application à partir de n’importe quel type d’application qui a été inscrit avec succès à l’aide de hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="c698a-143">nom Hello de chaque application doit commencer par hello *« fabric : «* schéma et doit être unique pour chaque instance d’application (au sein d’un cluster).</span><span class="sxs-lookup"><span data-stu-id="c698a-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="c698a-144">Tous les services par défaut définis dans le manifeste de l’application hello hello cible du type d’application sont également créés.</span><span class="sxs-lookup"><span data-stu-id="c698a-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="c698a-145">Plusieurs instances d'application peuvent être créées pour une version donnée d'un type d'application enregistré.</span><span class="sxs-lookup"><span data-stu-id="c698a-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="c698a-146">Chaque instance de l’application s’exécute en isolement, avec son propre répertoire de travail et son ensemble de processus.</span><span class="sxs-lookup"><span data-stu-id="c698a-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="c698a-147">toosee dont le nom des applications et services sont en cours d’exécution dans le cluster hello, exécutez hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) et [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="c698a-148">Créer une instance de service</span><span class="sxs-lookup"><span data-stu-id="c698a-148">Create a service instance</span></span>
<span data-ttu-id="c698a-149">Vous pouvez instancier un service à partir d’un type de service à l’aide de hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="c698a-150">Si le service de hello est déclaré comme un service par défaut dans le manifeste de l’application hello, service de hello est instancié lors de l’application hello est instanciée.</span><span class="sxs-lookup"><span data-stu-id="c698a-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="c698a-151">Appel hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API pour un service qui est déjà instancié renvoie une exception de type FabricException contenant un code d’erreur avec la valeur FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="c698a-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="c698a-152">Supprimer une instance de service</span><span class="sxs-lookup"><span data-stu-id="c698a-152">Remove a service instance</span></span>
<span data-ttu-id="c698a-153">Lorsqu’une instance de service n’est plus nécessaire, vous pouvez le supprimer hello instance d’application en cours d’exécution en appelant hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="c698a-154">Cette opération ne peut pas être annulée et l’état du service ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="c698a-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="c698a-155">Supprimer une instance d’application</span><span class="sxs-lookup"><span data-stu-id="c698a-155">Remove an application instance</span></span>
<span data-ttu-id="c698a-156">Lorsqu’une instance d’application n’est plus nécessaire, vous pouvez le supprimer définitivement par son nom hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="c698a-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) supprime automatiquement tous les services qui appartiennent application toohello également, définitivement suppression de tous les États de service.</span><span class="sxs-lookup"><span data-stu-id="c698a-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="c698a-158">Cette opération ne peut pas être annulée et l’état de l’application ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="c698a-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="c698a-159">Désinscrire un type d’application</span><span class="sxs-lookup"><span data-stu-id="c698a-159">Unregister an application type</span></span>
<span data-ttu-id="c698a-160">Lorsqu’une version particulière d’un type d’application n’est plus nécessaire, vous devez annuler l’inscription de cette version particulière du type d’application hello à l’aide de hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="c698a-161">Annulation de l’inscription des versions inutilisées application types versions d’espace de stockage utilisé par le magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="c698a-162">Une version d’un type d’application peut être effectuée tant qu’aucune application n’est instanciées par rapport à cette version du type d’application hello et aucune mise à niveau de l’application en attente n’est faisant référence à cette version du type d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="c698a-163">Supprimer un package d’application à partir du magasin d’images hello</span><span class="sxs-lookup"><span data-stu-id="c698a-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="c698a-164">Lorsqu’un package d’application n’est plus nécessaire, vous pouvez la supprimer hello image store toofree des ressources système à l’aide de hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="c698a-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c698a-165">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="c698a-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="c698a-166">Copy-ServiceFabricApplicationPackage demande un ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="c698a-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="c698a-167">environnement de Service Fabric SDK Hello doit déjà avoir hello correct à configurer des paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="c698a-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="c698a-168">Mais si nécessaire, hello ImageStoreConnectionString pour toutes les commandes doit correspondre à hello valeur ce hello Service Fabric à l’aide de cluster.</span><span class="sxs-lookup"><span data-stu-id="c698a-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="c698a-169">Vous pouvez trouver hello ImageStoreConnectionString dans le manifeste du cluster hello, récupéré à l’aide de hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) et les commandes Get-ImageStoreConnectionStringFromClusterManifest :</span><span class="sxs-lookup"><span data-stu-id="c698a-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="c698a-170">Hello **Get-ImageStoreConnectionStringFromClusterManifest** applet de commande, qui fait partie du module de Service Fabric SDK PowerShell hello, est l’image de hello tooget utilisés stocker la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c698a-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="c698a-171">module du Kit de développement logiciel de hello tooimport, exécutez :</span><span class="sxs-lookup"><span data-stu-id="c698a-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="c698a-172">Hello ImageStoreConnectionString se trouve dans le manifeste du cluster hello :</span><span class="sxs-lookup"><span data-stu-id="c698a-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="c698a-173">Consultez [comprendre la chaîne de connexion de magasin hello image](service-fabric-image-store-connection-string.md) pour plus d’informations sur le magasin d’images hello et image stockent la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="c698a-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="c698a-174">Déployer un package d’application volumineux</span><span class="sxs-lookup"><span data-stu-id="c698a-174">Deploy large application package</span></span>
<span data-ttu-id="c698a-175">Problème : l’API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) expire pour un package d’application volumineux (de l’ordre du Go).</span><span class="sxs-lookup"><span data-stu-id="c698a-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="c698a-176">Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="c698a-176">Try:</span></span>
- <span data-ttu-id="c698a-177">Spécifiez un délai d’expiration supérieur pour la méthode [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) avec le paramètre `timeout`.</span><span class="sxs-lookup"><span data-stu-id="c698a-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="c698a-178">Par défaut, le délai d’attente hello est 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="c698a-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="c698a-179">Vérifiez la connexion de réseau hello entre votre ordinateur source et le cluster.</span><span class="sxs-lookup"><span data-stu-id="c698a-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="c698a-180">Si hello connexion est lente, envisagez d’utiliser un ordinateur avec une connexion réseau mieux.</span><span class="sxs-lookup"><span data-stu-id="c698a-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="c698a-181">Si l’ordinateur client de hello est dans une autre région que le cluster de hello, envisagez d’utiliser un ordinateur client dans une région proche ou même en tant que cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="c698a-182">Vérifiez si vous êtes confronté à des limitations externes.</span><span class="sxs-lookup"><span data-stu-id="c698a-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="c698a-183">Par exemple, lorsque le magasin d’images hello est configuré toouse azure storage, téléchargement peut être limité.</span><span class="sxs-lookup"><span data-stu-id="c698a-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="c698a-184">Problème : le chargement du package s’est terminé avec succès, mais l’API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) expire. Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="c698a-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="c698a-185">[Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.</span><span class="sxs-lookup"><span data-stu-id="c698a-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="c698a-186">la compression de Hello réduit la taille de hello et nombre hello de fichiers, qui à son tour réduit le trafic hello et utiliser ce Service Fabric doit effectuer.</span><span class="sxs-lookup"><span data-stu-id="c698a-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="c698a-187">opération de téléchargement de Hello peut être plus lente (surtout si vous incluez des temps de compression hello), mais le type d’application hello inscrire et désinscrire sont plus rapides.</span><span class="sxs-lookup"><span data-stu-id="c698a-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="c698a-188">Spécifiez un délai d’expiration supérieur pour l’API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) avec le paramètre `timeout`.</span><span class="sxs-lookup"><span data-stu-id="c698a-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="c698a-189">Déployer un package d’application contenant de nombreux fichiers</span><span class="sxs-lookup"><span data-stu-id="c698a-189">Deploy application package with many files</span></span>
<span data-ttu-id="c698a-190">Problème : [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) expire pour un package d’application contenant un grand nombre de fichiers (de l’ordre de plusieurs milliers).</span><span class="sxs-lookup"><span data-stu-id="c698a-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="c698a-191">Essayez de procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="c698a-191">Try:</span></span>
- <span data-ttu-id="c698a-192">[Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello.</span><span class="sxs-lookup"><span data-stu-id="c698a-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="c698a-193">la compression de Hello réduit le nombre de hello de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c698a-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="c698a-194">Spécifiez un délai d’expiration supérieur pour [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) avec le paramètre `timeout`.</span><span class="sxs-lookup"><span data-stu-id="c698a-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="c698a-195">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="c698a-195">Code example</span></span>
<span data-ttu-id="c698a-196">Hello exemple suivant copie un magasin d’image application package toohello, configure le type de l’application hello, crée une instance d’application, crée une instance de service, instance de l’application hello supprime,-configure un type d’application hello, et Supprime le package d’application hello à partir du magasin d’images hello.</span><span class="sxs-lookup"><span data-stu-id="c698a-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c698a-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c698a-197">Next steps</span></span>
[<span data-ttu-id="c698a-198">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c698a-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="c698a-199">Présentation de l’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c698a-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="c698a-200">Diagnostiquer et résoudre les problèmes d'un service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c698a-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="c698a-201">Modéliser une application dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c698a-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
