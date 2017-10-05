---
title: "Utilisation du stockage d’objets blob Azure à partir de Java | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
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
ms.openlocfilehash: b8a4eca600b458802a7a23851bb80ea4da2664ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="5dbaf-103">Utilisation du stockage d'objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="5dbaf-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="5dbaf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5dbaf-104">Overview</span></span>
<span data-ttu-id="5dbaf-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="5dbaf-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5dbaf-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="5dbaf-108">Cet article décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de stockage d’objets blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="5dbaf-109">Les exemples sont écrits en Java et utilisent le [Kit de développement logiciel (SDK) Stockage Azure pour Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5dbaf-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="5dbaf-110">Les scénarios traités incluent le **chargement**, l’**énumération**, le **téléchargement** et la **suppression** d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="5dbaf-111">Pour plus d'informations sur les objets blob, consultez la section [Étapes suivantes](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="5dbaf-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="5dbaf-112">un Kit de développement logiciel (SDK) est disponible pour les développeurs qui utilisent Azure Storage sur des appareils Android.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="5dbaf-113">Pour plus d’informations, consultez la page [Kit de développement logiciel (SDK) Stockage Azure pour Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="5dbaf-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="5dbaf-114">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="5dbaf-114">Create a Java application</span></span>
<span data-ttu-id="5dbaf-115">Dans cet article, vous allez utiliser des fonctionnalités de stockage qui peuvent être exécutées dans une application Java en local ou dans le code d’un rôle Web ou d’un rôle de travail dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="5dbaf-116">Pour ce faire, vous devez installer le Kit de développement Java (JDK) et créer un compte Azure Storage dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="5dbaf-117">Vous devez ensuite vérifier que votre système de développement répond à la configuration minimale requise et aux dépendances répertoriées dans le référentiel [Kit de développement logiciel (SDK) Stockage Azure pour Java][Azure Storage SDK for Java] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="5dbaf-118">Si tel est le cas, vous pouvez suivre les instructions relatives au téléchargement et à l'installation des bibliothèques Azure Storage pour Java sur votre système à partir du référentiel.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="5dbaf-119">Une fois ces tâches effectuées, vous pouvez créer une application Java utilisant les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="5dbaf-120">Configurer votre application pour accéder au stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="5dbaf-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="5dbaf-121">Ajoutez les instructions d’importation suivantes au début du fichier Java dans lequel vous voulez utiliser des API de stockage Azure pour accéder aux objets blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="5dbaf-122">Configurer une chaîne de connexion au stockage Azure</span><span class="sxs-lookup"><span data-stu-id="5dbaf-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="5dbaf-123">Un client de stockage Azure utilise une chaîne de connexion au stockage pour stocker des points de terminaison et des informations d’identification permettant d’accéder aux services de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="5dbaf-124">Lors de l’exécution dans une application cliente, vous devez spécifier la chaîne de connexion au stockage au format suivant, en indiquant le nom de votre compte de stockage et sa clé d’accès primaire, correspondant aux valeurs *AccountName* et *AccountKey*, sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5dbaf-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="5dbaf-125">Cet exemple montre comment déclarer un champ statique pour qu’il contienne la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="5dbaf-126">Dans une application exécutée au sein d'un rôle dans Microsoft Azure, cette chaîne peut être stockée dans le fichier de configuration de service *ServiceConfiguration.cscfg*et elle est accessible en appelant la méthode **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="5dbaf-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="5dbaf-127">L’exemple suivant récupère la chaîne de connexion auprès d’un élément **Setting** nommé *StorageConnectionString* dans le fichier de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="5dbaf-128">Les exemples ci-dessous partent du principe que vous avez utilisé l’une de ces deux méthodes pour obtenir la chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="5dbaf-129">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="5dbaf-129">Create a container</span></span>
<span data-ttu-id="5dbaf-130">Un objet **CloudBlobClient** vous permet d’obtenir les objets de référence des conteneurs et objets blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="5dbaf-131">Le code suivant crée un objet **CloudBlobClient** .</span><span class="sxs-lookup"><span data-stu-id="5dbaf-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="5dbaf-132">D’autres méthodes permettent de créer des objets **CloudStorageAccount**. Pour plus d’informations, consultez la section **CloudStorageAccount** dans la page [Référence du Kit de développement logiciel (SDK) du client Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="5dbaf-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5dbaf-133">Utilisez l’objet **CloudBlobClient** pour obtenir une référence pointant vers le conteneur à utiliser.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="5dbaf-134">Si le conteneur n’existe pas, vous pouvez le créer en utilisant la méthode **createIfNotExists** ; sinon, le conteneur existant est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="5dbaf-135">Par défaut, le nouveau conteneur est privé. Vous devez donc indiquer votre clé d’accès au stockage (comme précédemment) pour télécharger des objets blob depuis ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="5dbaf-136">Optionnel : configuration d’un conteneur pour un accès public</span><span class="sxs-lookup"><span data-stu-id="5dbaf-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="5dbaf-137">Par défaut, les autorisations d’un conteneur sont configurées pour un accès privé. Cependant, vous pouvez aisément les configurer pour permettre un accès public en lecture seule pour tous les internautes :</span><span class="sxs-lookup"><span data-stu-id="5dbaf-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5dbaf-138">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="5dbaf-138">Upload a blob into a container</span></span>
<span data-ttu-id="5dbaf-139">Pour télécharger un fichier vers un objet blob, obtenez une référence de conteneur et utilisez-la pour obtenir une référence d'objet blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="5dbaf-140">Dès lors que vous disposez d'une référence d'objet blob, vous pouvez télécharger un flux vers cet objet.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="5dbaf-141">Si l'objet blob n'existe pas, cette opération entraîne sa création. S'il existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="5dbaf-142">Cet exemple de code illustre ce point, en supposant que le conteneur existe.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="5dbaf-143">Création d’une liste d’objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="5dbaf-143">List the blobs in a container</span></span>
<span data-ttu-id="5dbaf-144">Pour créer une liste d'objets blob dans un conteneur, commencez par obtenir une référence pointant vers un conteneur comme pour le téléchargement d'un objet blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="5dbaf-145">Vous pouvez utiliser la méthode **listBlobs** du conteneur avec une boucle **for**.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="5dbaf-146">Le code suivant génère l'URI de chaque objet blob d'un conteneur sur la console.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="5dbaf-147">Notez que les noms que vous attribuez aux objets blob peuvent inclure des informations de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="5dbaf-148">Vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="5dbaf-149">Notez que la structure de répertoires est uniquement virtuelle : les seules ressources disponibles dans le stockage d’objets blob sont des conteneurs et des objets blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="5dbaf-150">Toutefois, la bibliothèque cliente fournit un objet **CloudBlobDirectory** pour faire référence à un répertoire virtuel et simplifier le processus d’utilisation des objets blob organisés de cette façon.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="5dbaf-151">Par exemple, vous pouvez avoir un conteneur nommé « photos », dans lequel vous pouvez télécharger des objets blob nommés « rootphoto1 », « 2010/photo1 », « 2010/photo2 » et « 2011/photo1 ».</span><span class="sxs-lookup"><span data-stu-id="5dbaf-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="5dbaf-152">Vous créez ainsi virtuellement les répertoires « 2010 » et « 2011 » dans le conteneur « photos ».</span><span class="sxs-lookup"><span data-stu-id="5dbaf-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="5dbaf-153">Lorsque vous appelez la méthode **listBlobs** pour le conteneur « photos », la collection renvoyée contient les objets **CloudBlobDirectory** et **CloudBlob** qui représentent les répertoires et objets blob contenus au niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="5dbaf-154">Dans ce cas, les répertoires « 2010 » et « 2011 » et la photo « rootphoto1 » sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="5dbaf-155">Vous pouvez utiliser l'opérateur **instanceof** pour différencier ces objets.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="5dbaf-156">Vous pouvez également transmettre les paramètres à la méthode **listBlobs** avec le paramètre **useFlatBlobListing** défini sur true.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="5dbaf-157">Cela permet de renvoyer chaque objet blob, indépendamment du répertoire.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="5dbaf-158">Pour plus d’informations, consultez la section **CloudBlobContainer.listBlobs** dans la page [Référence du Kit de développement logiciel (SDK) du client Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="5dbaf-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="5dbaf-159">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="5dbaf-159">Download a blob</span></span>
<span data-ttu-id="5dbaf-160">Pour télécharger des objets blob, procédez comme pour le chargement d'un objet blob afin d'obtenir une référence d'objet blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="5dbaf-161">Dans l'exemple de chargement, vous avez appelé la méthode upload sur l'objet blob.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="5dbaf-162">Dans l'exemple suivant, appelez la méthode download pour transférer les contenus d'objets blob vers un objet de flux tel que **FileOutputStream** pouvant être utilisé pour rendre l'objet blob persistant dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="5dbaf-163">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="5dbaf-163">Delete a blob</span></span>
<span data-ttu-id="5dbaf-164">Pour supprimer un objet blob, obtenez une référence d'objet blob et appelez la méthode **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="5dbaf-165">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="5dbaf-165">Delete a blob container</span></span>
<span data-ttu-id="5dbaf-166">Enfin, pour supprimer un conteneur d’objets blob, obtenez sa référence, puis appelez la méthode **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="5dbaf-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5dbaf-167">Next steps</span></span>
<span data-ttu-id="5dbaf-168">Maintenant que vous connaissez les bases du stockage d’objets blob, consultez les liens suivants pour apprendre à exécuter des tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="5dbaf-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="5dbaf-169">[Kit de développement logiciel (SDK) Azure Storage pour Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="5dbaf-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="5dbaf-170">[Référence du Kit de développement logiciel (SDK) du client Azure Storage][Référence du Kit de développement logiciel (SDK) du client Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="5dbaf-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="5dbaf-171">[API REST Stockage Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="5dbaf-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="5dbaf-172">[Blog de l’équipe Stockage Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="5dbaf-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="5dbaf-173">Pour plus d’informations, consultez également le [Centre pour développeurs Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="5dbaf-173">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="5dbaf-174">[Référence du Kit de développement logiciel (SDK) du client Azure Storage]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="5dbaf-174">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
