---
title: "aaaHow toouse le stockage Blob Azure (stockage d’objets) à partir de Java | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a905d318abdaa7538ec3f6b53b5186b965b8b86e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Comment toouse stockage d’objets Blob à partir de Java
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Vue d'ensemble
Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Cet article vous explique comment tooperform des scénarios courants utilisant hello stockage d’objets Blob Microsoft Azure. exemples de Hello sont écrits en Java et utiliser hello [SDK de stockage Azure pour Java][Azure Storage SDK for Java]. Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB. Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#Next-Steps) section.

> [!NOTE]
> un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android. Pour plus d’informations, consultez hello [stockage de Azure SDK pour Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Création d’une application Java
Dans cet article, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local ou dans le code d’un rôle Web ou d’un rôle de travail dans Azure.

toodo par conséquent, vous devez tooinstall hello du Kit de développement Java (JDK) et créer un compte de stockage Azure dans votre abonnement Azure. Une fois que vous l’avez fait, vous devez tooverify votre système de développement répond aux exigences minimales de hello et les dépendances qui sont répertoriées dans hello [SDK de stockage Azure pour Java] [ Azure Storage SDK for Java] référentiel sur GitHub. Si votre système répond à ces exigences, vous pouvez suivre les instructions de hello pour télécharger et installer les bibliothèques de stockage Azure hello pour Java sur votre système à partir de ce référentiel. Une fois ces tâches terminées, vous serez en mesure de toocreate une application Java qui utilise des exemples de hello dans cet article.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurer votre application de tooaccess stockage d’objets Blob
Ajoutez hello après importation instructions toohello haut du fichier de Java hello où vous souhaitez toouse hello API de stockage Azure tooaccess BLOB.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurer une chaîne de connexion au stockage Azure
Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données. Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom de hello de votre compte de stockage et clé d’accès primaire pour le compte de stockage hello dans hello de hello [portail Azure](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs. Hello suivant montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Dans une application en cours d’exécution au sein d’un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service hello, *ServiceConfiguration.cscfg*et sont accessibles avec un appel toohello  **RoleEnvironment.getConfigurationSettings** (méthode). chaîne de connexion hello obtient Hello suivant un **paramètre** élément nommé *StorageConnectionString* dans le fichier de configuration de service hello.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.

## <a name="create-a-container"></a>Créez un conteneur.
Un objet **CloudBlobClient** vous permet d’obtenir les objets de référence des conteneurs et objets blob. Hello de code suivant crée un **CloudBlobClient** objet.

> [!NOTE]
> Il existe des méthodes supplémentaires toocreate **CloudStorageAccount** objets ; pour plus d’informations, consultez **CloudStorageAccount** Bonjour [référence de kit de développement logiciel Azure Storage Client].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Hello d’utilisation **CloudBlobClient** tooget un référence toohello conteneur toouse de l’objet. Vous pouvez créer le conteneur de hello s’il n’existe avec hello **createIfNotExists** méthode qui retourne un conteneur existant hello dans le cas contraire. Par défaut, le nouveau conteneur de hello est privé, vous devez spécifier votre clé d’accès (comme précédemment) BLOB toodownload à partir de ce conteneur.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Optionnel : configuration d’un conteneur pour un accès public
Autorisations d’un conteneur sont configurées pour l’accès privé par défaut, mais vous pouvez facilement configurer autorisations tooallow publics en lecture seule accès d’un conteneur pour tous les utilisateurs sur hello Internet :

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
tooupload un objet blob tooa de fichier, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux en appelant le téléchargement sur la référence d’objet blob hello. Cette opération va créer l’objet blob de hello si elle n’existe, ou vous pouvez remplacer si c’est le cas. Bonjour suivant l’exemple de code illustre ce point et suppose que le conteneur de hello a déjà été créé.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur comme vous le faisiez tooupload un objet blob. Vous pouvez utiliser du conteneur hello **listBlobs** méthode avec un **pour** boucle. Hello de code suivant génère hello Uri de chaque objet blob dans une console toohello de conteneur.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Notez que les noms que vous attribuez aux objets blob peuvent inclure des informations de chemin d’accès. Vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel. Notez que structure de répertoire hello est virtuel uniquement hello uniquement les ressources disponibles dans le stockage d’objets Blob sont les conteneurs et les objets BLOB. Toutefois, la bibliothèque cliente de hello propose un **CloudBlobDirectory** répertoire virtuel de toorefer tooa de l’objet et de simplifier les processus de hello de travailler avec des objets BLOB qui sont organisées de cette façon.

Par exemple, vous pouvez avoir un conteneur nommé « photos », dans lequel vous pouvez télécharger des objets blob nommés « rootphoto1 », « 2010/photo1 », « 2010/photo2 » et « 2011/photo1 ». Cela crée hello répertoires virtuels « 2010 » et « 2011 » dans le conteneur de « photos » hello. Lorsque vous appelez **listBlobs** sur le conteneur de « photos » hello, collection hello retournée contiendra **CloudBlobDirectory** et **CloudBlob** objets représentant hello les répertoires et les objets BLOB contenus au niveau supérieur de hello. Dans ce cas, les répertoires « 2010 » et « 2011 » et la photo « rootphoto1 » sont renvoyés. Vous pouvez utiliser hello **instanceof** opérateur toodistinguish ces objets.

Si vous le souhaitez, vous pouvez passer dans les paramètres toohello **listBlobs** méthode avec hello **useFlatBlobListing** paramètre la valeur tootrue. Cela permet de renvoyer chaque objet blob, indépendamment du répertoire. Pour plus d’informations, consultez **CloudBlobContainer.listBlobs** Bonjour [référence de kit de développement logiciel Azure Storage Client].

## <a name="download-a-blob"></a>Téléchargement d’un objet blob
objets BLOB toodownload, suivez hello même étapes comme vous l’avez fait pour le chargement d’un objet blob dans l’ordre tooget une référence d’objet blob. Bonjour télécharger l’exemple, vous avez appelé téléchargement sur l’objet blob de hello. Dans l’exemple suivant de hello, appelez téléchargement tootransfer hello contenu tooa flux de données objet blob comme un **FileOutputStream** que vous pouvez utiliser le fichier local de tooa toopersist hello blob.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Supprimer un objet blob
toodelete un objet blob, obtenir un objet blob de référence et appelez **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Suppression d’un conteneur d’objets blob
Enfin, toodelete un conteneur d’objets blob, obtenir un objet blob de référence de conteneur, puis appelez **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* [Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]
* [référence de kit de développement logiciel Azure Storage Client][référence de kit de développement logiciel Azure Storage Client]
* [API REST Stockage Azure][Azure Storage REST API]
* [Blog de l’équipe Stockage Azure][Azure Storage Team Blog]

Pour plus d’informations, consultez aussi [Azure pour les développeurs Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[référence de kit de développement logiciel Azure Storage Client]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
