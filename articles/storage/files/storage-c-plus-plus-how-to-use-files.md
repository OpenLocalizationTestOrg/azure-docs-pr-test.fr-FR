---
title: aaaDevelop pour le stockage de fichiers Azure avec C++ | Documents Microsoft
description: "Découvrez comment toodevelop C++ applications et services qui utilisent des fichiers Azure storage toostore fichier de données."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Développer pour le stockage de fichiers Azure avec C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>À propos de ce didacticiel

Dans ce didacticiel, vous allez apprendre comment tooperform les opérations de base sur le stockage de fichiers Azure. Via exemples écrits en C++, vous allez apprendre comment toocreate partage et de répertoires, télécharger, liste et supprimer des fichiers. Si vous êtes de nouveau stockage de fichier tooAzure, traverser des concepts hello dans les sections hello qui suivent sera utile pour comprendre les exemples hello.


* Créer et supprimer des partages de fichiers Azure
* Créer et supprimer des répertoires
* Énumérer des fichiers et répertoires dans un partage de fichiers Azure
* Charger, télécharger et supprimer un fichier
* Définir le quota de hello (taille maximale) pour un partage de fichiers Azure
* Créer une signature d’accès partagé (clé SAS) pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage de hello.

> [!Note]  
> Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des fonctions et classes C++ d’e/s standards de hello. Cet article décrit comment toowrite les applications qui utilisent hello SDK Azure Storage C++, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.

## <a name="create-a-c-application"></a>Création d’une application C++
exemples de hello toobuild, vous devez tooinstall hello bibliothèque cliente de stockage Azure 2.4.0 pour C++. Vous devez également avoir préalablement créé un compte de stockage Azure.

tooinstall hello Client de stockage Azure 2.4.0 pour C++, vous pouvez utiliser une des méthodes suivantes de hello :

