---
title: "stockage d’objets blob aaaHow toouse (stockage d’objets) à partir de PHP | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
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
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="ad2e5-103">Comment toouse stockage d’objets blob à partir de PHP</span><span class="sxs-lookup"><span data-stu-id="ad2e5-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ad2e5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ad2e5-104">Overview</span></span>
<span data-ttu-id="ad2e5-105">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ad2e5-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ad2e5-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ad2e5-108">Ce guide vous explique comment les scénarios courants tooperform hello Azure à l’aide de service d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="ad2e5-109">exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP][download].</span><span class="sxs-lookup"><span data-stu-id="ad2e5-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="ad2e5-110">Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="ad2e5-111">Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="ad2e5-112">Création d'une application PHP</span><span class="sxs-lookup"><span data-stu-id="ad2e5-112">Create a PHP application</span></span>
<span data-ttu-id="ad2e5-113">Hello uniquement requis pour la création d’une application PHP qui accède au service d’objets blob Azure hello est hello faisant référence à des classes Bonjour Azure SDK pour PHP à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="ad2e5-114">Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="ad2e5-115">Dans ce guide, vous allez utiliser des fonctionnalités de service qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="ad2e5-116">Obtenir les bibliothèques clientes Azure hello</span><span class="sxs-lookup"><span data-stu-id="ad2e5-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="ad2e5-117">Configurer le service blob d’applications tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="ad2e5-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="ad2e5-118">toouse hello Azure API service blob, vous devez :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="ad2e5-119">Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] instruction, et</span><span class="sxs-lookup"><span data-stu-id="ad2e5-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="ad2e5-120">référencer toute classe que vous êtes susceptible d'utiliser.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-120">Reference any classes you might use.</span></span>

<span data-ttu-id="ad2e5-121">Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="ad2e5-122">exemples Hello dans cet article supposent que vous avez installé hello PHP les bibliothèques clientes pour Azure via l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="ad2e5-123">Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello `WindowsAzure.php` fichier de chargeur automatique.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="ad2e5-124">Dans les exemples de hello ci-dessous, hello `require_once` instruction s’affiche toujours, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ad2e5-125">Configuration d’une connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ad2e5-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="ad2e5-126">tooinstantiate un client du service blob Azure, vous devez avoir une chaîne de connexion valide.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="ad2e5-127">format de Hello de chaîne de connexion de service blob hello est :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="ad2e5-128">Pour accéder à un service en ligne :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="ad2e5-129">Pour accéder à l’émulateur de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="ad2e5-130">toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="ad2e5-131">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-131">You can:</span></span>

* <span data-ttu-id="ad2e5-132">passer hello connexion chaîne directement tooit ou</span><span class="sxs-lookup"><span data-stu-id="ad2e5-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="ad2e5-133">Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="ad2e5-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="ad2e5-134">Par défaut, il prend en charge une source externe : les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="ad2e5-135">Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="ad2e5-136">Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="ad2e5-137">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ad2e5-138">A **BlobRestProxy** objet vous permet de créer un conteneur d’objets blob par hello **createContainer** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="ad2e5-139">Lorsque vous créez un conteneur, vous pouvez définir des options sur le conteneur de hello, mais cela n’est pas requis.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="ad2e5-140">(exemple hello ci-dessous indique comment le conteneur de hello tooset accéder à la liste de contrôle (ACL) et les métadonnées de conteneur).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="ad2e5-141">Appel de **setPublicAccess (PublicAccessType::CONTAINER\_AND\_objets BLOB)** rend hello conteneur et les données blob accessibles via des requêtes anonymes.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="ad2e5-142">L’appel de **setPublicAccess(PublicAccessType::BLOBS_ONLY)** ne rend que les données d’objets blob accessibles via des demandes anonymes.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="ad2e5-143">Pour plus d’informations sur les ACL de conteneur, consultez la page [Définition d’ACL de conteneur (API REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="ad2e5-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="ad2e5-144">Pour plus d’informations sur les codes d’erreur des services d’objets blob, consultez la page [Codes d’erreur de service BLOB][error-codes].</span><span class="sxs-lookup"><span data-stu-id="ad2e5-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ad2e5-145">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="ad2e5-145">Upload a blob into a container</span></span>
<span data-ttu-id="ad2e5-146">tooupload un fichier sous la forme d’un objet blob, utilisez hello **BlobRestProxy -> createBlockBlob** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="ad2e5-147">Cette opération crée les objets blob de hello si elle n’existe pas ou elle remplace dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="ad2e5-148">Hello exemple de code ci-dessous suppose que le conteneur de hello a déjà été créé et qu’il utilise [fopen] [ fopen] fichier de hello tooopen sous forme de flux.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="ad2e5-149">Notez que hello précédent exemple télécharge un objet blob en tant que flux.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="ad2e5-150">Toutefois, un objet blob peut également être téléchargé sous forme de chaîne à l’aide, par exemple, hello [fichier\_obtenir\_contenu] [ file_get_contents] (fonction).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="ad2e5-151">toodo cette hello précédent exemple, de modifier `$content = fopen("c:\myfile.txt", "r");` trop`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ad2e5-152">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="ad2e5-152">List hello blobs in a container</span></span>
<span data-ttu-id="ad2e5-153">objets BLOB de hello toolist dans un conteneur, utilisez hello **BlobRestProxy -> listBlobs** méthode avec un **foreach** tooloop via le résultat de hello en boucle.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="ad2e5-154">Hello de code suivant affiche le nom hello de chaque objet blob en tant que sortie dans un conteneur et affiche son navigateur toohello URI.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="ad2e5-155">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="ad2e5-155">Download a blob</span></span>
<span data-ttu-id="ad2e5-156">toodownload un objet blob, appel hello **BlobRestProxy -> getBlob** (méthode), puis appel hello **getContentStream** méthode hello résultant **GetBlobResult** objet.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="ad2e5-157">Notez que cet exemple hello ci-dessus Obtient un objet blob sous la forme d’une ressource de flux de données (comportement par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="ad2e5-158">Toutefois, vous pouvez utiliser hello [flux\_obtenir\_contenu] [ stream-get-contents] hello tooconvert de fonction a retourné une chaîne tooa de flux de données.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="ad2e5-159">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="ad2e5-159">Delete a blob</span></span>
<span data-ttu-id="ad2e5-160">toodelete un objet blob, passez le nom du conteneur hello et nom d’objet blob trop**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="ad2e5-161">Suppression d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="ad2e5-161">Delete a blob container</span></span>
<span data-ttu-id="ad2e5-162">Enfin, toodelete un conteneur d’objets blob, passez nom du conteneur hello trop**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ad2e5-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad2e5-163">Next steps</span></span>
<span data-ttu-id="ad2e5-164">Maintenant que vous avez appris les notions de base de hello Hello service blob Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="ad2e5-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="ad2e5-165">Visitez hello [blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="ad2e5-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="ad2e5-166">Consultez hello [exemple blob de bloc PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="ad2e5-167">Consultez hello [exemple d’objet blob PHP page](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="ad2e5-168">Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello</span><span class="sxs-lookup"><span data-stu-id="ad2e5-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="ad2e5-169">Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ad2e5-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
