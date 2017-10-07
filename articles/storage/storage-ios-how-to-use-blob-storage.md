---
title: "aaaHow toouse stockage d’objets Blob Azure à partir d’iOS | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="03263-103">Comment toouse stockage d’objets Blob à partir d’iOS</span><span class="sxs-lookup"><span data-stu-id="03263-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="03263-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="03263-104">Overview</span></span>
<span data-ttu-id="03263-105">Cet article vous indiquent comment les scénarios courants tooperform à l’aide du stockage d’objets Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03263-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="03263-106">les exemples de Hello sont écrites en Objective-C et utiliser hello [bibliothèque cliente de stockage Azure pour iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="03263-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="03263-107">Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="03263-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="03263-108">Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="03263-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="03263-109">Vous pouvez également télécharger hello [exemple d’application](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly voir hello utilisation du stockage Azure dans une application iOS.</span><span class="sxs-lookup"><span data-stu-id="03263-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="03263-110">Importer la bibliothèque e/s de stockage Azure hello dans votre application</span><span class="sxs-lookup"><span data-stu-id="03263-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="03263-111">Vous pouvez importer des bibliothèque e/s de stockage Azure hello dans votre application à l’aide de hello [CocoaPod de stockage Azure](https://cocoapods.org/pods/AZSClient) ou en important hello **Framework** fichier.</span><span class="sxs-lookup"><span data-stu-id="03263-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="03263-112">CocoaPod est hello recommandé de façon qu’il facilite la bibliothèque de hello intégrés, toutefois l’importation à partir du fichier de framework hello est moins importun pour votre projet existant.</span><span class="sxs-lookup"><span data-stu-id="03263-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="03263-113">toouse cette bibliothèque, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="03263-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="03263-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="03263-114">iOS 8+</span></span>
- <span data-ttu-id="03263-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="03263-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="03263-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="03263-116">CocoaPod</span></span>
1. <span data-ttu-id="03263-117">Si vous n’avez pas déjà fait, [CocoaPods d’installer](https://guides.cocoapods.org/using/getting-started.html#toc_3) sur votre ordinateur en ouvrant une fenêtre de terminal et en cours d’exécution hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="03263-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="03263-118">Ensuite, dans le répertoire du projet hello (directory hello contenant votre fichier .xcodeproj), créez un nouveau fichier appelé _Podfile_(aucune extension de fichier).</span><span class="sxs-lookup"><span data-stu-id="03263-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="03263-119">Ajoutez hello suivant too_Podfile_ et enregistrez.</span><span class="sxs-lookup"><span data-stu-id="03263-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="03263-120">Dans la fenêtre de terminal hello, accédez à toohello répertoire de projet et exécution hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="03263-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="03263-121">Si votre fichier .xcodeproj est ouvert dans Xcode, fermez-le.</span><span class="sxs-lookup"><span data-stu-id="03263-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="03263-122">Dans votre fichier de projet projet Active hello ouverts récemment créé qui disposent d’extension de .xcworkspace hello.</span><span class="sxs-lookup"><span data-stu-id="03263-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="03263-123">Il s’agit de fichier hello que vous allez utiliser à partir de maintenant.</span><span class="sxs-lookup"><span data-stu-id="03263-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="03263-124">Framework</span><span class="sxs-lookup"><span data-stu-id="03263-124">Framework</span></span>
<span data-ttu-id="03263-125">Hello autre bibliothèque de hello toouse est framework de hello toobuild manuellement de façon :</span><span class="sxs-lookup"><span data-stu-id="03263-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="03263-126">First, téléchargement ou hello du clone [référentiel d’azure-stockage-e/s](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="03263-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="03263-127">Accédez à *azure-storage-ios* -> *Bibliothèque* -> *Bibliothèque cliente Azure Storage*, puis ouvrez `AZSClient.xcodeproj` dans Xcode.</span><span class="sxs-lookup"><span data-stu-id="03263-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="03263-128">À hello en haut à gauche de Xcode, hello de modification active schéma à partir de « Bibliothèque cliente de stockage Azure » trop « Framework ».</span><span class="sxs-lookup"><span data-stu-id="03263-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="03263-129">Générez le projet hello (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="03263-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="03263-130">Cela créera un fichier `AZSClient.framework` sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="03263-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="03263-131">Vous pouvez ensuite importer le fichier de framework hello dans votre application de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="03263-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="03263-132">Créez un projet ou ouvrez votre projet existant dans Xcode.</span><span class="sxs-lookup"><span data-stu-id="03263-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="03263-133">Glisser- déposer hello `AZSClient.framework` dans votre navigateur de projet Xcode.</span><span class="sxs-lookup"><span data-stu-id="03263-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="03263-134">Sélectionnez *Copier les éléments si besoin*, puis cliquez sur *Terminer*.</span><span class="sxs-lookup"><span data-stu-id="03263-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="03263-135">Cliquez sur votre projet dans la navigation de gauche hello et cliquez sur hello *général* onglet en haut de hello de l’éditeur de projet hello.</span><span class="sxs-lookup"><span data-stu-id="03263-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="03263-136">Sous hello *lié infrastructures et bibliothèques* , cliquez sur le bouton Ajouter de hello (+).</span><span class="sxs-lookup"><span data-stu-id="03263-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="03263-137">Dans la liste hello bibliothèques déjà fournies, recherchez `libxml2.2.tbd` et ajoutez-le tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="03263-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="03263-138">Importer la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="03263-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="03263-139">Si vous utilisez Swift, sera toocreate un en-tête de transition et les importer < AZSClient/AZSClient.h > il :</span><span class="sxs-lookup"><span data-stu-id="03263-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="03263-140">Créer un fichier d’en-tête `Bridging-Header.h`et ajoutez hello ci-dessus instruction d’importation.</span><span class="sxs-lookup"><span data-stu-id="03263-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="03263-141">Accédez toohello *paramètres de génération* onglet et recherchez *en-tête de pontage Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="03263-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="03263-142">Double-cliquez sur le champ hello de *en-tête de Objective-C Bridging* et ajoutez le fichier d’en-tête tooyour hello chemin d’accès :`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="03263-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="03263-143">Build hello projet (⌘ + B) tooverify qui hello bridging en-tête a été récupéré par Xcode.</span><span class="sxs-lookup"><span data-stu-id="03263-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="03263-144">Démarrer à l’aide de la bibliothèque de hello directement dans n’importe quel fichier Swift, il n’est pas nécessaire pour les instructions d’importation.</span><span class="sxs-lookup"><span data-stu-id="03263-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="03263-145">Opérations asynchrones</span><span class="sxs-lookup"><span data-stu-id="03263-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="03263-146">Toutes les méthodes qui effectuent une demande de service de hello sont des opérations asynchrones.</span><span class="sxs-lookup"><span data-stu-id="03263-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="03263-147">Vous trouverez dans les exemples de code hello, que ces méthodes ont un gestionnaire d’achèvement.</span><span class="sxs-lookup"><span data-stu-id="03263-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="03263-148">Le code à l’intérieur du Gestionnaire d’achèvement hello s’exécutera **après** hello demande est terminée.</span><span class="sxs-lookup"><span data-stu-id="03263-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="03263-149">Le code après l’exécution de gestionnaire d’achèvement hello **tandis que** hello requête est effectuée.</span><span class="sxs-lookup"><span data-stu-id="03263-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="03263-150">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="03263-150">Create a container</span></span>
<span data-ttu-id="03263-151">Chaque objet blob dans Azure Storage doit résider dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="03263-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="03263-152">Hello exemple suivant montre comment toocreate un conteneur, appelée *newcontainer*, dans votre compte de stockage s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="03263-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="03263-153">Lorsque vous choisissez un nom pour votre conteneur, tenez compte de hello mentionnés ci-dessus des règles d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="03263-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="03263-154">Vous pouvez vérifier que cela fonctionne en examinant hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) et en vérifiant que *newcontainer* est dans la liste de hello des conteneurs pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="03263-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="03263-155">Définir les autorisations du conteneur</span><span class="sxs-lookup"><span data-stu-id="03263-155">Set Container Permissions</span></span>
<span data-ttu-id="03263-156">Les autorisations d’un conteneur sont configurées pour l’accès **Privé** par défaut.</span><span class="sxs-lookup"><span data-stu-id="03263-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="03263-157">Toutefois, les conteneurs fournissent d’autres options pour l’accès aux conteneurs :</span><span class="sxs-lookup"><span data-stu-id="03263-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="03263-158">**Privé**: données de conteneur et les objets blob peuvent être lues par le propriétaire du compte hello.</span><span class="sxs-lookup"><span data-stu-id="03263-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="03263-159">**BLOB**: les données blob à l’intérieur de ce conteneur sont lisibles au moyen d’une demande anonyme, mais les données du conteneur ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="03263-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="03263-160">Les clients ne peuvent pas énumérer les objets BLOB conteneur hello via une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="03263-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="03263-161">**Conteneur**: les données de conteneur et blob sont lisibles au moyen d’une demande anonyme.</span><span class="sxs-lookup"><span data-stu-id="03263-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="03263-162">Les clients peuvent énumérer des objets BLOB dans le conteneur hello via une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="03263-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="03263-163">Hello exemple suivant vous montre comment toocreate un conteneur avec **conteneur** autorisations d’accès, qui autorise l’accès public en lecture seule pour tous les utilisateurs sur hello Internet :</span><span class="sxs-lookup"><span data-stu-id="03263-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="03263-164">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="03263-164">Upload a blob into a container</span></span>
<span data-ttu-id="03263-165">Comme mentionné dans hello [concepts du service d’objets Blob](#blob-service-concepts) section, le stockage d’objets Blob offre trois types différents d’objets BLOB : objets BLOB de blocs, d’objets BLOB d’ajout et d’objets BLOB de pages.</span><span class="sxs-lookup"><span data-stu-id="03263-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="03263-166">bibliothèque d’iOS Hello le stockage Azure prend en charge les trois types d’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="03263-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="03263-167">Dans la plupart des cas, objet blob de blocs est hello recommandé toouse de type.</span><span class="sxs-lookup"><span data-stu-id="03263-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="03263-168">Bonjour à l’exemple suivant montre comment tooupload un bloc d’objets blob à partir d’un NSString.</span><span class="sxs-lookup"><span data-stu-id="03263-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="03263-169">Si un objet blob avec le même nom existe déjà dans ce conteneur de hello, contenu hello de cet objet blob est écrasées.</span><span class="sxs-lookup"><span data-stu-id="03263-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="03263-170">Vous pouvez vérifier que cela fonctionne en examinant hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) et la vérification de ce conteneur hello, *containerpublic*, contient l’objet blob de hello, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="03263-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="03263-171">Dans cet exemple, nous avons utilisé un conteneur public afin de vérifier également que cette application a fonctionné par des objets BLOB toohello des va URI :</span><span class="sxs-lookup"><span data-stu-id="03263-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="03263-172">En outre toouploading un objet blob de blocs à partir d’un NSString, des méthodes semblables existent pour NSData, NSInputStream ou un fichier local.</span><span class="sxs-lookup"><span data-stu-id="03263-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="03263-173">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="03263-173">List hello blobs in a container</span></span>
<span data-ttu-id="03263-174">Hello suivant montre comment toolist tous les objets BLOB dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="03263-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="03263-175">Lorsque vous effectuez cette opération, tenez compte de hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="03263-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="03263-176">**continuationToken** -hello représente de jeton de continuation où hello opération de liste doit commencer.</span><span class="sxs-lookup"><span data-stu-id="03263-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="03263-177">Si aucun jeton n’est fourni, il répertorie les objets BLOB à partir du début de hello.</span><span class="sxs-lookup"><span data-stu-id="03263-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="03263-178">N’importe quel nombre d’objets BLOB peut être répertorié, à partir de zéro des tooa valeur maximale.</span><span class="sxs-lookup"><span data-stu-id="03263-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="03263-179">Même si cette méthode retourne les résultats de zéro, si `results.continuationToken` n’est pas nil, il peut y avoir plus d’objets BLOB sur le service de hello qui n’ont pas été répertoriés.</span><span class="sxs-lookup"><span data-stu-id="03263-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="03263-180">**préfixe** -vous pouvez spécifier toouse de préfixe hello pour une liste d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="03263-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="03263-181">Seuls les objets blob qui commencent par ce préfixe sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="03263-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="03263-182">**useFlatBlobListing** - comme indiqué dans hello [Naming et faisant référence à des conteneurs et objets BLOB](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, bien que hello service Blob est un schéma de stockage plat, vous pouvez créer une hiérarchie virtuelle en nommant les objets BLOB avec le chemin d’accès plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="03263-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="03263-183">Toutefois, les listes de stockage non plat ne sont actuellement pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="03263-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="03263-184">Cette fonctionnalité sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="03263-184">This feature is coming soon.</span></span> <span data-ttu-id="03263-185">Pour le moment, cette valeur doit être **YES**.</span><span class="sxs-lookup"><span data-stu-id="03263-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="03263-186">**blobListingDetails** -vous pouvez spécifier quels tooinclude éléments lors de la liste d’objets BLOB</span><span class="sxs-lookup"><span data-stu-id="03263-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="03263-187">_AZSBlobListingDetailsNone_ : répertorie uniquement les objets blob validés et ne renvoie pas de métadonnées d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="03263-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="03263-188">_AZSBlobListingDetailsSnapshots_ : répertorie les objets blob validés et les instantanés d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="03263-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="03263-189">_AZSBlobListingDetailsMetadata_: récupérer les métadonnées d’objets blob pour chaque objet blob est retourné dans la liste hello.</span><span class="sxs-lookup"><span data-stu-id="03263-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="03263-190">_AZSBlobListingDetailsUncommittedBlobs_ : répertorie les objets blob validés et non validés.</span><span class="sxs-lookup"><span data-stu-id="03263-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="03263-191">_AZSBlobListingDetailsCopy_: inclure copie les propriétés dans la liste hello.</span><span class="sxs-lookup"><span data-stu-id="03263-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="03263-192">_AZSBlobListingDetailsAll_ : répertorie tous les objets blob validés, objets blob non validés et instantanés disponibles, et renvoie l’état de toutes les métadonnées et de la copie pour ces objets blob.</span><span class="sxs-lookup"><span data-stu-id="03263-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="03263-193">**maxResults** -hello nombre maximal de tooreturn de résultats pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="03263-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="03263-194">Utilisez -1 toonot définie une limite.</span><span class="sxs-lookup"><span data-stu-id="03263-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="03263-195">**completionHandler** -bloc hello du code tooexecute avec résultats hello Hello opération de liste.</span><span class="sxs-lookup"><span data-stu-id="03263-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="03263-196">Dans cet exemple, une méthode d’assistance est utilisé toorecursively appel hello list blobs (méthode) chaque fois qu’un jeton de continuation est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="03263-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="03263-197">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="03263-197">Download a blob</span></span>
<span data-ttu-id="03263-198">Hello suivant montre l’exemple de comment toodownload un objet de NSString tooa blob.</span><span class="sxs-lookup"><span data-stu-id="03263-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="03263-199">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="03263-199">Delete a blob</span></span>
<span data-ttu-id="03263-200">Hello suivant montre l’exemple de comment toodelete un objet blob.</span><span class="sxs-lookup"><span data-stu-id="03263-200">hello following example shows how toodelete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="03263-201">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="03263-201">Delete a blob container</span></span>
<span data-ttu-id="03263-202">Hello suivant montre l’exemple de comment toodelete un conteneur.</span><span class="sxs-lookup"><span data-stu-id="03263-202">hello following example shows how toodelete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="03263-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03263-203">Next steps</span></span>
<span data-ttu-id="03263-204">Maintenant que vous avez appris comment toouse stockage d’objets Blob à partir d’iOS, suivez ces liens de toolearn plus sur la bibliothèque d’iOS hello et hello du service de stockage.</span><span class="sxs-lookup"><span data-stu-id="03263-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="03263-205">Bibliothèque cliente d’Azure Storage pour iOS</span><span class="sxs-lookup"><span data-stu-id="03263-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="03263-206">Documentation de référence d’Azure Storage pour iOS</span><span class="sxs-lookup"><span data-stu-id="03263-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="03263-207">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="03263-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="03263-208">Blog de l’équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="03263-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="03263-209">Si vous avez des questions sur cette bibliothèque, vous pouvez libre toopost tooour [forum MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [débordement de pile](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="03263-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="03263-210">Si vous avez des suggestions de fonctionnalités pour le stockage Azure, posez trop[des commentaires de stockage Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="03263-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