* **Linux :** suivez instructions hello de hello [bibliothèque cliente de stockage Azure pour C++ Lisez-moi](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.
* **Windows :** dans Visual Studio, cliquez sur **Outils &gt; Gestionnaire de package NuGet &gt; Console du gestionnaire de package**. Tapez ce qui suit hello commande dans hello [console du Gestionnaire de Package NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) et appuyez sur **entrée**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurer votre toouse application stockage Azure
Ajouter suivant de hello inclure haut de toohello instructions du fichier source de hello C++ où vous souhaitez le stockage de fichiers Azure toomanipulate :

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuration d’une chaîne de connexion au stockage Azure
toouse stockage de fichiers, vous avez besoin de compte de stockage Azure tooconnect tooyour. Hello première étape serait tooconfigure une chaîne de connexion, que nous allons utiliser compte de stockage tooconnect tooyour. Nous allons définir une toodo variable statique qui.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Connexion de compte de stockage Azure tooan
Vous pouvez utiliser hello **cloud_storage_account** classe toorepresent vos informations de compte de stockage. tooretrieve plus d’informations à partir de la chaîne de connexion de stockage hello du compte de votre stockage, vous pouvez utiliser hello **analyser** (méthode).

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Création d’un partage de fichiers Azure
Tous les fichiers et répertoires d’un stockage de fichiers Azure se trouvent dans un conteneur appelé **Partage**. Votre compte de stockage peut avoir autant de partages que le permet la capacité de votre compte. partage de tooa accès tooobtain et son contenu, vous devez toouse un client de stockage de fichiers Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

À l’aide du client de stockage de fichier Azure hello, vous pouvez ensuite obtenir un partage de tooa de référence.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

partage de hello toocreate, utilisez hello **create_if_not_exists** méthode Hello **cloud_file_share** objet.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

À ce stade, **partager** contient un partage de tooa référence nommé **mon exemple-partage**.

## <a name="delete-an-azure-file-share"></a>Suppression d’un partage de fichiers Azure
Suppression d’un partage est effectuée en appelant hello **delete_if_exists** méthode sur un objet cloud_file_share. Voici un exemple de code permettant d’effectuer cette opération.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Créer un répertoire
Vous pouvez organiser le stockage en plaçant les fichiers à l’intérieur des sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello. Stockage de fichier Azure vous permet de toocreate car autorise de nombreux répertoires car votre compte. code Hello ci-dessous crée un répertoire nommé **répertoire Mes exemple** sous le répertoire racine de hello ainsi que d’un sous-répertoire nommé **mon exemple-sous-répertoire**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Supprimer un répertoire
La suppression d’un répertoire est une tâche simple, mais il convient de noter que vous ne pouvez pas supprimer de répertoire contenant des fichiers ou d’autres répertoires.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Énumérer des fichiers et répertoires dans un partage de fichiers Azure
Il est facile d’obtenir la liste de fichiers et de répertoires d’un partage en appelant **list_files_and_directories** sur une référence **cloud_file_directory**. tooaccess hello ensemble complet des propriétés et méthodes pour retourné **list_file_and_directory_item**, vous devez appeler hello **list_file_and_directory_item.as_file** méthode tooget un **cloud_ fichier** objet ou hello **list_file_and_directory_item.as_directory** méthode tooget un **cloud_file_directory** objet.

Hello suivant de code montre comment tooretrieve et sortie hello URI de chaque élément dans le répertoire racine de hello du partage de hello.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Charger un fichier
À hello très moins, un partage de fichiers Azure contient un répertoire racine où les fichiers peuvent résider. Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.

première étape de Hello lors du téléchargement d’un fichier est tooobtain un répertoire toohello de référence où elle doit résider. Pour ce faire, l’appelant hello **get_root_directory_reference** méthode d’objet de partage hello.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Maintenant que vous avez un répertoire de racine référence toohello du partage de hello, vous pouvez télécharger un fichier sur lui. Cet exemple télécharge à partir d’un fichier, d’un texte et d’un flux.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Téléchargement d’un fichier
les fichiers toodownload, tout d’abord extraire une référence de fichier et appelez ensuite hello **download_to_stream** méthode tootransfer hello fichier contenu tooa objet de flux, ce qui vous pouvez alors être conservées tooa des fichiers locaux. Vous pouvez également utiliser hello **download_to_file** contenu de hello méthode toodownload d’un fichier local tooa. Vous pouvez utiliser hello **download_text** contenu de hello méthode toodownload d’un fichier comme une chaîne de texte.

exemple Hello utilise hello **download_to_stream** et **download_text** toodemonstrate méthodes téléchargement de fichiers hello, qui ont été créées dans les sections précédentes.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Supprimer un fichier
La suppression de fichiers est également une opération courante liée au stockage des fichiers Azure. Hello de code suivant supprime un fichier nommé my-exemple-fichier-3 stocké sous le répertoire racine de hello.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Définir le quota de hello (taille maximale) pour un partage de fichiers Azure
Vous pouvez définir le quota de hello (ou la taille maximale) pour un partage de fichiers, en gigaoctets. Vous pouvez également vérifier toosee la quantité de données est actuellement stocké sur le partage de hello.

En définissant le quota de hello pour un partage, vous pouvez limiter la taille totale de hello hello les fichiers stockés sur le partage de hello. Si hello la taille totale des fichiers sur le partage de hello dépasse quota de hello défini sur le partage de hello, les clients seront taille de hello tooincrease impossible des fichiers existants ou créer de nouveaux fichiers, à moins que ces fichiers sont vides.

exemple Hello ci-dessous montre comment toocheck hello en cours d’utilisation pour un partage et comment tooset hello quota pour le partage de hello.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers
Vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier individuel. Vous pouvez également créer une stratégie d’accès partagé sur un toomanage partagé accès au partage de fichier signatures. Création d’une stratégie d’accès partagé est recommandée, car elle fournit un moyen de révocation hello SAS si elle doit être compromise.

Bonjour à l’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise que tooprovide hello les contraintes de stratégie pour une SAP sur un fichier dans hello partagent.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le stockage Azure, Explorez ces ressources :

* [Bibliothèque cliente de stockage pour C++](https://github.com/Azure/azure-storage-cpp)
* [Exemples de service de fichier de Stockage Azure en C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Storage Explorer](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Documentation d'Azure Storage](https://azure.microsoft.com/documentation/services/storage/)