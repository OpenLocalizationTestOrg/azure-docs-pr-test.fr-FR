---
title: aaaDevelop pour le stockage de fichiers Azure avec Python | Documents Microsoft
description: "Découvrez comment les applications Python toodevelop et les services qui utilisent des fichiers Azure storage toostore fichier des données."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Développer pour le stockage de fichiers Azure avec Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel va vous montrer des bases de hello de l’utilisation des applications de toodevelop Python ou services qui utilisent des données de fichier toostore fichier Azure storage. Dans ce didacticiel, nous crée une application console simple et montrent comment tooperform les actions de base avec le stockage de Python et des fichiers Azure :

* Créer des partages de fichiers Azure
* Créer des répertoires
* Énumérer des fichiers et répertoires dans un partage de fichiers Azure
* Charger, télécharger et supprimer un fichier

> [!Note]  
> Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des fonctions et des classes d’e/s de Python standards hello. Cet article décrit comment toowrite les applications qui utilisent hello SDK Azure Storage Python, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurer votre toouse application stockage Azure
Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier de source de Python dans lesquels vous souhaitez tooprogrammatically accès Azure Storage.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Configurer une connexion de tooAzure stockage de fichiers 
Hello `FileService` objet vous permet de travailler avec les partages, répertoires et fichiers. Hello de code suivant crée un `FileService` objet à l’aide de la clé de compte et le nom du compte de stockage hello. Remplacez `<myaccount>` et `<mykey>` par le nom et la clé de votre compte.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Création d’un partage de fichiers Azure
Bonjour exemple de code suivant, vous pouvez utiliser un `FileService` partage de hello toocreate objet si elle n’existe pas.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Créer un répertoire
Vous pouvez également organiser le stockage en plaçant les fichiers dans les sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello. Stockage de fichier Azure vous permet de toocreate car autorise de nombreux répertoires car votre compte. code Hello ci-dessous crée un sous-répertoire nommé **sampledir** sous le répertoire racine de hello.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Énumérer des fichiers et répertoires dans un partage de fichiers Azure
fichiers de hello toolist et des répertoires dans un partage, utilisez hello **liste\_répertoires\_et\_fichiers** (méthode). Cette méthode retourne un générateur. Hello de code suivant génère hello **nom** de chaque fichier et le répertoire dans une console toohello de partage.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Charger un fichier 
Fichier Azure partage contient de hello très moins, un répertoire racine où les fichiers peuvent résider. Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.

toocreate un fichier et les données de téléchargement, utilisez hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` méthodes. Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.

`create_file_from_path`téléchargements hello le contenu d’un fichier à partir du chemin d’accès spécifié hello, et `create_file_from_stream` téléchargements hello contenu à partir d’un flux de fichier/déjà ouvert. `create_file_from_bytes`télécharge un tableau d’octets, et `create_file_from_text` téléchargements hello spécifié la valeur de texte à l’aide de hello spécifié encodage (valeurs par défaut tooUTF-8).

exemple Hello télécharge contenu hello Hello **sunset.png** fichier hello **myfile** fichier.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Téléchargement d’un fichier
toodownload des données à partir d’un fichier, utilisez `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`. Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.

Hello exemple suivant montre comment utiliser `get_file_to_path` contenu de hello toodownload Hello **myfile** de fichier et le stocker toohello **hors-sunset.png** fichier.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Supprimer un fichier
Enfin, toodelete un fichier, appelez `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris comment toomanipulate stockage Azure files avec Python, suivez ces liens de toolearn plus.

* [Centre de développement Python](/develop/python/)
* [API REST des services d’Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Kit de développement logiciel (SDK) Microsoft Azure Storage pour Python](https://github.com/Azure/azure-storage-python)