---
title: aaaDevelop pour le stockage de fichiers Azure avec Java | Documents Microsoft
description: "Découvrez comment des applications Java toodevelop et les services qui utilisent des fichiers Azure storage toostore fichier des données."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Développer pour le stockage de fichiers Azure avec Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel va vous montrer bases hello de l’utilisation des applications Java toodevelop ou services qui utilisent des données de fichier toostore fichier Azure storage. Dans ce didacticiel, nous crée une application console simple et montrent comment les actions de base tooperform avec Java et le fichier Azure storage :

* Créer et supprimer des partages de fichiers Azure
* Créer et supprimer des répertoires
* Énumérer des fichiers et répertoires dans un partage de fichiers Azure
* Charger, télécharger et supprimer un fichier

> [!Note]  
> Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des classes d’e/s Java standard hello. Cet article décrit comment toowrite les applications qui utilisent hello SDK Java Azure Storage, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.

## <a name="create-a-java-application"></a>Création d’une application Java
exemples de hello toobuild, vous devez hello Kit de développement Java (JDK) et [] de hello (SDK de stockage Azure pour Java). Vous devez également avoir préalablement créé un compte de stockage Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Le programme d’installation de votre application de toouse stockage Azure
toouse hello API, le stockage Azure ajouter hello suivant en haut de toohello instruction hello du fichier de Java où vous avez l’intention tooaccess hello service de stockage.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion de stockage Azure
toouse stockage Azure, vous avez besoin de compte de stockage Azure tooconnect tooyour. Hello première étape serait tooconfigure une chaîne de connexion que nous allons utiliser compte de stockage tooconnect tooyour. Nous allons définir une toodo variable statique qui.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Remplacez your_storage_account_name et your_storage_account_key par des valeurs réelles de hello pour votre compte de stockage.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Connexion de compte de stockage Azure tooan
compte de stockage tooconnect tooyour, vous devez toouse hello **CloudStorageAccount** objet, en passant un tooits de chaîne de connexion **analyser** (méthode).

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** lève une InvalidKeyException et vous devrez donc tooput à l’intérieur d’une instruction try/catch bloquer.

## <a name="create-an-azure-file-share"></a>Création d’un partage de fichiers Azure
Tous les fichiers et répertoires d’un stockage de fichiers Azure se trouvent dans un conteneur appelé **Partage**. Votre compte de stockage peut avoir autant de partages que le permet la capacité de votre compte. partage de tooa accès tooobtain et son contenu, vous devez toouse un client de stockage de fichiers Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

À l’aide du client de stockage de fichier Azure hello, vous pouvez ensuite obtenir un partage de tooa de référence.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually créer le partage de hello, utilisez hello **createIfNotExists** méthode d’objet de CloudFileShare hello.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

À ce stade, **partager** contient un partage de tooa référence nommé **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Suppression d’un partage de fichiers Azure
Suppression d’un partage est effectuée en appelant hello **deleteIfExists** méthode sur un objet CloudFileShare. Voici un exemple de code permettant d’effectuer cette opération.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Créer un répertoire
Vous pouvez également organiser le stockage en plaçant les fichiers dans les sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello. Stockage de fichier Azure vous permet de toocreate que le permettent de répertoires car votre compte. code Hello ci-dessous crée un sous-répertoire nommé **sampledir** sous le répertoire racine de hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>Supprimer un répertoire
La suppression d’un répertoire est une tâche relativement simple, mais il convient de noter que vous ne pouvez pas supprimer de répertoire contenant des fichiers ou d’autres répertoires.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Énumérer des fichiers et répertoires dans un partage de fichiers Azure
Il est facile d’obtenir la liste de fichiers et de répertoires d’un partage en appelant **listFilesAndDirectories** sur une référence CloudFileDirectory. méthode Hello retourne une liste d’objets ListFileItem dont vous pouvez effectuer une itération sur. Par exemple, hello de code suivant répertorie les fichiers et répertoires à l’intérieur du répertoire racine de hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Charger un fichier
Un fichier Azure partage contient de hello très moins, un répertoire racine où les fichiers peuvent résider. Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.

première étape de Hello lors du téléchargement d’un fichier est tooobtain un répertoire toohello de référence où elle doit résider. Pour ce faire, l’appelant hello **getRootDirectoryReference** méthode d’objet de partage hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Maintenant que vous avez un répertoire de racine référence toohello du partage de hello, vous pouvez télécharger un fichier sur celui-ci à l’aide de hello suivant de code.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Téléchargement d’un fichier
Un des plus fréquentes sur le stockage de fichiers Azure, vous allez effectuer les opérations de hello est les fichiers toodownload. Dans l’exemple suivant de hello, code de hello télécharge SampleFile.txt et affiche son contenu.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Supprimer un fichier
La suppression de fichiers est également une opération courante liée au stockage des fichiers Azure. Hello de code suivant supprime un fichier nommé SampleFile.txt stocké à l’intérieur d’un répertoire nommé **sampledir**.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez que toolearn plus d’informations sur d’autres API de stockage Azure, suivez ces liens.

* [Centre de développement Java](http://azure.microsoft.com/develop/java/)
* [Kit de développement logiciel (SDK) Azure Storage pour Java](https://github.com/azure/azure-storage-java)
* [Kit de développement logiciel (SDK) Azure Storage pour Android](https://github.com/azure/azure-storage-android)
* [Référence du Kit de développement logiciel (SDK) du client Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)
