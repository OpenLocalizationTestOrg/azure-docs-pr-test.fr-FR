---
title: "application aaaOn local avec le stockage d’objets blob (Java) | Documents Microsoft"
description: "Découvrez comment toocreate une application console qui télécharge un tooAzure d’image, puis affiche hello image dans votre navigateur. Les exemples de code sont écrits en Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Application locale avec stockage d’objets blob
## <a name="overview"></a>Vue d'ensemble
Hello suivant montre comment vous pouvez utiliser le stockage Azure pour stocker les images dans Azure. code Hello dans cet article est pour une application console qui télécharge un tooAzure d’image, puis crée un fichier HTML qui affiche l’image de hello dans votre navigateur.

## <a name="prerequisites"></a>Composants requis
* Le Kit de développement logiciel Java (JDK) version 1.6 ou ultérieure est installé.
* Bonjour Azure SDK est installé.
* Bonjour JAR pour hello les bibliothèques Azure pour Java et les fichiers JAR dépendance applicable, est installés et se trouvent dans le chemin d’accès de build hello utilisé par le compilateur Java. Pour plus d’informations sur l’installation des bibliothèques de Azure hello pour Java, consultez [téléchargement hello SDK Azure pour Java](../java-download-azure-sdk.md).
* Un compte de stockage Azure a été configuré. Hello nom de compte et de la clé de compte pour le compte de stockage hello servira par code hello dans cet article. Consultez [comment tooCreate un compte de stockage](storage-create-storage-account.md#create-a-storage-account) pour plus d’informations sur la création d’un compte de stockage et [clés d’accès afficher et copier](storage-create-storage-account.md#view-and-copy-storage-access-keys) pour plus d’informations sur la récupération de clé de compte hello.
* Vous avez créé un fichier d’image locale nommé stockés sur hello path c:\\myimages\\image1.jpg. Vous pouvez également modifier le **FileInputStream** constructeur dans hello exemple toouse un image différente chemin d’accès et nom de fichier.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload de stockage d’objets blob Azure toouse un fichier
La procédure présentée ici détaille chaque étape. Si vous souhaitez que tooskip de manière anticipée, code d’entier hello est présenté plus loin dans cet article.

Commencer le code de hello en incluant des imports pour les classes de stockage Azure de base hello, classes de client d’objets blob Azure hello, classes d’e/s Java hello et hello **URISyntaxException** classe.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Déclarez une classe nommée **StorageSample**et inclure le crochet hello, **{**.

```java
public class StorageSample {
```

Au sein de hello **StorageSample** de classe, déclarez une variable de chaîne qui contiendra le protocole de point de terminaison hello par défaut, le nom de votre compte de stockage et votre clé d’accès, tel que spécifié dans votre compte de stockage Azure. Remplacez les valeurs d’espace réservé hello **votre\_compte\_nom** et **votre\_compte\_clé** avec votre propre nom de compte et de la clé de compte, respectivement.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Ajouter dans votre déclaration de **principal**, inclure un **essayez** bloquer et inclure des crochets ouvrants nécessaires de hello, **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Déclarer des variables de hello suite type (hello sont des descriptions de la façon dont elles sont utilisées dans cet exemple) :

* **CloudStorageAccount**: objet avec votre nom de compte de stockage Azure et la clé et la toocreate du compte utilisé tooinitialize hello l’objet blob du client.
* **CloudBlobClient**: tooaccess hello blob service utilisés.
* **CloudBlobContainer**: toocreate utilisé un conteneur d’objets blob, liste d’objets BLOB dans le conteneur de hello et delete hello conteneur.
* **CloudBlockBlob**: tooupload utilisé un conteneur toothe du fichier image locale.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Affecter une valeur toohello **compte** variable.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Affecter une valeur toohello **serviceClient** variable.

```java
serviceClient = account.createCloudBlobClient();
```

Affecter une valeur toohello **conteneur** variable. Nous obtenons un conteneur de tooa référence nommé **mise en route**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Créer un conteneur de hello. Cette méthode crée le conteneur de hello si elle n’existe pas (et retourner **true**). Si le conteneur de hello existe, elle retournera **false**. Une alternative trop**createIfNotExists** est hello **créer** (méthode) (qui retourne une erreur si le conteneur de hello existe déjà).

```java
container.createIfNotExists();
```

Définir l’accès anonyme pour le conteneur de hello.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Obtenir un référence toohello objet blob de blocs, qui représente les blob hello dans le stockage Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Hello d’utilisation **fichier** constructeur tooget un fichier toohello créé localement de référence que vous allez télécharger. Assurez-vous que vous avez créé ce fichier avant d’exécuter le code de hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Télécharger hello le fichier local via un appel de toohello **CloudBlockBlob.upload** (méthode). Hello premier paramètre toohello **CloudBlockBlob.upload** méthode est un **FileInputStream** ce fichier local de hello représente qui sera téléchargé tooAzure stockage de l’objet. Hello deuxième paramètre est hello taille, en octets, du fichier de hello.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Appeler une fonction d’assistance nommée **MakeHTMLPage**, page toomake un contenu HTML de base qui contient un  **&lt;image&gt;**  élément avec hello ensemble toohello objet blob source qui est désormais dans votre Azure compte de stockage. Hello code **MakeHTMLPage** l’aborderons plus loin dans cet article.

```java
MakeHTMLPage(container);
```

Imprime un message d’état et les informations sur hello créé de page HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Fermer hello **essayez** bloc en insérant un crochet fermant : **}**

Gérer hello suivant des exceptions :

* **FileNotFoundException**: pouvant être levées par hello **FileInputStream** ou **FileOutputStream** constructeurs.
* **StorageException**: pouvant être levées par la bibliothèque de stockage Azure client hello.
* **URISyntaxException**: pouvant être levées par hello **ListBlobItem.getUri** (méthode).
* **Exception**: traitement d’une exception générique.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Fermez **main** en insérant une parenthèse fermante : **}**

