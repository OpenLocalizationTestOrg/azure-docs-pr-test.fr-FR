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
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="cb04a-103">Comment toouse stockage d’objets Blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="cb04a-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="cb04a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cb04a-104">Overview</span></span>
<span data-ttu-id="cb04a-105">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb04a-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="cb04a-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="cb04a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="cb04a-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="cb04a-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="cb04a-108">Cet article vous explique comment tooperform des scénarios courants utilisant hello stockage d’objets Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cb04a-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="cb04a-109">exemples de Hello sont écrits en Java et utiliser hello [SDK de stockage Azure pour Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="cb04a-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="cb04a-110">Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb04a-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="cb04a-111">Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#Next-Steps) section.</span><span class="sxs-lookup"><span data-stu-id="cb04a-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="cb04a-112">un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="cb04a-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="cb04a-113">Pour plus d’informations, consultez hello [stockage de Azure SDK pour Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="cb04a-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="cb04a-114">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="cb04a-114">Create a Java application</span></span>
<span data-ttu-id="cb04a-115">Dans cet article, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local ou dans le code d’un rôle Web ou d’un rôle de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cb04a-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="cb04a-116">toodo par conséquent, vous devez tooinstall hello du Kit de développement Java (JDK) et créer un compte de stockage Azure dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cb04a-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="cb04a-117">Une fois que vous l’avez fait, vous devez tooverify votre système de développement répond aux exigences minimales de hello et les dépendances qui sont répertoriées dans hello [SDK de stockage Azure pour Java] [ Azure Storage SDK for Java] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb04a-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="cb04a-118">Si votre système répond à ces exigences, vous pouvez suivre les instructions de hello pour télécharger et installer les bibliothèques de stockage Azure hello pour Java sur votre système à partir de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="cb04a-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="cb04a-119">Une fois ces tâches terminées, vous serez en mesure de toocreate une application Java qui utilise des exemples de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cb04a-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="cb04a-120">Configurer votre application de tooaccess stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="cb04a-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="cb04a-121">Ajoutez hello après importation instructions toohello haut du fichier de Java hello où vous souhaitez toouse hello API de stockage Azure tooaccess BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb04a-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="cb04a-122">Configurer une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cb04a-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="cb04a-123">Un client de stockage Azure utilise une terminaison de stockage connexion chaîne toostore et informations d’identification pour accéder aux services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="cb04a-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="cb04a-124">Lors de l’exécution dans une application cliente, vous devez fournir la chaîne de connexion de stockage hello Bonjour suivant le format, à l’aide du nom de hello de votre compte de stockage et clé d’accès primaire pour le compte de stockage hello dans hello de hello [portail Azure](https://portal.azure.com)pour hello *AccountName* et *AccountKey* valeurs.</span><span class="sxs-lookup"><span data-stu-id="cb04a-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="cb04a-125">Hello suivant montre comment vous pouvez déclarer une chaîne de connexion de champ statique toohold hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="cb04a-126">Dans une application en cours d’exécution au sein d’un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service hello, *ServiceConfiguration.cscfg*et sont accessibles avec un appel toohello  **RoleEnvironment.getConfigurationSettings** (méthode).</span><span class="sxs-lookup"><span data-stu-id="cb04a-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="cb04a-127">chaîne de connexion hello obtient Hello suivant un **paramètre** élément nommé *StorageConnectionString* dans le fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="cb04a-128">Hello exemples suivants supposent que vous avez utilisé une de ces chaînes de connexion de stockage de deux méthodes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="cb04a-129">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb04a-129">Create a container</span></span>
<span data-ttu-id="cb04a-130">Un objet **CloudBlobClient** vous permet d’obtenir les objets de référence des conteneurs et objets blob.</span><span class="sxs-lookup"><span data-stu-id="cb04a-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="cb04a-131">Hello de code suivant crée un **CloudBlobClient** objet.</span><span class="sxs-lookup"><span data-stu-id="cb04a-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="cb04a-132">Il existe des méthodes supplémentaires toocreate **CloudStorageAccount** objets ; pour plus d’informations, consultez **CloudStorageAccount** Bonjour [référence de kit de développement logiciel Azure Storage Client].</span><span class="sxs-lookup"><span data-stu-id="cb04a-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="cb04a-133">Hello d’utilisation **CloudBlobClient** tooget un référence toohello conteneur toouse de l’objet.</span><span class="sxs-lookup"><span data-stu-id="cb04a-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="cb04a-134">Vous pouvez créer le conteneur de hello s’il n’existe avec hello **createIfNotExists** méthode qui retourne un conteneur existant hello dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="cb04a-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="cb04a-135">Par défaut, le nouveau conteneur de hello est privé, vous devez spécifier votre clé d’accès (comme précédemment) BLOB toodownload à partir de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb04a-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="cb04a-136">Optionnel : configuration d’un conteneur pour un accès public</span><span class="sxs-lookup"><span data-stu-id="cb04a-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="cb04a-137">Autorisations d’un conteneur sont configurées pour l’accès privé par défaut, mais vous pouvez facilement configurer autorisations tooallow publics en lecture seule accès d’un conteneur pour tous les utilisateurs sur hello Internet :</span><span class="sxs-lookup"><span data-stu-id="cb04a-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="cb04a-138">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="cb04a-138">Upload a blob into a container</span></span>
<span data-ttu-id="cb04a-139">tooupload un objet blob tooa de fichier, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="cb04a-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="cb04a-140">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux en appelant le téléchargement sur la référence d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="cb04a-141">Cette opération va créer l’objet blob de hello si elle n’existe, ou vous pouvez remplacer si c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="cb04a-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="cb04a-142">Bonjour suivant l’exemple de code illustre ce point et suppose que le conteneur de hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="cb04a-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="cb04a-143">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="cb04a-143">List hello blobs in a container</span></span>
<span data-ttu-id="cb04a-144">objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur comme vous le faisiez tooupload un objet blob.</span><span class="sxs-lookup"><span data-stu-id="cb04a-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="cb04a-145">Vous pouvez utiliser du conteneur hello **listBlobs** méthode avec un **pour** boucle.</span><span class="sxs-lookup"><span data-stu-id="cb04a-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="cb04a-146">Hello de code suivant génère hello Uri de chaque objet blob dans une console toohello de conteneur.</span><span class="sxs-lookup"><span data-stu-id="cb04a-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="cb04a-147">Notez que les noms que vous attribuez aux objets blob peuvent inclure des informations de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="cb04a-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="cb04a-148">Vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel.</span><span class="sxs-lookup"><span data-stu-id="cb04a-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="cb04a-149">Notez que structure de répertoire hello est virtuel uniquement hello uniquement les ressources disponibles dans le stockage d’objets Blob sont les conteneurs et les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb04a-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="cb04a-150">Toutefois, la bibliothèque cliente de hello propose un **CloudBlobDirectory** répertoire virtuel de toorefer tooa de l’objet et de simplifier les processus de hello de travailler avec des objets BLOB qui sont organisées de cette façon.</span><span class="sxs-lookup"><span data-stu-id="cb04a-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="cb04a-151">Par exemple, vous pouvez avoir un conteneur nommé « photos », dans lequel vous pouvez télécharger des objets blob nommés « rootphoto1 », « 2010/photo1 », « 2010/photo2 » et « 2011/photo1 ».</span><span class="sxs-lookup"><span data-stu-id="cb04a-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="cb04a-152">Cela crée hello répertoires virtuels « 2010 » et « 2011 » dans le conteneur de « photos » hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="cb04a-153">Lorsque vous appelez **listBlobs** sur le conteneur de « photos » hello, collection hello retournée contiendra **CloudBlobDirectory** et **CloudBlob** objets représentant hello les répertoires et les objets BLOB contenus au niveau supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="cb04a-154">Dans ce cas, les répertoires « 2010 » et « 2011 » et la photo « rootphoto1 » sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="cb04a-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="cb04a-155">Vous pouvez utiliser hello **instanceof** opérateur toodistinguish ces objets.</span><span class="sxs-lookup"><span data-stu-id="cb04a-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="cb04a-156">Si vous le souhaitez, vous pouvez passer dans les paramètres toohello **listBlobs** méthode avec hello **useFlatBlobListing** paramètre la valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="cb04a-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="cb04a-157">Cela permet de renvoyer chaque objet blob, indépendamment du répertoire.</span><span class="sxs-lookup"><span data-stu-id="cb04a-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="cb04a-158">Pour plus d’informations, consultez **CloudBlobContainer.listBlobs** Bonjour [référence de kit de développement logiciel Azure Storage Client].</span><span class="sxs-lookup"><span data-stu-id="cb04a-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="cb04a-159">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="cb04a-159">Download a blob</span></span>
<span data-ttu-id="cb04a-160">objets BLOB toodownload, suivez hello même étapes comme vous l’avez fait pour le chargement d’un objet blob dans l’ordre tooget une référence d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="cb04a-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="cb04a-161">Bonjour télécharger l’exemple, vous avez appelé téléchargement sur l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="cb04a-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="cb04a-162">Dans l’exemple suivant de hello, appelez téléchargement tootransfer hello contenu tooa flux de données objet blob comme un **FileOutputStream** que vous pouvez utiliser le fichier local de tooa toopersist hello blob.</span><span class="sxs-lookup"><span data-stu-id="cb04a-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="cb04a-163">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="cb04a-163">Delete a blob</span></span>
<span data-ttu-id="cb04a-164">toodelete un objet blob, obtenir un objet blob de référence et appelez **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="cb04a-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="cb04a-165">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="cb04a-165">Delete a blob container</span></span>
<span data-ttu-id="cb04a-166">Enfin, toodelete un conteneur d’objets blob, obtenir un objet blob de référence de conteneur, puis appelez **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="cb04a-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cb04a-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb04a-167">Next steps</span></span>
<span data-ttu-id="cb04a-168">Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="cb04a-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="cb04a-169">[Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="cb04a-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="cb04a-170">[référence de kit de développement logiciel Azure Storage Client][référence de kit de développement logiciel Azure Storage Client]</span><span class="sxs-lookup"><span data-stu-id="cb04a-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="cb04a-171">[API REST Stockage Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="cb04a-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="cb04a-172">[Blog de l’équipe Stockage Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="cb04a-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="cb04a-173">Pour plus d’informations, consultez également hello [centre de développement Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="cb04a-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[référence de kit de développement logiciel Azure Storage Client]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
