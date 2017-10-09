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
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Comment toouse stockage d’objets Blob à partir d’iOS
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article vous indiquent comment les scénarios courants tooperform à l’aide du stockage d’objets Blob Microsoft Azure. les exemples de Hello sont écrites en Objective-C et utiliser hello [bibliothèque cliente de stockage Azure pour iOS](https://github.com/Azure/azure-storage-ios). Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB. Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#next-steps) section. Vous pouvez également télécharger hello [exemple d’application](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly voir hello utilisation du stockage Azure dans une application iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Importer la bibliothèque e/s de stockage Azure hello dans votre application
Vous pouvez importer des bibliothèque e/s de stockage Azure hello dans votre application à l’aide de hello [CocoaPod de stockage Azure](https://cocoapods.org/pods/AZSClient) ou en important hello **Framework** fichier. CocoaPod est hello recommandé de façon qu’il facilite la bibliothèque de hello intégrés, toutefois l’importation à partir du fichier de framework hello est moins importun pour votre projet existant.

toouse cette bibliothèque, vous devez hello suivant :
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. Si vous n’avez pas déjà fait, [CocoaPods d’installer](https://guides.cocoapods.org/using/getting-started.html#toc_3) sur votre ordinateur en ouvrant une fenêtre de terminal et en cours d’exécution hello commande suivante
    
    ```shell   
    sudo gem install cocoapods
    ```

2. Ensuite, dans le répertoire du projet hello (directory hello contenant votre fichier .xcodeproj), créez un nouveau fichier appelé _Podfile_(aucune extension de fichier). Ajoutez hello suivant too_Podfile_ et enregistrez.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. Dans la fenêtre de terminal hello, accédez à toohello répertoire de projet et exécution hello commande suivante

    ```shell    
    pod install
    ```

4. Si votre fichier .xcodeproj est ouvert dans Xcode, fermez-le. Dans votre fichier de projet projet Active hello ouverts récemment créé qui disposent d’extension de .xcworkspace hello. Il s’agit de fichier hello que vous allez utiliser à partir de maintenant.

## <a name="framework"></a>Framework
Hello autre bibliothèque de hello toouse est framework de hello toobuild manuellement de façon :

1. First, téléchargement ou hello du clone [référentiel d’azure-stockage-e/s](https://github.com/azure/azure-storage-ios).
2. Accédez à *azure-storage-ios* -> *Bibliothèque* -> *Bibliothèque cliente Azure Storage*, puis ouvrez `AZSClient.xcodeproj` dans Xcode.
3. À hello en haut à gauche de Xcode, hello de modification active schéma à partir de « Bibliothèque cliente de stockage Azure » trop « Framework ».
4. Générez le projet hello (⌘ + B). Cela créera un fichier `AZSClient.framework` sur votre bureau.

Vous pouvez ensuite importer le fichier de framework hello dans votre application de manière hello suivante :

1. Créez un projet ou ouvrez votre projet existant dans Xcode.
2. Glisser- déposer hello `AZSClient.framework` dans votre navigateur de projet Xcode.
3. Sélectionnez *Copier les éléments si besoin*, puis cliquez sur *Terminer*.
4. Cliquez sur votre projet dans la navigation de gauche hello et cliquez sur hello *général* onglet en haut de hello de l’éditeur de projet hello.
5. Sous hello *lié infrastructures et bibliothèques* , cliquez sur le bouton Ajouter de hello (+).
6. Dans la liste hello bibliothèques déjà fournies, recherchez `libxml2.2.tbd` et ajoutez-le tooyour projet.

## <a name="import-hello-library"></a>Importer la bibliothèque de hello 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

Si vous utilisez Swift, sera toocreate un en-tête de transition et les importer < AZSClient/AZSClient.h > il :

1. Créer un fichier d’en-tête `Bridging-Header.h`et ajoutez hello ci-dessus instruction d’importation.
2. Accédez toohello *paramètres de génération* onglet et recherchez *en-tête de pontage Objective-C*.
3. Double-cliquez sur le champ hello de *en-tête de Objective-C Bridging* et ajoutez le fichier d’en-tête tooyour hello chemin d’accès :`ProjectName/Bridging-Header.h`
4. Build hello projet (⌘ + B) tooverify qui hello bridging en-tête a été récupéré par Xcode.
5. Démarrer à l’aide de la bibliothèque de hello directement dans n’importe quel fichier Swift, il n’est pas nécessaire pour les instructions d’importation.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Opérations asynchrones
> [!NOTE]
> Toutes les méthodes qui effectuent une demande de service de hello sont des opérations asynchrones. Vous trouverez dans les exemples de code hello, que ces méthodes ont un gestionnaire d’achèvement. Le code à l’intérieur du Gestionnaire d’achèvement hello s’exécutera **après** hello demande est terminée. Le code après l’exécution de gestionnaire d’achèvement hello **tandis que** hello requête est effectuée.
> 
> 

## <a name="create-a-container"></a>Créez un conteneur.
Chaque objet blob dans Azure Storage doit résider dans un conteneur. Hello exemple suivant montre comment toocreate un conteneur, appelée *newcontainer*, dans votre compte de stockage s’il n’existe pas. Lorsque vous choisissez un nom pour votre conteneur, tenez compte de hello mentionnés ci-dessus des règles d’affectation de noms.

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

Vous pouvez vérifier que cela fonctionne en examinant hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) et en vérifiant que *newcontainer* est dans la liste de hello des conteneurs pour votre compte de stockage.

## <a name="set-container-permissions"></a>Définir les autorisations du conteneur
Les autorisations d’un conteneur sont configurées pour l’accès **Privé** par défaut. Toutefois, les conteneurs fournissent d’autres options pour l’accès aux conteneurs :

* **Privé**: données de conteneur et les objets blob peuvent être lues par le propriétaire du compte hello.
* **BLOB**: les données blob à l’intérieur de ce conteneur sont lisibles au moyen d’une demande anonyme, mais les données du conteneur ne sont pas disponibles. Les clients ne peuvent pas énumérer les objets BLOB conteneur hello via une demande anonyme.
* **Conteneur**: les données de conteneur et blob sont lisibles au moyen d’une demande anonyme. Les clients peuvent énumérer des objets BLOB dans le conteneur hello via une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.

Hello exemple suivant vous montre comment toocreate un conteneur avec **conteneur** autorisations d’accès, qui autorise l’accès public en lecture seule pour tous les utilisateurs sur hello Internet :

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

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Comme mentionné dans hello [concepts du service d’objets Blob](#blob-service-concepts) section, le stockage d’objets Blob offre trois types différents d’objets BLOB : objets BLOB de blocs, d’objets BLOB d’ajout et d’objets BLOB de pages. bibliothèque d’iOS Hello le stockage Azure prend en charge les trois types d’objets BLOB. Dans la plupart des cas, objet blob de blocs est hello recommandé toouse de type.

Bonjour à l’exemple suivant montre comment tooupload un bloc d’objets blob à partir d’un NSString. Si un objet blob avec le même nom existe déjà dans ce conteneur de hello, contenu hello de cet objet blob est écrasées.

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

Vous pouvez vérifier que cela fonctionne en examinant hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) et la vérification de ce conteneur hello, *containerpublic*, contient l’objet blob de hello, *sampleblob*. Dans cet exemple, nous avons utilisé un conteneur public afin de vérifier également que cette application a fonctionné par des objets BLOB toohello des va URI :

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

En outre toouploading un objet blob de blocs à partir d’un NSString, des méthodes semblables existent pour NSData, NSInputStream ou un fichier local.

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
Hello suivant montre comment toolist tous les objets BLOB dans un conteneur. Lorsque vous effectuez cette opération, tenez compte de hello paramètres suivants :     

* **continuationToken** -hello représente de jeton de continuation où hello opération de liste doit commencer. Si aucun jeton n’est fourni, il répertorie les objets BLOB à partir du début de hello. N’importe quel nombre d’objets BLOB peut être répertorié, à partir de zéro des tooa valeur maximale. Même si cette méthode retourne les résultats de zéro, si `results.continuationToken` n’est pas nil, il peut y avoir plus d’objets BLOB sur le service de hello qui n’ont pas été répertoriés.
* **préfixe** -vous pouvez spécifier toouse de préfixe hello pour une liste d’objets blob. Seuls les objets blob qui commencent par ce préfixe sont répertoriés.
* **useFlatBlobListing** - comme indiqué dans hello [Naming et faisant référence à des conteneurs et objets BLOB](#naming-and-referencing-containers-and-blobs) section, bien que hello service Blob est un schéma de stockage plat, vous pouvez créer une hiérarchie virtuelle en nommant les objets BLOB avec le chemin d’accès plus d’informations. Toutefois, les listes de stockage non plat ne sont actuellement pas prises en charge. Cette fonctionnalité sera bientôt disponible. Pour le moment, cette valeur doit être **YES**.
* **blobListingDetails** -vous pouvez spécifier quels tooinclude éléments lors de la liste d’objets BLOB
  * _AZSBlobListingDetailsNone_ : répertorie uniquement les objets blob validés et ne renvoie pas de métadonnées d’objet blob.
  * _AZSBlobListingDetailsSnapshots_ : répertorie les objets blob validés et les instantanés d’objets blob.
  * _AZSBlobListingDetailsMetadata_: récupérer les métadonnées d’objets blob pour chaque objet blob est retourné dans la liste hello.
  * _AZSBlobListingDetailsUncommittedBlobs_ : répertorie les objets blob validés et non validés.
  * _AZSBlobListingDetailsCopy_: inclure copie les propriétés dans la liste hello.
  * _AZSBlobListingDetailsAll_ : répertorie tous les objets blob validés, objets blob non validés et instantanés disponibles, et renvoie l’état de toutes les métadonnées et de la copie pour ces objets blob.
* **maxResults** -hello nombre maximal de tooreturn de résultats pour cette opération. Utilisez -1 toonot définie une limite.
* **completionHandler** -bloc hello du code tooexecute avec résultats hello Hello opération de liste.

Dans cet exemple, une méthode d’assistance est utilisé toorecursively appel hello list blobs (méthode) chaque fois qu’un jeton de continuation est renvoyé.

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

## <a name="download-a-blob"></a>Téléchargement d’un objet blob
Hello suivant montre l’exemple de comment toodownload un objet de NSString tooa blob.

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

## <a name="delete-a-blob"></a>Supprimer un objet blob
Hello suivant montre l’exemple de comment toodelete un objet blob.

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

## <a name="delete-a-blob-container"></a>Suppression d’un conteneur d’objets blob
Hello suivant montre l’exemple de comment toodelete un conteneur.

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris comment toouse stockage d’objets Blob à partir d’iOS, suivez ces liens de toolearn plus sur la bibliothèque d’iOS hello et hello du service de stockage.

* [Bibliothèque cliente d’Azure Storage pour iOS](https://github.com/azure/azure-storage-ios)
* [Documentation de référence d’Azure Storage pour iOS](http://azure.github.io/azure-storage-ios/)
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage)

Si vous avez des questions sur cette bibliothèque, vous pouvez libre toopost tooour [forum MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) ou [débordement de pile](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Si vous avez des suggestions de fonctionnalités pour le stockage Azure, posez trop[des commentaires de stockage Azure](https://feedback.azure.com/forums/217298-storage/).