Créez une méthode nommée **MakeHTMLPage** page de toocreate un contenu HTML de base. Cette méthode a un paramètre de type **CloudBlobContainer**, qui sera utilisé tooiterate liste hello d’objets BLOB téléchargés. Cette méthode lève les exceptions de type **FileNotFoundException**, qui peuvent être levé par hello **FileOutputStream** constructeur, et **URISyntaxException**, ce qui risque levée par hello **ListBlobItem.getUri** (méthode). Incluez le crochet ouvrant **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Créez un fichier local nommé **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Écrire le fichier local toohello, ajout Bonjour  **&lt;html&gt;**,  **&lt;en-tête&gt;**, et  **&lt;corps&gt;**  éléments.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Parcourir la liste hello d’objets BLOB téléchargés. Pour chaque objet blob, dans la page de hello HTML, créez un  **&lt;img&gt;**  élément qui a son **src** attribut envoyé Hello URI d’objet blob de hello telle qu’elle existe dans votre compte de stockage Azure.
Dans cet exemple, vous avez ajouté une seule image, mais si vous en ajoutiez plus, ce code effectuerait une itération pour chacune d'entre elles.

Par souci de simplification, cet exemple part du principe que chaque objet blob chargé est une image. Si vous avez mis à jour des objets BLOB autres que des images ou des objets BLOB de pages au lieu d’objets BLOB de blocs, ajustez le code hello en fonction des besoins.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Fermer hello  **&lt;corps&gt;**  élément et hello  **&lt;html&gt;**  élément.

```java
stream.println("</body>");
stream.println("</html>");
```

Fichier local de fermer hello.

```java
stream.close();
```

Fermez **MakeHTMLPage** en insérant une parenthèse fermante : **}**

Fermez **StorageSample** en insérant une parenthèse fermante : **}**

Hello Voici code complet de hello pour cet exemple. N’oubliez pas de valeurs d’espace réservé hello toomodify **votre\_compte\_nom** et **votre\_compte\_clé** toouse votre nom de compte et un compte la clé, respectivement.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

Dans Ajout toouploading votre stockage tooAzure du fichier image locale, hello exemple de code crée un fichier local namedindex.html, que vous pouvez ouvrir dans votre navigateur toosee votre image téléchargée.

Étant donné que le code de hello contient votre nom de compte et votre clé de compte, assurez-vous que votre code source est sécurisé.

## <a name="toodelete-a-container"></a>toodelete un conteneur
Vous êtes facturé pour le stockage, il est souhaitable toodelete le **mise en route** conteneur une fois que vous avez terminé expérimenter de cet exemple. toodelete un conteneur, utilisez hello **CloudBlobContainer.delete** (méthode).

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

toocall hello **CloudBlobContainer.delete** (méthode), le processus hello d’initialisation **CloudStorageAccount**, **ClodBlobClient**, et  **CloudBlobContainer** objets est hello identique à celui décrit pour le **createIfNotExist** (méthode). Hello Voici un exemple complet que les suppressions hello conteneur nommé **mise en route**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Pour une vue d’ensemble des autres classes de stockage d’objets blob et les méthodes, consultez [comment toouse stockage d’objets Blob à partir de Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur les tâches de stockage plus complexes.

* [Kit de développement logiciel (SDK) Azure Storage pour Java](https://github.com/azure/azure-storage-java)
* [Référence du Kit de développement logiciel (SDK) du client Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog de l'équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

