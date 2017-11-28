---
title: "Utilisation du stockage d’objets blob à partir de PHP | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4b68844c5d0553eaede3997bf09bff4fe570e850
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="4ab7d-103">Utilisation du stockage d’objets blob à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="4ab7d-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4ab7d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4ab7d-104">Overview</span></span>
<span data-ttu-id="4ab7d-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="4ab7d-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="4ab7d-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="4ab7d-108">Ce guide décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="4ab7d-109">Les exemples sont écrits en PHP et utilisent le [Kit de développement logiciel (SDK) Azure pour PHP][download].</span><span class="sxs-lookup"><span data-stu-id="4ab7d-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="4ab7d-110">Les scénarios traités incluent le **chargement**, l’**énumération**, le **téléchargement** et la **suppression** d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="4ab7d-111">Pour plus d’informations sur les objets blob, consultez la section [Étapes suivantes](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="4ab7d-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="4ab7d-112">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="4ab7d-112">Create a PHP application</span></span>
<span data-ttu-id="4ab7d-113">Le référencement de classes issues du Kit de développement logiciel (SDK) Azure pour PHP dans votre code constitue la seule exigence pour créer une application PHP qui accède au service blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="4ab7d-114">Vous pouvez utiliser tous les outils de développement pour créer votre application, y compris Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="4ab7d-115">Dans ce guide, vous allez utiliser des fonctionnalités de service qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="4ab7d-116">Obtention des bibliothèques clientes Azure</span><span class="sxs-lookup"><span data-stu-id="4ab7d-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="4ab7d-117">Configuration de votre application pour accéder au service blob</span><span class="sxs-lookup"><span data-stu-id="4ab7d-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="4ab7d-118">Pour utiliser des API de service blob Azure, vous devez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="4ab7d-119">référencer le fichier de chargeur automatique à l’aide de l’instruction [require_once] ; et</span><span class="sxs-lookup"><span data-stu-id="4ab7d-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="4ab7d-120">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-120">Reference any classes you might use.</span></span>

<span data-ttu-id="4ab7d-121">L'exemple suivant montre comment inclure le fichier du chargeur automatique et référencer la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="4ab7d-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="4ab7d-122">Les exemples de cet article partent du principe que vous avez installé les bibliothèques clientes PHP pour Azure via Composer.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="4ab7d-123">Si vous avez installé les bibliothèques manuellement, vous devez référencer le fichier de chargeur automatique `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="4ab7d-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="4ab7d-124">Dans les exemples ci-dessous, l’instruction `require_once` s’affiche toujours, mais seules les classes nécessaires à l’exécution de l’exemple sont référencées.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="4ab7d-125">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4ab7d-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="4ab7d-126">Pour instancier un client de service blob Azure, vous devez disposer d’une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="4ab7d-127">Le format de la chaîne de connexion du service Blob est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="4ab7d-128">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="4ab7d-129">Pour accéder à l’émulateur de stockage :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="4ab7d-130">Pour créer un client de service Azure, vous devez utiliser la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="4ab7d-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="4ab7d-131">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-131">You can:</span></span>

* <span data-ttu-id="4ab7d-132">lui transmettre directement la chaîne de connexion ; ou</span><span class="sxs-lookup"><span data-stu-id="4ab7d-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="4ab7d-133">utiliser **CloudConfigurationManager (CCM)** pour vérifier plusieurs sources externes pour la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="4ab7d-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="4ab7d-134">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="4ab7d-135">Vous pouvez ajouter de nouvelles sources via une extension de la classe **ConnectionStringSource** .</span><span class="sxs-lookup"><span data-stu-id="4ab7d-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="4ab7d-136">Dans les exemples ci-dessous, la chaîne de connexion est passée directement.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="4ab7d-137">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="4ab7d-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="4ab7d-138">Un objet **BlobRestProxy** vous permet de créer un conteneur d’objets blob avec la méthode **createContainer**.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="4ab7d-139">Lors de la création d'un conteneur, vous pouvez définir des options sur ce dernier, mais vous n'y êtes pas obligé.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="4ab7d-140">(L’exemple ci-dessous montre comment définir la liste de contrôle d’accès (ACL) et les métadonnées du conteneur.)</span><span class="sxs-lookup"><span data-stu-id="4ab7d-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="4ab7d-141">L’appel de **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** rend le conteneur et les données d’objets blob accessibles via des demandes anonymes.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="4ab7d-142">L’appel de **setPublicAccess(PublicAccessType::BLOBS_ONLY)** ne rend que les données d’objets blob accessibles via des demandes anonymes.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="4ab7d-143">Pour plus d’informations sur les ACL de conteneur, consultez la page [Définition d’ACL de conteneur (API REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="4ab7d-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="4ab7d-144">Pour plus d’informations sur les codes d’erreur des services d’objets blob, consultez la page [Codes d’erreur de service BLOB][error-codes].</span><span class="sxs-lookup"><span data-stu-id="4ab7d-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4ab7d-145">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="4ab7d-145">Upload a blob into a container</span></span>
<span data-ttu-id="4ab7d-146">Pour télécharger un fichier en tant qu’objet blob, utilisez la méthode **BlobRestProxy->createBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="4ab7d-147">Si l’objet blob n’existe pas, cette opération le crée. S’il existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="4ab7d-148">L’exemple de code ci-dessous part du principe que le conteneur a déjà été créé et utilise [fopen][fopen] pour ouvrir le fichier en tant que flux.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="4ab7d-149">Notez que l’exemple ci-dessus télécharge un objet blob en tant que flux.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="4ab7d-150">Toutefois, un objet blob peut également être téléchargé en tant que chaîne à l’aide de la fonction [file\_get\_contents][file_get_contents] par exemple.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="4ab7d-151">Pour ce faire, utilisez l’exemple précédent et remplacez `$content = fopen("c:\myfile.txt", "r");` par `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="4ab7d-152">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="4ab7d-152">List the blobs in a container</span></span>
<span data-ttu-id="4ab7d-153">Pour répertorier les objets blob dans un conteneur, utilisez la méthode **BlobRestProxy->listBlobs** avec une boucle **foreach** pour lire en boucle le résultat.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="4ab7d-154">Le code suivant affiche le nom de chaque objet blob dans un conteneur et son URI dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="4ab7d-155">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="4ab7d-155">Download a blob</span></span>
<span data-ttu-id="4ab7d-156">Pour télécharger un objet blob, appelez la méthode **BlobRestProxy->getBlob**, puis la méthode **getContentStream** sur l’objet **GetBlobResult** résultant.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="4ab7d-157">Notez que l'exemple ci-dessus télécharge un objet blob en tant que ressource de flux (comportement par défaut).</span><span class="sxs-lookup"><span data-stu-id="4ab7d-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="4ab7d-158">Toutefois, vous pouvez utiliser la fonction [stream\_get\_contents][stream-get-contents] pour convertir le flux renvoyé en chaîne.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="4ab7d-159">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="4ab7d-159">Delete a blob</span></span>
<span data-ttu-id="4ab7d-160">Pour supprimer un objet blob, passez le nom du conteneur et le nom de l’objet blob à **BlobRestProxy->deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="4ab7d-161">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="4ab7d-161">Delete a blob container</span></span>
<span data-ttu-id="4ab7d-162">Enfin, pour supprimer un conteneur d’objets blob, passez le nom du conteneur à **BlobRestProxy->deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="4ab7d-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ab7d-163">Next steps</span></span>
<span data-ttu-id="4ab7d-164">Maintenant que vous connaissez les principes de base du service blob Azure, suivez ces liens pour apprendre à exécuter les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="4ab7d-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="4ab7d-165">Consultez le [Blog de l'équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="4ab7d-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="4ab7d-166">Consultez [l’exemple d’objet blob de blocs PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="4ab7d-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="4ab7d-167">Consultez [l’exemple d’objet blob de pages PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="4ab7d-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="4ab7d-168">Transfert de données avec l'utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="4ab7d-168">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="4ab7d-169">Pour plus d’informations, consultez également le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4ab7d-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
