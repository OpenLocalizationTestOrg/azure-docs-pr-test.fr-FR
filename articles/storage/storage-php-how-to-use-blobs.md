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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Comment toouse stockage d’objets blob à partir de PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Ce guide vous explique comment les scénarios courants tooperform hello Azure à l’aide de service d’objets blob. exemples de Hello sont écrits en PHP et utiliser hello [Azure SDK pour PHP][download]. Hello scénarios abordés incluent **téléchargement**, **liste**, **téléchargement**, et **suppression** objets BLOB. Pour plus d’informations sur les objets BLOB, consultez hello [étapes](#next-steps) section.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Création d'une application PHP
Hello uniquement requis pour la création d’une application PHP qui accède au service d’objets blob Azure hello est hello faisant référence à des classes Bonjour Azure SDK pour PHP à partir de votre code. Vous pouvez utiliser n’importe quel toocreate d’outils de développement de votre application, notamment le bloc-notes.

Dans ce guide, vous allez utiliser des fonctionnalités de service qui peuvent être appelées dans une application PHP localement ou dans le code d’un rôle web, d’un rôle de travail ou d’un site web Azure.

## <a name="get-hello-azure-client-libraries"></a>Obtenir les bibliothèques clientes Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Configurer le service blob d’applications tooaccess hello
toouse hello Azure API service blob, vous devez :

1. Fichier de chargeur automatique de hello référence à l’aide de hello [require_once] instruction, et
2. référencer toute classe que vous êtes susceptible d'utiliser.

Hello suivant montre comment tooinclude hello hello de référence et le fichier de chargeur automatique **ServicesBuilder** classe.

> [!NOTE]
> exemples Hello dans cet article supposent que vous avez installé hello PHP les bibliothèques clientes pour Azure via l’éditeur. Si vous avez installé les bibliothèques hello manuellement, vous devez tooreference hello `WindowsAzure.php` fichier de chargeur automatique.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Dans les exemples de hello ci-dessous, hello `require_once` instruction s’affiche toujours, mais uniquement les classes de hello nécessaires pour hello exemple tooexecute sont référencés.

## <a name="set-up-an-azure-storage-connection"></a>Configuration d’une connexion de stockage Azure
tooinstantiate un client du service blob Azure, vous devez avoir une chaîne de connexion valide. format de Hello de chaîne de connexion de service blob hello est :

Pour accéder à un service en ligne :

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Pour accéder à l’émulateur de stockage hello :

```php
UseDevelopmentStorage=true
```

toocreate n’importe quel client de service Azure, vous devez toouse hello **ServicesBuilder** classe. Vous pouvez :

* passer hello connexion chaîne directement tooit ou
* Utilisez hello **CloudConfigurationManager (CCM)** toocheck externe de plusieurs sources pour la chaîne de connexion hello :
  * Par défaut, il prend en charge une source externe : les variables d’environnement.
  * Vous pouvez ajouter de nouvelles sources en étendant hello **ConnectionStringSource** classe.

Pour obtenir des exemples hello décrites ici, la chaîne de connexion hello sera passé directement.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Créez un conteneur.
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** objet vous permet de créer un conteneur d’objets blob par hello **createContainer** (méthode). Lorsque vous créez un conteneur, vous pouvez définir des options sur le conteneur de hello, mais cela n’est pas requis. (exemple hello ci-dessous indique comment le conteneur de hello tooset accéder à la liste de contrôle (ACL) et les métadonnées de conteneur).

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

Appel de **setPublicAccess (PublicAccessType::CONTAINER\_AND\_objets BLOB)** rend hello conteneur et les données blob accessibles via des requêtes anonymes. L’appel de **setPublicAccess(PublicAccessType::BLOBS_ONLY)** ne rend que les données d’objets blob accessibles via des demandes anonymes. Pour plus d’informations sur les ACL de conteneur, consultez la page [Définition d’ACL de conteneur (API REST)][container-acl].

Pour plus d’informations sur les codes d’erreur des services d’objets blob, consultez la page [Codes d’erreur de service BLOB][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
tooupload un fichier sous la forme d’un objet blob, utilisez hello **BlobRestProxy -> createBlockBlob** (méthode). Cette opération crée les objets blob de hello si elle n’existe pas ou elle remplace dans ce cas. Hello exemple de code ci-dessous suppose que le conteneur de hello a déjà été créé et qu’il utilise [fopen] [ fopen] fichier de hello tooopen sous forme de flux.

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

Notez que hello précédent exemple télécharge un objet blob en tant que flux. Toutefois, un objet blob peut également être téléchargé sous forme de chaîne à l’aide, par exemple, hello [fichier\_obtenir\_contenu] [ file_get_contents] (fonction). toodo cette hello précédent exemple, de modifier `$content = fopen("c:\myfile.txt", "r");` trop`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, utilisez hello **BlobRestProxy -> listBlobs** méthode avec un **foreach** tooloop via le résultat de hello en boucle. Hello de code suivant affiche le nom hello de chaque objet blob en tant que sortie dans un conteneur et affiche son navigateur toohello URI.

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

## <a name="download-a-blob"></a>Téléchargement d’un objet blob
toodownload un objet blob, appel hello **BlobRestProxy -> getBlob** (méthode), puis appel hello **getContentStream** méthode hello résultant **GetBlobResult** objet.

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

Notez que cet exemple hello ci-dessus Obtient un objet blob sous la forme d’une ressource de flux de données (comportement par défaut de hello). Toutefois, vous pouvez utiliser hello [flux\_obtenir\_contenu] [ stream-get-contents] hello tooconvert de fonction a retourné une chaîne tooa de flux de données.

## <a name="delete-a-blob"></a>Supprimer un objet blob
toodelete un objet blob, passez le nom du conteneur hello et nom d’objet blob trop**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Suppression d’un conteneur d’objets blob
Enfin, toodelete un conteneur d’objets blob, passez nom du conteneur hello trop**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello Hello service blob Azure, suivez ces toolearn des liens sur les tâches de stockage plus complexes.

* Visitez hello [blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Consultez hello [exemple blob de bloc PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Consultez hello [exemple d’objet blob PHP page](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)

Pour plus d’informations, consultez également hello [centre de développement PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
